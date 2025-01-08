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
