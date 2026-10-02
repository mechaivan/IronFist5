# Proyectos similares de ingeniería inversa, decompilación y recompilación

Ver hallazgos asociados: TK5-0005, TK5-0006, TK5-0012, TK5-0013, TK5-0017.

Plantilla usada para cada proyecto (sección 9 del encargo original):

```text
Nombre:
Repositorio:
Objetivo:
Juego:
Técnica:
Lenguaje:
Herramientas:
Licencia:
Estado:
Qué podemos aprender:
Qué NO podemos asumir:
Relevancia para Tekken 5:
```

---

### PS2Recomp

```text
Nombre: PS2Recomp
Repositorio: https://github.com/ran-j/PS2Recomp
Objetivo: Recompilación estática de binarios ELF de PS2 a C++ ejecutable en PC
Juego: Ninguno específico; herramienta genérica
Técnica: Recompilación estática (traducción literal instrucción-a-instrucción)
Lenguaje: C++ (recompilador y runtime)
Herramientas: ELFIO, toml11, fmt; integración recomendada con Ghidra
Licencia: GPL-3.0
Estado: Experimental, activo (commits recientes a sept-oct 2026)
Qué podemos aprender: El flujo completo Ghidra → TOML → C++ → runtime; la
  separación entre "lo que la herramienta automatiza" y "lo que requiere
  trabajo específico del juego" (ver docs/investigacion/ps2recomp.md)
Qué NO podemos asumir: Que vaya a ejecutar Tekken 5 "de fábrica"; que su
  soporte de VU1/GS sea suficiente para un juego de lucha 3D sin trabajo
  adicional sustancial (ver TK5-0006)
Relevancia para Tekken 5: Muy alta — es la pieza central de la visión a
  largo plazo del proyecto (ver README.md, diagrama de visión)
```

### God Hand Decomp

```text
Nombre: god-hand-decomp
Repositorio: https://github.com/LucasPicoli/god-hand-decomp
Objetivo: Decompilación por "matching" de God Hand (recrear código fuente
  C que, compilado con el compilador original, produzca bytes idénticos)
Juego: God Hand (PS2, Clover Studio/Capcom, NTSC-U SLUS-21503) — distinto
  estudio y motor que Tekken 5
Técnica: Decompilación por matching, función a función
Lenguaje: C (código reconstruido), herramientas de build en JSON/Python
  (no inspeccionado en profundidad)
Herramientas: Compilador original identificado como "sn-2.95.3-136" (SN
  Systems), un `compile_config.json` propio del proyecto
Licencia: No verificada en esta pasada — DEBE comprobarse antes de mirar o
  reutilizar cualquier código (Regla 7 de AGENTS.md)
Estado: Trabajo en progreso, con actividad de commits reciente (2026)
Qué podemos aprender: Organización del progreso por unidad de compilación,
  medición de avance como "funciones que compilan idénticas", registro
  explícito del compilador/versión exacta usada por build
Qué NO podemos asumir: Que su metodología de "matching" sea directamente
  aplicable a Tekken 5 sin adaptar — distinto estudio (Namco, no Clover),
  presumiblemente distinta cadena de compilación
Relevancia para Tekken 5: Media — referencia metodológica valiosa para una
  eventual fase de decompilación (distinta de la recompilación de
  PS2Recomp), no para la fase actual del proyecto
```

### N64Recomp / Zelda64Recomp

