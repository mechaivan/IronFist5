# Investigación profunda: PS2Recomp

Ver hallazgos asociados: TK5-0005, TK5-0006, TK5-0007, TK5-0013, TK5-0017.

Fuente principal inspeccionada directamente: `https://github.com/ran-j/PS2Recomp`
(README leído completo, commit visible `c5a9d02`, 30 de septiembre de 2026).
También se consultó el fork `https://github.com/ej-sanmartin/ps2recomp`.

## Qué es

PS2Recomp es un **recompilador estático experimental**: traduce un binario
ELF de PS2 a código C++ que, compilado con un compilador moderno (C++20) y
enlazado contra un runtime propio (`ps2xRuntime`), puede ejecutarse en un
PC sin un emulador de instrucción-a-instrucción tradicional. Está
licenciado bajo **GPL-3.0**.

Explícitamente se inspira en `N64Recomp` (ver TK5-0013), adaptando la idea
a la arquitectura, mucho más compleja, de PS2.

## Arquitectura / módulos

| Módulo | Responsabilidad |
|---|---|
| `ps2xAnalyzer` | Escanea el ELF y genera una configuración TOML inicial (funciones candidatas, stubs sugeridos, skips). |
| `ps2xRecomp` | Lee ELF + TOML, desensambla instrucciones R5900 función por función, y emite C++. |
| `ps2xRuntime` | Runtime de ejecución: memoria de invitado (guest memory), tabla de despacho de funciones, manejo de syscalls, stubs de GS/VU/sistema de archivos. |
| `ps2xIOP` | Ejecución de módulos IRX del IOP (R3000A) mediante un kernel IOP virtual con HLE genérico de respaldo. |
| `ps2xStudio`, `ps2xTest` | Herramientas de soporte y pruebas (no se ha inspeccionado su contenido en detalle en esta pasada). |

## Proceso de recompilación, paso a paso (según el README)

1. **Parseo del ELF**: usa la librería `ELFIO` para leer el ELF de PS2 y
   extraer funciones, símbolos, y relocaciones.
2. **Identificación de funciones**: el flujo recomendado es exportar un
   mapa de funciones desde **Ghidra** (CSV/TOML, parámetro
   `general.ghidra_output`) en vez de confiar solo en `ps2xAnalyzer`,
   especialmente en binarios retail sin símbolos de depuración. Esto es
   explícito en el propio README: "Before manual binding, prefer
   recompilation from a Ghidra-exported TOML/CSV first. The extra
   boundaries and synthetic entry points are usually more important than
   manual early triage."
3. **Decodificación de instrucciones R5900**: incluye MMI (Multimedia
   Instructions, las SIMD de 128 bits propias de la EE) y VU0 en **modo
   macro** (es decir, cuando el programa principal de la EE emite
   instrucciones de VU0 como coprocesador, no el modo "micro" en el que
   VU0/VU1 ejecutan su propio microprograma independiente).
4. **Traducción literal a C++**: cada instrucción MIPS se traduce a una
   operación C++ equivalente sobre una estructura de contexto de registros.
   Ejemplo citado textualmente en el README: `addiu $r4, $r4, 0x20` →
   `ctx->r4 = ADD32(ctx->r4, 0X20);`. Esto es traducción mecánica, **no**
   decompilación: el C++ resultante no es código "limpio" ni legible como
   lógica de alto nivel (ver
   `docs/arquitectura/decompilacion-vs-recompilacion.md`).
5. **Resolución de llamadas**: para instrucciones `J`/`JAL` (saltos y
   llamadas estáticas), el recompilador intenta primero un auto-enlace por
   símbolo de relocación conocido (p. ej. `sceCdRead`); si no puede
   resolverlo estáticamente, el código generado cae a
   `runtime->lookupFunction(0x...)` en tiempo de ejecución.
6. **Syscalls**: la instrucción `SYSCALL` recompilada invoca
   `runtime->handleSyscall(...)` con el inmediato codificado; el
   despachador del runtime intenta primero el ID de syscall codificado y
   si falla cae a mirar el registro `$v1` (convención real del kernel de
   PS2 para syscalls).
7. **Stubs y skips**: funciones listadas como `stubs` en el TOML generan
   wrappers que llaman a manejadores conocidos del runtime (incluye
   manejadores genéricos `ret0`, `ret1`, `reta0` para triage rápido, y
   soporte de *bindeo* directo por dirección con sintaxis
   `handler@0xADDRESS` para binarios sin símbolos). Funciones listadas
   como `skip` generan wrappers explícitos `ps2_stubs::TODO_NAMED(...)`
   que no ejecutan la lógica original.
8. **Overrides específicos de juego** ("Game Override Hooks"): código C++
   que se ejecuta durante la carga del ELF y puede reemplazar, por
   dirección, funciones concretas de un build específico. Es
   explícitamente el mecanismo recomendado para lógica *per-build* sin
   contaminar el comportamiento global del runtime — este es el mecanismo
   más relevante para cualquier parche específico de Tekken 5 que
   necesitemos en el futuro.

## Qué puede hacer PS2Recomp automáticamente

- Desensamblar y traducir mecánicamente instrucciones R5900 (enteras,
  FPU, MMI, VU0 macro) a C++.
- Generar wrappers de entrada para puntos de entrada estáticos adicionales
  que detecta en el binario.
