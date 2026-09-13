# Sitio web de Procesa Tech SAC — procesa.com.pe

Landing de una sola pagina, estatica, sin proceso de compilacion.
Se despliega sola en Netlify con cada cambio que entra a la rama principal.

## Estructura

    public/                 lo que se publica
      index.html            el sitio (43 KB)
      img/                  las seis fotos, en webp
      privacidad.html       aviso de privacidad (Ley 29733 / DS 016-2024-JUS)
      gracias.html          confirmacion tras enviar el formulario
      og.jpg                imagen de vista previa al compartir el enlace
      robots.txt
      sitemap.xml
      _headers              cabeceras de seguridad
    netlify.toml            le dice a Netlify que publique public/

## Como se cambia algo

Se edita el archivo, se guarda el cambio en la rama principal y Netlify
publica solo. No hay que armar ningun paquete ni arrastrar nada.

Antes de este repositorio el despliegue era manual, y dos veces termino
publicandose la version equivocada. Esa es la razon de ser de este repositorio.

## Lo que NO se toca desde aqui

- **Registros DNS**: viven en GoDaddy. Los de correo (MX, SPF, DKIM, DMARC,
  autodiscover) no se tocan nunca al cambiar el sitio.
- **Formulario**: los envios llegan a Netlify > Forms > contacto y avisan por
  correo a comercial@procesa.com.pe. Esa configuracion esta en el panel de
  Netlify, no en el codigo.
- **Insignia "Powered by Netlify"**: apagada. Si alguien la vuelve a encender,
  tapa el boton flotante de WhatsApp y no hay forma de ganarle por CSS.

## Cuidados al editar

- El campo de correo del formulario **tiene que llamarse `email`**. Netlify toma
  de ahi el Reply-to del aviso; con cualquier otro nombre, responder un lead
  escribe a Netlify en vez de al prospecto.
- El aviso de privacidad declara que el sitio **no usa cookies ni analitica**.
  El dia que se agregue medicion, hay que actualizar esa pagina en el mismo acto.
- Las fotos viven en `public/img/` como webp y se referencian desde el CSS con
  rutas absolutas (`/img/portada-rack.webp`). Antes iban incrustadas en el HTML
  como base64 y el index pesaba 831 KB; ahora pesa 43 KB y el navegador pinta la
  portada sin esperar las fotos de abajo. Si se reemplaza una foto, conviene
  cambiarle el nombre: `_headers` las cachea un ano.

## Documentacion

El documento de gestion es el PT-COM-003, en el repositorio documental de
Procesa y en el proyecto de Claude.
