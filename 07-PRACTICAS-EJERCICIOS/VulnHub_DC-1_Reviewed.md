# DC-1 Vulhub | Write-Up

---

# **DC-1 Vulhub**

[**Enlace al desafío en Vulnhub**](https://www.vulnhub.com/entry/dc-1,292/)

## **Descripción**

DC-1 es un laboratorio vulnerable diseñado específicamente para que principiantes adquieran experiencia en pruebas de penetración. Su nivel de dificultad dependerá de las habilidades, conocimientos y capacidad de aprendizaje del usuario.

### **Requisitos para completarlo**

- Conocimientos básicos de Linux.
- Familiaridad con la línea de comandos de Linux.
- Experiencia con herramientas básicas de pruebas de penetración, como las disponibles en **Kali Linux** o **Parrot Security OS**.

### **Objetivo principal**

El objetivo es encontrar y leer la bandera ubicada en el directorio de inicio de **root**. Aunque no es necesario ser root para acceder a la bandera, sí se requieren privilegios de root.

### **Detalles adicionales**

- **Número de banderas:** 5
Estas banderas contienen pistas útiles para principiantes.
- **Opcional:** Los usuarios más avanzados pueden optar por saltar las banderas intermedias e ir directamente por root.

### 

---

Descargaremos la máquina y la importaremos en VirtualBox y utilizaremos una máquina Kali Linux para el acceso a la máquina laboratorio. 

En VirtualBox tendremos que tener creado previamente una red NAT: 

Archivo > Herramientas > Administrador de red > Redes NAT y creamos una nueva red (con + Crear)

![image](https://github.com/user-attachments/assets/fe4b3f3b-b818-4b2e-ac77-cfc508431d23)

Y ambas máquinas van a utilizar esta red NAT creada previamente:

![image](https://github.com/user-attachments/assets/f797b7a9-8bf9-45b9-8fd6-15f7d8d473cf)
![image](https://github.com/user-attachments/assets/2a17293e-8a4d-47d2-b7c2-fe206dc8f7be)

### **Descubrimiento de IP.**

Para descubrir la dirección IP de la máquina del laboratorio, utilizaremos **Netdiscover**.

Primero, iniciamos ambas máquinas: **DC-1** y nuestra **Kali Linux**.

Luego, desde Kali Linux, seguimos estos pasos:

1. Ejecutamos `ifconfig` para verificar la configuración de las interfaces de red.
2. Identificamos la dirección IP de la interfaz conectada a la red (**eth0**).
3. Utilizamos **Netdiscover** para escanear y detectar la IP de **DC-1**, ya que ambas máquinas comparten el mismo segmento de red.

   ![image](https://github.com/user-attachments/assets/d4216175-c2d5-4b7e-b89d-759be256a5cd)
   ![image](https://github.com/user-attachments/assets/9b5164fd-fa1b-4199-be3b-f37e07b7f67f)


Descubrimos la máquina DC-1

![image](https://github.com/user-attachments/assets/5445bfb9-fea9-47a4-9354-292de0fa9a34)

Comprobamos que la máquina está accesible: 

![image](https://github.com/user-attachments/assets/d5bcc1cb-3439-4e31-9bad-c72e4db1cff3)

## **Escaneo** de red (nmap) y enumeración.

Ejecutaremos nmap  para escanear los puertos abiertos, detectar los servicios en ejecución y obtener información adicional, como el sistema operativo.

![image](https://github.com/user-attachments/assets/34146c67-11b3-4512-8536-b76f5f671931)

En el puerto 80 tenemos corriendo Drupal y con whatweb confirmamos versión:

![image](https://github.com/user-attachments/assets/b9c0fc4c-e269-40f1-9b6a-651217142999)


Navegación por el puerto HTTPS (80) e identificación del CMS Drupal.

![image](https://github.com/user-attachments/assets/d6a7ac26-e1ca-4320-b0a7-9524d1dee144)

Al buscar en Google ("drupal 7 site:exploit-db.com") o usar searchsploit, se encuentran múltiples vulnerabilidades documentadas de Drupal 7 en Exploit-DB, destacando especialmente Drupalgeddon. 

Drupal < 7.58 / < 8.3.9 / < 8.4.6 / < 8.5.1 - 'Drupalgeddon2' Remote Code Execution
CVE-2018-7600

### **Explotación**

Explotaremos esta máquina utilizando el framwork metasploit.

![image](https://github.com/user-attachments/assets/e0db3fbc-1aed-4135-8677-eeda74990504)

Usaremos el exploit 1, indicando la ip de la máquina objetivo

![image](https://github.com/user-attachments/assets/b6808ecc-5e97-486f-b168-2ba1c390eca7)

Lanzamos un ls desde meterpreter y vemos que tenemos la primera bandera (flag1.txt)

![image](https://github.com/user-attachments/assets/51394ced-c002-42d2-a14b-9c7b631998d5)

**Flag1**

“Todo buen CMS necesita un archivo de configuración, lo mismo que tú.”

Esto nos indica que quizás sería buena idea buscar la ruta donde se guarda el fichero de configuración del CMS. Una simple búsqueda en Google nos indica que la configuración del sistema Drupal la podemos encontrar en el archivo **sites/default/settings.php**

![image](https://github.com/user-attachments/assets/ebce0eb4-cecf-448c-adfa-2d7f1b30ba55)

Lanzamos un cat settings.php y justo al comienzo del fichero obtenemos la segunda bandera (flag2), al mismo tiempo que descubrimos que al parecer podemos acceder a una base de datos en mysql.

![image](https://github.com/user-attachments/assets/9f28438c-5000-493a-b463-ec0ba295aec2)

**Flag2**

“Los ataques de fuerza bruta y de diccionario no son las únicas formas de obtener acceso (y lo necesitará). Qué puede hacer con estas credenciales?”

Para obtener un bash del sistema, usamos el comando **shell** de Meterpreter y, tras abrir un canal, ejecutamos:

`python -c "import pty; pty.spawn('/bin/bash')"`

Esto nos da acceso al prompt del sistema:

![image](https://github.com/user-attachments/assets/25cdfe8a-c8fd-4b6f-a8e0-e051f456ab12)

Aprovechamos la información anterior para acceder  a la base de datos:

![image](https://github.com/user-attachments/assets/f6d1baa5-ce6e-413f-837b-d91f16b4941c)
![image](https://github.com/user-attachments/assets/bc1c9f0e-5a14-4977-9ed3-eeb8fa02695b)


Para obtener la contraseña del usuario admin podemos usar hashcat o john the ripper. 

Sin embargo, con searchsploit descubrimos un exploit para crear un usuario administrador, que utilizaremos para acceder al CMS.

![image](https://github.com/user-attachments/assets/46a1aab8-1b36-41e4-88af-39106ef628e2)
![image](https://github.com/user-attachments/assets/94d5bedb-3317-4293-950d-1ca94a56b37b)
![image](https://github.com/user-attachments/assets/7376d17d-d4ed-44e2-99c1-c414b84ae73d)

Probamos y comprobamos que podemos acceder:

![image](https://github.com/user-attachments/assets/d8764dba-030d-4ba4-af85-f1d9c2b2ebb1)

Si vamos a ‘Content’ obtendremos la bandera 3 (flag3.txt)

![image](https://github.com/user-attachments/assets/d601f63b-04b3-4213-b57c-3cf23069627d)
![image](https://github.com/user-attachments/assets/78a5fd74-d4a5-48f8-b976-02702bcc3582)

**Flag3**

Permisos especiales ayudarán a encontrar la **passwd**, pero necesitarás usar `-exec` para averiguar cómo obtener lo que está en la sombra.

Si consultamos `/etc/passwd` que contiene información sobre los usuarios del sistema, nos encontramos con que existe un usuario llamado flag4, y que además se encuentra en /home.

Esto nos llevará a la bandera 4 (flag4.txt)

![image](https://github.com/user-attachments/assets/93fff86b-1d07-4541-add7-fdee7623cde6)

**Flag4**

¿Puedes usar este mismo método para encontrar o acceder a la bandera en root?

Probablemente. Pero tal vez no sea tan fácil. ¿O quizás sí lo sea?

O lo que es lo mismo, utilizar el comando find para acceder a root.

### Posexplotación

En la fase de **posexplotación**, para escalar privilegios y obtener acceso **root** mediante binarios **SUID**, podemos usar el siguiente comando: 

find / -perm -u=s 2>/dev/null

**`perm -u=s`**: Filtra los archivos que tienen el bit **SUID** habilitado para el propietario del archivo. El `u=s` especifica que el bit SUID está establecido.

![image](https://github.com/user-attachments/assets/7f591442-2205-4492-b25d-4e7e50787990)

Este comando permite encontrar binarios SUID que podrían ser explotados para escalar privilegios y obtener acceso de root. En la lista vemos que se encuentra find. Si consultamos GTFOBins, vemos que, por ejemplo, podemos usar el comando siguiente para escalar privilegios y obtener una shell como root

find . -exec /bin/sh \; -quit


Finalmente, realizamos un cat thefinalflag.txt
![image](https://github.com/user-attachments/assets/b47a0750-880a-4637-b8e8-6bbce24a4b30)





















