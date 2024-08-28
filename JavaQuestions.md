# Java Interview Questions and Answers

## OOP

### Explain OOP Concepts

**Object-Oriented Programming (OOP)** is a programming paradigm based on the concept of "objects," which can contain data and methods. The four main principles of OOP are:

1. **Encapsulation**: Bundles data and methods that operate on the data within a single unit (class) and restricts access to some of the object's components.
   - **Example**:
     ```java
     public class Person {
         private String name;

         public String getName() {
             return name;
         }

         public void setName(String name) {
             this.name = name;
         }
     }
     ```

2. **Inheritance**: Allows a new class to inherit properties and methods from an existing class.
   - **Example**:
     ```java
     public class Animal {
         public void eat() {
             System.out.println("This animal eats food.");
         }
     }

     public class Dog extends Animal {
         public void bark() {
             System.out.println("The dog barks.");
         }
     }
     ```

3. **Polymorphism**: Allows methods to do different things based on the object it is acting upon.
   - **Example**:
     ```java
     public class Animal {
         public void makeSound() {
             System.out.println("Animal makes a sound.");
         }
     }

     public class Dog extends Animal {
         @Override
         public void makeSound() {
             System.out.println("Dog barks.");
         }
     }
     ```

4. **Abstraction**: Hides complex implementation details and shows only the necessary features of an object.
   - **Example**:
     ```java
     public abstract class Shape {
         abstract void draw();
     }

     public class Circle extends Shape {
         @Override
         void draw() {
             System.out.println("Drawing a circle.");
         }
     }
     ```

### Differences Between Abstract Classes and Interfaces

- **Abstract Classes**:
  - Can have both abstract and concrete methods.
  - Can have state (fields).
  - Can have constructors.
  - **Example**:
    ```java
    public abstract class Animal {
        abstract void makeSound();
        
        public void eat() {
            System.out.println("This animal eats food.");
        }
    }
    ```

- **Interfaces**:
  - Can only have abstract methods (Java 8+ allows default and static methods).
  - Cannot have state.
  - Cannot have constructors.
  - **Example**:
    ```java
    public interface Animal {
        void makeSound();
    }
    ```

### Difference Between Method Overloading and Overriding

- **Method Overloading**:
  - Same method name with different parameter lists in the same class.
  - **Example**:
    ```java
    public class MathOperations {
        public int add(int a, int b) {
            return a + b;
        }

        public double add(double a, double b) {
            return a + b;
        }
    }
    ```

- **Method Overriding**:
  - Subclass provides a specific implementation of a method already defined in its superclass.
  - **Example**:
    ```java
    public class Animal {
        public void makeSound() {
            System.out.println("Animal makes a sound.");
        }
    }

    public class Dog extends Animal {
        @Override
        public void makeSound() {
            System.out.println("Dog barks.");
        }
    }
    ```

### What Are the Access Modifiers You Know? What Does Each One Do?

- **private**: Accessible only within the class it is declared.
  - **Example**:
    ```java
    public class Person {
        private String name;
    }
    ```

- **default** (no keyword): Accessible only within the same package.
  - **Example**:
    ```java
    class Person {
        String name;
    }
    ```

- **protected**: Accessible within the same package and by subclasses.
  - **Example**:
    ```java
    public class Animal {
        protected void makeSound() {
            System.out.println("Animal makes a sound.");
        }
    }
    ```

- **public**: Accessible from any class.
  - **Example**:
    ```java
    public class Person {
        public String name;
    }
    ```

### Can an Interface Implement Another Interface?

Yes, an interface can extend another interface. It uses the `extends` keyword.
- **Example**:
  ```java
  public interface Animal {
      void makeSound();
  }

  public interface Pet extends Animal {
      void play();
  }
  ```

### What is Polymorphism? What About Inheritance?

- **Polymorphism**: Allows objects to be treated as instances of their parent class rather than their actual class. The method that gets executed is determined at runtime based on the object type.
- **Inheritance**: Enables a new class to inherit properties and methods from an existing class, facilitating code reusability.

## Collections and Generics

### Arrays vs ArrayLists

- **Arrays**:
  - Fixed size.
  - Can hold primitive types.
  - **Example**:
    ```java
    int[] numbers = {1, 2, 3};
    ```

