# Testing diferencial (estrategia futura)

Sección 20 del encargo original. Este documento **investiga qué datos
podrían obtenerse realmente** para comparar el comportamiento del juego
original contra una futura implementación nativa. No se implementa todavía
ningún sistema de testing: eso sería implementar a ciegas (Regla 9 de
`AGENTS.md`) antes de saber qué es observable.

## Diagrama de la estrategia futura

```text
          TEKKEN 5 ORIGINAL (en PCSX2, instrumentado)
                 │
          ┌──────┴──────┐
          │             │
       entrada        estado
          │             │
          └──────┬──────┘
                 │
          Datos de referencia (capturados y versionados, NUNCA assets
          propietarios — solo valores numéricos/estructurales derivados)
                 │
                 ▼
       Implementación nativa (futura)
```

## Qué datos son, en principio, obtenibles vía PCSX2 (a confirmar experimentalmente)

Según las capacidades de depuración de PCSX2 documentadas en
`docs/investigacion/emulacion.md` (TK5-0015):

- **Memoria completa de la EE** (32 MB) en un instante dado, vía save
  state o volcado de RAM.
- **Registros de la EE/IOP** en un instante dado, vía el depurador o el
  protocolo GDB Remote Serial Protocol.
- **Inputs del jugador**, si se registran de forma determinista (requiere
  confirmar si PCSX2 soporta grabación de inputs de forma fiable para
  reproducción exacta — no verificado todavía en esta pasada).
- **Estado de memoria en direcciones conocidas**, una vez identificadas
  estructuras concretas (vida, posición, estado de animación, timers) con
  el trabajo de `research/memoria/`.

## Qué es, en principio, DIFÍCIL o requiere investigación adicional

- **RNG**: si Tekken 5 usa un generador de números pseudoaleatorios interno
  (razonable asumir que sí, para elementos como IA o ciertos efectos, pero
  no confirmado), reproducir exactamente la misma secuencia requeriría
  identificar la semilla y el algoritmo exacto — DESCONOCIDO todavía si es
  siquiera relevante para el núcleo del gameplay de combate (Tekken es,
  en su diseño competitivo, mayormente determinista por diseño, pero esto
  es una suposición de género, no un hecho verificado sobre esta
  implementación específica).
- **Resultados de renderizado**: comparar un frame renderizado por el GS
  original contra un frame de una futura implementación nativa requiere
  primero entender cómo el GS original produce esa imagen (muy relacionado
  con las preguntas abiertas de `docs/ps2/arquitectura-ee.md` sobre VU1/GS).
- **Timers de combate exactos**: Tekken es una franquicia con una escena
  competitiva que ya documenta framedata de forma empírica (jugando y
  contando frames), lo cual podría ser una fuente secundaria valiosa para
  contrastar contra lo que encontremos en el código, pero no se ha
  consultado ninguna fuente de ese tipo en esta pasada.

## Principio de diseño para cuando se implemente

Cuando llegue el momento de construir herramientas de testing diferencial
reales, deben cumplir, como mínimo:

1. No almacenar ni redistribuir ningún asset propietario del juego (solo
   valores derivados: posiciones, IDs de estado, timers, hashes de
   estructuras — nunca modelos, texturas, audio, ni el propio ejecutable).
2. Ser reproducibles: cualquier dato de referencia debe venir acompañado
   de la versión exacta del juego (serial + hash, TK5-0002), la versión de
   PCSX2 usada, y los pasos para regenerarlo.
3. Empezar por el subsistema más simple y mejor entendido primero (muy
   probablemente, datos de estado de combate simples como vida/posición,
   antes que renderizado).

## Estado actual

**No implementado.** Este documento es exclusivamente de investigación y
planificación, conforme a la sección 20 del encargo original ("No
implementes todavía un sistema gigantesco de testing. Primero investiga
qué datos pueden obtenerse realmente").
