# System.out.println ?



When you write `System.out.println` in your Java code, you're telling your program to display some text or information on the screen. It's like saying "Hey, computer, please print this out for me!"

### Breaking It Down

1. **System**: 
   - Think of `System` as the entire computer system. It's a built-in class in Java that contains useful tools for interacting with your computer.

2. **out**: 
   - Inside the `System` class, there's an object called `out`. This object is like a messenger that knows how to send information from your program to the screen (the console).

3. **println**: 
   - This stands for "print line". It's a method (a function) that tells the `out` object to print a line of text to the screen and then move to the next line. The "ln" at the end of `println` stands for "line".

### Example with Explanation

Here’s a simple example:

```java
public class Main {
    public static void main(String[] args) {
        System.out.println("Hello, World!");
    }
}
```

- **public class Main**: This is defining a class named `Main`. Think of a class as a blueprint for creating objects or as a container for your program's code.
- **public static void main(String[] args)**: This is the main method. It's the entry point of any Java program. When you run your program, this is where it starts.
- **System.out.println("Hello, World!");**: This line tells the computer to print "Hello, World!" to the screen.

### Step-by-Step Execution

1. **System**: You’re telling the program to use the computer system’s built-in tools.
2. **out**: You’re specifying the output tool that sends messages to the screen.
3. **println**: You’re using the `println` method to print a message.
4. **"Hello, World!"**: This is the message you want to print. It’s enclosed in double quotes because it’s a string (a piece of text).

### Visualization

Imagine you have a loudspeaker (the console). The `System.out` is like the microphone connected to the loudspeaker, and `println` is you speaking into the microphone. Whatever you say into the microphone (whatever you put in the parentheses) gets broadcasted through the loudspeaker (displayed on the screen).

In summary, `System.out.println` is a way to print text or information to the console, allowing you to see the output of your program. It's a fundamental tool for debugging and interacting with your program as it runs.

# Various ways to create object

In Java, there are several ways to create objects. Here are the most common methods:

### 1. Using the `new` Keyword

This is the most common way to create an object. You use the `new` keyword followed by the class constructor.

```java
public class Main {
    public static void main(String[] args) {
        // Creating an object using the new keyword
        MyClass obj = new MyClass();
    }
}

class MyClass {
    // Constructor
    MyClass() {
        System.out.println("Object created using new keyword");
    }
}
```

### 2. Using Reflection

Java's Reflection API allows you to create an object by calling the `newInstance` method on the `Class` object.

```java
public class Main {
    public static void main(String[] args) {
        try {
            // Creating an object using Reflection
            MyClass obj = MyClass.class.getDeclaredConstructor().newInstance();
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}

class MyClass {
    // Constructor
    MyClass() {
        System.out.println("Object created using Reflection");
    }
}
```

### 3. Using `clone` Method

The `clone` method is used to create a copy of an existing object. The class must implement the `Cloneable` interface.

```java
public class Main {
    public static void main(String[] args) {
        try {
            // Creating an object using clone method
            MyClass obj1 = new MyClass();
            MyClass obj2 = (MyClass) obj1.clone();
        } catch (CloneNotSupportedException e) {
            e.printStackTrace();
        }
    }
}

class MyClass implements Cloneable {
    // Constructor
    MyClass() {
        System.out.println("Object created using clone method");
    }

    // Overriding clone() method
    protected Object clone() throws CloneNotSupportedException {
        return super.clone();
    }
}
```

### 4. Using Deserialization

Deserialization is the process of converting a byte stream back into an object. The class must implement the `Serializable` interface.

```java
import java.io.*;

public class Main {
    public static void main(String[] args) {
        try {
            // Serializing the object
            MyClass obj1 = new MyClass();
            FileOutputStream fileOut = new FileOutputStream("object.ser");
            ObjectOutputStream out = new ObjectOutputStream(fileOut);
            out.writeObject(obj1);
            out.close();
            fileOut.close();

            // Deserializing the object
            FileInputStream fileIn = new FileInputStream("object.ser");
            ObjectInputStream in = new ObjectInputStream(fileIn);
            MyClass obj2 = (MyClass) in.readObject();
            in.close();
            fileIn.close();
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}

class MyClass implements Serializable {
    // Constructor
    MyClass() {
        System.out.println("Object created using deserialization");
    }
}
```

### 5. Using Factory Method

Factory methods are static methods in a class that return an instance of the class.

```java
public class Main {
    public static void main(String[] args) {
        // Creating an object using factory method
        MyClass obj = MyClass.createInstance();
    }
}

class MyClass {
    // Constructor
    private MyClass() {
        System.out.println("Object created using factory method");
    }

    // Factory method
    public static MyClass createInstance() {
        return new MyClass();
    }
}
```

### Summary

