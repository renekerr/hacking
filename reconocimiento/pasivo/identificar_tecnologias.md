# Identificación de tecnologías

En el contexto de análisis de seguridad, una herramienta como **WhatWeb** peude ser útil para identificar tecnologías empleadas en sitios web.

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
   whatweb https://udemy.com | awk '{gsub(/], /, "],\n"); print}'
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

