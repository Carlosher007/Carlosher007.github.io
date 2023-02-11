---
layout: single
title: Personalizar Arch Linux - 2
excerpt: 'Como instalar Arch Linux y no morir en el intento'
date: 2023-02-06
classes: wide
header:
  teaser: /assets/images/2023-02-06-Instalar-Arch-1/wallpapper-arch.png
  teaser_home_page: true
  icon: /assets/images/2023-02-06-Instalar-Arch-1/icon-arch.png
categories:
  - Personalización de Arch Linux
tags:
  - Linux
  - Arch Linux
---

# Otros Gestores de ventana

## Spectrwm

```bas
sudo pacman -S upower pamixer # para la bateria, volumen k
sudo pacman -S spectrwm
```

Si hacemos `ls /usr/share/xsessions` nos saldrá una lista de gestores de ventanas, entre ellos estará `spectrwm.desktop` y el que teníamos antes `qtile.desktop`. 

Copiamos la config de Antonio: `cp -r dotfiles-antonio/.config/spectrwm ~/.config/`
Copiamos la config de Antonio: `cp -r dotfiles-antonio/.spectrwm.conf .`

Para verlo, cierras sesión y en vez de elegir `qtile` elegimos `spectrwm`. Para cerrar sesion es con `mod + ctrl + q`.

Puedes hacer 

```bash
code .config/spectrwm
code .spectrwm.conf

# En el archivo baraction.sh, si no te funciona el icono de la bateria, ca,bia el baterry_BAT1 por BAT0

# Para que funcione igual que qtile las ventanas debes modificar en .spectrwm.conf la linea de workspace_clamp = 1 a workspace_clamp = 0.
```

Puedes hacer `code .config/spectrwm/ .spectrwm.conf` para abrir los dos archivos a la vez para ver la configuracion.

Para construir widgets aquí, primero elige un icono de nerd fonts y copialo. Supongamos que quieres un widget para la memoria, entonces debe buscar el comando el cual te traera eso en bash que en este caso es 

```bash
mem = `free | awk '/Mem/ {printf "%d Mib/%d MiB\n", $3 / 1024.0, $2 / 1024.0 }'`
echo -n "Icono: $mem"
```

Eso lo pones en el baraction.sh de la configuracion de spectrwm, debajo de cualquier otro widget. Para que se ejecute cada cierto tiempo quedaría así:

```bash
# Mem
if (($i % 15 == 0)); then
    mem = `free | awk '/Mem/ {printf "%d Mib/%d MiB\n", $3 / 1024.0, $2 / 1024.0 }'`
fi
echo -n "$(icon ICONO) $mem "
```

Para cambiar la posicion del trayer, pues hay que hacerlo si añades o eliminas widgets, es con el archivo autostart.sh y modificas la lines de `kmargin: # \` .

Para añadir Keys, sería en el .spectrwm.conf, en la parte de keys. donde dice cosas como `#File explorer` y demás, pues añades el tuyo, ejemplo:

```bash
# Code
program[vscode] = code
bind[vscode] = MOD+v
```


## OpenBox

- Nota: Para cerrar sesion debes hacer click en el fondo de pantalla y clicar "Log out"

```bash
sudo pacman -S openbox tint2 # tint2 es la barra de tareas

# Copiamos la configuracion
cp -r dotfiles-antonio/.config/openbox ~/.config/f
cp -r dotfiles-antonio/.config/tint2 ~/.config/

## Cerramos sesion y elegimos openbox
```

# Más sobre la configuración de qtile

## Colores

Si te vas al config de qtile, hay una carpeta llamada themes, ahí puedes colocar tus propios colores en un nuevo archvio .json y colocar el nombre de ese archivo en el config.json. Recuerda que son dos colores para los themes, puedes poner el mismo color , o dos diferentes para hacer un degradado.

## Widgets

Para los widgets te vas a la [documentacion de qtile](http://docs.qtile.org/en/stable/manual/ref/widgets.html?highlight=widgets) y ahi puedes elegir entre varias opciones. 

Para colocarlo te irias a `widgtets.py`. Despues de cualquier widget pones un powerline para el tema del color (tener en cuenta que cuadre el color) y podes el widget con las distintas configuraciones que puede tener, que se encuentran en la columna *key* de la pagina. Por ejemplo `widget.CPU(**base(bg='color3))`. Para ponerle un icono te vas a nerd fonts icons, lo buscas y lo copias como icono. Luego del powerline que añadiste dices:  `icon(bg='color2,text='icono')`. k

## Espacios de trabajo

Teniendo en cuenta que puedes tener como maximo 9 espacios de trabajo, en el apartado de `groups.py` puedes modificar el numero de estos, añadiendo o quitando iconos.

# Testear gestores de ventanas con xephyr arch

Lo instalas con 

```bash
sudo pacman -S xorg-server-xephyr

#Para probarlo, puedes hacer por ejemplo
Xephyr -br -ac -noreset -screen 1280-720 :1 &

# Te abre una ventana y con mod shift f la pasas a flotante. Esta ventana es un entorno de desarrollo para gestores de ventanas.

#Para lanzar un gestor sería (despues del comandoa anterior)
DISPLAY=:1 spectrwm # Te lanza pectrwm 

# Para qtile
Xephyr -br -ac -noreset -screen 1680-1050 :1 &
DISPLAY=:1 qtile
```

En este punto los atajos de teclado no funcionaran en esa ventana, para ello tendras que hacer `code .config/qtile` , buscar el keys.py y modificas mod = "mod4" por "mod1", *pero no reinicies el gestor de ventanas*, reinicias el xephyr dandole control c y volviedo a hacer el display de qtile.

SI tienes errores, ese test se ira a la configuracion por defecto y te saldran los errores o los puedes ver con `code .local/share/qtile/qtile.log`