```text
Nombre: N64Recomp (herramienta) / Zelda64Recomp (aplicación)
Repositorio: https://github.com/N64Recomp/N64Recomp
             https://github.com/Zelda64Recomp/Zelda64Recomp
Objetivo: Port nativo de Majora's Mask (y próximamente Ocarina of Time)
  mediante recompilación estática de N64 a PC
Juego: The Legend of Zelda: Majora's Mask / Ocarina of Time (N64, no PS2)
Técnica: Recompilación estática + runtime moderno (RT64 para render)
Lenguaje: C/C++
Herramientas: RT64, RmlUi, symbols files propios (Zelda64RecompSyms)
Licencia: MIT (N64Recomp) / GPL-3.0 (Zelda64Recomp)
Estado: Activo, con releases jugables públicas
Qué podemos aprender: Separación explícita entre decompilación (de la que
  toman "headers y definiciones de funciones" como ayuda) y recompilación
  estática (de la que depende el port real); política de no distribuir
  assets del juego; atar el proyecto a una ROM/versión específica en vez
  de intentar soportar "cualquier" versión
Qué NO podemos asumir: Que las soluciones de render (RT64) o la
  complejidad de la plataforma N64 sean comparables a PS2 — N64 no tiene
  Vector Units dedicadas ni un Graphics Synthesizer propio como PS2
Relevancia para Tekken 5: Alta como modelo de producto final (recompilación
  + runtime + exigir copia legal del usuario), baja como modelo técnico
  directo de la capa gráfica
```

### Proyectos mencionados en el encargo original aún no localizados o no confirmados

Los siguientes nombres se mencionan explícitamente en el encargo del
proyecto ("God Hand Decomp, PSRetrox, PS2 Decompiler Toolkit") y deben
investigarse en una futura sesión; en esta primera pasada no se ha logrado
confirmar su existencia con una fuente primaria propia (más allá de God
Hand Decomp, ya documentado arriba):

```text
Nombre: PSRetrox
Estado de la investigación: No localizado con una fuente primaria propia
  en esta pasada. DESCONOCIDO si corresponde a un proyecto de PS1, PS2 o
  un nombre de comunidad no indexado públicamente bajo ese término exacto.
Siguiente paso: Búsqueda dirigida específica en una futura sesión,
  incluyendo variantes de escritura del nombre.
```

```text
Nombre: "PS2 Decompiler Toolkit" (nombre genérico mencionado en el encargo)
Estado de la investigación: No localizado como un proyecto único con ese
  nombre exacto. Es posible que el encargo se refiera genéricamente al
  conjunto de herramientas ya documentadas aquí (ccc, ghidra-emotionengine-
  reloaded, PS2Recomp) en vez de a un proyecto específico.
Siguiente paso: Aclarar con quien encargó el proyecto si se refiere a una
  herramienta concreta, o tratarlo como una categoría (el "conjunto de
  herramientas" ya cubierto).
```

### Otras piezas del ecosistema de ingeniería inversa de PS2 (de chaoticgd)

```text
Nombre: ccc
Repositorio: https://github.com/chaoticgd/ccc
Objetivo: Parsear símbolos de depuración STABS de secciones .mdebug de
  binarios de PS2
Técnica: Análisis de formato de símbolos de depuración
Lenguaje: C++
Licencia: No verificada en esta pasada
Estado: Activo (105 estrellas al momento de observación)
Qué podemos aprender: Cómo extraer tipos/funciones/variables si el ELF de
  Tekken 5 conserva símbolos .mdebug (DESCONOCIDO todavía si los tiene)
Qué NO podemos asumir: Que Tekken 5 tenga estos símbolos — hay que
  comprobarlo con readelf/objdump sobre el ELF real
Relevancia para Tekken 5: Potencialmente muy alta si se confirma la
  presencia de símbolos .mdebug
```

```text
Nombre: vutrace
Repositorio: https://github.com/chaoticgd/vutrace
Objetivo: Depurador de trazas de Vector Unit de PS2
Técnica: Trazado de ejecución de microprogramas VU
Lenguaje: C
Licencia: No verificada en esta pasada
Estado: Activo (37 estrellas)
Relevancia para Tekken 5: Alta para la investigación de VU1 (ver
  docs/ps2/arquitectura-ee.md, preguntas abiertas sobre uso de VU1)
```

## Conclusión de esta sección

No se ha encontrado ningún proyecto de decompilación o recompilación
dedicado específicamente a Tekken 5 (TK5-0017). Los proyectos más
relevantes son de propósito general (PS2Recomp) o de otros juegos/
plataformas usados como referencia metodológica (God Hand Decomp,
N64Recomp/Zelda64Recomp). Esto confirma que este proyecto parte, en la
práctica, de cero en lo específico de Tekken 5.
