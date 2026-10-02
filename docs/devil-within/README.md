# Devil Within

`Devil Within` es una línea de investigación de primera clase de IronFist 5.
No se asume que sea simplemente Tekken 5 con una cámara distinta. Cualquier
relación entre sus sistemas y los modos principales debe demostrarse con
fuentes, análisis estático o comportamiento observado en PCSX2.

## Alcance

Esta área documentará, por separado del resto del juego:

- arquitectura y límites de los sistemas
- gameplay y reglas específicas
- Jin y sus estados de personaje
- animaciones y controladores
- enemigos e IA
- escenarios y streaming
- cámara
- efectos y pipeline asociado
- hallazgos, evidencias y preguntas abiertas

## Estado actual

**Investigación no iniciada en el ELF real.** No hay todavía resultados
experimentales, funciones identificadas, trazas de PCSX2 ni formatos
confirmados específicamente para Devil Within en este repositorio.

Las afirmaciones futuras deben indicar si proceden de:

1. documentación o código de una fuente externa;
2. análisis del ELF NTSC-U `SLUS-21059`;
3. observación en PCSX2;
4. comparación con otro modo, región o título.

## Identificadores

Los hallazgos específicos de Devil Within usan la familia `DW-XXXX` y se
registran en `research/hallazgos/`. La numeración es independiente de
`TK5-XXXX`. Para observaciones de hardware, recompilación, memoria o assets
que no sean exclusivas de Devil Within se debe usar la familia correspondiente
(`PS2-`, `RECOMP-`, `MEM-` o `ASSET-`) y enlazar el contexto aquí.

## Documentos

- [Arquitectura](arquitectura.md)
- [Gameplay](gameplay.md)
- [Plan de investigación](plan-investigacion.md)
- [Registro de preguntas](preguntas-abiertas.md)

## Restricciones legales

No se almacenarán ISOs, ELF retail, volcados de memoria, assets extraídos,
audio, modelos, texturas ni otros datos propietarios. Las futuras
observaciones deben ser reproducibles usando una copia legal local del
colaborador.
