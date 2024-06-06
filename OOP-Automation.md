
# Used OOPs in Automation Framework

Using Object-Oriented Programming (OOP) concepts in an automation framework helps make the code more modular, reusable, and easier to maintain. Here’s how the main OOP concepts—encapsulation, inheritance, polymorphism, and abstraction—can be applied in an automation framework

### Encapsulation

**Encapsulation** means bundling the data (variables) and methods (functions) that operate on the data into a single unit or class. It helps protect the data from outside interference and misuse.

**In Automation Framework:**

- **Where**: Encapsulation can be used to define test case classes, utility classes, and page object classes.
- **How**: By creating classes that encapsulate the details of test actions and data.

**Example:**

```java
// Page Object Class for Login Page
public class LoginPage {
    // Private variables for page elements
    private WebDriver driver;
    private By usernameField = By.id("username");
    private By passwordField = By.id("password");
    private By loginButton = By.id("login");

    // Constructor
    public LoginPage(WebDriver driver) {
        this.driver = driver;
    }

    // Public method to perform login
    public void login(String username, String password) {
        driver.findElement(usernameField).sendKeys(username);
        driver.findElement(passwordField).sendKeys(password);
        driver.findElement(loginButton).click();
    }
}
```

### Inheritance

**Inheritance** allows a new class to inherit properties and methods from an existing class. It promotes code reuse and establishes a natural hierarchy.

**In Automation Framework:**

- **Where**: Inheritance can be used for creating a base test class that contains common setup and teardown methods.
- **How**: By creating a base class and extending it in your test classes.

**Example:**

```java
// Base Test Class
public class BaseTest {
    protected WebDriver driver;

    // Setup method
    @Before
    public void setUp() {
        driver = new ChromeDriver();
        driver.manage().timeouts().implicitlyWait(10, TimeUnit.SECONDS);
    }

    // Teardown method
    @After
    public void tearDown() {
        driver.quit();
    }
}

// Test Class inheriting from BaseTest
public class LoginTest extends BaseTest {
    @Test
    public void testLogin() {
        driver.get("https://example.com/login");
        LoginPage loginPage = new LoginPage(driver);
        loginPage.login("user", "pass");
        // Assertions can be added here
    }
}
```

### Polymorphism

**Polymorphism** means "many shapes" and allows methods to do different things based on the object it is acting upon. It simplifies code and enhances flexibility.

**In Automation Framework:**

- **Where**: Polymorphism can be used in creating interfaces for different types of tests (e.g., UI tests, API tests).
- **How**: By defining a common interface or superclass and using it in different test classes.

**Example:**

```java
// Interface for different types of tests
public interface Test {
    void run();
}

// UI Test Class
public class UITest implements Test {
    @Override
    public void run() {
        System.out.println("Running UI Test");
    }
}

// API Test Class
public class APITest implements Test {
    @Override
    public void run() {
        System.out.println("Running API Test");
    }
}

// Main Class to run tests
public class TestRunner {
    public static void main(String[] args) {
        Test uiTest = new UITest();
        Test apiTest = new APITest();

        uiTest.run();
        apiTest.run();
    }
}
```

### Abstraction

**Abstraction** means hiding the complex implementation details and showing only the necessary features of an object. It helps reduce programming complexity and effort.

**In Automation Framework:**

- **Where**: Abstraction can be used to create abstract classes or interfaces for different components (e.g., page objects, test utilities).
- **How**: By defining abstract classes or interfaces that other classes can implement or extend.

**Example:**

```java
// Abstract class for a Page
public abstract class Page {
    protected WebDriver driver;

    // Constructor
    public Page(WebDriver driver) {
        this.driver = driver;
    }

    // Abstract method to get page title
    public abstract String getPageTitle();
}

// Concrete class for Login Page
public class LoginPage extends Page {
    public LoginPage(WebDriver driver) {
        super(driver);
    }

    @Override
    public String getPageTitle() {
        return driver.getTitle();
    }
}
```

### Putting It All Together

Using these OOP concepts, you can create a robust automation framework. Here's a high-level view of how you can structure it:

1. **Encapsulation**: Encapsulate web elements and actions in Page Object classes.
2. **Inheritance**: Use a base test class to manage common setup and teardown actions.
3. **Polymorphism**: Implement different types of tests (UI, API, etc.) using interfaces.
4. **Abstraction**: Define abstract classes for common page components and let specific pages extend them.

