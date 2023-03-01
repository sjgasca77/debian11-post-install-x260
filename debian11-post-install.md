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

## 3. Instalar firmware Wifi (sólo para Lenovo X260)

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

## 4. Desinstalar juegos preinstalados

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

## 5. Instalar programa retoques (gnome-tweak-tools)

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


## 6. Instalar gnome-extensions

Ir a https://extensions.gnome.org mediante el navegador Firefox e instalar extensión en en el navegador. Habilitar las siguientes extensiones:

Dash to dock

## 7. Instalar tlp


## 8. Eliminar tiempo de espera GRUB


## 9. Instalar sowftware básico

VLC
