# AGENTS.md — Reglas permanentes del proyecto Tekken 5 Native

Este archivo define las reglas de trabajo para **cualquier agente humano o
artificial** que contribuya a este repositorio. No es opcional. Si una
contribución viola estas reglas, debe corregirse antes de aceptarse.

Este proyecto es de **investigación e ingeniería inversa de larga duración**.
La velocidad nunca es más importante que la precisión.

---

## Regla 1 — No asumir

Ninguna suposición debe presentarse como un hecho.

Cada afirmación técnica relevante debe clasificarse con uno de estos niveles
de confianza (ver `docs/investigacion/metodologia.md`):

- `VERIFICADO`
- `MUY BIEN RESPALDADO`
- `PROBABLE`
- `HIPÓTESIS`
- `DESCONOCIDO`
- `PENDIENTE DE VERIFICACIÓN`

Frases como "el juego hace X" sin matizar su nivel de certeza **no están
permitidas** en `docs/` ni en `research/` cuando se refieren a
comportamiento interno de Tekken 5 que no ha sido comprobado directamente
sobre una copia retail.

## Regla 2 — Evidencia

Todo descubrimiento importante debe venir acompañado de evidencia
verificable: una herramienta usada, una captura, un volcado de memoria, un
commit, una URL, un hash, un log. "Lo leí en un foro" es una fuente válida
**solo si se cita como tal** y se marca con el nivel de confianza adecuado.

## Regla 3 — Documentación

Ningún descubrimiento importante vive solo en la cabeza del agente o en el
historial de chat. Si es relevante, se documenta en `research/hallazgos/`
con un identificador `TK5-XXXX` siguiendo la plantilla de
`docs/investigacion/metodologia.md`.

## Regla 4 — Reproducibilidad

Siempre que sea posible, un hallazgo debe venir con los pasos necesarios
para repetir el experimento: versión del juego, herramienta, versión de la
herramienta, comandos, direcciones de memoria, configuración de Ghidra, etc.

## Regla 5 — Versiones

Nunca mezclar información de NTSC-U, NTSC-J y PAL sin indicar explícitamente
a qué versión corresponde. Las direcciones de memoria, offsets del ELF y
estructuras **no son intercambiables entre regiones ni builds** (ver
`docs/investigacion/versiones-tekken5.md`).

## Regla 6 — Fuentes externas

Distinguir siempre:

- Información obtenida de **código fuente o documentación primaria**.
- Información obtenida de **herramientas de ingeniería inversa**
  (Ghidra, PCSX2, PS2Recomp, etc.) ejecutadas por nosotros.
- Información obtenida de **comunidades externas** (foros, wikis, cheats)
  que todavía no ha sido verificada de forma independiente.

Nunca presentar la tercera categoría como si fuera la primera.

## Regla 7 — Código externo

Antes de reutilizar código de otro proyecto (PS2Recomp, Ghidra extensions,
TekkenMovesetExtractor, God Hand Decomp, N64Recomp, etc.):

1. Comprobar su licencia real en el repositorio original.
2. Registrarla en `docs/investigacion/licencias.md`.
3. Confirmar que la licencia es compatible con la licencia de este
   repositorio (ver `LICENSE`).

No se debe copiar código sin este proceso, ni siquiera fragmentos pequeños.

## Regla 8 — Datos propietarios

Este repositorio **no debe contener nunca**:

- ISOs, BIN/CUE, CHD u otras imágenes de disco.
- El ELF, overlays o módulos IOP extraídos del juego.
- Texturas, modelos, animaciones, audio o vídeos extraídos del juego.
- BIOS de PlayStation 2.
- Cualquier dato derivado directamente de una copia del juego.

Las herramientas y scripts del repositorio deben operar sobre datos que el
**usuario** aporta localmente desde su propia copia legal, y nunca deben
subir, empaquetar o distribuir esos datos.

## Regla 9 — No implementar a ciegas

No se debe escribir código de sistemas complejos (renderizado, físicas,
IA, formatos de archivo) sin haber documentado primero la investigación que
lo sustenta. Si no hay evidencia suficiente, el siguiente paso es investigar,
no implementar.

## Regla 10 — README actualizado

El `README.md` raíz debe reflejar siempre el estado real del proyecto. Si
una fase avanza, se actualiza. Si una conclusión anterior se demuestra
incorrecta, se corrige inmediatamente, en el README y en la documentación
afectada. Nunca se deja una conclusión incorrecta "porque ya estaba escrita".

---

## Reglas adicionales de proceso

### Orden de prioridad de fuentes

1. Código fuente / repositorios originales.
2. Documentación técnica primaria.
3. Herramientas de ingeniería inversa ejecutadas por nosotros.
4. Scripts de Ghidra y extensiones específicas de PS2.
5. Código de emuladores (PCSX2, Play!).
6. Experimentos propios reproducibles.
7. Documentación de investigadores independientes.
8. Foros y comunidades.
9. Vídeos y fuentes secundarias.

Cuanto más abajo en la lista, mayor es la obligación de marcar la
información como no verificada.

### Qué NO hacer todavía

- No intentar construir el port completo.
- No escribir un motor nuevo sin necesidad demostrada.
- No reescribir el proyecto en Rust/Bevy (ver `future/rust-bevy/`, que es
  exclusivamente especulativo y no forma parte del desarrollo activo).
- No inventar estructuras, formatos, funciones o direcciones de memoria.
- No introducir ISOs, ROMs o assets del juego en el repositorio, ni en
  commits, issues, ni en archivos de ejemplo.
- No generar la falsa impresión de que existe un "port funcional" cuando
  no lo hay.

### Principio fundamental

> Entender primero. Verificar después. Documentar después. Implementar
> finalmente.

Cada agente que abra este repositorio debe poder responder, leyendo la
documentación:

- ¿Qué sabemos?
- ¿Cómo sabemos que es cierto?
- ¿Qué no sabemos?
- ¿Cómo podemos comprobarlo?
- ¿Qué está implementado?
- ¿Qué no funciona?
- ¿Qué se ha intentado y ha fallado?
- ¿Por qué se tomó cada decisión?
- ¿Cuál es el siguiente paso?

Si la documentación no permite responder a estas preguntas, la
documentación está incompleta, aunque el código compile.
