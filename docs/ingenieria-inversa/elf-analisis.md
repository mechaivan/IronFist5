# Análisis del ELF de Tekken 5

Sección 14 del encargo original. Este documento describe **qué
necesitamos determinar** sobre el ELF principal de Tekken 5 y **qué ya se
sabe de forma genérica** sobre la estructura de un ejecutable de PS2, sin
inventar ningún dato específico de Tekken 5 que no se haya verificado.

## Estructura esperada (genérica de cualquier ELF de PS2, no específica de Tekken 5)

```text
ISO (ISO9660, con extensiones específicas de PS2/Sony, no investigadas
     todavía en detalle en esta pasada)
 │
 ├── ELF principal (cargado por el kernel de PS2 según SYSTEM.CNF)
 │     ├── código EE (secciones .text)
 │     ├── datos (.data, .rodata)
 │     ├── BSS (.bss)
 │     ├── funciones (requieren identificación, ver workflow-ghidra.md)
 │     ├── strings
 │     ├── símbolos (posiblemente .mdebug/STABS, DESCONOCIDO si están
 │     │   presentes en Tekken 5, ver TK5-0008)
 │     └── overlays (posible, DESCONOCIDO todavía si Tekken 5 los usa)
 │
 ├── módulos IOP (archivos .IRX, DESCONOCIDO todavía cuáles usa Tekken 5)
 │
 ├── programas VU (microcódigo VU1, típicamente embebido en overlays o en
 │     el propio ELF; DESCONOCIDO todavía cómo los organiza Tekken 5)
 │
 └── recursos del juego (modelos, texturas, audio, etc. — ver
       research/filesystem/ y research/assets/)
```

## Qué está VERIFICADO de forma independiente del juego (hechos genéricos de PS2)

- El punto de entrada de un ejecutable de PS2 se referencia típicamente
  desde `SYSTEM.CNF` en la raíz del disco (archivo de arranque estándar de
  PS2, formato de texto plano con la línea `BOOT2 = cdrom0:\...\XXXXX.XX;1`
  entre otras). **No se ha leído todavía el `SYSTEM.CNF` real de ninguna
  ISO de Tekken 5** en esta pasada de investigación.
- El formato de archivo del ejecutable principal es un ELF MIPS de 32 bits
  little-endian estándar, lo cual es la razón por la que herramientas
  genéricas como `readelf`/`objdump` (con soporte MIPS) pueden leer su
  cabecera, secciones y segmentos sin necesidad de ninguna herramienta
  específica de PS2.

## Qué está DESCONOCIDO específicamente para Tekken 5 (requiere verificación directa)

- Entry point exacto (dirección).
- Lista completa de secciones y sus direcciones de carga.
- Tamaño y ubicación de `.bss`.
- Si existen overlays superpuestos en memoria (técnica común en juegos de
  PS2 para ahorrar RAM, cargando y descargando código bajo demanda).
- Si existe una sección `.mdebug` con símbolos STABS (ver TK5-0008) — esto
  es la pregunta de mayor impacto potencial para todo el proyecto, porque
  cambiaría radicalmente el costo de identificar funciones.
- Nombres de los módulos IOP (.IRX) que usa, si los incluye dentro del ELF,
  en un overlay, o como archivos sueltos en el filesystem del disco.
- Relocaciones presentes (relevante porque PS2Recomp usa información de
  relocación para auto-enlazar llamadas a funciones conocidas, ver
  `docs/investigacion/ps2recomp.md`).

## Procedimiento previsto para obtener esta información (sin herramientas específicas de PS2, como primer paso)

Estos comandos son estándar de cualquier toolchain binutils con soporte
MIPS, y no requieren ninguna herramienta específica de PS2 para una
primera pasada de reconocimiento (aunque la decompilación en sí sí
requiere Ghidra + extensión EE, ver `workflow-ghidra.md`):

```sh
file SLUS_210.59   # o el nombre real del ejecutable extraído
readelf -h SLUS_210.59    # cabecera: entry point, tipo de máquina, etc.
readelf -S SLUS_210.59    # tabla de secciones (buscar .mdebug aquí)
readelf -l SLUS_210.59    # tabla de segmentos/program headers
readelf -s SLUS_210.59    # tabla de símbolos, si existe
objdump -d SLUS_210.59    # desensamblado crudo (sin extensiones MMI/VU)
```

Nota: `objdump`/`readelf` estándar probablemente no decodifiquen
correctamente las instrucciones MMI y VU0 propias de la EE (son
extensiones no estándar del ISA MIPS); para eso es necesario Ghidra con la
extensión EE, o un desensamblador específico de PS2. Esto es una hipótesis
razonable basada en que MMI/VU0 son extensiones propietarias no
documentadas en el ISA MIPS genérico, pero no se ha confirmado
experimentalmente en esta pasada.

## Nombre de archivo esperado del ejecutable principal

Según las direcciones de cheats citadas en TK5-0009, el nombre de archivo
usado en notación de cheats antiguos es `SLUS_210.59` (con puntos en vez
de guion, convención típica de nombre de archivo real en el filesystem de
PS2 para el serial `SLUS-21059`). Esto es **consistente con la convención
de nomenclatura estándar de PS2** (los ejecutables en el filesystem suelen
llamarse igual que el serial pero con puntos), pero no se ha confirmado
leyendo directamente el `SYSTEM.CNF` de una ISO real en esta pasada.
Clasificación: PROBABLE, no VERIFICADO.

## Próximo paso real

Esta sección del proyecto pasa de "investigación documental" a
"investigación experimental propia" en cuanto un colaborador humano aporte
(localmente, sin subirla al repositorio) una copia legal de Tekken 5
NTSC-U y ejecute los comandos de arriba. El resultado debe documentarse
como un hallazgo `TK5-XXXX` nuevo, citando explícitamente el hash de disco
verificado (TK5-0002) usado para esa sesión de análisis.
