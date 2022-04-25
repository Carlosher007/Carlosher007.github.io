---
layout: single
title: Aprendiendo Java - 4
excerpt: 'Aprendiendo Java - Arreglos'
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

## Tema 1 : Introducción a los arrelogs

```java
package main;

import java.util.Arrays;

public class Main {
    public static void main(String[] args) {
        //Declarar un arreglo : <<tipo nombre[] = new tipo[numero_elemntos]>>

        //Declaramos
        int arr1[] = new int[10];
        int arr2[] = {1,2,3,4,5,6,7,8,9,10};

        //Le damos los mismo valores a cada arreglo
        for(int i=0;i<10;i++){
            arr1[i] = i+1;
        }


        //Imprimir la longitud del areglo
        System.out.println("Longitud arreglo 1 >>"+arr1.length);
        System.out.println("Longitud arreglo 2 >>"+arr2.length);
        System.out.println();

//Comparar los arrays
        // => => EL equals funciona con arreglos de tipo primitivos y de Strings, mas no con arreglos de objetos
        System.out.println((Arrays.equals(arr1, arr2))? "son iguales":"son distintos");

    }
}

```

## Tema 2: Arreglos del Main y For Each

```java
package main;

public class Main {

    //Ese args es porque el main recibe argumentos / parametros antes de ser ejecutado, vamos a mostrarlos
    public static void main(String[] args) {

        int cantidad = args.length;
        System.out.println("Cantidad de argumentos = " + cantidad);

        System.out.println("Lista de argumentos");

        int indice = 0;
        for(String arg : args){
            System.out.print((indice!=args.length-1)? arg + ", " : arg);
            indice++;
        }
        System.out.println("");

    }

}

```

## Tema 3: Busqueda Lineal

```java
package main;

import java.util.Scanner;
import java.util.Random;

public class Main {

    public static void main(String[] args) {

        var consola = new Scanner(System.in);
        var numerosAleatorios = new Random();

        int arregloInicial[] = new int[10], arregloPosiciones[] = new int[10];
        int tope = -1, numeroBuscado;

        //Darle valor al arregloInicial
        for(int i=0;i<arregloInicial.length;i++){
            arregloInicial[i] = numerosAleatorios.nextInt(10)+1;
        }

        //Preguntar por el nuero buscado
        System.out.print("Digite el numero que desea buscar: >>");
        numeroBuscado = consola.nextInt();
        consola.nextLine();

        //Buscamos el numero en el arregloInicial y si lo encuentra ponemos su posicion en el arregoPosiciones
        for(int i = 0; i < arregloInicial.length; i++){
            if(arregloInicial[i]==numeroBuscado){
                tope++;
                arregloPosiciones[tope] = i;
            }
        }

        System.out.println("");

        //Mostramos el arreglo original
        int indice = 0;
        System.out.println("Arreglo original");
        for(int numero : arregloInicial){
            System.out.print((indice!=arregloInicial.length-1)? numero+", ":numero);
        }
        System.out.println("");

        //Mostramos el numero de ocurrencias
        System.out.println("Numero de apariciones del numero " + numeroBuscado + " es >>"+(tope+1));

        System.out.println("");

        //Mostramos el arreglo de posiciones
        indice = 0;
        System.out.println("Arreglo de Posiciones");
        for(int i = 0; i<=tope ; i++){
            System.out.print((indice!=tope)? arregloPosiciones[i]+", ":arregloPosiciones[i]);
        }
        System.out.println("");

    }

}


```

## Tema 4 : Arreglo de Caracteres

