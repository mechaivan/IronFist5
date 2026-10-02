# research/elf/

Datos crudos y notas de análisis del ELF principal de Tekken 5 (y de sus
posibles overlays/módulos adicionales), por versión regional.

**Este directorio no debe contener nunca el ELF en sí**, ni ningún otro
dato extraído directamente del juego (Regla 8 de `AGENTS.md`). Debe
contener únicamente:

- Notas de análisis (texto/markdown).
- Resultados de comandos como `readelf`/`objdump` (texto, no el binario).
- Mapas de funciones/símbolos en formato CSV/TOML generados por nosotros.
- Scripts propios de análisis (no el ELF que analizan).

## Estado actual

Vacío de datos reales: la investigación documental está en
`docs/ingenieria-inversa/elf-analisis.md` y los hallazgos relacionados son
TK5-0003 (diferencias de build entre regiones). El análisis experimental
del ELF real está pendiente de que un colaborador aporte una copia legal
localmente (ver `docs/desarrollo/backlog.md`, sección "Ingeniería
inversa").

## Convención de nombres prevista

`research/elf/<REGION>/<hallazgo-o-tema>.md`, por ejemplo
`research/elf/ntsc-u/secciones.md`, para mantener separados los datos de
cada build (Regla 5 de `AGENTS.md`).
