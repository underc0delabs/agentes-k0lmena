# HU-001 — Crear cuenta (registro de usuario)

## Historia

**Como** visitante del sitio
**quiero** crear una cuenta completando el formulario de registro
**para** poder acceder a la plataforma con mi usuario.

## Criterios de aceptación

- **CA1:** Con todos los campos completos y válidos, al presionar **Registrar** la cuenta se crea correctamente y se muestra una confirmación de registro exitoso.
- **CA2:** Todos los campos son **obligatorios**. Si falta alguno, se muestra el mensaje de error correspondiente bajo ese campo y no se completa el registro.
- **CA3:** **Nombre** acepta entre 2 y 50 caracteres, solo letras y espacios. Si está fuera de ese rango o incluye números/símbolos, se rechaza con su mensaje.
- **CA4:** **Apellido** sigue la misma regla que Nombre: 2 a 50 caracteres, solo letras y espacios.
- **CA5:** **Sexo** requiere seleccionar una opción (Masculino, Femenino u Otro). Sin selección, se muestra "Seleccioná una opción".
- **CA6:** **Email** debe tener un formato válido (por ejemplo `nombre@dominio.com`). Con formato inválido, se rechaza con su mensaje.
- **CA7:** **País** requiere elegir una opción de la lista (Argentina, Chile, Uruguay, Perú, México, España, Estados Unidos). Sin selección, se muestra "Seleccioná un país".
- **CA8:** **Usuario** acepta entre 4 y 20 caracteres, solo letras, números o guion bajo (`_`). Fuera de esa regla, se rechaza.
- **CA9:** **Contraseña** requiere mínimo 8 caracteres e incluir al menos una mayúscula, una minúscula, un número y un símbolo (por ejemplo `Aa123456!`). Si no cumple, se rechaza indicando el requisito.
- **CA10:** Las validaciones se muestran como mensajes **por campo**, indicando el problema concreto de cada uno.

## Notas

- Página del formulario: https://qarmy.ar/practica/automation/ (formulario de ejemplo para automatización).
- Opciones del campo País: Argentina, Chile, Uruguay, Perú, México, España, Estados Unidos.
- **A confirmar:** el texto y la forma exactos de la confirmación de "registro exitoso" deben verificarse en la página (no se asume; se valida al ejecutar).
