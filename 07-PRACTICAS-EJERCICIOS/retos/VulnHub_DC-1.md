## DC-1 Vulhub | Write-Up

### Enlace al desafío en Vulnhub

### Descripción
DC-1 es un laboratorio vulnerable diseñado para que principiantes adquieran experiencia en **penetration testing**. Su nivel de dificultad varía según las habilidades y conocimientos del usuario.

### Requisitos para completarlo
- Conocimientos básicos de **Linux**.
- Familiaridad con la línea de comandos de **Linux**.
- Experiencia con herramientas básicas de pruebas de penetración, como las disponibles en **Kali Linux** o **Parrot Security OS**.

### Objetivo principal
El objetivo es encontrar y leer la bandera ubicada en el directorio de inicio de **root**. Aunque no es necesario ser root para acceder a la bandera, se requieren privilegios de root.

### Detalles adicionales
- **Número de banderas:** 5 (contienen pistas útiles para principiantes).
- **Opcional:** Usuarios avanzados pueden optar por saltar las banderas intermedias e ir directamente por root.

### Configuración del entorno
Descargaremos la máquina y la importaremos en **VirtualBox**, utilizando una máquina Kali Linux para el acceso al laboratorio. Se debe crear una red NAT:

1. Ir a Archivo > Herramientas > Administrador de red > Redes NAT y crear una nueva red.
2. Ambas máquinas utilizarán esta red NAT creada previamente.




### Descubrimiento de IP
Para descubrir la dirección IP de la máquina del laboratorio, utilizaremos **Netdiscover**.

1. Iniciar ambas máquinas: DC-1 y Kali Linux.
2. Desde Kali Linux:
   - Ejecutar `ifconfig` para verificar la configuración de las interfaces de red.
   - Identificar la dirección IP de la interfaz conectada (eth0).
   - Usar Netdiscover para escanear y detectar la IP de DC-1.

### Escaneo de red (nmap) y enumeración
Ejecutaremos **nmap** para escanear puertos abiertos, detectar servicios en ejecución y obtener información adicional sobre el sistema operativo.

- En el puerto 80 se ejecuta **Drupal**, confirmado con `whatweb`.

### Explotación
Usaremos el framework **Metasploit** para explotar esta máquina.

1. Lanzar el exploit correspondiente.
2. Ejecutar `ls` desde **Meterpreter** para ver la primera bandera (flag1.txt).

#### Flag1
“Todo buen CMS necesita un archivo de configuración, lo mismo que tú.”  
Esto sugiere buscar el archivo de configuración del CMS en `sites/default/settings.php`.

3. Ejecutar `cat settings.php` para obtener la segunda bandera (flag2) y descubrir acceso a una base de datos MySQL.

#### Flag2
“Los ataques de fuerza bruta y de diccionario no son las únicas formas de obtener acceso (y lo necesitará). ¿Qué puede hacer con estas credenciales?”

Para obtener un shell del sistema, usar el comando:

```bash
python -c "import pty; pty.spawn('/bin/bash')"
```

### Acceso a la base de datos
Para obtener la contraseña del usuario admin, podemos usar herramientas como **hashcat** o **john the ripper**, pero descubrimos un exploit para crear un usuario administrador mediante **searchsploit**.

### Acceso al CMS
Probamos y comprobamos que podemos acceder:

- En ‘Content’ obtendremos la bandera 3 (flag3.txt).

#### Flag3
“Permisos especiales ayudarán a encontrar la passwd, pero necesitarás usar -exec para averiguar cómo obtener lo que está en la sombra.”

Al consultar `/etc/passwd`, encontramos un usuario llamado flag4 en `/home`, lo que nos llevará a la bandera 4 (flag4.txt).

#### Flag4
“¿Puedes usar este mismo método para encontrar o acceder a la bandera en root? Probablemente. Pero tal vez no sea tan fácil. ¿O quizás sí lo sea?”

Utilizar el comando `find` para acceder a root.

### Posexplotación
En esta fase, para escalar privilegios y obtener acceso root mediante binarios SUID, podemos usar el siguiente comando:

```bash
find / -perm -u=s 2>/dev/null
```

Este comando permite encontrar binarios SUID que podrían ser explotados para escalar privilegios. En la lista vemos que se encuentra `find`. Consultando **GTFOBins**, podemos usar el siguiente comando para escalar privilegios:

```bash
find . -exec /bin/sh \; -quit
```

