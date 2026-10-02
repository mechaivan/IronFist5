# Gameplay

Investigación de los sistemas de gameplay de Tekken 5: máquina de estados
de combate, movesets, hitboxes/hurtboxes, IA de oponentes CPU, cámaras de
combate, timers y reglas de resolución de golpes.

## Estado actual

**Sin hallazgos verificados todavía.** No se ha identificado ninguna
función ni estructura de datos real de gameplay en el ELF de Tekken 5 (ver
TK5-0017: no hay trabajo previo público conocido sobre el que apoyarse).

Contexto relacionado ya documentado:

- `docs/arquitectura/arquitectura-futura.md` — lista de sistemas
  potenciales a identificar, explícitamente marcada como hipótesis de
  trabajo, no como estructura confirmada.
- `docs/desarrollo/incognitas.md` — preguntas abiertas específicas de
  gameplay (IA, RNG, "The Devil Within").
- `docs/desarrollo/testing-diferencial.md` — qué datos de combate podrían,
  en principio, capturarse de PCSX2 para comparación futura.

## Próximos pasos

Ver `docs/desarrollo/backlog.md`, secciones "Ingeniería inversa" y
"Gameplay". El primer paso realista es identificar, dentro del ELF, la
función responsable de procesar un input de combate simple (por ejemplo, un
golpe básico), una vez se disponga de un mapa de funciones mínimo vía
Ghidra.