- **ArrayLists**:
  - Dynamic size.
  - Can only hold objects.
  - **Example**:
    ```java
    ArrayList<Integer> numbers = new ArrayList<>();
    numbers.add(1);
    numbers.add(2);
    numbers.add(3);
    ```

### HashSet vs TreeSet

- **HashSet**:
  - Stores elements in a hash table.
  - Does not maintain order.
  - **Example**:
    ```java
    HashSet<String> set = new HashSet<>();
    set.add("Apple");
    set.add("Banana");
    ```

- **TreeSet**:
  - Stores elements in a tree structure.
  - Maintains natural order.
  - **Example**:
    ```java
    TreeSet<String> set = new TreeSet<>();
    set.add("Banana");
    set.add("Apple");
    ```

### HashMap vs Set

- **HashMap**:
  - Stores key-value pairs.
  - Allows null values and keys.
  - **Example**:
    ```java
    HashMap<String, Integer> map = new HashMap<>();
    map.put("Apple", 1);
    map.put("Banana", 2);
    ```

- **Set**:
  - Stores unique elements.
  - Does not allow duplicates.
  - **Example**:
    ```java
    Set<String> set = new HashSet<>();
    set.add("Apple");
    set.add("Banana");
    ```

### Explain Generics in Java

Generics enable classes, interfaces, and methods to operate on objects of various types while providing compile-time type safety.
- **Example**:
  ```java
  public class Box<T> {
      private T value;

      public void setValue(T value) {
          this.value = value;
      }

      public T getValue() {
          return value;
      }
  }

  Box<String> stringBox = new Box<>();
  stringBox.setValue("Hello");
  ```

## Objects and Primitives

### How is String Class Implemented? Why Was It Made Immutable?

- **Implementation**: The `String` class is implemented as a final class with an internal character array. Strings are immutable to ensure that their values remain constant after creation, which aids in security, efficiency, and thread safety.
- **Example**:
  ```java
  String s = "Hello";
  s.toUpperCase(); // returns a new String object with value "HELLO"
  ```

### What Does It Mean to Say That a String is Immutable?

It means that once a `String` object is created, its state (the sequence of characters) cannot be modified. Any operation that seems to modify the string will actually create a new string object.

### Can You List 8 Primitive Types in Java?

- `byte`
- `short`
- `int`
- `long`
- `float`
- `double`
- `char`
- `boolean`

### What is the Difference Between an Integer and int?

- **int**: A primitive data type.
- **Integer**: A wrapper class that encapsulates an `int` value and provides utility methods.
- **Example**:
  ```java
  int primitiveInt = 5;
  Integer wrapperInt = Integer.valueOf(5);
  ```

### Do Objects Get Passed by Reference or Value in Java?

Java passes object references by value. This means the reference itself is passed by value, not the actual object. Changes to the object via the reference affect the original object.

## Java Memory Model and Garbage Collector

### What is Garbage Collector? How Does it Work?

The garbage collector (GC) automatically reclaims memory used by objects that are no longer reachable or referenced. It works by identifying unused objects and freeing up the memory they occupy.

## Concurrency

### What Does the Keyword `synchronized` Mean?

The `synchronized` keyword ensures that a method or block of code can only be executed by one thread at a time, providing mutual exclusion.
- **Example**:
  ```java
  public synchronized void method() {
      // Critical section
  }
  ```

### What is a ThreadPoolExecutor?

`ThreadPoolExecutor` is a class in Java that provides a pool of threads for executing tasks. It helps in managing a pool of worker threads and is more efficient than creating a new thread for each task.

### What is Volatile Modifier?

The `volatile` modifier indicates

 that a variable's value will be updated by multiple threads. It ensures that changes made by one thread are visible to other threads immediately.

### Object Level Lock vs Class Level Lock in Java

- **Object Level Lock**: Synchronizes access to instance methods or blocks. Only one thread can access the synchronized block/method of a particular object.
- **Class Level Lock**: Synchronizes access to static methods or blocks. Only one thread can access the synchronized block/method of a class.

### Concurrency vs Parallelism

- **Concurrency**: Dealing with multiple tasks at the same time but not necessarily executing them simultaneously (e.g., multitasking).
- **Parallelism**: Executing multiple tasks simultaneously (e.g., multi-core processing).

### The Classes in the Atomic Package Expose a Common Set of Methods: `get`, `set`, `lazySet`, `compareAndSet`, and `weakCompareAndSet`. Please Describe Them.

