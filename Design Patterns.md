
# Design Patterns

Design patterns are reusable solutions to common problems in software design. Applying design patterns to an automation framework helps make it more robust, scalable, and maintainable. Here are some commonly used design patterns in the context of test automation frameworks:

### 1. Page Object Model (POM)

The Page Object Model pattern promotes creating a separate class for each web page in the application. Each class contains the elements and methods specific to that page. This pattern enhances maintainability and readability.

**Example:**

```java
// LoginPage.java
public class LoginPage {
    private WebDriver driver;
    private By usernameField = By.id("username");
    private By passwordField = By.id("password");
    private By loginButton = By.id("login");

    public LoginPage(WebDriver driver) {
        this.driver = driver;
    }

    public void login(String username, String password) {
        driver.findElement(usernameField).sendKeys(username);
        driver.findElement(passwordField).sendKeys(password);
        driver.findElement(loginButton).click();
    }
}

// LoginTest.java
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

### 2. Singleton Pattern

The Singleton pattern ensures that a class has only one instance and provides a global point of access to it. This is useful for managing WebDriver instances.

**Example:**

```java
public class WebDriverSingleton {
    private static WebDriver driver;

    private WebDriverSingleton() {
        // Private constructor to prevent instantiation
    }

    public static WebDriver getDriver() {
        if (driver == null) {
            driver = new ChromeDriver();
            driver.manage().timeouts().implicitlyWait(10, TimeUnit.SECONDS);
        }
        return driver;
    }
}

// Usage in tests
public class LoginTest {
    private WebDriver driver = WebDriverSingleton.getDriver();

    @Test
    public void testLogin() {
        driver.get("https://example.com/login");
        LoginPage loginPage = new LoginPage(driver);
        loginPage.login("user", "pass");
        // Assertions can be added here
    }
}
```

### 3. Factory Pattern

The Factory pattern provides a way to create objects without specifying the exact class of the object that will be created. This is useful for creating different types of page objects or test data.

**Example:**

```java
public class PageFactory {
    public static LoginPage getLoginPage(WebDriver driver) {
        return new LoginPage(driver);
    }

    public static HomePage getHomePage(WebDriver driver) {
        return new HomePage(driver);
    }
}

// Usage in tests
public class LoginTest extends BaseTest {
    @Test
    public void testLogin() {
        driver.get("https://example.com/login");
        LoginPage loginPage = PageFactory.getLoginPage(driver);
        loginPage.login("user", "pass");
        // Assertions can be added here
    }
}
```

### 4. Data-Driven Pattern

The Data-Driven pattern involves separating test data from test scripts. This allows tests to be run with multiple sets of data.

**Example:**

```java
import org.testng.annotations.DataProvider;
import org.testng.annotations.Test;

public class LoginTest extends BaseTest {
    @DataProvider(name = "loginData")
    public Object[][] loginDataProvider() {
        return new Object[][] {
            { "user1", "pass1" },
            { "user2", "pass2" },
            { "user3", "pass3" }
        };
    }

    @Test(dataProvider = "loginData")
    public void testLogin(String username, String password) {
        driver.get("https://example.com/login");
        LoginPage loginPage = new LoginPage(driver);
        loginPage.login(username, password);
        // Assertions can be added here
    }
}
```

### 5. Command Pattern

The Command pattern is useful for encapsulating a request as an object, thereby allowing for parameterization and queuing of requests. This can be used to create reusable test steps.

**Example:**

```java
// Command Interface
public interface Command {
    void execute();
}

// Concrete Command for login
public class LoginCommand implements Command {
    private LoginPage loginPage;
    private String username;
    private String password;

    public LoginCommand(LoginPage loginPage, String username, String password) {
        this.loginPage = loginPage;
        this.username = username;
        this.password = password;
    }

    @Override
    public void execute() {
        loginPage.login(username, password);
    }
}

