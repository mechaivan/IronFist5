# Artefactos de investigación y exclusiones

Este documento define qué puede permanecer en el repositorio cuando comience
el trabajo con la copia legal local de `SLUS-21059`.

## No versionar nunca

- ISO, BIN/CUE, CHD u otra imagen de disco
- ELF retail, overlays, IRX o módulos extraídos
- BIOS, save states y volcados completos de memoria
- texturas, modelos, animaciones, audio, vídeo o paquetes extraídos
- proyectos Ghidra que embeban el ELF o datos propietarios
- salidas de herramientas que permitan reconstruir directamente esos datos

## Artefactos permitidos, tras revisión

- comandos y versiones de herramientas
- hashes y metadatos de entrada
- notas de análisis sin bytes propietarios
- mapas de funciones, si contienen sólo direcciones, nombres y metadatos
- configuraciones reproducibles que usen rutas locales externas
- logs resumidos y resultados numéricos no propietarios
- scripts que reciban rutas suministradas por el usuario
- casos de prueba sintéticos y fixtures creados por el proyecto
- hallazgos con evidencia y limitaciones claramente descritas

## Convención de rutas locales

Las instrucciones deben asumir una variable o argumento local, por ejemplo:

```text
$IRONFIST5_ELF=/ruta/local/al/ELF
```

Nunca deben asumir que el ELF existe dentro del checkout ni incluir una ruta
que dependa del entorno de otro colaborador.

## Criterio de revisión

Antes de cada commit generado por Ghidra, PS2Recomp o PCSX2, revisar el
contenido con `git diff --stat`, `git status` y una inspección de archivos.
Ante la duda, conservar sólo documentación reproducible y eliminar del
commit el artefacto derivado.
