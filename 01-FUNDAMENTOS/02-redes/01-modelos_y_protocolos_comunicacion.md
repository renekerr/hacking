# Fundamentos de Redes: Modelo OSI, TCP/IP

## 1. Modelo OSI (Open Systems Interconnection)

### 1.1. Introducción al Modelo OSI

-   **Definición:** El modelo OSI es un marco conceptual que describe cómo las redes de computadoras se comunican. Proporciona una estructura en capas que facilita la comprensión y el diseño de sistemas de red. Permite la comunicación entre equipos con diseños y funciones diversas.
-   **Beneficio Clave:**  Garantiza que los datos transmitidos siguiendo el modelo sean comprensibles por todos los dispositivos en la red, promoviendo la interoperabilidad.
-   **Estructura:** Se compone de siete capas, cada una con responsabilidades específicas en el proceso de comunicación. Los datos se encapsulan al pasar por estas capas.

### 1.2. Características Principales del Modelo OSI

-   **Modularidad:** Cada capa tiene funciones específicas y se comunica únicamente con las capas adyacentes, facilitando el desarrollo y el mantenimiento.
-   **Encapsulación:** Los datos se envuelven con información adicional (encabezados) al pasar por cada capa, asegurando la correcta entrega.
-   **Interoperabilidad:** Permite la comunicación entre diferentes sistemas y redes, independientemente de sus arquitecturas internas.

### 1.3. Importancia del Modelo OSI

El modelo OSI es crucial porque:

-   **Comprensión:** Facilita la comprensión del funcionamiento interno de las redes.
-   **Solución de Problemas:** Simplifica la resolución de problemas al dividir las funciones en capas manejables.
-   **Estándar:** Proporciona un estándar para el desarrollo e implementación de protocolos y tecnologías de red.

### 1.4. Capas del Modelo OSI

| **Capa** | **Nombre**                 | **Descripción**                                                                         | **Dispositivos/Elementos**                                      |
| -------- | -------------------------- | --------------------------------------------------------------------------------------- | ---------------------------------------------------------------- |
| 7        | Aplicación (Application)   | Proporciona servicios de red directamente a los usuarios.                               | Navegadores web, clientes de correo electrónico, aplicaciones FTP |
| 6        | Presentación (Presentation) | Se encarga de la representación de los datos (cifrado, compresión).                      | Codificadores, decodificadores, encriptadores, compresores      |
| 5        | Sesión (Session)            | Controla el establecimiento, mantenimiento y finalización de sesiones.                   | NetBIOS, RPC (Remote Procedure Call)                              |
| 4        | Transporte (Transport)      | Garantiza la transferencia confiable de los datos.                                      | Firewalls de capa 4, balanceadores de carga                      |
| 3        | Red (Network)               | Determina cómo se enrutan los datos (direcciones IP).                                  | Routers, switches de capa 3                                      |
| 2        | Enlace de Datos (Data Link) | Gestiona la transmisión de datos en un enlace físico (direcciones MAC).                  | Switches, bridges, tarjetas de red (NIC)                          |
| 1        | Física (Physical)           | Transmite los datos a través del medio físico (cables, señales).                        | Cables, conectores, hubs, repetidores                             |

### 1.5. Conclusión

El Modelo OSI es un marco conceptual fundamental para comprender la comunicación en redes modernas. Su enfoque modular facilita el diseño, mantenimiento y resolución de problemas en sistemas complejos, asegurando una comunicación eficiente y estandarizada entre dispositivos diversos.

## 2. Modelo TCP/IP (Transmission Control Protocol/Internet Protocol)

### 2.1. Descripción

El modelo TCP/IP es un conjunto de protocolos que permite la comunicación en redes como Internet. Está compuesto por 4 capas, más simples que las del modelo OSI, pero igualmente esenciales para la comunicación en red.

### 2.2. Capas del Modelo TCP/IP

| **Capa** | **Nombre**                         | **Descripción**                                                               |
| -------- | ---------------------------------- | ----------------------------------------------------------------------------- |
| Capa 4   | Aplicación (Application)           | Protocolo que permite la comunicación entre aplicaciones (HTTP, FTP, etc.).     |
| Capa 3   | Transporte (Transport)             | Controla la transmisión de datos entre sistemas (TCP, UDP).                   |
| Capa 2   | Internet (Internet)                | Enrutamiento de paquetes a través de redes (IP).                             |
| Capa 1   | Interfaz de Red (Network Interface) | Controla el acceso al medio físico, como Ethernet (direcciones MAC).           |

