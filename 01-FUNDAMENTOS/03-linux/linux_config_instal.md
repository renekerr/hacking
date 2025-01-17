---

# Documentación de Comandos para Instalación y Configuración de Entornos

Este documento presenta una recopilación de comandos útiles para la instalación y configuración de entornos en sistemas operativos basados en Linux, específicamente Kali Linux y Ubuntu. Los comandos están organizados por categorías y se incluye una breve descripción de cada uno.

---

## I. Configuración del Sistema Base

### 1. Modificación del Lenguaje

```bash
sudo dpkg-reconfigure locales
sudo reboot
```

**Descripción:** Permite reconfigurar las configuraciones regionales del sistema, incluyendo el lenguaje de la interfaz. El reinicio es necesario para aplicar los cambios.

---

### 2. Actualización del Sistema

```bash
sudo apt update && sudo apt upgrade -y
```

**Descripción:** Actualiza la lista de paquetes disponibles e instala las actualizaciones para todos los paquetes instalados. La opción `-y` acepta automáticamente las confirmaciones.

---

## II. Configuración Inicial en Kali Linux

### 3. Creación de Usuario

Tras la instalación de Kali Linux, es recomendable crear un usuario personalizado para tareas cotidianas en lugar de utilizar el usuario root. Esto mejora la seguridad del sistema.

**Pasos para crear un nuevo usuario:**

```bash
sudo adduser newuser
sudo adduser newuser sudo
sudo adduser newuser kali-trusted
```

**Descripción:**  
- `adduser newuser`: Crea el usuario `newuser`.  
- `adduser newuser sudo`: Añade `newuser` al grupo `sudo`, permitiéndole ejecutar comandos con privilegios de administrador.  
- `adduser newuser kali-trusted`: Agrega `newuser` al grupo `kali-trusted`, habilitando el acceso a herramientas propias de Kali.  

Para verificar la creación del usuario y su pertenencia a los grupos, ejecuta:  

```bash
id newuser
```

Salida esperada:  
```bash
uid=1001(newuser) gid=1001(newuser) groups=1001(newuser),27(sudo),100(users),133(kali-trusted)
```

---

## III. Configuración de Carpetas Compartidas (Ubuntu)

### 4. Habilitación de Carpetas Compartidas

```bash
mkdir /mnt/hgfs
vi /etc/fstab
```

Línea a añadir en `fstab`:

```
.host:/ /mnt/hgfs fuse.vmhgfs-fuse auto,allow_other 0 0
```

```bash
sudo reboot
cd /mnt/hgfs
ls
```

**Descripción:** Crea un directorio para montar la carpeta compartida y edita el archivo `fstab` para añadir la configuración necesaria. Después de reiniciar, verifica que la carpeta compartida esté disponible.

---

## IV. Instalación de Herramientas

### 5. Instalación de Miniconda

**Descripción:** Miniconda es una distribución mínima de Anaconda para crear entornos virtuales y gestionar paquetes.

**Instalación:**  
Seguir las instrucciones en el sitio oficial de [Miniconda](https://docs.anaconda.com/miniconda/install/). 

Alternativamente se puede descargar de este [repositorio](https://repo.anaconda.com/miniconda/) la release que deseemos.

**Cierre y reapertura de terminal:** Después de la instalación, cerrar y abrir nuevamente la terminal.

**Configuración del entorno base:**
Nota: si no aparece 'base', ejecutamos lo siguiente:

```bash
echo 'export PATH="$HOME/miniconda3/bin:$PATH"' >> ~/.zshrc
source miniconda3/bin/activate
```

**Desactivar auto-activación del entorno base:**

```bash
conda config --set auto_activate_base false
```

**Creación de un nuevo entorno:**

```bash
conda create -n "old_harvester" python=3.8.0 -c conda-forge
```

**Activar el nuevo entorno**
```bash
conda activate old_harvester
```

**Desactivar el nuevo entorno**
```bash
conda deactivate
```

---

### 6. Instalación de una Versión Anterior de theHarvester

```bash
mkdir old_harvester
cd old_harvester
wget https://github.com/laramies/theHarvester/archive/refs/tags/3.2.2.zip
unzip 3.2.2.zip
cd theHarvester-3.2.2/
pip install -r requirements/base.txt
```

**Descripción:** Crea un directorio para la versión anterior de theHarvester, descarga el archivo comprimido de la versión 3.2.2, lo descomprime, accede al directorio y luego instala las dependencias necesarias desde el archivo `requirements/base.txt`.

---

