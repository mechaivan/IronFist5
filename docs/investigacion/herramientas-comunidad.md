# Herramientas de la comunidad de Tekken

Ver hallazgos asociados: TK5-0010, TK5-0011, TK5-0019.

Plantilla usada (sección 11 del encargo original):

```text
Nombre:
Repositorio:
Página:
Juegos compatibles:
Versión de Tekken compatible:
Entrada:
Salida:
Formatos:
Código fuente:
Licencia:
Estado:
Utilidad para este proyecto:
Limitaciones:
```

---

### TekkenMovesetExtractor (obsoleto, reemplazado por TKMovesets)

```text
Nombre: TekkenMovesetExtractor
Repositorio: https://github.com/Kiloutre/TekkenMovesetExtractor
Página: https://tekkenmods.com/mod/2365/tekkenmovesetextractor-for-tekken-7
Juegos compatibles (según su propia página de distribución): Tekken 7
  (desde Season 2), Tekken Tag Tournament 2, Tekken Revolution, Tekken 6,
  Tekken 5, Tekken 3DS
Versión de Tekken compatible: El README inspeccionado SOLO documenta en
  detalle el flujo para Tekken 7 (lectura/escritura de memoria en vivo del
  proceso del juego en PC) y Tag 2 vía CEMU (emulador de Wii U). El
  mecanismo exacto para "Tekken 5" NO está documentado en el texto
  disponible del README (ver TK5-0011) — PENDIENTE DE VERIFICACIÓN si
  implica PS2/PCSX2 en absoluto.
Entrada: Memoria de proceso en vivo (Tekken 7, vía Pywin32) o memoria de
  emulador (Tag 2 vía CEMU)
Salida: JSON + datos de animación en una carpeta `extracted_chars/`
Formatos: Formato propio del proyecto (moveset como JSON), no un formato
  nativo de ningún juego de PS2
Código fuente: Python, disponible completo en el repositorio (archivado,
  solo lectura desde 2023)
Licencia: GPL-3.0 (confirmada en la página del repositorio)
Estado: Archivado por su autor ("THIS PROJECT IS OBSOLETE"), reemplazado
  por https://github.com/Kiloutre/TKMovesets (no inspeccionado en
  profundidad en esta pasada)
Utilidad para este proyecto: Baja/incierta hasta aclarar el mecanismo real
  de soporte de "Tekken 5" — si resulta ser compatible solo con una
  reimplementación del moveset dentro de Tekken 6/7, no es aplicable
  directamente al binario PS2 original (Regla 6 de AGENTS.md: no asumir
  que estructuras de otro juego son idénticas a Tekken 5 PS2)
Limitaciones: Requiere el juego en ejecución (no es un extractor de
  archivos estático); el propio autor lo considera obsoleto; no hay
  documentación textual confirmada de un flujo PS2/PCSX2
```

### csplitb + Noesis (extracción de la versión arcade Tekken 5.1)

```text
Nombre: csplitb (script) + Noesis (visor/convertidor)
Repositorio de csplitb: No localizado como repositorio propio verificado
  en esta pasada (referenciado como herramienta externa en el tutorial de
  tekkenmods.com, enlace no re-verificado todavía)
Página: https://tekkenmods.com/article/48/extracting-vanilla-tekken-5-assets-for-modding
Juegos compatibles: Tutorial escrito específicamente para datos extraídos
  de un CHD de la versión arcade "Tekken 5.1 Ver. B" (placa Namco, no PS2)
Versión de Tekken compatible: Arcade Tekken 5.1 — explícitamente NO la
  versión retail de PS2, que según el mismo tutorial tiene escenarios y
  personajes "obfuscados" (ver TK5-0010)
Entrada: Archivos .BIN extraídos de un CHD de MAME (vía `chdman`)
Salida: Archivos separados por cabecera mágica (.nud para modelos NUDP,
  .tm2 para texturas TIM2)
Formatos: NUDP (contenedor de modelo), TIM2 (textura, formato de Sony
  usado ampliamente en PS2/PS3), MIF (interpretación de "datos de hueso"
  no confirmada por el propio tutorial)
Código fuente: Noesis es de Rich Whitehouse, con plugins en Python de
  terceros; csplitb no se ha podido confirmar como proyecto con código
  fuente propio auditable en esta pasada
Licencia: No verificada (Noesis es gratuito para uso personal según su
  distribución habitual, pero no se ha confirmado licencia de
  redistribución de sus plugins de terceros)
Estado: Tutorial de comunidad, sin indicación de mantenimiento activo
Utilidad para este proyecto: Indirecta — confirma formatos de contenedor
  potencialmente reutilizables (TIM2 es un formato bien documentado en
  general) pero sobre la versión equivocada del juego para nuestro
  objetivo (ver TK5-0018, trabajamos sobre PS2 retail NTSC-U)
Limitaciones: No aplicable directamente al filesystem de PS2 retail sin
  verificación; los propios autores señalan huecos (sin texturas
  asignadas, sin esqueleto reconocible, archivos corruptos ocasionales)
```

### Noesis (herramienta genérica)

```text
Nombre: Noesis
Repositorio: Cerrado/propietario (distribución gratuita por el autor,
  Rich Whitehouse); existen plugins de terceros en Python de código
  abierto variable
Página: Sitio del autor (no re-verificado en esta pasada)
Juegos compatibles: Muy amplio catálogo mediante plugins específicos por
  formato; no es una herramienta específica de Tekken
Versión de Tekken compatible: Depende exclusivamente del plugin usado;
  ningún plugin específico de Tekken 5 PS2 retail ha sido confirmado en
  esta pasada
Entrada/Salida: Variable según plugin; exporta habitualmente a .obj/.fbx
Formatos: Variable según plugin instalado
Código fuente: El núcleo de Noesis es cerrado; los plugins .py son
  frecuentemente de código abierto individual (sin licencia uniforme)
Licencia: Variable, debe comprobarse plugin por plugin
Estado: Activamente usado por la comunidad de modding de múltiples juegos
Utilidad para este proyecto: Potencialmente alta como visor de verificación
  una vez que tengamos un parser propio de los formatos reales del
  filesystem de Tekken 5 PS2 (todavía no determinados, ver
  research/filesystem/README.md), pero no debe asumirse que un plugin
  existente ya cubre Tekken 5 PS2 retail sin comprobarlo
Limitaciones: Dependencia de un núcleo cerrado; variabilidad de calidad y
  licencia entre plugins de terceros
```

## Conclusión de esta sección

Ninguna herramienta de la comunidad examinada hasta ahora confirma, con
evidencia directa, soporte para **extraer assets o movesets directamente
del filesystem/ejecutable de la versión retail de PS2** de Tekken 5. Las
herramientas más citadas (TekkenMovesetExtractor) operan sobre memoria en
vivo de juegos posteriores, y el tutorial de extracción de assets usa la
versión arcade, no la de PS2. Esto refuerza la conclusión de TK5-0017: la
ingeniería inversa específica de Tekken 5 PS2 retail es, en gran medida,
terreno inexplorado públicamente, y este proyecto deberá desarrollar sus
propias herramientas de análisis de filesystem y assets desde una base
mínima (ver `research/filesystem/README.md` y `research/assets/README.md`).
