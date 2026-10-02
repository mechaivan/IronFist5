# Metodología de investigación

Este documento define cómo se registra el conocimiento en este proyecto.
Es de obligado cumplimiento para cualquier agente (ver `AGENTS.md`).

## Niveles de confianza

| Nivel | Significado |
|---|---|
| `VERIFICADO` | Comprobado directamente por este proyecto (o por una fuente primaria indiscutible, como redump.org, código fuente oficial, o un repositorio inspeccionado línea a línea) con evidencia reproducible. |
| `MUY BIEN RESPALDADO` | Documentado de forma consistente por múltiples fuentes técnicas independientes y creíbles (mantenedores de herramientas, documentación oficial de un proyecto), pero no reproducido todavía por nosotros contra una copia retail de Tekken 5. |
| `PROBABLE` | Consistente con la evidencia disponible y con el comportamiento conocido de proyectos similares, pero con huecos de verificación. |
| `HIPÓTESIS` | Interpretación razonable, pero sin evidencia directa suficiente. Puede ser incorrecta. |
| `DESCONOCIDO` | No existe información pública fiable. Requiere investigación original. |
| `PENDIENTE DE VERIFICACIÓN` | Afirmación de la comunidad (foro, vídeo, wiki) que parece plausible pero no se ha contrastado de forma independiente. |

Ningún hallazgo debe quedar sin uno de estos niveles.

## Plantilla de hallazgo

Cada hallazgo importante se documenta en `research/hallazgos/TK5-XXXX.md`
usando esta estructura:

```text
Identificador: TK5-XXXX
Fecha:
Versión del juego: NTSC-U (SLUS-21059) | NTSC-J (SLPS-25510) | PAL (SCES-53202) | N/A (genérico)
Categoría:

Descubrimiento:

Evidencia:

Fuente:

Interpretación:

Nivel de confianza:

¿Está verificado?:

¿Cómo podría verificarse?:

Investigaciones relacionadas:
```

## Numeración

Los identificadores son secuenciales y permanentes: `TK5-0001`, `TK5-0002`,
etc. Nunca se reutiliza un número, incluso si un hallazgo se demuestra
incorrecto más adelante (en ese caso, se corrige el propio hallazgo y se
indica en el campo "Interpretación" que fue revisado, con fecha).

El índice completo vive en `research/hallazgos/README.md`.

## Separación de versiones

Tekken 5 tiene al menos tres ejecutables de PS2 distintos y verificados
(ver `docs/investigacion/versiones-tekken5.md`): NTSC-U, NTSC-J y PAL,
con fechas de compilación distintas. Ninguna dirección de memoria, offset
de ELF, o estructura de datos descubierta en una versión puede asumirse
válida en otra sin verificación explícita.

## Separación por origen de juego

Información proveniente de Tekken 5: Dark Resurrection, Tekken 6, Tekken
Tag Tournament 2 o cualquier otro título debe marcarse explícitamente con
el juego de origen. Nunca se traslada automáticamente a Tekken 5 (PS2,
2005) sin verificación.
