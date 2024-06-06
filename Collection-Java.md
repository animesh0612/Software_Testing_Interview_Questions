
# Collection in Java

In Java, a Collection is a framework that provides an architecture to store and manipulate a group of objects. It includes interfaces and classes to manage groups of objects in a more structured way.

### ArrayList

An `ArrayList` is a resizable array. It allows us to store elements and dynamically adjust its size when elements are added or removed.

Here's a simple example:

```java
import java.util.ArrayList;

public class Main {
    public static void main(String[] args) {
        // Creating an ArrayList to store strings
        ArrayList<String> fruits = new ArrayList<>();

        // Adding elements to the ArrayList
        fruits.add("Apple");
        fruits.add("Banana");
        fruits.add("Orange");

        // Accessing elements from the ArrayList
        System.out.println(fruits.get(0)); // Output: Apple

        // Removing an element from the ArrayList
        fruits.remove("Banana");

        // Iterating over the ArrayList
        for (String fruit : fruits) {
            System.out.println(fruit);
        }
    }
}
```

### LinkedList

A `LinkedList` is a doubly-linked list implementation of the List and Deque interfaces. It allows for fast insertions and deletions.

Here's an example:

```java
import java.util.LinkedList;

public class Main {
    public static void main(String[] args) {
        // Creating a LinkedList to store integers
        LinkedList<Integer> numbers = new LinkedList<>();

        // Adding elements to the LinkedList
        numbers.add(1);
        numbers.add(2);
        numbers.add(3);

        // Accessing elements from the LinkedList
        System.out.println(numbers.get(0)); // Output: 1

        // Removing an element from the LinkedList
        numbers.remove(Integer.valueOf(2));

        // Iterating over the LinkedList
        for (Integer number : numbers) {
            System.out.println(number);
        }
    }
}
```

### Vector

A `Vector` is similar to an `ArrayList`, but it is synchronized, meaning it is thread-safe.

Here's an example:

```java
import java.util.Vector;

public class Main {
    public static void main(String[] args) {
        // Creating a Vector to store strings
        Vector<String> books = new Vector<>();

        // Adding elements to the Vector
        books.add("Harry Potter");
        books.add("Lord of the Rings");
        books.add("Game of Thrones");

        // Accessing elements from the Vector
        System.out.println(books.get(0)); // Output: Harry Potter

        // Removing an element from the Vector
        books.remove("Lord of the Rings");

        // Iterating over the Vector
        for (String book : books) {
            System.out.println(book);
        }
    }
}
```

### HashSet

A `HashSet` is a collection that uses a hash table for storage. It doesn't allow duplicate elements and doesn't maintain any order.

Here's an example:

```java
import java.util.HashSet;

public class Main {
    public static void main(String[] args) {
        // Creating a HashSet to store strings
        HashSet<String> cities = new HashSet<>();

        // Adding elements to the HashSet
        cities.add("New York");
        cities.add("Los Angeles");
        cities.add("Chicago");

        // Attempting to add a duplicate element
        cities.add("New York"); // This will not be added

        // Iterating over the HashSet
        for (String city : cities) {
            System.out.println(city);
        }
    }
}
```

### TreeSet

A `TreeSet` is a sorted collection that uses a tree for storage. It stores elements in ascending order and doesn't allow duplicates.

Here's an example:

```java
import java.util.TreeSet;

public class Main {
    public static void main(String[] args) {
        // Creating a TreeSet to store strings
        TreeSet<String> countries = new TreeSet<>();

        // Adding elements to the TreeSet
        countries.add("USA");
        countries.add("Canada");
        countries.add("Mexico");

        // Attempting to add a duplicate element
        countries.add("Canada"); // This will not be added

        // Iterating over the TreeSet
        for (String country : countries) {
            System.out.println(country);
        }
    }
}
```

### Summary

- **ArrayList**: Resizable array, fast access, slow insertion/removal.
- **LinkedList**: Doubly-linked list, fast insertion/removal, slow access.
- **Vector**: Similar to ArrayList but synchronized (thread-safe).
- **HashSet**: No duplicates, no order, fast access.
- **TreeSet**: No duplicates, sorted order.

Each of these collections serves different needs based on how you need to store, access, and manipulate data.

Idempotency is a concept from mathematics and computer science where an operation can be applied multiple times without changing the result beyond the initial application. In the context of collections, this often refers to the behavior of adding and removing elements.

### Idempotent Operations
Idempotent operations are those that can be performed multiple times without changing the result after the first application.

- **HashSet**: Adding an element to a HashSet is idempotent because adding the same element multiple times doesn't change the set after the first addition. Removing an element is also idempotent because removing a non-existent element doesn't change the set.