```java
package main;

import java.util.Scanner;

public class Main {

    public static void main(String[] args) {

        Scanner consola = new Scanner(System.in);

        final int CANTIDAD_CARACTERES = 10;
        char[] simbolos = new char[CANTIDAD_CARACTERES];
        int contador = 0;

        String frase,letraString;

        System.out.print("Ingrese la frase de "+CANTIDAD_CARACTERES+" caracteres : >>");
        frase = consola.nextLine();
        simbolos = frase.toCharArray();

        System.out.print("Ingrese un caracter: >>");
        letraString = consola.nextLine();

        char letraChar = letraString.charAt(0);
        letraChar = Character.toLowerCase(letraChar);

        for(char simbolo : simbolos){
            if(Character.toLowerCase(simbolo) == letraChar){
                contador++;
            }
        }

        System.out.println("El caracter "+letraChar+" aparece "+contador+ ((contador==1)? " vez":" veces"));
    }

}

```

## Tema 5 : Numeros aleatorios

```java
package main;

import java.util.Scanner;
import java.util.Random;

public class Main {

    public static void main(String[] args) {

        var consola = new Scanner(System.in);
        var numerosAleatorios = new Random();

        int arreglo[] = new int[10];

        int numero;


//        PRIMERA FORMA
/*
        //Darle valor al arregloInicial
        for (int i = 0; i < arreglo.length; i++) {


            boolean estadoWhile = true;
            while (estadoWhile) {

                arreglo[i] = numerosAleatorios.nextInt(10) + 1;

                boolean esIgual = false;
                for (int j = 0; j < i; j++) {
                    if (arreglo[i] == arreglo[j]) {
                        esIgual = true;
                    }
                }

                if(esIgual==false){estadoWhile = false;}

            }

        }
*/

//      SEGUNDA FORMA
        for(int i = 0; i < arreglo.length; i++){
            numero = numerosAleatorios.nextInt(10)+1;

            int j=0;
            while(j<i){
                if(arreglo[j]==numero){
                    j=0;
                    numero=numerosAleatorios.nextInt(10);
                }else{
                    j++;
                }
            }

            arreglo[i] = numero;
        }

        System.out.println("Lista de numeros del arreglo: ");

        int indice = 0;
        for(int valor : arreglo){
            System.out.print((indice!=arreglo.length-1)? valor+", " : valor);
            indice++;
        }
        System.out.println("");
    }
}

```

## Tema 6 : Letras Aleatorias

```java
package main;

import java.util.Random;

public class Main {
    /*Generaremos letras aleatorias a través del codigo ASCII*/
    /*
    Letra en mayusculas al azar : generar un numero entre 65 y 90
    Letra en minuscula al azar : generar un numero entre 97 y 122
    */
    public static void main(String[] args) {

        int numero,min,max;
        var aleatorio = new Random();
        char letra;


        /*
        COMO OBTENER UN NUMERO ALEATORIO ENTRE UN RANGO
        - Supone que tu rango es 10 - 25
        => El numero de datos que hay en ese rango es 25-10+1 = 15 posibles datos
        => De modo que generariamos un numero random entre 0 y 15 + 1 [Para que Java tenga en cuenta el 15]
        => Así que si a ese le sumamos el minimo, obtendriamos un numero entre 10 y 25
        - 0+10  = 10
        - 15+10 = 25
        */

        // Generar numeros aleatorios entre 65 y 90
        min = 65;
        max = 90;

        numero = aleatorio.nextInt((max-min)+1) + min;

        //Pasamos el numero a letra para pasarlo a un caracter
        letra = (char)numero;

        //Lo imprimimos
        System.out.println("letra = " + letra);

    }
}

```

## Tema 7 : Arreglos Bidimensionales

```java
package main;

import java.util.Random;

public class Main {

    public static void main(String[] args) {

        var aleatorio = new Random();

        int filas = 5;
        int columnas = 4;

        //Creamos nuestro arreglo bidimensional
        char[][] tablaLetras = new char[filas][columnas];

        //Le damos valores random
        for (int i = 0; i < filas; i++) {
            for (int j = 0; j < columnas; j++) {
                tablaLetras[i][j] = (char) (aleatorio.nextInt(90 - 65 + 1) + 65);
            }
        }

        //Imprimimos la tabla o arreglo bidimensional
        for (int i = 0; i < filas; i++) {
            for (int j = 0; j < columnas; j++) {
                System.out.print(tablaLetras[i][j] + "\t");
            }
            System.out.println("");
        }

    }
}

```

