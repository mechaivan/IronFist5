# PCSX2 y Play! como herramientas de investigación

Ver hallazgos asociados: TK5-0015, TK5-0016.

Este documento trata los emuladores **exclusivamente como instrumento de
investigación** (para observar el comportamiento del juego original,
inspeccionar memoria, y validar hipótesis), no como el objetivo final del
proyecto. Ver `AGENTS.md` y la visión general en el `README.md` raíz.

## PCSX2

- Repositorio: `PCSX2/pcsx2`. Licencia: **GPL-3.0**.
- Es el emulador de PS2 de referencia de la comunidad, con el conjunto de
  herramientas de depuración más maduro conocido hasta ahora en esta
  investigación:
  - Depurador con desensamblador MIPS integrado.
  - Inspección y edición de memoria en vivo.
  - Breakpoints de ejecución y de acceso a memoria.
  - Ejecución paso a paso.
  - Save states (volcado y restauración de estado completo de la máquina
    virtual, útil para reproducir un escenario de combate exacto cada vez).
  - Un protocolo GDB Remote Serial Protocol para los procesadores EE e IOP
    por separado (confirmado indirectamente porque un proyecto de
    terceros, `snowyegret23/PCSX2_MCP`, construye un puente MCP apoyándose
    en este protocolo sin necesidad de parchear PCSX2).

### Usos previstos para este proyecto

1. **Volcados de RAM**: capturar los 32 MB de RAM de la EE en un momento
   concreto (p. ej., en medio de un combate) para buscar estructuras de
   datos con Cheat Engine o scripts propios, siguiendo el patrón descrito
   por guías de la comunidad (ver `suxin.space`, citada en TK5-0007, que
   recomienda explícitamente volcar RAM antes que usar punteros en vivo
   por estabilidad).
2. **Comparación de frames y estados**: usar save states como puntos de
   partida reproducibles para comparar el comportamiento del juego
   original contra una futura implementación nativa (ver
   `docs/desarrollo/testing-diferencial.md`).
3. **Localización de direcciones conocidas de la comunidad** (TK5-0009):
   cargar los parches widescreen/cheats citados y confirmar en el
   depurador de PCSX2 qué instrucción exacta ocupa cada dirección antes de
   asumir su propósito.
4. **Trazado de DMA/VIF/GIF** (pendiente de investigar en profundidad qué
   expone exactamente el depurador de PCSX2 para esto) para responder a la
   pregunta de la sección 7 del encargo original: qué partes de la
   arquitectura usa realmente Tekken 5.

### Herramientas MCP relacionadas (contexto, no adoptadas todavía)

`hkmodd/PCSX2-MCP` y `snowyegret23/PCSX2_MCP` exponen el depurador de
PCSX2 a asistentes de IA vía Model Context Protocol. Se documentan como
referencia (TK5-0016) pero no se han auditado ni adoptado en este
proyecto; cualquier adopción futura debe pasar primero por revisión de
licencia y de seguridad (recordar que exponen lectura/escritura de memoria
de un proceso, lo cual no es inocuo).

## Play!

- Repositorio: `jpd002/Play-`.
- HLE (High-Level Emulation) del BIOS: no requiere que el usuario aporte un
  dump de BIOS real, a diferencia de PCSX2.
- Multiplataforma: Windows, macOS, Linux, Android, iOS, navegador.
- Compatibilidad reportada por la comunidad como inferior a PCSX2 ("half of
  the commercial titles will run" según emulation.gametechwiki.com).
- Licencia: fuentes secundarias discrepan entre BSD-2-Clause y MIT (ver
  TK5-0015); pendiente de confirmar contra el archivo `LICENSE` real del
  repositorio antes de cualquier decisión que dependa de ello.

### Rol previsto

Principalmente exploratorio/comparativo: si Play! consigue ejecutar Tekken
5 con una arquitectura de emulación más simple y de código más legible
(por ser HLE, no requiere la complejidad de LLE de PCSX2 para el BIOS),
podría servir como referencia secundaria más fácil de leer para entender
el arranque del juego. **No se ha probado todavía en este proyecto si
Play! ejecuta Tekken 5 en absoluto.**

## Qué NO vamos a hacer con estos emuladores

- No vamos a construir el port "sobre" PCSX2 ni sobre Play!: son
  herramientas de investigación temporales, no una dependencia del
  producto final (ver visión del proyecto en el `README.md`).
- No vamos a distribuir BIOS, ISOs, ni volcados de memoria derivados del
  juego en este repositorio (Regla 8 de `AGENTS.md`).

## Preguntas abiertas

- ¿Qué opciones concretas de trazado de DMA/GIF/VIF expone el depurador de
  PCSX2 en su versión estable actual? (PENDIENTE DE VERIFICACIÓN, requiere
  instalar PCSX2 y explorar su UI/API de depuración directamente)
- ¿Tekken 5 arranca en Play!? ¿Con qué nivel de fidelidad? (DESCONOCIDO)
- ¿Cuál es la licencia exacta de Play!? (PENDIENTE DE VERIFICACIÓN, ver
  TK5-0015)

## Fuentes

- https://github.com/hkmodd/PCSX2-MCP
- https://github.com/snowyegret23/PCSX2_MCP
- https://emulation.gametechwiki.com/index.php/Play!
- https://sourceforge.net/projects/play.mirror/
- https://suxin.space/notes/tracking-down-playstation-pointers-using-debuggers-ghidra/
