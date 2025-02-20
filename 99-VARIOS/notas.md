# Documentación Técnica Organizada

## Scripting Bash y Automatización

### Script de Autenticación
```bash
#!/bin/bash

# Defining the variables
username=""
companyname=""
pin=""

# Defining the loop
for i in {1..3}; do
    # Defining the conditional statements
    if [ "$i" -eq 1 ]; then
        echo "Enter your Username:"
        read username
    elif [ "$i" -eq 2 ]; then
        echo "Enter your Company name:"
        read companyname
    else
        echo "Enter your PIN:"
        read pin
    fi
done

# Checking if the user entered the correct details
if [ "$username" = "John" ] && [ "$companyname" = "Tryhackme" ] && [ "$pin" = "7385" ]; then
    echo "Authentication Successful. You can now access your locker, John."
else
    echo "Authentication Denied!!"
fi
```

### Script de Búsqueda de Flags
```bash
#!/bin/bash

# Defining the directory to search our flag
directory="/var/log"

# Defining the flag to search
flag="thm-flag01-script"

echo "Flag search in directory: $directory in progress..."

# Defining for loop to iterate over all the files with .log extension in the defined directory
for file in "$directory"/*.log; do
    # Check if the file contains the flag
    if grep -q "$flag" "$file"; then
        # Print the filename and the full path for clarity
        echo "Flag found in: $file"
    fi
done
```

## Herramientas de Pentesting y Hacking

### Enumeración Web
```bash
# Obtener favicon y calcular su hash MD5
curl https://static-labs.tryhackme.cloud/sites/favicon/images/favicon.ico | md5sum

# Petición HTTP con información detallada
curl http://10.10.245.129/ -v

# Herramientas de Fuzzing y Enumeración de Directorios
ffuf -w /usr/share/wordlists/seclists/Discovery/Web-Content/common.txt -u http://10.10.245.129/FUZZ
dirb http://10.10.245.129/ /usr/share/wordlists/seclists/Discovery/Web-Content/common.txt
gobuster dir --url http://10.10.245.129/ -w /usr/share/wordlists/seclists/Discovery/Web-Content/common.txt
```

### Crackeo de Contraseñas
```bash
# Información hash encontrada
# [+] Salt for password found: 1dac0d92e9fa6bb2
# [+] Username found: mitch
# [+] Email found: admin@admin.com
# [+] Password found: 0c01f4468bd75d7a84c7eb73846e8d96

# Crackeo de hash usando hashcat
hashcat -O -a 0 -m 20 0c01f4468bd75d7a84c7eb73846e8d96:1dac0d92e9fa6bb2 /usr/share/wordlists/rockyou.txt
# Resultado: 0c01f4468bd75d7a84c7eb73846e8d96:1dac0d92e9fa6bb2:secret
```

## Operaciones con Hashes y Codificación

### Cálculo de Hashes
```bash
# Cálculo de hash MD5 (sin salto de línea)
echo -n "LearnTheHashFunction" | md5sum
# -n impide que se agregue un salto de línea final

# Cálculo de hash SHA256
echo -n "ThisIsAMoreSecureHashFunction" | sha256sum
# d191ce0a9d8061acb609be613d0a6dccd13d93946fa3e8aa3c0c40a2102502ff  -

# Encadenamiento de hashes (SHA256 seguido de MD5)
echo -n "d191ce0a9d8061acb609be613d0a6dccd13d93946fa3e8aa3c0c40a2102502ff" | md5sum
# dd321a22229e0bbb5f8271e370b61eb0  -

# Versión usando awk para eliminar el formato de sha256sum
echo -n "ThisIsAMoreSecureHashFunction" | sha256sum | awk '{printf $1}' | md5sum
# dd321a22229e0bbb5f8271e370b61eb0  -

# Uso de caracteres especiales en echo
echo -n 'TheASCIITable!' | md5sum
echo -n "TheASCIITable\!" | md5sum
```

### Codificación Base64
```bash
# Decodificar archivo base64
base64 -d base64-c6d8efd649ad94af23eb2bd2af63edd0.txt 

# Nota importante: Base64 no es cifrado, solo codificación
# La contraseña para superar este reto es: recuerdaquebase64NOescifrar

echo -n "recuerdaquebase64NOescifrar" | md5sum
# cf9df460535b4ec175a464c6c120d3fe  -
```

## Protocolos de Red y Modelos de Comunicación

