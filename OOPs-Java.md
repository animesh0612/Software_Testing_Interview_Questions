What is OOPs concept?

The OOPS (Object-Oriented Programming System) concept in Java is a way to structure and organize your code in a way that mimics real-world objects and their interactions. Here are the key concepts explained in simple terms:

1. **Class**: Think of a class as a blueprint or a template. For example, if you're creating a program about cars, the class would be the blueprint for a car, describing its features like color, model, and functions like driving or stopping.

2. **Object**: An object is an instance of a class. Using the car example, if the class is the blueprint, then an object would be an actual car built from that blueprint. You can have many objects (cars) from the same class (blueprint).

3. **Inheritance**: This allows one class to inherit the properties and methods of another class. It's like a child inheriting traits from a parent. For example, if you have a class called "Vehicle" and another class called "Car," the Car class can inherit features from the Vehicle class, like having wheels and an engine.

4. **Encapsulation**: This is about bundling the data (variables) and methods (functions) that operate on the data into a single unit or class. It also involves hiding the internal state of the object from the outside world to protect it from unintended changes. Think of it like a pill capsule that contains medicine inside; you only interact with the capsule (object) and not directly with the medicine (data).

5. **Polymorphism**: This allows objects to be treated as instances of their parent class rather than their actual class. It means "many forms." For example, if you have a parent class called "Animal" and child classes like "Dog" and "Cat," you can use an Animal class reference to refer to a Dog or Cat object. This allows for flexibility and the ability to use a single interface to represent different underlying forms (objects).

6. **Abstraction**: This involves hiding complex implementation details and showing only the necessary features of an object. It's like using a TV remote; you don't need to know how the TV works internally, just how to use the remote to change channels or adjust the volume.

In summary, the OOPS concept in Java helps in organizing code by creating blueprints (classes), building instances (objects), inheriting traits (inheritance), protecting data (encapsulation), using different forms (polymorphism), and simplifying complex systems (abstraction). This makes the code easier to understand, maintain, and reuse.

### Encapsulation

Encapsulation in Java is the concept of wrapping the data (variables) and the code (methods) that manipulates the data into a single unit called a class. It also involves restricting direct access to some of an object's components, which is a way of preventing accidental interference and misuse of the data.

Here's a simple example to illustrate encapsulation:

```java
// Define a class named Person
public class Person {
    
    // Private variables (fields) that store the data of the class
    private String name;
    private int age;

    // Public method to set the value of the name variable
    public void setName(String name) {
        this.name = name;  // 'this.name' refers to the class variable, 'name' is the parameter
    }

    // Public method to get the value of the name variable
    public String getName() {
        return name;  // return the value of the private variable 'name'
    }

    // Public method to set the value of the age variable
    public void setAge(int age) {
        if (age > 0) {  // Check to ensure the age is positive
            this.age = age;  // 'this.age' refers to the class variable, 'age' is the parameter
        }
    }

    // Public method to get the value of the age variable
    public int getAge() {
        return age;  // return the value of the private variable 'age'
    }
}

// Main class to demonstrate encapsulation
public class Main {
    public static void main(String[] args) {
        Person person = new Person();  // Create an object of the Person class
        
        // Set values for the object's fields using setter methods
        person.setName("Alice");
        person.setAge(30);
        
        // Get and print the values of the object's fields using getter methods
        System.out.println("Name: " + person.getName());  // Output: Name: Alice
        System.out.println("Age: " + person.getAge());  // Output: Age: 30
    }
}
```

### Explanation of Each Line of Code:

```java
// Define a class named Person
public class Person {
```
- This defines a new class called `Person`.

```java
    // Private variables (fields) that store the data of the class
    private String name;
    private int age;
```
- These are private variables (also called fields) that store the data for the class. The keyword `private` means these variables cannot be accessed directly from outside the class.

```java
    // Public method to set the value of the name variable
    public void setName(String name) {
        this.name = name;  // 'this.name' refers to the class variable, 'name' is the parameter
    }
```
- This is a public method (setter) that allows us to set the value of the `name` variable. `this.name` refers to the class variable, and `name` is the parameter passed to the method.

```java
    // Public method to get the value of the name variable
    public String getName() {
        return name;  // return the value of the private variable 'name'
    }
```
- This is a public method (getter) that allows us to retrieve the value of the `name` variable.

```java
    // Public method to set the value of the age variable
    public void setAge(int age) {
        if (age > 0) {  // Check to ensure the age is positive
            this.age = age;  // 'this.age' refers to the class variable, 'age' is the parameter
        }
    }
```
- This is a public method (setter) that allows us to set the value of the `age` variable, but only if the provided age is positive. This is an example of encapsulation providing validation logic.

```java
    // Public method to get the value of the age variable
    public int getAge() {
        return age;  // return the value of the private variable 'age'
    }
}
```
- This is a public method (getter) that allows us to retrieve the value of the `age` variable.

```java
// Main class to demonstrate encapsulation
public class Main {
    public static void main(String[] args) {
        Person person = new Person();  // Create an object of the Person class
```
- This is the main class containing the `main` method, which is the entry point of the program. It creates an object of the `Person` class.

