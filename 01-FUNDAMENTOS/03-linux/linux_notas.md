# Guía Completa de Comandos y Conceptos de Linux

## 1. Operadores y Redirecciones

### Operadores Básicos
| Símbolo | Descripción |
|---------|-------------|
| & | Ejecución en segundo plano |
| && | Ejecución condicional |
| > | Redirección de salida (sobreescribe) |
| >> | Redirección de salida (añade) |

### Ejemplos de Redirección
- `echo "Hola, mundo!" > mi_archivo.txt`
- `echo "Esta es una nueva línea." >> mi_archivo.txt`
- `long-running-command &`
- `cd /ruta/del/directorio && ls -la`

### Stdout y Stderr
- `ls -lah > fichero_salida_ls.txt`
- `ls -lah fditufy >> fichero_salida_ls.txt`
- `ls -lah > fichero_salida_2.txt 2>&1`
- `ls -lah &>> fichero_salida_moderna.txt`

## 2. Stdin y Pipelines

### Stdin
- `cat > file_stdin.txt`
- `cat file1.txt file2.txt > file12.txt`

### Pipelines
- `ls -lah /usr/bin/ | less`
- `ls /usr/bin/ /var/log | sort | less`

## 3. Atajos de Teclado

| Atajo | Descripción |
|-------|-------------|
| Ctrl + A | Ir al principio de la línea |
| Ctrl + E | Ir al final de la línea |
| Ctrl + L | Limpiar pantalla |
| Ctrl + U | Borrar línea anterior al cursor |
| Ctrl + R | Buscar comandos anteriores |
| Ctrl + C | Interrumpir programa en ejecución |
| Ctrl + D | Cerrar shell actual |
| Alt + . o !$ | Referenciar último argumento |
| Tab | Autocompletar archivos y carpetas |

## 4. Comandos de Búsqueda y Filtrado

### find
- `find / -name ls 2> /dev/null`
- `find / -name firefox -type d 2> /dev/null`
- `find / -name shadow ! -path "/snap/*" -ls 2> /dev/null`
- `find /usr/bin -type f -name "*[[:digit:]]" 2>/dev/null`
- `find / -type f -name "*_*_*.txt" 2>/dev/null`
- `find /var/log/ -type f -not -name "*.log" 2>/dev/null`
- `find . -type f -size 1033c 2>/dev/null`
- `find /your/path -type f -user myusernane -group mygroup -size 33c`
- `find ~/project/files/ -type f \( -name "*.txt" -o -name "*.pdf" \)`
- `find ~/project/files -type f ! -name "*.txt"`
- `find ~/project/files -type f \( -name "*.jpg" -o -name "*.png" \) -size +0c`
- `find ~/project/files -type f \( -name "*.jpg" -o -name "*.png" \) -size +0c`
- `find ~/project/files/documents -type f ! -name "*.pdf"`
- `find ~/project/files/documents -type f ! -name "*.pdf"`
- `find ~/project/files/images -type f \( -name "*.jpg" -o -name "*.png" \) \( -size 0 -o -size +1k \)`
- 


### Filtros
- `sort`: Ordena líneas de texto
- `uniq`: Elimina o cuenta líneas repetidas
- `wc`: Cuenta líneas, palabras y caracteres
- `grep`: Busca patrones en texto
- `head`: Muestra las primeras líneas de un archivo
- `tail`: Muestra las últimas líneas de un archivo
- `tee`: Escribe la salida a un archivo y también la muestra en pantalla

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


### Ejemplos de Uso
- `ls archivo?.txt`
- `ls foto[ab].jpg`
- `find /var/log/ -type f -name *[!a].log`
- `ls reporte[a-z].pdf`
- `find /data -name 'data[A-Z].csv'`
- `ls imagen[0-9].png`
- `ls foto{1,2,3}.jpg`

## 6. Expansiones en Bash

### Expansión de Rutas
- `echo /*/log`
- `ls /*/log`

### Expansión Aritmética
- `echo $((2+2))`
- `ls fichero$((2+2)).txt`

### Expansión de Llaves
- `mkdir dir{1..10}`
- `touch fichero{1..5}.txt`
- `touch fichero{A{1,2},B{3,4}}`
- `mkdir {2020..2024}-{01..12}`

## 7. Sustitución de Comandos

- `ls -la $(which cat)`
- `echo $(python3 -c 'print("Hola")')`

## 8. Uso de Comillas y Escapado

### Comillas
- `echo $(ls)` vs `echo "S(ls)"`
- `echo "la ruta de cat es $(which cat)"`
- `echo 'la ruta de cat es $(which cat)'`
- `echo "estas son comillas simples ''"`
- `echo 'estas son comillas dobles ""'`

### Escapado
- `echo "Este es un texto con comillas dobles \"entre comillas\"."`
- `echo "Esto es un texto con espacio\ dentro\ de\ la\ cadena."`

## 9. Comando sed

### Ejemplos Prácticos
1. `sed 's/vieja_palabra/nueva_palabra/g' archivo.txt`
2. `sed '/^$/d' archivo.txt`
3. `sed -n '5,10p' archivo.txt`
4. `sed 's/^/PREFIJO: /' archivo.txt`
5. `sed 's/^...//' archivo.txt`
6. `sed 's/ */ /g' archivo.txt`

## 10. Ejemplos Adicionales

- `ls -lh | sort -k5 -h`: Ordena archivos por tamaño
- `sort -t, -k2 -n fichero.csv`: Ordena CSV por segundo campo
- `head -n 55 /var/log/auth.log | tail -n 1`: Muestra línea específica

-----
# Permisos en Directorios