### Modelo TCP/IP
- **Capas:**
  - **Aplicación:** Combina aplicación, presentación y sesión de OSI (HTTP, HTTPS, FTP)
  - **Transporte:** Gestiona transferencia de datos (TCP, UDP)
  - **Internet:** Direccionamiento y enrutamiento (IP, ICMP, IPSec)
  - **Enlace:** Acceso físico a la red (Ethernet, WiFi)
  - **Física** (en variantes comunes)

### Direccionamiento IP (IPv4)
- Formato: Cuatro octetos (32 bits) en decimal separados por puntos (ej. 192.168.0.1)
- Direcciones reservadas: 0 (red) y 255 (difusión)
- Aproximadamente 4 mil millones de direcciones únicas
- Verificación de configuración: `ipconfig` (Windows), `ifconfig`/`ip a s` (Linux/Unix)
- **Tipos de direcciones:**
  - **Privadas:** (RFC 1918)
    - 10.0.0.0 - 10.255.255.255 (10/8)
    - 172.16.0.0 - 172.31.255.255 (172.16/12)
    - 192.168.0.0 - 192.168.255.255 (192.168/16)
  - **Públicas:** Accesibles desde internet

### Protocolos de Transporte

| Característica | UDP | TCP |
|----------------|-----|-----|
| **Tipo** | Sin conexión | Orientado a conexión |
| **Fiabilidad** | No garantiza entrega | Entrega confiable |
| **Velocidad** | Más rápido | Más lento (con verificación) |
| **Mecanismos** | Números de puerto | Números de secuencia, ACKs |
| **Establecimiento** | No requiere | Handshake de 3 vías (SYN, SYN-ACK, ACK) |
| **Puertos** | 1-65535 (0 reservado) | 1-65535 (0 reservado) |

### Ciclo de Vida del Paquete
- **Capa de Aplicación:** Prepara datos (ej. solicitud HTTP)
- **Transporte:** Agrega encabezado (TCP/UDP) → Segmento
- **Internet:** Agrega IP origen/destino → Paquete
- **Enlace:** Agrega encabezado/tráiler → Trama
- **Transmisión física**
- **Proceso inverso** en el receptor

## Protocolos y Servicios de Red

### Telnet
- Protocolo para conexión de terminal remota (no seguro)
- Útil para probar servicios que escuchan en puertos TCP
- Servidores de prueba: Echo (7), Daytime (13), HTTP (80)
- Comandos: `telnet <IP> <puerto>`, cerrar con CTRL+] seguido de `quit`
- Ejemplo HTTP: `GET / HTTP/1.1` seguido de `Host: telnet.thm`

### DHCP (Protocolo de Configuración Dinámica de Host)
- **Proceso DORA:**
  - **D**iscover: Cliente transmite mensaje de descubrimiento
  - **O**ffer: Servidor ofrece dirección IP disponible
  - **R**equest: Cliente acepta la oferta
  - **A**cknowledge: Servidor confirma asignación
- Puertos: Servidor UDP 67, Cliente UDP 68
- Proporciona: IP, puerta de enlace, servidor DNS

### ARP (Protocolo de Resolución de Direcciones)
- Resuelve direcciones IP a direcciones MAC
- Proceso:
  - Host envía solicitud ARP a MAC de difusión
  - Host con IP correspondiente responde con su MAC
- Herramientas de análisis: `tshark`, `tcpdump`
- Opera en Capa 2 (Enlace de datos)

### ICMP (Protocolo de Mensajes de Control de Internet)
- Usado para diagnóstico y notificación de errores
- Comandos clave:
  - `ping`: Prueba conectividad (solicitud/respuesta eco ICMP)
  - `traceroute`: Descubre ruta entre hosts (mensajes Time Exceeded)
- Tipos ICMP importantes:
  - Tipo 0: Respuesta eco
  - Tipo 8: Solicitud eco
  - Tipo 11: Time Exceeded

### Protocolos de Enrutamiento
- **OSPF:** Open Shortest Path First (estado de enlace)
- **EIGRP:** Enhanced Interior Gateway Routing Protocol (propietario Cisco)
- **BGP:** Border Gateway Protocol (entre ISPs)
- **RIP:** Routing Information Protocol (redes pequeñas)

### NAT (Traducción de Direcciones de Red)
- Permite compartir una IP pública entre múltiples dispositivos privados
- Solución al agotamiento de direcciones IPv4
- Mantiene tabla de asignación entre IPs/puertos internos y externos

