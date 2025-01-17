# Google Hacking: Comandos y Operadores Booleanos

## Google Search Commands (Google Dorks)
Los Google Dorks son búsquedas avanzadas en Google que permiten localizar información, archivos específicos y páginas vulnerables en sitios web. Aunque no son herramientas de hacking, pueden ser utilizadas para detectar sitios web expuestos a riesgos como inyecciones SQL o accesos no autorizados. Es fundamental emplearlos de forma ética y responsable, especialmente en el campo de la seguridad informática.

### Comandos

| Comando        | Ejemplo                                      | Descripción                                                                 |
|----------------|----------------------------------------------|-----------------------------------------------------------------------------|
| `intitle`      | `intitle:"Index of" invoices`                | Muestra directorios con archivos de facturas.                               |
|                | `intitle:"Security Camera"`                  | Encuentra cámaras de seguridad accesibles.                                  |
| `filetype`     | `filetype:doc inurl:"report.doc"`            | Muestra reportes expuestos en archivos Word.                                |
|                | `filetype:log inurl:"access.log"`            | Encuentra archivos de registro de accesos.                                  |
| `inurl`        | `inurl:"admin" site:example.com`             | Encuentra páginas de administración en un sitio específico.                 |
|                | `inurl:/files/ filetype:pdf`                 | Encuentra archivos PDF en la carpeta de "files".                            |
| `site`         | `site:.edu intitle:"research" filetype:pdf`  | Encuentra archivos PDF de investigaciones en sitios educativos.             |
|                | `site:.gov intitle:"budget" filetype:doc`    | Encuentra documentos Word de presupuestos en sitios gubernamentales.        |
| `intext`       | `intext:"Welcome to Joomla"`                 | Busca páginas con "Welcome to Joomla" en el contenido.                      |
|                | `intext:"Powered by Joomla"`                 | Muestra sitios web que usan Joomla.                                         |
| `define`       | `define:criptografía`                        | Muestra definiciones del término "criptografía".                            |
|                | `define:bioinformática`                      | Muestra definiciones del término "bioinformática".                          |
| `filetype`     | `filetype:txt`                               | Busca archivos de texto.                                                    |
|                | `filetype:env intext:APP_KEY`                | Busca archivos de configuración con claves de aplicación.                   |
| `link`         | `link:example.net`                           | Muestra páginas que enlazan a la URL definida.                              |
|                | `link:example.com`                           | Muestra páginas que enlazan a la URL definida.                              |
| `cache`        | `cache:example.net`                          | Muestra la versión en caché de una página.                                  |
|                | `cache:example.com`                          | Muestra la versión en caché de una página.                                  |
| `info`         | `info:example.net`                           | Muestra información sobre la página especificada.                           |
|                | `info:example.com`                           | Muestra información sobre la página especificada.                           |
| `related`      | `related:example.net`                        | Muestra páginas similares a la URL especificada.                            |
|                | `related:example.com`                        | Muestra páginas similares a la URL especificada.                            |
| `allinanchor`  | `allinanchor:tecnología innovadora`          | Páginas apuntadas por enlaces con los términos buscados.                    |
|                | `allinanchor:educación en línea`             | Páginas apuntadas por enlaces con los términos buscados.                    |
| `inanchor`     | `inanchor:tecnología`                        | Páginas apuntadas por enlaces con el término especificado.                  |
|                | `inanchor:marketing`                         | Páginas apuntadas por enlaces con el término especificado.                  |
| `allintext`    | `allintext:seguridad informática`            | Resultados que contienen los términos en el texto de la página.             |
|                | `allintext:desarrollo de software`           | Resultados que contienen los términos en el texto de la página.             |
| `intext`       | `intext:ciberseguridad`                      | Resultados que contienen el término "ciberseguridad" en el texto.           |
|                | `intext:machine learning`                    | Resultados que contienen el término "machine learning" en el texto.         |
| `allinurl`     | `allinurl:documentos confidenciales`         | Resultados que contienen los términos buscados en la URL.                   |
|                | `allinurl:contratos legales`                 | Resultados que contienen los términos buscados en la URL.                   |
| `inurl`        | `inurl:confidencial`                         | Resultados que contienen el término "confidencial" en la URL.               |
|                | `inurl:status "Apache Server Status"`        | Muestra el estado del servidor Apache.                                      |
| `allintitle`   | `allintitle:informes anuales`                | Resultados que contienen los términos en el título.                         |
|                | `allintitle:proyectos finales`               | Resultados que contienen los términos en el título.                         |
| `intitle`      | `intitle:privado`                            | Resultados que contienen el término "privado" en el título.                 |
|                | `intitle:seguro`                             | Resultados que contienen el término "seguro" en el título.                  |
| `intitle`      | `intitle:"index of" ssh_key`                 | Encuentra claves SSH privadas.                                              |
|                | `intitle:"index of" passwords`               | Muestra directorios con archivos de contraseñas.                            |
| `filetype`     | `filetype:log inurl:"server.log"`            | Encuentra archivos de registro de servidores.                               |
|                | `filetype:xls inurl:"contacts.xls"`          | Muestra contactos expuestos en archivos Excel.                              |
| `inurl`        | `inurl:/uploads/ filetype:jpg`               | Encuentra imágenes JPEG en la carpeta de "uploads".                         |
|                | `inurl:config "Server Configuration"`        | Muestra la configuración del servidor.                                      |
| `ext`          | `ext:pdf site:example.org`                   | Restringe resultados a archivos PDF en el sitio especificado.               |
|                | `ext:docx site:example.com`                  | Busca documentos de Word en el sitio especificado.                          |




### Operadores Booleanos
| Operador   | Descripción                                          | Ejemplo                                 |
|----------------|----------------------------------------------------------|---------------------------------------------|
| `""`           | Busca palabras exactas                                   | `"seguridad informática"`                   |
| `AND` o `+`    | Busca uno y otro término                                  | `"seguridad informática" AND "ciberseguridad"` |
| `OR` o `\|`     | Busca uno u otro término                                  | `"seguridad informática" OR "ciberseguridad"` |
| `+`            | Incluye palabras comunes o distingue caracteres           | `+seguridad +informática`                   |
| `*`            | Comodín para reemplazar palabras o parte de ellas        | `"segur* informática"`                      |

