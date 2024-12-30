## Referencia Rápida de Operadores y Atajos de Teclado en Linux

### Operadores de Linux

**¿Qué hacen los operadores de Linux?**
Permiten combinar y dirigir el flujo de comandos en tu terminal.

| Símbolo/Operador | Descripción |
|---|---|
| & | **Ejecución en segundo plano:** Envía un comando a ejecutarse en segundo plano, permitiendo continuar con otras tareas en el terminal. |
| && | **Ejecución condicional:** Ejecuta el siguiente comando solo si el anterior se completó exitosamente. |
| > | **Redirección de salida:** Redirige la salida estándar (generalmente, lo que se muestra en pantalla) de un comando a un archivo, sobreescribiéndolo. |
| >> | **Anexar a un archivo:** Redirige la salida estándar de un comando a un archivo, pero agrega la nueva información al final del archivo existente. |

# Ejemplos de comandos en la terminal

## Crear un archivo y escribir algo en él
`echo "Hola, mundo!" > mi_archivo.txt`

## Añadir una nueva línea al archivo
`echo "Esta es una nueva línea." >> mi_archivo.txt`

## Ejemplos de Uso

`# Proceso en segundo plano con &`
`long-running-command &`

`# Encadenamiento de comandos con &&`
`cd /ruta/del/directorio && ls -la`

`# Redirección de salida con >`
`echo "Hola" > archivo.txt`

`# Añadir salida con >>`
`echo "Mundo" >> archivo.txt`

--------
# Atajos de Linux

| Atajo | Descripción |
|-------|-------------|
| Ctrl + A | Ir al principio de la línea |
| Ctrl + E | Ir al final de la línea |
| Ctrl + L | Limpiar pantalla (similar a clear) |
| Ctrl + U | Borrar línea anterior al cursor |
| Ctrl + H | Borrar carácter anterior (retroceso) |
| Ctrl + R | Buscar comandos anteriores |
| Ctrl + C | Interrumpir programa en ejecución |
| Ctrl + D | Cerrar shell actual |
| Ctrl + W | Cortar palabra anterior |
| Ctrl + K | Cortar línea siguiente |
| Ctrl + T | Intercambiar últimos dos caracteres |
| Esc + T | Intercambiar últimas dos palabras |
| Alt + . o !$ | Referenciar último argumento |
| Alt + F | Avanzar una palabra |
| Alt + B | Retroceder una palabra |
| Alt + l/u | Convertir a mayúsculas/minúsculas |
| Tab | Autocompletar archivos y carpetas |

----------
## Comandos

### Encuentra la ubicación del comando `ls` en el sistema utilizando `find`, y suprime los mensajes de error por permisos denegados.
`find / -name ls 2> /dev/null`

### Localiza los directorios de configuración de `firefox` instalados en Ubuntu, asegurándote de que el nombre del directorio sea `firefox`.
`find / -name firefox -type d 2> /dev/null`

### Identifica al propietario del archivo `shadow` en el sistema de archivos, excluyendo aquellos ubicados en `/snap`.
`find / -name shadow ! -path "/snap/*" -ls 2> /dev/null`

### Busca archivos en `/usr/bin` cuyos nombres terminen en un dígito.
`find /usr/bin -type f -name "*[[:digit:]]" 2>/dev/null`

### Encuentra archivos en el sistema que contengan dos guiones bajos en sus nombres y terminen con `.txt`.
`find / -type f -name "*_*_*.txt" 2>/dev/null`

### Busca archivos en `/var/log` que no tengan la extensión `.log`.
`find /var/log/ -type f -not -name "*.log" 2>/dev/null`

### Alternativamente, busca archivos en `/var/log` excluyendo aquellos que terminen en `.log` usando `!`.
`find /var/log/ -type f -name "*[!.log]"`

--------
## Wildcards. Comodines y algunas clases de caracteres POSIX utilizados en Linux

