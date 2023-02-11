---
layout: single
title: Personalizacion de Arch Linux - 1
excerpt: 'Como personalizar Arch Linux y no morir en el intento - 1'
date: 2023-02-08
classes: wide
header:
  teaser: /assets/images/2023-02-06-Instalar-Arch-1/wallpapper-arch.png
  teaser_home_page: true
  icon: /assets/images/2023-02-06-Instalar-Arch-1/icon-arch.png
categories:
  - Personalizacion de Arch Linux
tags:
  - Linux
  - Arch Linux
---

<!-- @format -->

# Introducción

Luego de ver [la primera parte](https://carlosher007.github.io/Instalar-Arch-1/#) en donde se explica como instalar Arch Linux, ahora vamos a ver como terminar de personalizarlo.

# Empezemos con la personalización

## Nota

Si se queda bloqueado puedes hacer `Ctrl + Alt + F2` y entrar en la terminal. Luego escribes `startx` y ya. `startx` es el comando que inicia el entorno gráfico.

Para actualizar: `sudio pacman -Syu` y luego `sudo pacman -Syyu` que sirve para actualizar los repositorios.

## Si deseas instalar todo el software de una vez

```bash
# Basic utilities
sudo pacman -S networkmanager network-manager-applet pulseaudio pavucontrol pamixer brightnessctl xinit libnotify notification-daemon udiskie ntfs-3g arandr cbatticon volumeicon glib2 gvfs

# Fonts, theming and gtk
sudo pacman -S picom 
sudo pacman -S ttf-ubuntu-font-family ttf-roboto ttf-roboto-mono ttf-font-awesome ttf-hack ttf-inconsolata ttf-liberation ttf-opensans ttf-roboto ttf-roboto-mono ttf-ubuntu-font-family
#Material Black : https://www.gnome-look.org/p/1316887/
sudo pacman -S lxappearance
sudo pacman -S nitrogen
sudo pacman -S feh

# Apps
sudo pacman -S alacritty
sudo pacman -S thunar thunar-archive-plugin thunar-media-tags-plugin thunar-volman
# thunar-archive-plugin: Permite extraer archivos de un archivo comprimido
# thunar-media-tags-plugin: Permite editar las etiquetas de los archivos de audio y video
# thunar-volman: Permite montar y desmontar dispositivos de almacenamiento
sudo pacman -S neovim
sudo pacman -S git
sudo pacman -S rofi
sudo pacman -S scrot
sudo pacman -S redshift
sudo pacman -S trayer

```

## Si tienes el error de los mirros

Vas a [Mirror](https://archlinux.org/mirrorlist/) y le das a generate. Luego abres una consola y escribes `sudo code /etc/pacman.d/mirrorlist`. Buscas los de tu pais y los colocas, luego de United States, Canada, United Kingdom (2), Irland y Wordwide. Cierras la ventana y ya.

## Menu

```bash
sudo pacman -S rofi
```

En el config.py colocas al final de la lista de keys

```python
Key([mod], "m", lazy.spawn("rofi -show drun")),
Key([mod, "shift"], "m", lazy.spawn("rofi -show")),
```

Luego escribes en bash

```bash
sudo pacman -S sed
sudo pacman -S which
Cierras y abres la terminal
rofi-theme-selector
```

Eliges: android_notificaction by Rasi.

## Instalación Software

```bash
sudo pacman -S feh
```

Buscas algun fondo de pantalla que y lo descargas

```bash
feh --bg-scale ruta.png
```

## Audio y brillo

```bash
sudo pacman -S pulseaudio
sudo pacman -S pavucontrol
sudo pacman -S brightnessctl  
```

Escribes pulseaudio en bash o lo abres en el rofi, con eso ya deberías tener audio, compruebalo. Con **pavucontrol** puedes controlar el volumen.

Para **desprender un programa, en este caso pulseaudio de la terminal lo haces asi**

```bash
pulseaudio &
```

En las keys pegas al final esto:

```python
#Volume
Key([], "XF86AudioLowerVolume", lazy.spawn(
"pactl set-sink-volume @DEFAULT_SINK@ -5%"
)),
Key([], "XF86AudioRaiseVolume", lazy.spawn(
"pactl set-sink-volume @DEFAULT_SINK@ +5%"
)),
Key([], "XF86AudioMute", lazy.spawn(
"pactl set-sink-mute @DEFAULT_SINK@ toggle"
)),

# Brightness
Key([], "XF86MonBrightnessUp", lazy.spawn("brightnessctl set +10%")),
Key([], "XF86MonBrightnessDown", lazy.spawn("brightnessctl set 10%-")),
```

Eliminas esto en config.py : *Lo de key mod space lazy.layout.next*, *mod, shift space lazy.layout.ratate*, *lo de toggle_split*, *mod, i lazy.spawncmd*.

Y modificas lo de *lazy.layiout.suffle do wn y up*, en vez de control pones shift. Ten en cuenta que j es down y k es up.

## Para mejor experiencia desde la terminal con el audio

```bash
sudo pacman -S pamixer
```

Ahora puedes escribeir pulsemixer y encontrar el volumen, mute y demas.

Y en las keys colocas

```python
# Volumen
Key([], "XF86AudioLowerVolume", lazy.spawn("pamixer --decrease 5")),
Key([], "XF86AudioRaiseVolume", lazy.spawn("pamixer --increase 5")),
Key([], "XF86AudioMute", lazy.spawn("pamixer --toggle-mute")),
```


## Sesion

### Primera forma

Como he mencionado antes, estos cambios no son permanentes. Para que lo sean necesitamos un par de cosas. Primero instala xinit:

```bash
sudo pacman -S xorg-xinit
sudo pacman -S nitrogen
sudo pacman -S network-manager-applet
sudo pacman -S cbatticon
```

Ahora puedes usar ~/.xprofile para lanzar programas antes de que se ejecute el gestor de ventanas:

```bash
touch ~/.xprofile
```

Pegas lo siguiente, comentando lo que no hayas hecho aún

```bash
# Env vars
export PATH=$HOME/.local/bin:$PATH
export _JAVA_AWT_WM_NONREPARENTING=1
export QT_STYLE_OVERRIDE=kvantum 

# Screens
hdmi=`xrandr | grep ' connected' | grep 'HDMI' | awk '{print $1}'`

if [ "$hdmi" = "HDMI-1" ]; then
  xrandr --output eDP-1 --primary --mode 1366x768 --pos 276x1080 --output HDMI-1 --mode 1920x1080 --pos 0x0 &
else
  xrandr --output eDP-1 --primary --mode 1366x768 --pos 0x0 --rotate normal --output HDMI-1 --off --output DP-1 --off &
fi


#Audio
pulseaudio &
# Composer
picom &
# Network
nm-applet &
# Battery
cbatticon &
# Keyboard Layout
setxkbmap es &
# Automount Devices
udiskie -t &
# Java Fonts
xsettingsd &
# Wallpaper
nitrogen --restore &
# Wallpaper2
# feh --bg-scale Wallpapers/04.jpg &
# Overlay Bar
xob-pulse-py | xob -s pulse &
xob-brightness-js | xob -s brightness &
```

### Segunda forma

Abres una consola y escribes `touch .xsession`, luego escribes `sudo pacman -S xorg-xinit nmapplet`, `chmod u+x .xsession`, `rm .config/pulse/*` y lo abres con `code .xsession` y pegas esto:

```bash
#!/bin/sh

userresources=$HOME/.Xresources
usermodmap=$HOME/.Xmodmap
sysresources=/etc/X11/xinit/.Xresources
sysmodmap=/etc/X11/xinit/.Xmodmap

# merge in defaults and keymaps

if [ -f $sysresources ]; then
    xrdb -merge $sysresources
fi

if [ -f $sysmodmap ]; then
    xmodmap $sysmodmap
fi

if [ -f "$userresources" ]; then
    xrdb -merge "$userresources"
fi

if [ -f "$usermodmap" ]; then
    xmodmap "$usermodmap"
fi

# start some nice programs

if [ -d /etc/X11/xinit/xinitrc.d ] ; then
 for f in /etc/X11/xinit/xinitrc.d/?*.sh ; do
  [ -x "$f" ] && . "$f"
 done
 unset f
fi

##Teclado
setxkbmap es &
# Wallpaper
feh --bg-scale Wallpapers/04.jpg &
#Audio
pulseaudio &
# Composer
picom &

# Screens
hdmi=`xrandr | grep ' connected' | grep 'HDMI' | awk '{print $1}'`

if [ "$hdmi" = "HDMI-1" ]; then
  xrandr --output eDP-1 --primary --mode 1366x768 --pos 276x1080 --output HDMI-1 --mode 1920x1080 --pos 0x0 &
else
  xrandr --output eDP-1 --primary --mode 1366x768 --pos 0x0 --rotate normal --output HDMI-1 --off --output DP-1 --off &
fi

# Network
nm-applet &
# Keyboard Layout
setxkbmap es &
# Automount Devices
udiskie -t &
# Java Fonts
xsettingsd &

```

Comentas desde screen pues eos no lo tenemos aún. 

Este archivo sirve para que se ejecute al iniciar la sesión.  

## Fuentes

Instala estas fuentes:

```bash
sudo pacman -S ttf-dejavu ttf-liberation noto-fonts
fc-list
```

## Panel

En consola escribes

```bash
sudo pacman -S picom
```

Si no tienes config de alacritty:

```bash
cd .config/
mkdir alacritty
cd alacritty
touch alacritty.yml
```

Hables tu `.config/alacritty/alacritty.yml` y pegas:

```yml
background_opacity: 0.95
colors:
  bright:
    black: '0x282a40'
    blue: '0xa3c5ff'
    cyan: '0x98fffd'
    green: '0xe0ffad'
    magenta: '0xd6afed'
    red: '0xeb7f84'
    white: '0xd1e5ed'
    yellow: '0xffee7e'
  normal:
    black: '0x181a29'
    blue: '0x93bbff'
    cyan: '0x98e4ff'
    green: '0xcdea9f'
    magenta: '0xd3a7ee'
    red: '0xF07178'
    white: '0xbfd5de'
    yellow: '0xffd47e'
  primary:
    background: '0x0f101a'
    foreground: '0xc5c9de'
font:
  bold:
    family: UbuntuMono Nerd Font
  italic:
    family: UbuntuMono Nerd Font
  normal:
    family: UbuntuMono Nerd Font
    style: Regular
  size: 12.0
window:
  padding:
    x: 5
    y: 5
```

Ahora abres el ~/.config/qtile con code y selecciones el congif.py y pegas:


```python
# En groups del for i eliminas el array y colocas
["WWW","DEV","TERM","MISC"]

# Reemplazas el for i in groups por este.
for i, group in enumerate(groups):
    actual_key = str(i + 1)
    keys.extend([
        # Switch to workspace N
        Key([mod], actual_key, lazy.group[group.name].toscreen()),
        # Send window to workspace N
        Key([mod, "shift"], actual_key, lazy.window.togroup(group.name))
    ])

# Guardas los cambios mod ctrl r, y cierras sesion con mod ctrl q
```

Ahora vamos con los widgets, que se encuentran en la parte de widget_default = ...

```python
## Instalamos binutils
sudo pacman -S binutils

# Instalamos fuentes nerd fonts
yay -S nerd-fonts-ubuntu-mono

#Gimp
sudo pacman -S gimp 

# volume icon
sudo pacman -S volumeicon
## Encontraras el icono en la barra, si le das `volumeicon &` en la terminal se ejecutara y podras verlo en la barra. Le daras click derecho,  preferencias, te vas a status icon y en layout le das horizontal, en left mouse button action le das show slider.
```

Lo mejor sera copiar y pegar la conf de Antonio que se encuentra [aquí](https://github.com/antoniosarosi/dotfiles/tree/master/.config/qtile) teniendo en cuenta que no dañe lo anterior.

En el array  de groups donde pusimos DEV WWW y demás, lo puedes reemplazar por iconos de nerd fonts, hazlo, es mas bonito.

Para poner una key para el navegador pones en Keys

```python
#Browser
Key([mod], "b", lazy.spawn("fi krefox")),
```

## Archivo de logs de qtile

```bash
code .local/share/qtile/qtile.log
# Para vaciarlo
echo "" > .local/share/qtile/qtile.log
# Cierras sesion con mod ctrl q y vuelves a mirar
``` 

## Widget y powerline

(Icono necesario)[https://s3.amazonaws.com/thinkific-import-development/220744/bar2-200817-151001.png]

Aquí pudes hacer la [configuración](https://github.com/antoniosarosi/dotfiles/tree/master/.config/alacritty) de alacritty

## Tema funtes

```bash
sudo pacman -S ttf-dejavu ttf-liberation noto-fonts
```

## Monitores

Si tienes múltiples monitores, seguramente quieras usarlos todos. Así es como funciona xrandr:

```bash
# Lista todas las salidas y resoluciones disponibles
xrandr
# EN HDMI-1 Te saldra las salidas del monitor.
# Formato común para un portátil con monitor extra (reviar los px con el xrandr)
xrandr --output eDP-1 --primary --mode 1366-768 --pos 0x1080 --output HDMI-1 --mode 1280x1024 --pos 0x
```

O puedes hacer esto con interfaz grafica

```bash
sudo pacman -S arandr
```

Ábrela con rofi, ordena las pantallas como quieras, y después puedes guardar la disposición de las mismas. Muevelas a tu gusto, en mi caso la principal (eDF-1 a la izq y la HDMI-1  a la derecha), lo cual simplemente te dará un script con el comando exacto de xrandr que necesitas. Guarda ese script con el icono de descargar, lo guardas y miras el codigo que te guardo , pero todavía no le des al botón de aplicar.

Luego vas a tu .xprofile y modificas la linea por la primera, si no te funciona, eliminas el if else y lo podes y ya añadiendo al final un &.


### Explicación por si quieres saber como funciona....

Para un sistema con múltiples monitores deberías crear una instancia de Screen por cada uno de ellos en la configuración de Qtile.

Encontrarás una lista llamada screens en la configuración de Qtile que contiene solo un objeto inicializado con una barra en la parte de abajo. Dentro de esa barra puedes ver los widgets con los que viene por defecto.

Añade tantas pantallas como necesites y copia-pega los widgets, más adelante podrás personalizarlos. Ahora puedes volver a arandr, darle click en "apply" y reiniciar el gestor de ventanats.

Con esto tus monitores deberían funcionar.

## Imagenes y videos

```bash
sudo pacman -S vlc

sudo pacman -S imv
# Para visualizarla en consola
imv img.png
```

## Capturas de pantalla

```bash
# En la config de antonio el atajo es mod+s

sudo pacman -S scrot

# Si vas a config.py de qtile y vas a las Keys puedes poner esto
Key([mod], "s", lazy.spawn("scrot -e 'mv $f ~/Pictures/Screenshots/'")),
```

## Almacenamiento

Otra utilidad básica que podrías necesitar es montar de forma automática unidades de almacenamiento externas. Para ello uso udisks y udiskie. udisks es una dependencia de udiskie, así que solo instalaremos este último. Instala también el paquete ntfs-3g para leer y escribir en discos NTFS:

`sudo pacman -S udisks2`

`sudo pacman -S udiskie ntfs-3g`

Asegurate actualizar el x.session poniendo `udiskie -t &`

## Redes

Hemos configurado la red a través de nmcli, pero un programa gráfico es más cómodo. Yo uso nm-applet:

`sudo pacman -S network-manager-applet`

## Systray

Por defecto, tenemos una "bandeja del sistema" en Qtile, pero no hay nada ejecutándose en ella. Puedes lanzar los programas que acabamos de instalar así:

```bash
udiskie -t &
nm-applet &
```

Ahora deberías ver unos iconos en la barra, puedes clicar en ellos para configurar la red y discos. Puedes instalar también iconos para la batería y el volumen:

```bash
sudo pacman -S volumeicon cbatticon
volumeicon &
cbatticon &
```

## Notificaciones
Me gusta tener notificaciones en el escritorio también, para ello tienes que instalar libnotify y notification-daemon:

```bash
sudo pacman -S libnotify notification-daemon 
```

En nuestro caso, esto es lo que tenemos que hacer para tener notificaciones:

```bash
# Crea este fichero con nano o vim
sudo nano /usr/share/dbus-1/services/org.freedesktop.Notifications.service
# Pega estas líneas
[D-BUS Service]
Name=org.freedesktop.Notifications
Exec=/usr/lib/notification-daemon-1.0/notification-daemon
```

Pruébalo:

```bash
Pruébalo:
notify-send "Hola mundo"
```

# Otras configuraciones y herramientas

## AUR helper

Ahora que ya tienes un poco de software que te permite usar tu PC sin perder la paciencia, es hora de hacer cosas más interesantes. Primero, instala un AUR helper, yo uso yay:

```bash
sudo pacman -S base-devel git
cd /opt/
sudo git clone https://aur.archlinux.org/yay-git.git
sudo chown -R username:username yay-git/
cd yay-git
makepkg -si
```

Con acceso al Arch User Repository, puedes instalar prácticamente todo el software de este planeta que haya sido pensado para correr en Linux.

## Media Transfer Protocol

Si quieres conectar tu teléfono usando un cable USB, necesitarás una implementación de MTP y alguna interfaz de línea de comandos como esta:

```bash
sudo pacman -S libmtp
yay -S simple-mtpfs

# Lista todos los dispositivos conectados
simple-mtpfs -l
# Monta el primer dispositivo de la lista anterior
simple-mtpfs --device 1 /mount/point 
```

## Explorador de archivos

Hasta ahora siempre hemos manejado los ficheros a través de la terminal, pero puedes instalar un explorador de archivos. Para uno gráfico, recomiendo thunar, y para uno basado en terminal, ranger, aunque este último está pensado para usuarios de vim, usalo solo si sabes moverte en vim.

```bash
sudo pacman -S thunar ranger
``` 

Asegurate de tener una Key para el explorados en .config.py de qtile, asi:

`Key([mod], "e", lazy.spawn("thunar"))`

## Basura

Si no quieres usar rm constantemente y arriesgarte a perder ficheros, necesitas un sistema de basura. Por suerte, es bastante sencillio de hacer usando alguna de estas herramientas como glib2, y para interfaces gráficas como thunar necesitas gvfs:

```bash
sudo pacman -S glib2 gvfs
# Uso
gio trash path/to/file
# Vaciar papelera
gio trash --empty
```

Con thunar puedes abrir la basura desde el panel izquierdo, pero desde la línea de comandos puedes hacer:

```bash
ls ~/.local/share/Trash/files
```
https://www.gnome-look.org/browse?cat=135
## Tema de GTK

El momento que has estado esperando ha llegado, finalmente vas a instalar un tema oscuro. Yo uso Material Black Colors, puedes descargar una versión [aquí](https://www.gnome-look.org/p/1316887/), con sus respectivos iconos [aquí](https://www.pling.com/p/1333360/).

Sugiero empezar con Material-Black-Blueberry y Material-Black-Blueberry-Suru para iconos, o el Material-Black-Plum y Material-Black-Plum-Suru. Puedes encontrar otros temas para GTK en esta [página](https://www.gnome-look.org/browse?cat=135).  Una vez tengas descargados los temas, puedes hacer esto:

Otra opcion es (Juno)[https://github.com/EliverLara/Juno]

```bash
# Asumiendo que has descargado Material-Black-Blueberry
cd Downloads/
sudo pacman -S unzip
unzip Material-Black-Blueberry.zip
unzip Material-Black-Blueberry-Suru.zip
rm Material-Black*.zip

# Si tieens nombres mas largos renombralos, sera mas sencillo
mv Material-Black-Blueberry-xxxx Material-Black-Blueberry

# Haz tu tema visible a GTK
sudo mv Material-Black-Blueberry /usr/share/themes
sudo mv Material-Black-Blueberry-Suru /usr/share/icons
```

Ahora edita ~/.gtkrc-2.0 y ~/.config/gtk-3.0/settings.ini añdiendo estas líneas:

```bash
# ~/.gtkrc-2.0
gtk-theme-name = "Material-Black-Blueberry"
gtk-icon-theme-name = "Material-Black-Blueberry-Suru"

# ~/.config/gtk-3.0/settings.ini
gtk-theme-name = Material-Black-Blueberry
gtk-icon-theme-name = Material-Black-Blueberry-Suru
```

Esta es la versiona anterior:
```bash
# ~/.gtkrc-2.0
gtk-theme-name="Material-Black-Plum"
gtk-icon-theme-name="Material-Black-Plum-Suru"
gtk-font-name="Noto Sans 11"
gtk-cursor-theme-name="Breeze_Default"
gtk-cursor-theme-size=0
gtk-toolbar-style=GTK_TOOLBAR_BOTH_HORIZ
gtk-toolbar-icon-size=GTK_ICON_SIZE_SMALL_TOOLBAR
gtk-button-images=0
gtk-menu-images=0
gtk-enable-event-sounds=0
gtk-enable-input-feedback-sounds=0
gtk-xft-antialias=1
gtk-xft-hinting=1
gtk-xft-hintstyle="hintslight"
gtk-xft-rgba="rgb"

# ~/.config/gtk-3.0/settings.ini

[Settings]
gtk-theme-name=Material-Black-Plum
gtk-icon-theme-name=Material-Black-Plum-Suru
gtk-font-name=Noto Sans 11
gtk-cursor-theme-name=Breeze_Default
gtk-cursor-theme-size=0
gtk-toolbar-style=GTK_TOOLBAR_BOTH_HORIZ
gtk-toolbar-icon-size=GTK_ICON_SIZE_SMALL_TOOLBAR
gtk-button-images=0
gtk-menu-images=0
gtk-enable-event-sounds=0
gtk-enable-input-feedback-sounds=0
gtk-xft-antialias=1
gtk-xft-hinting=1
gtk-xft-hintstyle=hintslight
gtk-xft-rgba=rgb
gtk-decoration-layout=menu:close
# gtk-application-prefer-dark-theme=1
```

La próxima vez que inicies sesión verás los cambios aplicados. Puedes instalar también un tema de cursor distinto, para ello necesitas [xcb-util-cursor](https://archlinux.org/packages/extra/x86_64/xcb-util-cursor/). El tema que yo uso es [Breeze](https://www.gnome-look.org/p/999927/), descárgalo, y después:

```bash
sudo pacman -S xcb-util-cursor
cd Downloads/
tar -xf Breeze.tar.gz
sudo mv Breeze /usr/share/icons
```

Edita /usr/share/icons/default/index.theme añadiendo esto:

```bash
[Icon Theme]
Inherits = Breeze
```

Ahora vuelve a editar ~/.gtkrc-2.0 y ~/.config/gtk-3.0/settings.ini:

```bash
# ~/.gtkrc-2.0
gtk-cursor-theme-name = "Breeze"

# ~/.config/gtk-3.0/settings.ini
gtk-cursor-theme-name = Breeze
```

Asegurate de escribir bien los nombres de los temas e iconos, deben ser exactamente los nombres de los directorios donde se encuentran, los que ofrece esta salida:

```bash
ls /usr/share/themes
ls /usr/share/icons
```

Si no funciona, tal vez debas cambiar el `/usr/share/gtk-2.0/gtkrc`, `/usr/share/gtk-3.0/settings.ini` y `/etc/gtk-2.0/gtkrc`

## Qt

Los temas de GTK no se aplican a programas Qt, pero puedes usar Kvantum para cambiar los temas por defecto:

```bash
sudo pacman -S kvantum-qt5
echo "export QT_STYLE_OVERRIDE=kvantum" >> ~/.profile
```

# Tema de lightdm

También podemos cambiar el tema de lightdm, ¿por qué no? Necesitamos otro greeter y algún tema, en concreto lightdm-webkit2-greeter y lightdm-webkit-theme-aether:

```bash
sudo pacman -S lightdm-webkit2-greeter
yay -S lightdm-webkit-theme-aether
```

Estas son las configuraciones que tienes que hacer:

```bash
# /etc/lightdm/lightdm.conf
[Seat:*]
# ...
# Descomenta esta línea y pon este valor
greeter-session = lightdm-webkit2-greeter
# ...

# /etc/lightdm/lightdm-webkit2-greeter.conf
[greeter]
# ...
webkit_theme = lightdm-webkit-theme-aether
```

Listo.

## Multimedia

Consulta [esta página](https://wiki.archlinux.org/title/List_of_applications/Multimedia) para ver la variedad de programas multimedia disponibles

### Imágenes

```bash
sudo pacman -S geeqie
```

### Video y audio

```bash
sudo pacman -S vlc
```

Tema oscuro: https://github.com/antoniosarosi/dotfiles/blob/master/README.es.md#v%C3%ADdeo-y-audio

---

# Clonar configueacion de dotfiles qtile 

[Enlace](https://github.com/antoniosarosi/dotfiles/tree/83fb32e60921a879cfab717553f8f016e0145d2b)

Vamos a una consola

```bash
cd ~
git clone https://github.com/antoniosarosi/dotfiles/tree/83fb32e60921a879cfab717553f8f016e0145d2b
mv dotfiles/ dofiles-antonio
cp -r dotfiles-anotnio/.config/qtile/ .config/ 
```

## Cosas a tener en cuenta si tienes errores

```bash
sudo pacman -S python-pip gcc
pip install psutil # Esto es para que funcione el widget de la red

sudo pacman -S pacman-contrib # Esto es para que funcione el widget de la actualización de paquetes
checkupdates 

# Recuerda hacer mod control r para reiniciar qtile

# Para ver errores
code .local/share/qtile/qtile.log 

# Tal vez tengas que cambiar el icono de clock
``` 

## Mas cosas que puedes hacer

```bash
sudo pacman -S redhift # Para que el brillo de la pantalla se adapte a la hora del dia
# Con mod r se activo, con mod shift r se desactivav 
```

```bash
sudo pacman -S python-notify
cd ~
cp -r dotfiles-antonio/.theme/ .
cp -r dotfiles-antonio/.config/alacritty .config 

# Para ver temas de alacritty
cd .config/alacritty
ls themes/ # Te aparecen todos los temas
./theme.py nombreTema # Para cambiar el tema 

# Para temas general
cd
cd .theme/

# Si no te funciona puedes mofidicar el set-themes.py de .theme
## Eliminas lo de from notigy... y en vez del notifications ese, escribes subprocess.call(['notify-send','Theme set!'])
## haces ./set-themes.py qtile
# Recuerda que para modificarlo vas a theme.json y modificas el wm y alacritty por el tema que quieras, tipo darcula, onde-dark, etc
```

```bash
sudo pacman -S lightdm-webkit2-greeter # Para cambiar el tema de lightdm
cd
sudo code 7etc/lightdm/lightdm.conf
#Buscas la linea que es  greeter-session=example... y la descomentas
#Le pones = lightdm-webkit2-greeter
```

```bash
cp dotfiles-antonio/.bashrc .
code .bashrc

# Si hay un alias de bateria lo eliminas
# Vas a https://github.com/git/git/blob/master/contrib/completion/git-prompt.sh y copias eso en raw
code .git-prompt.sh
chmod 755 .git-prompt.sh
# Pegas todo eso ahí en el code]]]
```

## Para más gestores

```bash
sudo pacman -S xlockmore trayer # Para el gestor de ventanas
```

# Repaso de Configuración de Qtile

## Que son las teclas mod

| mod1 | mod2  | mod3  | mod4 = mod | mod5 | mod6 | mod7 | mod8  | mod9  | mod10 | mod11 | mod12 | mod13 |
| ---- | ----- | ----- | ---------- | ---- | ---- | ---- | ----- | ----- | ----- | ----- | ----- | ----- |
| alt  | shift | super | win        | ctrl | tab  | esc  | space | enter | up    | down  | left  | right |

## Que son los groups

Son los entornos de trabajo que aparecen en nuestra ventanita, en plan para cambiar de escritorio, pero en realidad es para cambiar de entorno de trabajo.

## Layouts

Además del básico lo más usados son MonadTall y MonadWide, que son en los que tienes una ventana grande y las demás pequeñas se van abriendo.

## Widgets

Es lo que aparece en la barra de tareas, en plan el reloj, la bateria, el volumen, etc.

## Screens

Es la pantalla, en plan si tienes dos monitores, es la pantalla de la izquierda y la de la derecha.

## Mouse

- Estando en una ventana haces mod + click izquierdo y arrastras la ventana
- Estando en una ventana haces mod + click derecho y cambias el tamaño

# Atajos de teclado

Estos son algunos atajos de teclado comunes a todos mis gestores de ventanas:

## Ventanas

| Atajo                   | Acción                                       |
| ----------------------- | -------------------------------------------- |
| **mod + j**             | siguiente ventana                            |
| **mod + k**             | ventana previa                               |
| **mod + shift + h**     | aumentar master                              |
| **mod + shift + l**     | decrementar master                           |
| **mod + shift + j**     | mover ventana abajo                          |
| **mod + shift + k**     | mover ventana arriba                         |
| **mod + shift + f**     | pasar ventana a flotante                     |
| **mod + tab**           | cambiar la disposición de las ventanas       |
| **mod + [1-9]**         | cambiar al espacio de trabajo N (1-9)        |
| **mod + shift + [1-9]** | mandar ventana al espacio de trabajo N (1-9) |
| **mod + punto**         | enfocar siguiente monitor                    |
| **mod + coma**          | enfocar monitor previo                       |
| **mod + w**             | cerrar ventana                               |
| **mod + ctrl + r**      | reiniciar gestor de ventana                  |
| **mod + ctrl + q**      | cerrar sesión                                |

Los siguientes atajos de teclado funcionarán solo si instalas los programas que
lanzan:

```bash
sudo pacman -S rofi thunar firefox alacritty redshift scrot
```

Para configurar *rofi*,
[lee este README](https://github.com/antoniosarosi/dotfiles/tree/master/.config/rofi/README.es.md),
y para *alacritty*, [este](https://github.com/antoniosarosi/dotfiles/tree/master/.config/alacritty/README.es.md).

## Apps

| Atajo               | Acción                                 |
| ------------------- | -------------------------------------- |
| **mod + m**         | lanzar rofi                            |
| **mod + shift + m** | navegación (rofi)                      |
| **mod + b**         | lanzar navegador (firefox)             |
| **mod + e**         | lanzar explorador de archivos (thunar) |
| **mod + return**    | lanzar terminal (alacritty)            |
| **mod + r**         | redshift                               |
| **mod + shift + r** | parar redshift                         |
| **mod + s**         | captura de pantalla (scrot)            |

# Software

## Utilidades básicas

| Software                                                                                            | Utilidad                                      |
| --------------------------------------------------------------------------------------------------- | --------------------------------------------- |
| **[networkmanager](https://wiki.archlinux.org/index.php/NetworkManager)**                           | Autoexplicativo                               |
| **[network-manager-applet](https://wiki.archlinux.org/index.php/NetworkManager#nm-applet)**         | *NetworkManager* systray                      |
| **[pulseaudio](https://wiki.archlinux.org/index.php/PulseAudio)**                                   | Autoexplicativo                               |
| **[pavucontrol](https://www.archlinux.org/packages/extra/x86_64/pavucontrol/)**                     | *pulseaudio* GUI                              |
| **[pamixer](https://www.archlinux.org/packages/community/x86_64/pamixer/)**                         | *pulseaudio* CLI                              |
| **[brightnessctl](https://www.archlinux.org/packages/community/x86_64/brightnessctl/)**             | Brillo para portátiles                        |
| **[xinit](https://wiki.archlinux.org/index.php/Xinit)**                                             | Inicia programas antes del gestor de ventanas |
| **[libnotify](https://wiki.archlinux.org/index.php/Desktop_notifications)**                         | Notificaciones de escritorio                  |
| **[notification-daemon](https://www.archlinux.org/packages/community/x86_64/notification-daemon/)** | Autoexplicativo                               |
| **[udiskie](https://www.archlinux.org/packages/community/any/udiskie/)**                            | Montar discos automáticamente                 |
| **[ntfs-3g](https://wiki.archlinux.org/index.php/NTFS-3G)**                                         | Leer y escribir NTFS                          |
| **[arandr](https://www.archlinux.org/packages/community/any/arandr/)**                              | GUI para *xrandr*                             |
| **[cbatticon](https://www.archlinux.org/packages/community/x86_64/cbatticon/)**                     | Systray para la batería                       |
| **[volumeicon](https://www.archlinux.org/packages/community/x86_64/volumeicon/)**                   | Systray para el volumen                       |
| **[glib2](https://www.archlinux.org/packages/core/x86_64/glib2/)**                                  | Basura                                        |
| **[gvfs](https://www.archlinux.org/packages/extra/x86_64/gvfs/)**                                   | Basura para GUIs                              |

## Fuentes, temas y GTK

| Software                                                                               | Utilidad                               |
| -------------------------------------------------------------------------------------- | -------------------------------------- |
| **[Picom](https://wiki.archlinux.org/index.php/Picom)**                                | Compositor para Xorg                   |
| **[UbuntuMono Nerd Font](https://aur.archlinux.org/packages/nerd-fonts-ubuntu-mono/)** | Nerd Font para iconos                  |
| **[Material Black](https://www.gnome-look.org/p/1316887/)**                            | Tema e iconos para GTK                 |
| **[lxappearance](https://www.archlinux.org/packages/community/x86_64/lxappearance/)**  | GUI para cambiar temas                 |
| **[nitrogen](https://wiki.archlinux.org/index.php/Nitrogen)**                          | GUI para establecer fondos de pantalla |
| **[feh](https://wiki.archlinux.org/index.php/Feh)**                                    | CLI para establecer fondos de pantalla |

## Apps

| Software                                                              | Utilidad                           |
| --------------------------------------------------------------------- | ---------------------------------- |
| **[alacritty](https://wiki.archlinux.org/index.php/Alacritty)**       | Emulador de Terminal               |
| **[thunar](https://wiki.archlinux.org/index.php/Thunar)**             | Gestor de archivos gráfico         |
| **[ranger](https://wiki.archlinux.org/index.php/Ranger)**             | Gestor de archivos de terminal     |
| **[neovim](https://wiki.archlinux.org/index.php/Neovim)**             | Editor de texto basado en terminal |
| **[rofi](https://wiki.archlinux.org/index.php/Rofi)**                 | Menú y navegación                  |
| **[scrot](https://wiki.archlinux.org/index.php/Screen_capture)**      | Captura de pantalla                |
| **[redshift](https://wiki.archlinux.org/index.php/Redshift)**         | Cuida tus ojos                     |
| **[trayer](https://www.archlinux.org/packages/extra/x86_64/trayer/)** | Systray                            |
