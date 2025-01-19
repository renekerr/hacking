# Estructura de Repositorio para Hacking Ético y Ciberseguridad

```plaintext
└── hacking
    ├── .github                 # Directorio para configuración de GitHub (workflows, templates, etc.)
    │   └── workflows
    │       └── markdown-link-check.yml   # Ejemplo: workflow para verificar enlaces rotos
    ├── 00-INTRODUCCION
    │   ├── 00-README.md        # README principal del repositorio (se mueve el original)
    │   ├── 01-LICENSE          # Mantiene el archivo de licencia
    │   └── 02-glosario.md      # Glosario general, movido aquí para mejor acceso.
    ├── 01-FUNDAMENTOS
    │   ├── 01-ciberseguridad
    │   │    ├── 01-metodologias_hacking_etico.md
    │   │    ├── 02-modelo-osi.md
    │   │    ├── 03-principios_seguridad.md
    │   │    └── 04-seguridad_defensiva.md
    │   ├── 02-redes
    │   │    └── 01-modelos_y_protocolos_comunicacion.md
    │   └── 03-linux  
    │        ├── 01-linux_config_instal.md
    │        └── 02-linux_notas.md
    ├── 02-RECONOCIMIENTO
    │   ├── 01-pasivo
    │   │   ├── 01-OSINT.md
    │   │   ├── 02-comandos_google.md
    │   │   ├── 03-comandos_shodan.md
    │   │   ├── 04-identificar_tecnologias.md
    │   │   └── 05-recopilacion_pasiva.md
    │   └── 02-activo
    │       ├── 01-dns.md
    │       └── 02-recopilacion_activa.md
    ├── 03-ANALISIS-VULNERABILIDADES
    │  └── ...                  # Carpetas y archivos según vayas avanzando (Nmap, Nessus, etc.)
    ├── 04-EXPLOITACION
    │  └── ...                  # Carpetas y archivos según vayas avanzando (Metasploit, exploits manuales, etc.)
    ├── 05-POST-EXPLOTACION
    │  └── ...                  # Carpetas y archivos según vayas avanzando (Escalada de privilegios, persistencia, etc.)
    ├── 06-INFORMES-Y-DOCUMENTACION
    │  └── ...                  # Carpetas y archivos sobre cómo hacer informes y documentación
    ├── 07-PRACTICAS-EJERCICIOS       # Carpeta para prácticas o ejercicios realizados
    │   ├── retos                   # Subcarpeta para retos y CTFs
    │   │   ├── 01-retos_plataforma.md    # Notas sobre retos en plataformas como Hack The Box, TryHackMe, etc.
    │   │   ├── 02-competencias.md        # Información sobre competencias realizadas
    │   │   └── 03-notas_generales.md     # Notas generales sobre estrategias o aprendizaje en CTFs
    │   ├── ejemplos                # Subcarpeta para ejercicios prácticos
    │   └── assets                  # Multimedia relacionado con las prácticas o ejercicios
    ├── 99-VARIOS               # Para notas misceláneas o archivos que no encajan en las categorías principales
    │   ├── 01-estructura_repositorio.md
    │   ├── 02-md_formatos.md
    │   ├── 03-notas.md
    │   └── 04-revisar.md
    └── assets                # (Nuevo) Para guardar imágenes o archivos multimedia usados en los .md
```
