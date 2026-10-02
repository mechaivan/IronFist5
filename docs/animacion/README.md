# Animación

Investigación del sistema de animación de personajes de Tekken 5:
esqueletos, clips de animación, blending, y su relación con los sistemas
de combate (framedata) y con VU0/VU1 (ver `docs/ps2/arquitectura-ee.md`).

## Estado actual

**Sin verificación propia.** La única pista disponible (TK5-0010,
TK5-0019) proviene de un tutorial de extracción de la versión **arcade**
Tekken 5.1, que menciona una cabecera `MIF` interpretada tentativamente
como "datos de hueso" por el propio autor del tutorial (sin confirmar), y
advierte que los modelos extraídos de esa fuente no incluyen un esqueleto
reconocible por Noesis. Esto es, en el mejor de los casos, una pista sobre
la versión arcade, no sobre el retail de PS2.

## Preguntas abiertas específicas

- ¿Las animaciones se comparten entre variantes de un mismo personaje
  (distintos trajes) o se duplican?
- ¿El formato de animación está comprimido (habitual en PS2 por
  limitaciones de memoria/ancho de banda)?
- ¿La interpolación/blending ocurre en la EE, en VU0, o en ambos?

## Próximos pasos

Bloqueado hasta tener un reconocimiento básico del filesystem retail (ver
`research/filesystem/README.md`) y, posiblemente, hasta identificar
funciones relacionadas en Ghidra.
