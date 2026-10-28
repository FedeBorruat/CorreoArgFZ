# Decisiones técnicas y limitaciones

## Enlaces de un solo uso

Los enlaces de solicitud se registran en una hoja y se validan en el servidor. El objetivo es evitar que el mismo enlace se utilice para registrar solicitudes repetidas. La apertura del formulario no consume el enlace; el consumo se realiza cuando se registra correctamente la solicitud.

## Token de automatización

El token vincula la solicitud registrada con el userscript que se ejecuta en MiCorreo. En la versión anterior, se recibe en el fragmento de la URL (`#frz=...`), se guarda temporalmente en `sessionStorage` y se elimina del fragmento visible mediante la API de historial del navegador.

No publicar tokens reales ni ejemplos tomados de solicitudes reales.

## Base fija de sucursales

Para evitar cargar y procesar la hoja completa en cada apertura del formulario, Apps Script serializa la base y la almacena comprimida en partes dentro de Script Properties. El HTML recibe una representación JSON que utiliza para construir las listas de provincias y sucursales.

## Selección de sucursal

El código anterior de Tampermonkey identifica una sucursal mediante su código en las clases de la opción HTML, en vez de confiar únicamente en el valor de la opción, que puede representar el código postal y no ser único.

## Dependencia de una interfaz externa

Tampermonkey depende de IDs, opciones, eventos y lógica de la página de MiCorreo. Una modificación del sitio puede cambiar el orden de los pasos, los nombres de campos, las validaciones o las peticiones internas. Por ello, el userscript debe probarse después de cambios en MiCorreo.

## Límite de automatización

La versión disponible espera que el servicio elegido se habilite y no fuerza el botón final de guardado. Este comportamiento mantiene la confirmación final bajo control humano.

## Estado de la versión

El archivo Tampermonkey compartido corresponde a una versión anterior (v3.3) que funcionaba en una etapa previa del proyecto. No representa necesariamente el último estado operativo. La documentación debe describir la arquitectura y evitar presentar detalles de esa versión como garantía de la versión actual.