- `get()`: Returns the current value.
- `set()`: Sets the value.
- `lazySet()`: Sets the value with minimal synchronization.
- `compareAndSet()`: Atomically sets the value if it equals the expected value.
- `weakCompareAndSet()`: Similar to `compareAndSet()` but provides weaker guarantees.

## Exceptions

### How Does the `try{}`, `catch{}`, `finally` Work?

- **try**: Contains code that may throw exceptions.
- **catch**: Catches and handles exceptions thrown by the `try` block.
- **finally**: Contains code that is always executed, regardless of whether an exception was thrown.

### What is the Difference Between a Checked Exception and an Unchecked Exception?

- **Checked Exception**: Must be either caught or declared in the method signature (e.g., `IOException`).
- **Unchecked Exception**: Does not need to be declared or caught (e.g., `NullPointerException`).

## Others

### Shallow vs. Deep Copy in Java

- **Shallow Copy**: Creates a new object but does not create copies of objects referenced by the original object.
- **Deep Copy**: Creates a new object and recursively copies all objects referenced by the original object.

### Explain Serialization and Deserialization

- **Serialization**: The process of converting an object into a byte stream.
- **Deserialization**: The process of converting a byte stream back into an object.
- **Example**:
  ```java
  ObjectOutputStream out = new ObjectOutputStream(new FileOutputStream("file.ser"));
  out.writeObject(object);
  out.close();

  ObjectInputStream in = new ObjectInputStream(new FileInputStream("file.ser"));
  MyObject obj = (MyObject) in.readObject();
  in.close();
  ```

### What is the `transient` Modifier?

The `transient` modifier prevents serialization of a field. When an object is serialized, transient fields are not included in the serialized representation.

### What are Anonymous Classes?

Anonymous classes are classes without a name that are used to instantiate objects with certain behavior on the fly.

### What is the Difference Between Using `==` and `.equals()` on an Object?

- `==` compares object references (memory addresses).
- `.equals()` compares object content (if overridden).

### What is the `hashCode()` and `equals()` Used For?

- **`hashCode()`**: Provides a hash code representation of an object, used in hash-based collections.
- **`equals()`**: Compares two objects for logical equality.

### When Would You Make an Object Value `final`?

Make a variable `final` when its value should not be changed after initialization.

### What are the `final`, `finally`, and `finalize` Keywords?

- **`final`**: Used to declare constants, methods that cannot be overridden, and classes that cannot be subclassed.
- **`finally`**: Used in exception handling to execute a block of code regardless of whether an exception is thrown.
- **`finalize`**: A method called by the garbage collector before an object is removed from memory.

### What is the Difference Between `throw` and `throws` Keyword in Java?

- **`throw`**: Used to explicitly throw an exception.
- **`throws`**: Used in method signatures to declare that a method can throw exceptions.

### What Does the `static` Word Mean in Java?

The `static` keyword indicates that a variable or method belongs to the class rather than instances of the class. Static members are shared across all instances of the class.

### Can a Static Method Be Overridden in Java?

Static methods cannot be overridden. They can be hidden in a subclass, but the subclass’s static method does not override the parent class’s static method.

### When is a Static Block Run?

A static block is executed when the class is first loaded into memory.

### Explain Reflection in Java

Reflection is an API that allows programs to examine and modify the runtime behavior of applications. It can be used to access and manipulate classes, methods, and fields dynamically.

### What is Dependency Injection?

Dependency Injection is a design pattern where an object receives its dependencies from an external source rather than creating them itself. This promotes loose coupling and easier testing.

### Difference Between `StringBuffer` and `StringBuilder`

- **`StringBuffer`**: Thread-safe and synchronized, used in multi-threaded scenarios.
- **`StringBuilder`**: Not synchronized, faster than `StringBuffer`, used in single-threaded scenarios.

### What is the Difference Between Fail-Fast and Fail-Safe Iterators in Java?

- **Fail-Fast**: Throws `ConcurrentModificationException` if the collection is modified while iterating.
- **Fail-Safe**: Works on a clone of the collection, does not throw exceptions if the collection is modified during iteration.

### Monitor and Synchronization

Monitors are used in Java to handle synchronization of threads. Synchronization ensures that only one thread can execute a block of code or method at a time, which prevents concurrent access issues.

