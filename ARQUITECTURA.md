# Arquitectura del repositorio

Este repo está pensado para crecer de forma ordenada. Hoy se enfoca en **generar** artefactos de QA (análisis de historias, casos manuales, BDD, casos de API, datos de prueba, reportes de bug); más adelante sumará **ejecución** (correr pruebas, integrarse con las herramientas del equipo). Para que eso entre sin romper lo que ya funciona, todo se organiza en piezas, cada una con su lugar.

## Las piezas

### Agentes — el *quién* (`.claude/agents/`)

Cada agente es un subagente de Claude Code con su rol, su proceso y sus reglas. Es a quién se le delega una tarea entera. Hoy hay seis. La clave de cada uno está en el `description` de su frontmatter: es lo que usa Claude Code para saber cuándo invocarlo.

### Skills — el *cómo* (`.claude/skills/`)

Conocimiento empaquetado que Claude Code carga **on-demand** (solo cuando hace falta). Encapsula el "cómo" de una capacidad reutilizable, para que varios agentes lo aprovechen sin repetir instrucciones. Cada skill es una carpeta con un `SKILL.md` (ver `.claude/skills/README.md`).

> Lo que un agente usa para **actuar** viene en tres formas: conexiones MCP, herramientas externas y scripts internos.

### MCP — conexiones a sistemas externos (`.mcp.json`)

Para tocar sistemas de afuera (Jira, Xray, un navegador…), un agente usa un **server MCP**. **Es un solo archivo, pero escala a todas las conexiones que quieras**: `.mcp.json` es un *registro* de servers, donde agregás una entrada por cada integración.

```json
{
  "mcpServers": {
    "atlassian":  { "type": "http", "url": "https://mcp.atlassian.com/v1/mcp" },
    "xray":       { "type": "http", "url": "${XRAY_MCP_URL}", "headers": { "Authorization": "Bearer ${XRAY_TOKEN}" } },
    "playwright": { "type": "stdio", "command": "npx", "args": ["-y", "@playwright/mcp@latest"] }
  }
}
```

Dejamos un `.mcp.json.example` de plantilla. Para usarlo, copialo a `.mcp.json` (que está gitignored) y dejá solo las conexiones que necesites.

> **Regla de oro de los secretos:** tokens y credenciales van como variables de entorno con `${VARIABLE}` (en tu entorno o un `.env` local), **nunca** con el valor real en el archivo. Si se commitea un secreto, rotalo de inmediato.

### Herramientas — herramientas externas de testing (`herramientas/`)

Herramientas que el agente **ejecuta** por línea de comandos —por ejemplo **JMeter** para performance—, con sus plantillas y configuraciones. Cada herramienta va en su **propia subcarpeta**, así escala: sumar una herramienta = sumar una carpeta (ver `herramientas/README.md`).

### Scripts — utilidades internas (`scripts/`)

Código Python propio del repo para tareas mecánicas (generar la planilla `.xlsx`, normalizar tablas). Las utilidades internas nuevas viven acá.

## En resumen

- **Agente** = a quién le pido la tarea.
- **Skill** = el conocimiento de cómo hacerla.
- **MCP** = conexiones a sistemas externos (un archivo, muchas conexiones: Jira, Xray, Playwright…).
- **Herramientas** = herramientas externas que se ejecutan por CLI (JMeter…).
- **Script** = utilidad interna determinística.

Esto es el **chasis**. Las conexiones MCP, las herramientas y los skills reales se suman en la fase de ejecución.
