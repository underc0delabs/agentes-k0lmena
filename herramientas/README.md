# Herramientas

Acá se integran las **herramientas externas de testing** que los agentes usan para *ejecutar* (no para generar): herramientas que se corren por línea de comandos o que necesitan sus propios archivos de configuración y plantillas.

Cada herramienta va en su **propia subcarpeta**, así el repo escala sin pisarse: sumar una herramienta = sumar una carpeta.

```
herramientas/
├── jmeter/          # ejemplo a futuro: pruebas de performance
│   ├── planes/      # plantillas .jmx
│   ├── config/      # configuración
│   └── README.md    # cómo la usa el agente
└── ...              # otras (k6, Postman/Newman, etc.)
```

Todavía está vacía: las herramientas reales (JMeter y las que vengan) se suman con las funcionalidades de ejecución.

> ¿En qué se diferencia de `scripts/` y de `.mcp.json`?
> - **`herramientas/`** → herramientas externas que se ejecutan por CLI (JMeter, k6…), con sus plantillas y configs.
> - **`scripts/`** → utilidades en Python propias del repo (generan o dan formato a los artefactos).
> - **`.mcp.json`** → conexiones a sistemas externos por protocolo MCP (Jira, Xray, navegador vía Playwright…).
