-------------
# Test de Penetración

## 1. Definición del alcance del test de penetración

## 2. Recopilación de información
- **Recopilación pasiva**
- **Recopilación semi-pasiva**
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


# Modificar lenguaje
sudo dpkg-reconfigure locales
sudo reboot

# Actualizar Kali Linux
sudo apt update && sudo apt upgrade -y

# Instalar kalipwm
git clone https://github.com/afsh4ck/kalipwm.git
cd kalipwm
bash kalipwm.sh
sudo reboot

# Habilitar shared folder en Ubuntu
mkdir /mnt/hgfs

# Editar fstab
vi /etc/fstab
# Añadir la línea:
# .host:/ /mnt/hgfs fuse.vmhgfs-fuse auto,allow_other 0 0

sudo reboot
cd /mnt/hgfs
ls  # Debería mostrarse la carpeta compartida previamente, PRUEBAS




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

------------------


METODOLOGÍA DE ESTE CURSO
▪ [Definición del alcance del test de penetración]

▪ Recopilación de información
	+ Recopilación pasiva de información (difícil, resultados pocos concluyentes)
	
	Recolección de información sobre un objetivo determinado, sin que las actividades realizadas por el analista sean mínimamente detectadas por ese objetivo.

	La manera habitua de la recopilación de pasiva de información se realizará mediante el acceso a información almacenada en lugares públicos.

	Herramientas:
		Google Dorks (Hacking con buscadores)
		https://www.exploit-db.com/google-hacking-database

		Ejemplos:

		site:website.com filetype/ext:pdf, sql, txt, etc... 
		"index of" / "chats/logs" / = and, sería buscar "string" y "string"
		ext:sql "MySQL dump" (pass|password|passwd|pwd) site:website.com
		inurl:index.php?id= site:website.com
		site:gov filetype:pdf allintitle:restricted

		https://www.shodan.io/
		https://search.censys.io/

		theHarvester -h


	Resumen herramientas/utilidades (recopilación pasiva de info)
	Google Dorks
	Shodan
	Censys
	Whois
	Archive.org
	The Harvester
		




	+ Reocpilación semi-pasiva de información
	+ Recopilación activa de información
	
▪ Identificación y análisis de vulnerabilidades
▪ Explotación de las vulnerabilidades
▪ Post-explotación
▪ [Elaboración de un documento de reporte]

Google Hacking: Comandos y Operadores Booleanos

Comandos principales Google Hacking

A continuación se muestran los comandos principales que podemos utilizar con Google. Hay que tener en cuenta que todos ellos deben ir seguidos (sin espacios) de la consulta que quiere realizarse:

    define:término - Se muestran definiciones procedentes de páginas web para el término buscado.

    filetype:término - Las búsquedas se restringen a páginas cuyos nombres acaben en el término especificado. Sobretodo se utiliza para determinar la extensión de los ficheros requeridos. Nota: el comando ext:término se usa de manera equivalente.

    site:sitio/dominio - Los resultados se restringen a los contenidos en el sitio o dominio especificado. Muy útil para realizar búsquedas en sitios que no tienen buscadores internos propios.

    link:url - Muestra páginas que apuntan a la definida por dicha url. La cantidad (y calidad) de los enlaces a una página determina su relevancia para los buscadores. Nota: sólo presenta aquellas páginas con pagerank 5 o más.

    cache:url - Se mostrará la versión de la página definida por url que Google tiene en su memoria, es decir, la copia que hizo el robot de Google la última vez que pasó por dicha página.

    info:url - Google presentará información sobre la página web que corresponde con la url.

    related:url - Google mostrará páginas similares a la que especifica la url.  Nota: Es difícil entender que tipo de relación tiene en cuenta Google para mostrar dichas páginas. Muchas veces carece de utilidad.

    allinanchor:términos - Google restringe las búsquedas a aquellas páginas apuntadas por enlaces donde el texto contiene los términos buscados.

    inanchor:término - Las búsquedas se restringen a aquellas apuntadas por enlaces donde el texto contiene el término especificado. A diferencia de allinanchor se puede combinar con la búsqueda habitual.

    allintext:términos - Se restringen las búsquedas a los resultados que contienen los términos en el texto de la página.

    intext:término - Restringe los resultados a aquellos textos que contienen término en el texto. A diferencia de allintext se puede combinar con la búsqueda habitual de términos.

    allinurl:términos - Sólo se presentan los resultados que contienen los términos buscados en la url.

    inurl:término - Los resultados se restringen a aquellos que contienen término en la url. A diferencia de allinurl se puede combinar con la búsqueda habitual de términos.

    allintitle:términos - Restringe los resultados a aquellos que contienen los términos en el título.

    intitle:término - Restringe los resultados a aquellos documentos que contienen término en el título. A diferencia de allintitle se puede combinar con la búsqueda habitual de términos.

Operadores Booleanos Google Hacking

Google hace uso de los operadores booleanos para realizar búsquedas combinadas de varios términos. Esos operadores son una serie de símbolos que Google reconoce y modifican la búsqueda realizada:

    " " - Busca las palabras exactas.

    - - Excluye una palabra de la búsqueda. (Ej: gmail -hotmail, busca páginas en las que aparezca la palabra gmail y no aparezca la palabra hotmail)

    OR (ó |) - Busca páginas que contengan un término u otro.

    + - Permite incluir palabras que Google por defecto no tiene en cuenta al ser muy comunes (en español: "de", "el", "la".....). También se usa para que Google distinga acentos, diéresis y la letra ñ, que normalmente son elementos que no distingue.

    * - Comodín. Utilizado para sustituir una palabra. Suele combinarse con el operador de literalidad (" ").


Shodan: Comandos principales

Comandos relevantes para Shodan

A continuación se presentan algunos de los filtros más relevantes para el uso de Shodan:

    after: Only show results after the given date (dd/mm/yyyy) string

    asn: Autonomous system number string

    before: Only show results before the given date (dd/mm/yyyy) string

    category: Available categories: ics, malwarestring

    city: Name of the city string

    country: 2-letter country code string

    geo: Accepts between 2 and 4 parameters. If 2 parameters: latitude, longitude. If 3 parameters: latitude, longitude, range. If 4 parameters: top left latitude, top left longitude, bottom right latitude, bottom right longitude.

    hash: Hash of the data property integer

    has_ipv6: True/False boolean

    has_screenshot: True/False boolean

    server: Devices or servers that contain a specific server header flag string

    hostname: Full host name for the device string

    ip: Alias for net filter string

    isp: ISP managing the netblock string

    net: Network range in CIDR notation (ex.199.4.1.0/24) string

    org: Organization assigned the netblock string

    os: Operating system string

    port: Port number for the service integer

    postal: Postal code (US-only) string

    product: Name of the software/product providing the banner string

    region: Name of the region/state string

    state: Alias for region string

    version: Version for the product string

    vuln: CVE ID for a vulnerability string



   Useful commands


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





