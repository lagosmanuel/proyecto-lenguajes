# Proyecto de Traducción Java a SimpleSem

## Descripción

Este proyecto tiene como objetivo estudiar técnicas de implementación para mecanismos y constructores provistos por un lenguaje orientado a objetos utilizando Java como lenguaje fuente y SimpleSem como lenguaje destino. SimpleSem es un lenguaje desarrollado por la cátedra, similar a assembly, diseñado para enseñar la traducción de programas. Su propósito es proporcionar una base simplificada para el estudio de la implementación de lenguajes orientados a objetos. Para más información sobre el lenguaje SimpleSem, se puede consultar el [Manual de Usuario de SimpleSem](https://github.com/lagosmanuel/proyecto-lenguajes/blob/main/simplesem-manual.pdf) que ofrece una guía detallada sobre la sintaxis y el uso de este lenguaje.

## Objetivo del Proyecto

El proyecto se centra en traducir código Java a SimpleSem, asegurando que el comportamiento del programa original se mantenga fiel en la versión traducida.
## Estructura del Proyecto

1. **Traducción de Código:**
   - Traducción de código Java a SimpleSem.
   - En el repositorio se encuentran los archivos .simplon de la traducción.

## Código de las Clases Java

A continuación se muestra el código de las clases que se deben traducir:

### Clase `A.java`

```java
public class A {

    static int a1 = 0;

    int v1, v2;

    public A(){
        v1 = 1;
        v2 = 20;
    }
    
    public int m1() {
        for (int i = 0; i < v1+v2; i++) {
            v1 += i; 
            v2 -= i;
            
            if ((v1+v2) >= 100){
                break;
            }
        }
        a1 = a1+1;
        return v1 + v2;  
    }
    
    public int m1(int x){
        a1 = a1+1;
        return a1;
    }
}

```

### Clase `B.java`

```java
public class B extends A {

    int v3;

    public B(){
        super();
        v3 = a1 * 3;
    }

    public int m1(){
        int j = 0;

        switch (a1) {
            case 1:
            case 2:
            case 3:
                j = 3*a1 + 1;
                break;
            case 4:
            case 5:
            case 6:
                j = v1 + 12;
                break;
            default:
                j = 1;
                break;
        }

        return super.m1(j);
    }

    public int m2(){
        a1 = a1+1;
        return (v3+a1) + super.m1() + this.m1();
    }
}

```

### Clase `C.java`

```java
public class C extends B {

    int v4, v5;
    A o1;

    public C(int x){
        super();
        v4 = x + 1;
        v5 = (v1 + v2) * 3;
        o1 = new A();
    }

    public int m1(int x){
        int t = 5;
    
        if(x < 100 || x <= (t+1)){
            this.m3();
            return t - x;
        }
        if((x > 100) & (x > t)){
            return t - x - 1;
        }

        return t * 5;
    }

    public int m2(int x) {
        int aux1 = 0;
        int aux2 = 0;
        int j = 0;
        int out = aux1;

        while (j < 30) {
            aux1 += x;
            aux2 += 3; 

            if (aux1 > 50) { 
                break;
            }
            else{
                aux2 = aux2 + 1;
            }

            j = j+1;
        }

        if(aux1 > aux2){
            out = aux2;
        }

        return out;
    }

    public void m3(){
        o1 = new A();
    }
}

```
Estas no se deben traducir:

### Clase `Sistema.java`

```java
import java.util.Scanner;

public class Sistema {
    // ESTA CLASE NO HAY QUE TRADUCIRLA! fue creada para testeo interno
    static Scanner input = new Scanner(System.in);
    
    /* ESTE METODO NO ES NECESARIO IMPLEMENTARSE!!!! asuma que cuando es
    utilizado se traduce usando un SetOUT de SimpleSem */
    public static void print(int p){
        System.out.println(p);
    }

    /* ESTE METODO NO ES NECESARIO IMPLEMENTARSE!!!! asuma que cuando es
    utilizado se traduce usando un SetIN de SimpleSem */
    public static int read(){
        return input.nextInt();
    }
}

```

### Clase `Principal.java`

```java
public class Principal {

    public static void main(String[] args){

        // A oA = null;
        A oA = new A();

        Sistema.print(oA.m1());
    }
    
}
```

## Ejercicios Adicionales

El enunciado incluye ejercicios opcionales que pueden significar una mejora en la nota de promoción o en la evaluación del examen final. A continuación se detallan estos ejercicios opcionales junto con las clases Java correspondientes:

### Ejercicio Opcional a: Control de Referencias Nulas

#### Clase `ControlNulo.java`

```java
public class Principal {

    public static void main(String[] args){

        // A oA = null;
        A oA = new A();

        Sistema.print(oA.m1());
    }
    
}

public class A {
    int v1, v2;

    public A(){
        v1 = 3;
        v2 = 2;
    }

    public int m1(){
        return v1+v2;
    }
}
```

### Ejercicio Opcional b: Asignación Condicional

#### Clase `AsignacionCondicional.java`

```java
public class Principal {
    public static void main(String[] args) {
        A o1 = new A(5);
        Sistema.print(o1.m1());

        A o2 = new A(-3);
        Sistema.print(o2.m1());
    }
    
}

public class A {
    private int v1;

    public A(int x) {
        v1 = (x > 10) ? x-10 : x;
    }

    public int m1() {
        return v1;
    }    
}

```

### Ejercicio Opcional c: Llamadas Encadenadas

#### Clase `LlamadasEncadenadas.java`

```java

public class Principal {
    public static void main(String[] args) {
        B obj = new B();

        Sistema.print(obj.m2().m1());
    }
    
}

public class A {
    int v1;

    public A(int x){
        v1 = x+100;
    }

    public int m1(){
        return v1+1;
    }
}

public class B {

    int v1;

    public B(){
        v1 = 0;
    }

    public A m2(){
        A o1 = new A(v1);
        return o1;
    }
    
}

```

### Ejercicio Opcional d: Incorporación de Arreglos

#### Clase `Arreglos.java`

```java
public class Principal {
    
    public static void main(String[] args) {
        
        A obj = new A();

        Sistema.print(obj.m1());
    }


}

public class A {
    int[] v1;

    public A(){
        v1 = new int[]{1, 2, 3, 4, 5};
    }

    public int m1(){
        int suma = 0;
        for (int i = 0; i < 5; i++) {
            suma = suma + v1[i];
        }
        return suma;
    }
}

```

## Licencia

Este proyecto está licenciado bajo la Licencia Pública General de GNU (GPL). Consulta el archivo [LICENSE](LICENSE) para más detalles.
