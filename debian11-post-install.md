# Lista de tareas de después de la instalación de Debian11 en X260

Después de instalar Debian 11, version netinst [Debian 11 netinst](https://cdimage.debian.org/debian-cd/current/amd64/iso-cd/debian-11.6.0-amd64-netinst.iso) desde [Obtener Debian](https://www.debian.org/distrib/index.es.html), éstas son las tareas que debemos hacer para tener un sistema funcional y preparado para instalar cualquier tipo de sofware.

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

## 3. Instalar firmware Wifi (sólo Lenovo X260)

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

## 4. Habilitar lector huellas dactilares (sólo Lenovo X260)

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

## 5. Desinstalar juegos preinstalados

Debian 11 viene por defecto con un montón de juegos (19) preinstalados. ¿Porque Debian (o mejor dicho Gnome) viene con tantos juegos preinstalados? Quien sabe, pero yo prefiero desinstalarlos todos y luego instalar aquel que vaya a utilizar. Los juegos que se van a desinstalar son los siguientes:

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

## 6. Instalar programa retoques (gnome-tweak-tools)

```bash
sudo apt install gnome-tweak-tools
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

## 8. Ajustes 

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

## 11. Instalar sowftware básico

### 11.1. Habilitar soporte Flatpak o Snap

sudo apt install flatpak
sudo apt install gnome-software-plugin-flatpak 
flatpak remote-add --if-not-exists flathub https://flathub.org/repo/flathub.flatpakrepo

### 11.2. Aplicaciones varias.
Virtualbox
VLC
Telegram
Spotify 
Visual Studio
