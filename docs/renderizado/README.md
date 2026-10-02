# Renderizado

Investigación de cómo Tekken 5 usa el Graphics Synthesizer (GS), VU1 y el
pipeline de render de PS2 (GIF, VIF1), y qué implicaciones tiene esto para
una futura implementación nativa.

## Estado actual

**Sin verificación propia.** Lo que sabemos hasta ahora es genérico del
hardware PS2 (TK5-0014), no específico de cómo Tekken 5 construye sus
listas de despliegue o gestiona sus texturas/materiales.

Dato relevante de planificación: PS2Recomp, la herramienta central de la
visión de recompilación de este proyecto, declara explícitamente
rendimiento muy pobre para GS y VU (TK5-0006). Esto hace **probable** (no
seguro) que el renderizado requiera reimplementación en vez de
recompilación estática directa (ver
`docs/arquitectura/decompilacion-vs-recompilacion.md`).

## Preguntas abiertas

- ¿Cuántas listas de despliegue construye por frame, y con qué
  complejidad geométrica (número de personajes + escenario + efectos)?
- ¿Usa VU1 en modo micro para transformaciones de geometría, o delega más
  trabajo a la EE/VU0?
- ¿Qué formato de textura usa en el filesystem (ver TK5-0019, hipótesis de
  TIM2 basada en la versión arcade, no confirmada en retail)?

## Próximos pasos

Bloqueado hasta completar la instrumentación de una sesión real en PCSX2
(ver `docs/desarrollo/backlog.md`, sección "PS2") y el análisis de
funciones relacionadas con GIF/VIF1 en Ghidra.
