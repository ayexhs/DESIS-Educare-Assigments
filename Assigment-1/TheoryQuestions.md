-----------------------------------Question1-------------------------------
Q1. Identify and list down key differences amongst JDK, JRE and JVM.

JDK (Java Development Kit):
  1.It is used by developers to create and compile Java programs.
  2.Includes tools like the Java compiler (javac), debugger, and JRE.
JRE (Java Runtime Environment):
  1.Used to run Java applications.
  2.Includes the Java Virtual Machine (JVM) and libraries but does not have tools for development (like javac).
JVM (Java Virtual Machine):
  1.It runs the compiled Java bytecode.
  2.Converts bytecode into machine code and ensures Java programs run the same way on any platform.


-----------------------------------Question2-------------------------------
Q2. Explain the Garbage Collection process in Java with diagrams covering various generations where the
memory is managed.

->Garbage Collection (GC) in Java is an automatic process where unused objects are removed from memory to free up space for new ones. 
It helps in managing memory efficiently so that we don’t have to manually delete objects, as is the case in some other programming languages. 
The GC runs in the background as a Daemon Thread, meaning it works quietly without disturbing the program.
->Java divides the memory (heap) into three main sections:
Eden Space: This is where new objects are created. It’s like the first stop for all objects.
Survivor Spaces (S0 and S1): If objects survive for a while in Eden (they are still in use after some time), they are moved to these spaces.
Old Generation: Long-lived objects, like those used throughout the program, are eventually moved here.
->Mark: The GC identifies which objects are still being used.
Sweep: It removes the objects that are no longer needed, reclaiming memory.
Compact: After cleaning, it may reorganize the remaining objects to optimize memory usage.
->Eligibility:
1.You set the object’s reference to null (e.g., myObject = null;).
2.The reference is reassigned to another object (e.g., myObject = anotherObject;).
3.The object was created inside a method, and the method has finished running.
4.It’s an anonymous object, meaning it was created without a name (e.g., new MyClass();).
->Types of Garbage Collection in Java
Java offers different strategies for garbage collection, depending on your program’s needs:
Serial GC: Works step-by-step and is best for simple programs.
Parallel GC: Uses multiple threads to clean up faster, ideal for larger programs.
Concurrent Mark Sweep (CMS): Focuses on reducing pause times, so your program keeps running smoothly during GC.
G1 GC: Splits the memory into smaller chunks and cleans the most important parts first, making it great for big applications.


-----------------------------------QUESTION3--------------------------------
Q3. Explain the difference between Compile and Run-time polymorphism. How are both achieved in Java? Give
examples to elaborate.
Polymorphism is a concept which explains that single task can be performed in multiple ways. 
In simple terms, it allows one action to behave differently depending on the context. The word "polymorphism" itself means "many forms."

There are two main types of polymorphism in Java:
1. Compile-Time Polymorphism
    ->Also known as method overloading.
    ->It happens during the compilation of the program.
    ->Method overloading means having multiple methods with the same name but different parameter lists (number, type, or order of parameters).
    ->It allows you to perform a similar operation in slightly different ways.
```java
class Calculator {
    // Adding two integers
    int add(int a, int b) {
        return a + b;
    }

    // Adding two doubles
    double add(double a, double b) {
        return a + b;
    }
}

public class Main {
    public static void main(String[] args) {
        Calculator calc = new Calculator();
        System.out.println(calc.add(2, 3));       // Calls the int version
        System.out.println(calc.add(2.5, 3.5));  // Calls the double version
    }
}