| Wildcard      | Descripción                                                                                           | Ejemplo                        | Coincide con                                    | No coincide con         |
|---------------|-------------------------------------------------------------------------------------------------------|--------------------------------|-------------------------------------------------|-------------------------|
| `*`           | Coincide con cero o más caracteres.                                                                   | `*.txt`                        | `file.txt`, `document.txt`, `notes.txt`         | `file.doc`, `image.jpg` |
| `?`           | Coincide con un solo carácter.                                                                        | `file?.txt`                    | `file1.txt`, `fileA.txt`, `file_.txt`           | `files.txt`, `file12.txt`|
| `[]`          | Coincide con cualquiera de los caracteres individuales listados entre los corchetes.                  | `file[12].txt`                 | `file1.txt`, `file2.txt`                        | `file3.txt`, `fileA.txt`|
| `[! ]`        | Coincide con cualquier carácter que no esté listado entre los corchetes.                              | `file[!12].txt`                | `fileA.txt`, `fileB.txt`                        | `file1.txt`, `file2.txt`|
| `[a-z]`       | Coincide con cualquier carácter en el rango especificado (minúsculas de `a` a `z`).                   | `file[a-z].txt`                | `filea.txt`, `filem.txt`, `filez.txt`           | `fileA.txt`, `file1.txt`|
| `[A-Z]`       | Coincide con cualquier carácter en el rango especificado (mayúsculas de `A` a `Z`).                   | `file[A-Z].txt`                | `fileA.txt`, `fileM.txt`, `fileZ.txt`           | `filea.txt`, `file1.txt`|
| `[0-9]`       | Coincide con cualquier carácter en el rango especificado (dígitos de `0` a `9`).                      | `file[0-9].txt`                | `file0.txt`, `file5.txt`, `file9.txt`           | `filea.txt`, `fileA.txt`|
| `{}`          | Coincide con cualquiera de los patrones especificados separados por comas.                            | `file{1,2,3}.txt`              | `file1.txt`, `file2.txt`, `file3.txt`           | `file4.txt`, `fileA.txt`|
| `[[:alnum:]]` | Coincide con cualquier carácter alfanumérico.                                                         | `file[[:alnum:]].txt`          | `file1.txt`, `fileA.txt`, `file9.txt`           | `file_.txt`, `file!.txt`|
| `[[:alpha:]]` | Coincide con cualquier carácter alfabético.                                                           | `file[[:alpha:]].txt`          | `filea.txt`, `fileM.txt`, `fileZ.txt`           | `file1.txt`, `file9.txt`|
| `[[:digit:]]` | Coincide con cualquier dígito.                                                                        | `file[[:digit:]].txt`          | `file0.txt`, `file5.txt`, `file9.txt`           | `fileA.txt`, `file_.txt`|
| `[[:lower:]]` | Coincide con cualquier carácter en minúscula.                                                         | `file[[:lower:]].txt`          | `filea.txt`, `filem.txt`, `filez.txt`           | `fileA.txt`, `fileM.txt`|
| `[[:upper:]]` | Coincide con cualquier carácter en mayúscula.                                                         | `file[[:upper:]].txt`          | `fileA.txt`, `fileM.txt`, `fileZ.txt`           | `filea.txt`, `filem.txt`|
| `[[:space:]]` | Coincide con cualquier carácter de espacio en blanco (espacios, tabuladores, etc.).                   | `file[[:space:]].txt`          | `file .txt`, `file\t.txt`                       | `fileA.txt`, `file1.txt`|
| `[[:punct:]]` | Coincide con cualquier carácter de puntuación.                                                        | `file[[:punct:]].txt`          | `file!.txt`, `file@.txt`, `file#.txt`           | `fileA.txt`, `file1.txt`|

### Lista archivos en el directorio actual donde el nombre tiene un solo carácter adicional antes de la extensión `.txt`, como `archivo1.txt`, `archivoA.txt`, `archivo_.txt`, pero no `archivos.txt` o `archivo12.txt`.
`ls archivo?.txt`

### Lista archivos en el directorio actual donde el nombre del archivo contiene `fotoa.jpg` o `fotob.jpg`, pero no `fotoc.jpg` o `foto1.jpg`.
`ls foto[ab].jpg`

### Busca archivos en `/var/log/` que terminan en `.log` y cuyo nombre no termina en `a`, como `file1.log`, `file2.log`, pero no `filea.log`.
`find /var/log/ -type f -name *[!a].log`

