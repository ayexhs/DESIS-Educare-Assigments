# Assignment Questions

---

## Question 1: Key Differences Between JDK, JRE, and JVM

### **JDK (Java Development Kit):**
1. It is used by developers to create and compile Java programs.
2. Includes tools like the Java compiler (`javac`), debugger, and JRE.

### **JRE (Java Runtime Environment):**
1. Used to run Java applications.
2. Includes the Java Virtual Machine (JVM) and libraries but does not have tools for development (like `javac`).

### **JVM (Java Virtual Machine):**
1. It runs the compiled Java bytecode.
2. Converts bytecode into machine code and ensures Java programs run the same way on any platform.

---

## Question 2: Garbage Collection Process in Java

Garbage Collection (GC) in Java is an automatic process where unused objects are removed from memory to free up space for new ones. It helps in managing memory efficiently, so we don’t have to manually delete objects, as is the case in some other programming languages. 

The GC runs in the background as a **Daemon Thread**, meaning it works quietly without disturbing the program.

### **Memory Management in Java**

Java divides the memory (heap) into three main sections:

1. **Eden Space**:  
   - This is where new objects are created.  
   - It’s like the first stop for all objects.

2. **Survivor Spaces (S0 and S1)**:  
   - If objects survive for a while in Eden (they are still in use after some time), they are moved to these spaces.

3. **Old Generation**:  
   - Long-lived objects, like those used throughout the program, are eventually moved here.

### **Garbage Collection Steps**
1. **Mark**: The GC identifies which objects are still being used.  
2. **Sweep**: It removes the objects that are no longer needed, reclaiming memory.  
3. **Compact**: After cleaning, it may reorganize the remaining objects to optimize memory usage.

### **When is an Object Eligible for Garbage Collection?**
1. You set the object’s reference to `null` (e.g., `myObject = null;`).
2. The reference is reassigned to another object (e.g., `myObject = anotherObject;`).
3. The object was created inside a method, and the method has finished running.
4. It’s an anonymous object, meaning it was created without a name (e.g., `new MyClass();`).

### **Types of Garbage Collection in Java**
Java offers different strategies for garbage collection, depending on your program’s needs:

1. **Serial GC**:  
   - Works step-by-step and is best for simple programs.

2. **Parallel GC**:  
   - Uses multiple threads to clean up faster, ideal for larger programs.

3. **Concurrent Mark Sweep (CMS)**:  
   - Focuses on reducing pause times, so your program keeps running smoothly during GC.

4. **G1 GC**:  
   - Splits the memory into smaller chunks and cleans the most important parts first, making it great for big applications.

---

## Question 3: Compile-Time and Run-Time Polymorphism in Java

Polymorphism is a concept that explains how a single task can be performed in multiple ways. In simple terms, it allows one action to behave differently depending on the context. The word "polymorphism" itself means "many forms."

### **Types of Polymorphism in Java**

1. **Compile-Time Polymorphism (Method Overloading):**
   - Happens during the compilation of the program.
   - Involves having multiple methods with the same name but different parameter lists (number, type, or order of parameters).
   - Allows you to perform similar operations in slightly different ways.

#### **Example: Compile-Time Polymorphism**
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
```

## Run-Time Polymorphism
- Run-time polymorphism is achieved through **method overriding**, where a **child class** provides its own implementation of a method in the **parent class**.
- **Key Points:**
  1. Also known as **method overriding**.
  2. It happens during the **execution of the program (runtime)**.
  3. Allows a child class to provide its own version of a method that is already defined in its parent class.
  4. Implements the concept of **dynamic method dispatch**, where the method that gets called is determined by the **object type** (not the reference type).

---

### Example: Run-Time Polymorphism
```java
class Animal {
    void sound() {
        System.out.println("Animals make sounds");
    }
}

class Dog extends Animal {
    @Override
    void sound() {
        System.out.println("Dogs bark");
    }
}

public class Main {
    public static void main(String[] args) {
        Animal myAnimal = new Dog(); // Reference of parent, object of child
        myAnimal.sound(); // Calls the overridden method in Dog class
    }
}
```