// Usage in tests
public class LoginTest extends BaseTest {
    @Test
    public void testLogin() {
        driver.get("https://example.com/login");
        LoginPage loginPage = new LoginPage(driver);
        Command loginCommand = new LoginCommand(loginPage, "user", "pass");
        loginCommand.execute();
        // Assertions can be added here
    }
}
```

### Summary

- **Page Object Model (POM)**: Encapsulates page elements and actions in separate classes.
- **Singleton Pattern**: Ensures a single instance of a class, useful for WebDriver management.
- **Factory Pattern**: Creates objects without exposing the instantiation logic.
- **Data-Driven Pattern**: Runs tests with multiple sets of data.
- **Command Pattern**: Encapsulates requests as objects for reusable test steps.

Using these design patterns helps create a structured, maintainable, and scalable automation framework. Each pattern addresses specific problems and contributes to the overall robustness of the framework.

Sure! Here are the details about the Transfer Object Design Pattern and the Fluent Design Pattern and how they can be applied in an automation framework.

### Transfer Object Design Pattern

The Transfer Object Design Pattern, also known as the Data Transfer Object (DTO) pattern, is used to transfer data between software application subsystems. It reduces the number of method calls, improving performance and making code cleaner by bundling multiple data elements into a single object.

**Example:**

Suppose we need to transfer user data between different layers of the application.

**UserDTO.java**
```java
public class UserDTO {
    private String username;
    private String password;
    private String email;

    public UserDTO(String username, String password, String email) {
        this.username = username;
        this.password = password;
        this.email = email;
    }

    // Getters and Setters
    public String getUsername() { return username; }
    public void setUsername(String username) { this.username = username; }

    public String getPassword() { return password; }
    public void setPassword(String password) { this.password = password; }

    public String getEmail() { return email; }
    public void setEmail(String email) { this.email = email; }
}
```

**UserService.java**
```java
public class UserService {
    public void createUser(UserDTO user) {
        // Business logic to create user
        System.out.println("Creating user: " + user.getUsername());
    }
}
```

**UserTest.java**
```java
public class UserTest {
    public static void main(String[] args) {
        // Create a user DTO
        UserDTO user = new UserDTO("john_doe", "password123", "john@example.com");

        // Pass the DTO to the service
        UserService userService = new UserService();
        userService.createUser(user);
    }
}
```

### Fluent Design Pattern

The Fluent Design Pattern is a way of implementing method chaining, allowing for more readable and expressive code. It is often used in the context of builders and configuration.

**Example:**

Suppose we need to configure and create a complex object like a user account.

**UserBuilder.java**
```java
public class UserBuilder {
    private String username;
    private String password;
    private String email;

    public UserBuilder setUsername(String username) {
        this.username = username;
        return this;
    }

    public UserBuilder setPassword(String password) {
        this.password = password;
        return this;
    }

    public UserBuilder setEmail(String email) {
        this.email = email;
        return this;
    }

    public User build() {
        return new User(username, password, email);
    }
}
```

**User.java**
```java
public class User {
    private String username;
    private String password;
    private String email;

    public User(String username, String password, String email) {
        this.username = username;
        this.password = password;
        this.email = email;
    }

    @Override
    public String toString() {
        return "User [username=" + username + ", email=" + email + "]";
    }
}
```

**UserTest.java**
```java
public class UserTest {
    public static void main(String[] args) {
        // Using Fluent Design Pattern to build a user
        User user = new UserBuilder()
                        .setUsername("jane_doe")
                        .setPassword("password456")
                        .setEmail("jane@example.com")
                        .build();

        System.out.println(user);
    }
}
```

### Applying These Patterns in an Automation Framework

#### Transfer Object Design Pattern in Automation Framework

This pattern can be useful when transferring test data, configuration data, or results between different parts of the test framework.

**TestDataDTO.java**
```java
public class TestDataDTO {
    private String username;
    private String password;

    public TestDataDTO(String username, String password) {
        this.username = username;
        this.password = password;
    }

