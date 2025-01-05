| **Tipo**   | **Descripción**                                                                                   |
|------------|---------------------------------------------------------------------------------------------------|
| **A**      | Asocia un nombre de dominio con una dirección IPv4.                                               |
| **AAAA**   | Asocia un nombre de dominio con una dirección IPv6.                                               |
| **CNAME**  | Alias de un dominio hacia otro.                                                                   |
| **MX**     | Redirige correos electrónicos a un servidor de correo.                                            |
| **TXT**    | Contiene información de texto arbitraria, utilizada comúnmente para SPF, DKIM o DMARC.            |
| **NS**     | Delegación de un dominio a servidores DNS autoritativos.                                          |
| **PTR**    | Asocia una dirección IP con un nombre de dominio (DNS inverso).                                   |
| **SOA**    | Contiene información administrativa sobre el dominio y configuración de la zona.                  |
| **SRV**    | Define la ubicación de servicios específicos, como SIP o LDAP.                                    |
| **CAA**    | Especifica las autoridades de certificación autorizadas para emitir certificados para el dominio. |
| **NAPTR**  | Usado para localización de recursos más complejos, común en VoIP o ENUM.                          |
| **DNSKEY** | Parte de DNSSEC, contiene la clave pública para validar firmas DNSSEC.                            |
| **RRSIG**  | Contiene la firma digital de los registros protegidos por DNSSEC.                                 |
| **DS**     | Apunta a un registro DNSKEY en una zona hija para DNSSEC.                                         |
| **HINFO**  | Describe el hardware y sistema operativo de un host.                                              |
| **SPF**    | Define servidores de correo autorizados (ahora implementado como registro TXT).                   |
| **TLSA**   | Usado para DANE (Autenticación basada en DNS).                                                    |
| **LOC**    | Especifica la ubicación geográfica de un dominio.                                                 |
| **RP**     | Proporciona información de contacto de la persona responsable del dominio.                        |
| **AFSDB**  | Apunta a servidores para el sistema de archivos Andrew (AFS).                                     |