- **Using `new` Keyword**: `MyClass obj = new MyClass();`
- **Using Reflection**: `MyClass obj = MyClass.class.getDeclaredConstructor().newInstance();`
- **Using `clone` Method**: `MyClass obj = (MyClass) originalObj.clone();`
- **Using Deserialization**: `MyClass obj = (MyClass) in.readObject();`
- **Using Factory Method**: `MyClass obj = MyClass.createInstance();`

Each method has its use cases and advantages, depending on the requirements and constraints of your application.

Java is often described as not being 100% object-oriented. This is because, while Java supports object-oriented programming and most of its features adhere to the principles of object-oriented design, it also includes elements that are not objects. Let's break this down:

# Reasons Why Java is Not 100% Object-Oriented

1. **Primitive Data Types**:
   - Java has eight primitive data types: `int`, `byte`, `short`, `long`, `float`, `double`, `char`, and `boolean`. These are not objects; they are simple data types that are used for efficiency and performance reasons.
   - Example:
     ```java
     int number = 10;
     char letter = 'A';
     boolean flag = true;
     ```

2. **Static Methods and Variables**:
   - Java allows the use of static methods and variables. Static methods belong to the class, not to any specific instance, and can be called without creating an instance of the class.
   - Example:
     ```java
     public class MyClass {
         public static void myStaticMethod() {
             System.out.println("This is a static method");
         }
     }

     public class Main {
         public static void main(String[] args) {
             MyClass.myStaticMethod(); // Call static method without creating an object
         }
     }
     ```

3. **Wrapper Classes**:
   - Java provides wrapper classes (such as `Integer`, `Character`, `Boolean`, etc.) for primitive data types to work with them as objects when needed. This is a workaround rather than a solution that fits purely within an object-oriented paradigm.
   - Example:
     ```java
     int num = 10;
     Integer numObj = Integer.valueOf(num); // Using wrapper class to convert primitive to object
     ```

4. **Native Methods**:
   - Java allows the use of native methods, which are implemented in languages like C or C++. These methods are not written in Java and do not follow the object-oriented principles of Java.
   - Example:
     ```java
     public class MyClass {
         // Declare a native method
         public native void myNativeMethod();
     }
     ```

### Why These Exceptions?

- **Performance**: Primitive types are more efficient and faster than objects because they are stored directly in memory, without the overhead of object creation and garbage collection.
- **Legacy and Interoperability**: Java was designed to be a practical and usable language for real-world applications. Supporting primitives and native methods allows Java to be more efficient and to interact with system-level code and libraries written in other languages.
- **Ease of Use**: Static methods and variables provide convenience for utility functions and constants that do not need to be associated with object instances.

### Conclusion

Java strives to be an object-oriented language and encourages the use of objects and classes to design applications. However, for practical reasons, it includes features like primitive data types and static methods that do not conform to strict object-oriented principles. These features help balance performance and usability, making Java a versatile and widely used programming language.

### Java Package

A package in Java is a namespace that organizes a set of related classes and interfaces. Think of it as a folder in a file directory. Packages help to avoid name conflicts and to control access to classes, interfaces, and methods. They also make it easier to locate and use classes, as they group related classes together.

#### Benefits of Using Packages

1. **Namespace Management**: Packages help avoid name conflicts between classes.
2. **Access Protection**: Packages can control the visibility and accessibility of classes and their members.
3. **Organization**: Packages organize related classes and interfaces, making the codebase easier to manage and navigate.

#### Creating and Using Packages

To create a package, use the `package` keyword at the top of your Java source file. To use a class from a package, you need to import it using the `import` statement.

**Creating a Package**

Let's create a package named `mypackage` and a class inside it.

1. **MyClass.java**
   ```java
   package mypackage;

   public class MyClass {
       public void display() {
           System.out.println("Hello from MyClass in mypackage!");
       }
   }
   ```

2. **Main.java**
   ```java
   import mypackage.MyClass;

   public class Main {
       public static void main(String[] args) {
           MyClass obj = new MyClass();
           obj.display();
       }
   }
   ```

In this example, `MyClass` is part of the `mypackage` package, and we import it in `Main.java` to use it.

### Default Imported Package

In Java, the `java.lang` package is imported by default. This package includes fundamental classes that are essential to the Java programming language, such as `String`, `System`, `Integer`, `Object`, `Thread`, and many others.

Because the `java.lang` package is imported automatically, you do not need to explicitly import its classes. You can use them directly.

**Example**

```java
public class Main {
    public static void main(String[] args) {
        // Using String class from java.lang package without explicit import
        String message = "Hello, World!";
        
        // Using System class from java.lang package without explicit import
        System.out.println(message);
    }
}
```

In this example, `String` and `System` are used without any import statements because they are part of the `java.lang` package, which is imported by default.

### Summary

- **Package**: A way to organize related classes and interfaces to avoid naming conflicts, control access, and manage code organization.
- **Default Imported Package**: `java.lang` is imported automatically, so you can use its classes without needing to import them explicitly.

By using packages, you can create modular, maintainable, and scalable Java applications.





