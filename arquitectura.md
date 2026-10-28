# Arquitectura del sistema

## Componentes

### 1. Google Sheets

Funciona como almacenamiento operativo. En los archivos compartidos se identifican estas hojas:

- `Sucursales`: catálogo de sucursales habilitadas.
- `Solicitudes`: solicitudes registradas desde el formulario.
- `LinksEnvio`: registro de enlaces generados, su configuración y estado.

La implementación también incluye una base fija de sucursales comprimida y guardada en Script Properties para poder servirla al formulario sin reconstruirla desde la hoja en cada carga.

### 2. Google Apps Script

El código central concentra la lógica de negocio:

- inicialización, compresión y carga de la base fija de sucursales;
- presentación del formulario mediante `doGet(e)`;
- generación de enlaces de envío;
- validación de enlaces y registro de solicitudes;
- consulta de una solicitud a partir del token de automatización mediante `doPost(e)`;
- utilidades de diagnóstico.

El formulario y el generador interno usan `google.script.run` para invocar funciones del servidor.

### 3. Formulario HTML

El formulario solicita los datos del destinatario y la modalidad de entrega.

Para entrega en sucursal, utiliza el catálogo local de sucursales y permite seleccionar provincia y sucursal. Cuando hay información disponible, puede mostrar la dirección y ofrecer una apertura de ubicación en Google Maps.

Para entrega a domicilio, recopila provincia, localidad, dirección, código postal y observaciones.

El formulario recibe la configuración del enlace y fija el tipo de entrega y servicio que corresponden a esa solicitud.

### 4. Generador de enlaces

La interfaz interna se abre desde el menú `FRANZEBI` de la hoja de cálculo. Genera enlaces configurados para estas combinaciones:

- Sucursal + Clásico.
- Sucursal + Expreso.
- Domicilio + Clásico.
- Domicilio + Expreso.

El servidor registra el enlace y su estado. La validación del token administrativo se realiza en Apps Script.

### 5. Tampermonkey y MiCorreo

El userscript se ejecuta en páginas de MiCorreo dentro del dominio configurado. La versión anterior compartida:

1. Lee el token presente en el fragmento de la URL (`#frz=...`).
2. Lo conserva en `sessionStorage` y limpia el fragmento de la URL.
3. Consulta Apps Script usando una petición POST.
4. Completa los datos del paquete.
5. Configura entrega en sucursal o domicilio.
6. Completa los datos del destinatario.
7. Selecciona el servicio cuando MiCorreo lo habilita.
8. Se detiene antes de pulsar el botón final de guardar.

La versión más reciente del userscript no está disponible en esta documentación. No debe asumirse que cada detalle interno de la versión antigua coincide con la versión actualmente utilizada.

## Comunicación entre componentes

La versión anterior de Tampermonkey manda los parámetros como `application/x-www-form-urlencoded`, con una acción `getSolicitud` y el token de la solicitud. Apps Script contempla lectura de JSON y de parámetros de formulario para atender la consulta.

Los tokens son identificadores de acceso al flujo de una solicitud; no deben incluirse en capturas, ejemplos públicos ni commits.