```java
        // Set values for the object's fields using setter methods
        person.setName("Alice");
        person.setAge(30);
```
- These lines use the setter methods to set the `name` and `age` of the `person` object.

```java
        // Get and print the values of the object's fields using getter methods
        System.out.println("Name: " + person.getName());  // Output: Name: Alice
        System.out.println("Age: " + person.getAge());  // Output: Age: 30
```
- These lines use the getter methods to retrieve the `name` and `age` of the `person` object and print them out.

### Summary

Encapsulation ensures that the internal representation of an object is hidden from the outside. Only the necessary parts of the object are exposed, which is achieved by making the fields private and providing public getter and setter methods to access and update those fields. This protects the data and ensures it can only be modified in controlled ways.

### Polymorphism

Polymorphism in Java is the ability of an object to take on many forms. It allows methods to do different things based on the object it is acting upon, even if they share the same method name. This is achieved through method overriding and method overloading.

Here's a simple example to illustrate polymorphism:

### Example: Method Overriding

Let's create a base class `Animal` and two derived classes `Dog` and `Cat`. Each class will have a method `makeSound()` that is overridden to provide specific implementations.

```java
// Base class Animal
class Animal {
    // Method that will be overridden in derived classes
    public void makeSound() {
        System.out.println("Some generic animal sound");
    }
}

// Derived class Dog that extends Animal
class Dog extends Animal {
    // Overriding the makeSound() method for Dog
    @Override
    public void makeSound() {
        System.out.println("Woof");
    }
}

// Derived class Cat that extends Animal
class Cat extends Animal {
    // Overriding the makeSound() method for Cat
    @Override
    public void makeSound() {
        System.out.println("Meow");
    }
}

// Main class to demonstrate polymorphism
public class Main {
    public static void main(String[] args) {
        // Create Animal reference and assign it to Dog object
        Animal myDog = new Dog();
        // Call the makeSound method
        myDog.makeSound();  // Output: Woof

        // Create Animal reference and assign it to Cat object
        Animal myCat = new Cat();
        // Call the makeSound method
        myCat.makeSound();  // Output: Meow
    }
}
```

### Explanation of Each Line of Code:

```java
// Base class Animal
class Animal {
    // Method that will be overridden in derived classes
    public void makeSound() {
        System.out.println("Some generic animal sound");
    }
}
```
- This defines a base class `Animal` with a method `makeSound()` that prints a generic animal sound.

```java
// Derived class Dog that extends Animal
class Dog extends Animal {
    // Overriding the makeSound() method for Dog
    @Override
    public void makeSound() {
        System.out.println("Woof");
    }
}
```
- This defines a derived class `Dog` that extends `Animal`. It overrides the `makeSound()` method to print "Woof".

```java
// Derived class Cat that extends Animal
class Cat extends Animal {
    // Overriding the makeSound() method for Cat
    @Override
    public void makeSound() {
        System.out.println("Meow");
    }
}
```
- This defines a derived class `Cat` that extends `Animal`. It overrides the `makeSound()` method to print "Meow".

```java
// Main class to demonstrate polymorphism
public class Main {
    public static void main(String[] args) {
        // Create Animal reference and assign it to Dog object
        Animal myDog = new Dog();
        // Call the makeSound method
        myDog.makeSound();  // Output: Woof
```
- This is the main class containing the `main` method, which is the entry point of the program. It creates an `Animal` reference and assigns it to a `Dog` object, then calls the `makeSound()` method. The overridden method in the `Dog` class is executed, printing "Woof".

```java
        // Create Animal reference and assign it to Cat object
        Animal myCat = new Cat();
        // Call the makeSound method
        myCat.makeSound();  // Output: Meow
    }
}
```
- It creates an `Animal` reference and assigns it to a `Cat` object, then calls the `makeSound()` method. The overridden method in the `Cat` class is executed, printing "Meow".

### Summary

Polymorphism allows methods to perform different tasks based on the object they are called upon. Method overriding is a common way to achieve polymorphism, where a derived class provides a specific implementation of a method that is already defined in its base class. This enables you to use a single method name and interface to operate on different types of objects in different ways.

### Classes and Objects

In Java, a class is a blueprint for creating objects. An object is an instance of a class, containing actual values stored in its fields (attributes) and defined behaviors (methods).

Here's a simple example:

```java
// Define a class named Car
public class Car {
    
    // Fields (attributes) of the class
    private String color;
    private String model;

    // Constructor to initialize the object
    public Car(String color, String model) {
        this.color = color;  // Set the color attribute
        this.model = model;  // Set the model attribute
    }

    // Method to display car details
    public void displayDetails() {
        System.out.println("Car Model: " + model);
        System.out.println("Car Color: " + color);
    }
}

// Main class to create and use Car objects
public class Main {
    public static void main(String[] args) {
        // Create a Car object
        Car myCar = new Car("Red", "Toyota");

        // Call the displayDetails method to print car details
        myCar.displayDetails();  // Output: Car Model: Toyota, Car Color: Red
    }
}
```

### Explanation of Each Line of Code:

```java
// Define a class named Car
public class Car {
```
- This defines a new class called `Car`.

