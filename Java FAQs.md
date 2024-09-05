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
