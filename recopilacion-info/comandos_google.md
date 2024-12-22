# Google Hacking: Comandos y Operadores Booleanos

# Google Search Commands (Google Dorks)
Los Google Dorks son búsquedas avanzadas en Google que permiten localizar información, archivos específicos y páginas vulnerables en sitios web. Aunque no son herramientas de hacking, pueden ser utilizadas para detectar sitios web expuestos a riesgos como inyecciones SQL o accesos no autorizados. Es fundamental emplearlos de forma ética y responsable, especialmente en el campo de la seguridad informática.

## Tabla de Comandos

| Comando | Ejemplo | Descripción (basado en el ejemplo) |
|---------|---------|------------------------------------|
| `intitle` | `intitle:"Index of" password.txt` | Muestra directorios que contienen archivos de texto con nombres como "password.txt". |
| `intitle` | `intitle:"Index of" /admin` | Muestra directorios de administración en sitios web. |
| `filetype` | `filetype:xls inurl:"email.xls"` | Muestra listado de emails expuestos. |
| `inurl` | `inurl:"login" site:example.com` | Encuentra páginas de inicio de sesión en un sitio web específico. |
| `filetype` | `filetype:log inurl:"password.log"` | Encuentra archivos de registro (logs) que contienen "password" en su nombre. |
| `intitle` | `intitle:index.of id_rsa -id_rsa.pub` | Encuentra claves privadas SSH. |
| `site` | `site:.gov intitle:"secret" filetype:pdf` | Encuentra archivos gubernamentales expuestos en internet. |
| `intext` | `intext:"Welcome to phpMyAdmin"` | Busca páginas que contienen la cadena "Welcome to phpMyAdmin" en su contenido. |
| `inurl` | `inurl:/wp-content/uploads/ filetype:pdf` | Encuentra archivos PDF en la carpeta de "uploads" de sitios web basados en WordPress. |
| `intitle` | `intitle:"Index of" /backup` | Muestra directorios que contienen archivos de backup. |
| `site` | `site:example.com ext:sql` | Encuentra archivos SQL en el sitio web especificado. |
| `intitle` | `intitle:"index of" "database.sql"` | Encuentra archivos de bases de datos SQL. |
| `intitle` | `intitle:"SQL Injection" site:example.com` | Encuentra páginas web que contienen la frase "SQL Injection" en un sitio web específico. |
| `site` | `site:example.com ext:doc` | Encuentra documentos de Microsoft Word en el sitio web especificado. |
| `site` | `site:example.com ext:xml` | Encuentra documentos Excel en el sitio web especificado. |
| `site` | `site:example.com ext:conf` | Busca archivos de configuración en el sitio web especificado. |
| `inurl` | `inurl:"/cgi-bin/pass.txt"` | Busca archivos de texto con nombres como "pass.txt" en carpetas de "cgi-bin". |
| `intitle` | `intitle:"WebcamXP 5"` | Encuentra cámaras web accesibles a través de WebcamXP 5. |
| `site` | `site:example.com inurl:config` | Busca archivos de configuración en el sitio web especificado. |
| `intitle` | `intitle:"index of" intext:config.php` | Muestra directorios que contienen archivos de configuración PHP. |
| `intitle` | `intitle:"index of" intext:.htpasswd` | Encuentra directorios que contienen archivos .htpasswd. |
| `intitle` | `intitle:"index of" intext:.env` | Busca directorios que contengan archivos .env. |
| `intitle` | `intitle:"index of" "wp-content/uploads" site:example.com` | Encuentra archivos cargados en WordPress en un sitio web específico. |
| `filetype` | `filetype:xls inurl:"email.xls"` | Encuentra archivos de hojas de cálculo Excel que contienen "email" en su nombre. |
| `intext` | `intext:"Powered by phpBB"` | Muestra sitios web que utilizan el sistema de gestión de contenido phpBB. |
| `intext` | `intext:"Powered by Wordpress"` | Muestra sitios web que utilizan Wordpress. |
| `intext` | `intext:"@outlook.com" site:example.com` | Encuentra webs que contienen direcciones de correo de Outlook en un sitio específico. |
| `inurl` | `inurl:/dana-na/ filetype:cgi` | Encuentra páginas CGI en la carpeta "/dana-na/". |
| `inurl` | `inurl:server-info "Apache Server Information"` | Muestra información del servidor Apache. |
| `intext` | `intext:"sql syntax near"` | Muestra webs con posibles errores de SQL. |
| `intext` | `intext:"confidential" site:example.com` | Encuentra páginas web que contienen la palabra "confidencial" en un sitio web específico. |
| `inurl` | `inurl:/proc/self/cwd` | Muestra el directorio de trabajo actual de un servidor. |
| `intitle` | `intitle:"index of" intext:web.config` | Encuentra archivos de configuración web en directorios indexados. |
| `filetype` | `filetype:reg reg HKEY_CURRENT_USER username` | Busca archivos de registro (registries) que contengan la cadena "username" en la clave HKEY_CURRENT_USER. |
| `inurl` | `inurl:"ViewerFrame?Mode="` | Encuentra cámaras web accesibles a través de scripts de visualización. |
| `intext` | `intext:"powered by vBulletin"` | Muestra sitios web que utilizan el sistema de gestión de contenido vBulletin. |
| `intitle` | `intitle:"index of" inurl:ftp` | Encuentra servidores FTP que tienen directorios indexados. |
| `intitle` | `intitle:"index of" "WhatsAppDB.csv"` | Muestra directorios que contienen archivos CSV de bases de datos de WhatsApp. |
| `filetype` | `filetype:env intext:APP_ENV` | Busca archivos de configuración con información sobre el entorno de la aplicación. |
| `inurl` | `inurl:"/phpinfo.php"` | Muestra información sobre el servidor PHP. |
| `intitle` | `intitle:"index of" intext:sftp-config.json` | Encuentra archivos de configuración SFTP en directorios indexados. |



## Operadores Booleanos

`" "`: Busca palabras exactas.  
`OR` o `|`: Busca uno u otro término.  
`+`: Incluye palabras comunes o distingue caracteres.  
`*`: Comodín para reemplazar palabras.