## 3. Protocolos de la Capa de Transporte

### 3.1. Protocolo TCP (Transmission Control Protocol)

-   **Descripción:** Es un protocolo orientado a la conexión, diseñado para asegurar la entrega confiable y ordenada de datos.
-   **Características:**
    -   **Conexión Orientada:** Establece una conexión antes de transmitir datos.
    -   **Fiabilidad:** Utiliza checksum, secuenciación y retransmisión para garantizar la entrega correcta de los datos.
-   **Three-Way Handshake:** Proceso utilizado por TCP para establecer una conexión confiable:
    | **Paso** | **Mensaje** | **Descripción**                                                                                             |
    | -------- | ----------- | ----------------------------------------------------------------------------------------------------------- |
    | 1        | **SYN**     | El cliente envía su Número de Secuencia Inicial (ISN) para sincronizar la conexión (ejemplo: ISN = 0).      |
    | 2        | **SYN/ACK** | El servidor responde con su propio ISN (ejemplo: ISN = 5000) y confirma el ISN del cliente (0).             |
    | 3        | **ACK**     | El cliente confirma el ISN del servidor (5000) y comienza a enviar datos, iniciando con ISN+1 (0 + 1 = 1). |

-   **Secuenciación de Datos:** Los datos se envían con números de secuencia incrementales, asegurando que se reciban correctamente y en el orden adecuado:

    | **Cliente (Emisor)** | **Número de Secuencia Inicial (ISN)** | **Primer Paquete** | **Segundo Paquete** | **Tercer Paquete** |
    | -------------------- | ------------------------------------ | ------------------ | ------------------- | ------------------ |
    | Cliente              | 0                                    | 1                 | 2                 | 3                |

-   **Ventajas:**
    -   Alta fiabilidad, garantiza el orden y la integridad de los datos.
    -   Utilizado en aplicaciones críticas como navegación web (HTTP) y correo electrónico.
-   **Desventajas:**
    -   Más lento que UDP debido a la sobrecarga de verificación de datos.
    -   Requiere más recursos del sistema debido al control de flujo y congestión.

### 3.2. Encabezado de Paquetes TCP

Los paquetes TCP incluyen varios encabezados que se añaden durante el proceso de encapsulación, incluyendo:

| **Encabezado**           | **Descripción**                                                                                                                                                                 |
| ------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Source Port**          | Puerto abierto por el remitente para enviar el paquete (0-65535).                                                                                                               |
| **Destination Port**     | Número de puerto donde se ejecuta la aplicación o servicio en el host remoto.                                                                                                   |
| **Source IP**            | Dirección IP del dispositivo que envía el paquete.                                                                                                                              |
| **Destination IP**       | Dirección IP del dispositivo de destino.                                                                                                                                        |
| **Sequence Number**      | Número asignado aleatoriamente al primer fragmento de datos transmitido al inicio de una conexión.                                                                             |
| **Acknowledgement Number** | Número que indica el siguiente número de secuencia esperado, confirmando la recepción de datos anteriores.                                                                    |
| **Checksum**             | Valor para la integridad de TCP. Detecta datos corruptos comparando el cálculo del emisor y receptor.                                                                          |
| **Data**                 | Información que se está transmitiendo.                                                                                                                                            |
| **Flag**                  | Encabezado que determina cómo se debe manejar el paquete durante el handshake, definiendo comportamientos específicos. |

### 3.3. Protocolo UDP (User Datagram Protocol)

-   **Descripción:** Es un protocolo más sencillo y rápido que TCP, pero no garantiza la entrega ni la integridad de los datos.
-   **Características:**
    -   **Sin Conexión:** No establece una conexión antes de enviar los datos.
    -   **Stateless:** No mantiene información sobre el estado de la conexión.
-   **Ventajas:**
    -   Mucho más rápido que TCP, ideal para aplicaciones como video streaming, juegos en línea y VoIP.
    -   Menos overhead, eficiente en términos de recursos.
