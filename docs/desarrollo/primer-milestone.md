# Primer milestone técnico propuesto

Sección 19 del encargo original. Este documento propone, de forma
razonada, cuál debería ser el primer objetivo técnico concreto y
demostrable del proyecto, una vez completada la fase de investigación
inicial.

## Progresión prevista

```text
ELF (NTSC-U, SLUS-21059, ver TK5-0018)
 ↓
Ghidra + extensión R5900/PS2 (docs/ingenieria-inversa/workflow-ghidra.md)
 ↓
Identificación de al menos un pequeño conjunto de funciones reales
 ↓
Exportación a TOML/CSV para PS2Recomp
 ↓
PS2Recomp genera C++ para esas funciones
 ↓
Compilación del C++ generado junto con ps2xRuntime
 ↓
Ejecución del runtime mínimo, invocando esas funciones recompiladas
 ↓
Verificación de que el resultado (valores de registros/memoria) coincide
con el comportamiento observado en PCSX2 para la misma entrada
```

## Propuesta de criterio de éxito del primer milestone

**No se propone que el primer milestone tenga gráficos.** Siguiendo
explícitamente la sección 19 del encargo original, el primer milestone
propuesto es:

> Lograr que una función real, no trivial, del ELF de Tekken 5 NTSC-U
> (por ejemplo, una función pura de cálculo, sin dependencias de GS/VU1 —
> idealmente algo como una función matemática, de validación de datos, o
> de gestión de una tabla simple) sea identificada en Ghidra, recompilada
> con PS2Recomp, compilada, y ejecutada en el runtime de PS2Recomp,
> produciendo un resultado que se pueda comparar y verificar contra el
> comportamiento observado para la misma función en PCSX2 con la misma
> entrada.

Esto es deliberadamente modesto. Es un hito de **demostración de la
cadena de herramientas completa funcionando de extremo a extremo sobre
Tekken 5 específicamente**, no un hito de jugabilidad.

## Por qué este criterio y no uno más ambicioso

1. Según TK5-0006, PS2Recomp tiene rendimiento y soporte pobres para
   GS/VU — cualquier milestone que dependa de ver algo en pantalla
   requeriría resolver primero una cantidad de trabajo no cuantificada de
   emulación de hardware gráfico, lo cual no es razonable como "primer"
   hito.
2. Según TK5-0017, no existe ningún trabajo previo específico de Tekken 5
   sobre el que apoyarse: el primer hito debe validar que la cadena de
   herramientas (Ghidra → PS2Recomp → runtime) funciona en absoluto sobre
   este binario concreto, antes de invertir esfuerzo en sistemas más
   complejos.
3. Es verificable de forma objetiva (comparación de valores de registros/
   memoria contra PCSX2), no depende de juicio subjetivo ("se ve bien").

## Qué NO es este milestone

- No es un menú funcional.
- No es un combate jugable.
- No es siquiera necesariamente una función relacionada con gameplay — puede
  ser una función de utilidad interna, siempre que sea real (extraída del
  ELF real, no inventada) y no trivial (más de una instrucción, con al
  menos una rama condicional o un bucle).

## Condición de bloqueo actual

Este milestone está bloqueado hasta completar:

1. Acceso local (por parte de un colaborador humano, con una copia legal)
   al ELF de Tekken 5 NTSC-U.
2. Instalación y configuración de Ghidra + extensión EE
   (`docs/ingenieria-inversa/workflow-ghidra.md`).
3. Compilación de PS2Recomp (`docs/investigacion/ps2recomp.md`, sección
   "Build": CMake 3.20+, compilador C++20).

Ninguno de estos tres pasos se ha completado todavía dentro de este
proyecto (a fecha de esta documentación, 2026-10-02).
