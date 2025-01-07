# Documentación de Comandos para Instalación y Configuración de Entornos

Este documento presenta una recopilación de comandos útiles para la instalación y configuración de entornos en sistemas operativos basados en Linux, específicamente Kali Linux y Ubuntu. Los comandos están organizados por categorías y se incluye una breve descripción de cada uno.

## I. Configuración del Sistema Base

### 1. Modificación del Lenguaje

`sudo dpkg-reconfigure locales`  
`sudo reboot`

**Descripción:** Permite reconfigurar las configuraciones regionales del sistema, incluyendo el lenguaje de la interfaz. El reinicio es necesario para aplicar los cambios.

### 2. Actualización del Sistema

`sudo apt update && sudo apt upgrade -y`

**Descripción:** Actualiza la lista de paquetes disponibles e instala las actualizaciones para todos los paquetes instalados. La opción `-y` acepta automáticamente las confirmaciones.

## II. Configuración de Carpetas Compartidas (Ubuntu)

### 3. Habilitación de Carpetas Compartidas

`mkdir /mnt/hgfs`  
`vi /etc/fstab`

**Descripción:** Crea un directorio para montar la carpeta compartida y edita el archivo `fstab` para añadir la configuración necesaria.

**Línea a añadir en `fstab`:**

`.host:/ /mnt/hgfs fuse.vmhgfs-fuse auto,allow_other 0 0`

`sudo reboot`  
`cd /mnt/hgfs`  
`ls`

**Descripción:** Después de editar `fstab`, se reinicia el sistema para aplicar los cambios y se accede al directorio montado para verificar que la carpeta compartida está disponible.

## III. Instalación de Herramientas

### 4. Instalación de Kalipwm

`git clone https://github.com/afsh4ck/kalipwm.git`  
`cd kalipwm`  
`bash kalipwm.sh`  
`sudo reboot`

**Descripción:** Clona el repositorio de Kalipwm desde GitHub, accede al directorio clonado y ejecuta el script de instalación. Reinicia el sistema para completar la instalación.

### 5. Instalación de Miniconda

**Descripción:** Miniconda es una distribución mínima de Anaconda para crear entornos virtuales y gestionar paquetes.

1.  **Instalación:** Seguir las instrucciones en [Miniconda](https://docs.anaconda.com/miniconda/install/).
2.  **Cierre y reapertura de terminal:** Después de la instalación, cerrar y abrir nuevamente la terminal.
3.  **Configuración del entorno base:**

    `echo 'export PATH="$HOME/miniconda3/bin:$PATH"' >> ~/.zshrc`  
    `source miniconda3/bin/activate`

4.  **Desactivar auto-activación del entorno base:**

    `conda config --set auto_activate_base false`
5.  **Creación de un nuevo entorno:**

    `conda create -n "old_harvester" python=3.8.0 -c conda-forge`

### 6. Instalación de una Versión Anterior de theHarvester

`mkdir old_harvester`  
`cd old_harvester`  
`wget https://github.com/laramies/theHarvester/archive/refs/tags/3.2.2.zip`  
`unzip 3.2.2.zip`  
`cd theHarvester-3.2.2/`  
`pip install -r requirements/base.txt`

**Descripción:** Crea un directorio para la versión anterior de theHarvester, descarga el zip de la versión 3.2.2, lo descomprime, accede al directorio de la versión y luego instala las dependencias necesarias del archivo `requirements/base.txt`.
