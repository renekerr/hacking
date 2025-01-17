# DNS Zones  

Esta tabla describe los diferentes tipos de registros DNS que se utilizan para configurar y gestionar zonas DNS. Cada tipo de registro cumple una función específica, como asociar nombres de dominio con direcciones IP, gestionar el enrutamiento de correos electrónicos o garantizar la seguridad de las consultas DNS.


| **Tipo**   | **Descripción**                                                                                   | **Significado**                                                          |
|------------|---------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------|
| **A**      | Asocia un nombre de dominio con una dirección IPv4.                                               | Address Record                                                           |
| **AAAA**   | Asocia un nombre de dominio con una dirección IPv6.                                               | IPv6 Address Record                                                      |
| **CNAME**  | Alias de un dominio hacia otro.                                                                   | Canonical Name Record                                                    |
| **MX**     | Redirige correos electrónicos a un servidor de correo.                                            | Mail Exchange                                                            |
| **TXT**    | Contiene información de texto arbitraria, utilizada comúnmente para SPF, DKIM o DMARC.            | Text Record                                                              |
| **NS**     | Delegación de un dominio a servidores DNS autoritativos.                                          | Name Server Record                                                       |
| **PTR**    | Asocia una dirección IP con un nombre de dominio (DNS inverso).                                   | Pointer Record                                                           |
| **SOA**    | Contiene información administrativa sobre el dominio y configuración de la zona.                  | Start of Authority Record                                                |
| **SRV**    | Define la ubicación de servicios específicos, como SIP o LDAP.                                    | Service Locator                                                          |
| **CAA**    | Especifica las autoridades de certificación autorizadas para emitir certificados para el dominio. | Certification Authority Authorization                                    |
| **NAPTR**  | Usado para localización de recursos más complejos, común en VoIP o ENUM.                          | Naming Authority Pointer Record                                          |
| **DNSKEY** | Parte de DNSSEC, contiene la clave pública para validar firmas DNSSEC.                            | DNS Public Key Record                                                    |
| **RRSIG**  | Contiene la firma digital de los registros protegidos por DNSSEC.                                 | DNSSEC Signature                                                         |
| **DS**     | Apunta a un registro DNSKEY en una zona hija para DNSSEC.                                         | Delegation Signer                                                        |
| **HINFO**  | Describe el hardware y sistema operativo de un host.                                              | Host Information Record                                                  |
| **SPF**    | Define servidores de correo autorizados (ahora implementado como registro TXT).                   | Sender Policy Framework                                                  |
| **TLSA**   | Usado para DANE (Autenticación basada en DNS).                                                    | Transport Layer Security Authentication                                  |
| **LOC**    | Especifica la ubicación geográfica de un dominio.                                                 | Location Record                                                          |
| **RP**     | Proporciona información de contacto de la persona responsable del dominio.                        | Responsible Person                                                       |
| **AFSDB**  | Apunta a servidores para el sistema de archivos Andrew (AFS).                                     | Andrew File System Database                                              |
