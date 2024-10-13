In Java, a **static function** (also called a **static method**) is a method that belongs to the **class** rather than an instance of the class. This means that you can call a static method without creating an object of the class.

### Key characteristics of static methods:
1. **Belong to the class**: Static methods are associated with the class itself, not with instances (objects) of the class.
   
2. **Can be called without an instance**: You can call a static method directly using the class name. Example:
   ```java
   ClassName.methodName();
   ```
   
3. **Cannot access instance variables or methods**: Static methods can only access other static variables and static methods. They **cannot** access instance variables or instance methods because instance-specific data does not exist without an object.

4. **Common utility methods**: Static methods are often used for utility or helper functions, like mathematical calculations or operations that do not depend on instance data (e.g., `Math.pow()`).

### Example:
```java
public class MyClass {
    // static variable
    static int count = 0;
    
    // static method
    public static void displayCount() {
        System.out.println("Count: " + count);
    }

    // non-static method
    public void incrementCount() {
        count++;
    }
}

public class Main {
    public static void main(String[] args) {
        // Call static method without creating an object
        MyClass.displayCount();  // Output: Count: 0

        // Create an object and call non-static method
        MyClass obj = new MyClass();
        obj.incrementCount();

        // Call static method again
        MyClass.displayCount();  // Output: Count: 1
    }
}
```

In this example, `displayCount()` is a static method, and you can call it using the class name (`MyClass.displayCount()`) without creating an instance of `MyClass`.

Static methods are particularly useful for utility operations that don't rely on object state.

# Chapter 11

## Abstract

# Java Lesson on Abstraction

## Introduction to Abstraction
Abstraction is the last major principle of object-oriented programming (OOP). It allows us to define templates for classes or methods that do not have a concrete implementation. 

In Java, we achieve abstraction using the `abstract` keyword, which can be applied to classes and methods. Abstract classes and methods are designed to be extended or implemented by subclasses, rather than being instantiated or used directly.

## Abstract Classes in Java
An abstract class:
- Cannot be instantiated.
- Is designed to be extended by subclasses that will provide implementations for the abstract methods.

For example, a `Shape` is an abstract concept. It can specify some general behaviors (e.g., calculating the area), but it’s too abstract to define the specific behavior without knowing the type of shape (rectangle, circle, etc.).

### Abstract Class Example

```java
package chapter11;

public abstract class Shape {
    abstract double calculateArea();  // Abstract method without a body

    public void print() {
        System.out.println("I am a shape");
    }
}
```

Here, we define an abstract class `Shape` with one abstract method `calculateArea()` and one implemented method `print()`. 

### Creating a Subclass
Now, let's create a concrete subclass `Rectangle` that extends the `Shape` class and provides the specific implementation for `calculateArea()`.

```java
package chapter11;

public class Rectangle extends Shape {

    private double length;
    private double width;

    public Rectangle(double length, double width) {
        this.length = length;
        this.width = width;
    }

    public double getLength() {
        return length;
    }

    public void setLength(double length) {
        this.length = length;
    }

    public double getWidth() {
        return width;
    }

    public void setWidth(double width) {
        this.width = width;
    }

    @Override
    double calculateArea() {
        return length * width;
    }
}
```

In this class:
- We implement the abstract method `calculateArea()` inherited from `Shape`.
- We define fields (`length` and `width`) and provide appropriate constructors and getter/setter methods.

## Testing Abstraction

Let’s create a class `ShapeTester` to test the `Rectangle` class.

```java
package chapter11;

public class ShapeTester {
    public static void main(String[] args) {
        Shape rectangle = new Rectangle(5, 7);  // Instantiating a subclass
        rectangle.print();                      // Calls print() from Shape class
        System.out.println(rectangle.calculateArea());  // Calls overridden calculateArea() from Rectangle class
    }
}
```

### Output:
```
I am a shape
35.0
```

Even though `rectangle` is of type `Shape`, it uses the overridden `calculateArea()` method from the `Rectangle` class. The `print()` method is inherited from `Shape` and remains unchanged.

## Key Points of Abstraction
- **Abstract classes and methods** are templates meant to be extended or implemented by subclasses.
- **`abstract` keyword** is used to declare an abstract class or method.
- Subclasses **must implement abstract methods** or be declared abstract themselves.
- **Abstract classes cannot be instantiated**. They are used solely as a superclass for other classes.
- If a class contains at least one abstract method, the class **must be declared as abstract**.

