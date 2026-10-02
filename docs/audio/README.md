# Audio

Investigación del sistema de audio de Tekken 5: música, efectos de
sonido, voces de personajes, y su relación con el IOP/SPU2 (ver
`docs/ps2/arquitectura-ee.md`).

## Estado actual

**Sin investigación dedicada todavía.** No se ha realizado ninguna
búsqueda específica de formatos de audio de Tekken 5 en esta primera
pasada (ver tarea pendiente en `docs/desarrollo/backlog.md`, sección
"Audio").

Lo único verificado de forma genérica (no específica de Tekken 5): PS2 usa
el procesador de sonido SPU2, gestionado desde el IOP, típicamente con
audio comprimido en formato ADPCM — esto es conocimiento general de la
plataforma (TK5-0014), no una confirmación sobre Tekken 5.

## Preguntas abiertas

- ¿Qué formato de archivo de audio usa Tekken 5 internamente?
- ¿La música está en streaming desde el disco o precargada en memoria?
- ¿Existen herramientas genéricas de extracción de audio de PS2 (no
  específicas de Tekken) aplicables sin modificación?

## Próximos pasos

Ver `docs/desarrollo/backlog.md`, sección "Audio".
