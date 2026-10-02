# Lista de incógnitas (qué no sabemos todavía)

Esta lista es deliberadamente honesta y, a día de hoy, larga. Es el
inventario de preguntas abiertas más importante del proyecto. Cada entrada
debería, eventualmente, resolverse en un hallazgo `TK5-XXXX` que la
reemplace por una respuesta verificada (o la reclasifique si se demuestra
irrelevante).

## Sobre el ELF y el ejecutable

- ¿Cuál es el entry point exacto del ELF de NTSC-U?
- ¿Tiene secciones `.mdebug`/STABS? (La pregunta de mayor impacto del
  proyecto, ver TK5-0008 y problema conocido #3)
- ¿Usa overlays? ¿Cuántos, y para qué subsistemas?
- ¿Qué cambió concretamente entre el build NTSC-U 1.00 y el NTSC-J 1.01?
- ¿Por qué el build PAL es tan posterior (3 meses)?

## Sobre la arquitectura de PS2 usada

- ¿Usa VU1 en modo micro, y para qué (geometría, skinning, ambos)?
- ¿Qué proporción de animación/física corre en VU0 frente a en la EE?
- ¿Qué módulos IOP (.IRX) carga, y son módulos estándar de Sony o módulos
  propios de Namco?
- ¿Usa la IPU para vídeo?
- ¿Cómo gestiona el timing de combate (interrupciones de hardware,
  temporizadores del kernel, o un bucle propio)?

## Sobre el filesystem y los assets

- ¿Cuál es la estructura real de directorios/archivos del ISO9660 de la
  versión PS2 retail?
- ¿Usa el mismo formato de contenedor (NUDP/TIM2) que la versión arcade
  Tekken 5.1, o uno distinto?
- ¿Qué tipo exacto de "ofuscación"/compresión tienen los escenarios y
  personajes del modo principal (más allá de "The Devil Within")? ¿Es
  compresión genérica (LZ, etc.) o algo propietario?
- ¿Cómo se almacenan las animaciones? ¿En qué formato, y compartido entre
  personajes o por personaje?
- ¿Cómo se definen hitboxes/hurtboxes? ¿Como parte de los datos de
  animación, como una estructura de datos separada, o calculadas en
  tiempo de ejecución a partir de la geometría?

## Sobre gameplay

- ¿Cómo está implementada la IA de los oponentes controlados por CPU?
- ¿Usa algún RNG interno? ¿Dónde y con qué alcance (solo estética, o
  también mecánicas de combate)?
- ¿Cómo funciona exactamente "The Devil Within" a nivel de código —
  comparte motor con el modo principal o es sustancialmente distinto?
- ¿Los tres arcades incluidos (Tekken, Tekken 2 Ver. B, Tekken 3) corren
  sobre una emulación de su hardware arcade original embebida en el disco,
  o son ports/reimplementaciones hechas para esta recopilación? (No
  investigado en esta pasada)

## Sobre herramientas y comunidad

- ¿Qué mecanismo usa exactamente TekkenMovesetExtractor para su supuesto
  soporte de "Tekken 5"? (TK5-0011)
- ¿Existe algún esfuerzo de ingeniería inversa de Tekken 5 PS2 no indexado
  públicamente (por ejemplo, en un Discord privado de modding)?
- ¿Cuál es la licencia exacta de Play!, `ghidra-emotionengine` (original),
  `ccc`, y `god-hand-decomp`?

## Cómo se prioriza resolver estas incógnitas

Ver `docs/desarrollo/backlog.md` para tareas concretas derivadas de esta
lista, ordenadas aproximadamente por impacto potencial en el resto del
proyecto (empezando por la pregunta de los símbolos `.mdebug`, que
condiciona el costo de casi todo lo demás).