### Notes:
- Abstract methods do not have a body; they only declare a method signature.
- A class can contain both abstract and non-abstract methods.
- Subclasses that extend an abstract class must provide implementations for all abstract methods unless they are abstract themselves.

## Interfaces

# Java Interfaces Lesson

## Overview
An interface in Java is similar to an abstract class, but there are key differences. Unlike abstract classes, interfaces consist solely of abstract methods. These methods do not require the `abstract` keyword because they are implicitly abstract. Additionally, interfaces are **implemented** by classes, not extended.

When a class implements an interface, it must provide implementations for all of its methods or declare itself as abstract. This lesson explores how to work with interfaces in Java.

---

## Interface vs. Abstract Class
### Differences:
1. **Abstract Classes**: Can have both abstract and non-abstract methods.
2. **Interfaces**: Consist entirely of abstract methods (until Java 8 introduced default methods).

### Key Points:
- In an abstract class, you can define methods that have already been implemented.
- In an interface, every method is abstract by nature, and you do not need to explicitly declare them as such.
- Interfaces are **implemented** by classes, whereas abstract classes are **extended**.

---

## Example: Creating an Interface

### Step 1: Define the Interface
Let’s create a `Product` interface and a `Book` class that implements the `Product` interface.

```java
package chapter11;

public interface Product {

    double getPrice();
    void setPrice(double price);

    String getName();
    void setName(String name);

    String getColor();
    void setColor(String color);
}
```

### Notes:
- No need to declare the methods as `abstract`—it's implicit.
- Fields are not defined in an interface. If a field exists, it must be `final` (a constant) and must be assigned a value immediately.

---

## Implementing the Interface

### Step 2: Create a Class to Implement the Interface
Now, we will create a `Book` class that implements the `Product` interface. This class must provide implementations for all of the methods from the interface.

```java
package chapter11;

public class Book implements Product {

    private double price;
    private String name;
    private String color;
    private String author;
    private int pages;
    private String isbn;

    @Override
    public double getPrice() {
        return price;
    }

    @Override
    public void setPrice(double price) {
        this.price = price;
    }

    @Override
    public String getName() {
        return name;
    }

    @Override
    public void setName(String name) {
        this.name = name;
    }

    @Override
    public String getColor() {
        return color;
    }

    @Override
    public void setColor(String color) {
        this.color = color;
    }

    public String getAuthor() {
        return author;
    }

    public void setAuthor(String author) {
        this.author = author;
    }

    public int getPages() {
        return pages;
    }

    public void setPages(int pages) {
        this.pages = pages;
    }

    public String getIsbn() {
        return isbn;
    }

    public void setIsbn(String isbn) {
        this.isbn = isbn;
    }
}
```

### Notes:
- The `Book` class must implement all of the methods declared in the `Product` interface.
- In addition to the methods required by the `Product` interface, we’ve added additional fields and methods specific to the `Book` class.

---

## Using the Interface

### Step 3: Create a `Customer` Class to Test the Interface
Now, let’s test the `Book` class by creating a `Customer` class.

```java
package chapter11;

public class Customer {

    public static void main(String[] args) {

        Product book = new Book();
        book.setPrice(9.99);
    }
}
```

### Notes:
- You cannot instantiate an interface directly (`new Product()`), but you can use it as a type.
- The `Book` class is instantiated, and it implements the methods from the `Product` interface.

---

## Java 8: Default Methods in Interfaces
In Java 8, the concept of **default methods** was introduced. This allows you to define a method in an interface with a default implementation. This is useful for maintaining backward compatibility when new methods are added to an interface.

### Example: Default Method
```java
default String getBarcode() {
    return "no barcode";
}
```
With default methods, you can provide a basic implementation in the interface, so that classes implementing the interface aren't required to provide their own implementation.

---

## Key Points on Interfaces
- Interfaces **cannot be instantiated**.
- Interfaces are **implemented**, not extended.
- Any class that implements an interface must implement **all of its methods** or declare itself as abstract.
- Methods in an interface are either abstract or default (from Java 8 onward).
- Interface methods are implicitly `public`, and you don't need to declare an access modifier.

---

## Implementing Multiple Interfaces
Unlike classes, which can only extend one class, a class can implement multiple interfaces. When a class implements multiple interfaces, it must provide implementations for all the methods declared by each interface.

```java
public class MyClass implements Interface1, Interface2 {
    // Must implement all methods from Interface1 and Interface2
}
```