By applying OOP principles, you make your automation framework more modular, easier to maintain, and scalable for future changes.

Sure, let's include classes and objects and explain how they are used in an automation framework using Object-Oriented Programming (OOP) concepts.

### Classes and Objects

**Classes** are blueprints for creating objects. They define properties (attributes) and behaviors (methods) that the objects created from the class will have. 

**Objects** are instances of classes. When a class is instantiated, it creates an object with the defined properties and behaviors.

### Using Classes and Objects in an Automation Framework

In an automation framework, classes can represent different components such as test cases, page objects, utility functions, and more. Objects are instances of these classes that perform the actual actions during the test execution.

#### Example Framework Structure

Let's build a simple automation framework using OOP concepts, including classes and objects.

1. **BaseTest Class** (for setup and teardown)
2. **LoginPage Class** (encapsulation and abstraction)
3. **Test Interface** (polymorphism)
4. **UITest Class** (implements Test interface)
5. **APITest Class** (implements Test interface)
6. **TestRunner Class** (main class to run tests)

### BaseTest Class

This class will handle common setup and teardown actions for all tests.

```java
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.chrome.ChromeDriver;
import org.junit.Before;
import org.junit.After;

public class BaseTest {
    protected WebDriver driver;

    // Setup method
    @Before
    public void setUp() {
        driver = new ChromeDriver();
        driver.manage().timeouts().implicitlyWait(10, TimeUnit.SECONDS);
    }

    // Teardown method
    @After
    public void tearDown() {
        driver.quit();
    }
}
```

### LoginPage Class

This class will encapsulate the elements and actions of the login page.

```java
import org.openqa.selenium.By;
import org.openqa.selenium.WebDriver;

public class LoginPage {
    private WebDriver driver;
    private By usernameField = By.id("username");
    private By passwordField = By.id("password");
    private By loginButton = By.id("login");

    // Constructor
    public LoginPage(WebDriver driver) {
        this.driver = driver;
    }

    // Method to perform login
    public void login(String username, String password) {
        driver.findElement(usernameField).sendKeys(username);
        driver.findElement(passwordField).sendKeys(password);
        driver.findElement(loginButton).click();
    }
}
```

### Test Interface

This interface will be used for different types of tests to demonstrate polymorphism.

```java
public interface Test {
    void run();
}
```

### UITest Class

This class will implement the Test interface for UI tests.

```java
public class UITest extends BaseTest implements Test {
    @Override
    public void run() {
        driver.get("https://example.com/login");
        LoginPage loginPage = new LoginPage(driver);
        loginPage.login("user", "pass");
        // Assertions can be added here
    }
}
```

### APITest Class

This class will implement the Test interface for API tests.

```java
public class APITest implements Test {
    @Override
    public void run() {
        System.out.println("Running API Test");
        // API test logic goes here
    }
}
```

### TestRunner Class

This class will run the tests.

```java
public class TestRunner {
    public static void main(String[] args) {
        // Create objects for UI and API tests
        Test uiTest = new UITest();
        Test apiTest = new APITest();

        // Run the tests
        uiTest.run();
        apiTest.run();
    }
}
```

### Putting It All Together

1. **Classes**: We have different classes for different components.
   - `BaseTest` for setup and teardown.
   - `LoginPage` for encapsulating the login page actions.
   - `UITest` and `APITest` for different types of tests.
   - `TestRunner` to run the tests.

2. **Objects**: Instances of these classes are created to perform actions.
   - `LoginPage loginPage = new LoginPage(driver);` creates an object to interact with the login page.
   - `Test uiTest = new UITest();` and `Test apiTest = new APITest();` create objects for different test types.

3. **OOP Concepts**:
   - **Encapsulation**: `LoginPage` encapsulates the details of the login actions.
   - **Inheritance**: `UITest` inherits from `BaseTest` for common setup/teardown.
   - **Polymorphism**: `UITest` and `APITest` implement the `Test` interface, allowing them to be used interchangeably.
   - **Abstraction**: The `Test` interface abstracts the concept of a test.

### Summary

By using classes and objects, along with OOP principles, we can create a modular, reusable, and maintainable automation framework. Each class represents a specific component or functionality, and objects of these classes perform the actual operations during test execution. This approach makes it easy to manage and extend the framework as needed.

