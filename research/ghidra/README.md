# research/ghidra/

Artefactos propios generados durante el análisis en Ghidra del ELF de
Tekken 5: notas de renombrado, mapas de funciones exportados, scripts de
Ghidra propios (si se escriben), y resultados de analizadores (STABS,
constant reference, etc.).

**Este directorio no debe contener nunca** proyectos completos de Ghidra
que embeban el ELF original, ni volcados de memoria/save states derivados
de una sesión con el juego cargado, salvo que se purgue cualquier dato
derivado directamente del juego antes de versionarlo (Regla 8 de
`AGENTS.md`). En caso de duda, no se sube.

## Estado actual

Vacío. El procedimiento previsto está documentado en
`docs/ingenieria-inversa/workflow-ghidra.md`. La ejecución real está
pendiente (ver `docs/desarrollo/backlog.md`, sección "Ghidra").

## Qué se espera encontrar aquí en el futuro

- `mapa-funciones-ntsc-u.csv` (o `.toml`): mapa de funciones exportado para
  `ps2xAnalyzer`/`ps2xRecomp`.
- Notas de cada función identificada manualmente, enlazando al hallazgo
  `TK5-XXXX` correspondiente en `research/hallazgos/`.
- Registro de si se encontraron símbolos `.mdebug`/STABS y qué cubrieron.
