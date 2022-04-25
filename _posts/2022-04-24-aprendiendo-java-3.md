---
layout: single
title: Aprendiendo Java - 3
excerpt: 'Aprendiendo Java - Repetición Iterativa'
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

## Tema 1 : Sentencia For

```java

package main;

import java.util.Scanner;


public class Main {

    public static void main(String[] args) {
        Scanner entrada = new Scanner(System.in);

        int cantidad;

        System.out.print("Ingrese un numero: ");
        cantidad = entrada.nextInt();
        entrada.nextLine();

        System.out.println("");

        for(int i=0;i<cantidad;i++){
            for(int j=i;j>0;j--){
            System.out.print("*");
            }
            System.out.println("");
        }

        System.out.println("");
    }

}

```

## Tema 2: Adivinador Basico

```java
package main;

import java.util.Scanner;
import java.util.Random;

public class Main {

    public static void main(String[] args) {
        Scanner entrada = new Scanner(System.in);
        Random numeros = new Random();

        final int rango = 100;
        final int MAX_INTENTOS = 10;
        boolean adivino = false;
        int numeroSecreto = numeros.nextInt(rango) + 1;

        //System.out.println("numeroSecreto = " + numeroSecreto);

        System.out.println("Adivinador 2.0 - Dispones de " + MAX_INTENTOS + " MAX_INTENTOS para adivinar");
        System.out.println("Rango de valores: 1 a " + rango);

        for (int i = 0; i < MAX_INTENTOS; i++) {
            System.out.print("Intento " + (i + 1) + ">> ");

            int numeroLeido;
            numeroLeido = entrada.nextInt();
            entrada.nextLine();

            if (numeroLeido == numeroSecreto) {
                adivino = true;
                System.out.println("Has adivinado el numero, eres el mejor");
                break;
            } else {
                if (numeroLeido > numeroSecreto && i != MAX_INTENTOS - 1) {
                    System.out.println("El numero a adivinar es mas pequeño que " + numeroLeido);
                } else {
                    if (i != MAX_INTENTOS - 1) {
                        System.out.println("El numero a adivinar es mas grande que " + numeroLeido);
                    }
                }
            }
        }

        if (!adivino) {
            System.out.println("No adivinaste el numero, suerte para la proxima \nEl numero era: >> " + numeroSecreto);
        }
    }
}

```

## Tema 3: Do While

```java
package main;

import java.util.Scanner;

public class Main {

    public static void main(String[] args) {

        Scanner consola = new Scanner(System.in);

        final String OPCION_1 = "1";
        final String OPCION_2 = "2";
        final String OPCION_SALIR = "0";
        String opcion;
        double perimetro, area;

        do {
            System.out.println("");
            System.out.print("Ingrese una opcion :\n\n"
                    + "0 - s) Salir\n"
                    + "1 - a) Rectangulo\n"
                    + "2 - b) Circunferenncia\n\n"
                    + ">> ");
            opcion = consola.nextLine();

            switch (opcion) {
                case OPCION_SALIR, "s", "S":
                    System.out.println("");
                    break;
                case OPCION_1 , "a" , "A":
                    System.out.println("");
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

                    System.out.println("");

                    System.out.println("perimetro = " + perimetro);
                    System.out.println("area = " + area);

                    System.out.println("");

                    System.out.print("Presione ENTER para continuar...");
                    consola.nextLine();
                    break;
                case OPCION_2 , "b", "B":
                    System.out.println("");
                    double radio;
                    final double PI = 3.1415;

                    System.out.print("Ingrese el radio: ");
                    radio = consola.nextDouble();
                    consola.nextLine();

                    perimetro = radio * 2 * PI;
                    area = radio * radio * PI;

                    System.out.println("");

                    System.out.println("perimetro = " + perimetro);
                    System.out.println("area = " + area);

                    System.out.println("");

                    System.out.print("Presione ENTER para continuar...");
                    consola.nextLine();
                    break;
                default:
                    System.out.println("");
                    System.out.print("ERROR, no has ingresado una opcion valida \nPresione ENTER para volver a intentarlo >>");
                    consola.nextLine();
                    break;
            }

        } while (!opcion.equals(OPCION_SALIR) && !opcion.equals("s") && !opcion.equals("S"));


        System.out.print("Presione ENTER para salir...");
        consola.nextLine();
    }
}

```

## Tema 4 : Adivinador un poco mas complejo

```java
package main;

import java.util.Scanner;

/*

QUEREMOS HACER UN PROGRAMA EN DONDE SEA EL PROPIO PROGRAMA QUE ADIVINE NUESTRO NUMERO, DE MODO QUE TENDREMOS EN CUENTA LO SIGUIENTE:

- Valor Inicial : 1
- Valor Final : 10

- Programa dice que el numero que esta en el medio
    = 5

- Si decimos que es mayor >
    = 8 (Mitad del nuevo rango)

- Decimos que es menor <
    = 6 (Adivino)
 */
public class Main {

    public static void main(String[] args) {

        Scanner entrada = new Scanner(System.in);

        //Declaramos las variables a utilizar
        String opcion;
        boolean adivino, trampa;
        int min, max, i, maxIntentos, numeroPosible;

        //Mostramos los mensajes
        System.out.println("Intentaré adivinar un número que tu elijas. ");
        System.out.println("Cuando indique un número tu deberás ingresar:");
        System.out.println("\t= si acierto al número que tu quieres que adivine.");
        System.out.println("\t> si el número que tu quieres que adivine es mayor que el que mostré. ");
        System.out.println("\t< si el número que tu quieres que adivine es menor que el que mostré. ");
        System.out.print("Dime el número minimo: ");
        min = entrada.nextInt();
        entrada.nextLine();
        System.out.print("Dime el número máximo: ");
        max = entrada.nextInt();
        entrada.nextLine();

        System.out.println();

        //Calculamos el numero de intentos necesarios para adivinar dependiendo del rango dado anteriormente
        maxIntentos = (int) (Math.log(max - min + 1) / Math.log(2) + 1);

        //Mostramos los mensajes
        System.out.println("EXCELENTE. Adivinaré tu número en no más de " + maxIntentos + " intentos. ");
        System.out.print("Presiona ENTER cuando quieras comenzar...");
        entrada.nextLine();
        System.out.println();

        adivino = false;
        trampa = false;

        for(i = 1; i<maxIntentos; i++){
            numeroPosible = ((max-min)/2)+min;

            System.out.print("Intento "+i+" -> El numero es... >>"+numeroPosible+": ");
            opcion = entrada.nextLine();

            switch(opcion){
                case "=":
                    adivino = true;
                    break;
                case "<":
                    max = numeroPosible-1;
                    break;
                case ">":
                    min = numeroPosible+1;
                    break;
            }

            if(adivino) break;

            if((min>max) || (max<min)){
                System.out.println("¡¡¡ ESTAS HACIENDO TRAMPA PELOTUDO !!!");
                trampa = true;
                break;
            }
        }

        if ((i==maxIntentos) && (!adivino) && (!trampa)){
            System.out.println("NO PUDE ENCONTRAR EL NUMERO, HAS GANADO...");
        }else if(adivino){
            System.out.println("HE GANADO, PON UN NUMERO MAS DIFICIL");
        }
    }
}
```
