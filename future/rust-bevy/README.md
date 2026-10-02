# future/rust-bevy/ — Exploración futura, fuera del desarrollo activo

> **Este directorio es exclusivamente especulativo.** No contiene ni
> contendrá código de producción mientras el proyecto esté en las fases
> 0-6 de `docs/desarrollo/roadmap.md`. Ver sección 22 del encargo original
> del proyecto y la Regla de `AGENTS.md` correspondiente: "No introducir
> Rust en el proyecto principal todavía."

## Por qué existe este directorio ahora, si no se va a usar todavía

Para dejar explícito, desde el principio, dónde debería vivir en el futuro
cualquier exploración de una reescritura en Rust/Bevy, evitando que se
mezcle accidentalmente con el desarrollo activo en `src/`, `runtime/` y
`tools/`, que sigue la estrategia principal de recompilación estática +
reconstrucción progresiva (ver `README.md` raíz).

## Condición para empezar a usar este directorio

Según el encargo original: "la futura reescritura deberá basarse en el
conocimiento obtenido de Tekken 5", es decir, no antes de que
`docs/arquitectura/arquitectura-futura.md` deje de ser exploratorio y
contenga una separación de sistemas **verificada por investigación real**
del juego (no solo hipótesis).

## Proyectos de referencia mencionados en el encargo (no investigados en profundidad en esta pasada)

- Proyectos de preservación en Rust en general.
- Proyectos Rust/Bevy de recreación de juegos.
- "Skate 3 Rust" y `2010-rust-rewrite-mashup` — nombres citados
  explícitamente en el encargo original; no se ha realizado todavía una
  búsqueda dedicada para confirmar su existencia, estado o metodología.
  Si se investigan en el futuro, el resultado debe documentarse como un
  hallazgo `TK5-XXXX` igual que cualquier otra investigación, aunque sea
  sobre una tecnología fuera del alcance actual.

## Qué NO hacer aquí todavía

- No copiar arquitecturas externas de Rust/Bevy sin entenderlas primero
  (Regla explícita del encargo original, sección 22).
- No empezar ninguna implementación, por pequeña que sea, de lógica de
  Tekken 5 en Rust, hasta que el conocimiento real del juego (obtenido en
  `docs/`, `research/`) lo justifique.