## Tema 8: Proyecto 21 Cartas

```java
package main;

import java.util.Random;
import java.util.Scanner;

/*
Autor: Carlos Andrés Hernandez Agudelo
 */
//EXPLICACION

/*
¿ Que se quiere hacer?
Un programa que replique el  Truco de las 21 cartas , de forma tal que el programa adivine cual carta es la que el usuario eligio, tal como sucede con el truco de cartas en la vida real.

=> Explicación del truco de las 21 Cartas

1. Colocar las cartas en tres columnas de forma aleatoria, cada columna con 7 cartas, para un total de 21 cartas
2. El espectador dice en que numero de columna esta la carta
3. Juntar las cartas en tres montones sin desordenarlas
4. Poner el monton de cartas que dijo el espectador en el medio
5. Repartir el mazo de la siguiente manera:  tomar el mazo y poner la primera
carta en la columna 1, la segunda en la columna 2, la
tercera en la columna 3, luego la cuarta en la columna 1,
la quinta en la columna 2, la sexta en la columna 3, y así
hasta el final.
6. El espectador dice en que numero de columna esta la carta
7. Volver a repetir los pasos del 3 al 6 dos veces más.
8. La carta del espectador sera la #11, es decir la tercera carta de la segunda columna
 */
//CODIGO

/*
    -> Letras de la A a la U en codigo ASCII : 65 - 85
 */
public class Main {

    public static void main(String[] args) {

        //Inicializamos Scanner y Random
        var consola = new Scanner(System.in);
        var aleatorios = new Random();

        //CONSTANTES PARA ESTANDARIZAR LOS VALORES DEL PROGRAMA
        final short MAX_TARJETAS_GRUPO = 7; //Tarjetas por grupo

        final short MAX_GRUPOS = 3; //Cantidad de grupos (o columnas)

        final short MAX_TARJETAS = MAX_TARJETAS_GRUPO * MAX_GRUPOS; //Total de tarjetas.

        final short MIN_TARJETA_VALOR = 'A'; //Tarjeta incial, en este caso letra A.

        final short MAX_TARJETA_VALOR = (char) (MAX_TARJETAS + (int) ('A') - 1); //Tarjeta final, la U.

        //Variables que deben usarse para resolver el problema.
        char[] grupo1 = new char[MAX_TARJETAS_GRUPO],
                grupo2 = new char[MAX_TARJETAS_GRUPO],
                grupo3 = new char[MAX_TARJETAS_GRUPO];

        //deck servira para poner el monto de cartas aquí
        char[] deck = new char[MAX_TARJETAS];

        //GENERAR LETRAS AL AZAR Y SIN REPETIR EN EL DECK
        for (int i = 0; i < MAX_TARJETAS; i++) {

            while (true) {

                int numero = (aleatorios.nextInt((int) MAX_TARJETA_VALOR - (int) MIN_TARJETA_VALOR + 1) + (int) MIN_TARJETA_VALOR);

                deck[i] = (char) numero;

                boolean esIgual = false;

                for (int j = 0; j < i; j++) {
                    if (deck[i] == deck[j]) {
                        esIgual = true;
                    }
                }

                if (esIgual == false) {
                    break;
                }
            }
        }

        //ASIGNAR A CADA GRUPO ( O COLUMNA) SUS RESPECTIVAS CARTAS SACADAS DEL DECK
        // Esto es simple, se recorre el arreglo deck hasta el final. Las primeras 7 celdas se copian a grupo1, las otras 7 a grupo2 y las últimas 7 a grupo3.
        int indice = 0;
        int grupo = 1;
        /*
            => Primeras siete cartas
            indice = 0,1,2,3,4,5,6
            grupo = 1;
            => Segundas siete cartas
            indice = 0,1,2,3,4,5,6
            grupo = 2;
            => Terceras siete cartas
            indice = 0,1,2,3,4,5,6
            grupo = 3;
         */
        for (char tarjeta : deck) {

            //Asignamos la tarjeta a su grupo correspondiente
            if (grupo == 1) {
                grupo1[indice] = tarjeta;
            }
            if (grupo == 2) {
                grupo2[indice] = tarjeta;
            }
            if (grupo == 3) {
                grupo3[indice] = tarjeta;
            }

            //Le sumamos uno a indice
            indice++;
            //Si indice ya llego a su limite (cada 7 cartas) entonces reiniciammos indice a 0y le sumamos uno al grupo;
            if (indice == 7) {
                indice = 0;
                grupo++;
            }
        }


        /*
        //PRUEBA : Sirve para saber si el anterior algoritmo realmente cumple con su funcion, asignar a cada grupo sus correspondientes cartas sacadas del deck.
        //Imprimir el grupo 1
        for(char valor : grupo1){
            System.out.print(valor + " ");
        }
        System.out.println("");
        //Imprimir el grupo 2
        for(char valor : grupo2){
            System.out.print(valor + " ");
        }
        System.out.println("");
        //Imprimir el grupo 3
        for(char valor : grupo3){
            System.out.print(valor + " ");
        }
         */
        //YA CON LAS CARTAS EN LOS GRUPOS, PODEMOS MOSTRARSELAS AL USUARIO
        //Imprimimos el mensaje inicial
        System.out.println("Haremos 3 secuencias. Empecemos...");

        //Como son tres veces que debemos hacer lo mismo, hacemos un for que repita lo mismo tres veces
        for (int i = 0; i < 3; i++) {

            //Imprimimos el numero de secuencia
            System.out.println("Secuencia " + (i + 1) + "\n");

            //I. Se muestran los 3 grupos en pantalla intercalando las letras de modo que cada grupo aparezca en una columna. Esto se logra simplemente imprimiendo los tres arreglos a la vez, primero la celda de grupo1, luego la de grupo2 y finalmente la de grupo3.
            for (int j = 0; j < MAX_TARJETAS_GRUPO; j++) {
                System.out.println("\t\t" + grupo1[j] + "  " + grupo2[j] + "  " + grupo3[j]);
            }
            System.out.println("");

            //II. Se entra en un bucle para pedir el número de grupo.
            //i. Si la opción ingresada no es correcta (1, 2 o 3) se repite este bucle.
            int opcion;
            do {
                System.out.print("En que grupo esta tu tarjeta [1,2,3]: ");
                opcion = consola.nextInt();
                consola.nextLine();
            } while ((opcion != 1) && (opcion != 2) && (opcion != 3));

            //Según la opción ingresada se vuelven a poner los grupos en deck manteniendo el orden de sus letras, de forma que el grupo en que está la letra elegida quede en medio.
            /*
            Opcion del espectador es 1 : Primero colocamos en el deck el monto del grupo 2, luego el monto del grupo 1 (que debe quedar en el medio) y finalmente el monto del grupo 3

            Opcion del espectador es 2: Primero colocamos en el deck el monto del grupo 3, luego el monto del grupo 2 (que debe quedar en el medio) y finalmente el monto del grupo 1

            Opcion del espectador es 3: Primero colocamos en el deck el monto del grupo 1, luego el monto del grupo 3 (que debe quedar en el medio) y finalmente el monto del grupo 2
             */
            int numeroCarta = 0;
            switch (opcion) {
                case 1:
                    for (int j = 0; j < 3; j++) {
                        //Primero  colocamos las cartas del grupo 2
                        if (j == 0) {
                            for (char carta : grupo2) {
                                deck[numeroCarta] = carta;
                                numeroCarta++;
                            }
                        }
                        //colocamos las cartas del grupo 1
                        if (j == 1) {
                            for (char carta : grupo1) {
                                deck[numeroCarta] = carta;
                                numeroCarta++;
                            }
                        }
                        //colocamos las cartas del grupo 3
                        if (j == 2) {
                            for (char carta : grupo3) {
                                deck[numeroCarta] = carta;
                                numeroCarta++;
                            }
                        }
                    }
                    break;
                case 2:
                    for (int j = 0; j < 3; j++) {
                        //Primero  colocamos las cartas del grupo 2
                        if (j == 0) {
                            for (char carta : grupo3) {
                                deck[numeroCarta] = carta;
                                numeroCarta++;
                            }
                        }
                        //colocamos las cartas del grupo 1
                        if (j == 1) {
                            for (char carta : grupo2) {
                                deck[numeroCarta] = carta;
                                numeroCarta++;
                            }
                        }
                        //colocamos las cartas del grupo 3
                        if (j == 2) {
                            for (char carta : grupo1) {
                                deck[numeroCarta] = carta;
                                numeroCarta++;
                            }
                        }
                    }
                    break;
                case 3:
                    for (int j = 0; j < 3; j++) {
                        //Primero  colocamos las cartas del grupo 2
                        if (j == 0) {
                            for (char carta : grupo1) {
                                deck[numeroCarta] = carta;
                                numeroCarta++;
                            }
                        }
                        //colocamos las cartas del grupo 1
                        if (j == 1) {
                            for (char carta : grupo3) {
                                deck[numeroCarta] = carta;
                                numeroCarta++;
                            }
                        }
                        //colocamos las cartas del grupo 3
                        if (j == 2) {
                            for (char carta : grupo2) {
                                deck[numeroCarta] = carta;
                                numeroCarta++;
                            }
                        }
                    }
                    break;
            }

            //MOVEMOS LAS LETRAS DEL DECK A CADA UNO DE LOS GRUPOS DE FORMA INTERCALADA
            /* Es decir, tomará el mazo (deck) y pondrá la primera
                carta en la columna 1, la segunda en la columna 2, la
                tercera en la columna 3, luego la cuarta en la columna 1,
                la quinta en la columna 2, la sexta en la columna 3, y así
                hasta el final.*/
            int numeroGrupo = 1;
            int numeroCartaGr1 = 0;
            int numeroCartaGr2 = 0;
            int numeroCartaGr3 = 0;

            for (int j = 0; j < MAX_TARJETAS; j++) {
                //Reiniciamos el grupo para que solo intercale entre 1-3
                if (numeroGrupo == 4) {
                    numeroGrupo = 1;
                }
                //Dependiendo del grupo agregamos la carta a este y sumamos el indice del numero de carta a agregar
                if (numeroGrupo == 1) {
                    grupo1[numeroCartaGr1] = deck[j];
                    numeroCartaGr1++;
                }
                if (numeroGrupo == 2) {
                    grupo2[numeroCartaGr2] = deck[j];
                    numeroCartaGr2++;
                }
                if (numeroGrupo == 3) {
                    grupo3[numeroCartaGr3] = deck[j];
                    numeroCartaGr3++;
                }

                numeroGrupo++;
            }
        }

        System.out.println("Obviamente elegiste la " + grupo2[3]);

    }

}
```

