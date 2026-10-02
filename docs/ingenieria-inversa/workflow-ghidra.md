# Workflow de Ghidra para Tekken 5 (PS2)

Ver hallazgos asociados: TK5-0007, TK5-0008. Sección 15 del encargo
original.

Este documento describe el **procedimiento planeado** para analizar el ELF
de Tekken 5 con Ghidra. Donde el procedimiento ya se ha verificado con
fuentes externas, se indica. Donde todavía no se ha ejecutado sobre el ELF
real de Tekken 5, se indica explícitamente como pendiente.

## Diagrama de flujo esperado

```text
Juego original (copia legal del usuario)
      ↓
Extracción del ELF principal (y, si existen, overlays/módulos IOP)
      ↓
Importación en Ghidra
      ↓
Configuración del lenguaje R5900 / PS2 (requiere extensión de terceros)
      ↓
Análisis automático + comprobación de símbolos .mdebug/STABS
      ↓
Identificación manual de funciones (si no hay símbolos)
      ↓
Renombrado y tipado progresivo
      ↓
Identificación de estructuras de datos
      ↓
Documentación (hallazgo TK5-XXXX por cada función/estructura relevante)
      ↓
Exportación de mapa de funciones (CSV/TOML)
      ↓
PS2Recomp (ps2xAnalyzer / ps2xRecomp)
```

## Instalación (verificado documentalmente, no ejecutado todavía en este entorno)

1. Instalar Ghidra (versión a decidir; debe anotarse la versión exacta en
   cuanto se instale, porque la extensión de PS2 debe coincidir
   exactamente con ella — ver TK5-0007, cita de fobes.dev).
2. Instalar la extensión `chaoticgd/ghidra-emotionengine-reloaded`
   (Apache-2.0), eligiendo la release compatible con la versión de Ghidra
   instalada. Alternativa histórica: `beardypig/ghidra-emotionengine` (no
   recomendada por defecto, dado que el fork "Reloaded" está más activo a
   fecha de esta investigación).
3. Reiniciar Ghidra tras instalar la extensión (requisito estándar de
   Ghidra para cargar nuevas extensiones).

## Importación del ELF

1. Crear un proyecto Ghidra **no compartido** ("Non-Shared Project"), según
   recomienda la guía de fobes.dev para trabajo individual con PS2.
2. Arrastrar el ELF extraído de la ISO (nunca la ISO ni el ELF en sí deben
   subirse a este repositorio, Regla 8 de `AGENTS.md`).
3. Seleccionar manualmente el lenguaje `R5900:LE:64:PS2` (o el nombre
   exacto que exponga la extensión instalada) si el autodetector de Ghidra
   no lo asigna automáticamente. Existe un caso documentado
   (`chaoticgd/ghidra-emotionengine-reloaded`, issue #127, "ELF not
   detected as PS2 ELF") donde el autodetector falla y hay que elegir el
   lenguaje R5900 de forma manual, aunque la decompilación funcione
   correctamente una vez seleccionado.

## Análisis

1. Ejecutar el análisis automático estándar de Ghidra.
2. **Comprobar inmediatamente si el ELF tiene una sección `.mdebug`** (se
   puede verificar antes incluso de entrar en Ghidra, con
   `readelf -S archivo.elf` sobre el ELF extraído localmente por el
   usuario). Si existe, usar el "STABS Analyzer" incluido en
   `ghidra-emotionengine-reloaded` (que se apoya en `chaoticgd/ccc`) para
   recuperar automáticamente nombres de funciones, tipos y variables
   globales. **Esto no se ha comprobado todavía para Tekken 5** (ver
   TK5-0008, backlog).
3. Si no hay símbolos, proceder a identificación manual: usar las
   direcciones de memoria conocidas por parches de la comunidad (TK5-0009)
   como puntos de entrada para localizar funciones de interés (por
   ejemplo, la función de cálculo de FOV de cámara, o la tabla de
   desbloqueo de personajes).
4. Usar el "MIPS-R5900 Constant Reference Analyzer" de la extensión para
   corregir referencias a variables globales mal interpretadas por el
   analizador genérico de Ghidra.
5. Si se dispone de un volcado de memoria o save state de PCSX2 capturado
   durante una sesión de juego real, importarlo con el importador de save
   states de PCSX2 incluido en la extensión, para correlacionar direcciones
   estáticas del ELF con el comportamiento observado en ejecución.

## Renombrado y documentación

Cada función o estructura identificada con un nivel razonable de certeza
debe:

1. Renombrarse en Ghidra de forma descriptiva.
2. Documentarse como un hallazgo `TK5-XXXX` en `research/hallazgos/`
   (siguiendo `docs/investigacion/metodologia.md`), indicando la dirección
   exacta, la versión del ELF (NTSC-U/NTSC-J/PAL), y el método de
   identificación usado.
3. Registrarse también en `research/simbolos/` (ver ese directorio) con un
   formato más tabular/compacto pensado para consumo por herramientas
   (p. ej. para generar el CSV/TOML de PS2Recomp).

## Exportación hacia PS2Recomp

Una vez que exista un mapa de funciones razonable, exportarlo en el formato
que espera `ps2xRecomp` (`general.ghidra_output` en la configuración TOML,
ver `docs/investigacion/ps2recomp.md`). El formato exacto del CSV/TOML
esperado debe confirmarse leyendo el código fuente de `ps2xAnalyzer`/
`ps2xRecomp` (pendiente, no se ha inspeccionado el código fuente interno de
PS2Recomp más allá de su README en esta pasada).

## Problemas conocidos (documentados por la comunidad, no experimentados aún por nosotros)

- Autodetección de "ELF de PS2" puede fallar y requerir selección manual
  del lenguaje (issue #127 de ghidra-emotionengine-reloaded).
- La versión de la extensión debe coincidir exactamente con la versión de
  Ghidra instalada (fobes.dev).
- El IOP (R3000A) se analiza, según el hilo de Reddit de 2019, con la
  configuración MIPS estándar de Ghidra (no la extensión EE), lo cual debe
  tenerse en cuenta si se analizan módulos IRX por separado.

## Pendiente de ejecutar en este proyecto

Todo este workflow está descrito a partir de documentación externa
(MUY BIEN RESPALDADO), pero **no se ha ejecutado todavía sobre ningún ELF
de Tekken 5** en este proyecto, porque este entorno de trabajo no dispone
de una copia legal del juego para extraer el ELF (y no debe dispondría de
una subida al repositorio, Regla 8). La ejecución de este workflow sobre
una copia legal aportada por un colaborador humano es la primera tarea
técnica real del roadmap (ver `docs/desarrollo/roadmap.md`).
