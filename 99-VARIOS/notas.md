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
