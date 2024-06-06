
# Upcasting and Downcasting

In Java, upcasting and downcasting are techniques related to type conversion between a subclass and its superclass. These concepts are essential for understanding how polymorphism works in Java. Here's a detailed explanation of both:

### Upcasting

Upcasting is the process of converting a subclass type to a superclass type. It is done implicitly by the Java compiler. Upcasting is safe and doesn't require explicit casting. The primary purpose of upcasting is to achieve polymorphism.

#### Example:
```java
class Animal {
    void makeSound() {
        System.out.println("Animal sound");
    }
}

class Dog extends Animal {
    void makeSound() {
        System.out.println("Bark");
    }
    
    void fetch() {
        System.out.println("Fetches ball");
    }
}

public class Main {
    public static void main(String[] args) {
        Dog dog = new Dog();
        Animal animal = dog; // Upcasting
        animal.makeSound();  // Outputs: Bark
    }
}
```

In this example, the `Dog` object is upcast to an `Animal` reference. Even though the reference type is `Animal`, the actual object is still a `Dog`, and it calls the overridden `makeSound` method in the `Dog` class.

### Downcasting

Downcasting is the process of converting a superclass type to a subclass type. It requires an explicit cast and can be risky because it can lead to a `ClassCastException` if the object being cast is not actually an instance of the subclass.

#### Example:
```java
class Animal {
    void makeSound() {
        System.out.println("Animal sound");
    }
}

class Dog extends Animal {
    void makeSound() {
        System.out.println("Bark");
    }
    
    void fetch() {
        System.out.println("Fetches ball");
    }
}

public class Main {
    public static void main(String[] args) {
        Animal animal = new Dog(); // Upcasting
        Dog dog = (Dog) animal;    // Downcasting
        dog.fetch();               // Outputs: Fetches ball
    }
}
```

In this example, the `Animal` reference is downcast back to a `Dog` reference. This allows access to methods specific to the `Dog` class, like `fetch`.

#### Unsafe Downcasting Example:
```java
public class Main {
    public static void main(String[] args) {
        Animal animal = new Animal(); 
        Dog dog = (Dog) animal;    // Unsafe downcasting
        dog.fetch();               // Throws ClassCastException
    }
}
```

In this case, the `Animal` object is not actually a `Dog`, so attempting to downcast it to `Dog` results in a `ClassCastException`.

### Key Points

- **Upcasting:**
  - Converts a subclass type to a superclass type.
  - Implicit and safe.
  - Used for achieving polymorphism.

- **Downcasting:**
  - Converts a superclass type to a subclass type.
  - Explicit and potentially unsafe.
  - Requires explicit casting and runtime type checking.

Understanding these concepts is crucial for working with inheritance and polymorphism in Java, enabling you to write more flexible and reusable code.

# Object classes and Object clss methods

In Java, the `Object` class is the root of the class hierarchy. Every class has `Object` as a superclass. All objects, including arrays, implement the methods of this class. This class provides general-purpose methods that are fundamental to all Java objects.

### Key Methods of the `Object` Class

Here are some of the most commonly used methods provided by the `Object` class:

1. **`equals(Object obj)`**:
   - Compares this object to the specified object for equality.
   - The default implementation compares memory addresses, but it can be overridden to compare the values of the object's fields.

   ```java
   @Override
   public boolean equals(Object obj) {
       if (this == obj) return true;
       if (obj == null || getClass() != obj.getClass()) return false;
       MyClass myClass = (MyClass) obj;
       return this.field == myClass.field;
   }
   ```

2. **`hashCode()`**:
   - Returns a hash code value for the object.
   - It is used in hashing-based collections like `HashMap`, `HashSet`, etc.
   - If `equals` is overridden, `hashCode` should also be overridden to maintain the general contract for the `hashCode` method.

   ```java
   @Override
   public int hashCode() {
       return Objects.hash(field);
   }
   ```

3. **`toString()`**:
   - Returns a string representation of the object.
   - The default implementation returns a string consisting of the class name followed by the "@" character and the object's hash code in hexadecimal.

   ```java
   @Override
   public String toString() {
       return "MyClass{" +
               "field=" + field +
               '}';
   }
   ```

4. **`getClass()`**:
   - Returns the runtime class of the object.
   - It is useful for reflection, where you want to analyze or manipulate the object at runtime.

   ```java
   Class<?> clazz = obj.getClass();
   System.out.println("Class name: " + clazz.getName());
   ```

5. **`clone()`**:
   - Creates and returns a copy of this object.
   - The class must implement the `Cloneable` interface and override the `clone` method to make it public.

   ```java
   @Override
   protected Object clone() throws CloneNotSupportedException {
       return super.clone();
   }
   ```

6. **`finalize()`**:
   - Called by the garbage collector on an object when garbage collection determines that there are no more references to the object.
   - It is used to perform cleanup before the object is reclaimed by the garbage collector.

   ```java
   @Override
   protected void finalize() throws Throwable {
       try {
           // Cleanup code
       } finally {
           super.finalize();
       }
   }
   ```

7. **`notify()`**:
   - Wakes up a single thread that is waiting on this object's monitor.
   - Used in multithreading to signal that a condition has changed.

   ```java
   synchronized (obj) {
       obj.notify();
   }
   ```

8. **`notifyAll()`**:
   - Wakes up all threads that are waiting on this object's monitor.
   - Used to signal all waiting threads that a condition has changed.

   ```java
   synchronized (obj) {
       obj.notifyAll();
   }
   ```

9. **`wait()`**:
   - Causes the current thread to wait until another thread invokes the `notify` or `notifyAll` method for this object.
   - There are overloaded versions of this method that allow waiting for a specified amount of time.

   ```java
   synchronized (obj) {
       while (condition) {
           obj.wait();
       }
   }
   ```

These methods are fundamental to how Java handles objects and provide essential functionality for equality checks, object representation, concurrency, and more.


# Superclass

In Java, the superclass of all classes is the `Object` class. It is the root of the class hierarchy, and every class, directly or indirectly, inherits from `Object`. This means that all classes, whether they are user-defined or part of the Java API, are descendants of `Object`.

Here are a few key points about the `Object` class:

1. **Universal Superclass**: Every class in Java implicitly extends `Object` if no other superclass is explicitly defined. For example:
   ```java
   public class MyClass {
       // This class implicitly extends Object
   }
   ```

2. **Methods Inherited by All Classes**: All classes inherit the methods of `Object`, such as `equals()`, `hashCode()`, `toString()`, `getClass()`, `clone()`, `finalize()`, `notify()`, `notifyAll()`, and `wait()`.

3. **Fundamental Methods**: The methods provided by the `Object` class are fundamental to how Java objects work, enabling functionality such as object comparison, synchronization, and reflection.

### Example Demonstrating Inheritance from Object

Here's an example demonstrating how every class inherits from `Object`:

```java
class MyClass {
    private int value;

    MyClass(int value) {
        this.value = value;
    }

    @Override
    public String toString() {
        return "MyClass{" +
                "value=" + value +
                '}';
    }
}

public class Main {
    public static void main(String[] args) {
        MyClass myObject = new MyClass(10);
        
        // Methods inherited from Object
        System.out.println(myObject.toString());       // MyClass{value=10}
        System.out.println(myObject.hashCode());       // Hash code of the object
        System.out.println(myObject.equals(myObject)); // true
        System.out.println(myObject.getClass().getName()); // MyClass
    }
}
```

In this example, `MyClass` inherits the `toString()`, `hashCode()`, `equals()`, and `getClass()` methods from `Object`. Even though `MyClass` doesn't explicitly extend any class, it still implicitly extends `Object`.


