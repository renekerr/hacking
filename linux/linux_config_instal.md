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
Seguir las instrucciones en el sitio oficial de [Miniconda](https://docs.conda.io/en/latest/miniconda.html).

**Cierre y reapertura de terminal:** Después de la instalación, cerrar y abrir nuevamente la terminal.

**Configuración del entorno base:**

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

### 7. Instalación de kalipwm

```bash
git clone https://github.com/afsh4ck/kalipwm.git
cd kalipwm
bash kalipwm.sh
sudo reboot
```

**Descripción:**  
Clona el repositorio de Kalipwm desde GitHub, accede al directorio clonado y ejecuta el script de instalación. Reinicia el sistema para completar la instalación. Una vez reiniciado, en la pantalla de inicio de sesión, selecciona el entorno de ventana `bspwm` para comenzar a utilizarlo.

Fuente: [https://github.com/afsh4ck/kalipwm](https://github.com/afsh4ck/kalipwm)

---

### Personalización de `bspwm` tras la instalación

Las siguientes modificaciones se realizan para optimizar el entorno de trabajo en `bspwm`: la primera elimina el padding entre ventanas ajustando los márgenes y bordes, lo que maximiza el uso del espacio en pantalla y crea un diseño más compacto. La segunda asegura que el atajo para abrir la terminal utilice `qterminal` en lugar de `kitty`, proporcionando acceso a menús, preferencias y opciones de personalización integradas directamente en la interfaz de `qterminal`.


#### 1. Ajustes en el archivo `bspwmrc`

```bash
cd .config
```

Modifica el archivo ubicado en `~/.config/bspwm/bspwmrc`.  

Cambia los valores de las siguientes configuraciones para personalizar el entorno:  

```bash
bspc config border_width         1 # Por defecto: 2
bspc config window_gap           1 # Por defecto: 12
```

**Descripción:**  
- **`border_width`**: Ajusta el grosor del borde de las ventanas a un valor más delgado (1 píxel en lugar de 2).  
- **`window_gap`**: Reduce el espacio entre las ventanas de 12 píxeles a 1 píxel, proporcionando un diseño más compacto.  

#### 2. Cambios en el archivo `sxhkdrc`

Modifica el archivo ubicado en `~/.config/sxhkd/sxhkdrc`.  

Cambia las configuraciones relacionadas con el emulador de terminal para usar `qterminal` en lugar de la línea comentada:  

```bash
# terminal emulator
super + Return
#	~/.local/kitty.app/bin/kitty (línea comentada)
	qterminal
```

**Descripción:**  
- **`super + Return`**: Define el atajo de teclado para abrir el emulador de terminal (`qterminal` en este caso).  
- La línea predeterminada para `kitty` se deja comentada, indicando que ahora se utilizará `qterminal` como alternativa.  

### Comandos de BSPWM

| **Comando**                     | **Descripción**                                                                 |
|----------------------------------|---------------------------------------------------------------------------------|
| **Clic derecho en Polybar**     | Cambia el tema de Polybar usando el menú del clic derecho.                      |
| **Windows + 1,2,3,4**           | Navega entre escritorios.                                                       |
| **Windows + Enter**             | Abre una nueva terminal.                                                       |
| **Windows + Enter**             | Divide la terminal actual.                                                     |
| **Windows + Flechas**           | Navega entre ventanas abiertas.                                                |
| **Windows + Tab**               | Cambia entre los dos escritorios más recientes.                                |
| **Windows + W**                 | Cierra la terminal actual.                                                     |
| **Windows + Alt + R**           | Recarga el entorno de escritorio.                                              |
| **Windows + Alt + Q**           | Reinicia BSPWM.                                                                |
| **Windows + Alt + Flechas**     | Redimensiona la ventana actual.                                                |
| **Windows + Shift + F**         | Abre Firefox.                                                                  |
| **Windows + Shift + B**         | Abre Burp Suite.                                                               |
| **Windows + Shift + 1,2,3,4**   | Mueve la ventana actual a otro escritorio.                                     |
| **Windows + Shift + Flechas**   | Mueve la ventana actual.                                                       |
| **Ctrl + Shift + -/+**          | Cambia el tamaño del texto en la terminal.                                     |
| **Ctrl + T**                    | Abre un navegador avanzado desde la terminal.                                  |

---