-   **Desventajas:**
    -   No garantiza la entrega de los datos ni su orden.
    -   No tiene mecanismos de control de flujo ni retransmisión en caso de error.

## 4. Otros Protocolos y Conceptos Clave

### 4.1. Protocolo ARP (Address Resolution Protocol)

-   **Descripción:** Utilizado para mapear una dirección IP a una dirección MAC en una red local.
-   **Funcionamiento:**
    -   **ARP Request:** Un dispositivo solicita la dirección MAC asociada a una dirección IP.
    -   **ARP Reply:** El dispositivo correspondiente responde con su dirección MAC.

### 4.2. Paquetes y Tramas

-   **Definiciones:**
    -   **Trama (Frame):** Un paquete encapsulado en la capa de enlace de datos para la transmisión física a través de la red, no incluye direcciones IP.
    -   **Paquete (Packet):** Una unidad de datos transmitida en la capa de red, que incluye direcciones IP de origen y destino.
-   **Encapsulación:** Proceso por el cual los datos se envuelven con información adicional al pasar a través de las capas del modelo OSI o TCP/IP.

### 4.3. Puertos

-   **Definición:** Valores numéricos que identifican aplicaciones o servicios dentro de un dispositivo (rango de 0 a 65535).
    -   **Puertos bien conocidos:** (0-1024) - Usados por protocolos comunes (HTTP, FTP, etc.)
    -   **Puertos registrados:** (1025-49151)
    -   **Puertos dinámicos:** (49152-65535)

| **Protocolo** | **Puerto** | **Descripción**                               |
| ------------- | ---------- | --------------------------------------------- |
| **FTP**       | 21         | Transferencia de archivos (cliente-servidor)   |
| **SSH**       | 22         | Acceso remoto seguro                          |
| **HTTP**      | 80         | Navegación web                                |
| **HTTPS**     | 443        | Versión segura de HTTP                        |
| **SMB**       | 445        | Compartición de archivos y dispositivos         |
| **RDP**       | 3389       | Acceso remoto a escritorio                    |

### 4.4. Topologías de Redes LAN

-   **Descripción:** Definición de la disposición física y lógica de los dispositivos en una red.

    1.  **Topología Estrella (Star):**
        -   **Descripción:** Todos los dispositivos se conectan a un dispositivo central (switch, router).
        -   **Ventajas:** Alta confiabilidad, fácil de gestionar y escalar.
        -   **Desventajas:** Dependencia de un único punto de fallo (dispositivo central).
    2.  **Topología Bus (Bus):**
        -   **Descripción:** Todos los dispositivos están conectados a un único cable central.
        -   **Ventajas:** Económica y fácil de instalar.
        -   **Desventajas:** Sujeta a congestión y problemas si el cable central se daña.
    3.  **Topología Anillo (Ring):**
        -   **Descripción:** Los dispositivos se conectan en un anillo cerrado, transmitiendo datos en una sola dirección.
        -   **Ventajas:** Menos congestión y fácil de identificar fallos.
        -   **Desventajas:** Un fallo en un dispositivo interrumpe toda la red.

### 4.5. Subnetting (Subredes)

-   **Descripción:** Proceso de dividir una red en subredes más pequeñas para mejorar la administración y seguridad.
-   **Propósitos:**
    -   **Network Address:** Identifica la subred.
    -   **Host Address:** Asigna una IP única a cada dispositivo en la subred.
    -   **Default Gateway:** Permite la comunicación entre diferentes subredes o hacia internet.

### 4.6. Estructura de un Paquete IP

| **Campo**             | **Descripción**                                |
| --------------------- | ---------------------------------------------- |
| **TTL (Time to Live)** | Previene que los paquetes circulen indefinidamente |
| **Checksum**          | Verifica la integridad de los datos.          |
| **Source Address**    | Dirección IP de origen.                        |
| **Destination Address** | Dirección IP de destino.                       |

### 4.7. Proceso de Three-Way Handshake (Reiteración)

-   **Descripción:** Proceso que utiliza TCP para establecer una conexión.