### Notes:
- Interfaces provide a way for classes to share behavior without being bound by inheritance rules (one parent class).
  
---

## Conclusion
Interfaces in Java are powerful tools for defining **contracts** that classes can follow. By using interfaces, you separate the **what** from the **how** in your code design. They enable polymorphism and multiple inheritance of type in Java.

# chapter 12 

In this chapter, we'll explore **Collections** in Java. 

## Collections
A **Collection** is an object that holds references to other objects, also known as elements. These elements are typically organized in various data structures.

### Collections Framework
Java provides a **Collections Framework** which includes interfaces, classes, and methods for storing and manipulating aggregate data. Key points include:
- Some collections allow duplicate elements; others require uniqueness.
- Some collections are ordered, while others are not.
- The framework is part of the `java.util` package.

### Common Collection Types

#### 1. Set
- **Set** is a collection that doesn't allow duplicate elements.
- Example use case: A deck of cards where each card is unique.
  
#### 2. List
- **List** is a collection where the elements are ordered and duplicates are allowed.
- Example: A phone call history, where the order matters and duplicates (like repeated numbers) may exist.

#### 3. Queue
- **Queue** is an ordered collection typically used for processing elements in a **First In, First Out (FIFO)** manner.
- Example: People in a checkout line.

#### 4. Map
- **Map** stores **key/value pairs** and is not technically a collection, but it behaves similarly.
- Example: Bank transactions where each transaction ID is a unique key, and the value is the transaction object.

### Examples of Collection Implementations

#### Set
- **Set** does not maintain element order and rejects duplicates. Common implementations include `HashSet`, `LinkedHashSet`, and `TreeSet`.
- Example:
  ```java
  Set<String> fruit = new HashSet<>();
  fruit.add("apple");
  fruit.add("banana");
  fruit.add("lemon");
  fruit.add("lemon"); // duplicate, won't be added
  ```

#### List
- **List** maintains order and allows duplicates. Implementations include `ArrayList`, `LinkedList`, `Stack`, and `Vector`.
- Example:
  ```java
  List<String> fruit = new ArrayList<>();
  fruit.add("apple");
  fruit.add("lemon");
  fruit.add("lemon"); // duplicate, will be added
  ```

#### Queue
- **Queue** follows a FIFO order and allows duplicates. Common implementations include `LinkedList` and `PriorityQueue`.
- Example:
  ```java
  Queue<String> fruit = new LinkedList<>();
  fruit.add("apple");
  fruit.add("banana");
  fruit.remove(); // Removes "apple" (the head of the queue)
  ```

#### Map
- **Map** holds key-value pairs, with unique keys. Common implementations include `HashMap`, `TreeMap`, and `LinkedHashMap`.
- Example:
  ```java
  Map<String, Integer> fruitCalories = new HashMap<>();
  fruitCalories.put("apple", 95);
  fruitCalories.put("banana", 105);
  fruitCalories.put("apple", 80); // Replaces the previous value for "apple"
  ```

### Adding Elements with `of()`
Collections can also be initialized with `of()` for simplicity, but such collections become immutable.
```java
List<String> fruit = List.of("apple", "banana", "lemon");
```

In the next section, we'll explore how to iterate through collections.

# Looping Through Collections and Maps in Java

In this section, we will explore several ways to loop through Collections and Maps in Java. We will be using the `CollectionsDemo` class, which contains methods demonstrating different approaches for iterating through common data structures.

## `CollectionsDemo` Class

The `CollectionsDemo` class contains methods for demonstrating how to iterate over various collections such as `Set`, `List`, `Queue`, and `Map`.

```java
package chapter12;

import java.util.*;

public class CollectionsDemo {

    public static void main(String[] args) {
        setDemo();
        listDemo();
        queueDemo();
        mapDemo();
    }
}
```

## Looping Through Collections

### 1. Collection: **Iterator**
The first way to loop through a collection is by using an **Iterator**. This is provided by the `Collection` interface.

#### Example:
```java
public static void setDemo() {
    Set<String> fruit = new HashSet<>();
    fruit.add("apple");
    fruit.add("lemon");
    fruit.add("banana");
    fruit.add("orange");
    fruit.add("lemon");

    var i = fruit.iterator();
    while (i.hasNext()) {
        System.out.println(i.next());
    }
}
```
- The `iterator()` method returns an `Iterator` for the collection.
- The `hasNext()` method checks if there are more elements to iterate over.
- The `next()` method returns the next element.