### DNS (Sistema de Nombres de Dominio)
- Traduce nombres de dominio a direcciones IP
- Opera en Capa 7 del modelo OSI
- Puertos: UDP 53, TCP 53
- **Tipos de registros:**
  - **A:** Dominio → IPv4
  - **AAAA:** Dominio → IPv6
  - **CNAME:** Redirección de dominio
  - **MX:** Servidor de correo
- Consulta: `nslookup <dominio>`
- Análisis con `tshark`

### Registros WHOIS
- Proporciona información del propietario del dominio
- Incluye: nombre, dirección, teléfono, email
- Consulta mediante servicios online o comando `whois`

### HTTP y HTTPS
- **HTTP:** Hypertext Transfer Protocol (TCP 80)
- **HTTPS:** HTTP con cifrado SSL/TLS (TCP 443)
- **Métodos comunes:**
  - GET: Solicita datos
  - POST: Envía datos
  - PUT: Crea/actualiza recurso
  - DELETE: Elimina recurso
- Análisis con Wireshark
- Pruebas manuales con telnet

## Protocolos de Comunicación Detallados

### Protocolo de Transferencia de Archivos (FTP)
- **Comandos principales:**
  - `USER <usuario>`: Ingresar nombre usuario
  - `PASS <contraseña>`: Ingresar contraseña
  - `RETR <archivo>`: Descargar archivo
  - `STOR <archivo>`: Subir archivo

### Protocolo de Transferencia de Correo (SMTP)
- **Comandos principales:**
  - `HELO <cliente>`: Iniciar sesión
  - `MAIL FROM:<remitente>`: Especificar remitente
  - `RCPT TO:<destinatario>`: Especificar destinatario
  - `DATA`: Inicio del mensaje
  - `.`: Final del mensaje

### Protocolo POP3 (Post Office Protocol v3)
- **Comandos principales:**
  - `USER <usuario>`: Identificar usuario
  - `PASS <contraseña>`: Autenticación
  - `STAT`: Obtener estadísticas
  - `LIST`: Listar mensajes
  - `RETR <número>`: Descargar mensaje
  - `DELE <número>`: Eliminar mensaje

### Protocolo IMAP (Internet Message Access Protocol)
- **Comandos principales:**
  - `LOGIN <usuario> <contraseña>`: Autenticación
  - `SELECT <buzón>`: Seleccionar carpeta
  - `FETCH <número> <datos>`: Obtener mensaje
  - `MOVE <número> <buzón>`: Mover mensaje
  - `LOGOUT`: Cerrar sesión

### Puertos Predeterminados de Protocolos

| Protocolo | Transporte | Puerto |
|-----------|------------|--------|
| TELNET    | TCP        | 23     |
| DNS       | UDP/TCP    | 53     |
| HTTP      | TCP        | 80     |
| HTTPS     | TCP        | 443    |
| FTP       | TCP        | 21     |
| SMTP      | TCP        | 25     |
| POP3      | TCP        | 110    |
| IMAP      | TCP        | 143    |

## Seguridad en Protocolos y VPN

### Seguridad en Credenciales
- Importancia del cifrado para evitar captura de credenciales en texto plano

### TLS (Transport Layer Security)
- Garantiza confidencialidad e integridad en comunicaciones
- Implementaciones: HTTPS, DoT, MQTTS, SIPS, SMTPS, POP3S, IMAPS

### Puertos Seguros con TLS

| Protocolo | Puerto inseguro | Puerto seguro (TLS) |
|-----------|-----------------|---------------------|
| HTTP      | 80              | 443                 |
| SMTP      | 25              | 465 / 587          |
| POP3      | 110             | 995                |
| IMAP      | 143             | 993                |

### Funcionamiento de HTTPS
- Conexión TCP
- Negociación TLS (intercambio de claves)
- Comunicación HTTP cifrada

### SSH vs Telnet
- **Telnet (puerto 23):** Inseguro, transmite en texto plano
- **SSH (puerto 22):** Proporciona:
  - Autenticación segura
  - Cifrado extremo a extremo
  - Protección contra ataques MitM
  - Túneles SSH y X11 Forwarding

### VPN (Redes Privadas Virtuales)
- Permiten conexiones seguras entre ubicaciones
- Enmascaran IP y protegen tráfico
- **Consideraciones:**
  - Posible filtración de IP real
  - No todas enrutan todo el tráfico
  - Restricciones legales en algunos países
