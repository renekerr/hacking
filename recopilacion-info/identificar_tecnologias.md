# Identificación de tecnologías

En el contexto de análisis de seguridad, herramientas como **WhatWeb** y **Web Analyzer** son útiles para identificar tecnologías empleadas en sitios web. A continuación, se presenta un breve resumen sobre su uso.

---

## **WhatWeb**
WhatWeb es una herramienta que detecta tecnologías web utilizadas por un sitio, incluyendo servidores, frameworks, sistemas de gestión de contenidos (CMS), librerías JavaScript, entre otros.

### **Instalación**
En sistemas basados en Debian (como Kali Linux), WhatWeb generalmente está preinstalado. Si no lo está, puedes instalarlo con:

```
sudo apt update && sudo apt install whatweb
```

### **Uso Básico**
1. **Análisis simple:**
   ```
   whatweb <URL>
   ```
   Ejemplo:
   ```
   whatweb https://ejemplo.com
   ```

2. **Análisis más detallado:**
   Utiliza el modo "verbose" para obtener más información:
   ```
   whatweb -v https://ejemplo.com
   ```

3. **Escaneo de múltiples URLs:**
   Puedes analizar varias URLs almacenadas en un archivo:
   ```
   whatweb -i urls.txt
   ```

4. **Salida en formato JSON:**
   Útil para integraciones o análisis automatizados:
   ```
   whatweb -a 3 --log-json resultado.json https://ejemplo.com
   ```

---

## **Web Analyzer**
Web Analyzer es otra herramienta poderosa para identificar tecnologías web. Ofrece una interfaz gráfica y también puede ser utilizada desde la línea de comandos.

### **Instalación**
Web Analyzer es un port de Wappalyzer en Go, diseñado para ser eficiente y analizar grandes listas de hosts.

1. Instala Web Analyzer con Go:
   ```
   go install -v github.com/rverton/webanalyze/cmd/webanalyze@latest
   ```

2. Copia el ejecutable al directorio `/usr/bin` para facilitar su uso:
   ```
   cp go/bin/webanalyze /usr/bin
   ```

### **Uso Básico**
1. **Mostrar opciones de ayuda:**
   ```
   webanalyze -h
   ```

2. **Análisis de un sitio web:**
   ```
   webanalyze -host https://ejemplo.com
   ```

3. **Escaneo de múltiples URLs desde un archivo:**
   ```
   webanalyze -hosts urls.txt
   ```
---

Estas herramientas son fundamentales en fases de reconocimiento durante pruebas de penetración. Con ellas, puedes obtener una visión clara de las tecnologías en uso, facilitando la identificación de posibles vulnerabilidades.
