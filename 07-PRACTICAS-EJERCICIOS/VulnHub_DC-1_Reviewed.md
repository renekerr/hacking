# DC-1 VulHub | Walkthrough

## Enlace al Desafío en Vulnhub
[https://www.vulnhub.com/entry/dc-1,292/](https://www.vulnhub.com/entry/dc-1,292/)


## Descripción
DC-1 es un laboratorio vulnerable diseñado específicamente para que principiantes adquieran experiencia en pruebas de penetración. La dificultad dependerá de las habilidades, conocimientos y capacidad de aprendizaje del usuario.

### Requisitos
- Conocimientos básicos de Linux.
- Familiaridad con la línea de comandos de Linux.
- Experiencia con herramientas básicas de pruebas de penetración, como las disponibles en Kali Linux o Parrot Security OS.

### Objetivo
El objetivo es encontrar y leer la bandera ubicada en el directorio `root`. Aunque no es necesario ser `root` para acceder a la bandera, sí se requieren privilegios elevados.

### Detalles adicionales
- **Número de banderas:** 5
- Estas banderas contienen pistas útiles para principiantes.
- Opcional: los usuarios avanzados pueden omitir las banderas intermedias e ir directamente por `root`.

## Configuración del Entorno
Descargaremos la máquina y la importaremos en VirtualBox. Utilizaremos una máquina Kali Linux para interactuar con el laboratorio. En VirtualBox, debemos crear previamente una red NAT: 

1. Ir a **Archivo → Herramientas → Administrador de red → Redes NAT** y crear una nueva red.
2. Asignar ambas máquinas (DC-1 y Kali Linux) a la red NAT creada.

![image](https://github.com/user-attachments/assets/fa3a8b20-82f7-45ba-93c2-242ab3340db8)
