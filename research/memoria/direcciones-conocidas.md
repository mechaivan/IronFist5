# Direcciones de memoria conocidas (EE) — Tekken 5

Plantilla usada (sección 12 del encargo original):

```text
Versión:
Dirección:
Valor conocido:
Comportamiento:
Fuente:
Cómo se descubrió:
Interpretación actual:
Nivel de confianza:
```

Todas las entradas de esta tabla proceden, por ahora, de **fuentes de
comunidad** (cheats/parches), no de verificación propia. Ver TK5-0009 para
el hallazgo que respalda esta sección completa.

---

```text
Versión: NTSC-U (SLUS-21059 / SLUS_210.59)
Dirección: 0x0032b448 (EE, notación "Code Breaker" 0x2032b448)
Valor conocido: 0x3c013f40 (parche), valor original desconocido (no
  capturado por la fuente)
Comportamiento: Parte de un parche de "widescreen" (FOV de cámara),
  atribuido por la fuente a "nemesis2000"
Fuente: https://www.ps2-home.com/forum/viewtopic.php?t=2680
Cómo se descubrió: Desconocido (no documentado por la fuente; típicamente
  este tipo de parche se descubre comparando FOV en distintos modos o
  interceptando escrituras a registros de cámara)
Interpretación actual: Posible dirección de código relacionada con el
  cálculo de FOV de la cámara de combate
Nivel de confianza: PENDIENTE DE VERIFICACIÓN
```

```text
Versión: PAL (SCES-53202)
Dirección: 0x00340bb0 (EE)
Valor conocido: 0x3c013f40 (parche)
Comportamiento: Mismo parche conceptual que la entrada anterior, pero
  portado a PAL ("Ported to PAL (elhecht)")
Fuente: https://www.ps2-home.com/forum/viewtopic.php?t=1131
Cómo se descubrió: Desconocido (adaptación manual desde la versión NTSC-U)
Interpretación actual: Confirma que la misma función conceptual vive en
  una dirección distinta en el build PAL respecto al NTSC-U (consistente
  con TK5-0003: son binarios distintos)
Nivel de confianza: PENDIENTE DE VERIFICACIÓN
```

```text
Versión: NTSC-U (SLUS-21059)
Dirección: 0x203E4568 (notación con prefijo de región de memoria tipo
  "20" + offset 0x3E4568)
Valor conocido: 0xFFFFFFFF (parche de "desbloquear todos los personajes
  estándar")
Comportamiento: Citado de forma consistente en al menos dos fuentes
  independientes de cheats (Scribd/Codejunkies y un hilo de ngemu.com de
  2006 atribuido a "redlofredlof"/"Code Master")
Fuente:
  - https://www.scribd.com/document/821716554/SLUS-21059-pnach
  - https://www.ngemu.com/threads/convert-code-breaker-cheats-to-pnach-files.75097/page-10
Cómo se descubrió: Desconocido (no documentado por ninguna de las dos
  fuentes)
Interpretación actual: Probable dirección de una tabla o bitmask de
  personajes desbloqueados en memoria (estructura de progreso del juego)
Nivel de confianza: PENDIENTE DE VERIFICACIÓN (dos fuentes independientes
  coinciden en la misma dirección y valor, lo cual aumenta la plausibilidad,
  pero sigue sin verificación propia de este proyecto)
```

## Próximos pasos

Ver `docs/desarrollo/backlog.md`, sección "Memoria": verificar al menos una
de estas direcciones directamente en el depurador de PCSX2 contra una copia
legal, y solo entonces promover la entrada a `VERIFICADO` o `MUY BIEN
RESPALDADO` en un hallazgo `TK5-XXXX` dedicado.