```java
    // Fields (attributes) of the class
    private String color;
    private String model;
```
- These are private fields that store the color and model of the car.

```java
    // Constructor to initialize the object
    public Car(String color, String model) {
        this.color = color;  // Set the color attribute
        this.model = model;  // Set the model attribute
    }
```
- This is a constructor method that initializes the fields of the class when a new object is created.

```java
    // Method to display car details
    public void displayDetails() {
        System.out.println("Car Model: " + model);
        System.out.println("Car Color: " + color);
    }
}
```
- This method prints the details of the car.

```java
// Main class to create and use Car objects
public class Main {
    public static void main(String[] args) {
        // Create a Car object
        Car myCar = new Car("Red", "Toyota");
```
- This is the main class containing the `main` method, which creates a `Car` object with specified color and model.

```java
        // Call the displayDetails method to print car details
        myCar.displayDetails();  // Output: Car Model: Toyota, Car Color: Red
    }
}
```
- This line calls the `displayDetails` method on the `myCar` object to print its details.

### Inheritance

Inheritance allows a class to inherit fields and methods from another class. The class that inherits is called the subclass, and the class being inherited from is called the superclass.

Here's an example:

```java
// Superclass
class Animal {
    // Method in the superclass
    public void eat() {
        System.out.println("This animal eats food.");
    }
}

// Subclass that inherits from Animal
class Dog extends Animal {
    // Method in the subclass
    public void bark() {
        System.out.println("The dog barks.");
    }
}

// Main class to demonstrate inheritance
public class Main {
    public static void main(String[] args) {
        // Create a Dog object
        Dog myDog = new Dog();
        
        // Call the method from the superclass
        myDog.eat();  // Output: This animal eats food.
        
        // Call the method from the subclass
        myDog.bark();  // Output: The dog barks.
    }
}
```

### Explanation of Each Line of Code:

```java
// Superclass
class Animal {
    // Method in the superclass
    public void eat() {
        System.out.println("This animal eats food.");
    }
}
```
- This defines a superclass `Animal` with a method `eat()`.

```java
// Subclass that inherits from Animal
class Dog extends Animal {
    // Method in the subclass
    public void bark() {
        System.out.println("The dog barks.");
    }
}
```
- This defines a subclass `Dog` that inherits from `Animal` and adds a method `bark()`.

```java
// Main class to demonstrate inheritance
public class Main {
    public static void main(String[] args) {
        // Create a Dog object
        Dog myDog = new Dog();
        
        // Call the method from the superclass
        myDog.eat();  // Output: This animal eats food.
        
        // Call the method from the subclass
        myDog.bark();  // Output: The dog barks.
    }
}
```
- This is the main class, creating a `Dog` object and calling methods from both the superclass and the subclass.

### Abstraction

Abstraction is the concept of hiding the complex implementation details and showing only the necessary features of an object. It can be achieved using abstract classes and interfaces.

Here's an example using an abstract class:

```java
// Abstract class
abstract class Animal {
    // Abstract method (does not have a body)
    public abstract void makeSound();
    
    // Regular method
    public void sleep() {
        System.out.println("This animal sleeps.");
    }
}

// Subclass (inherited from Animal)
class Dog extends Animal {
    // Provide implementation for the abstract method
    public void makeSound() {
        System.out.println("Woof");
    }
}

// Main class to demonstrate abstraction
public class Main {
    public static void main(String[] args) {
        // Create a Dog object
        Dog myDog = new Dog();
        
        // Call the abstract method
        myDog.makeSound();  // Output: Woof
        
        // Call the regular method
        myDog.sleep();  // Output: This animal sleeps.
    }
}
```

### Explanation of Each Line of Code:

```java
// Abstract class
abstract class Animal {
    // Abstract method (does not have a body)
    public abstract void makeSound();
    
    // Regular method
    public void sleep() {
        System.out.println("This animal sleeps.");
    }
}
```
- This defines an abstract class `Animal` with an abstract method `makeSound()` and a regular method `sleep()`.

```java
// Subclass (inherited from Animal)
class Dog extends Animal {
    // Provide implementation for the abstract method
    public void makeSound() {
        System.out.println("Woof");
    }
}
```
- This defines a subclass `Dog` that extends `Animal` and provides an implementation for the abstract method `makeSound()`.

```java
// Main class to demonstrate abstraction
public class Main {
    public static void main(String[] args) {
        // Create a Dog object
        Dog myDog = new Dog();
        
        // Call the abstract method
        myDog.makeSound();  // Output: Woof
        
        // Call the regular method
        myDog.sleep();  // Output: This animal sleeps.
    }
}
```
- This is the main class, creating a `Dog` object, calling the implemented abstract method `makeSound()`, and the regular method `sleep()`.

### Summary

- **Classes and Objects**: A class is a blueprint for objects, defining their properties and behaviors. An object is an instance of a class with actual values.
- **Inheritance**: Allows a class to inherit properties and methods from another class, promoting code reuse and logical hierarchy.
- **Abstraction**: Hides complex implementation details and shows only the necessary features, achieved using abstract classes and interfaces.




