# research/simbolos/

Mapas de símbolos (funciones, variables globales, tipos) identificados en
el ELF de Tekken 5, ya sea recuperados automáticamente (si existen
símbolos `.mdebug`/STABS, ver TK5-0008) o identificados manualmente
durante el trabajo en Ghidra.

Este directorio es el formato "tabular, para consumo de herramientas" que
complementa a la narrativa de cada hallazgo en `research/hallazgos/`. Cada
función o símbolo aquí listado debería, idealmente, enlazar a un hallazgo
`TK5-XXXX` que documente cómo se identificó.

## Estado actual

Vacío. Pendiente de la primera sesión de análisis real en Ghidra (ver
`docs/desarrollo/backlog.md`, sección "Ghidra").

## Formato previsto

`research/simbolos/<region>/funciones.csv` con columnas mínimas:
`direccion, nombre, tamano, nivel_confianza, hallazgo_relacionado`.
