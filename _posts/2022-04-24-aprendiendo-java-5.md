---
layout: single
title: Aprendiendo Java - 5
excerpt: 'Aprendiendo Java - Procedimientos y Funciones'
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

## Tema 1 : Introduccion a los Procedimeintos y las Funciones

```java
package main;

import java.util.Scanner;

public class Main {

    public static void main(String[] args) {

        //PROCEDIMIENTO ^ FUNCION
        int c;
        String caracter;
        var entrada = new Scanner(System.in);

        System.out.print("Ingrese un numero entero: >>");
        c = entrada.nextInt();
        entrada.nextLine();

        System.out.print("Ingrese un caracter: >>");
        caracter = entrada.nextLine();

        imprimirLinea(c, caracter);

        //FUNCION BOOLEANA
        System.out.print("Ingrese un caracter: >>");
        caracter = entrada.nextLine();
        System.out.println((esUnEntero(caracter)? "ES UN ENTERO":"NO ES UN ENTERO"));
    }

    //Si retorna void es procedimiento
    public static void imprimirLinea(int cantidad, String caracter) {
        for (int i = 0; i < cantidad; i++) {
            System.out.print(caracter.charAt(0));
        }
        System.out.println("");
    }
    //Si no retorna void es una funcion
    public static double areaRectangulo(int base, int altura){
        double area = base*altura;
        return area;
    }
    //Funcion booleana
    public static boolean esUnEntero(String valor){
        if(valor.length()==0){
            return false;
        }

        for (int i = 0; i < valor.length(); i++) {
            if(valor.charAt(i)<'0' || valor.charAt(i) >'9'){
                return false;
            }
        }

        return true;

    }
}
```

## Tema 2: Paso por referencia

```java
package main;

import java.util.concurrent.atomic.AtomicInteger;

public class Main {

    public static int x, y;
    public static AtomicInteger a;

    public static void main(String[] args) {
        a = new AtomicInteger(0);
        System.out.println("a = " + a.get());

        x = 5;
        y = 5;

        if(areaRectangulo(x,y,a)){
            System.out.println("a = " + a.get());
            System.out.println("x = " + x);
            System.out.println("y = " + y);
        }else{
            System.out.println("Los valores no son correctos");
        }

    }

    public static boolean areaRectangulo(int ancho, int largo, AtomicInteger area) {
        if ((ancho > 0) && (largo > 0)) {
            area.set(largo * ancho);
            return true;
        }
        area.set(0);
        return false;
    }

}
```

## Tema 3: Java Doc
```java
package main;

import java.util.concurrent.atomic.AtomicInteger;

public class Main {

    public static void main(String[] args) {
        AtomicInteger a = new AtomicInteger(0);
        System.out.println(areaTriangulo(2,5,a));
    }

    //ADMITEN CODIGO HTML (LOS JAVA DOCS)

    /**
     * Se retorna TRUE si los valores de <b>base</b> y <b>altura</b> son ambos mayores que 0.
     * En tal caso, además se retorna el valor del area en el parametro area.
     * Si largo o ancho resultan menores que 0, se retorna FALSE y el area vale 0.
     * @param base La base del triangulo
     * @param altura La altura del triangulo
     * @param area El area del triangulo
     * @return TRUE si largo y ancho son mayores que 0. FALSE si largo o ancho son menores que 0.
     * @see AtomicInteger
     */
    public static boolean areaTriangulo(int base, int altura, AtomicInteger area){
        if(base>0 && altura>0){
            area.set((base*altura)/2);
            return true;
        }
        area.set(0);
        return false;
    }

    //OTROS PARAMETROS
    /**
     * @author
     * @version
     *
     */
}
```

## Tema 4: Parametros tipo String
```java
package main;

import java.util.Scanner;
import java.util.concurrent.atomic.AtomicInteger;

public class Main {

    //Variables globales
    public static AtomicInteger area = new AtomicInteger(0);
    public static StringBuilder mensajeArea = new StringBuilder("Aun no inicializado");

    public static void main(String[] args) {

        Scanner consola = new Scanner(System.in);
        int largo, ancho;

        System.out.print("Largo >>");
        largo = consola.nextInt();
        consola.nextLine();

        System.out.print("Ancho >>");
        ancho = consola.nextInt();
        consola.nextLine();

        while (!areaRectangulo(largo, ancho, mensajeArea, area)) {
            System.out.println(mensajeArea);
            System.out.print("Largo >>");
            largo = consola.nextInt();
            consola.nextLine();

            System.out.print("Ancho >>");
            ancho = consola.nextInt();
            consola.nextLine();
        }

        System.out.println("AREA >>" + area.get());
    }

    /**
     * Queremos saber cual de todos los parametros nos da error a la hora de calcular el area, si el largo,
     * ancho, los dos o ninguno.
     *
     * @param largo
     * @param ancho
     * @param mensaje
     * @param area
     * @return true si es correcto, false si no lo es (los valores de entrada).
     */
    public static boolean areaRectangulo(int largo, int ancho, StringBuilder mensaje, AtomicInteger area) {
        //Borramos el contenido para añdir uno nuevo (el del mensaje)
        mensaje.delete(0, mensaje.length());
        if (largo <= 0 && ancho <= 0) {
            mensaje.append("El largo y ancho son incorrectos. Ingrese valores mayores que 0");
            area.set(0);
            return false;
        } else if (largo <= 0 && ancho > 0) {
            mensaje.append("El largo es incorrecto. Ingresa valores mayores que 0");
            area.set(0);
            return false;
        } else if (ancho <= 0 && largo > 0) {
            mensaje.append("El ancho es incorrecto. Ingresa valores mayores que 0");
            area.set(0);
            return false;
        }
        mensaje.append("El ancho y el largo son correctos");

        area.set(ancho * largo);
        return true;
    }

}
```

## Tema 5: Parametros Tipo Arreglo

```java
package main;

import java.util.Arrays;
import java.util.Scanner;

public class Main {

    public static Scanner consola = new Scanner(System.in);
    public static int[] miArreglo;

    public static void main(String[] args) {

        miArreglo = new int[]{1, 2, 3, 4, 5, 6};
        System.out.print("Arreglo original >>");
        System.out.println(Arrays.toString(miArreglo));

        invertir(miArreglo);
        System.out.println("");

        System.out.print("Arreglo invertido >>");
        System.out.println(Arrays.toString(miArreglo));
    }

    public static void invertir(int[] arreglo) {
        int[] retorno = new int[arreglo.length];
        for (int i = arreglo.length - 1; i >= 0; i--) {
            retorno[arreglo.length - i - 1] = arreglo[i];
        }
        // (arreglo a copiar, indice inicial, arreglo original, indice inicial, cuantas celdas a copiar)
        System.arraycopy(retorno, 0, arreglo, 0, arreglo.length);
    }

}
```