    // Getters and Setters
    public String getUsername() { return username; }
    public void setUsername(String username) { this.username = username; }

    public String getPassword() { return password; }
    public void setPassword(String password) { this.password = password; }
}
```

**LoginTest.java**
```java
public class LoginTest extends BaseTest {
    @Test
    public void testLogin() {
        driver.get("https://example.com/login");
        TestDataDTO testData = new TestDataDTO("user", "pass");
        LoginPage loginPage = new LoginPage(driver);
        loginPage.login(testData.getUsername(), testData.getPassword());
        // Assertions can be added here
    }
}
```

#### Fluent Design Pattern in Automation Framework

This pattern can be useful for configuring complex test setups or for building test data in a readable manner.

**TestDataBuilder.java**
```java
public class TestDataBuilder {
    private String username;
    private String password;

    public TestDataBuilder setUsername(String username) {
        this.username = username;
        return this;
    }

    public TestDataBuilder setPassword(String password) {
        this.password = password;
        return this;
    }

    public TestDataDTO build() {
        return new TestDataDTO(username, password);
    }
}
```

**LoginTest.java**
```java
public class LoginTest extends BaseTest {
    @Test
    public void testLogin() {
        driver.get("https://example.com/login");
        TestDataDTO testData = new TestDataBuilder()
                                    .setUsername("user")
                                    .setPassword("pass")
                                    .build();
        LoginPage loginPage = new LoginPage(driver);
        loginPage.login(testData.getUsername(), testData.getPassword());
        // Assertions can be added here
    }
}
```

### Summary

- **Transfer Object Design Pattern**: Used for transferring data between different parts of the application, making code cleaner and reducing method calls.
- **Fluent Design Pattern**: Implements method chaining to create more readable and expressive code, often used in builders and configurations.

By incorporating these design patterns into your automation framework, you can improve its maintainability, readability, and scalability.

### POJO Classes and DAO Classes

#### POJO Classes

**POJO** stands for Plain Old Java Object. A POJO is a simple Java object that doesn't extend or implement some special classes or interfaces required by frameworks. POJOs are used for data representation and have minimal behavior other than getters and setters.

##### Characteristics of POJO:
- It does not extend any prespecified classes, such as `javax.servlet.http.HttpServlet`.
- It does not implement any prespecified interfaces, such as `java.rmi.Remote`.
- It does not have any prespecified annotations, such as `@Entity`.

**Example of a POJO Class:**

```java
public class User {
    private String username;
    private String password;
    private String email;

    // Default constructor
    public User() {}

    // Parameterized constructor
    public User(String username, String password, String email) {
        this.username = username;
        this.password = password;
        this.email = email;
    }

    // Getter and Setter methods
    public String getUsername() {
        return username;
    }

    public void setUsername(String username) {
        this.username = username;
    }

    public String getPassword() {
        return password;
    }

    public void setPassword(String password) {
        this.password = password;
    }

    public String getEmail() {
        return email;
    }

    public void setEmail(String email) {
        this.email = email;
    }
}
```

#### DAO Classes

**DAO** stands for Data Access Object. A DAO class is responsible for providing an abstract interface to some type of database or other persistence mechanism. By mapping application calls to the persistence layer, the DAO provides data operations without exposing the details of the database.

##### Characteristics of DAO:
- Encapsulates the logic for accessing data from the database.
- Provides methods for CRUD (Create, Read, Update, Delete) operations.
- Decouples the application from the underlying data source.

**Example of a DAO Class:**

```java
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.PreparedStatement;
import java.sql.ResultSet;
import java.sql.SQLException;

public class UserDAO {
    private String jdbcURL = "jdbc:mysql://localhost:3306/mydatabase";
    private String jdbcUsername = "root";
    private String jdbcPassword = "password";