## Tema 9: Proyecto MasterMind 1

```java
package main;

import java.util.Random;
import java.util.Scanner;
import java.util.Arrays;

/*
Proyecto MasterMind1

Resumen:
- Existe un adivinador y un Pensador, este ultimo da imagina un codigo conformado por cuatro letras que no se repiten entre la A y la H que en codigo ascci es desde el 65 hasta el 72.
- El adivinador debe decir su codigo (con el objetivo que sea igual al del pensador)
- El pensador da el numero de letras buenas (La letra existe y coincide con la posicion) y el numero de letras regulares (la letra existe y no coincide con la posicion)
- El adivinador dispone de 10 intentos

De este modo vemos que el pensador pierde cuando se acaba los intentos y gana cuando el numero de letras buenas es igual a 4.

En el juego el Pensador sera la maquina y el adivinador sera el usuario
 */

 /*
Pasos
1. Generar un array de 4 letras aleatorias sin repetir
2. Hacer un for que vaya de 0 a MAX_INTENTOS - 1 , para replicar los intentos
3. Mostrar el mensaje inicial con el numero de intento actual
4. Preguntar el codigo al usuario
5. Verificar cuales el numero de letras buenas y el numero de letras regulares
6. Verificar si el codigo del usuario es igual al codigo del pensador
6. Si no gano entonces mostrar el mensaje de que perdio, esto fuera del do while.
 */
public class Main {

    public static void main(String[] args) {
        //Random y Scanner
        Scanner consola = new Scanner(System.in);
        Random aleatorio = new Random();

        //Mensajes en el juego
        String versionJuego = "MasterMind V1.0";
        String mensajeInicial = "Dispones de 10 intentos para adivinar el codigo";
        String mensajeGanar = "EXCELENTE!!! GANASTE";
        String mensajePerder = "PERDISTE!!!";

        //Constantes para el juego
        final byte MAX_INTENTOS = 10;
        final byte LARGO_CODIGO = 4;
        final char PRIMERA_LETRA = 'A';
        final char ULTIMA_LETRA = 'H';

        //Variables para el juego
        boolean haGanado = false;

        char[] letrasPensador = new char[LARGO_CODIGO];
        char[] letrasAdivinador = new char[LARGO_CODIGO];

        //Generamos letras aleatorioas entre PRIMERA_LETRA y ULTIMA_LETRA para el arreglo letrasPensador
        for (int i = 0; i < LARGO_CODIGO; i++) {
            while (true) {
                int numero = (aleatorio.nextInt((int) ULTIMA_LETRA - (int) PRIMERA_LETRA)) + 1 + (int) PRIMERA_LETRA;
                letrasPensador[i] = (char) numero;

                boolean esIgual = false;

                for (int j = 0; j < i; j++) {
                    if (letrasPensador[i] == letrasPensador[j]) {
                        esIgual = true;
                    }
                }

                if (esIgual == false) {
                    break;
                }
            }
        }

        //PRUEBA: Verificamos que el algoritmo anterior sea correcto
        /*
        System.out.print("Codigo Pensador >>");
        for (char letra : letrasPensador) {
            System.out.print(" " + letra + " ");
        }
        System.out.println("");
        */

        //Mensajes Iniciales del Juego
        System.out.println(versionJuego);
        System.out.println(mensajeInicial);
        System.out.println("");
        //Bucle For para replicar los intentos
        for (int intento = 0; intento < MAX_INTENTOS; intento++) {

            //Declaramos e inicalizamos el numero de letras buenas y regulares a 0
            int numeroBuenas = 0;
            int numeroRegulares = 0;

            System.out.print("Codigo " + (intento + 1) + " de " + MAX_INTENTOS + " >>");

            //Variable donde almacenaremos el codigo que da el adivinador
            String codigoAdivinador;

            //Pedimos al usuario que ingrese el codigo
            codigoAdivinador = consola.nextLine();

            //Pasamos codigoAdivinador a mayusculas
            codigoAdivinador = codigoAdivinador.toUpperCase();

            //Asignamos letrasAdivinador (lista de char) el codigo almacenado en codigoAdivinador
            letrasAdivinador = codigoAdivinador.toCharArray();

            //Vemos cual es el numero de letras buenas
            for (int i = 0; i < LARGO_CODIGO; i++) {
                if (letrasPensador[i] == letrasAdivinador[i]) {
                    numeroBuenas++;
                }
            }

            //Vemos cual es el numero de letras regulares
            for (int i = 0; i < LARGO_CODIGO; i++) {
                for (int j = 0; j < LARGO_CODIGO; j++) {
                    if (letrasPensador[i] == letrasAdivinador[j] && i != j) {
                        numeroRegulares++;
                    }
                }
            }

            //Imprimimos el numero de letras buenas y regulares
            System.out.println("B= " + numeroBuenas + " R= " + numeroRegulares);

            //Vemos si el adivinador gano, puede ser comparando ambos arreglos o viendo si el numero de letras buenas es igual a 4
            if (Arrays.equals(letrasPensador, letrasAdivinador)) {
                haGanado = true;
                System.out.println(mensajeGanar);
                break;
            }
        }

        if (!haGanado) {
            System.out.print(mensajePerder + " El codigo era ");
            for (char letra : letrasPensador) {
                System.out.print(letra);
            }
            System.out.println("");
        }

    }
}
```

