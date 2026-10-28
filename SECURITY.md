# Seguridad y privacidad

## No publicar

Antes de subir el proyecto a GitHub, revisar todos los archivos y eliminar:

- URLs reales de Web Apps que no deban divulgarse.
- Tokens administrativos y tokens de solicitudes.
- IDs privados de hojas de cálculo o recursos.
- Credenciales, cookies, claves API o secretos.
- Nombres, teléfonos, correos, direcciones y códigos de seguimiento reales.
- Capturas de pantalla con información de clientes.
- Datos de envíos reales o exportaciones completas de Google Sheets.

La URL de una Web App puede ser accesible públicamente según su configuración. No debe tratarse como mecanismo de autenticación por sí sola.

## Recomendaciones

- Mantener la hoja de cálculo y el proyecto de Apps Script con permisos mínimos necesarios.
- Validar los tokens en el servidor, no solamente en el navegador.
- Evitar reutilizar tokens de prueba en producción.
- Revisar quién puede acceder a la Web App y con qué identidad se ejecuta.
- No registrar el objeto completo de una solicitud en consola en entornos con datos reales.
- Usar datos sintéticos en ejemplos, capturas y pruebas públicas.
- Si un secreto se publicó accidentalmente, rotarlo o invalidarlo; borrar el texto de un commit no garantiza que desaparezca del historial.

## Reportar un problema

No incluir datos de clientes ni tokens activos en reportes de errores. Compartir únicamente mensajes sanitizados y pasos reproducibles.
