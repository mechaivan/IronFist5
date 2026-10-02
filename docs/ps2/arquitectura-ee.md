# Arquitectura de PlayStation 2 relevante para Tekken 5

Ver hallazgo asociado: TK5-0014.

Este documento **no pretende ser una enciclopedia de PlayStation 2**. Su
propósito es doble: (1) fijar un resumen mínimo, verificado, del hardware
relevante para cualquier trabajo de recompilación en esta plataforma, y
(2) dejar explícitamente registrado qué partes de esa arquitectura usa
*realmente* Tekken 5 — que, a día de hoy, es mayoritariamente
**DESCONOCIDO** y requiere trabajo de investigación propio.

## Resumen verificado del hardware (genérico, no específico de Tekken 5)

| Componente | Función | Dato verificado |
|---|---|---|
| Emotion Engine (EE) | CPU principal | Núcleo MIPS III (R5900), 128-bit SIMD, 294.912 MHz (299 MHz en consolas posteriores) |
| VU0 | Vector Unit acoplada a la EE (modo macro o micro) | Usada típicamente para física/IA/animación según fuentes técnicas generales |
| VU1 | Vector Unit independiente, conectada directamente al GIF | Usada típicamente para generar listas de despliegue ("display lists") de geometría |
| GS (Graphics Synthesizer) | Procesador de render con eDRAM embebida | 147.456 MHz |
| GIF | Interfaz que conecta EE/VU1 con la GS | Bus 64-bit a 150 MHz, hasta 1.2 GB/s teóricos |
| VIF0 / VIF1 | Canales DMA dedicados hacia VU0 / VU1 | Parte del controlador DMA de 10 canales |
| DMAC | Controlador de acceso directo a memoria | 10 canales |
| RDRAM | Memoria principal | 32 MB, 3.2 GB/s de ancho de banda |
| Scratchpad | Memoria local de muy baja latencia de la EE | 16 KB, dual-port (fuente secundaria técnica, no oficial) |
| IOP | Procesador de entrada/salida (CD/DVD, audio, tarjetas de memoria, mandos) | Núcleo R3000A (no profundizado todavía en esta pasada) |
| SIF | Interfaz de comunicación EE ↔ IOP | Usa RPC (remote procedure call) sobre un enlace serie, según la especificación técnica agregada de Wikipedia |

Fuentes: ver TK5-0014 para citas completas (Wikipedia, "Sound and Vision:
A Technical Overview of the Emotion Engine", 2008).

## Lo que todavía NO sabemos (y es la pregunta real a responder)

El encargo original de este proyecto es explícito: no basta con describir
PS2 en general, hay que responder **qué usa realmente Tekken 5 y por
qué**. A fecha de esta investigación, estas preguntas están abiertas:

1. ¿Tekken 5 usa VU1 en modo "micro" (microprograma independiente
   ejecutándose en paralelo a la EE) para el skinning de personajes, para
   generación de geometría, para ambos? — DESCONOCIDO.
2. ¿Qué proporción del trabajo de animación/física recae en VU0 frente a
   en la EE directamente? — DESCONOCIDO.
3. ¿Cuántos canales DMA activa simultáneamente durante un combate con dos
   personajes, efectos de partículas, y HUD? — DESCONOCIDO.
4. ¿Qué módulos IRX carga el IOP (audio ADPCM vía SPU2, lectura de
   CD/DVD, tarjeta de memoria, controlador)? ¿Usa algún módulo propio de
   Namco además de los estándar de Sony? — DESCONOCIDO.
5. ¿Usa la IPU (descompresión de vídeo) para las cinemáticas o para
   "The Devil Within"? — DESCONOCIDO.
6. ¿El juego usa interrupciones y temporizadores de hardware de forma
   directa para el timing de combate (frame-perfect inputs, ventanas de
   bloqueo), o se apoya en el kernel de PS2 para esto? — DESCONOCIDO, pero
   de alto interés dado que Tekken es una franquicia donde el framedata
   exacto importa mucho para la escena competitiva (ver
   `docs/gameplay/README.md`).

## Cómo se plantea investigarlo (plan, no resultado)

1. **Trazas de ejecución en PCSX2**: usar el depurador de PCSX2 (ver
   `docs/investigacion/emulacion.md`) para observar, durante una sesión de
   juego real, qué canales DMA/VIF/GIF se activan y con qué frecuencia.
2. **Análisis estático en Ghidra**: una vez identificadas funciones clave
   en el ELF (ver `docs/ingenieria-inversa/workflow-ghidra.md`), buscar
   referencias a registros mapeados en memoria conocidos de EE/GS/DMAC
   (direcciones de hardware documentadas de forma genérica por la
   comunidad de homebrew de PS2, pendiente de contrastar con una fuente
   como psdevwiki.com, no consultada todavía en esta pasada).
3. **Correlación**: cruzar ambos resultados para poder afirmar, con
   evidencia y no por generalización, qué partes de la arquitectura usa
   Tekken 5 y para qué subsistema del juego (renderizado de personaje,
   escenario, UI, audio, etc.).

Ninguno de estos tres pasos se ha ejecutado todavía. Este documento se
actualizará con los resultados conforme se obtengan, citando el hallazgo
`TK5-XXXX` correspondiente.

## Relación con PS2Recomp

Las limitaciones de PS2Recomp (TK5-0006) son precisamente más severas
cuanto más dependa el juego de VU1/GS reales: "Performance is very bad for
VU and GS". Si Tekken 5 depende fuertemente de VU1 para geometría de
personajes (hipótesis razonable para un juego de lucha 3D de 2005, pero no
confirmada), el camino de recompilación estática para el *renderizado*
específicamente puede no ser viable sin una reimplementación sustancial,
mientras que el camino de recompilación para la *lógica de juego* (estado
de combate, hitboxes, IA, timers) podría ser más tratable si esa lógica
corre mayoritariamente en la EE/VU0. Esto es una hipótesis de trabajo, no
una conclusión.
