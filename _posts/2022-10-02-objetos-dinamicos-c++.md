---
layout: single
title: Objetos dinamicos c++
excerpt: 'Un vistaso a la creación y uso de objetos dinamicos en C++'
date: 2022-02-05
classes: wide
header:
  teaser: /assets/images/objetos-dinamicos/background.jpg
  teaser_home_page: true
  icon: /assets/images/objetos-dinamicos/code-solid.svg
categories:
  - Objetos Dinamicos
tags:
  - Lenguajes de programacion
  - C++
  - Teoria
---

![Programming Image](/assets/images/objetos-dinamicos/background.jpg)

# Vaibles dinamicas

- Crear => new
- Destruir => delete

> El operador new crea un nuevo objeto de la clase y retorna un puntero que apunta a ese objeto

```cpp
// Para crearlo
int *edad = new int(40);
Amigo *amigo = new Amigo("Javier");
// Para destruirlo
delete edad;
edad = nullptr;

delete amigo;
amigo = nullptr;
```

> Los objetos creados dinámicamente no se destruyen al llegar a la llave final del bloque. Aunque los punteros que apuntan a ellos, sí se destruyen

>Eso da la posibilidad de retornar un puntero desde una funcion

```cpp
int main(){
  //
  Persona *persona = empresa.quienEsElJefe();
  //
}

Persona *Empresa::quienEsElJefe(){
  Persona *jefe = new Persona("Ana");
  return jefe;
}
```

>Saber si tienes memory leaks
```
valgrind --tool=memcheck --leak-check=full ./main
```

>Crear un array dinamico con new
```cpp
cout << “¿Cuántos meses de salario son?” << endl;
string aux;
getline(cin, aux);
int numeroDeMeses = stoi(aux);
double *salarios = new double[numeroDeMeses];
for(int mes=0; mes<numeroDeMeses; mes++)
{
cout << “Dime el salario del mes “ << mes << “: “;
getline(cin, aux);
salarios[mes] = stof(aux);
}
/* … */
delete [] salarios;
salarios = 0;
```
