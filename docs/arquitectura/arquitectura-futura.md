# Arquitectura futura: separación de sistemas (exploratorio)

Sección 21 del encargo original. **Este documento es exploratorio.** La
arquitectura final no está decidida y no debe tratarse como un diseño
cerrado. Se revisará y corregirá conforme avance la ingeniería inversa
real del ELF de Tekken 5.

## Por qué esto todavía no es un diseño

No se puede diseñar correctamente la separación en capas de un sistema que
todavía no hemos analizado. Proponer una arquitectura de software "limpia"
ahora, antes de saber cómo está organizado realmente el código original,
sería exactamente el tipo de suposición que `AGENTS.md` prohíbe (Regla 1 y
Regla 9: no implementar a ciegas).

## Dirección conceptual (no estructura confirmada)

La progresión conceptual que se espera seguir, en términos muy generales:

```text
Código específico de PS2 (traducción literal de MIPS, syscalls, hardware)
        │
        ▼
Capa de compatibilidad (runtime: memoria, despacho de funciones, stubs)
        │
        ▼
Lógica del juego (lo que hoy vive dentro del código recompilado/decompilado)
        │
        ▼
Sistemas independientes (una vez identificados y separados con evidencia)
```

## Sistemas potenciales a identificar (lista de hipótesis a confirmar, no de diseño)

Estos son los sistemas que **cabría esperar** encontrar en un juego de
lucha 3D de la generación PS2, basándonos en conocimiento general de la
industria de la época, no en evidencia directa sobre Tekken 5 todavía:

- Personajes (datos de definición por personaje)
- Animación (esqueletos, clips, blending)
- Combate (máquina de estados de movimientos, framedata)
- Hitboxes / hurtboxes / colisiones
- Física (empujones, caídas, "wall bounce", etc.)
- Cámaras
- Escenarios
- IA (oponentes controlados por CPU)
- Audio
- Partículas / efectos
- Interfaz (menús, HUD)
- Input
- Gestión de recursos (carga de assets, streaming)

**Ninguno de estos sistemas tiene todavía una ubicación, formato o
estructura confirmada dentro del código de Tekken 5.** Esta lista es un
punto de partida para la investigación (qué buscar), no una afirmación de
cómo está organizado el juego.

## Qué determinará la arquitectura real

La separación real en capas/sistemas debe **emerger de**:

1. El análisis de funciones y símbolos en Ghidra (si hay símbolos STABS,
   TK5-0008, esto podría ser mucho más directo).
2. La observación de qué módulos/overlays carga el juego y cuándo (TK5-0004
   sugiere que el disco incluye, como mínimo, contenido separable para los
   arcades clásicos y "The Devil Within").
3. El comportamiento observado en PCSX2 (qué funciones se llaman en qué
   fases del juego: menú, selección de personaje, combate, replay).

## Qué NO vamos a hacer

- No vamos a copiar la arquitectura de otro proyecto (por ejemplo, la
  estructura de carpetas de un decomp de N64 o de God Hand) y asumir que
  aplica a Tekken 5 sin verificarlo primero.
- No vamos a diseñar una arquitectura de Entity-Component-System, un motor
  de ECS moderno, ni ningún otro patrón de moda, antes de entender la
  arquitectura original. Si eventualmente se adopta un patrón moderno,
  será una decisión consciente documentada, no un punto de partida.

## Relación con la futura reescritura en Rust/Bevy

Esta arquitectura de sistemas, una vez identificada con evidencia real, es
precisamente lo que permitiría evaluar en el futuro (no ahora, ver sección
22 del encargo y `future/rust-bevy/README.md`) qué partes podrían
reescribirse de forma independiente en una arquitectura moderna tipo
ECS (como Bevy). Pero eso depende enteramente de que primero exista
conocimiento real y verificado del juego — no al revés.
