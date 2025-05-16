
# DC-1 Vulhub | Write-Up

---

## **DC-1 Vulhub**

[**Enlace al desafío en Vulnhub**](https://www.vulnhub.com/entry/dc-1,292/)

### **Descripción**

DC-1 es un laboratorio vulnerable diseñado específicamente para que principiantes adquieran experiencia en pruebas de penetración. Su nivel de dificultad dependerá de las habilidades, conocimientos y capacidad de aprendizaje del usuario.

#### **Requisitos para completarlo**

- Conocimientos básicos de Linux.
- Familiaridad con la línea de comandos de Linux.
- Experiencia con herramientas básicas de pruebas de penetración, como las disponibles en Kali Linux o Parrot Security OS.

#### **Objetivo principal**

El objetivo es encontrar y leer la bandera ubicada en el directorio de inicio de **root**. Aunque no es necesario iniciar sesión como root para acceder a la bandera, sí se requieren privilegios de root para ello.

#### **Detalles adicionales**

- **Número de banderas:** 5  
  Estas banderas contienen pistas útiles para principiantes.
- **Opcional:** Los usuarios más avanzados pueden optar por saltarse las banderas intermedias e ir directamente por root.

---

## **Importación y configuración en VirtualBox**

1. Descargamos la máquina desde el enlace anterior y la importamos en VirtualBox.
2. Creamos una red NAT:
   - **Archivo > Herramientas > Administrador de red > Redes NAT > + Crear**
   
![Red NAT](https://github.com/user-attachments/assets/fe4b3f3b-b818-4b2e-ac77-cfc508431d23)

3. Asignamos la red NAT a las interfaces de red de **Kali Linux** y **DC-1**:

![Red Kali](https://github.com/user-attachments/assets/f797b7a9-8bf9-45b9-8fd6-15f7d8d473cf)
![Red DC1](https://github.com/user-attachments/assets/2a17293e-8a4d-47d2-b7c2-fe206dc8f7be)

## **Descubrimiento de IP**

Usamos **Netdiscover** para identificar la IP de la máquina DC-1:

```bash
ifconfig      # para identificar la interfaz conectada
netdiscover   # para descubrir la IP de DC-1
```

![Netdiscover](https://github.com/user-attachments/assets/d4216175-c2d5-4b7e-b89d-759be256a5cd)

![Interfaz](https://github.com/user-attachments/assets/9b5164fd-fa1b-4199-be3b-f37e07b7f67f)

![IP Descubierta](https://github.com/user-attachments/assets/5445bfb9-fea9-47a4-9354-292de0fa9a34)

Verificamos conectividad:

![Ping](https://github.com/user-attachments/assets/d5bcc1cb-3439-4e31-9bad-c72e4db1cff3)

## **Escaneo con Nmap y enumeración**

Escaneamos la máquina con `nmap`:

![Nmap](https://github.com/user-attachments/assets/34146c67-11b3-4512-8536-b76f5f671931)

Confirmamos que el CMS es Drupal:

![WhatWeb](https://github.com/user-attachments/assets/b9c0fc4c-e269-40f1-9b6a-651217142999)
![Sitio Drupal](https://github.com/user-attachments/assets/d6a7ac26-e1ca-4320-b0a7-9524d1dee144)

Buscamos la vulnerabilidad **CVE-2018-7600 (Drupalgeddon2)**.

## **Explotación con Metasploit**

Ejecutamos el módulo correspondiente:

![Exploit Metasploit](https://github.com/user-attachments/assets/e0db3fbc-1aed-4135-8677-eeda74990504)
![Configuración Exploit](https://github.com/user-attachments/assets/b6808ecc-5e97-486f-b168-2ba1c390eca7)

Obtenemos shell y vemos:

![Flag1](https://github.com/user-attachments/assets/51394ced-c002-42d2-a14b-9c7b631998d5)

### **Flag1**

```
Todo buen CMS necesita un archivo de configuración, lo mismo que tú.
```

Buscamos `settings.php`:

![Settings.php](https://github.com/user-attachments/assets/ebce0eb4-cecf-448c-adfa-2d7f1b30ba55)

### **Flag2**

```
Los ataques de fuerza bruta y de diccionario no son las únicas formas de obtener acceso (y lo necesitarás). ¿Qué puedes hacer con estas credenciales?
```

![Flag2 y base de datos](https://github.com/user-attachments/assets/9f28438c-5000-493a-b463-ec0ba295aec2)

Elevamos la sesión a shell:

![PTY Bash](https://github.com/user-attachments/assets/25cdfe8a-c8fd-4b6f-a8e0-e051f456ab12)

Accedemos a la base de datos:

![MySQL](https://github.com/user-attachments/assets/f6d1baa5-ce6e-413f-837b-d91f16b4941c)
![Credenciales](https://github.com/user-attachments/assets/bc1c9f0e-5a14-4977-9ed3-eeb8fa02695b)

Creamos un nuevo usuario admin en Drupal:

![Exploit admin](https://github.com/user-attachments/assets/46a1aab8-1b36-41e4-88af-39106ef628e2)
![Comando Exploit](https://github.com/user-attachments/assets/94d5bedb-3317-4293-950d-1ca94a56b37b)
![Acceso CMS](https://github.com/user-attachments/assets/7376d17d-d4ed-44e2-99c1-c414b84ae73d)

Entramos a 'Content' y obtenemos:

![Content Drupal](https://github.com/user-attachments/assets/d8764dba-030d-4ba4-af85-f1d9c2b2ebb1)
![Flag3](https://github.com/user-attachments/assets/d601f63b-04b3-4213-b57c-3cf23069627d)

### **Flag3**

```
Permisos especiales ayudarán a encontrar la passwd, pero necesitarás usar -exec para averiguar cómo obtener lo que está en la sombra.
```

Encontramos usuario `flag4`:

![Flag4.txt](https://github.com/user-attachments/assets/93fff86b-1d07-4541-add7-fdee7623cde6)

### **Flag4**

```
¿Puedes usar este mismo método para encontrar o acceder a la bandera en root?
Probablemente. Pero tal vez no sea tan fácil. ¿O quizás sí lo sea?
```

## **Post-explotación y escalada de privilegios**

Buscamos binarios SUID:

```bash
find / -perm -u=s 2>/dev/null
```

![Binarios SUID](https://github.com/user-attachments/assets/7f591442-2205-4492-b25d-4e7e50787990)

Usamos GTFOBins:

```bash
find . -exec /bin/sh \; -quit
```

Obtenemos shell como root. Finalmente:

![Final Flag](https://github.com/user-attachments/assets/b47a0750-880a-4637-b8e8-6bbce24a4b30)

```bash
cat /root/thefinalflag.txt
```

---

