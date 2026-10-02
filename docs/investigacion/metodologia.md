# Metodología de investigación

Este documento define cómo se registra el conocimiento en IronFist 5. Es de
obligado cumplimiento para cualquier agente (ver `AGENTS.md`).

## Niveles de confianza

| Nivel | Significado |
|---|---|
| `VERIFICADO` | Comprobado directamente por este proyecto con evidencia reproducible, o por una fuente primaria inspeccionada de forma suficiente. |
| `MUY BIEN RESPALDADO` | Documentado por múltiples fuentes técnicas independientes, pero aún no reproducido contra el ELF retail objetivo. |
| `PROBABLE` | Consistente con la evidencia disponible, pero con huecos de verificación. |
| `HIPÓTESIS` | Interpretación razonable sin evidencia directa suficiente. Puede ser incorrecta. |
| `DESCONOCIDO` | No existe información pública fiable o todavía no se ha investigado. |
| `PENDIENTE DE VERIFICACIÓN` | Afirmación externa plausible que aún no se ha contrastado de forma independiente. |

Ningún hallazgo debe quedar sin nivel de confianza. Las observaciones y las
interpretaciones deben mantenerse separadas.

## Familias de identificadores

Los hallazgos usan una familia que indica su contexto. Cada familia tiene una
secuencia independiente, permanente y sin reutilización de números:

| Familia | Uso |
|---|---|
| `TK5-XXXX` | Tekken 5 específico, versiones, builds y hechos generales del título. |
| `DW-XXXX` | Devil Within, cuando el hallazgo es específico de ese modo. |
| `PS2-XXXX` | Hardware, EE, VU, GS, IOP, DMA, BIOS y comportamiento de la plataforma. |
| `RECOMP-XXXX` | PS2Recomp, generación, runtime, toolchain de recompilación y matching. |
| `ASSET-XXXX` | Formatos, contenedores y referencias a assets, sin almacenar assets propietarios. |
| `MEM-XXXX` | Direcciones, regiones de memoria, estados, breakpoints y observaciones de memoria. |

Si un hallazgo afecta a varias áreas, se crea un expediente principal en la
familia más específica y se enlazan los expedientes relacionados. No se
renumera ni se convierte un ID existente sólo por cambiar una interpretación.

## Plantilla de hallazgo

Cada hallazgo se documenta en `research/hallazgos/<ID>.md`:

```text
Identificador: DW-0001
Fecha:
Versión/build: NTSC-U (SLUS-21059) | NTSC-J | PAL | N/A
Familia/categoría:
Estado: CONFIRMED | PROBABLE | HYPOTHESIS | UNKNOWN

Pregunta o afirmación:

Observación:

Evidencia:

Fuente:

Interpretación:

Limitaciones y alternativas:

¿Cómo podría verificarse o refutarse?:

Investigaciones relacionadas:
```

En documentación en español se pueden usar también las etiquetas
`VERIFICADO`, `PROBABLE`, `HIPÓTESIS` y `DESCONOCIDO`, pero no se deben
mezclar estados en una misma entrada sin explicar su equivalencia.

## Reglas de evidencia

1. Indicar si la evidencia procede de documentación, código externo,
   Ghidra, PCSX2, PS2Recomp o una fuente comunitaria.
2. Registrar versión, región, herramienta y comandos cuando sea posible.
3. No inferir exclusividad por un nombre de función, archivo o pantalla.
4. No subir ISO, ELF, volcados, save states ni assets derivados.
5. Una ausencia de resultados se registra como ausencia de evidencia, no como
   prueba de inexistencia.

## Separación de versiones

Tekken 5 tiene al menos tres ejecutables PS2 distintos y verificados (ver
`docs/investigacion/versiones-tekken5.md`). Ninguna dirección, offset o
estructura puede asumirse válida entre regiones o builds sin verificación
explícita.

## Separación por origen de juego

Información proveniente de Tekken 5: Dark Resurrection, Tekken 6, Tekken Tag
Tournament 2 u otro título debe marcarse con su juego de origen. Nunca se
traslada automáticamente a Tekken 5 PS2.

## Índice

El índice completo y las siguientes secuencias disponibles viven en
`research/hallazgos/README.md`.
