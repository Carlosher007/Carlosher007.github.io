---
layout: single
title: Crear una pagina web con GitHub
excerpt: 'Como crear y publicar tu propia pagina web estatica totalmente gratis con GitHub Pages, utilizando Markdown y unas plantillas muy buenas'
date: 2022-02-05
classes: wide
header:
  teaser: /assets/images/crear-pagina-web/principal_logo.png
  teaser_home_page: true
  icon: https://image.flaticon.com/icons/png/512/889/889192.png?w=740
categories:
  - GitHub Pages
  - Create a Page
tags:
  - GitHub
  - Pages
  - Markdown
---

![](/assets/images/crear-pagina-web/principal_logo.png)

Así como yo que tengo esta espectacular pagina / blog para publicar diferentes temas que aprendo y me gustaría compartir, tu tambien podrías tener la tuya totalmente gratis, y esto con GitHub Pages, además de unas cuantas plantillas que nos facilitará mucho las cosas. Para que entiendas, _GitHub Pages_ es un servicio (de GitHub claramente) que permite alojar nuestros proyectos con la posibilidad de publicarlo como una pagina web estatica sin tener que pagar ni un centavo, todo de forma muy sencilla y usando un lenguajes de marcado ligero llamado _Markdown_.

## ¿Que es lo que necesitas?

Antes de todo tienes que tener en cuenta que debes tener una cuenta de GitHub activa, así como tener unos conocimientos previos de Markdown (lo cual lo puedes encontrar en otro post del blog), y realmente nada más, debido a que todo es muy intuitivo, así que empezemos.

## Posibles templates que puedes usar

