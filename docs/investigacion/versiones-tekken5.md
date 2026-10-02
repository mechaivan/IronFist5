# Versiones de Tekken 5 (PS2)

Ver también los hallazgos originales: TK5-0001, TK5-0002, TK5-0003,
TK5-0004, TK5-0018.

## Resumen

Tekken 5 se publicó en PlayStation 2 en 2005 con al menos tres ejecutables
EE distintos, uno por región principal. No son el mismo binario: difieren
en fecha de compilación y número de versión de producto.

| Región | Serial principal | Otras ediciones con el mismo serial base | EXE date | Versión | Tamaño ISO (bytes) | CRC-32 | MD5 |
|---|---|---|---|---|---|---|---|
| NTSC-U | `SLUS-21059` | `SLUS-21059GH` (Greatest Hits) | 2005-02-08 | 1.00 | 4 483 547 136 | `b1c8b5a6` | `7472a628307a0e4309aef66c14d6dbc4` |
| NTSC-J | `SLPS-25510` | `SLPS-73223` ("the Best"), `SCAJ-20125` | 2005-03-07 | 1.01 | 4 077 191 168 | `aadc8c14` | `246ea391261c89d979cb6d2699f87ae2` |
| PAL | `SCES-53202` | `SCES-53202/P` (Platinum), `/ANZ`, `/GER` | 2005-05-10 | 1.00 | 4 100 685 824 | `b49f5c1c` | `bc0685727cf9d68e04da3e166b33016e` |

Fuente primaria de esta tabla: redump.org (ver TK5-0002 para SHA-1
completos y enlaces).

Hay además variantes regionales asiáticas (`SCKA-20049`/`SCKA-20081`,
Corea) que no se han investigado en detalle en esta pasada.

## Fechas de lanzamiento comercial (distintas de la fecha de compilación)

Según GameFAQs/retroplace (fuentes secundarias de catálogo, no primarias
de hash):

- NTSC-U: 24 de febrero de 2005.
- NTSC-J: 31 de marzo de 2005.
- PAL (Europa): 24 de junio de 2005 (una fuente) / fecha de compilación
  10 de mayo de 2005 según redump — la fecha de EXE siempre precede a la
  fecha de lanzamiento comercial, como es de esperar.

## Por qué estos tres ejecutables probablemente no son idénticos

1. Fechas de compilación separadas por más de tres meses (NTSC-U a PAL).
2. Número de versión de producto distinto: NTSC-J es "1.01" frente a
   "1.00" de NTSC-U y PAL, lo que normalmente indica al menos una revisión
   de corrección de errores adicional.
3. Direcciones de memoria distintas documentadas por parches widescreen de
   la comunidad entre NTSC-U y PAL para, aparentemente, el mismo efecto
   (ver TK5-0009) — evidencia indirecta pero consistente con builds
   distintos, no una prueba definitiva por sí sola.
4. Tamaños de ISO distintos (NTSC-J es el más pequeño en casi 400 MB
   respecto a NTSC-U), lo cual puede deberse a diferencias de doblaje de
   voces, compresión de vídeo, o contenido incluido — **no investigado a
   fondo todavía**.

Ninguna de estas diferencias se ha cuantificado función por función. Eso
requiere extraer los tres ELF y compararlos con Ghidra (ver
`docs/ingenieria-inversa/workflow-ghidra.md`), tarea pendiente.

## Contenido del disco más allá del ejecutable principal

La ficha de redump.org del disco NTSC-J lista explícitamente contenido
adicional: Tekken, Tekken 2 Ver. B, Tekken 3 y Starblade (ver TK5-0004).
Esto es consistente con el modo "Arcade History" anunciado como
característica de producto de Tekken 5 en todas las regiones, pero **solo
se ha confirmado mediante metadatos de catálogo para la edición NTSC-J**;
no se ha confirmado el mismo campo para NTSC-U ni PAL en esta pasada.

Esto implica que el "Tekken 5 ELF" no es necesariamente un único
ejecutable: es plausible (pero no confirmado) que existan ejecutables o
overlays separados para:

- El modo principal de Tekken 5 (el "juego" propiamente dicho).
- "The Devil Within" (modo historia tipo beat'em up).
- Los tres arcades emulados/portados de generaciones anteriores.
- Starblade (en el disco NTSC-J al menos).

Esto debe verificarse inspeccionando directamente el filesystem ISO9660 de
una copia legal (ver `research/filesystem/README.md`).

## Versión canónica elegida para este proyecto

Ver TK5-0018: se trabaja sobre **NTSC-U, SLUS-21059, versión 1.00, EXE date
2005-02-08**. Cualquier dato de memoria, offset o estructura documentado en
este repositorio sin indicar región se asume referido a esta versión; si no
es así, debe decirse explícitamente.

## Preguntas abiertas

- ¿Qué cambió exactamente entre NTSC-U 1.00 y NTSC-J 1.01? (DESCONOCIDO)
- ¿Por qué el build PAL es tan posterior (3 meses) al NTSC-U? ¿Localización
  de voces, corrección de bugs, ambos? (DESCONOCIDO)
- ¿El contenido de "Arcade History" es bit-idéntico entre regiones o cada
  región incluye su propia versión regional de los arcades clásicos?
  (DESCONOCIDO)
- ¿Existen builds de desarrollo/prototipo filtrados de Tekken 5 (como
  ocurre con otros juegos de la época)? No se ha buscado explícitamente en
  esta pasada. (PENDIENTE DE INVESTIGACIÓN)
