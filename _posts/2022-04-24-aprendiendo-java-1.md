---
layout: single
title: Aprendiendo Java - 1
excerpt: 'Aprendiendo Java - Entrada y Salida Estandar'
date: 2022-04-24
classes: wide
header:
  teaser: /assets/images/aprendiendo-java/Poster.png
  teaser_home_page: true
  icon: https://symbols.getvecta.com/stencil_25/38_java.bc46b9254c.png
categories:
  - Aprendiendo
tags:
  - Java
  - Entrada y Salida Estandar
---

## Tema 1 : Inputs o Entradas

```java
package main;
import java.util.Scanner;

public class Leyendo {
    public static void main(String[] args) {
        String nombre , nombre2;
        int edad , edad2 ;

        Scanner entrada = new Scanner(System.in);

        //Persona 1

        System.out.print("Digite su nombre: ");
        nombre = entrada.nextLine();


        System.out.print("Digite su edad: ");
        edad = entrada.nextInt();
        entrada.nextLine();
        //El nextLine sirve para consumir el \n que no consume nextInt y asi poder seguir

        //Persona 2
        System.out.print("Digite otro nombre: ");
        nombre2 = entrada.nextLine();


        System.out.print("Digite otra edad: ");
        edad2 = entrada.nextInt();
        entrada.nextLine();


        System.out.println("Tu nombre es " + nombre + " y tu edad es " + edad);
        System.out.println("Tu otro nombre es " + nombre2 + " y tu otra edad es " + edad2);
    }
}
```

## Tema 2: Calculos simples

```java
package calculos_simples;

import java.util.Scanner;

public class CalculosSimples {

    public static void main(String[] args) {
        Scanner consola = new Scanner(System.in);
        // Area de un rectangulo
        int largo, ancho, perimetro, area;

        System.out.print("Digite el largo del rectangulo: ");
        largo = consola.nextInt();
        consola.nextLine();

        System.out.print("Digite el ancho del rectangulo: ");
        ancho = consola.nextInt();
        consola.nextLine();

        perimetro = largo * 2 + ancho * 2;
        area = ancho * largo;

        System.out.println("area = " + area);
        System.out.println("perimetro = " + perimetro);

        System.out.println("");

        // Area de un triangulo
        double base, alto;
        double areaT;

        System.out.print("Digite el alto del triangulo: ");
        alto = consola.nextDouble();
        consola.nextLine();

        System.out.print("Digite la base del triangulo: ");
        base = consola.nextDouble();
        consola.nextLine();

        areaT = (alto*base)/2;

        System.out.println("areaT = " + areaT);

        // Area y perimetro de una circunferencia
        double radio, perimetroC, areaC;
        //constante
        final double pi = 3.1415;

        System.out.print("Ingrese el radio del circulo: ");
        radio = consola.nextDouble();
        consola.nextLine();

        perimetroC = 2*radio * pi;
        areaC = radio * radio * pi;

        System.out.println("Perimetro :"+perimetroC+", Radio: "+areaC);

    }
}
```

## Tema 3: División entera

```java
package division_entera;

import java.util.Scanner;

public class DivisionEntera {

    public static void main(String[] args) {

        //EJERCICIO DE PELOTAS Y NIÑOS
        Scanner consola = new Scanner(System.in);

        int cantPelotas, cantNiños;
        int pelotasPorNiño, pelotasSobrantes;
        System.out.print("Ingrese la cantidad de niños y luego la cantidad de pelotas: ");

        cantNiños = consola.nextInt();

        cantPelotas = consola.nextInt();

        consola.nextLine();

        pelotasPorNiño = cantPelotas/cantNiños;
        pelotasSobrantes = cantPelotas % cantNiños;

        System.out.println("Pelotas por niño: " + pelotasPorNiño);
        System.out.println("Pelotas sobrantes = " + pelotasSobrantes);

        //EJERCICIO DE SUMA DE DIGITOS
        int numeroCuatroCifras;
        int c1,c2,c3,c4,suma;
        System.out.print("Digite el numero de cuatro cifras: ");
        numeroCuatroCifras = consola.nextInt();
        consola.nextLine();

        //4578
        // c1: 4578%10 = 8
        c1 = numeroCuatroCifras%10;

        //c2: (4578/10)%10
        c2 = (numeroCuatroCifras/10)%10;

        //c3: (4578/100)%10
        c3 = (numeroCuatroCifras/100)%10;

         //c2: (4578/1000)
        c4 = (numeroCuatroCifras/10)%10;

        suma = c1+c2+c3+c4;

        System.out.println("Suma: "+suma);
    }
}
```

## Tema 4: Caracteres especiales
```
package main;

/*
Escape Sequence

\t => tabulado
\b => Quita un espacio atras
\n => Salto de linea
\f => Añade un signo de interrofacion :  ?
\' => Escribir una palabra con comillas simples
\" => Escribir una palabra con dobles comillas
\\ => Colocar una sola barra inclinada inversa
*/

public class CaracteresEspeciales {
    public static void main(String[] args) {
    }
}
```
