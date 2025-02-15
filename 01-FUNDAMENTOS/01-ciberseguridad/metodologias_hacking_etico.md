# Metodologías de Hacking Ético

## Importancia
Las metodologías proporcionan un conjunto ordenado de actividades que garantizan el éxito en la evaluación y mejora de la seguridad de sistemas informáticos. Siguiendo un enfoque estructurado, los profesionales pueden identificar, explotar y mitigar vulnerabilidades de manera eficiente.

## Metodologías Principales
1. **OSSTMM (Open Source Security Testing Methodology Manual)**  
   - [Documento oficial](https://www.isecom.org/OSSTMM.3.pdf)
2. **The Penetration Testing Execution Standard (PTES)**  
   - [Sitio web oficial](http://www.pentest-standard.org/index.php/Main_Page)
3. **ISSAF (Information Systems Security Assessment Framework)**
4. **OTP (OWASP Testing Project)**

## Metodología de Pruebas de Penetración
1. **Definición del Alcance:** Establecimiento de objetivos y límites de la prueba.
2. **Recopilación de Información:** OSINT, exploración y enumeración.
3. **Identificación y Análisis de Vulnerabilidades:** Evaluación de seguridad en servicios, aplicaciones y redes.
4. **Explotación de Vulnerabilidades:** Ejecución de pruebas para validar las debilidades.
5. **Escalada de Privilegios:** Obtención de accesos avanzados dentro del sistema.
6. **Post-Explotación:** Mantenimiento del acceso, extracción de información y persistencia.
7. **Elaboración del Reporte Final:** Documentación de hallazgos y recomendaciones.

## Equipos de Seguridad: Red Team vs. Blue Team

| **Equipo**    | **Rol**                                       | **Actividades Típicas**  |
|--------------|-------------------------------------------|------------------------------------------------|
| **Red Team** | Simula ataques reales (seguridad ofensiva). | Phishing, pruebas de penetración, evaluaciones de ingeniería social, simulaciones de ataques avanzados (APT), análisis de vectores de ataque. |
| **Blue Team** | Protege y responde a amenazas (seguridad defensiva). | Respuesta a incidentes, análisis forense digital, investigación de amenazas emergentes, bastionado de sistemas, creación de políticas de seguridad, monitorización activa. |

## Tipos de Pruebas de Penetración

| **Tipo**         | **Descripción**  | **Conocimiento** | **Ventajas** | **Desventajas** |
|-----------------|----------------|---------------|-------------|-------------|
| **Caja Negra**  | Sin conocimiento previo del sistema. | Ninguno | Simula un atacante real, sin información previa. | Requiere mayor tiempo para recopilación de datos. |
| **Caja Gris**   | Conocimiento parcial del sistema. | Limitado | Equilibrio entre realismo y eficiencia. | Puede no revelar todas las vulnerabilidades. |
| **Caja Blanca** | Conocimiento total del sistema. | Total | Permite un análisis exhaustivo y profundo. | Puede ser más lento y costoso. |

## Metodologías de la Industria

| **Metodología** | **Descripción** | **Ventajas** | **Desventajas** |
|------------------|----------------|------------|------------|
| **OSSTMM** | Marco detallado para evaluar seguridad en sistemas, software y comunicaciones. | Estrategia flexible, cobertura amplia, estándar global. | Complejo, usa definiciones técnicas específicas. |
| **OWASP** | Enfocado en pruebas de seguridad en aplicaciones web. | Frecuentemente actualizado, fácil de aplicar. | No cubre todas las vulnerabilidades posibles. |
| **NIST CSF** | Marco para mejorar la seguridad cibernética. | Estandarizado, detallado, ampliamente utilizado. | Políticas de auditoría pueden ser débiles. |
| **NCSC CAF** | Evalúa riesgos cibernéticos en servicios críticos. | Diseñado por una agencia gubernamental, acreditado. | Basado en principios más que reglas explícitas. |