| **Paso** | **Mensaje** | **Descripción**                                |
| -------- | ----------- | ---------------------------------------------- |
| 1        | **SYN**     | El cliente inicia la sincronización.           |
| 2        | **SYN/ACK** | El servidor responde.                         |
| 3        | **ACK**     | El cliente o servidor confirma la conexión.   |
| 4        | **DATA**    | Inicia la transmisión de datos.               |
| 5        | **FIN**     | Cierre de la conexión.                        |
| 6        | **RST**     | Terminación abrupta de la conexión si hay un error.|

### 4.8. Asignación de Direcciones IP

-   **Descripción:** Proceso mediante el cual un dispositivo obtiene una dirección IP.
    -   **Manual:** Asignación estática al dispositivo.
    -   **Automática:** A través de un servidor DHCP (Dynamic Host Configuration Protocol).
-   **Proceso de DHCP:**
    1.  **DHCP Discover:** El dispositivo busca servidores DHCP.
    2.  **DHCP Offer:** El servidor ofrece una dirección IP disponible.
    3.  **DHCP Request:** El dispositivo confirma que acepta la dirección.
    4.  **DHCP ACK:** El servidor confirma la asignación.

## 5. Conceptos de Redes

### 5.1. Port Forwarding

-   **Descripción:** Esencial para conectar aplicaciones y servicios a Internet desde una red local. Se configura en el router.

### 5.2. Firewalls

-   **Descripción:** Dispositivo que determina qué tráfico puede entrar y salir de una red, inspeccionando paquetes según origen, destino, puerto y protocolo.

    | **Tipo**     | **Características**                                                                                                 |
    | ------------ | ------------------------------------------------------------------------------------------------------------------ |
    | **Stateful** | Usa información completa de la conexión, decisiones dinámicas, mayor consumo de recursos, bloquea dispositivos completos si la conexión es mala.   |
    | **Stateless**| Usa reglas estáticas para paquetes, menor consumo de recursos, menos inteligente, útil contra ataques DDoS. |

### 5.3. VPN (Virtual Private Network)

-   **Descripción:** Permite que dispositivos en redes separadas se comuniquen de forma segura a través de un túnel en Internet.
-   **Beneficios:**
    | **Beneficio**  | **Descripción**                                     |
    | ------------- | --------------------------------------------------- |
    | Conectividad  | Conecta redes en diferentes ubicaciones geográficas |
    | Privacidad    | Encripta datos para proteger contra sniffing       |
    | Anonimato     | Oculta el tráfico de ISPs y otros intermediarios    |
-   **Tecnologías VPN:**
    | **Tecnología** | **Características**                                                                  |
    | ------------- | ----------------------------------------------------------------------------------- |
    | **PPP**        | Permite autenticación y encriptación, no enrutable por sí mismo.                         |
    | **PPTP**       | Permite que PPP salga de una red, fácil configuración, encriptación débil.              |
    | **IPSec**      | Encripta usando el framework IP, configuración compleja, alta seguridad.                |

### 5.4. Routers

-   **Descripción:** Conectan redes y transmiten datos entre ellas mediante routing. Operan en la Capa 3 del modelo OSI y pueden configurarse para port forwarding y firewalling.

### 5.5. Switches

-   **Descripción:** Dispositivos dedicados para conectar múltiples dispositivos en una red.
    | **Tipo de Switch** | **Funcionalidad**                                |
    | ----------------- | ----------------------------------------------- |
    | **Layer 2**        | Reenvía frames usando direcciones MAC.            |
    | **Layer 3**        | Reenvía frames y enruta paquetes usando direcciones IP.  |

### 5.6. VLAN (Virtual Local Area Network)

-   **Descripción:** Divide virtualmente dispositivos dentro de una red, proporcionando seguridad al determinar cómo los dispositivos específicos se comunican entre sí.

## 6. Conclusión

El modelo OSI y los protocolos TCP/IP son fundamentales para la comunicación en redes. TCP proporciona una comunicación confiable y ordenada, mientras que UDP es más eficiente en velocidad, pero carece de garantías de entrega. Además, conceptos como ARP, subnetting, y la correcta gestión de puertos y topologías de red son esenciales para el diseño, mantenimiento y seguridad de las redes. La correcta implementación y entendimiento de estos modelos y protocolos permite optimizar el tráfico de red y asegurar una comunicación eficiente.
