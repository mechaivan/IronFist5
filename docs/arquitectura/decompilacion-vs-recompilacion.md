# Decompilación vs. recompilación estática vs. reimplementación vs. port nativo

Sección 18 del encargo original. Estos cuatro términos se usan de forma
intercambiable con demasiada frecuencia fuera de este proyecto, y eso
genera expectativas falsas. Se definen aquí con precisión porque el
proyecto usará varias de estas técnicas en fases distintas y **no deben
confundirse**.

## Decompilación

Reconstruir **código fuente legible** (típicamente C) que, compilado de
nuevo con el compilador original exacto (o uno compatible a nivel de
salida), produce un binario idéntico o funcionalmente equivalente al
original ("matching decompilation"). Es un proceso manual e intensivo,
función por función, que requiere entender la lógica real del código.

Ejemplo de referencia estudiado en este proyecto: God Hand Decomp
(TK5-0012). El progreso se mide en "funciones que compilan igual al
original".

**Lo que obtenemos**: código fuente real, legible, modificable con
comprensión total de su funcionamiento.

**Costo**: muy alto esfuerzo humano por función; requiere conocer o
inferir el compilador y las opciones de compilación exactas originales.

## Recompilación estática

Traducir **mecánicamente** las instrucciones de la CPU original (en
nuestro caso, MIPS R5900) a un lenguaje de alto nivel (C++), de forma
automatizada, sin necesariamente entender qué hace cada función en
términos de lógica de juego. El resultado es código que *funciona* igual
(si el runtime que lo acompaña es correcto) pero que **no es legible como
lógica de negocio**: es, literalmente, una traducción instrucción a
instrucción (ver el ejemplo citado en TK5-0005: `addiu $r4, $r4, 0x20` →
`ctx->r4 = ADD32(ctx->r4, 0X20);`).

Herramienta de referencia en este proyecto: PS2Recomp
(`docs/investigacion/ps2recomp.md`). Referencia metodológica en otra
plataforma: N64Recomp/Zelda64Recomp (TK5-0013).

**Lo que obtenemos**: un binario que, en teoría, se comporta como el
original, ejecutable nativamente en PC, sin haber tenido que entender el
juego función por función.

**Costo**: el código generado es ilegible como lógica de alto nivel
(aunque sí se puede anotar/renombrar progresivamente); requiere un runtime
que emule el hardware específico que el código recompilado siga
necesitando (memoria, syscalls, y en el caso de PS2, potencialmente
GS/VU1/IOP reales).

## Reimplementación

Escribir **desde cero** un sistema que reproduce el comportamiento
observado y/o documentado de un sistema original, sin partir de una
traducción mecánica ni de una decompilación exacta de su código. Se apoya
en la investigación (ingeniería inversa de comportamiento, no
necesariamente de bytes) para producir un sistema equivalente mantenible y
moderno.

**Lo que obtenemos**: código completamente propio, idiomático, fácil de
mantener y extender — pero con riesgo de divergencia de comportamiento
respecto al original si la investigación previa fue incompleta.

**Costo**: requiere la investigación más profunda de las cuatro técnicas,
porque no hay "atajo mecánico" (como en recompilación) ni "andamiaje"
(como en decompilación por matching) que garantice fidelidad.

## Port nativo

Es el **resultado final** perseguido por este proyecto, no una técnica en
sí misma: un ejecutable que corre de forma nativa en PC (sin depender de
un emulador completo de PS2 en tiempo de ejecución) y que reproduce el
comportamiento del juego original con la mayor fidelidad posible. Un port
nativo puede construirse combinando las tres técnicas anteriores en
distintas proporciones para distintos subsistemas: por ejemplo,
recompilación estática para la lógica de combate de la EE, y
reimplementación para el renderizado (porque la recompilación de VU1/GS es
poco viable según TK5-0006).

## Qué significa esto para el estado actual del proyecto

Es importante no confundir estos dos enunciados, que son muy diferentes:

> "Tenemos código C++ generado por PS2Recomp a partir del ELF de Tekken 5."

frente a:

> "Tenemos una implementación limpia y comprendida del juego."

El primero, si llega a ocurrir, es un paso mecánico que no implica
comprensión real del sistema. El segundo es el objetivo final del
proyecto, y requiere documentación, verificación y, probablemente,
reimplementación de las partes que la recompilación estática no resuelva
bien (ver `docs/arquitectura/arquitectura-futura.md`).

## Plan de uso de cada técnica en este proyecto (sujeto a revisión)

| Fase | Técnica probable | Justificación |
|---|---|---|
| Arranque mínimo / lógica de la EE sin gráficos | Recompilación estática (PS2Recomp) | Es la vía con menor esfuerzo humano inicial para código escalar/control de flujo |
| Renderizado (GS/VU1) | Reimplementación (probable) | PS2Recomp declara rendimiento muy pobre aquí (TK5-0006); se necesitará un renderer moderno equivalente, no una traducción literal |
| Funciones críticas de combate (hitboxes, framedata) | Decompilación dirigida (probable, para las funciones más importantes) | Garantiza comprensión exacta de reglas que afectan directamente a la fidelidad competitiva del juego |
| Audio | Por determinar | Depende de si el IOP/SPU2 es tratable vía stubs de PS2Recomp o necesita reimplementación |

Esta tabla es una hipótesis de planificación, no una decisión cerrada; se
revisará conforme avance la investigación real sobre el ELF de Tekken 5.
