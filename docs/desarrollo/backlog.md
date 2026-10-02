# Backlog de investigación y desarrollo

Sección 27 del encargo original. Tareas concretas, no vagas. Cada tarea
debe poder marcarse como completada con un resultado verificable (un
hallazgo `TK5-XXXX`, un documento actualizado, o un artefacto de
herramienta). Formato: `[ ]` pendiente, `[x]` completada (con referencia al
resultado).

## Investigación

- [ ] Consultar directamente psdevwiki.com para contrastar
      `docs/ps2/arquitectura-ee.md` contra documentación técnica de
      desarrollo homebrew, no solo fuentes de especificación general.
- [ ] Investigar específicamente "The Devil Within" como posible sistema de
      juego diferenciado (motor, assets, IA) de forma independiente del
      modo Tekken 5 principal.
- [ ] Buscar explícitamente documentación o ingeniería inversa de la IA de
      oponentes CPU de Tekken 5 (no encontrado nada en la primera pasada,
      TK5-vacío — registrar como hallazgo negativo si se repite la
      búsqueda sin éxito).
- [ ] Preguntar en comunidades especializadas (Tekken modding Discord
      mencionado en la página de TekkenMovesetExtractor, foros de PS2 RE)
      si existe algún esfuerzo de ingeniería inversa de Tekken 5 PS2 no
      indexado públicamente.
- [ ] Investigar "PSRetrox" y "PS2 Decompiler Toolkit" con búsquedas
      dirigidas adicionales (no localizados en la primera pasada, ver
      `docs/investigacion/proyectos-similares.md`).

## Ingeniería inversa (requiere copia legal local del colaborador)

- [ ] Extraer el `SYSTEM.CNF` y el ELF principal de una ISO legal NTSC-U
      verificada contra el hash de TK5-0002, documentando el nombre real
      de archivo del ejecutable.
- [ ] Ejecutar `readelf -h/-S/-l/-s` sobre el ELF extraído y documentar el
      resultado completo como un hallazgo nuevo `TK5-XXXX`.
- [ ] Determinar si existe una sección `.mdebug` (pregunta de máximo
      impacto, ver problema conocido #3).
- [ ] Listar el contenido de nivel superior del ISO9660 (sin extraer
      archivos individuales todavía) y documentar nombres/tamaños.
- [ ] Repetir los puntos anteriores para NTSC-J y PAL una vez cubierto
      NTSC-U, para poder cuantificar por primera vez las diferencias reales
      entre builds (más allá de la fecha de compilación).

## PS2

- [ ] Instrumentar una sesión de juego real en PCSX2 (menú y un combate
      corto) con su depurador, registrando qué canales DMA/VIF/GIF se
      activan, como primer dato real para responder las preguntas de
      `docs/ps2/arquitectura-ee.md`.
- [ ] Confirmar si PCSX2 soporta grabación/reproducción determinista de
      inputs, como requisito para `docs/desarrollo/testing-diferencial.md`.

## Ghidra

- [ ] Instalar Ghidra y `chaoticgd/ghidra-emotionengine-reloaded`,
      confirmando la versión exacta usada de cada uno (registrar en este
      backlog o en un hallazgo).
- [ ] Importar el ELF de NTSC-U y confirmar si el autodetector reconoce el
      lenguaje R5900 automáticamente o requiere selección manual (ver
      issue #127 citado en TK5-0007).
- [ ] Si hay símbolos `.mdebug`, ejecutar el STABS Analyzer y documentar
      cuántas funciones/tipos se recuperan automáticamente.
- [ ] Identificar manualmente, como prueba de concepto, la función
      asociada a al menos una de las direcciones de los parches widescreen
      de TK5-0009, confirmando o refutando la hipótesis de esa comunidad.

## PS2Recomp

- [ ] Clonar y compilar PS2Recomp según sus instrucciones, confirmando los
      requisitos reales en el entorno de desarrollo del equipo (CMake,
      compilador C++20).
- [ ] Ejecutar `ps2xAnalyzer` sobre el ELF de NTSC-U como primera pasada
      exploratoria (sin exportación de Ghidra todavía) y documentar qué
      detecta automáticamente.
- [ ] Ejecutar una recompilación de prueba con un mapa de funciones mínimo
      (una sola función identificada manualmente) y documentar el C++
      generado como referencia.

## Filesystem

- [ ] Determinar la herramienta o biblioteca a usar para leer el ISO9660
      de PS2 (que puede tener extensiones específicas no estándar;
      investigar si herramientas genéricas de ISO9660 son suficientes o si
      hace falta algo específico de PS2).
- [ ] Escanear binariamente el ISO (sin extraer archivos) en busca de las
      cabeceras `4E 55 44 50` (NUDP) y `54 49 4D 32` (TIM2) citadas en
      TK5-0019, y documentar cuántas apariciones hay.

## Assets

- [ ] Una vez identificado al menos un archivo candidato a modelo o
      textura en el filesystem retail, intentar abrirlo con Noesis (sin
      redistribuir el archivo) y documentar el resultado.
- [ ] Investigar específicamente el formato de archivos de "The Devil
      Within", dado que TK5-0010 sugiere que podría ser la única parte del
      juego accesible sin ofuscación adicional.

## Memoria

- [ ] Verificar en PCSX2 (con una copia legal) al menos una de las
      direcciones de widescreen de TK5-0009 para NTSC-U, confirmando en el
      depurador qué instrucción ocupa esa dirección antes del parche.
- [ ] Ampliar `research/memoria/direcciones-conocidas.md` con cualquier
      dirección adicional verificada de esta forma.

## Renderizado

- [ ] (Bloqueada hasta tener resultados de la sección "PS2" y "Ghidra"
      de este backlog) Determinar qué funciones del ELF corresponden a
      construcción de listas de despliegue para el GIF.

## Audio

- [ ] Investigar qué formato de audio usa Tekken 5 (ADPCM vía SPU2 es lo
      estándar en PS2, pero no confirmado específicamente para este
      juego) y si hay herramientas de extracción de audio de PS2 genéricas
      aplicables.

## Gameplay

- [ ] Buscar fuentes de framedata documentado empíricamente por la
      comunidad competitiva de Tekken 5 (útil para contrastar contra lo
      que se descubra en el código).

## Runtime

- [ ] (Bloqueada hasta completar "PS2Recomp" arriba) Documentar qué partes
      de `ps2xRuntime` son reutilizables tal cual y cuáles requieren
      extensión específica de Tekken 5 (overrides, ver
      `docs/investigacion/ps2recomp.md`).

## Testing

- [ ] (Bloqueada hasta completar "PS2" arriba) Definir el primer conjunto
      mínimo de datos de referencia capturables de forma reproducible.

## Documentación

- [ ] Confirmar la licencia exacta de Play!, `ghidra-emotionengine`
      (original), `ccc`, y `god-hand-decomp`, actualizando
      `docs/investigacion/licencias.md`.
- [ ] Revisar y actualizar este backlog cada vez que se complete una tarea
      o se descubra una nueva incógnita relevante.