### 2. Collection: **Enhanced For Loop**
Another way to loop through a collection is by using an enhanced **for loop**. This approach is clean and concise.

#### Example:
```java
public static void setDemo() {
    Set<String> fruit = new HashSet<>();
    fruit.add("apple");
    fruit.add("lemon");
    fruit.add("banana");
    fruit.add("orange");
    fruit.add("lemon");

    for (String item : fruit) {
        System.out.println(item);
    }
}
```
- By specifying the type of elements in the collection (e.g., `Set<String>`), we can directly iterate over the items in the collection.

### 3. Collection: **forEach**
The `forEach()` method is another way to iterate through a collection, using lambda expressions for simplicity.

#### Example:
```java
public static void setDemo() {
    Set<String> fruit = new HashSet<>();
    fruit.add("apple");
    fruit.add("lemon");
    fruit.add("banana");
    fruit.add("orange");
    fruit.add("lemon");

    fruit.forEach(item -> System.out.println(item));
}
```
- This method takes a lambda expression that defines the action for each item in the collection.
- Alternatively, we can use method references to make the code even cleaner:

```java
fruit.forEach(System.out::println);
```
This is a shorthand version using a method reference (`System.out::println`).

## Looping Through Maps

Maps are a bit different from other collections, as they store key-value pairs. We need specific methods to iterate over maps.

### 1. Map: **Enhanced For Loop**
We can loop through a `Map` by first retrieving its `entrySet()`.

#### Example:
```java
public static void mapDemo() {
    Map<String, Integer> fruitCalories = new HashMap<>();
    fruitCalories.put("apple", 95);
    fruitCalories.put("lemon", 20);
    fruitCalories.put("banana", 105);
    fruitCalories.put("orange", 45);
    fruitCalories.put("lemon", 17);

    for (var entry : fruitCalories.entrySet()) {
        System.out.println(entry.getValue());
    }
}
```
- The `entrySet()` method returns a `Set` of the map entries.
- `entry.getValue()` retrieves the value for each key-value pair in the map.

### 2. Map: **forEach**
Similar to collections, we can also use the `forEach()` method with maps, which provides a convenient way to access both keys and values.

#### Example:
```java
public static void mapDemo() {
    Map<String, Integer> fruitCalories = new HashMap<>();
    fruitCalories.put("apple", 95);
    fruitCalories.put("lemon", 20);
    fruitCalories.put("banana", 105);
    fruitCalories.put("orange", 45);
    fruitCalories.put("lemon", 17);

    fruitCalories.forEach((k, v) -> System.out.println("Fruit: " + k + ", Calories: " + v));
}
```
- The `forEach()` method here takes two parameters, the key (`k`) and the value (`v`), allowing us to access and print both for each entry in the map.

## Conclusion
We've explored various ways to iterate through collections and maps in Java:
1. **Iterator**: Works for all collections and offers control over the iteration.
2. **Enhanced For Loop**: Simple and readable.
3. **forEach**: A modern approach that is concise and works with lambda expressions.

These methods are applicable to different types of collections (`Set`, `List`, `Queue`, etc.) and can be chosen based on your specific use case and preference.

# chapter 13

# Exception Handling in Java

An **exception** is an unexpected event that occurs during the runtime of a program, typically due to errors. When an exception is thrown, it interrupts the normal flow of the program, often leading to a crash if not handled properly. For example, trying to access an array element that doesn't exist will throw an `ArrayIndexOutOfBoundsException`.

## Handling Exceptions
To prevent a program from crashing when an exception occurs, we use **exception handling** with the `try/catch` blocks. This way, we can provide meaningful feedback when something goes wrong.

### Example: Creating a File
Let’s start by creating a file using the `File` class in Java and handling the potential exception that may occur if the directory doesn’t exist.

```java
package chapter13;

public class ExceptionHandling {
    public static void main(String args[]) {
        createNewFile();
    }

    public static void createNewFile() {
        File file = new File("resources/nonexistent.txt");
        try {
            file.createNewFile();
        } catch (IOException e) {
            System.out.println("Directory does not exist.");
            e.printStackTrace();  // Prints the stack trace for debugging
        }
    }
}
```

In this code:
- We use `try` to attempt the creation of the file.
- `catch` handles the `IOException` if the directory does not exist. We print an error message and the stack trace.

