-------------
# Test de Penetración

## 1. Definición del alcance del test de penetración

## 2. Recopilación de información
- **Recopilación pasiva**
- **Recopilación activa**

## 3. Identificación y análisis de vulnerabilidades

## 4. Explotación de las vulnerabilidades

## 5. Post-explotación

## 6. Elaboración de un documento de reporte

-------------


# Metodologías Principales

## 1. OSSTMM (Open-Source Security Testing Methodology Manual)
[Enlace al documento](https://www.isecom.org/OSSTMM.3.pdf)

## 2. The Penetration Testing Execution Standard
[Enlace al sitio web](http://www.pentest-standard.org/index.php/Main_Page)

## 3. ISSAF (Information Systems Security Assessment Framework)

## 4. OTP (OWASP Testing Project)

-------------

# Comandos útiles para instalación y configuración de entornos

Modificar lenguaje

`sudo dpkg-reconfigure locales`

`sudo reboot`




Actualizar Kali Linux

`sudo apt update && sudo apt upgrade -y`



Habilitar shared folder en Ubuntu
`mkdir /mnt/hgfs`

Editar fstab
`vi /etc/fstab`

Añadir la línea:
`.host:/ /mnt/hgfs fuse.vmhgfs-fuse auto,allow_other 0 0`

`sudo reboot`
`cd /mnt/hgfs`
`ls`  Debería mostrarse la carpeta compartida previamente, PRUEBAS

Instalar kalipwm
`git clone https://github.com/afsh4ck/kalipwm.git`
`cd kalipwm`
`bash kalipwm.sh`
`sudo reboot`

Intalar miniconda para crear un entorno virtual y mantener varias versiones de una misma herramienta
https://docs.anaconda.com/miniconda/install/
https://repo.anaconda.com/miniconda/

Después de instalar Miniconda, debemos cerrar la terminal y abrirla nuevamente.
Aparecerá `(base)` en el prompt.

Si no aparece (base), ejecutaremos lo siguiente:
`echo 'export PATH="$HOME/miniconda3/bin:$PATH"' >> ~/.zshrc`
`source miniconda3/bin/activate`

Para eliminar (base) del prompt, ejecutamos: `conda config --set auto_activate_base false`.

Para crear un nuevo entorno (añadiendo el canal conda-forge , que tiene un soporte más amplio para paquetes)
`conda create -n "old_harvester" python=3.8.0 -c conda-forge`

Instalar una version anterior de theHarvester, (3.2.2 incluye Google)
`mkdir old_harvester (/home/kali/)`
`wget https://github.com/laramies/theHarvester/archive/refs/tags/3.2.2.zip`
`unzip 3.2.2.zip`
`pip install -r requirements/base.txt (instalar dependencias para esta versión)`


-- Modificar lenguaje 
sudo dpkg-reconfigure locales
sudo reboot


-- Actualizar Kali Linux
sudo apt update && sudo apt upgrade -y

-- Install kalipwn
git clone https://github.com/afsh4ck/kalipwm.git
cd kalipwm
bash kalipwm.sh
sudo reboot

-- Habilitar shared folder Ubuntu
En VMWare > Sharing > [añadir carpeta, e.g: PRUEBAS]

En Ubuntu:
mkdir /mnt/hgfs

vi /etc/fstab 
añadir: 
.host:/ /mnt/hgfs fuse.vmhgfs-fuse auto,allow_other 0 0

sudo reboot
cd /mnt/hgfs
ls (debería mostrarse la carpeta compartida previamente, PRUEBAS)


Listado de atajos para la shell de Linux

A continuación os dejo un listado de algunos atajos interesantes para la shell de Linux. Os recomiendo que le echéis un ojo a todos y seleccionéis los que os resulten más cómodos para vuestro día a día.

Ctrl + A → Ir al principio de la línea en la que se está escribiendo.

Ctrl + E → Ir al final de la línea en la que se está escribiendo.

Ctrl + L → Borra la pantalla, similar al comando clear

Ctrl + U → Borra la línea anterior a la posición del cursor. Si está al final de la línea, borra toda la línea.

Ctrl + H → Borra el carácter anterior a la posición del cursos. Igual que retroceso.

Ctrl + R → Permite buscar entre los comandos utilizados anteriormente.

Ctrl + C → Interrumpe la ejecución de un programa.

Ctrl + D → Cierra la shell actual.

Ctrl + W → Corta la palabra anterior a la posición cursor.

Ctrl + K → Corta la línea siguiente a la posición del cursor.

Ctrl + T → Intercambia los dos últimos caracteres anteriores a la posición del cursor.

Esc + T → Intercambia las dos últimas palabras anteriores a la posición del cursor.

Alt + . o !$ → Referencia el último argumento del comando anterior.

Alt + F → Avanza el cursor una palabra en la línea actual.

Alt + B → Retrocede el cursor una palabra en la línea actual.

Alt + l/u → Convierte la palabra en mayúsculas o minúsculas.

Tab → Autocompleta nombres de archivos y carpetas.



Índice curso Linux
Sección 4: La shell de Linux
Sección 8: Permisos y usuarios
Lectura Comandos
Lectura Comandos
La shell de Linux Clear, history
Permisos y usuarios Passwd, shadow, group
Comandos de la shell Type
Lectura, Escritura y
Ejecución
Rwx-rwx-rwx
El usuario root Root
Información de los
comandos
Help, man, info, whatis, apropos
Modificación de permisos
en octal
Chmod, notación octal
Manejo de commandos y
expresiones lógicas
&&, ||
Modificación de permisos
simbólica
Chmod, notación simbólica
Atajos Documento de atajos en lectura 13
Permisos por defecto Umask
Caso práctico: Creando
nuestro propio alias
alias
Setuid, Setgid, Sticky bit Setuid, setgid, sticky bit
Cambio de identidad Su
Sección 5: Sistema de ficheros
Sudo Sudo
Sudoers sudoers
Lectura Comandos
El Sistema de ficheros Tree,
Gestión de usuarios y
grupos
Useradd, groupadd, usermod,
passwd, delgroup…
Navegación Pwd, ls, cd, ., .., -
Cambio de propietario Chown, chgrp
Ficheros Tipos de ficheros en Linux
Sección 9: Procesos
Creación de ficheros y
editores de texto
Mkdir, nano, pico, vi, emacs
Lectura Comandos
Visualización de ficheros y
directorios
File, more, less, cat
Procesos en Linux /proc, pidof
Manipulación de ficheros Cp, mv, rm
Find
Visualización estática de
procesos
Ps
Búsqueda de ficheros y
directories
Visualización dinámica de
procesos
Top
Principales directorios de
Linux
Home, lib, media, mnt, sys, usr, var,
snap, opt…
Interrupción de procesos Ctrl+C, Ctrl+Z, bg
Procesos en segundo plano &, jobs, fg, bg
Sección 6: Conceptos avanzados
del Sistema de ficheros
Señales Kill, killall, STOP, INT, KILL…
Init, demonios y servicios Init, init.d
Gestión de servicios Init.d, systemctl, service
Lectura Comandos
Apagado del sistema Halt, poweroff, reboot, shutdown
Inodos Debugfs, df
Cambio de prioridad Nice, renice
Dentries Debugfs, df
Soft Links Ln -s
Sección 10: Networking
Hard Links Ln
Wildcards *, ?, [, ], classes…
Lectura Comandos
Shell expansions Echo, $(()), {}…
Interfaces de red ip link
Command substitution $()
Direcciones IP ip addr
Comillas en la shell ‘, “
Escapando caracteres \, \t, \n…
Routing ip route, traceroute
Sniffers Wireshark, Tcpdump
Sección 7: Redirecciones y
pipelines
Examinando la red Ping, nmap
DHCP y DNS Dhclient, resolv.conf
Lectura Comandos
Descarga y subida de
información
Curl, wget
I/O Redirection Stdout, stderr, stdin
Conexiones remotas Ssh
Standard Output >
Intercambio de ficheros I ftp
Standard Error 2>
Intercambio de ficheros II Sftp
/dev/null /dev/null
Standard Input <
Visualizando las conexiones
activas
Ss
Pipelines |
Netstat netstat
Filtros y búsquedas Sort, uniq, wc
Filtros y búsquedas II Grep, head, tail, tee
Comando sed sed
Sección 11: Gestión de paquetes
y liberías
Lectura Comandos
Buscar, instalar y actualizar
paquetes
Apt update, sources.list, apt-cache,
apt upgrade
Instalación manual de
paquetes
dpkg
Eliminar, listar y buscar
paquetes
Apt remove, dpkg
Sección 12: El entorno
Lectura Comandos
El entorno en Linux Printenv, alias, set
Como se establece el
entorno
/etc/environment, /etc/profile,
/etc/profile.d, /etc/bash.bashrc,
~/.profile, ~/.bashrc, ~/bash_profile,
~/bash_login
Modificando el entorno Creación de variables de Shell y de
entorno
Variables de entorno
interesantes
SHELL, HOME, LANG, PATH, PWD, _,
USER…
Sección 13: Dispositivos de
Almacenamiento externos
Lectura Comandos
Dispositivos extraibles mount
Montar y desmontar
dispositivos
Mount, umount, /dev
Identificando el nombre del
dispositivo
/dev, syslog
Sección 14: Archivando y
Comprimiendo ficheros
Lectura Comandos
Comprimiendo y
descomprimiendo ficheros
Gzip, gunzip
Otra solución para
comprimir y descomprimir
Bzip2, bunzip2
Archivando ficheros Tar
Archivar y comprimir con zip Zip, unzip
Sección 15: Expresiones regulares
Y búsquedas avanzadas
Lectura Comandos
Referenciar cualquier
carácter
.
Símbolos de anclaje ^, $
Expresiones con corchetes [, ]
POSIX Classes Clases Posix (Ej. [:alnum:], [:word:],
[:alpha:]…
Alternancia y Paréntesis |, (, )
Cuantificadores *, +, {,}
Editores de expresiones
regulares
regex101
Shell Script
Sección 17: Introducción a
Shell Script
Lectura Comandos
Shebang y comentarios #!/bin/bash, #
Variables Definición de variables
Constantes Declare –r
Here Documents <<
Funciones Function, return
Parámetros y argumentos $, parámetros
Variables Locales local
Sección 18: Control de Flujo
Lectura Comandos
Sentencia if If, else,
Comando test Test, [ ]
Condiciones avanzadas [[ ]]
Combinando expresiones AND, OR, NOT
Comando Exit Exit, return
Bucle for For
Bucle while While
Break y Continue Break, continue
Bucle until Until
Sentencia case case
Sección 19: Otros componentes
importantes
Lectura Comandos
Lectura de teclado Read
Argumentos en un script $
Conceptos avanzados sobre
argumentos y parámetros
$#, $0, ${}, shift
Importando otros scripts Source
Arrays Declare –a, arrays asociativos
Operadores lógicos &&, ||


Comandos:
---------

echo 'export PATH="$HOME/miniconda3/bin:$PATH"' >> ~/.zshrc

source miniconda3/bin/activate

Metodologías
Hacking Ético

IMPORTANCIA DE LAS METODOLOGÍAS
▪ Las metodologías nos facilitan la realización de un
conjunto de actividades en un orden determinado y
estableciendo una prioridad adecuada para intentar
garantizar el éxito y alcanzar un objetivo final

METODOLOGÍAS PRINCIPALES
▪ OSSTMM (Open-Source Security Testing Methodology Manual):
https://www.isecom.org/OSSTMM.3.pdf
▪ The Penetration Testing Execution Standard: http://www.pentest-
standard.org/index.php/Main_Page
▪ ISSAF (Information Systems Security Assessment Framework)
▪ OTP (OWASP Testitng Project)

METODOLOGÍA DE ESTE CURSO
▪ Definición del alcance del test de penetración
▪ Recopilación de información
▪ Identificación y análisis de vulnerabilidades
▪ Explotación de las vulnerabilidades
▪ Post-explotación
▪ Elaboración de un documento de reporte


DEFINICIÓN DEL ALCANCE DEL HACKING ÉTICO
▪ Antes de realizar ninguna acción, discutir con el cliente las tareas
que llevará a cabo el analista durante el Hacking Ético, así como los
roles y responsabilidades de ambos
▪ Asegurar mediante contrato firmado que las acciones que se llevan
a cabo son en representación del cliente
▪ Análisis de las políticas de la organización que definen el uso que
los usuarios hacen de los sistemas y de la infraestructura
▪ Procedimiento en el caso de que se localice una intrusión por un
tercero.

