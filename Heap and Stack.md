
# Heap and Stack Memory

### Heap and Stack Memory in Java

In Java, memory is divided into two main areas: the **heap** and the **stack**. These areas have different purposes and behaviors. Let's break it down in simple terms.

#### Stack Memory

1. **What is it?**
   - Stack memory is used for static memory allocation. It stores primitive data types (int, float, etc.) and references to objects, as well as method call details (method frame) like parameters and local variables.

2. **Characteristics:**
   - **Fast Access**: Stack memory is faster to access because it follows a Last In First Out (LIFO) order.
   - **Size Limit**: It is smaller in size compared to the heap and has limited space.
   - **Scope**: Data stored in the stack is short-lived and is cleaned up automatically once the method completes execution.

3. **Example:**
   - When a method is called, a block is created in the stack to hold local variables and references.
   - When the method finishes, the block is removed.

#### Heap Memory

1. **What is it?**
   - Heap memory is used for dynamic memory allocation. It stores objects and class instances.

2. **Characteristics:**
   - **Flexible**: It is larger in size and can grow dynamically.
   - **Slower Access**: Accessing heap memory is slower compared to stack memory because of the overhead of garbage collection.
   - **Persistence**: Objects in the heap remain there as long as they are referenced. The Java Garbage Collector removes objects that are no longer referenced to free up space.

3. **Example:**
   - When you create a new object using the `new` keyword, it is allocated in the heap.
   - Objects created in the heap can be accessed globally, and they persist until they are no longer referenced.

### Diagram Explanation

Below is a simplified diagram to illustrate the difference between stack and heap memory.

```
+---------------------+       +------------------------+
|                     |       |                        |
|   Stack Memory      |       |      Heap Memory       |
|                     |       |                        |
|   +-------------+   |       |  +------------------+  |
|   | main()      |   |       |  |    Object A      |  |
|   | +---------+ |   |       |  +------------------+  |
|   | | refA    | |   |       |  |                  |  |
|   | +---------+ |   |       |  |  +------------+  |  |
|   +-------------+   |       |  |  |  Instance   |  |  |
|   | method1()   |   |       |  |  |  Variables  |  |  |
|   | +---------+ |   |       |  |  +------------+  |  |
|   | localVar1  | |   |       |  +------------------+  |
|   | +---------+ |   |       |                        |
|   +-------------+   |       +------------------------+
|                     |
+---------------------+
```

### In Layman's Terms:

1. **Stack Memory**:
   - Think of the stack as a series of boxes stacked on top of each other.
   - Each time you call a method, you add a new box on top.
   - When the method finishes, you remove the box from the top.
   - These boxes are small and quick to manage.

2. **Heap Memory**:
   - Think of the heap as a large storage area with shelves.
   - When you create an object, you place it on a shelf.
   - These shelves can grow to accommodate more objects as needed.
   - The heap is like a warehouse that needs organizing (garbage collection) to keep track of what's still needed and what's not.

### Summary

- **Stack**: Stores method calls, local variables, and is short-lived. Fast and limited in size.
- **Heap**: Stores objects, accessible from anywhere in the application, and managed by the garbage collector. Slower but larger in size.

This should give you a clear understanding of the differences between heap and stack memory in Java!

Sure! Let's illustrate the concepts of stack and heap memory using a simple Java program.

### Java Code Example

```java
public class MemoryExample {
    public static void main(String[] args) {
        int x = 10; // Stored in stack memory
        MyClass obj = new MyClass(); // Reference stored in stack, object stored in heap
        obj.setValue(20); // Setting value in the heap object
        obj.displayValue(); // Accessing the heap object method
    }
}

class MyClass {
    private int value; // Stored in heap memory
    
    public void setValue(int value) {
        this.value = value; // Modifying the value in the heap
    }
    
    public void displayValue() {
        System.out.println("Value: " + value); // Accessing the value in the heap
    }
}
```

### Memory Allocation Breakdown

1. **Stack Memory**:
   - When `main` method is called, a stack frame is created for it.
   - The local variable `x` and the reference `obj` are stored in this stack frame.

2. **Heap Memory**:
   - When `new MyClass()` is called, a new `MyClass` object is created in the heap memory.
   - The `value` field of `MyClass` is also stored in the heap as part of the object.

### Detailed Diagram

```
+-----------------------------+       +-----------------------------+
|         Stack Memory        |       |         Heap Memory         |
|                             |       |                             |
|  +-----------------------+  |       |  +-----------------------+  |
|  | main()                |  |       |  |       MyClass         |  |
|  | +-------------------+ |  |       |  | +-------------------+ |  |
|  | | int x = 10        | |  |       |  | | int value = 20    | |  |
|  | | MyClass obj       | |  |       |  | +-------------------+ |  |
|  | | (ref to heap obj) | |  |       |  +-----------------------+  |
|  | +-------------------+ |  |       |                             |
|  +-----------------------+  |       +-----------------------------+
|                             |
+-----------------------------+
```

### Step-by-Step Execution

1. **`main` method starts**:
   - A stack frame is created for `main`.
   - Local variables `x` and `obj` are declared in the stack frame of `main`.

2. **`int x = 10;`**:
   - `x` is a primitive type and its value (10) is stored directly in the stack.

3. **`MyClass obj = new MyClass();`**:
   - The `new MyClass()` expression creates a new `MyClass` object in the heap.
   - The reference to this object is stored in the stack variable `obj`.

4. **`obj.setValue(20);`**:
   - The `setValue` method is called on the `obj` reference.
   - A new stack frame is created for the `setValue` method.
   - The parameter `value` (20) is passed to this method and stored in the stack frame of `setValue`.
   - Inside `setValue`, the `value` field of the `MyClass` object (in the heap) is set to 20.
   - The stack frame for `setValue` is removed after the method execution is complete.

5. **`obj.displayValue();`**:
   - The `displayValue` method is called on the `obj` reference.
   - A new stack frame is created for the `displayValue` method.
   - The method accesses the `value` field of the `MyClass` object (20) from the heap and prints it.
   - The stack frame for `displayValue` is removed after the method execution is complete.

### Summary

- **Stack Memory**: Holds local variables (`x` and `obj`) and method call details.
- **Heap Memory**: Holds the actual objects (instance of `MyClass` and its fields).

This code example and explanation should help you understand how stack and heap memory work in Java.

