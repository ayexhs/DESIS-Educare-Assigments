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
# Answer for Q4: What’s an Exception?

---

## a) Under what circumstances should a developer throw an exception?

A developer should throw an exception when an abnormal condition occurs in the program that prevents it from functioning correctly. Examples include:

1. **Invalid Input**:  
   - If a user provides an invalid value (e.g., entering a negative age or dividing by zero).

2. **Resource Issues**:  
   - When a required resource, like a file, is unavailable or inaccessible.

3. **Violations of Rules**:  
   - When certain program rules or constraints are broken, like trying to withdraw more money than the available balance in a bank account.

Throwing an exception ensures that the program can signal this abnormal condition for handling.

---

## b) Should a thrown exception always be caught?

- No, a thrown exception does not always need to be caught.

1. **When to Catch an Exception**:  
   - If the program can meaningfully handle the exception (e.g., by providing alternative logic or a recovery mechanism), it should be caught using a `try-catch` block.

2. **When Not to Catch an Exception**:  
   - If the exception is something the program cannot handle locally (like a critical system error), it can be allowed to propagate up the call stack and handled by a higher-level method or Java’s in-built exception handler.

- **Finally Block**:  
  - Even if the exception is not caught, the `finally` block will still execute, ensuring cleanup tasks (like closing files or releasing resources) are performed.

---

## c) What’s the difference between checked and unchecked exceptions?

| **Aspect**            | **Checked Exceptions**                                       | **Unchecked Exceptions**                              |
|------------------------|-------------------------------------------------------------|------------------------------------------------------|
| **Compile-Time Check** | Checked during compile time by the compiler.                | Not checked during compile time.                    |
| **Handling**           | Must be handled using a `try-catch` block or declared with `throws`. | Handling is optional and can be ignored by the programmer. |
| **Examples**           | `IOException`, `SQLException`                              | `NullPointerException`, `ArrayIndexOutOfBoundsException`, `ArithmeticException` |

---

## d) Code for Defining a Custom Exception

To create a custom exception:
- Inherit the `Exception` class or any of its child classes.
- Custom exceptions are useful for throwing and handling specific errors in the program.

### Example: Custom Exception

```java
// Defining the custom exception
class MyCustomException extends Exception {
    // Constructor to accept the custom error message
    public MyCustomException(String message) {
        super(message);
    }
}

// Using the custom exception
public class Main {
    public static void main(String[] args) {
        try {
            // Simulating a condition to throw the exception
            validateAge(-1);
        } catch (MyCustomException e) {
            // Catching and displaying the custom exception
            System.out.println("Exception caught: " + e.getMessage());
        }
    }

    // Method to validate age and throw custom exception
    public static void validateAge(int age) throws MyCustomException {
        if (age < 0) {
            throw new MyCustomException("Age cannot be negative.");
        }
    }
}
```
# Answer for Q5: Difference between Concurrency and Parallelism

---

## Concurrency
- Concurrency means handling multiple tasks at the same time by **interleaving their execution**.
- Tasks appear to run simultaneously but may not actually execute at the same time.
- Focuses on **task management** and making programs responsive.

**Example**: Typing a document while saving it in the background.

---

## Parallelism
- Parallelism means executing multiple tasks **simultaneously** using multiple CPU cores.
- Focuses on **speeding up execution** by dividing tasks and running them on different processors.
- Requires **multi-core hardware**.

**Example**: Downloading multiple files simultaneously.

---

## Key Differences

| **Feature**    | **Concurrency**                              | **Parallelism**                              |
|-----------------|---------------------------------------------|---------------------------------------------|
| **Execution**   | Tasks are interleaved, not truly simultaneous. | Tasks run simultaneously on multiple processors. |
| **Goal**        | Efficient task management.                  | Faster task execution.                      |

Concurrency manages tasks efficiently, while parallelism physically executes tasks at the same time.

# Answer for Q6: Singleton Class with Thread Safety

---