## Tema 10: Proyecto Mastermind 2

```java
package main;

import java.util.Random;
import java.util.Scanner;
import java.util.Arrays;

/*
Proyecto MasterMind1

Resumen:
- Existe un adivinador y un Pensador, este ultimo da imagina un codigo conformado por cuatro letras que SE PUEDEN REPETIR entre la A y la H que en codigo ascci es desde el 65 hasta el 72.
- El adivinador debe decir su codigo (con el objetivo que sea igual al del pensador)
- El pensador da el numero de letras buenas (La letra existe y coincide con la posicion) y el numero de letras regulares (la letra existe y no coincide con la posicion)
- El adivinador dispone de 10 intentos

De este modo vemos que el pensador pierde cuando se acaba los intentos y gana cuando el numero de letras buenas es igual a 4.

En el juego el Pensador sera la maquina y el adivinador sera el usuario
 */

 /*
Pasos
1. Generar un array de 4 letras aleatorias, las cuales SE PUEDEN REPETIR
2. Hacer un for que vaya de 0 a MAX_INTENTOS - 1 , para replicar los intentos
3. Mostrar el mensaje inicial con el numero de intento actual
4. Preguntar el codigo al usuario
5. Verificar cuales el numero de letras buenas y el numero de letras regulares
6. Verificar si el codigo del usuario es igual al codigo del pensador
6. Si no gano entonces mostrar el mensaje de que perdio, esto fuera del do while.
 */

 /*
EJEMPLOS: Estos ejemplos es para graficar lo que se tendra que hacer en el algoritmo

Ej 1:
    Pensador:   DBAD
    Adivinador: ABCE
    B:1     R:1

Ej 2:
    Pensador:   DBAD
    Adivinador: ABBA
    B:1     R:1

Ej 3:
    Pensador:   DBAD
    Adivinador: ADBB
    B:0     R:3

Ej 4:
    Pensador:   BABB
    Adivinador: BBBE
    B:2     R:1

Ej 1:
    Pensador:   BABB
    Adivinador: BBBB
    B:3     R:0
 */

 /*
COMO HALLAR EL NUMERO DE LETRAS BUENAS Y REGULARES
- Tenemos en cuenta que poseemos dos arreglos : letrasPensador y letrasAdivinador
- Tenemos un arreglo de indicesUsados
- Vemos cual es el numero de buenas, viendo que si la letras y la posicion es igual, pues sería una buena. Y sabiendo que si encontramos una buena, pues añadimos el indice de la letra al arrelgo indicesUsados.
- Vemos cual es el numero de regulares, haciendo un recorrido por letrasPensador y dentro de este recorremos a letrasAdivinador, de la misma forma que en el proyecto anterior, pero sabiendo que se llega a la condicion solamente si i != a cualquier indice de indicesUsados, pues estos ya fueron comparados. Si se llega a la condicion y se da el caso que la letra es Regular, se agrega el indice a indicesUsados

 */
public class Main {

    public static void main(String[] args) {
        //Random y Scanner
        Scanner consola = new Scanner(System.in);
        Random aleatorio = new Random();

        //Mensajes en el juego
        String versionJuego = "MasterMind V1.0";
        String mensajeInicial = "Dispones de 10 intentos para adivinar el codigo";
        String mensajeGanar = "EXCELENTE!!! GANASTE";
        String mensajePerder = "PERDISTE!!!";

        //Constantes para el juego
        final byte MAX_INTENTOS = 10;
        final byte LARGO_CODIGO = 4;
        final char PRIMERA_LETRA = 'A';
        final char ULTIMA_LETRA = 'H';

        //Variables para el juego
        boolean haGanado = false;

        char[] letrasPensador = new char[LARGO_CODIGO];
        char[] letrasAdivinador = new char[LARGO_CODIGO];

        //Generamos letras aleatorioas entre PRIMERA_LETRA y ULTIMA_LETRA para el arreglo letrasPensador
        for (int i = 0; i < LARGO_CODIGO; i++) {
            int numero = (aleatorio.nextInt((int) ULTIMA_LETRA - (int) PRIMERA_LETRA)) + 1 + (int) PRIMERA_LETRA;
            letrasPensador[i] = (char) numero;
        }

        //La sigueinte linea es para prueba
        //PRUEBA: Verificamos que el algoritmo anterior sea correcto
        System.out.print("Codigo Pensador >>");
        for (char letra : letrasPensador) {
            System.out.print(" " + letra + " ");
        }
        System.out.println("");

        //Mensajes Iniciales del Juego
        System.out.println(versionJuego);
        System.out.println(mensajeInicial);
        System.out.println("");
        //Bucle For para replicar los intentos
        for (int intento = 0; intento < MAX_INTENTOS; intento++) {

            //Declaramos e inicalizamos el numero de letras buenas y regulares a 0
            int numeroBuenas = 0;
            int numeroRegulares = 0;

            System.out.print("Codigo " + (intento + 1) + " de " + MAX_INTENTOS + " >>");

            //Variable donde almacenaremos el codigo que da el adivinador
            String codigoAdivinador;

            //Pedimos al usuario que ingrese el codigo
            codigoAdivinador = consola.nextLine();

            //Pasamos codigoAdivinador a mayusculas
            codigoAdivinador = codigoAdivinador.toUpperCase();

            //Asignamos letrasAdivinador (lista de char) el codigo almacenado en codigoAdivinador
            letrasAdivinador = codigoAdivinador.toCharArray();

            //Creamos un arreglo de enteros que almacene los indices de letras ya usadas al saber si es buena o regular
            int[] indicesUsados = new int[LARGO_CODIGO];
            int indiceAgregar = 0;

            //Vemos cual es el numero de letras buenas
            for (int i = 0; i < LARGO_CODIGO; i++) {
                if (letrasPensador[i] == letrasAdivinador[i]) {
                    numeroBuenas++;
                    indicesUsados[indiceAgregar] = i;
                    indiceAgregar++;
                }
            }

            //Vemos cual es el numero de letras regulares
            for (int i = 0; i < LARGO_CODIGO; i++) {
                for (int j = 0; j < LARGO_CODIGO; j++) {
                    boolean esIgual = false;

                    for (int indice : indicesUsados) {
                        if (indice == i) {
                            esIgual = true;
                        }
                    }

                    if (!esIgual) {
                        if (letrasPensador[i] == letrasAdivinador[j] && i != j) {
                            numeroRegulares++;
                            indicesUsados[indiceAgregar] = i;
                            indiceAgregar++;
                        }
                    }

                }
            }

            //Imprimimos el numero de letras buenas y regulares
            System.out.println("B= " + numeroBuenas + " R= " + numeroRegulares);

            //Vemos si el adivinador gano, puede ser comparando ambos arreglos o viendo si el numero de letras buenas es igual a 4
            if (Arrays.equals(letrasPensador, letrasAdivinador)) {
                haGanado = true;
                System.out.println(mensajeGanar);
                break;
            }
        }

        if (!haGanado) {
            System.out.print(mensajePerder + " El codigo era ");
            for (char letra : letrasPensador) {
                System.out.print(letra);
            }
            System.out.println("");
        }

    }
}
```