### Descripción de Permisos

- **Ejecución (`x`)**: Permite acceder a los archivos dentro del directorio.
- **Lectura (`r`)**: Permite enumerar las entradas del directorio.
- **Escritura (`w`)**: Permite crear y eliminar entradas en el directorio.

### Consideraciones

- **Lectura o escritura sin ejecución**: No son útiles.
- **Ejecución sin lectura**: Permite acceder a archivos si se conoce su nombre exacto (protección rudimentaria).

### Permisos Útiles

- `---`: Sin acceso.
- `--x`: Acceso a archivos conocidos por nombre.
- `r-x`: Acceso normal de sólo lectura.
- `rwx`: Acceso normal de lectura y escritura.




## Atajos útiles en Linux
*   CTRL+L: Limpia la pantalla rápidamente.
*   Flecha arriba: Recupera el último comando escrito.
*   2>/dev/null: Excluye archivos/directorios sin permisos al ejecutar find.

## Procesos en Linux

*   **ps**: Ver procesos.
    

bash
    ps aux


*   **top**: Monitorizar procesos en tiempo real.
*   **kill**: Terminar un proceso.
    

bash
    kill <PID>


*   **systemctl**: Gestionar servicios.
    

bash
    systemctl start apache2
    systemctl enable apache2


*   **comando &**: Ejecutar en segundo plano.
*   **fg**: Traer proceso al primer plano.
*   **cron**: Programar tareas.
    

bash
    crontab -e



## Búsqueda y Administración de Archivos en Linux

*   **find**: Buscar archivos.
    

bash
    find [ruta] -type f -name [nombre]


*   **cp**: Copiar archivos.
    

bash
    cp [archivo/carpeta] [directorio]


*   **mv**: Mover/renombrar archivos.
    

bash
    mv [archivo] [directorio]


*   **touch**: Crear archivos.
    

bash
    touch [nombre]


*   **mkdir**: Crear directorios.
    

bash
    mkdir [nombre]


*   **nano/cat**: Editar/Ver archivos.
    

bash
    nano [archivo]
    cat [archivo]


*   **scp**: Subir archivos a remoto.
    

bash
    scp [archivo] [usuario]@[IP]:/[directorio]


*   **./[script]**: Ejecutar script Bash.


** Comandos para Revisar Uso de Espacio en Disco**

| Comando       | Descripción                                                                      | Ejemplo           |
|---------------|----------------------------------------------------------------------------------|-------------------|
| `df -h`       | Muestra espacio libre por sistema de archivos (human-readable).               | `df -h`            |
| `df -Th`      | Muestra espacio libre + tipo de sistema de archivos (human-readable).          | `df -Th`           |
| `df -i`       | Muestra información sobre el uso de inodos.                                       | `df -i`            |
| `du -sh <dir>`| Tamaño total de un directorio (human-readable).                               | `du -sh /home`     |
| `du -h --max-depth=1 <dir>` | Tamaño de subdirectorios directos (human-readable).                             | `du -h --max-depth=1 /home`|
| `btrfs filesystem df /` | Información detallada de uso de espacio en sistemas Btrfs (requiere Btrfs).   |  `sudo btrfs filesystem df /` |
| `lsblk`       | Lista los dispositivos de bloque (discos, particiones).                        | `lsblk`           |

**`less` Cheat Sheet**

| Acción        | Comando | Descripción                                                                              |
|----------------|---------|------------------------------------------------------------------------------------------|
| **Navegación** |         |                                                                                          |
| Avanzar Página   | `SPACE` | Moverse una ventana hacia adelante.                                                        |
| Retroceder Página  | `b`       | Moverse una ventana hacia atrás.                                                        |
| Avanzar Media Página | `d`       | Moverse media ventana hacia adelante.                                                     |
| Retroceder Media Página| `u`       | Moverse media ventana hacia atrás.                                                     |
| Línea Siguiente  | `j`       | Moverse una línea hacia adelante.                                                        |
| Línea Anterior  | `k`       | Moverse una línea hacia atrás.                                                        |
| Ir al Final     | `G`       | Ir al final del archivo.                                                                |
| Ir al Inicio    | `g`       | Ir al principio del archivo.                                                             |
| Salir          | `q` o `ZZ`| Salir del visor `less`.                                                                |
| **Búsqueda**  |         |                                                                                          |
| Buscar Siguiente  | `/pattern`| Buscar la siguiente ocurrencia de "pattern".                                                  |
| Buscar Anterior  | `?pattern`| Buscar la ocurrencia anterior de "pattern".                                                  |
| Siguiente Coincidencia| `n`       | Ir a la siguiente coincidencia (en la dirección de búsqueda).                                    |
| Anterior Coincidencia| `N`       | Ir a la coincidencia anterior (en la dirección de búsqueda).                                    |
| **Otros**      |         |                                                                                          |
| Tail -f        | `F`       | Simular el comportamiento de `tail -f` (mostrar actualizaciones en tiempo real).                    |
| Marcar Posición  | `ma`      | Marcar la posición actual con la letra 'a' (reemplaza 'a' con cualquier letra).                         |
| Ir a Posición Marcada | `'a`     | Ir a la posición marcada con la letra 'a' (reemplaza 'a' con la letra de la marca).                  |
| Filtrar Líneas  | `&pattern`| Mostrar solo las líneas que coincidan con "pattern".                                              |
| Editar Archivo   | `v`       | Abrir el archivo en el editor de texto configurado.                                          |
| Estadísticas     | `CTRL+G` | Mostrar el nombre del archivo, número de línea, byte y porcentaje del archivo que se está viendo. |
