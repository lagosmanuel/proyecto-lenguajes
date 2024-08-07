# Java to SimpleSem Translation Project

## Description

This project aims to study implementation techniques for mechanisms and constructors provided by an object-oriented language using Java as the source language and SimpleSem as the target language. SimpleSem is a language developed by the course, similar to assembly, designed to teach program translation. Its purpose is to provide a simplified foundation for studying the implementation of object-oriented languages. For more information on SimpleSem, refer to the [SimpleSem User Manual (spanish)](https://github.com/lagosmanuel/proyecto-lenguajes/blob/main/simplesem-manual.pdf), which offers a detailed guide on the syntax and usage of this language.

## Project Objective

The project focuses on translating Java code to SimpleSem, ensuring that the behavior of the original program is faithfully preserved in the translated version.

## Project Structure

1. **Code Translation:**
   - Translation of Java code to SimpleSem.
   - The repository contains the `.simplon` files of the translation.

## Java Class Code

Below is the code of the classes that need to be translated:

### Class `A.java`

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

### Class `B.java`

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

### Class `C.java`

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

These classes should not be translated:

### Class `Sistema.java`

```java
import java.util.Scanner;

public class Sistema {
    // THIS CLASS SHOULD NOT BE TRANSLATED! It was created for internal testing
    static Scanner input = new Scanner(System.in);
    
    /* THIS METHOD DOES NOT NEED TO BE IMPLEMENTED!!!! Assume that when it is
    used, it is translated using a SetOUT of SimpleSem */
    public static void print(int p){
        System.out.println(p);
    }

    /* THIS METHOD DOES NOT NEED TO BE IMPLEMENTED!!!! Assume that when it is
    used, it is translated using a SetIN of SimpleSem */
    public static int read(){
        return input.nextInt();
    }
}

```

### Class `Principal.java`

```java
public class Principal {

    public static void main(String[] args){

        // A oA = null;
        A oA = new A();

        Sistema.print(oA.m1());
    }
    
}
```

## Additional Exercises

The statement includes optional exercises that may improve the grade or the final exam evaluation. The optional exercises along with the corresponding Java classes are detailed below:

### Optional Exercise a: Null Reference Control

#### Class `ControlNulo.java`

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

### Optional Exercise b: Conditional Assignment

#### Class `AsignacionCondicional.java`

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

### Optional Exercise c: Chained Calls

#### Class `LlamadasEncadenadas.java`

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

### Optional Exercise d: Array Integration

#### Class `Arreglos.java`

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

## License

This project is licensed under the GNU General Public License (GPL). See the [LICENSE](LICENSE) file for more details.