- **TreeSet**: Similar to HashSet, adding an element is idempotent because duplicates are not allowed. Removing an element is also idempotent.

### Non-Idempotent Operations
Non-idempotent operations are those that, when performed multiple times, result in a change in the state or outcome each time they are applied.

- **ArrayList**: Adding an element is non-idempotent because each addition increases the size of the list. Removing an element is also non-idempotent because it changes the size of the list and may affect the order of remaining elements.

- **LinkedList**: Adding and removing elements are non-idempotent for the same reasons as ArrayList.

- **Vector**: Similar to ArrayList, adding and removing elements are non-idempotent.

### Code Examples with Comments

#### ArrayList (Non-Idempotent)

```java
import java.util.ArrayList;

public class Main {
    public static void main(String[] args) {
        // Creating an ArrayList to store strings
        ArrayList<String> fruits = new ArrayList<>();

        // Adding elements to the ArrayList (Non-idempotent)
        fruits.add("Apple");
        fruits.add("Apple"); // Adding "Apple" again changes the list
        fruits.add("Banana");

        // Accessing elements from the ArrayList
        System.out.println(fruits.get(0)); // Output: Apple

        // Removing an element from the ArrayList (Non-idempotent)
        fruits.remove("Apple"); // Removing "Apple" changes the list

        // Iterating over the ArrayList
        for (String fruit : fruits) {
            System.out.println(fruit); // Output: Apple, Banana
        }
    }
}
```

#### LinkedList (Non-Idempotent)

```java
import java.util.LinkedList;

public class Main {
    public static void main(String[] args) {
        // Creating a LinkedList to store integers
        LinkedList<Integer> numbers = new LinkedList<>();

        // Adding elements to the LinkedList (Non-idempotent)
        numbers.add(1);
        numbers.add(1); // Adding "1" again changes the list
        numbers.add(2);

        // Accessing elements from the LinkedList
        System.out.println(numbers.get(0)); // Output: 1

        // Removing an element from the LinkedList (Non-idempotent)
        numbers.remove(Integer.valueOf(1)); // Removing "1" changes the list

        // Iterating over the LinkedList
        for (Integer number : numbers) {
            System.out.println(number); // Output: 1, 2
        }
    }
}
```

#### Vector (Non-Idempotent)

```java
import java.util.Vector;

public class Main {
    public static void main(String[] args) {
        // Creating a Vector to store strings
        Vector<String> books = new Vector<>();

        // Adding elements to the Vector (Non-idempotent)
        books.add("Harry Potter");
        books.add("Harry Potter"); // Adding "Harry Potter" again changes the list
        books.add("Lord of the Rings");

        // Accessing elements from the Vector
        System.out.println(books.get(0)); // Output: Harry Potter

        // Removing an element from the Vector (Non-idempotent)
        books.remove("Harry Potter"); // Removing "Harry Potter" changes the list

        // Iterating over the Vector
        for (String book : books) {
            System.out.println(book); // Output: Harry Potter, Lord of the Rings
        }
    }
}
```

#### HashSet (Idempotent)

```java
import java.util.HashSet;

public class Main {
    public static void main(String[] args) {
        // Creating a HashSet to store strings
        HashSet<String> cities = new HashSet<>();

        // Adding elements to the HashSet (Idempotent)
        cities.add("New York");
        cities.add("New York"); // Adding "New York" again doesn't change the set
        cities.add("Los Angeles");

        // Attempting to add a duplicate element
        cities.add("New York"); // No change in the set

        // Iterating over the HashSet
        for (String city : cities) {
            System.out.println(city); // Output: New York, Los Angeles
        }
    }
}
```

#### TreeSet (Idempotent)

```java
import java.util.TreeSet;

public class Main {
    public static void main(String[] args) {
        // Creating a TreeSet to store strings
        TreeSet<String> countries = new TreeSet<>();

        // Adding elements to the TreeSet (Idempotent)
        countries.add("USA");
        countries.add("USA"); // Adding "USA" again doesn't change the set
        countries.add("Canada");

        // Attempting to add a duplicate element
        countries.add("USA"); // No change in the set

        // Iterating over the TreeSet
        for (String country : countries) {
            System.out.println(country); // Output: Canada, USA (sorted order)
        }
    }
}
```

### Summary of Idempotency

- **Idempotent**: HashSet, TreeSet (add/remove operations)
- **Non-Idempotent**: ArrayList, LinkedList, Vector (add/remove operations)

Understanding idempotency is crucial when designing systems that require consistent and predictable behavior, especially in concurrent or distributed environments.

