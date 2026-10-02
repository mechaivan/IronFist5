# Problemas técnicos conocidos

Lista de problemas identificados hasta ahora, con referencia al hallazgo
que los sustenta. Esta lista debe revisarse y ampliarse conforme avance la
investigación; no debe usarse para justificar inacción, sino para
priorizar correctamente el trabajo.

## 1. No existe trabajo previo específico de Tekken 5 sobre el que apoyarse

Referencia: TK5-0017. El proyecto parte, en la práctica, de cero en lo que
respecta a ingeniería inversa específica de este título en PS2. Las
herramientas disponibles (PS2Recomp, Ghidra+extensión EE) son de propósito
general.

## 2. PS2Recomp es experimental y tiene rendimiento pobre en GS/VU

Referencia: TK5-0006. Es razonable esperar que Tekken 5, como juego de
lucha 3D, dependa significativamente de VU1/GS para personajes y
escenarios. Esto implica que el camino de "solo recompilar y listo" no es
viable para el renderizado sin trabajo adicional sustancial (muy
probablemente reimplementación, ver
`docs/arquitectura/decompilacion-vs-recompilacion.md`).

## 3. Desconocemos si el ELF tiene símbolos de depuración

Referencia: TK5-0008. Esto es, probablemente, el factor individual que más
impacto tendrá en el costo total del proyecto. Si existen símbolos
`.mdebug`/STABS, gran parte del trabajo de identificación de funciones
podría automatizarse con `ccc` y el analizador STABS de
`ghidra-emotionengine-reloaded`. Si no existen, el trabajo de
identificación será mucho más manual y lento.

## 4. Las tres versiones regionales no son intercambiables

Referencia: TK5-0001, TK5-0002, TK5-0003. Cualquier dato de memoria u
offset descubierto debe anclarse explícitamente a una versión concreta
(se ha elegido NTSC-U como canónica, TK5-0018), y no puede asumirse válido
para las otras dos sin re-verificación.

## 5. El filesystem/assets retail parecen estar ofuscados o comprimidos

Referencia: TK5-0010. La única evidencia de extracción de assets
encontrada hasta ahora corresponde a la versión arcade (Tekken 5.1), no a
la versión PS2 retail, y según esa misma fuente, el retail tiene los
escenarios y personajes "obfuscados", con la excepción de "The Devil
Within". Esto implica que, incluso si identificamos el formato de
contenedor correcto, puede haber una capa adicional de compresión u
ofuscación que debe entenderse antes de poder leer los assets reales.

## 6. No está claro si existe algún proyecto de terceros no indexado que debamos conocer

Referencia: TK5-0017 (hallazgo negativo). Siempre existe el riesgo de que
un esfuerzo privado o insuficientemente indexado exista y no lo hayamos
encontrado. Mitigación: preguntar directamente en comunidades
especializadas (ver backlog).

## 7. Licencias de varias herramientas de interés no están confirmadas

Referencia: `docs/investigacion/licencias.md` (entradas marcadas "NO
VERIFICADA" o "PENDIENTE DE VERIFICACIÓN": `beardypig/ghidra-emotionengine`,
`chaoticgd/ccc`, `LucasPicoli/god-hand-decomp`, licencia exacta de Play!).
Esto bloquea cualquier decisión de reutilización de código de esos
proyectos hasta confirmarlo.

## 8. Toolchain de PS2Recomp probado principalmente con MSVC

Referencia: TK5-0005 (sección "Requirements" del README de PS2Recomp,
"currently tested mainly with MSVC"). Si el equipo de desarrollo
multiplataforma objetivo incluye Linux/macOS, esto es un riesgo de
portabilidad a evaluar, no confirmado como bloqueante ni como no
bloqueante todavía.

## Cómo se usa esta lista

Cada problema aquí listado debe tener, idealmente, una o más tareas
correspondientes en `docs/desarrollo/backlog.md` orientadas a reducir la
incertidumbre que lo rodea, siguiendo el principio fundamental del
proyecto: reducir la incertidumbre antes de implementar.
