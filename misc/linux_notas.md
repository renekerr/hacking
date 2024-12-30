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


# Atajos de Linux

## Tabla de Atajos de Teclado

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


## Comandos:
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

`find /var/log/ -type f ! -name "*.log" 2>/dev/null`

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