### Polymorphism with Exceptions
Java allows catching exceptions through their superclass. For example, the `ArrayIndexOutOfBoundsException` inherits from the `Exception` class, which is the top-most class in the exception hierarchy. Using this knowledge, we can catch exceptions using a more general type:

```java
try {
    file.createNewFile();
} catch (Exception e) {
    System.out.println("An error occurred.");
    e.printStackTrace();
}
```

This approach catches any exception that is a subclass of `Exception`.

## Handling Multiple Exceptions
You can handle multiple exceptions using separate `catch` blocks. However, related exceptions should have the subclass caught first, or it will never reach the other blocks. For example:

```java
try {
    fileReader = new Scanner(file);
    while (fileReader.hasNext()) {
        double num = fileReader.nextDouble();
        System.out.println(num);
    }
} catch (FileNotFoundException e) {
    e.printStackTrace();
} catch (InputMismatchException e) {
    e.printStackTrace();
}
```

If you want to catch multiple exceptions in the same block, you can use the pipe symbol `|`:

```java
catch (FileNotFoundException | InputMismatchException e) {
    e.printStackTrace();
}
```

This simplifies handling multiple exceptions that require the same logic.

## The `finally` Block
The `finally` block is used to execute code after `try` and `catch`, regardless of whether an exception occurred. This is commonly used for resource cleanup, like closing files.

```java
finally {
    fileReader.close();
}
```

If an exception occurs and the `try` block does not complete, the `finally` block will still execute.

## Try-with-Resources
An alternative to using `finally` for resource management is the **try-with-resources** statement. It ensures that the resource is automatically closed after the block finishes, without needing a `finally` block. This works with classes that implement `Closeable` or `AutoCloseable`.

```java
try (Scanner fileReader = new Scanner(new File("resources/numbers.txt"))) {
    while (fileReader.hasNext()) {
        double num = fileReader.nextDouble();
        System.out.println(num);
    }
}
```

This approach simplifies the code by automatically handling resource closure.

### Rethrowing Exceptions

When a method has code that can throw an exception, it can either catch the exception or rethrow it. This allows the calling method to handle the exception if desired.

Let's create a method called `createNewFileRethrow` that rethrows an exception without catching it. This is done by adding the `throws` keyword in the method declaration, followed by the type of exception to be thrown.

Example:

```java
package chapter13;

import java.io.File;
import java.io.IOException;

public class ExceptionHandling {

    public static void main(String[] args) {
        try {
            createNewFileRethrow();
        } catch (IOException e) {
            System.out.println("Exception caught in main: " + e.getMessage());
        }
    }

    public static void createNewFileRethrow() throws IOException {
        File file = new File("resources/nonexistent.txt");
        file.createNewFile();  // Might throw IOException
    }
}
```

In this example:
- The method `createNewFileRethrow` declares that it might throw an `IOException` by using the `throws` keyword in its signature.
- When this method is called from `main()`, it must either catch the exception in a `try-catch` block or rethrow it by declaring `throws IOException` in `main()`.

#### Explanation:
- If the method that throws the exception is called, the calling method becomes responsible for handling the exception. You can either catch it using `try-catch` or propagate it using the `throws` clause.
- Here, the `main()` method handles the exception by catching it and printing a message.

### Throwing Exceptions

In some cases, you might want to explicitly throw an exception inside a method. This can be done using the `throw` keyword followed by an instance of an exception class.

Let's take an example of a method that throws an `IllegalArgumentException` if overtime is not allowed:

```java
public class OvertimeChecker {

    public static void main(String[] args) {
        try {
            calculatePay(45, 15);
        } catch (IllegalArgumentException e) {
            System.out.println("Error: " + e.getMessage());
        }
    }

    public static double calculatePay(int hours, double rate) {
        if (hours > 40) {
            throw new IllegalArgumentException("Overtime is not allowed.");
        }
        return hours * rate;
    }
}
```

In this example:
- The method `calculatePay()` checks if the hours worked are more than 40, and if they are, it throws an `IllegalArgumentException` with a custom message.
- The exception is then caught in the `main()` method using a `try-catch` block.

#### Custom Exception
You can also define your own custom exception by extending the `Exception` class. Here's an example:

