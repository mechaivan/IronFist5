# Registro de licencias de proyectos externos

Regla 7 de `AGENTS.md`: nunca reutilizar código externo sin comprobar su
licencia primero y registrarla aquí. Esta tabla se actualiza cada vez que
se evalúa un proyecto externo para posible reutilización, inspiración, o
dependencia.

Plantilla (sección 26 del encargo original):

```text
Proyecto:
URL:
Licencia:
Copyright:
¿Podemos reutilizar código?:
Condiciones:
Uso previsto:
```

---

```text
Proyecto: PS2Recomp
URL: https://github.com/ran-j/PS2Recomp
Licencia: GPL-3.0
Copyright: ran-j y contribuidores (ver historial de commits del repositorio)
¿Podemos reutilizar código?: Sí, respetando copyleft fuerte
Condiciones: Cualquier binario derivado que enlace o incluya código de
  PS2Recomp (incluido su runtime, ps2xRuntime) debe distribuirse también
  bajo GPL-3.0 (o licencia compatible), con el código fuente disponible.
  Esto tiene una implicación directa para la licencia de este propio
  repositorio una vez que dependamos de PS2Recomp en tiempo de compilación
  o enlace (ver sección "Implicación para la licencia de este proyecto"
  más abajo).
Uso previsto: Dependencia externa (no vendorizada) para la fase de
  recompilación estática del ELF de Tekken 5, cuando el proyecto llegue a
  esa fase.
```

```text
Proyecto: Ghidra Emotion Engine: Reloaded (ghidra-emotionengine-reloaded)
URL: https://github.com/chaoticgd/ghidra-emotionengine-reloaded
Licencia: Apache-2.0
Copyright: chaoticgd y contribuidores
¿Podemos reutilizar código?: Sí, la Apache-2.0 es permisiva (requiere
  conservar avisos de copyright y de licencia, y documentar cambios si se
  modifica el código)
Condiciones: Atribución; no exige que nuestro propio código se publique
  bajo la misma licencia
Uso previsto: Herramienta externa instalada en Ghidra, no se vendoriza
  código dentro de este repositorio
```

```text
Proyecto: ghidra-emotionengine (original, beardypig)
URL: https://github.com/beardypig/ghidra-emotionengine
Licencia: No confirmada en esta pasada (pendiente de verificación directa
  del archivo LICENSE del repositorio)
Copyright: beardypig y contribuidores
¿Podemos reutilizar código?: PENDIENTE DE VERIFICACIÓN hasta comprobar
Condiciones: Pendiente
Uso previsto: Posible alternativa/antecedente histórico de
  ghidra-emotionengine-reloaded; no se prevé depender de este directamente
  si el fork "Reloaded" sigue activo y es compatible con versiones
  recientes de Ghidra
```

```text
Proyecto: ccc (parser de símbolos STABS/.mdebug)
URL: https://github.com/chaoticgd/ccc
Licencia: No confirmada en esta pasada (pendiente de verificación)
Copyright: chaoticgd y contribuidores
¿Podemos reutilizar código?: PENDIENTE DE VERIFICACIÓN
Condiciones: Pendiente
Uso previsto: Posible dependencia si se confirma que el ELF de Tekken 5
  tiene secciones .mdebug (ver TK5-0008)
```

```text
Proyecto: N64Recomp
URL: https://github.com/N64Recomp/N64Recomp
Licencia: MIT
Copyright: N64Recomp / Mr-Wiseguy y contribuidores
¿Podemos reutilizar código?: Sí, MIT es muy permisiva (solo exige
  conservar el aviso de copyright y la licencia)
Condiciones: Atribución
Uso previsto: Solo referencia metodológica de diseño; no se prevé
  dependencia directa de código dado que la arquitectura objetivo (N64) es
  muy distinta de PS2
```

```text
Proyecto: Zelda64Recomp
URL: https://github.com/Zelda64Recomp/Zelda64Recomp
Licencia: GPL-3.0
Copyright: Zelda64Recomp Team
¿Podemos reutilizar código?: Sí, respetando copyleft fuerte
Condiciones: Igual que PS2Recomp — cualquier reuso obliga a GPL-3.0
Uso previsto: Solo referencia metodológica (no se prevé reutilizar código
  directamente, al ser de otra plataforma)
```

