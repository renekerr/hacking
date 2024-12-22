# Google Hacking: Comandos y Operadores Booleanos

# Google Search Commands (Google Dorks)
Los Google Dorks son búsquedas avanzadas en Google que permiten localizar información, archivos específicos y páginas vulnerables en sitios web. Aunque no son herramientas de hacking, pueden ser utilizadas para detectar sitios web expuestos a riesgos como inyecciones SQL o accesos no autorizados. Es fundamental emplearlos de forma ética y responsable, especialmente en el campo de la seguridad informática.

## Comandos

| Comando   | Ejemplo                                     | Descripción                                                                 |
|-----------|---------------------------------------------|-----------------------------------------------------------------------------|
| `intitle` | `intitle:"Index of" password.txt`           | Muestra directorios que contienen archivos de texto con nombres como "password.txt". |
| `filetype`| `filetype:xls inurl:"email.xls"`            | Muestra listado de emails expuestos en archivos Excel.                      |
| `inurl`   | `inurl:"login" site:example.com`            | Encuentra páginas de inicio de sesión en un sitio web específico.           |
| `site`    | `site:.gov intitle:"secret" filetype:pdf`   | Encuentra archivos gubernamentales expuestos en internet.                   |
| `intext`  | `intext:"Welcome to phpMyAdmin"`            | Busca páginas que contienen la cadena "Welcome to phpMyAdmin" en su contenido. |




## Operadores Booleanos
| Operador   | Descripción                                          | Ejemplo                                 |
|----------------|----------------------------------------------------------|---------------------------------------------|
| `""`           | Busca palabras exactas                                   | `"seguridad informática"`                   |
| `AND` o `+`    | Busca uno y otro término                                  | `"seguridad informática" AND "ciberseguridad"` |
| `OR` o `\|`     | Busca uno u otro término                                  | `"seguridad informática" OR "ciberseguridad"` |
| `+`            | Incluye palabras comunes o distingue caracteres           | `+seguridad +informática`                   |
| `*`            | Comodín para reemplazar palabras o parte de ellas        | `"segur* informática"`                      |

