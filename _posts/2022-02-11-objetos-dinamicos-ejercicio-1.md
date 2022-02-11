---
layout: single
title: Ejercicio 1 C++ - Objetos Dinamicos
excerpt: 'Ejercicio sobre objetos dinamicos en el lenguaje de programación c++'
date: 2022-02-11
classes: wide
header:
  teaser: /assets/images/ejercicios-c++.png
  teaser_home_page: true
  icon: /assets/images/objetos-dinamicos/code-solid.svg
categories:
  - Objetos Dinamicos
  - POO
tags:
  - Lenguajes de programacion
  - C++
  - Ejercicios
---

![Programming Image](/assets/images/objetos-dinamicos/ejercicio-1.jpg)

## Enunciado del Problema

> Suponemos que varias personas reciben un salario durante un cierto número de meses (variable) y queremos saber el total de lo pagado.

- Entradas

  > deberá leer por consola

- Salidas

  > La salida deberá indicar el salario total

- Nota
  > La entrada y la salida no llevan los mensaje de "¿Cuántas personas son?", "¿Cuántos meses de salario son?", ni "El salario del mes 1:"

## Casos de Prueba

Entrada 1

```
Cuántas personas son: 2
Cuántos meses de salario son: 1
El salario del mes 1: 100000
El salario del mes 1: 200000
```

Salida 1

```
300000
```

## Solucion

![Imagen de Programacion](/assets/images/objetos-dinamicos/image-1.jpg)

Pensemos primero en el ejercicio, como vemos lo que queremos es saber cual va a ser el total del salario de ciertas personas por cierto numero de meses, donde el numero de meses y el numero de personas seran variables que digitara el usuario.

¿ Pero como haremos para calcular el total de salario? Pues simple, esto lo haremos con un doble for, uno que recorra el numero de meses y otro que recorra el numero de personas, de tal forma que quedaría algo así:

```cpp
=> Mes #1
  -> Persona #1
      Leemos su salario
  -> Persona #2
     Leemos su salario
=> Mes #2
  -> Persona #1
      Leemos su salario
  -> Persona #2
      Leemos su salario
```

Ahora bien, debido a que vamos a usar la programación orientada a objetos, debemos pensar en una clase, en nuestro clase la clase se llamara _Empresa_, así que empezemos definiendo el .h y el .cpp

### Empresa.h

```cpp
/*
Archivo: Empresa.h
Autor: Carlos Hernandez
Fecha creacion: 2022/02/07
Fecha ultima modificacion: 2022/02/07
licencia: GNU-GPL
*/

/**
Clase: Empresa
Responsabilidad: Esta clase servira para almacenar el numero de personas y el numero de meses que cobra estas personas para así determinar el total de salario que reciben los trabajadores
Relaciones: Ninguna
*/

#ifndef _EMPRESA_H_
#define _EMPRESA_H_
#include <iostream>
using namespace std;

class Empresa
{
  // Atributos
private:
  int numeroPersonas;
  int numeroMeses;
  int totalSalario;
  // Metodos
public:
  // Constructor
  Empresa();
  // Destructor
  virtual ~Empresa();
  // Funciones
  int getNumeroPersonas();
  int getNumeroMeses();
  int getTotalSalario();
  void setNumeroPersonas();
  void setNumeroMeses();
  void setTotalSalario(int _totalSalario);
  void calcularElTotalSalario();
};

#endif
```

> Lo más importante que vemos en esta clase son los atributos, en los cuales almacenaremos el numero de personas, meses y el total de salario. Además encontramos los metodos, con sus getters y setters, adicionalmente hay un metodo llamado calcularElTotalSalario en donde haremos el doble for.

### Empresa.cpp

```cpp
/**
Archivo: Empresa.cpp
Autor: Carlos Hernandez
Fecha creacion: 2022/02/07
Fecha ultima modificacion: 2022/02/07
licencia: GNU-GPL
*/

#include "Empresa.h"

/*
Nombre: Empresa
Funcion: Constructor
Retorno: No aplica
*/
Empresa::Empresa()
{
  numeroMeses = 0;
  numeroPersonas = 0;
  totalSalario = 0;
}
/*
Nombre: ~Empresa
Funcion: Destructor
Retorno: No aplica
*/
Empresa::~Empresa()
{
}

// En este metodo retornamos el atributo numeroMeses de la clase
int Empresa::getNumeroMeses()
{
  return numeroMeses;
}

// En este metodo retornamos el atributo numeroPersonas de la clase
int Empresa::getNumeroPersonas()
{
  return numeroPersonas;
}

// En este metodo retornamos el atributo totalSalario de la clase
int Empresa::getTotalSalario()
{
  return totalSalario;
}

// Aquí lo que hacemos es declarar un auxiliar int, leer mediante cin ese auxliar y darle al atributo numeroMeses de la clase el valor del auxiliar
void Empresa::setNumeroMeses()
{
  int aux;
  cin >> aux;
  numeroMeses = aux;
}

// Aquí lo que hacemos es declarar un auxiliar int, leer mediante cin ese auxliar y darle al atributo numeroPersonas de la clase el valor del auxiliar
void Empresa::setNumeroPersonas()
{
  int aux;
  cin >> aux;
  numeroPersonas = aux;
}

// Este metodo es un poco diferente pero con la misma funcionalidad de los otros setters, mediant eun parametro de tipo int podremos darle a totalSalario el valor de ese parametro
void Empresa::setTotalSalario(int _totalSalario)
{
  totalSalario = _totalSalario;
}

// Finalmente encontramos el metodo donde calculamos el total salario, aqui como bien dijimos anteriormente, mediante un doble for recorremos primero los meses y luego el numero de personas, y en cada recorrido hacemos un cin (para guardar el valor de salario de la persona) y le sumamos al atributo totalSalario ese valor
void Empresa::calcularElTotalSalario()
{
  for (int i = 0; i < numeroMeses; i++)
  {
    for (int j = 0; j < numeroPersonas; j++)
    {
      int aux;
      cin >> aux;
      totalSalario += aux;
    }
  }
}
```

## main.cpp

```cpp
/**
Archivo: main.cpp
Autor: Carlos Hernandez
Fecha creacion: 2022/02/07
Fecha ultima modificacion: 2022/02/07
licencia: GNU-GPL
*/

/**
Historia: Nos encontramos en una empresa que quiere calcular cuanto es el total de salario que se le ha pagado a un numero de personas en ciertos meses, por lo que empieza pidiendole al usuario el numero de personas y el numero de meses, para así calcular el total pagado.
*/

#include "Empresa.h"

// Funcion main
int main()
{
  Empresa *miEmpresa = new Empresa();
  miEmpresa->setNumeroPersonas();
  miEmpresa->setNumeroMeses();
  miEmpresa->calcularElTotalSalario();
  cout << miEmpresa->getTotalSalario() << endl;

  delete miEmpresa;
  miEmpresa = nullptr;

  return 0;
}
```

> En este archivo lo que hacemos es declarar un objeto de la clase Empresa, pero no un objeto normal, si no un objeto dinamico, el cual ya vimos su teoría en [Articulo de Objetos dinamicos](https://carlosher007.github.io/objetos-dinamicos-c++/). Y simplemente para llamar a los metodos de esta clase no lo hacemos mediante un . (punto) si no con la flecha (->), pues es un puntero