    private static final String INSERT_USERS_SQL = "INSERT INTO users (username, password, email) VALUES (?, ?, ?)";
    private static final String SELECT_USER_BY_ID = "SELECT username, password, email FROM users WHERE id = ?";
    private static final String UPDATE_USER_SQL = "UPDATE users SET username = ?, password = ?, email = ? WHERE id = ?";
    private static final String DELETE_USER_SQL = "DELETE FROM users WHERE id = ?";

    protected Connection getConnection() {
        Connection connection = null;
        try {
            connection = DriverManager.getConnection(jdbcURL, jdbcUsername, jdbcPassword);
        } catch (SQLException e) {
            e.printStackTrace();
        }
        return connection;
    }

    // Create or insert user
    public void insertUser(User user) throws SQLException {
        try (Connection connection = getConnection();
             PreparedStatement preparedStatement = connection.prepareStatement(INSERT_USERS_SQL)) {
            preparedStatement.setString(1, user.getUsername());
            preparedStatement.setString(2, user.getPassword());
            preparedStatement.setString(3, user.getEmail());
            preparedStatement.executeUpdate();
        } catch (SQLException e) {
            e.printStackTrace();
        }
    }

    // Select user by ID
    public User selectUser(int id) {
        User user = null;
        try (Connection connection = getConnection();
             PreparedStatement preparedStatement = connection.prepareStatement(SELECT_USER_BY_ID)) {
            preparedStatement.setInt(1, id);
            ResultSet rs = preparedStatement.executeQuery();
            while (rs.next()) {
                String username = rs.getString("username");
                String password = rs.getString("password");
                String email = rs.getString("email");
                user = new User(username, password, email);
            }
        } catch (SQLException e) {
            e.printStackTrace();
        }
        return user;
    }

    // Update user
    public boolean updateUser(User user, int id) throws SQLException {
        boolean rowUpdated;
        try (Connection connection = getConnection();
             PreparedStatement statement = connection.prepareStatement(UPDATE_USER_SQL)) {
            statement.setString(1, user.getUsername());
            statement.setString(2, user.getPassword());
            statement.setString(3, user.getEmail());
            statement.setInt(4, id);
            rowUpdated = statement.executeUpdate() > 0;
        }
        return rowUpdated;
    }

    // Delete user
    public boolean deleteUser(int id) throws SQLException {
        boolean rowDeleted;
        try (Connection connection = getConnection();
             PreparedStatement statement = connection.prepareStatement(DELETE_USER_SQL)) {
            statement.setInt(1, id);
            rowDeleted = statement.executeUpdate() > 0;
        }
        return rowDeleted;
    }
}
```

### Putting It All Together

Let's demonstrate how to use the POJO and DAO classes together in a simple application.

**Example Application:**

```java
public class UserApp {
    public static void main(String[] args) {
        UserDAO userDAO = new UserDAO();
        
        // Creating a new user
        User newUser = new User("john_doe", "password123", "john@example.com");
        try {
            userDAO.insertUser(newUser);
            System.out.println("User inserted successfully");
        } catch (SQLException e) {
            e.printStackTrace();
        }

        // Retrieving a user
        User user = userDAO.selectUser(1);
        if (user != null) {
            System.out.println("User Retrieved: " + user.getUsername());
        }

        // Updating a user
        user.setUsername("john_doe_updated");
        try {
            boolean updated = userDAO.updateUser(user, 1);
            if (updated) {
                System.out.println("User updated successfully");
            }
        } catch (SQLException e) {
            e.printStackTrace();
        }

        // Deleting a user
        try {
            boolean deleted = userDAO.deleteUser(1);
            if (deleted) {
                System.out.println("User deleted successfully");
            }
        } catch (SQLException e) {
            e.printStackTrace();
        }
    }
}
```

### Summary

- **POJO Class**: A simple Java object used for data representation, containing fields and getter/setter methods.
- **DAO Class**: A class that provides an abstract interface to the database, encapsulating the logic for CRUD operations.

By using POJO and DAO classes, you can effectively separate the concerns of data representation and data access in your application, leading to cleaner and more maintainable code.