- [Plantilla SupunKavinda](https://github.com/SupunKavinda/jekyll-theme-leaf)
- [Plantilla Hacker-Blog](https://github.com/tocttou/hacker-blog)
- [Plantilla Neumorphism](https://github.com/longpdo/neumorphism)
- [Plantilla Slemire](https://github.com/slemire/slemire.github.io)

![](/assets/images/crear-pagina-web/image_neumorphism.png)

Estas son 4 de muchas otras plantillas que puedes utilizar para tu pagina, te recomiendo que le eches un vistazo a cada uno de ellas y eligas la que mas te agrade, en mi caso, la pagina que uso es la última, ya que es muy personalizable y se ve muy, pero muy bien.

## Clonar una plantilla

Una vez seleccinada la plantilla que te gusta, le daras `Fork`, que es basicamente clonar ese repositorio a nuestra cuenta de Github. Luego, iremos a settings y cambiaremos el _Repository name_ a : _tuNombreDeUsuario.github.io_. Como ejemplo puede ver como lo hice a continuación.
![](/assets/images/crear-pagina-web/fork_github.png)

![](/assets/images/crear-pagina-web/repository_name.png)

Ya con esto y esperando unos minutos a que Github trabaje tendremos nuestra pagina web publica a través de este enlace : **https://_nombreDeRepositorio_**
![](/assets/images/crear-pagina-web/snowscane_page.png)

---

Para personalizarla desde nuestro computador crearemos un carpeta en el pc y clonarmos el repositorio con el siguiente comando en cmd : `git clone https://github.com/Carlosher007/Carlosher007.github.io.git`, donde claramente, el link del github cambia al tuyo.

Con esto ya podemos mirar el _README.md_ del repo que elegiste y seguir los pasos, pero si estas como yo que el github no tenía readme seguiras los pasos siguientes-

## Instalación de herramientas necesarias

Existen programas que debemos instalar para poder personalizar estas paginas de forma agrable, estos programas se encuentran generalmente en el readme de cada pagina, mientras que en otros no, y es por ello que veremos como instalar aquellas que yo necesité. Cabe aclarar que el sistema operativo en el cual hare los pasos sera Windows.

![](/assets/images/crear-pagina-web/readme_instalar.png)

- En primer lugar encontramos un editor de codigo, algo que nos ayudara mucho para modificar archivos y demás. En mi caso recomiendo mucho _Visual Studio Code_, el cual lo puedes instalar por medio del siguiente link: [Instalar VSC](https://code.visualstudio.com/download)
- En segundo lugar encontramos una herramienta que nos va a permitir ver los cambios de la pagina mientras codificamos en tiempo real sin tener que publicarla en nuestro github, como un _live server_. Esta herramienta es **_Jekyll_**.

## Instalar Jekyll en Windows

Para instalar _Jekyll_ tendremos que instalar primero Ruby a través de este enlace : [Instalar Ruby](https://rubyinstaller.org). Escogeremos el paquete con DevKit de una version mayor que la 2.0, y sí es la ultima versión es mucho mejor.
![](/assets/images/crear-pagina-web/ruby_install1.png)

![](/assets/images/crear-pagina-web/ruby_install2.png)

Una vez descargado el archivo .exe lo ejecutaremos y como cualquier instalación de Windows le daremos a todo siguiente y aceptar. Sin olvidar seleccionar `Add Ruby executables to your PATH`.

![](/assets/images/crear-pagina-web/Path_Ruby.png)

Cuando haya finalizado la instalación le daremos a finalizar, para que se nos abra una consola de _rldk install_ que es para instalar el MSYS2. En esta consola te aparecera que eligas entre dos numeros, nosotros seleccionaremos la #1.

![](/assets/images/crear-pagina-web/ruby_MSY2.png)

En este punto abriremos en cmd la carpeta que habiamos creado y en la que hicimos clone de nuestro repo. En esta carpeta escribiremos los siguientes comandos, uno despues de otro.

```
gem -v
gem install bundler jekyll
bundle install
```

![](/assets/images/crear-pagina-web/cmd_jekyll.png)

Una vez hecho esto abriremos nuestro codigo en la carpeta que clonamos el repo. En el archivo **Gemfile** añadiremos `gem "webrick"` al final.

![](/assets/images/crear-pagina-web/webrick.png)

## Instalar Jekyll en Linux

Para este caso los siguientes comandos serán para la distribución de Arch Linux. Lo primero es actualizarlos paquetes e instalar ruby, así como otros paquetes necesarios.

```bash
sudo pacman -Syu
sudo pacman -S ruby base-devel rubygems
```

| Nombre     | Descripción                                                                                        |
|------------|---------------------------------------------------------------------------------------------------|
| ruby       | Lenguaje de programación dinámico, de código abierto, centrado en la simplicidad y la productividad |
| base-devel | Conjunto de herramientas de desarrollo básicas necesarias para compilar paquetes en Arch Linux    |
| rubygems   | Gestor de paquetes de Ruby que facilita la descarga, instalación, actualización y eliminación de gemas (librerías) en un proyecto de Ruby |

Luego, tenemos que agregar ruby al path de nuestra bash

```bash
# Escribes lo siguiente en una consola
nvim ~/.bashrc # Tambien puedes usar otro editor
#Agregas lo siguiente al archivo
export PATH=$PATH:/usr/bin/ruby
# Guardas y sales

#Para que los cambios se vean reflejados
source ~/.bashrc
```
Con eso ya hemos colocado ruby en el path, por lo que podremos ir a nuestra carpeta donde tenemos el repositorio. Eliminamos el archivo Gemfile.lock y escribimos lo siguiente

```bash
gem install bundler jekyll
bundle install --path vendor/bundle
bundle install
```

## Lanzar en local nuestra pagina

Ahora sí, ya podemos lanzar en local nuestra web, para testear la pagina en vivo mientras modificamos los archivos, con el comando `bundle exec jekyll serve`.

![](/assets/images/crear-pagina-web/bundle.png)

Con esto ya tendremos nuestra pagina corriendo en local, por lo que si vamos al navegador y buscamos **_localhost:4000_** tendremos nuestra pagina, la cual se vera un poco diferente a la que veras ahora.
![](/assets/images/crear-pagina-web/pagina_github.png)

## Personalizar Pagina

### Config.yml

Personalizar nuestra pagina sera muy intuitivo, pues en la mayoria de los casos solo tendremos que modificar o crear archivos.md . En mi caso para customizar el sidebar, tendre que modificar el archivo \_config.yml

![](/assets/images/crear-pagina-web/cap_config.png)

En la parte de site settings encontramos información general de la pagina, mientras que en Side Author encontraremos diferentes apartaods que podemos colocar en el sidebar como github, linkeding o redes sociales. Cabe aclar que en este último si no quieres que aparesca algo no escribes nada, en caso contrario escribes el link de tu perfil correspondiente.

![](/assets/images/crear-pagina-web/site_settings.png)

![](/assets/images/crear-pagina-web/side_author.png)

---

Para modificar los titulos que estan en la parte superior derecha, debes entrar en la carpeta _data_ y modificar el *title* del archivo _navigation.yml_
![](/assets/images/crear-pagina-web/heading_titles.png)

---

El apartado de about por defecto no lleva nada, entonces si quieres colocar algo allí debes seguir estos pasos:

- Abres la carpeta _pages y en el archivo about.md colocas `layout: about`
![](/assets/images/crear-pagina-web/about_layou.png)

- En la carpeta de _layouts creas un archivo *about.html* y añades esto:

```html
---
layout: archive
---

{{ content }}

<div class="entries-{{ page.entries_layout }}">
  <p>Aquí escribes la información que quiera colocar</p>
</div>
```

