# Tareas postinstalación para Debian 11 y 12 en PC (También Lenovo X260)

Listado de tareas postinstalación para Debian 11 o 12. Tras este checklist, se podría realizar un backup del sistema por si alguna vez necesitamos instalar el sistema operativo rápidamente.
Para este propósito se puede utilizar [Clonezilla Downloads](https://clonezilla.org/downloads.php)

## 1. Agregar permisos administrador (sudo) a usuario normal.

Abrir el terminal y validarse como root

```bash
su
```

Agregar al usuario como usuario administrador

```bash
/sbin/usermod -aG sudo usuario
```

Cierra sesión o reinicia para que los cambios sean efectivos

## 2. Actualizar el sistema

```bash
sudo apt update && sudo apt upgrade
```

## 3. Desinstalar juegos preinstalados

Debian 11 viene por defecto con un montón de juegos (19) preinstalados. ¿Porque Gnome viene con tantos juegos preinstalados? Quien sabe, pero yo prefiero desinstalarlos todos y luego instalar aquel que vaya a utilizar. Los juegos que se van a desinstalar son los siguientes:

* Gnome 2048 
* Aisleriot (solitario) 
* Atomix (?)
* Gnome Chess 
* Five or More 
* Hitori 
* Iagno (reversi) 
* Gnome Klotski  
* Gnome Mahjongg 
* Gnome Mines 
* Gnome Nibbles 
* Quadrapassel  
* Four in a row 
* Gnome Robots  
* Gnome Sudoku 
* Gnome Swell (swell-foop) 
* Tali 
* Gnome Taquin 
* Gnome Tetravex 
* Luces fuera (lightsoff) 


Para desinstalar los juegos:

```bash
sudo apt purge gnome-2048 aisleriot atomix gnome-chess five-or-more hitori iagno gnome-klotski gnome-mahjongg gnome-mines gnome-nibbles quadrapassel four-in-a-row gnome-robots gnome-sudoku gnome-swell-foop  tali gnome-taquin gnome-tetravex lightsoff

sudo apt autoremove -y
```

Con esto liberamos un poco el panel de aplicaciones y algo de espacio.

## 4. Instalar firmware Wifi (sólo Lenovo X260)

Los drivers para tarjeta Wifi no son de código abierto, por lo que Debian no la reconoce automáticamente. Hay que habilitar el repositorio non-free e instalarlos.

Primero habilitamos el repositorio. Editamos el arcivo sources.list:

```bash
sudo nano /etc/apt/sources.list
```

descomentamos (o agregamos) las siguientes lineas:

```bash
deb http://security.debian.org/debian-security bullseye-security main non-free
deb-src http://security.debian.org/debian-security bullseye-security main non-free
```

Por último instalamos el firmware para la tarjeta wifi:

```bash
sudo apt update
sudo apt install firmware-iwlwifi
```

## 5. Habilitar lector huellas dactilares (sólo Lenovo X260)

El soporte de drivers es muy bueno para el Lenovo X260 (ver [wiki Gentoo](https://wiki.gentoo.org/wiki/Lenovo_ThinkPad_X260)) pero para que Debian reconozca el lector de huellas tenemos que instalar la libreria [libprint](https://github.com/freedesktop/libfprint). Los paquetes para Debian por suerte ya estan disponibles y para ello solo debemos instalar los siguientes paquetes:

```bash
sudo apt install libfprint-2-2 fprintd libpam-fprintd 
```
* libfprint-2-2: libreria para el proyecto fprint 
* fprintd Demonio para el lector de huellas dactilares. Este paquete nos permite ir a Configuración -> Usuarios y ver la opción "Inicio de sesión con huella".
* libpam-fprintd Permite la autenticación mediante huella en el inicio de sesión.

Después de agregar nuestra huella y reiniciar sesión, ya podremos iniciar sesión con la huella. Si queremos que el comando sudo también nos reconozca la huella, debemos añadir la siguiente linea al siguiente archivo de configuración PAM.

```bash
sudo nano /etc/pam.d/sudo

auth required pam_fprintd.so
#@include common-auth
```
NOTA: si no comentamos la segunda linea, nos pedida la huella y además el password de usuario.

## 6. Instalar programa retoques (gnome-tweak-tools)

Debian 11
```bash
sudo apt install gnome-tweak-tools
```

Debian 12.5
```bash
sudo apt install gnome-tweaks
```

Hay bastantes ajustes interesantes que podemos llevar a cabo con esta herramienta, pero estos son algunos de los que tengo configurados:

* Barra superior -> Porcentaje de la batería (activar)
* Barra superior -> Fecha
* Barras de título de las ventanas -> Maximizar
* Barras de título de las ventanas -> Minimizar
* Barras de título de las ventanas -> Colocación derecha
* Extensiones - Habilitar


## 7. Instalar gnome-extensions

Ir a https://extensions.gnome.org mediante el navegador Firefox e instalar extensión en en el navegador. Hay muchas extensiones, pero no tantas útiles. Habilitar las siguientes extensiones:

* [Dash to dock](https://extensions.gnome.org/extension/307/dash-to-dock/). Por defecto el dash (barra lateral que aparece al pulsar sobre Actividades) no se mantiene en pantalla, al estilo Ubuntu. Para dejarlo fijo puedes instalar esta extensión o Dash to panel para un look más parecido a Windows/Mac.

* [Applications Menu](https://extensions.gnome.org/extension/6/applications-menu/). Añade un menú en la barra superior del escritorio con todos los programas ordenados por categorías.

* [Places Status Indicator](https://extensions.gnome.org/extension/8/places-status-indicator/). Añade un menú en la barra superior del escritorio con accesos a las areas más importantes del equipo (Home, Escritorio, Musica, Redes, etc.)

* [GS Connect](https://extensions.gnome.org/extension/1319/gsconnect/). Permite integrar el móvil y el escritorio de una forma rápida. Debemos instalarnos la aplicacion [KDE Connect](https://play.google.com/store/apps/details?id=org.kde.kdeconnect_tp) pero me parece una de las más útiles. Enviar archivos desde/hacia el móvil, ver las llamadas y mensajes de texto, etc.

* [WinTile](https://extensions.gnome.org/extension/1723/wintile-windows-10-window-tiling-for-gnome/). Permite ajustar las ventanas en cada una de las mitades del escritorio. Muy útil para tener dos ventanas a la vista y es una funcionalidad de Windows que siempre echaba de menos. 

[Top 20 Gnome Extensions](https://itsfoss.com/best-gnome-extensions/)

## 8. Ajustes básicos

Dentro de ajustes Ir a los siguientes ajustes: 

### 8.1 Activar el modo noche

Dentro de ajustes Ir a pantallas -> Luz noctura -> Luz nocturna. 

Podemos mantener los ajustes estandar para que la luz nocturna se active desde el atardecer hasta el amanecer.

### 8.2 Mostrar porcentaje bateria

Dentro de ajustes Ir a Energía -> Mostrar porcentaje batería.

### 8.3 Cambiar fondo de pantalla

Fondo

## 9. Instalar tlp (sólo para portátiles)

Tlp permite optimizar el uso de bateria en los portátiles. Para instalarlo.

```bash
sudo apt install tlp tlp-rdw
```

El paquete tlp-rdw también está recomendado pues permite a TLP encender/apagar los dispositivos Wifi, Bluetooth y WWAN (Wireless Wan).

La documentación es muy completa y se puede consultar en [TLP - Optimize Linux Laptop](https://linrunner.de/tlp/index.html)

NOTA para X260. Al suspender el equipo no es posible restaurarlo de nuevo. Para ello tenemos dos opciones: 

* Deshabilitar la opción en la BIOS del sistema. Para ello debemos ir al menu --> Security Chip y establecer en Disable.

* Agregar la opción "intel_iommu=off" a los parámetros de GRUB [Reddit](https://www.reddit.com/r/thinkpad/comments/73i20g/x260_with_archi3wmtlp_will_not_wake_from_suspend/)

## 10. Eliminar tiempo de espera GRUB

Al iniciar Debian, nos aparece el menú de GRUB para indicar el sistema operativo a arrancar. Si solo tenemos Linux, podemos agilizar un poco el tiempo de carga y eliminar esta espera. 

Para ello, editamos el siguiente archivo:

```bash
sudo nano /etc/default/grub
```
y Modificamos el parámetro GRUB_TIMEOUT

```bash
GRUB_TIMEOUT=0
```

Si queremos acceder nuevamente al menú de GRUB, podemos pulsar la tecla SHIFT durante el inicio.

## 11. Instalar y configurar un sistema de backup

Si queremos que no perder nuestros datos o alguna de las configuraciones que hemos hecho, tendremos que instalar un programa de backup. Para Linux hay distintos paquetes que nos permiten automatizar dicha tarea. Entre los software gráficos más importantes tenemos [Timeshift](https://github.com/teejee2008/timeshift), uno de los más utilizados. Otros también populares son [Grsync](http://www.opbyte.it/grsync/) o [luckyBackup](https://luckybackup.sourceforge.net/). Casi todos están basados en la herramienta de línea de comandos [rsync](https://rsync.samba.org/), que es la herramienta que vamos a utilizar. Antes de instalar la herramienta, debemos preguntarnos ¿Que respaldar? ¿Cada cuando? ¿En que ubicación? ¿En que medios de almacenamiento?. Algunas consideraciones:

* Podemos respaldar todo el sistema completo o solo los datos de usuario. Restaurar todo el sistema completo es más complicado que hacer una instalación desde cero y normalmente solo necesitaremos hacer una copia de seguridad de nuestros datos personales (directorio /home) y alguna configuración del software (/etc/). 

* Lo normal es hacer una copia diaria de todos nuestros datos. Alguna de estas copias la podemos guardar de forma periódica en un disco externo. 

* En cuanto a medios de almacenamiento y numero de copias, en general no debemos volvernos locos. La mayor parte de la gente respalda sus datos mediante una copia en la nube. Para linux principalmente tenemos dos opciones para hacer un backup en la nube: [insync](https://www.insynchq.com/) (de pago) o [Rclone](https://rclone.org/) (gratuito). Sin embargo, aparte de guardar los datos en la nube, es recomendable tener nuestros datos en un disco duro aparte (disco USB, NAS, etc...). Así que primero crearemos un script que respalde los datos de usuario y los guarde en /var/backups.

Crearemos el siguiente script rsync-backup.sh en un directorio dentro de nuestra carpeta personal.

```bash
    #!/bin/sh

    # Simple rsync backup of Linux user data

    # 1. setup 1st time
    # mkdir ~/Documentos/rsync && cd !$
    # nano rsync-backup.sh
    # sudo mkdir /var/backups/rsync
    # nano exclude-file.txt

    # 2. add exclusions
    # https://sites.google.com/site/rsync2u/home/rsync-tutorial/the-exclude-from-option
    # https://github.com/rubo77/rsync-homedir-excludes/blob/master/rsync-homedir-excludes.txt
    #.mozilla
    #.cache
    #.local

    sudo rsync -av --exclude-from=/home/salva/Documentos/rsync/exclude-file.txt \
    /home/salva /etc /var/backups/rsync/ --log-file=rsync.log
```



## 12. Instalar software básico

Para instalar software adicional en nuestro equipo disponemos de varias opciones en Debian.

* Desde los repositorios de Debian (apt install o herramienta gráfica).
* Desde un paquete Debian .deb (dpkg -i).
* Mediante sistemas independientes como Snap, Flatpak o Appimage.

Estos tres últimos tienen defensores y detractores cada uno, aquí tenemos una [comparativa](https://github.com/AppImage/AppImageKit/wiki/Similar-projects#comparison).

### 12.1. Habilitar soporte Flatpak o Snap

```bash
sudo apt install flatpak
sudo apt install gnome-software-plugin-flatpak 
flatpak remote-add --if-not-exists flathub https://flathub.org/repo/flathub.flatpakrepo
```

### 12.2. Aplicaciones varias.


|Aplicacion |Como instalar|
|-----------|-------------|
|Virtualbox |
|VLC        | sudo apt install vlc |
|Telegram   |             |
|Spotify    |             |
|Visual Studio |         |
