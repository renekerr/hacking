# Google Hacking: Comandos y Operadores Booleanos

## Comandos Principales
| Comando | Descripción | Ejemplo |
|---------|-------------|---------|
| `define:palabra` | muestra definiciones de la palabra. | `define:gato` |
| `filetype:palabra` | filtra por extensión de archivo. | `filetype:pdf historia` |
| `site:sitio/dominio` | limita la búsqueda a un sitio o dominio. | `site:wikipedia.org` |
| `link:url` | muestra páginas que enlazan la URL indicada. | `link:example.com` |
| `cache:url` | muestra la versión en caché de una página. | `cache:example.com` |
| `info:url` | proporciona información sobre la página. | `info:example.com` |
| `related:url` | muestra páginas similares a la URL. | `related:example.com` |
| `allinanchor:palabras` | filtra páginas por enlaces con las palabras. | `allinanchor:tecnología innovación` |
| `inanchor:palabra` | filtra por enlaces que contienen la palabra. | `inanchor:educación` |
| `allintext:palabras` | filtra por páginas con las palabras en el texto. | `allintext:ciencia ficción` |
| `intext:palabra` | filtra por páginas con la palabra en el texto. | `intext:arte` |
| `allinurl:palabras` | filtra por palabras en la URL. | `allinurl:recetas cocina` |
| `inurl:palabra` | filtra por palabra en la URL. | `inurl:viajes` |
| `allintitle:palabras` | filtra por palabras en el título. | `allintitle:libros aventura` |
| `intitle:palabra` | filtra por palabra en el título. | `intitle:música` |



## Operadores Booleanos

`" "`: Busca palabras exactas.  
`OR` o `|`: Busca uno u otro término.  
`+`: Incluye palabras comunes o distingue caracteres.  
`*`: Comodín para reemplazar palabras.
