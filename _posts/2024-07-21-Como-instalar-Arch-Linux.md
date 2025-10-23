---
title: Como instalar Arch Linux
description: Esta guía ha sido creada con el propósito de facilitar la instalación de Arch Linux. Casi toda la información recopilada en esta guía a sido obtenida de la wiki oficial de Arch Linux.
date: 2024-07-21 19:28:00 +0200
categories: [Linux]
tags: [Linux, Arch Linux, Avanzado]
pin: true
mermaid: true
image:
  path: /assets/img/posts/archbtw.png
  alt: Imagen creada por el usuario xyproto (Alexander F. Rødseth) bajo la licencia CC0 "No Rights Reserved" (https://bbs.Archlinux.org/viewtopic.php?id=259604)
---

## Índice
0. [Introducción](#Introducción)
1. [Preinstalación](#Preinstalación)
    1. [Definir la distribución del teclado](#Definir-la-distribución-del-teclado)
    2. [Verificar la modalidad de arranque (BIOS, UEFI)](#Verificar-la-modalidad-de-arranque-BIOS-UEFI)
    3. [Conectarse a Internet](#Conectarse-a-Internet)
    4. [Sincronizar el reloj del sistema](#Sincronizar-el-reloj-del-sistema)
    5. [Particionar el disco](#Particionar-el-disco)
    6. [Montar las particiones](#Montar-las-particiones)
2. [Instalación](#Instalación)
3. [Configuración básica del sistema](#Configuración-básica-del-sistema)
	1. [Generamos el Archivo fstab](#Generamos-el-Archivo-fstab)
	2. [Chroot](#Chroot)
	3. [Zona horaria](#Zona-horaria)
	4. [Idioma del sistema](#Idioma-del-sistema)
	5. [Configurar la red](#Configurar-la-red)
	6. [Contraseña de root](#Contraseña-de-root)
	7. [Instalar el gestor de arranque](#Instalar-el-gestor-de-arranque)
	8. [Crear un usuario](#Crear-un-usuario)
	9. [Conectarse a Internet](#Conectarse-a-Internet)
	10. [Reiniciar](#Reiniciar)
4. [Instalar los repositorios](#Instalar-los-repositorios)
    1. [AUR (Arch User Repository)](#AUR-Arch-User-Repository)
        1. [Yay](#Yay)
        2. [Paru](#Paru)
    2. [Instalar Flatpak](#Instalar-Flatpak)
    3. [Instalar los repositorios de BlackArch](#Instalar-los-repositorios-de-BlackArch)
5. [Instalar o crear un entorno de escritorio](#Instalar-o-crear-un-entorno-de-escritorio)
    1. [Instalar KDE](#Instalar-KDE)
    2. [Instalar Gnome](#Instalar-Gnome)
6. [Fuentes](#Fuentes)

## Introducción {#Introducción}

Esta guía ha sido creada con el propósito de facilitar la instalación de Arch Linux. Casi toda la información recopilada en esta guía a sido obtenida de la wiki oficial de Arch Linux. Aunque no es habitual, es posible que a la fecha en que este leyendo esta guía, algunos pasos del método de instalación hayan cambiado, por ello también recomiendo revisar las fuentes oficiales para obtener información mas actualizada o detallada. Podéis encontrar todas las fuentes haciendo clic [aquí](#Fuentes) o al final de esta guía.

## 1. Preinstalación {#Preinstalación}
### 1.1. Definir la distribución del teclado {#Definir-la-distribución-del-teclado}

La ISO de instalación de Arch Linux viene por defecto con la distribución del teclado en inglés, por lo que para cambiarlo a español deberemos utilizar el siguiente comando:

```bash
loadkeys es
```

### 1.2. Verificar la modalidad de arranque (BIOS, UEFI) {#Verificar-la-modalidad-de-arranque-BIOS-UEFI}

Para comprobar el modo de arranque, listamos el directorio efivars:

```bash
ls /sys/firmware/efi/efivars
```

Si la orden muestra el directorio sin errores, el sistema se iniciará en modo UEFI. Si no existe el directorio, el sistema se iniciará en modo BIOS o en modalidad CSM (Compatibility Support Module).

### 1. 3. Conectarse a Internet {#Conectarse-a-Internet}

Para poder instalar Arch necesitamos conexión a Internet. Esto podemos hacerlo de dos formas, conectando nuestro pc por cable o por wifi. Conectarnos a Internet por cable es la manera más rápida y sencilla, pero si esto no es posible, veremos como podemos conectarnos por wifi. Para ello utilizaremos el programa `iwd` (iNet Wireless Daemon).

1. Para ejecutar el programa y empezar a utilizar sus comandos escribiremos:

    ```bash
iwctl
```

2. Para listar todos los dispositivos wifi:

    ```bash
device list
```

3. Si nuestros dispositivo o adaptador están apagados, podemos encenderlos con uno de los siguientes comandos:

    ```bash
device "nombre de la red" set-property Powered on
adapter "nombre del adaptador" set-property Powered on
```

4. Para buscar las redes disponibles: 

    ```bash
station "nombre del adaptador" scan
```

Este comando no mostrará nada, ya que solo inicia el proceso de escaneo en segundo plano.

5. Para ver la lista de todas las redes encontradas:

    ```bash
station "nombre del adaptador" get-networks
```

6. Por último, para conectarnos a una red ejecutaremos el siguiente comando e introduciremos la contraseña de la red:

    ```bash
station "nombre del adaptador" connect "SSID o nombre de la red"
```

7. Para comprobar que tenemos Internet, salimos del prompt de iwd con el comando `exit` y hacemos un ping a una dirección ip o dominio. Esto nos indicará si tenemos Internet mostrándonos la latencia (tiempo) de ida y vuelta de los paquetes de datos entre nuestro equipo y el servidor. Por ejemplo:

    ```bash
ping Archlinux.org
```
		
    Nos mostrará algo así:

    ```bash
PING Archlinux.org (95.217.163.246) 56(84) bytes of data.
64 bytes from Archlinux.org (95.217.163.246): icmp_seq=1 ttl=51 time=55.2 ms
64 bytes from Archlinux.org (95.217.163.246): icmp_seq=2 ttl=51 time=65.7 ms
64 bytes from Archlinux.org (95.217.163.246): icmp_seq=3 ttl=51 time=187 ms
64 bytes from archlinux.org (95.217.163.246): icmp_seq=4 ttl=51 time=57.3 ms
64 bytes from archlinux.org (95.217.163.246): icmp_seq=5 ttl=51 time=56.7 ms
^C
--- archlinux.org ping statistics ---
5 packets transmitted, 5 received, 0% packet loss, time 4006ms
rtt min/avg/max/mdev = 56.280/57.345/58.584/0.823 ms
```
Como podemos ver, la salida nos muestra que tenemos Internet.

### 1. 4. Sincronizar el reloj del sistema {#Sincronizar-el-reloj-del-sistema}

Ahora que tenemos Internet, podemos sincronizar el reloj del sistema con el siguiente comando:

```bash
timedatectl set-ntp true
```

### 1. 5. Particionar el disco {#Particionar-el-disco}

1. Para crear las particiones podemos usar las herramientas `fdisk` o `cfdisk`. Yo recomiendo `cfdisk` puesto que tiene una interfaz más fácil de usar. 

	Al ejecutar cfdisk para crear las particiones saldrá un menú preguntando el tipo de tabla de particiones. Si estáis en máquina virtual deberéis seleccionar DOS (MBR o Master Boot Record). Si estáis en máquina real y vuestro pc utiliza BIOS, también deberéis seleccionar DOS y si utiliza UEFI deberéis seleccionar GPT (GUID Partition Table).

	Si os habéis equivocado al seleccionar la tabla de particiones, podéis cambiarla utilizando la herramienta `parted`, si no podéis saltaros este paso. 
	
	**Para cambiar de GPT a DOS (MBR):**

    Seleccionamos el disco en el que queremos trabajar:

    ```bash
sudo parted /dev/sdX
```

    Cambiamos la tabla de particiones:

    ```bash
(parted) mklabel msdos
```
    Salimos del programa:

    ```bash
(parted) quit
```
		
   **Para cambiar de DOS (MBR) a GPT:**
		
	Seleccionamos el disco en el que queremos trabajar:

    ```bash
sudo parted /dev/sda
```

    Cambiamos la tabla de particiones:

    ```bash
(parted) mklabel gpt
```
    Salimos del programa:

    ```bash
(parted) quit
```


	Deberéis crear las particiones que consideréis necesarias, sin embargo lo mas habitual es crear tres si tenéis BIOS, o cuatro si tenéis UEFI. 
	
	1. Una partición para el sistema (directorio raíz `/`).
	2. Otra partición para el directorio personal del usuario (`/home`).
	3. Otra partición para el `swap` o área de intercambio.
	
		La partición swap es un espacio reservado en el disco duro que utiliza el sistema como memoria virtual cuando se queda sin espacio suficiente en la memoria RAM. 
			
		No existe un tamaño predefinido para esta partición, pero lo mas habitual suele ser asignarle mínimo la misma cantidad o el doble que de memoria RAM en caso de que esta sea muy pequeña, como las de 2GB o 4GB. O asignarle la misma cantidad o la mitad que de memoria RAM en caso de que esta sea mas grande, como las de 8GB o 16GB. Sin embargo si  la memoria es muy grande, como las 64GB, no tiene sentido asignarle 32GB al swap, ya que es demasiado grande y todo ese espacio no se usará  y lo estaremos desperdiciando, por lo que en este sentido el máximo sería de 16GB.

		Al crear esta partición en cfdisk, deberéis indicarle que es de tipo `Linux Swap`. Al resto de particiones no hay que asignarle nada.

	4. Partición `efi`. En caso de que tengáis un ordenador con UEFI, también deberéis crear esta partición. Esta debe tener mínimo 300MB. Aquí es donde se almacenan los cargadores de arranque EFI y las aplicaciones y controladores que utiliza el firmware UEFI durante el arranque.

2. Para listar las particiones que hemos creado:

    ```bash
lsblk
```

3. Formateamos las particiones con el sistema de Archivos correspondiente. En este caso, para las particiones raiz `/` y `/home` utilizaremos el formato ext4, para la partición del swap utilizaremos el formato swap y para la partición efi, utilizaremos FAT32:

    ```bash
mkfs.ext4 /dev/"partición raiz, por ejemplo sda1"
mkfs.ext4 /dev/"partición para home, por ejemplo sda2"
mkswap /dev/"partición swap"
mkfs.fat -F 32 /dev/"partición efi, por ejemplo sda3"
```

4. Para activar la partición swap o área de intercambio:

    ```bash
swapon /dev/"nombre de la partición swap"
```

### 1. 6. Montar las particiones {#Montar-las-particiones}

1. La partición raíz la montamos en /mnt:

    ```bash
mount /dev/"partición_raiz" /mnt
```

2. La partición home la montamos dentro de /mnt/home. Puesto que no existe este directorio, tendremos que crearlo:

    ```bash
mount --mkdir /dev/"partición_home" /mnt/home
```

3. Por último, si disponemos de parción efi, la montamos en /mnt/boot:

    ```bash
mount --mkdir /dev/"partición_efi" /mnt/boot
```

### 2. Instalación {#Instalación}

Ahora ya estamos listos para instalar los paquetes esenciales de Arch en el directorio donde hemos montado el sistema, en `/mnt`. Para ello utilizamos el script pacstrap para instalar el paquete base, un Kernel de Linux y un firmware para hardware común:

```bash
pacstrap -K /mnt base linux linux-firmware
```

## 3. Configuración básica del sistema {#Configuración-básica-del-sistema}
### 3.1. Generamos el Archivo fstab {#Generamos-el-Archivo-fstab}

Fstab o "File System Table", es un Archivo de configuración en sistemas operativos basados en Unix como Linux, que especifica cómo y dónde se deben montar los sistemas de Archivos en el sistema durante el proceso de arranque. Contiene entradas que describen las particiones y dispositivos de almacenamiento que deben montarse, así como la ubicación donde se montarán y las opciones de montaje asociadas.

Generamos el  Archivo fstab:

```bash
genfstab -U /mnt >> /mnt/etc/fstab
```

Podemos comprobar que el Archivo se ha generado correctamente:

```bash
cat /mnt/etc/fstab
```

### 3.2 Chroot {#Chroot}

Cambiamos la raíz al nuevo sistema:

```bash
Arch-chroot /mnt
```

### 3.3. Zona horaria {#Zona-horaria}

Definimos nuestra zona horaria:

```bash
ln -sf /usr/share/zoneinfo/"región"/"ciudad" /etc/localtime
```

Generamos el Archivo /etc/adjtime:

```bash
hwclock --systohc
```

### 3.4. Idioma del sistema {#Idioma-del-sistema}

1. Accedemos a `/etc/locale.gen`  y descomentamos el locale correspondiente, por ejemplo en el caso de España sería `es_ES.UTF-8 UTF-8`. Además, también debemos descomentar el de `en_US.UTF-8 UTF-8`. Para ello necesitaremos instalar un editor de textos de terminal como vim o nano. Luego generamos los locales con el siguiente comando:

    ```bash
locale-gen
```

2. Creamos el Archivo `locale.conf` en `/etc` y definimos la variable LANG. En el caso de España:

    ```bash
LANG=es_ES.UTF-8
```

3. Definimos el idioma del teclado. Para ello creamos el Archivo `vconsole.conf` en `/etc` y escribimos dentro de el `KEYMAP=es`.

### 3.5. Configurar la red {#Configurar-la-red}

1. Creamos el Archivo `/etc/hostname`  y en el escribimos el nombre del equipo.

2. Editamos el Archivo `/etc/hosts` y escribimos lo siguiente:

    ```bash
127.0.0.1    localhost
::1          localhost
127.0.1.1    "nombredehost".localhost "nombredehost"
```

### 3.6. Contraseña de root {#Contraseña-de-root}

Para establecer una contraseña al usuario `root` ejecutamos el siguiente comando:

```bash
passwd
```

### 3.7. Instalar el gestor de arranque {#Instalar-el-gestor-de-arranque}

En Linux el gestor de arranque es el grub. Este debe instalarse de dos formas dependiendo de si tu pc es BIOS o UEFI. 

1. Para instalarlo y configurarlo en BIOS:

    ```bash
    pacman -S grub
    grub-install /dev/"disco, por ejemplo sda"
    ```

	Utilizamos la herramienta `grub-mkconfig` para generar `/boot/grub/grub.cfg`:
	
    ```bash
	grub-mkconfig -o /boot/grub/grub.cfg
    ```

2. Para instalarlo y configurarlo en UEFI:

    ```bash
    pacman -S grub efibootmgr
    grub-install --target=x86_64-efi --efidirectory=/boot
    ```

	Utilizamos la herramienta `grub-mkconfig` para generar `/boot/grub/grub.cfg`:

    ```bash
    grub-mkconfig -o /boot/grub/grub.cfg
    ```

3. Comprobar si hay otros sistemas operativos:

	Para que `grub-mkconfig` busque otros sistemas instalados y los agregue automáticamente al menú de arranque, debemos instalar el paquete `os-prober` y ejecutarlo. Luego deberemos volver a generar el Archivo `grub.cfg`:

    ```bash
    pacman -S os-prober
    os-prober
    grub-mkconfig -o /boot/grub/grub.cfg
    ```

### 3.8. Crear un usuario {#Crear-un-usuario}

1. Creamos nuestro usuario:

    ```bash
	useradd -m "usuario"
    ```

2. Ponemos contraseña a nuestro usuario:

    ```bash
    passwd "usuario"
    ```

3. Añadimos nuestro usuario a los grupos:

    ```bash
    usermod -aG wheel,video,audio,storage "usuario"
    ```

4. Instalamos `sudo` y descomentamos la línea `%wheel ALL=(ALL:ALL) ALL` en el fichero `/etc/sudoers`.

### 3.9. Conectarse a Internet {#Conectarse-a-Internet}

Por último, antes de reiniciar y arrancar por primera vez el sistema, debemos instalar `networkmanager` y habilitarlo para tener Internet:

```bash
pacman -S networkmanger
systemctl enable NetworkManager
```

Si ya has reiniciado el sistema y no has completado este paso, no tendrás Internet. Para solucionarlo, basta con iniciar nuevamente desde el usb booteable o desde la ISO en máquina virtual y volver a montar las particiones y acceder a ellas con `Arch-chroot` como vimos en los pasos anteriores. Una vez hecho esto, ya podremos instalar y habitlitar NetworkManager.
### 3.10. Reiniciar {#Reiniciar}

Para comprobar que el grub se ha instalado correctamente e iniciar por primera vez el sistema:

1. Salimos del entorno chroot:

    ```bash
    exit
    ```

2. Desmontamos las particiones:

    ```bash
    umount -R /mnt
    ```

3. Reiniciamos el sistema y desconectamos el usb booteable si lo estamos instalando en máquina real, o la ISO si estamos lo instalando en máquina virtual:

    ```bash
    reboot
    ```

### 4. Instalar los repositorios {#Instalar-los-repositorios}

#### 4.1. AUR (Arch User Repository) {#AUR-Arch-User-Repository}

AUR (Arch User Repository) es un repositorio mantenido por la comunidad de usuarios de Arch Linux, el cual es usado tanto en Arch como en distribuciones derivadas, como Manjaro, ArcoLinux,  BlackArch, EndeavourOS o Garuda Linux entre otros. Para instalar paquetes de AUR es necesario instalar algún gestor de paquetes compatible, también conocidos como helpers, puesto que pacman solo funciona con los repositorios oficiales. Existen muchos gestores de paquetes para AUR, como yay, paru, trizen, pakaur, etc. Como es lógico, no es necesario instalarlos todos, basta con tener uno. En este caso solo vamos a ver como instalar los dos principales, yay y paru.

#### Yay {#Yay}

1. Instalamos los paquetes necesarios:

    ```bash
    pacman -S --needed git base-devel
    ```

2. Clonamos el repositorio:

    ```bash
    git clone https://aur.Archlinux.org/yay.git
    ```

3.  Accedemos a la carpeta del repositorio clonado, compilamos e instalamos el paquete:

    ```bash
    cd yay
    makepkg -si
    ```

#### Paru {#Paru}

1. Instalamos los paquetes necesarios:

    ```bash
    sudo pacman -S --needed base-devel
    ```

2. Clonamos el repositorio:

    ```bash
    git clone https://aur.Archlinux.org/paru.git
    ```

3.  Accedemos a la carpeta del repositorio clonado, compilamos e instalamos el paquete:

    ```bash
    cd paru
    makepkg -si
    ```

### 4.2. Instalar Flatpak {#Instalar-Flatpak}

Flatpak es una tecnología que permite empaquetar, distribuir e instalar softaware de manera global en cualquier distribución de Linux utilizada. Funciona como un gestor de paquetes global compatible con cualquier distribución de Linux, que permite instalar cualquier software empaquetado en formato Flatpak disponible en repositorios como Flathub, el mas usado y conocido. Las aplicaciones Flatpak se ejecutan en un entorno aislado del resto del sistema (sandbox) y utilizan un sistema de permisos para acceder a los recursos del equipo necesarios para el correcto funcionamiento de las aplicaciones, lo que previene conflictos con otros programas y protege el sistema contra posibles amenazas de seguridad. Los permisos pueden gestionarse por línea de comandos, o de forma gráfica con la aplicación `flatseal`. No es obligatorio instalarlo, pero es una excelente opción para aquellos que deseen mayor seguridad y privacidad y disfrutar de un abanico mas amplio de aplicaciones.

Para instalar Flatpak, simplemente debemos ejecutar el siguiente comando:

```bash
sudo pacman -S flatpak
```

Esto nos instalará Flatpak y el repositorio de Flathub por defecto. Si no es así, podemos agregar Flathub manualmente con el siguiente comando:

```bash
flatpak remote-add --if-not-exists flathub https://dl.flathub.org/repo/flathub.flatpakrepo
```

### 4.3. Instalar los repositorios de BlackArch {#Instalar-los-repositorios-de-BlackArch}

Para aquellos que necesiten tener acceso a una gran variedad de herramientas de ciberseguridad, pueden instalar el respositorio de BlackArch.

BlackArch Linux es una distribución derivada de Arch Linux destinada a la ciberseguridad. Sin embargo, BlackArch contiene miles de herramientas de ciberseguridad de las cuales la mayoría no llegará a usar. De este modo, en lugar de instalar BlackArch, es posible instalar el repositorio de BlackArch en Arch Linux e instalar solo las herramientas que necesite.

1. Descargamos el script de configuración strap.sh del sitio web de BlackArch con curl:

    ```bash
    curl -O https://blackArch.org/strap.sh
    ```

2. Otorgamos permiso de ejecución al script:

    ```bash
    chmod +x strap.sh
    ```

3. Ejecutamos el script:

    ```bash
    sudo ./strap.sh
    ```

### 5. Instalar o crear un entorno de escritorio {#Instalar-o-crear-un-entorno-de-escritorio}

Llegados a este punto, ya hemos instalado y realizado la configuración básica de Arch. Sin embargo, aún no contamos con una interfaz gráfica, ni con audio, ni con otras funcionalidades básicas para el uso normal de nuestro sistema. Para solucionar esto, debemos instalar un entorno de escritorio, que no es mas que un conjunto de programas como un servidor gráfico, un compositor de imágenes, un servidor de audio, un gestor de ventanas, un gestor de pantallas, una barra de tareas, un explorador de Archivos, un navegador web o un emulador de terminal, entre otras muchas herramientas básicas que nos permiten usar el sistema de forma habitual.

Para esto existen dos opciones, instalar un entorno de escritorio ya hecho y configurado, o crear el nuestro instalando y configurando todas las herramientas necesarias. Dado que crear un entorno de escritorio es un proceso más complejo y extenso de explicar, en este artículo nos centraremos únicamente en cómo instalar uno ya existente, y en un artículo futuro veremos cómo crear uno. Existen muchos entornos de escritorio, como Gnome, KDE, Cinnamon, xfce, Budgie, etc., pero explicarlos todos nos llevaría demasiado tiempo, por lo que únicamente vamos a centrarnos en los dos mas populares, KDE Plasma y Gnome, así que vamos a ver como instalarlos.


#### 5.1. Instalar KDE {#Instalar-KDE}

Antes de instalar KDE es necesario instalar el servidor gráfico `Xorg`, que es una implementación del sistema de ventanas `X11`:

```bash
sudo pacman -S xorg
```

Nos mostrará una lista de paquetes del grupo `xorg`, podemos elegir cuales queremos instalar o pulsar enter para instalarlos todos por omisión. Lo mas recomendado es instalarlos todos para no tener problemas.

Para instalar KDE, tenemos disponibles los siguientes paquetes:
- **plasma-meta:** Instala el entorno de escritorio KDE Plasma.
- **plasma-desktop:** Una instalación minimalista de KDE Plasma.
- **kde-applications-meta:** Instala el conjunto completo de aplicaciones de KDE.

Para instalar KDE, podemos instalar el metapaquete `plasma-meta` o el paquete `plasma-desktop` para una instalación más minimalista. Opcionalmente también podemos instalar el metapaquete `kde-applications-meta` para obtener el conjunto completo de aplicaciones KDE. Por ejemplo:

```bash
sudo pacman -S plasma-meta kde-applications-meta
```

De nuevo, al ejecutar este comando nos mostrará una lista de paquetes del grupo `plasma`, aquí podemos elegir los que queramos instalar o pulsar enter para instalarlos todos por omisión (opción recomendada).

Una vez instalado nuestro entorno de escritorio, ya solo nos queda habilitar el gestor de pantallas o display manager y reiniciar el ordenador para empezar a disfrutar de nuestra nueva instalación de Arch Linux con KDE. En KDE el gestor de pantallas por defecto es sddm:

```bash
sudo systemctl enable sddm.service
```

#### 5.2. Instalar Gnome {#Instalar-Gnome}

Para instalar Gnome, existen tres paquetes que debemos tener en cuenta: 
- **gnome:** Contiene el escritorio base de GNOME y un subconjunto de aplicaciones.
- **gnome-extra:** Contiene aplicaciones adicionales, como un cliente de correo, un conjunto de juegos, etc.
- **gnome-shell:** Es la interfaz de usuario básica de Gnome.

Para instalar Gnome tendremos que instalar los paquetes de `gnome` y `gnome-shell` y opcionalmente también podemos instalar el paquete `gnome-extra`.

```bash
sudo pacman -S gnome gnome-shell
```

Al ejecutar este comando, nos mostrará una lista de paquetes del grupo `gnome`, aquí podemos elegir los que queramos instalar o pulsar enter para instalarlos todos por omisión.

Una vez instalado nuestro entorno de escritorio, ya solo nos queda reiniciar el ordenador para empezar a disfrutar de nuestra nueva instalación de Arch Linux con Gnome.

### Fuentes {#Fuentes}

- Guía de instalación oficial en Español:

	[https://wiki.Archlinux.org/title/Installation_guide_(Espa%C3%B1ol)](https://wiki.Archlinux.org/title/Installation_guide_(Espa%C3%B1ol))

- Conectarse al Wifi:

	[https://wiki.Archlinux.org/title/Iwd#iwctl](https://wiki.Archlinux.org/title/Iwd#iwctl)

- Configuración de red:

	[https://wiki.Archlinux.org/title/Network_configuration_(Espa%C3%B1ol)](https://wiki.Archlinux.org/title/Network_configuration_(Espa%C3%B1ol))

- Instalar el grub:

	[https://wiki.Archlinux.org/title/GRUB_(Espa%C3%B1ol)](https://wiki.Archlinux.org/title/GRUB_(Espa%C3%B1ol))

	[https://wiki.Archlinux.org/title/Arch_boot_process_(Espa%C3%B1ol)#Gestor_de_arranque](https://wiki.Archlinux.org/title/Arch_boot_process_(Espa%C3%B1ol)#Gestor_de_arranque)

- AUR (Arch User Repository)
    - Yay:

        [https://github.com/Jguer/yay?tab=readme-ov-file](https://github.com/Jguer/yay?tab=readme-ov-file)

    - Paru:

        [https://github.com/Morganamilo/paru](https://github.com/Morganamilo/paru)

- Flatpak:

    [https://www.flatpak.org/setup/Arch](https://www.flatpak.org/setup/Arch)

    [https://wiki.Archlinux.org/title/Flatpak_(Espa%C3%B1ol)](https://wiki.Archlinux.org/title/Flatpak_(Espa%C3%B1ol))

- Repositorios BlackArch:

    [https://blackArch.org/downloads.html#mirror-list](https://blackArch.org/downloads.html#mirror-list)

- Instalar KDE:

	[https://wiki.Archlinux.org/title/KDE_(Espa%C3%B1ol)](https://wiki.Archlinux.org/title/KDE_(Espa%C3%B1ol))

- Instalar Gnome:

	[https://wiki.Archlinux.org/title/GNOME_(Espa%C3%B1ol)](https://wiki.Archlinux.org/title/GNOME_(Espa%C3%B1ol))