### Lista archivos en el directorio actual donde el nombre del archivo contiene una letra minúscula entre `a` y `z` antes de la extensión `.pdf`, como `reportea.pdf`, `reportex.pdf`, `reportez.pdf`, pero no `reporteA.pdf` o `reporte1.pdf`.
`ls reporte[a-z].pdf`

### Busca archivos en `/data` cuyo nombre contiene una letra mayúscula entre `A` y `Z` antes de la extensión `.csv`, como `dataA.csv`, `dataM.csv`, `dataZ.csv`, pero no `dataa.csv` o `data1.csv`.
`find /data -name 'data[A-Z].csv'`

### Lista archivos en el directorio actual donde el nombre del archivo contiene un dígito entre `0` y `9` antes de la extensión `.png`, como `imagen0.png`, `imagen5.png`, `imagen9.png`, pero no `imagena.png` o `imagenA.png`.
`ls imagen[0-9].png`

### Lista archivos en el directorio actual que terminan en `foto1.jpg`, `foto2.jpg`, `foto3.jpg`, pero no `foto4.jpg` o `fotoA.jpg`.
`ls foto{1,2,3}.jpg`

### Busca archivos en el directorio actual cuyo nombre contiene un carácter alfanumérico antes de la extensión `.txt`, como `archivo1.txt`, `archivoA.txt`, `archivo9.txt`, pero no `archivo!.txt` o `archivo .txt`.
`find . -name 'archivo[[:alnum:]].txt'`

### Lista archivos en el directorio actual cuyo nombre contiene una letra antes de la extensión `.md`, como `nombrea.md`, `nombreZ.md`, `nombref.md`, pero no `nombre1.md` o `nombre!.md`.
`ls nombre[[:alpha:]].md`

### Busca archivos en el directorio actual cuyo nombre contiene un dígito antes de la extensión `.pdf`, como `reporte1.pdf`, `reporte5.pdf`, `reporte9.pdf`, pero no `reporteA.pdf` o `reporte!.pdf`.
`find . -name 'reporte[[:digit:]].pdf'`

### Lista archivos en el directorio actual cuyo nombre contiene una letra minúscula antes de la extensión `.csv`, como `archivox.csv`, `archivoy.csv`, `archivoz.csv`, pero no `archivoA.csv` o `archivo1.csv`.
`ls archivo[[:lower:]].csv`

### Busca archivos en `/images` cuyo nombre contiene una letra mayúscula antes de la extensión `.png`, como `imagenA.png`, `imagenZ.png`, `imagenM.png`, pero no `imagena.png` o `imagen1.png`.
`find /images -name 'imagen[[:upper:]].png'`

### Busca archivos en el directorio actual cuyo nombre contiene un espacio en blanco antes de la extensión `.txt`, como `documento .txt`, `documento	.txt` (con tabuladores), pero no `documentoA.txt` o `documento1.txt`.
`find . -name 'documento[[:space:]].txt'`

### Lista archivos en el directorio actual cuyo nombre contiene un carácter de puntuación antes de la extensión `.md`, como `archivo!.md`, `archivo#.md`, `archivo@.md`, pero no `archivoA.md` o `archivo1.md`.
`ls archivo[[:punct:]].md`

---------

## Expansiones en bash

### Muestra coincidencias de directorios en el nivel raíz del sistema de archivos que contienen una carpeta "log".
`echo /*/log`

### Lista el contenido de los directorios que contienen una carpeta "log" en el nivel superior del sistema de archivos.
`ls /*/log`

### Evalúa la expresión aritmética 2 + 2 y muestra el resultado, que es 4.
`echo $((2+2))`

### Intenta listar un archivo llamado "fichero4.txt", asumiendo que el cálculo de $((2+2)) da 4.
`ls fichero$((2+2)).txt`

### Crea diez directorios numerados del "dir1" al "dir10".
`mkdir dir{1..10}`

### Crea cinco archivos numerados del "fichero1.txt" al "fichero5.txt".
`touch fichero{1..5}.txt`

### Crea cuatro archivos con nombres específicos: "ficheroA1", "ficheroA2", "ficheroB3", y "ficheroB4".
`touch fichero{A{1,2},B{3,4}}`

### Crea una estructura de directorios para los años 2020 a 2024, con subdirectorios para cada mes de enero a diciembre en cada año.
`mkdir {2020..2024}-{01..12}`









