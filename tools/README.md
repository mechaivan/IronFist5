# tools/

Herramientas propias (scripts/CLIs) para apoyar la investigación: análisis
de ELF, escaneo de filesystem, generación de mapas de símbolos, utilidades
de verificación de hashes contra `research/hallazgos/TK5-0002.md`.

## Regla de oro

Cualquier herramienta de este directorio debe operar sobre datos que el
usuario aporta localmente desde su propia copia legal de Tekken 5, y nunca
debe subir, empaquetar, cachear ni distribuir esos datos (Regla 8 de
`AGENTS.md`). Si una herramienta necesita un archivo de entrada del juego,
debe recibirlo como parámetro de línea de comandos apuntando a una ruta
local del usuario, nunca embebido ni incluido por defecto en el repositorio.

## Estado actual

Vacío. Ninguna herramienta propia se ha escrito todavía: la fase actual
del proyecto es de investigación (ver `docs/desarrollo/roadmap.md`, Fase 0).
La primera herramienta prevista es un verificador de hash de ISO contra la
tabla de `research/hallazgos/TK5-0002.md`, para que cualquier colaborador
pueda confirmar que trabaja sobre la versión correcta antes de reportar un
hallazgo.
