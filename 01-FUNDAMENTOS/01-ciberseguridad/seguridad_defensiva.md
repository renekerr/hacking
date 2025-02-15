# Visión General de la Seguridad Defensiva

## Roles en Ciberseguridad

- **Especialista en Pruebas de Penetración (Penetration Tester)**: Profesional que realiza evaluaciones de seguridad simulando ataques reales para identificar vulnerabilidades en sistemas, aplicaciones y redes, con el objetivo de proporcionar recomendaciones para mejorar la defensa ante posibles amenazas.
- **Equipo Rojo (Red Teamer)**: Simula ataques reales sobre una organización para poner a prueba sus defensas y mejorar la capacidad de respuesta ante incidentes de seguridad.
- **Ingeniero de Seguridad (Security Engineer)**: Diseña, implementa y mantiene controles de seguridad, redes y sistemas para proteger contra ciberamenazas.

---

## Tareas de Seguridad Defensiva

### Responsabilidades Clave:
- **Concientización en Ciberseguridad**: Educar a los usuarios para reducir los riesgos de ataques dirigidos como phishing o ingeniería social.
- **Gestión de Activos**: Mantener un inventario actualizado de sistemas y dispositivos para aplicar políticas de seguridad adecuadas.
- **Mantenimiento de Parches**: Asegurar que todos los sistemas estén al día con las últimas actualizaciones de seguridad.
- **Configuración de Herramientas de Seguridad**:
  - **Firewalls (Cortafuegos)**: Controlan el tráfico de red y bloquean posibles amenazas.
  - **Sistemas de Prevención de Intrusiones (IPS)**: Detectan y bloquean ataques en tiempo real.
- **Monitoreo y Registro de Seguridad**: Detectar comportamientos inusuales o no autorizados en la red.

### Metodologías de Evaluación en Ciberseguridad

Las siguientes metodologías son fundamentales para evaluar la seguridad de sistemas, aplicaciones y redes:

#### OSSTMM (Open Source Security Testing Methodology Manual)
Proporciona un marco detallado para la evaluación de la seguridad de sistemas, redes y el aspecto humano, abarcando:
- Telecomunicaciones (VoIP, redes móviles)
- Redes cableadas e inalámbricas

#### OWASP (Open Web Application Security Project)
Enfocado en la seguridad de aplicaciones web, con un listado anual de las **10 vulnerabilidades más críticas** y mejores prácticas para mitigarlas.

#### NIST Cybersecurity Framework 1.1
Un marco estándar para mejorar las prácticas de ciberseguridad en infraestructuras críticas y organizaciones comerciales, centrándose en la gestión de riesgos cibernéticos.

#### NCSC CAF (Cyber Assessment Framework)
Evalúa la postura de seguridad de organizaciones críticas como proveedores de servicios financieros y de infraestructura, centrándose en áreas clave como resiliencia y monitoreo continuo.

---

## Centro de Operaciones de Seguridad (SOC)

Un SOC está compuesto por expertos en ciberseguridad que supervisan continuamente redes y sistemas para detectar y responder a incidentes de seguridad.

### Áreas de Enfoque:
- **Vulnerabilidades**: Gestionar debilidades en los sistemas, aplicando parches o mitigaciones si no hay soluciones inmediatas.
- **Violaciones de Políticas**: Detectar y responder a infracciones de las normas internas de seguridad.
- **Accesos No Autorizados**: Identificar y bloquear inicios de sesión o actividades maliciosas.
- **Intrusiones de Red**: Detectar ataques como phishing, malware y explotación de vulnerabilidades.

### Inteligencia de Amenazas
La inteligencia de amenazas involucra la recopilación de información sobre adversarios potenciales para reforzar las defensas. Implica:
- Analizar registros de red y fuentes externas.
- Estudiar tácticas y motivaciones de los atacantes.
- Desarrollar estrategias de mitigación adaptadas.

---

## Análisis Forense Digital y Respuesta a Incidentes (DFIR)

### Análisis Forense Digital
Se centra en la recolección y análisis de evidencia digital tras un ataque. Las áreas clave incluyen:
- **Sistemas de Archivos**: Investigación de archivos eliminados y datos corrompidos.
- **Memoria del Sistema**: Análisis de la RAM para identificar procesos maliciosos en ejecución.
- **Registros de Red**: Estudio de logs para rastrear el origen y la extensión de los ataques.

### Respuesta a Incidentes
La respuesta estructurada a incidentes incluye las siguientes fases:
1. **Preparación**: Desarrollar planes y capacitar a equipos para prevenir futuros incidentes.
2. **Detección y Análisis**: Identificar rápidamente y evaluar la naturaleza del ataque.
3. **Contención, Erradicación y Recuperación**: Limitar los daños, eliminar la amenaza y restaurar los sistemas.
4. **Revisión Post-Incidente**: Analizar las lecciones aprendidas para fortalecer la seguridad.

---

## Análisis de Malware

El malware (virus, troyanos, ransomware) se utiliza para dañar o tomar control de sistemas. Algunas de las formas más comunes incluyen:
- **Virus**: Programas que se replican y dañan archivos y sistemas.
- **Troyanos**: Programas maliciosos que se camuflan como legítimos, permitiendo el acceso remoto.
- **Ransomware**: Cifra archivos importantes y solicita un rescate para su liberación.

### Técnicas de Análisis:
- **Análisis Estático**: Inspección sin ejecutar el malware, analizando el código y las firmas.
- **Análisis Dinámico**: Ejecutar el malware en un entorno controlado para estudiar su comportamiento en tiempo real.

---
