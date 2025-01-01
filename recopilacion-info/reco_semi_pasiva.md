# Recopilación Semi-Pasiva de Información

La recopilación semi-pasiva de información se diferencia de la recopilación pasiva en que sí genera tráfico o interacción con el objetivo, pero de manera que este no detecte dicha actividad como inusual. Las técnicas utilizadas imitan el comportamiento normal de un usuario o cliente legítimo.

## Actividades Incluidas
1. **Consultas DNS**
   - Resolver nombres de dominio.
   - Buscar dominios registrados en un servidor DNS.

2. **Acceso a Recursos Internos**
   - Interactuar con aplicaciones web de la organización.
   - Registrarse y descargar archivos.

3. **Análisis de Metadatos**
   - Revisar documentos que requieren un intercambio previo de tráfico de red.

## Exclusiones
- Actividades que generen tráfico anómalo, como escaneos de puertos o vulnerabilidades, y fuerza bruta, ya que entrarían en la recopilación activa de información.

La recopilación semi-pasiva sigue siendo parte del proceso de obtención de información, buscando datos útiles para las fases siguientes del proceso de análisis cinético.


# Acciones, Herramientas y Utilidades para la Recopilación Semi-Pasiva de Información

En la recopilación semi-pasiva de información se utilizan diversas acciones, herramientas y utilidades para interactuar con el objetivo sin que este detecte actividad anómala. Aquí se detallan algunas de las más comunes:

## Acciones Comunes
1. **Consultas a Servidores DNS**
   - Resolución de nombres de dominio.
   - Búsqueda de dominios registrados en un servidor DNS específico.

2. **Acceso a Aplicaciones Web**
   - Registro y login en aplicaciones web.
   - Descarga de archivos y recursos internos.

3. **Análisis de Metadatos**
   - Análisis de documentos obtenidos a través de interacciones normales con el objetivo.

## Herramientas y Utilidades
1. **DNSenum**
   - Herramienta para enumerar información DNS, incluyendo la búsqueda de nombres de dominio asociados a un servidor DNS.

2. **Fierce**
   - Utilidad para realizar escaneos de DNS y encontrar posibles subdominios y otros registros relacionados.

3. **HTTrack**
   - Herramienta para descargar y clonar sitios web, permitiendo un análisis offline.

4. **Burp Suite**
   - Plataforma para realizar pruebas de seguridad en aplicaciones web, facilitando la interacción con los recursos internos de manera controlada.

5. **Metagoofil**
   - Herramienta para extraer metadatos de documentos disponibles públicamente y aquellos obtenidos a través de interacciones con el objetivo.

6. **WhatWeb**
   - Utilidad para identificar tecnologías utilizadas en sitios web, proporcionando información detallada sobre el objetivo sin generar tráfico anómalo.

## Prácticas Recomendadas
- **Imitar Comportamiento Normal:** Asegurarse de que todas las interacciones imiten el comportamiento de un usuario legítimo.
- **Evitar Fuerza Bruta:** No utilizar técnicas que generen un volumen elevado de tráfico o que puedan ser detectadas fácilmente como anómalas.
- **Monitoreo Continuo:** Utilizar herramientas de monitoreo para asegurarse de que el tráfico generado no es detectado por el objetivo.

Estas acciones y herramientas permiten una recopilación eficiente y discreta de información, facilitando las siguientes fases del análisis sin alertar al objetivo.