## What is a Singleton Class?
A Singleton class ensures that only a single instance of the class can be created. This is useful in scenarios where a single point of control is needed, such as managing configuration settings, database connections, etc.

---

## a) How to Ensure Only a Single Instance is Created:
1. **Private Static Variable**:  
   Use a private static variable to hold the single instance of the class.
2. **Private Constructor**:  
   Make the constructor private to prevent external instantiation.
3. **Public Static Method**:  
   Provide a public static method to return the single instance.

---

## b) What if Multiple Threads Try to Create the Class?
1. **Thread Safety with `synchronized`**:  
   Use the `synchronized` keyword in the method that creates the instance to prevent multiple threads from creating multiple instances.
2. **Double-Checked Locking**:  
   To improve performance, synchronize only during the first instance creation using double-checked locking.

---

## Code: Singleton Class with Thread Safety

```java
class Singleton {
    // Static variable to hold the single instance of the class
    private static Singleton instance;

    // Private constructor to prevent creating new objects from outside
    private Singleton() {}

    // Public method to provide the single instance, synchronized for thread safety
    public static synchronized Singleton getInstance() {
        if (instance == null) { // Create instance if it doesn't exist
            instance = new Singleton();
        }
        return instance;
    }

    // Example method to demonstrate the Singleton behavior
    public void showMessage() {
        System.out.println("This is a Singleton instance: " + this);
    }
}

public class Main {
    public static void main(String[] args) {
        // Accessing the Singleton instance
        Singleton singleton1 = Singleton.getInstance();
        singleton1.showMessage();

        Singleton singleton2 = Singleton.getInstance();
        singleton2.showMessage();

        // Both instances are the same
        System.out.println(singleton1 == singleton2); // Output: true
    }
}
```
# Q7: Java Application for Employee Data Handling
## Code Implementation

```java
import java.io.*;
import java.util.*;

// Employee Class
class Employee {
    private int id;
    private String name;
    private double salary;

    // Constructor
    public Employee(int id, String name, double salary) {
        this.id = id;
        this.name = name;
        this.salary = salary;
    }

    // Getters
    public int getId() {
        return id;
    }

    public String getName() {
        return name;
    }

    public double getSalary() {
        return salary;
    }

    // toString method for formatted output
    @Override
    public String toString() {
        return id + ", " + name + ", " + salary;
    }
}

// Main Class
public class Main {
    public static void main(String[] args) {
        // Create employee data
        List<Employee> employees1 = Arrays.asList(
            new Employee(1, "Alice", 50000),
            new Employee(2, "Bob", 60000),
            new Employee(3, "Charlie", 70000)
        );

        List<Employee> employees2 = Arrays.asList(
            new Employee(4, "David", 55000),
            new Employee(5, "Eva", 65000),
            new Employee(6, "Frank", 75000)
        );

        // Save employee data to files
        saveToFile(employees1, "employees1.txt");
        saveToFile(employees2, "employees2.txt");

        // Create threads to read from files
        Thread thread1 = new Thread(() -> readFromFile("employees1.txt"), "File1-Thread");
        Thread thread2 = new Thread(() -> readFromFile("employees2.txt"), "File2-Thread");

        thread1.start();
        thread2.start();
    }

    // Method to save employees to a file without throwing IOException
    public static void saveToFile(List<Employee> employees, String fileName) {
        try (BufferedWriter writer = new BufferedWriter(new FileWriter(fileName))) {
            for (Employee employee : employees) {
                writer.write(employee.toString());
                writer.newLine();
            }
        } catch (Exception e) {
            System.out.println("Error writing to file: " + e.getMessage());
        }
    }

    // Method to read from a file without throwing IOException
    public static void readFromFile(String fileName) {
        try (BufferedReader reader = new BufferedReader(new FileReader(fileName))) {
            String line;
            while ((line = reader.readLine()) != null) {
                System.out.println(Thread.currentThread().getName() + ": " + line);
            }
        } catch (Exception e) {
            System.out.println("Error reading file: " + e.getMessage());
        }
    }
}




