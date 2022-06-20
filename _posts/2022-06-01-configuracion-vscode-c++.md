---
layout: single
title: Configuración de C++ en Visual Studio COde
excerpt: 'Recursos y Configuración'
date: 2022-04-24
classes: wide
header:
  teaser: /assets/images/ejercicios-c++.png
  teaser_home_page: true
  icon: https://symbols.getvecta.com/stencil_25/38_java.bc46b9254c.png
categories:
  - Personalización y Configuración
tags:
  - C++ Visual Studio Code
---

## Configurar C++ en Visual Studio Code

### Instalar el compilador para VSC

[Descargr w64devkit](https://github.com/skeeto/w64devkit/releases/tag/v1.14.0)

- Extraer los archivos en disco local C
- Tenemos en cuenta la carpeta bin de w64devkit
- Abrimos **editar las variables de entorno**
- Buscas **Path** y le das editar
- Creas una nueva carpeta y pega la carpeta anteriormente tomada en cuenta
- En cmd escribes `gcc --version`

## En VSC

Una vez creado tu archivo c++ le das F5 para ejecutar, y le das a la opcion de **C++ (GDB)** y luego g++.exe
