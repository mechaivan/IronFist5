# Contribuir a Tekken 5 Native

Gracias por tu interés en este proyecto de investigación e ingeniería
inversa. Antes de contribuir, lee **obligatoriamente** `AGENTS.md`: define
las reglas permanentes del proyecto (no asumir, exigir evidencia,
documentar, respetar versiones y licencias, no introducir datos
propietarios).

## Antes de abrir una contribución

1. ¿Tu cambio es una afirmación técnica sobre el funcionamiento de Tekken
   5? Si es así, debe venir con un nivel de confianza explícito (ver
   `docs/investigacion/metodologia.md`) y, si es relevante, un hallazgo
   nuevo en `research/hallazgos/` con el siguiente ID disponible.
2. ¿Tu cambio reutiliza código externo? Comprueba su licencia primero y
   regístrala en `docs/investigacion/licencias.md` antes de incluir nada.
3. ¿Tu cambio incluye algún archivo extraído del juego (ISO, ELF, assets,
   audio, vídeo, volcados de memoria)? **No lo incluyas.** Este
   repositorio no distribuye datos propietarios de Tekken 5 bajo ninguna
   circunstancia (Regla 8 de `AGENTS.md`).
4. ¿Tu cambio mezcla información de distintas versiones regionales
   (NTSC-U, NTSC-J, PAL) sin indicarlo? Sepáralas explícitamente (Regla 5).

## Tipos de contribución bienvenidos en esta fase

- Hallazgos de investigación nuevos, bien documentados y con fuente.
- Correcciones a hallazgos existentes que se demuestren incorrectos
  (corrige el hallazgo, no lo borres; indica la fecha de revisión).
- Mejoras a la documentación existente (claridad, enlaces rotos,
  actualización de estado).
- Scripts/herramientas de análisis que operen sobre datos aportados
  localmente por el propio usuario (nunca incluidos en el repositorio).
- Verificación experimental de pistas marcadas como "PENDIENTE DE
  VERIFICACIÓN" o "HIPÓTESIS" en los hallazgos existentes.

## Qué NO se va a aceptar todavía

Ver la sección 31 del encargo original, resumida en `AGENTS.md`: no se
acepta un "port completo", un motor nuevo sin justificación, un renderer
definitivo, código en Rust/Bevy fuera de `future/rust-bevy/` (y ahí solo
como documentación especulativa), estructuras/formatos/funciones
inventadas, código sin revisión de licencia, o cualquier dato propietario
del juego.

## Formato de commits

Usa mensajes claros y descriptivos que indiquen qué se investigó, qué se
documentó, o qué se corrigió. Si el commit añade o modifica un hallazgo,
referencia su ID (`TK5-XXXX`) en el mensaje.

## Proceso para añadir un hallazgo

Ver la sección "Cómo añadir un hallazgo nuevo" en
`research/hallazgos/README.md`.