```java
public class NoOvertimeAllowedException extends Exception {
    public NoOvertimeAllowedException(String message) {
        super(message);
    }
}

public class OvertimeChecker {

    public static void main(String[] args) {
        try {
            calculatePay(45, 15);
        } catch (NoOvertimeAllowedException e) {
            System.out.println("Custom Exception: " + e.getMessage());
        }
    }

    public static double calculatePay(int hours, double rate) throws NoOvertimeAllowedException {
        if (hours > 40) {
            throw new NoOvertimeAllowedException("Overtime is not allowed.");
        }
        return hours * rate;
    }
}
```

In this custom exception example:
- The custom exception class `NoOvertimeAllowedException` extends the `Exception` class.
- It is thrown when the hours worked exceed 40, and the calling method (`main()`) handles this custom exception.

# chapter 14

### Test Automation with Java: Applying What You've Learned

### Test Automation Project Overview

Here’s a sample **test automation project** structure, which you can find on GitHub. Notice the project contains numerous **packages** and **classes**—this is typical in test automation projects. Since you already know about **packages** and **classes**, this structure should make sense to you.

#### BaseTests Class

Let's examine the `BaseTests` class:

```java
public class BaseTests {
    private WebDriver driver;
    protected SomeOtherClass page;

    public void launchApplication() {
        driver.get("http://example.com");
    }
}
```

- On lines 12-13, we see two objects: one private (`WebDriver driver`) and one protected (`SomeOtherClass page`). You are already familiar with access modifiers like **private** and **protected**, so you know these objects' visibility.
- **WebDriver** is an object from **Selenium WebDriver**, which you will become more familiar with when learning Selenium.

#### Page Class

The **Page** class defines web elements and methods to interact with a webpage. This class is an example of the **Page Object Model (POM)**, a common design pattern in test automation.

```java
public class Page {
    protected WebDriver driver;
    private By searchBox = By.name("q");

    public Page(WebDriver driver) {
        this.driver = driver;
    }

    public void search(String keyword) {
        driver.findElement(searchBox).sendKeys(keyword);
    }
}
```

- Fields like `searchBox` are **locators**—used to find web elements, like input boxes, on a web page.
- The `search()` method interacts with the search box, similar to how you'd interact with fields in any Java class.

#### Using Methods in Test Automation

In the **BaseTests** class, we can use methods like `launchApplication()` to start the application. Here, we instantiate new objects and use **decision structures** to handle different conditions, such as determining the operating system:

```java
if (System.getProperty("os.name").startsWith("Windows")) {
    // Set Windows-specific properties
} else {
    // Set properties for other OS
}
```

This is an excellent example of applying **if-else** structures in automation projects, just as you’ve learned throughout the course.

### Test Class Example: SearchTest

Here’s an example of a test class that extends `BaseTests`. Notice how **inheritance** is used:

```java
public class SearchTest extends BaseTests {
    @Test
    public void searchProduct() {
        String productName = "Apple TV";
        homePage.search(productName);
        Assert.assertTrue(searchResults.isProductListed(productName));
    }
}
```

- The `SearchTest` class **inherits** methods and fields from `BaseTests`, which means we don’t have to redefine `homePage` here.
- **Assertions** (from JUnit or TestNG) are used to verify test outcomes, such as whether a product is listed in the search results.

### SearchResults Class

The `SearchResults` class encapsulates the results of a search. Here's how we use **Lists** and **loops** in test automation:

```java
public class SearchResults {
    private List<WebElement> products;

    public WebElement findProduct(String productName) {
        for (WebElement product : products) {
            if (product.getText().equals(productName)) {
                return product;
            }
        }
        return null;
    }
}
```

- The **List** of `WebElement` objects holds all the products on the search results page.
- The **enhanced for loop** goes through each product, checking if its name matches the product we're looking for. This demonstrates how **loops** and the **equals()** method can be applied to automate tests.

### CartPage Class

The `CartPage` class represents the shopping cart in an application. It inherits from the `Page` class, similar to other page classes:

```java
public class CartPage extends Page {
    public CartPage(WebDriver driver) {
        super(driver);
    }

    public void addToCart(WebElement product) {
        product.click();
    }
}
```

- The call to `super(driver)` in the constructor shows **inheritance** in action, where `CartPage` inherits from `Page`.
- Just as we've learned, inheritance is used to share common behavior (like interacting with web pages) between different page classes.

### Handling Exceptions in Automation

You can also handle **exceptions** in your test automation code. Here’s an example of throwing an exception if a condition fails:

```java
if (cartIsEmpty) {
    throw new IllegalStateException("The cart is empty.");
}
```

This applies the exception handling concepts learned in previous chapters.

