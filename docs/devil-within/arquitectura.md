# Devil Within — arquitectura

## Estado de conocimiento

No hay todavía una arquitectura interna confirmada para Devil Within. Este
documento es un marco de trabajo, no una descripción de hechos del juego.

## Preguntas de investigación

- ¿Qué módulos y funciones son compartidos con el modo principal de Tekken 5?
- ¿Qué subsistemas tienen variantes específicas para Devil Within?
- ¿Existe un flujo de carga o streaming de escenarios distinto?
- ¿Cómo se relacionan sus entidades, enemigos y estados con las estructuras
generales del juego?
- ¿Qué partes dependen de EE, VU, GS, IOP o servicios de disco?
- ¿Hay puntos de entrada identificables en el ELF de `SLUS-21059`?

## Método

1. Extraer localmente el ELF desde una copia legal, sin incorporarlo al
   repositorio.
2. Registrar versión, hash y comandos de análisis.
3. Crear un mapa de funciones en Ghidra sin subir el proyecto que contenga
   datos propietarios.
4. Comparar llamadas, datos y flujo con los estados observados en PCSX2.
5. Registrar cada conclusión como `DW-XXXX` u otra familia apropiada,
   indicando nivel de confianza.

## Separación de certeza

Una función cuyo nombre sugiera Devil Within no prueba por sí sola que sea
exclusiva de ese modo. La exclusividad requiere evidencia adicional y debe
marcarse como `PROBABLE`, `HIPÓTESIS` o `VERIFICADO` según corresponda.
