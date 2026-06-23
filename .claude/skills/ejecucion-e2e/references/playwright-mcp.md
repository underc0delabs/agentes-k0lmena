# Playwright MCP — referencia de ejecución

Detalle del skill `ejecucion-e2e`: setup, tools principales, robustez y un ejemplo trabajado.

## Setup (recordatorio)

- Registrar el server: `claude mcp add playwright npx @playwright/mcp@latest` (el oficial es `@playwright/mcp` de Microsoft). En este repo ya está en `.mcp.json` (con modo headed y headless).
- Navegadores: `npx playwright install` (ocupan ~700 MB; en Linux además `npx playwright install-deps`).
- Para configs compartidas conviene **pinear la versión** (`@playwright/mcp@<versión>`) en lugar de `@latest`, para evitar fallos por cambios entre versiones.
- Gotcha: la primera vez, nombrá **"Playwright MCP"** en el pedido; si no, a veces se intenta correr Playwright por Bash en lugar del MCP.

## Tools principales

- **Navegar**: abrir URL, ir atrás/adelante, recargar.
- **Snapshot de accesibilidad**: obtener la estructura de la página (roles + nombres) para ubicar elementos.
- **Interacción**: click, escribir/llenar campos, seleccionar de un dropdown, teclas, hover.
- **Screenshot**: capturar la página o un elemento.
- **Consola / red**: leer mensajes de consola y requests (útil para depurar un fallo).

## Robustez

- **Selectores**: por rol + nombre accesible (textbox "Email"), no CSS/XPath frágiles.
- **Esperas**: esperá visibilidad/estabilidad antes de actuar; reintentá con un nuevo snapshot ante "no encontrado" antes de marcar fallo.
- **Datos**: nunca los inventes; pedí URL y datos si faltan.
- **Estado limpio**: para una corrida aislada, el server puede correr con `--isolated` (cada sesión arranca de cero).

## Ejemplo trabajado — registro válido (CA1 de HU-001)

Escenario: crear cuenta con datos válidos en https://qarmy.ar/practica/automation/.

1. Navegar a la URL.
2. Snapshot → ubicar los campos por su nombre.
3. Completar: Nombre "María", Apellido "González", Sexo "Femenino", Email "maria.gonzalez@test.com", País "Argentina", Usuario "maria_gonzalez", Contraseña "Aa123456!".
4. Click en "Registrar".
5. Verificar la confirmación de registro exitoso (lo que muestre la página) y sacar screenshot.
6. Resultado: **Aprobado** si aparece la confirmación; si no, **Fallido** con el detalle + screenshot.

Los casos negativos (por ejemplo email inválido, contraseña sin símbolo, usuario de 3 caracteres) siguen el mismo flujo, verificando que aparezca el **mensaje de error** del campo correspondiente.
