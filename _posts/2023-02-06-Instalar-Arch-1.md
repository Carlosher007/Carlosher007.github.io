---
layout: single
title: Arch Linux - Instalación 1
excerpt: 'Como instalar Arch Linux y no morir en el intento'
date: 2022-02-11
classes: wide
header:
  teaser: /assets/images/2023-02-06-Instalar-Arch-1/wallpapper-arch.png
  teaser_home_page: true
  icon: /assets/images/2023-02-06-Instalar-Arch-1/icon-arch.png
categories:
  - Instalación de Arch Linux
tags:
  - Linux
  - Arch Linux
---.


## Instalacioón de Arch Linux 

Debes tener en cuenta que este tutorial supone que ya tienes la imagen ISO de arch y que ya estas en la consola preparado para instalar el sistema operativo. Con esto en cuenta vamos con los pasos.

### Colocar teclado en español

```
loadkeys es 
```

### Conectarse a una red wifi : Metodo 1

```
iwctl
device list
```

Este ultimo comando te saca las tarjetas de red inalambricas, donde debes tener en cuenta el *name_device* que generalm,ente es **wlan0**

```
station name_device get-networks
```

Saca las redes inalambricas existentes, ten en cuenta el *network_name* de tu red inalambrica

```
station name_device connect network_name 
Escribes la contraseña de la red
```

Luego estarias conectarlo para comprobarlo te sales con *exit* y ejecutas

```
ping archlinux.org
```

A lo que no debería aparecerte error.

### Conectarse a una red wifi : Metodo 2

Teniendo en cuenta como se llama el nombre de tu red, la contraseña de tu red y que wlan0 sea tu tarjeta de red inalambrica, escribes lo siguiente, teniendo en cuenta que si tu red tiene espacios debes escribirla dentro de comillas simples '...' o comillas dobles "..."

```
iwctl --passphrase CLAVE_DE_RED station wlan0 connect NOMBRE_DE_RED
```

Luego estarias conectarlo para comprobarlo y ejecutas

```
ping archlinux.org
```


### Sincronizar el reloj para la ISO

```
timedatectl set-ntp true
```

### Particiones

Escribes esto a lo cual te saldrá una "interfaz" para el particionado

```
cfdisk
```

Si te aparece **Select label type** eliges *gpt* si tienes UEFI, en cambio si tienes *BIOS* elige *dos*.

Si tienes varias particiones, eliminas todas. Pero **ojo**, ten en cuenta que sda# vas a eliminar, no vaya a ser que elimines el datos de un disco que no querias. Ahora bien, para eliminar te paras en la partición, te paras en ella , le das *DELETE* y ENTER.

Para crear una nueva particion, te paras en el *Free Space*, le das a *NEW* y te aparecerá el espacio que quieres darle en GB.

Particiones que haremos en este tutorial, teniendo en cuenta que tengas 256GB en tu disco duro o SSD:

- Partición del sistema operativo: 110G
- Partición del home: 137G
- Partición del swap: 8G
- Particion EFI: 1G

Una vez asignadas todas las particiones, te vas a la particion del *swap*, vas a *type* y eliges **Linux swap**. 

Vas a la particion de *EFI*, vas a *type* y eliges **EFIS System**

Le das a **Write**, escribes *yes*, das ENTER y luego a ** Quit**

### Formateando las particiones

Escribes esto para ver como quedaron las particiones:

```
lsblk
```

Luego debes tener muy en cuenta el *NAME* de las particiones que creaste, en este caso **sda1** es el sistema operativo, **sda2** es el home, **sda3** es el swap y **sda4** es la EFI.

Para formatear escribes:


```
mkfs.ext4 /dev/sda1
mkfs.ext4 /dev/sda2
mkswap /dev/sda3
swapon /dev/sda3
```

### Montar los sitemas de fichero

Teniendo en cuenta nuevamente que en este caso **sda1** es el sistema operativo, **sda2** es el home, **sda3** es el swap y **sda4** es la EFI vamos a seguir, ten en cuenta que puedes comprobar esto nuevamente escribiendo *cfdisk*.


```
mount /dev/sda1 /mnt
mkdir /mnt/home
mount /dev/sda2 /mnt/home
```

Ahora vamos a montar la partificion EFI

```
mkdir /mnt/boot
mount /dev/sda4 /mnt/boot
```

### Instalación

```
pacstrap /mnt base linux linux-firmware 
genfstab -U /mnt >> /mnt/etc/fstab
cat /mnt/etc/fstab
```

Con esto deberías ver las particiones realizadas, con el fin de comprobar que esten bien.

```
arch-chroot /mnt/
```

### Zona horaria

Para buscar que zona horaria es la tuya escribes 

```
ls /usr/share/zoneinfo/
```

Que en mi caso quedaría así:

```
ln -sf /usr/share/zoneinfo/America/Bogota /etc/localtime
hwclock --systohc
```

