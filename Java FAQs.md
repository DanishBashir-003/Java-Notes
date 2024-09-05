### 1. **What is the difference between `==` and `equals()` in Java?**

#### Core Theory:
- `==`: This is a reference comparison operator in Java. It checks whether two reference variables point to the same object in memory. For primitive types, `==` compares the actual values.
- `equals()`: This method is defined in the `Object` class and is meant for logical comparison. It checks whether two objects are "equal" based on the criteria defined in the class's `equals()` method. In the default implementation, `equals()` behaves the same as `==`, but many classes (e.g., `String`, `Integer`) override this method to compare object values.

#### Practical Application:
- For reference types like `String`, using `==` compares memory addresses:
  
```java
String s1 = new String("hello");
String s2 = new String("hello");

System.out.println(s1 == s2);      // false, as both refer to different objects
System.out.println(s1.equals(s2)); // true, as the content of the strings is the same
```

- For primitives, `==` works correctly:

```java
int a = 5;
int b = 5;
System.out.println(a == b); // true, compares values
```

#### Key Takeaway:
Use `==` for reference equality (whether two objects point to the same location in memory) and `equals()` for value-based comparison (whether two objects have the same content).

---

### 2. **How does garbage collection work in Java?**

#### Core Theory:
Garbage collection (GC) in Java is an automatic memory management process. Java uses a **heap** to store objects, and GC is responsible for reclaiming memory by removing objects that are no longer referenced. The JVM has several GC algorithms (e.g., Mark-and-Sweep, Generational GC) that help improve performance and minimize memory leaks.

#### Key Concepts:
- **Generational GC**: The heap is divided into three regions: Eden, Survivor (Young Generation), and Tenured (Old Generation). Most objects are short-lived and are collected in the Young Generation.
- **Finalization**: Before an object is garbage collected, its `finalize()` method is called, allowing cleanup operations.

#### Practical Application:
- Programmers don't need to explicitly manage memory, but understanding GC behavior can optimize performance, especially in memory-intensive applications.
  
```java
// Requesting GC (JVM may or may not invoke it immediately)
System.gc();

// Example of finalize() method:
class Demo {
    @Override
    protected void finalize() throws Throwable {
        System.out.println("Object is garbage collected.");
    }
}
Demo obj = new Demo();
obj = null;  // Object is no longer referenced and eligible for GC
```

#### Key Takeaway:
Java's garbage collector frees up memory automatically, improving application performance without manual intervention. However, understanding its behavior helps developers write more efficient code, especially in applications dealing with large data sets or long-running processes.

---

### 3. **What is the difference between method overloading and method overriding?**

#### Core Theory:
- **Method Overloading**: Occurs when multiple methods in the same class have the same name but different parameter lists (different types, numbers, or both). It’s a compile-time polymorphism (static binding).
- **Method Overriding**: Occurs when a subclass provides a specific implementation of a method already defined in its superclass. The overridden method in the subclass must have the same signature as the method in the superclass. It’s a runtime polymorphism (dynamic binding).

#### Practical Application:
- **Overloading Example**:
  
```java
class Calculator {
    public int add(int a, int b) {
        return a + b;
    }
    
    public double add(double a, double b) {
        return a + b;
    }
}
```

Here, the `add()` method is overloaded to accept both `int` and `double` types.

- **Overriding Example**:

```java
class Animal {
    public void sound() {
        System.out.println("Animal makes a sound");
    }
}

class Dog extends Animal {
    @Override
    public void sound() {
        System.out.println("Dog barks");
    }
}
```

In this case, `Dog` overrides the `sound()` method of `Animal` to provide a specific implementation.

#### Key Takeaway:
- **Overloading** is used for methods that perform similar tasks but require different inputs.
- **Overriding** is used when a subclass needs to provide its own behavior for an inherited method.

Here are some frequently searched Java interview questions with clear and in-depth answers:

### 1. **What is the difference between `==` and `equals()` in Java?**
   - **`==` Operator:** In Java, the `==` operator is used to compare the memory addresses of objects to check if they refer to the same instance. For primitive data types (like `int`, `char`, etc.), it compares the actual values.
   - **`equals()` Method:** The `equals()` method, defined in the `Object` class, is used to compare the contents of two objects to check if they are logically equal. For example, when comparing two `String` objects, `equals()` checks if the characters in the strings are the same, rather than comparing their memory addresses.

   **Example:**
   ```java
   String str1 = new String("hello");
   String str2 = new String("hello");

   // Using == operator
   System.out.println(str1 == str2); // Output: false

   // Using equals() method
   System.out.println(str1.equals(str2)); // Output: true
   ```

### 2. **What is the purpose of the `final` keyword in Java?**
   - **`final` Variable:** A `final` variable can be initialized only once, either when it’s declared or within a constructor. After that, it cannot be modified.
   - **`final` Method:** A method declared as `final` cannot be overridden by subclasses, ensuring that the method's behavior remains consistent across all instances.
   - **`final` Class:** A class declared as `final` cannot be extended or subclassed. This is often used to create immutable classes.

   **Example:**
   ```java
   final class ImmutableClass {
       final int value = 10;

       final void display() {
           System.out.println("Value: " + value);
       }
   }

   // The following code will cause a compilation error:
   // class SubClass extends ImmutableClass { }
   ```

### 3. **What are Java’s access modifiers, and how do they work?**
   - **`private`:** The member is accessible only within its own class.
   - **`default` (no modifier):** The member is accessible only within classes in the same package.
   - **`protected`:** The member is accessible within its own package and by subclasses.
   - **`public`:** The member is accessible from any other class.

   **Example:**
   ```java
   public class AccessModifiers {
       private int privateVar = 1;
       int defaultVar = 2;
       protected int protectedVar = 3;
       public int publicVar = 4;

       public void display() {
           System.out.println("Private: " + privateVar);
           System.out.println("Default: " + defaultVar);
           System.out.println("Protected: " + protectedVar);
           System.out.println("Public: " + publicVar);
       }
   }
   ```

### 4. **What is the difference between an abstract class and an interface in Java?**
   - **Abstract Class:** An abstract class can have both abstract methods (without a body) and concrete methods (with a body). It is used when classes share common behavior but need to implement some details differently.
   - **Interface:** An interface can only have abstract methods (until Java 8, which introduced default and static methods). It is used to define a contract that implementing classes must follow, allowing for multiple inheritance (since a class can implement multiple interfaces).

   **Example:**
   ```java
   abstract class Animal {
       abstract void sound();

       void eat() {
           System.out.println("Eating...");
       }
   }

   interface Pet {
       void play();
   }

   class Dog extends Animal implements Pet {
       void sound() {
           System.out.println("Bark");
       }

       public void play() {
           System.out.println("Playing fetch");
       }
   }
   ```

### 5. **What is multithreading in Java, and how is it achieved?**
   - **Multithreading:** Multithreading in Java is a process where multiple threads run concurrently within a program to perform multiple tasks simultaneously, improving performance for tasks like web services, games, and heavy computations.
   - **How to Achieve Multithreading:** Java provides the `Thread` class and the `Runnable` interface to create and manage threads.

   **Example:**
   ```java
   class MyThread extends Thread {
       public void run() {
           for (int i = 0; i < 5; i++) {
               System.out.println(Thread.currentThread().getName() + " is running");
           }
       }
   }

   public class MultithreadingExample {
       public static void main(String[] args) {
           MyThread t1 = new MyThread();
           MyThread t2 = new MyThread();

           t1.start();
           t2.start();
       }
   }
   ```

These are some of the frequently asked Java interview questions, each explained with clear concepts and practical examples to help you prepare effectively.
