# Registro de hallazgos

Índice de todos los hallazgos documentados. Cada fila enlaza al expediente
completo con evidencia, fuente y nivel de confianza. Ver la plantilla y las
reglas de familias en `docs/investigacion/metodologia.md`.

## Familias y siguiente ID

Las secuencias son independientes y no se reutilizan:

| Familia | Siguiente ID | Uso |
|---|---:|---|
| `TK5-` | `TK5-0020` | Hechos específicos de Tekken 5 y sus builds |
| `DW-` | `DW-0001` | Devil Within |
| `PS2-` | `PS2-0001` | Hardware y comportamiento de PS2 |
| `RECOMP-` | `RECOMP-0001` | PS2Recomp y recompilación |
| `ASSET-` | `ASSET-0001` | Formatos y análisis de assets sin distribuirlos |
| `MEM-` | `MEM-0001` | Memoria, direcciones y estados observados |

Los identificadores provisionales de preguntas (`DW-Qxxx`) no son hallazgos
y no consumen esta numeración.

| ID | Resumen | Versión | Confianza |
|---|---|---|---|
| [TK5-0001](TK5-0001.md) | Identificadores regionales oficiales de Tekken 5 (SLUS-21059, SLPS-25510, SCES-53202 y variantes) | Todas | VERIFICADO |
| [TK5-0002](TK5-0002.md) | Hashes de disco verificados (redump.org) para las tres ediciones principales | Todas | VERIFICADO |
| [TK5-0003](TK5-0003.md) | Las versiones NTSC-U, NTSC-J y PAL usan ejecutables distintos (fechas y versión de build diferentes) | Todas | VERIFICADO |
| [TK5-0004](TK5-0004.md) | El disco NTSC-J contiene además Tekken, Tekken 2 Ver. B, Tekken 3 y Starblade | NTSC-J | VERIFICADO (parcial) |
| [TK5-0005](TK5-0005.md) | Qué hace PS2Recomp automáticamente (capacidades reales de la herramienta) | N/A | MUY BIEN RESPALDADO |
| [TK5-0006](TK5-0006.md) | Limitaciones conocidas de PS2Recomp (GS/VU1, hardware parcial) | N/A | MUY BIEN RESPALDADO |
| [TK5-0007](TK5-0007.md) | Ghidra no soporta R5900/PS2 de forma nativa; requiere extensiones de terceros | N/A | VERIFICADO |
| [TK5-0008](TK5-0008.md) | Capacidades de `ghidra-emotionengine-reloaded` (STABS/.mdebug, savestates PCSX2, analizador de constantes) | N/A | MUY BIEN RESPALDADO |
| [TK5-0009](TK5-0009.md) | Existen parches widescreen y cheats comunitarios de Tekken 5 con direcciones EE distintas por región | NTSC-U, PAL | PENDIENTE DE VERIFICACIÓN (comunidad) |
| [TK5-0010](TK5-0010.md) | Extracción comunitaria de assets de Tekken 5 se ha hecho sobre la versión arcade (Tekken 5.1), no sobre el retail PS2; el retail tiene datos ofuscados/comprimidos salvo "The Devil Within" | Arcade (T5.1) / PS2 sin confirmar | HIPÓTESIS / COMUNIDAD |
| [TK5-0011](TK5-0011.md) | El soporte de "Tekken 5" en TekkenMovesetExtractor/TKMovesets no está confirmado como extracción directa del ELF de PS2 | Desconocida | DESCONOCIDO / PENDIENTE DE VERIFICACIÓN |
| [TK5-0012](TK5-0012.md) | God Hand Decomp como referencia metodológica de decompilación por matching | N/A (otro juego, PS2) | VERIFICADO (existencia) / PROBABLE (metodología) |
| [TK5-0013](TK5-0013.md) | N64Recomp / Zelda64Recomp como referencia metodológica de recompilación estática | N/A (otra plataforma) | VERIFICADO |
| [TK5-0014](TK5-0014.md) | Resumen verificable de la arquitectura EE/VU/GS/IOP de PS2 (hardware general, no específico de Tekken 5) | N/A | VERIFICADO (hardware genérico) / DESCONOCIDO (uso específico por Tekken 5) |
| [TK5-0015](TK5-0015.md) | PCSX2 y Play! como herramientas de investigación: licencias y capacidades de depuración | N/A | VERIFICADO |
| [TK5-0016](TK5-0016.md) | Ecosistema emergente de herramientas de IA para ingeniería inversa de PS2 (PCSX2-MCP, GhidraMCP, skills de agentes) | N/A | PROBABLE (existencia) / PENDIENTE DE VERIFICACIÓN (fiabilidad, licencias) |
| [TK5-0017](TK5-0017.md) | No se ha encontrado ningún proyecto público de decompilación o recompilación específico de Tekken 5 PS2 (a 2026-10-02) | N/A | DESCONOCIDO (ausencia de evidencia, no prueba de inexistencia) |
| [TK5-0018](TK5-0018.md) | Selección de SLUS-21059 (NTSC-U) como versión canónica de trabajo | NTSC-U | DECISIÓN DE PROYECTO (basada en TK5-0001, TK5-0002, TK5-0003, TK5-0009) |
| [TK5-0019](TK5-0019.md) | Cabeceras de formato observadas en extracción comunitaria de Tekken 5.1 (arcade): NUDP, TIM2, MIF | Arcade (T5.1), no confirmado en PS2 retail | HIPÓTESIS / COMUNIDAD |

## Cómo añadir un hallazgo nuevo

1. Elige la familia correcta y usa su siguiente número disponible en la
   tabla anterior.
2. Crea `research/hallazgos/<FAMILIA>-XXXX.md` con la plantilla de
   `docs/investigacion/metodologia.md`.
3. Añade la fila correspondiente a esta tabla o crea el índice de la familia
   si aún no existe.
4. Si el hallazgo cambia una conclusión anterior, edita el hallazgo antiguo
   para reflejar la corrección (no lo borres) y referencia el nuevo ID.
5. No uses un prefijo para ocultar una afirmación no verificada: el nivel de
   confianza y la evidencia siguen siendo obligatorios.
