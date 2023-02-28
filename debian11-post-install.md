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

## 3. Instalar firmware Wifi (obligatorio para Lenovo X260)

Los drivers para tarjeta Wifi no son de código abierto, por lo que debian no la reconoce automáticamente. Hay que habilitar el repositorio non-free e instalarlos.



## 4. Desinstalar juegos preinstalados



## 5. Instalar programa retoques (gnome-tweak-tools)



## 6. Instalar gnome-extensions

