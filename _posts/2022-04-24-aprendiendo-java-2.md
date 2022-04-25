---
layout: single
title: Aprendiendo Java - 2
excerpt: 'Aprendiendo Java - Selección'
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

## Tema 1 : Caso Practico IF

```java
package main;

import java.util.Scanner;

public class Main {

    public static void main(String[] args) {
        Scanner consola = new Scanner(System.in);

        int opcion;
        double perimetro, area;

        System.out.print("Ingrese una opcion :\n\n "+
                "1) Rectangulo\n" +
                "2) Circunferenncia\n\n"+
                ">> ");
        opcion = consola.nextInt();
        consola.nextLine();


        //opcion.equals("1")
        if (opcion == 1) {
            int largo, ancho;

            System.out.print("Ingrese el largo: ");
            largo = consola.nextInt();
            consola.nextLine();

            System.out.print("Ingrese el ancho: ");
            ancho = consola.nextInt();
            consola.nextLine();

            perimetro = largo * 2 + ancho * 2;
            area = largo * ancho;

            System.out.println("perimetro = " + perimetro);
            System.out.println("area = " + area);

        } else if (opcion == 2) {
            double radio;
            final double pi = 3.1415;

            System.out.print("Ingrese el radio: ");
            radio = consola.nextDouble();
            consola.nextLine();

            perimetro = radio * 2 * pi;
            area = radio * radio * pi;

            System.out.println("perimetro = " + perimetro);
            System.out.println("area = " + area);

        } else {
            System.out.println("ERROR");
        }

    }
}

```

## Tema 2: Caso Switch

```java
package main;

import java.util.Scanner;

public class Main {

    public static void main(String[] args) {
        Scanner consola = new Scanner(System.in);

        String opcion;
        double perimetro, area;

        final String OPCION_1 = "1";
        final String OPCION_2 = "2";
        final String OPCION_SALIR = "0";

        System.out.print("Ingrese una opcion :\n\n"
                + "0 - s) Salir\n"
                + "1 - a) Rectangulo\n"
                + "2 - b) Circunferenncia\n\n"
                + ">> ");
        opcion = consola.nextLine();

        switch (opcion) {
            case OPCION_SALIR , "s" , "S" -> {
                System.out.print("Presione enter >> ");
                consola.nextLine();
            }
            case OPCION_1 , "a" , "A" -> {
                double largo,
                        ancho;
                System.out.print("Ingrese el largo: ");
                largo = consola.nextDouble();
                consola.nextLine();
                System.out.print("Ingrese el ancho: ");
                ancho = consola.nextDouble();
                consola.nextLine();
                perimetro = largo * 2 + ancho * 2;
                area = largo * ancho;
                System.out.println("perimetro = " + perimetro);
                System.out.println("area = " + area);
            }
            case OPCION_2 , "b", "B" -> {
                double radio;
                final double PI = 3.1415;

                System.out.print("Ingrese el radio: ");
                radio = consola.nextDouble();
                consola.nextLine();

                perimetro = radio * 2 * PI;
                area = radio * radio * PI;

                System.out.println("perimetro = " + perimetro);
                System.out.println("area = " + area);
            }
            default -> {
                    System.out.print("ERROR, no has ingresado una opcion valida \nPresione ENTER para salir >>");
                    consola.nextLine();
            }
        }
    }
}

```

## Tema 3: Operador Ternario

```java

package main;

public class Main {

    public static void main(String[] args) {
        /*
        SINTAXIS OPERADOR TERNARIO

        variable = (condicion)? primerValor : segundoValor
        */
        int i = 1;
        int j = 2;

        System.out.println("Nummero Mayor: " + ((i>j)? "i es mayor":"j es mayor"));
    }

}

```
