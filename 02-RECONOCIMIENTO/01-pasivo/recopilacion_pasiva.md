# Recopilación Pasiva de Información y OSINT

La recopilación pasiva de información y la Inteligencia de Fuentes Abiertas (OSINT) están estrechamente relacionadas, siendo el OSINT un marco más amplio que integra la recopilación pasiva como uno de sus componentes fundamentales. La recopilación pasiva se enfoca en obtener datos sobre un objetivo sin interactuar directamente con él, utilizando fuentes públicamente disponibles.

## Características de la Recopilación Pasiva

- No genera tráfico hacia el objetivo
- Utiliza información públicamente disponible
- Menor riesgo de detección
- Puede proporcionar información limitada o desactualizada

## Herramientas y Técnicas

### Motores de Búsqueda Especializados

- [Shodan](https://www.shodan.io/): Motor de búsqueda que indexa dispositivos conectados a Internet, proporcionando información sobre servicios, sistemas operativos, puertos abiertos, vulnerabilidades y tipos específicos de dispositivos como servidores, equipos de red y sistemas IoT.
- [Censys Search](https://search.censys.io/): Motor de búsqueda especializado en identificar hosts, sitios web, certificados y activos conectados públicamente a Internet, permitiendo auditar puertos, servicios y descubrir activos no autorizados en una red.
- [IntelligenceX](https://intelx.io/tools): Plataforma de investigación e inteligencia de datos que recopila y analiza información de la web abierta, la web oscura (dark web) y otras bases de datos.

### Análisis de Dominio y DNS

- [Whois](https://who.is/): Herramienta para obtener información sobre la propiedad de un dominio, como la organización, los contactos administrativos, los servidores de nombres, etc.
- [DNSdumpster](https://dnsdumpster.com/): Herramienta que permite obtener información detallada sobre la infraestructura DNS de un dominio.

### Búsqueda Avanzada

- Google Dorks (Google Hacking): Utiliza búsquedas avanzadas en Google para localizar información sensible o expuesta en sitios web.
   * [Google Hacking DataBase](https://www.exploit-db.com/google-hacking-database)

### Herramientas OSINT Integrales

- [theHarvester](https://github.com/laramies/theHarvester): Herramienta para recopilar información de fuentes públicas, como direcciones de correo electrónico, subdominios, hosts, servidores DNS, entre otros.
- [Maltego](https://www.maltego.com/): Herramienta de inteligencia que permite realizar análisis visual de redes y relaciones entre personas, grupos, sitios web, infraestructura, etc.
- [Recon-ng](https://github.com/lanmaster53/recon-ng): Framework para realizar recopilación de inteligencia y análisis de información a partir de fuentes abiertas (OSINT).
- [OSINT Framework](http://osintframework.com): Reune herramientas y recursos gratuitos para facilitar la búsqueda de información OSINT.
- [Intel Techniques](https://inteltechniques.com/tools/): Conjunto de herramientas y recursos para la investigación de OSINT, que ofrece una variedad de utilidades para búsquedas en redes sociales, análisis de correo electrónico, y más.

### Servicios Especializados

- [Have I Been Pwned](https://haveibeenpwned.com/): Servicio que permite verificar si una cuenta de correo electrónico ha sido comprometida en una brecha de datos.
- [TinEye](https://tineye.com/): Motor de búsqueda inversa de imágenes que permite rastrear el origen y uso de una imagen en internet.
- [Wayback Machine](https://archive.org/web/): Servicio que permite ver versiones archivadas de páginas web a través del tiempo.
- [WebCheck](https://web-check.xyz/): Herramienta para verificar la disponibilidad y la integridad de sitios web, proporcionando información sobre el estado del servidor, certificados SSL, y otros detalles técnicos.

## Recopilación Semi-Pasiva

La recopilación semi-pasiva genera tráfico o interacción con el objetivo, pero de manera que simula el comportamiento de un usuario legítimo.

### Herramientas

#### Análisis de Red
- [Wireshark](https://www.wireshark.org/): Analizador de protocolos de red que permite capturar y examinar detalladamente el tráfico de red en tiempo real.
- [TCPdump](https://www.tcpdump.org/): Herramienta de línea de comandos para analizar el tráfico de red, capturando y mostrando paquetes transmitidos o recibidos en una interfaz de red.

#### Escaneo y Enumeración
- [F.O.C.A](https://github.com/ElevenPaths/FOCA): Herramienta para encontrar metadatos y información oculta en documentos.
- [CentralOps](https://centralops.net/): Conjunto de herramientas en línea para realizar investigaciones de red y dominio.

## Herramientas Adicionales para OSINT

### Análisis de Sitios Web y Tecnología

- [WhatWeb](https://github.com/urbanadventurer/WhatWeb): Herramienta para identificar tecnologías utilizadas por un sitio web, como servidores web, CMS, frameworks, y más.
- [Wappalyzer](https://www.wappalyzer.com/): Extensión y herramienta que detecta tecnologías web, incluidos CMS, servidores web, herramientas de análisis y más.

### Análisis de Imágenes

- [WebCheck](https://web-check.xyz/): Herramienta para verificar la disponibilidad y la integridad de sitios web, proporcionando información sobre el estado del servidor, certificados SSL, y otros detalles técnicos.
- [TinEye](https://tineye.com/): Motor de búsqueda inversa de imágenes que permite rastrear el origen y uso de una imagen en internet.

### Análisis de Metadatos

- [Exiftool / exifprobe / exiv2](https://www.sno.phy.queensu.ca/~phil/exiftool/): Herramientas para extraer metadatos de archivos de imagen, audio y video, lo que permite identificar información como la ubicación, el dispositivo utilizado y más.
  
### Otros

- [Snov Plugin](https://snov.io/): Herramienta utilizada para la recopilación de correos electrónicos y la búsqueda de datos públicos en Internet.
- [Ghost Recon](https://www.ghostrecon.com/): Herramienta para realizar un rastreo de amenazas y obtener información sobre vulnerabilidades.
- [Mr. Holmes](https://mrholmes.co/): Plataforma de OSINT que permite la recopilación y análisis de datos de fuentes abiertas.
- [The Spy Jobs](https://www.thespyjobs.com/): Herramienta para obtener información relacionada con ciberseguridad, delitos cibernéticos y fuentes abiertas.
- [Infoooze](http://www.infoooze.com/): Herramienta utilizada para realizar búsquedas en múltiples fuentes abiertas.
  
## Consideraciones Finales

La combinación de técnicas pasivas y semi-pasivas es esencial para obtener una visión completa y precisa del objetivo. Estas técnicas permiten recopilar información valiosa de manera discreta, minimizando el riesgo de detección. Aunque la información obtenida puede ser limitada en comparación con métodos más activos, la recopilación pasiva ofrece una base sólida para el análisis de OSINT, permitiendo construir una imagen inicial del objetivo de manera legal y ética.

