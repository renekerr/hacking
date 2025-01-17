# Comandos Relevantes para Shodan

## Tabla de Comandos

| Comando         | Ejemplo                                      | Descripción                                                                 |
|-----------------|----------------------------------------------|-----------------------------------------------------------------------------|
| `after`         | `after:01/01/2023`                          | Muestra resultados posteriores a la fecha especificada (dd/mm/yyyy).        |
| `asn`           | `asn:AS12345`                               | Filtra los resultados por número de sistema autónomo (ASN).                  |
| `before`        | `before:01/01/2022`                         | Muestra resultados anteriores a la fecha especificada (dd/mm/yyyy).         |
| `category`      | `category:malware`                           | Filtra los resultados según una categoría específica, como malware.         |
| `city`          | `city:"New York"`                            | Muestra dispositivos ubicados en una ciudad específica.                     |
| `country`       | `country:"US"`                               | Filtra resultados para un país específico usando el código de dos letras.  |
| `geo`           | `geo:40.7128,-74.0060,50`                   | Muestra dispositivos dentro de un rango geográfico especificado.           |
| `hash`          | `hash:1234567890abcdef`                      | Filtra los resultados por un valor hash específico.                         |
| `has_ipv6`      | `has_ipv6:true`                              | Filtra los dispositivos que tienen soporte IPv6.                            |
| `has_screenshot`| `has_screenshot:true`                        | Filtra dispositivos que tienen una captura de pantalla disponible.         |
| `server`        | `server:"Apache"`                            | Filtra dispositivos que usan un servidor específico, como Apache.           |
| `hostname`      | `hostname:"example.com"`                     | Filtra dispositivos por su nombre de host.                                  |
| `ip`            | `ip:192.168.1.1`                            | Filtra resultados para una dirección IP específica.                        |
| `isp`           | `isp:"Comcast"`                              | Filtra los resultados por el ISP (Proveedor de servicios de Internet).     |
| `net`           | `net:192.168.1.0/24`                        | Filtra resultados dentro de un rango de red especificado en notación CIDR. |
| `org`           | `org:"Google Inc."`                          | Filtra los resultados por la organización asignada al bloque de red.       |
| `os`            | `os:"Linux"`                                 | Filtra dispositivos que usan un sistema operativo específico.               |
| `port`          | `port:22`                                    | Muestra dispositivos que tienen el puerto especificado (por ejemplo, SSH). |
| `postal`        | `postal:"90210"`                             | Filtra dispositivos en un código postal específico (solo en EE. UU.).      |
| `product`       | `product:"nginx"`                            | Filtra los resultados por un producto de software específico.               |
| `region`        | `region:"California"`                        | Filtra dispositivos en una región o estado específico.                      |
| `state`         | `state:"Texas"`                              | Alias de `region`, filtra dispositivos en un estado específico.            |
| `version`       | `version:"1.0"`                              | Filtra resultados que contienen una versión específica de un producto.     |
| `vuln`          | `vuln:CVE-2023-1234`                         | Filtra resultados por una vulnerabilidad específica identificada por CVE.  |
