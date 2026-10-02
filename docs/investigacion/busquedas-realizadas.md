# Registro de búsquedas realizadas

Este documento existe para que futuros agentes sepan qué ya se buscó, con
qué resultado aproximado, y así evitar repetir trabajo o, al contrario,
saber cuándo vale la pena repetir una búsqueda porque el panorama cambia
rápido (como ha ocurrido con PS2Recomp, que pasó de no existir a tener
miles de estrellas en el curso de este mismo proyecto de investigación).

Fecha de esta tanda de búsquedas: 2026-10-02.

| Consulta (resumen) | Resultado principal |
|---|---|
| Tekken 5 PS2 SLUS-21059 / SLPS-25510 / SCES-53202 versiones | Confirmó los tres seriales principales y variantes de reedición (TK5-0001) |
| PS2Recomp github static recompilation | Encontrado y analizado en profundidad `ran-j/PS2Recomp` (TK5-0005, TK5-0006) |
| Ghidra PS2 extension R5900 EmotionEngine | Confirmadas extensiones `beardypig/ghidra-emotionengine` y `chaoticgd/ghidra-emotionengine-reloaded` (TK5-0007, TK5-0008) |
| God Hand decompilation project github | Encontrado `LucasPicoli/god-hand-decomp` (TK5-0012) |
| TekkenMovesetExtractor github Tekken 5 moveset format | Encontrado `Kiloutre/TekkenMovesetExtractor`; soporte de Tekken 5 no confirmado en detalle (TK5-0011) |
| Tekken 5 PS2 widescreen patch cheat code address gamehacking | Confirmadas direcciones de parches widescreen distintas por región (TK5-0009) |
| Tekken 5 PS2 file format .mot .obj TKD archive extraction Noesis | Encontrado tutorial de extracción sobre la versión arcade Tekken 5.1 (TK5-0010, TK5-0019) |
| PCSX2 debugger memory scanner Devil Within Tekken 5 IA reverse engineering | No se encontró documentación específica de IA/Devil Within de Tekken 5; sí se encontró el ecosistema de herramientas MCP para PCSX2 (TK5-0015, TK5-0016) |
| N64Recomp github license | Confirmada licencia MIT de N64Recomp y GPL-3.0 de Zelda64Recomp (TK5-0013) |
| ghidra-emotionengine-reloaded license redump Tekken 5 datfile hash | Confirmada licencia Apache-2.0 de la extensión; obtenidos hashes de redump.org (TK5-0002) |
| redump.org Tekken 5 SLUS-21059 / SLPS-25510 / SCES-53202 | Hashes y fechas de EXE verificados directamente en redump.org (TK5-0002, TK5-0003) |
| psdevwiki Emotion Engine overview VU0 VU1 GIF DMA | Resumen de hardware obtenido de Wikipedia y un artículo técnico de 2008 (TK5-0014) — **psdevwiki no se consultó directamente todavía, pendiente** |
| Play! PS2 emulator github jpd002 open source status | Confirmada existencia y licencia (con discrepancia a resolver) (TK5-0015) |
| PCSX2 license LGPL debugger memory viewer breakpoints savestate | Confirmada licencia GPL-3.0 de PCSX2 vía proyecto derivado | 

## Búsquedas pendientes para futuras sesiones

Estas búsquedas no se realizaron todavía por límite de alcance de esta
primera pasada, y quedan registradas como tareas de investigación (ver
también `docs/desarrollo/backlog.md`):

- Consulta directa de psdevwiki.com (wiki técnica de homebrew de PS2) para
  contrastar el resumen de arquitectura de TK5-0014 contra una fuente más
  técnica y específica de desarrollo homebrew.
- Búsqueda específica de "Tekken 5 Devil Within" + ingeniería inversa /
  modding, por separado del resto del juego.
- Búsqueda específica de la IA de Tekken 5 (estados de CPU, "ghost data",
  árbol de decisión) — no se encontró nada en esta pasada y no se ha vuelto
  a intentar con términos alternativos.
- Inspección directa del código fuente de `T5Aliases.py` en
  TekkenMovesetExtractor (no solo el README).
- Inspección directa de `Kiloutre/TKMovesets` (sucesor del extractor).
- Búsqueda de trainers/Cheat Engine tables específicos de Tekken 5 en
  PCSX2 (Cheat Engine + PINE/Pine IPC), que podrían aportar más
  direcciones de memoria verificadas que los simples pnach de widescreen.
- Consulta directa del archivo `LICENSE` de `jpd002/Play-` para resolver
  la discrepancia BSD-2-Clause vs. MIT señalada en TK5-0015.
- Búsqueda de foros de la escena de speedrunning/competitivo de Tekken 5
  (pueden tener documentación de frame data y timers ya "reverse
  engineered" de forma empírica, útil para testing diferencial).