```text
Proyecto: TekkenMovesetExtractor
URL: https://github.com/Kiloutre/TekkenMovesetExtractor
Licencia: GPL-3.0
Copyright: Kiloutre y contribuidores
¿Podemos reutilizar código?: Sí, respetando copyleft fuerte, PERO el
  proyecto está archivado/obsoleto y su aplicabilidad real a Tekken 5 PS2
  no está confirmada (ver TK5-0011) — evaluar primero la utilidad real
  antes de depender de él
Condiciones: Copyleft fuerte (GPL-3.0)
Uso previsto: Ninguno confirmado todavía; en evaluación
```

```text
Proyecto: God Hand Decomp
URL: https://github.com/LucasPicoli/god-hand-decomp
Licencia: NO VERIFICADA en esta pasada — debe comprobarse el archivo
  LICENSE del repositorio antes de cualquier uso, aunque sea solo de
  lectura de su metodología como referencia
Copyright: LucasPicoli y contribuidores
¿Podemos reutilizar código?: NO hasta confirmar licencia
Condiciones: N/A hasta verificar
Uso previsto: Solo referencia metodológica de organización de un proyecto
  de decompilación (observación de su estructura pública, no de su código
  fuente línea a línea)
```

```text
Proyecto: PCSX2
URL: https://github.com/PCSX2/pcsx2
Licencia: GPL-3.0
Copyright: PCSX2 Team
¿Podemos reutilizar código?: Sí, respetando copyleft fuerte
Condiciones: Copyleft fuerte
Uso previsto: Herramienta externa de investigación (depuración, volcados de
  memoria), no se prevé vendorizar ni modificar su código fuente en este
  repositorio salvo que se justifique explícitamente
```

```text
Proyecto: Play! (jpd002/Play-)
URL: https://github.com/jpd002/Play-
Licencia: PENDIENTE DE VERIFICACIÓN — fuentes secundarias discrepan entre
  BSD-2-Clause (emulation.gametechwiki.com) y "MIT License" (mirror de
  SourceForge). Debe confirmarse contra el archivo LICENSE real del
  repositorio antes de cualquier decisión.
Copyright: jpd002 y contribuidores
¿Podemos reutilizar código?: Probablemente sí (ambas licencias candidatas
  son permisivas), pero confirmar la licencia exacta antes de actuar
Condiciones: Pendiente de confirmación
Uso previsto: Herramienta exploratoria de investigación, no está prevista
  dependencia de código
```

```text
Proyecto: Herramientas MCP de depuración de PCSX2 (PCSX2-MCP de hkmodd,
  PCSX2_MCP de snowyegret23) y skills de agentes (ps2-recomp-Agent-SKILL,
  RecompHamr)
URL: Ver TK5-0015, TK5-0016 para enlaces completos
Licencia: Variable — hkmodd/PCSX2-MCP declara GPL-3.0 para su plugin
  derivado de PCSX2 y MIT para su propio servidor MCP; las demás no
  verificadas en esta pasada
Copyright: Respectivos autores
¿Podemos reutilizar código?: Evaluar caso por caso; son proyectos muy
  recientes (2026) y de procedencia no auditada en profundidad
Condiciones: Pendiente, caso por caso
Uso previsto: Ninguno confirmado; documentados solo como contexto de
  ecosistema (TK5-0016)
```

## Estado de integración en IronFist 5

A fecha de esta revisión, el repositorio no incluye código vendorizado,
submódulos ni binarios de PS2Recomp, Ghidra, PCSX2 u otra herramienta
externa. Las herramientas listadas son dependencias de investigación
previstas o referencias documentales, no componentes distribuidos por este
repositorio. Cualquier integración futura debe registrar la versión, licencia
y forma de distribución antes de añadir código o binarios.

## Implicación para la licencia de este propio repositorio

Dado que la visión a largo plazo de este proyecto (ver `README.md`) depende
explícitamente de PS2Recomp (GPL-3.0), cualquier código de este repositorio
que termine enlazándose o distribuyéndose junto con PS2Recomp/ps2xRuntime
deberá, con alta probabilidad, licenciarse también bajo GPL-3.0 (o una
licencia compatible) para cumplir con su copyleft. Por eso se ha elegido
**GPL-3.0** como licencia de este repositorio desde el inicio (ver
`LICENSE`), evitando así un conflicto de licencias más adelante. Esta
decisión se revisará si la estrategia técnica cambia de forma que ya no
dependa de software GPL-3.0 de terceros.

La documentación en `docs/` y `research/` (texto, no código) se considera
cubierta por la misma licencia del repositorio salvo que se indique lo
contrario, pero su naturaleza de documentación de investigación significa
que, en la práctica, lo más relevante a proteger es que **nunca contenga
datos propietarios del juego** (Regla 8 de `AGENTS.md`), independientemente
de la licencia del texto.
