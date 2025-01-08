### **Topologías de Redes de Área Local (LAN Topologies)**  
#### **Topologías y sus características**  

**Star (Estrella)**  
- **Descripción:** Dispositivos conectados a un dispositivo central (switch/hub).  
- **Ventajas:** Confiable, escalable, fácil de expandir.  
- **Desventajas:** Costosa, dependiente del dispositivo central.  

**Bus (Bus)**  
- **Descripción:** Dispositivos conectados a un cable principal (backbone).  
- **Ventajas:** Económica, fácil instalación.  
- **Desventajas:** Cuellos de botella, difícil de reparar, sin redundancia.  

**Ring (Anillo)**  
- **Descripción:** Dispositivos conectados en forma de bucle.  
- **Ventajas:** Menos congestión, fácil de diagnosticar fallos.  
- **Desventajas:** Ineficiente, falla total si un dispositivo o cable se rompe.  

---

### **Routers y Switches en Redes**  

#### **Router (Enrutador)**  
- **Descripción:** Conecta redes y dirige datos entre ellas (enrutamiento).  
- **Características:** Establece rutas, asegura entrega de datos, ofrece múltiples caminos redundantes.  

#### **Switch (Conmutador)**  
- **Descripción:** Conecta múltiples dispositivos en una red mediante puertos Ethernet.  
- **Características:** Eficiente, evita tráfico innecesario, admite conexiones redundantes con routers y otros switches.  

---

### **Subnetting (Subredes)**  

#### **Descripción**  
Subnetting es el proceso de dividir una red en redes más pequeñas (subredes), similar a repartir una torta en porciones. Esto permite asignar recursos específicos a diferentes secciones de una red según las necesidades.

#### **Propósitos de una Subred**  
Las subredes utilizan direcciones IP para:  
1. **Identificar la dirección de la red (Network Address):** Representa el inicio de la red. Ejemplo: `192.168.1.0`.  
2. **Identificar direcciones de host (Host Address):** Asignan una IP a cada dispositivo en la subred. Ejemplo: `192.168.1.100`.  
3. **Definir la puerta de enlace predeterminada (Default Gateway):** Dispositivo que envía datos a otras redes. Ejemplo: `192.168.1.254`.  

---

### **Protocolo de Resolución de Direcciones (ARP)**  

#### **Descripción**  
El Protocolo de Resolución de Direcciones (ARP) es responsable de asociar una dirección MAC con una dirección IP en una red. Esto permite a los dispositivos identificar y comunicarse entre sí utilizando estos identificadores únicos.

#### **Funcionamiento de ARP**  
Cada dispositivo en la red mantiene un **cache** (registro) que guarda los identificadores de otros dispositivos. Para mapear las direcciones IP y MAC, ARP envía dos tipos de mensajes:

1. **ARP Request (Solicitud ARP):** El dispositivo emite una solicitud de difusión en la red preguntando, "¿Cuál es la dirección MAC de esta IP?"  
2. **ARP Reply (Respuesta ARP):** Los dispositivos que poseen la dirección IP solicitada responden con su dirección MAC.

El dispositivo solicitante guarda esta información en su cache ARP para futuras comunicaciones.

---

### **Asignación de Direcciones IP (IP Address Allocation)**  

#### **Métodos de Asignación**  
1. **Manual:** Introduciendo la dirección directamente en el dispositivo.  
2. **Automática:** Utilizando un servidor DHCP (Dynamic Host Configuration Protocol), el método más común.  

#### **Proceso de DHCP**  
1. **DHCP Discover:** El dispositivo envía una solicitud para encontrar servidores DHCP.  
2. **DHCP Offer:** El servidor DHCP responde con una IP disponible.  
3. **DHCP Request:** El dispositivo confirma que acepta la dirección ofrecida.  
4. **DHCP ACK:** El servidor confirma que la dirección está asignada, permitiendo su uso.  

---
