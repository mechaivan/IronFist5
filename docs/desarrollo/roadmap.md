# Hoja de ruta (roadmap)

Esta hoja de ruta es honesta sobre el estado actual: estamos en la fase 0
(investigación). Las fases posteriores son planificación, no compromisos
de fecha.

## Fase 0 — Investigación y organización (ACTUAL)

Estado: **en progreso**.

- [x] Estructura del repositorio.
- [x] `README.md` y `AGENTS.md`.
- [x] Investigación de versiones de Tekken 5 y selección de versión
      canónica (TK5-0018).
- [x] Investigación de PS2Recomp.
- [x] Investigación de Ghidra y extensiones de PS2.
- [x] Investigación de proyectos similares (decompilación/recompilación).
- [x] Investigación de herramientas de la comunidad de Tekken.
- [x] Registro de licencias de proyectos externos relevantes.
- [x] Sistema de hallazgos (`research/hallazgos/`) con primeros 19
      hallazgos documentados.
- [x] Backlog de investigación concreto.
- [ ] Verificación experimental propia sobre un ELF real de Tekken 5
      (bloqueada hasta que un colaborador aporte una copia legal
      localmente; nunca se sube al repositorio).
- [ ] Primer análisis real en Ghidra (comprobar símbolos .mdebug/STABS).
- [ ] Primer reconocimiento real del filesystem del disco.

## Fase 1 — Primer objetivo técnico demostrable

Estado: **pendiente**, depende de completar la Fase 0.

Ver `docs/desarrollo/primer-milestone.md` para el criterio de éxito
propuesto. En resumen: lograr que PS2Recomp genere y compile C++ a partir
de al menos una función real y no trivial del ELF de Tekken 5 NTSC-U, y
ejecutarla en el runtime de PS2Recomp con un resultado verificable (no
necesariamente visual).

## Fase 2 — Mapeo progresivo de funciones y sistemas

Estado: **pendiente**.

- Identificar y documentar (como hallazgos `TK5-XXXX`) funciones clave de
  arranque, menús, selección de personaje y lógica de combate básica.
- Determinar qué partes de la lógica de combate son tratables por
  recompilación estática directa y cuáles requieren decompilación dirigida
  (ver `docs/arquitectura/decompilacion-vs-recompilacion.md`).
- Comenzar a responder las preguntas abiertas de
  `docs/ps2/arquitectura-ee.md` (qué usa realmente Tekken 5 de VU0/VU1/
  DMA/IOP).

## Fase 3 — Runtime mínimo ejecutando código real sin gráficos

Estado: **pendiente**. Es, según el encargo original, un hito válido por
sí mismo aunque no tenga gráficos: "un primer objetivo que consiga
ejecutar correctamente código original recompilado ya puede ser un avance
importante".

## Fase 4 — Reconstrucción de sistemas independientes

Estado: **pendiente**, condicionado a que la Fase 2 revele una separación
real de sistemas en el código original (ver
`docs/arquitectura/arquitectura-futura.md` — no se presupone el resultado).

## Fase 5 — Renderizado y reimplementación de subsistemas no recompilables

Estado: **pendiente**. Dado que PS2Recomp declara explícitamente mal
rendimiento en GS/VU1 (TK5-0006), es probable (no seguro) que esta fase
requiera reimplementación, no recompilación directa.

## Fase 6 — Port nativo jugable

Estado: **pendiente**, objetivo final de las fases anteriores.

## Fase 7 (futura, fuera del alcance actual) — Evaluación de reescritura en Rust/Bevy

Estado: **explícitamente fuera de alcance por ahora**. Ver
`future/rust-bevy/README.md`. No se iniciará ningún trabajo de
implementación en Rust/Bevy dentro del desarrollo activo hasta que las
fases anteriores aporten conocimiento suficiente del juego original.

## Principio de actualización de esta hoja de ruta

Cada vez que una fase avance de forma significativa, este documento y el
`README.md` raíz deben actualizarse en el mismo cambio. Nunca se debe dejar
una fase marcada como completada si no lo está, ni viceversa.