### Configurar Lenguaje 

```
pacman -S nano
nano /etc/locale.gen
```

Descomentas las lines que digan *#en_US.UTF-8 UTF-8* y *#es_ES.UTF-8 UTF8*. Luego Ctrl+O para guardar y Ctrl+X para salir.

```
locale-gen
echo "LANG=es_ES.UTF-8" > /etc/locale.conf
echo "KEYMAP=es" > /etc/vconsole.conf
```

### Configuar red

Ten en cuenta que puedes cambiar *asus* por lo que quieras

```
echo "asus" > /etc/hostname
nano /etc/hosts
```

Dentro, escribes lo siguiente sin borrar lo que ya esta:

```
127.0.0.1     localhost
::1           localhost
121.0.1.1     asus.localhost asus
```

### Contraseña al root

```
passwd
Escribes la contraseña super segura
```

### Network manager

```
pacman -S networkmanager
systemctl enable NetworkManager
```

### Configurar el grub

```
pacman -S grub efibootmgr 
grub-install --target=x86_64-efi --efi-directory=/boot
grub-mkconfig -o /boot/grub/grub.cfg
```

### Crear Usuario

Si pones *carlosHot* tu pc ira más ardiente, pero lo **puedes cambiar** claro.

```
useradd -m carlosHot
passwd carlosHot
Colocas una contraseña
usermod -aG wheel,video,audio,storage carlosHot 
pacman -S sudo 
nano /etc/sudoers
```

Ahi debe haber una linea que diga **# %wheel ALL=(ALL) ALL**, debajo de la lines **## Uncomment to allow memebers of group wheel to execute any command**, debes descomentarla (la primera que mencione).Guardas y sales.

Si haces `su carlosHot` y escribes `groups` te deben aparecer los grupos escritos anteriormente. Para salirte escribes `exit`.

Una vez estes en el root, debes salirte (despues de haberte salido del usuario si es que lo hiciste) esicribiendo `exit`. Con esto ya estaremos en la ISO.

### Pasos finales

```
umount -R /mnt
shutdown now
```

Cuando se apague, sacas el USB y luego prendes el pc, ahí te debe aparecer el GRUB y eliges *Arch Linux*.

Te debería aparecer algo como `asus login: _`, ahi escribes tu nombre de usuario y luego tu contraseña.

Nos contectamos nuevamente al internet:

```
nmcli device wifi list
nmcli device wifi connect NOMBRE_RED password CONTRASEÑA_RED
```

Para poder tener graficos:  

```
sudo pacman -S xorg
``` 

### Gestor de ventanas QTile

Comprobamos que no tengamos nada al darle *ls*. Si tenemos algo hacemos un *rm -r Directory/*.

Hacemos

```
sudo pacman -S curl
sudo pacman -S xorg-server
sudo pacman -S qtile lightdm
sudo pacman -S lightdm-gtk-greeter
```

Si te sales, error no harás nada más de esta sección, si te sale error es porque las mirrors no son suficientes para encontrar ese paquete y haras todo lo siguiente.

```
curl "https://www.archlinux.org/mirrorlist/?cuntry=all&protocol=http&protocolo=https&ip_version=4" -o mirror.txt
cat mirrors.txt
sudo cp mirrors.txt /etc/pacman.d/mirrorlist
sudo nano /etc/pacman.d/mirrorlist
```

Descomentas los servidores de *Worldwide*. Al igua que algunos de *Germany*, *Ireland*,  *United States*, *United Kingdom*, *Spain* y *Austria*. El de *Colombia* tambien y lo subes antes de *Worldwide*. Los otros los eliminas.  (Con Ctrl+K eliminas y con Ctrl+U pegas si lo necesitas). 

```
sudo pacman -S qtile lightdm
sudo pacman -S lightdm-gtk-greeter
```


### Siguiendo

```
sudo systemctl enable lightdm
```

Si sale error escribes `sudo rm /etc/systemd/system/display-manager.service` y lo vuelves a intentar. 

Si haces un `ls /usr/share/xsessions/` te deberia aparecer qtile.desktop.

Sigues con:

```bash
sudo pacman -S xterm
# sudo pacman -Syy
sudo pacman -S alacritty
sudo pacman -S firefox
```

Finalmente haces un `reboot`


### Iniciando Sesión en Qtile

Cuando inicies sesión te deberia aparecer una consola, si no, abre una. 


```
setxkbmap es
sudo pacman -S code
```

Estando en la carpeta `/home/carlosHot` escribimos `cd .config/` y luego `code qtile/`

Cambias el *xterm* de *[mod],"Return"* por *alacritty*

## Final

Espera la segunda parte de personalización, mientras puedes ver los archivos en:

[Configuracion 1](https://github.com/antoniosarosi/dotfiles)
[Configuracion 2](https://github.com/antoniosarosi/dotfiles/tree/83fb32e60921a879cfab717553f8f016e0145d2b)