- Enlazar automáticamente llamadas a funciones conocidas de biblioteca de
  sistema PS2 por nombre de relocación, cuando el símbolo está presente.
- Proveer un esqueleto de runtime (memoria, despacho de funciones,
  syscalls básicos, stubs de hardware) suficiente para **enlazar y
  ejecutar** el código generado, aunque sea de forma incompleta.
- Ejecutar módulos IRX del IOP contra un kernel IOP virtual con HLE
  genérico (no HLE específico de cada módulo).
- Incluir el ELF original embebido en el ejecutable final generado (según
  el flujo de CI de referencia `Ps2recompGames`), de modo que el binario
  distribuido no necesita el ELF por separado en tiempo de ejecución
  (aunque sí sigue dependiendo de activos externos del juego, como la ISO,
  que el usuario debe aportar).

## Qué NO hace automáticamente (y qué tendríamos que construir para Tekken 5)

Esto es la pregunta más importante del encargo original y se responde con
el nivel de certeza que permite la evidencia disponible (MUY BIEN
RESPALDADO, no VERIFICADO, porque no lo hemos ejecutado nosotros todavía):

1. **No identifica qué hace cada función en términos de lógica de juego.**
   El mapa de funciones (nombres, límites) debe venir de Ghidra y de
   nuestro propio trabajo de análisis; el C++ generado no es legible como
   "lógica de combate", es una traducción literal de MIPS.
2. **No implementa el Graphics Synthesizer ni VU1 de forma utilizable en
   la práctica.** El propio README admite rendimiento "muy malo" para GS y
   VU (ver TK5-0006). Para Tekken 5, que es un juego 3D con animación de
   personajes dependiente de VU1 (hipótesis razonable pero no verificada
   todavía, pendiente de TK5-0014), esto implica que **el renderizado y
   probablemente buena parte de la animación tendrán que reconstruirse o
   reimplementarse**, no simplemente "ejecutarse" vía recompilación.
3. **No resuelve automáticamente syscalls o módulos IOP específicos de un
   juego.** El despachador genérico cubre IDs de kernel comunes; los
   módulos IRX propios de Namco (si existen, no verificado) tendrían que
   analizarse e implementarse como HLE a medida.
4. **No garantiza que el juego arranque.** El propio flujo de CI de
   referencia lo declara explícitamente: una compilación exitosa del C++
   generado no implica que el título arranque ni sea jugable sin trabajo
   adicional de mapeo Ghidra, stubs, syscalls, parches y overrides
   específicos del juego.
5. **No reconstruye los formatos de archivo internos del juego** (modelos,
   animaciones, audio, etc.) — eso es un problema de ingeniería inversa de
   assets, completamente independiente de la recompilación de código (ver
   `docs/investigacion/licencias.md` para el límite legal: PS2Recomp solo
   toca código ejecutable, nunca assets, y este proyecto debe mantener esa
   misma separación).

## Limitaciones declaradas explícitamente por el propio proyecto

Ver TK5-0006 para el detalle con cita textual. En resumen: estado
"Experimental", rendimiento muy pobre en VU/GS, emulación de hardware
parcial con muchas rutas "stubbeadas", y requisitos de compilación
específicos (CMake 3.20+, C++20, SSE4/AVX, probado principalmente con
MSVC — lo cual tiene implicaciones para portabilidad Linux/macOS que
deberán evaluarse más adelante).

## Relevancia directa para Tekken 5

Dado TK5-0017 (no existe ningún trabajo previo específico de Tekken 5 con
PS2Recomp ni con ninguna otra herramienta de recompilación/decompilación),
cualquier aplicación de PS2Recomp a Tekken 5 sería un esfuerzo desde cero:

1. Obtener el ELF principal de una copia legal de NTSC-U (TK5-0018).
2. Analizarlo en Ghidra con la extensión EE (ver
   `docs/ingenieria-inversa/workflow-ghidra.md`), comprobando primero si
   existen símbolos `.mdebug`/STABS (TK5-0008) que aceleren
   drásticamente la identificación de funciones.
3. Exportar el mapa de funciones a TOML/CSV para `ps2xAnalyzer`/`ps2xRecomp`.
4. Compilar PS2Recomp y ejecutar la recompilación, inspeccionando el C++
   generado como primer criterio de éxito (que se genere sin errores),
   sin esperar que el resultado sea ejecutable todavía.
5. Determinar, función por función, qué necesita convertirse en stub,
   override o implementación real, empezando por el código más simple y
   menos dependiente de GS/VU1 (ver `docs/desarrollo/primer-milestone.md`).

## Fuentes

- https://github.com/ran-j/PS2Recomp (README completo, inspeccionado
  directamente)
- https://github.com/ej-sanmartin/ps2recomp (fork, mismo README base,
  marcado "Not ready" por su propio mantenedor)
- https://github.com/Kittystyle850/Ps2recompGames (ejemplo de pipeline de
  CI que usa PS2Recomp de extremo a extremo)
- https://github.com/menaman123/Ps2Recomp (ejemplo de proyecto de
  aplicación temprana/manual a otro juego, Crash Twinsanity, útil como
  referencia de la fase "Hello World" previa a automatizar nada)
- https://gigazine.net/gsc_news/en/20260130-ps2recomp/ (cobertura
  periodística independiente, usada solo como contexto, no como fuente
  técnica primaria)
