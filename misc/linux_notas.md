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






