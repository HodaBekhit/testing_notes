# Selenium WebDriver with java

The browser driver is an intermediary between Selenium and the actual browser, allowing Selenium to interact with it programmatically.

[[TOC]]

## Web Driver

### Objectives 

This project demonstrates how to use Selenium WebDriver in Java to launch a browser, navigate to a web application, and interact with it. Follow the steps below to set up your Selenium environment and run the test automation script.

---

### Project Structure

- **Source Directories**: 
  - `main/` (if needed)
  - `test/`: Contains the Java folder where you will create packages and classes for testing.
  
### Steps to Set Up

1. **Create a Package:**
   - Inside the `test` directory, right-click the Java folder and select "New" > "Package".
   - Name the package: `base`.

2. **Create a Java Class:**
   - Inside the `base` package, create a new Java class called `BaseTests`.

---

### Code Overview

#### 1. **WebDriver Setup**
   - We need to set up the ChromeDriver to allow Selenium to interact with the browser.
   - Use the `System.setProperty()` method to specify the path to the ChromeDriver executable.

```java
System.setProperty("webdriver.chrome.driver", "resources/chromedriver");
```

- **Note for Windows Users**: If you are using Windows, ensure that the path includes the `.exe` extension like this:
  ```java
  System.setProperty("webdriver.chrome.driver", "resources/chromedriver.exe");
  ```

#### 2. **Launch the Browser**
   - Instantiate the WebDriver using `ChromeDriver`:

   ```java
   driver = new ChromeDriver();
   ```

#### 3. **Navigate to a URL**
   - Use the `get()` method to navigate to a website. In this example, we use an open-source project called "The Internet" for test automation practice.

   ```java
   driver.get("https://the-internet.herokuapp.com/");
   ```

#### 4. **Print the Page Title**
   - Use `driver.getTitle()` to print the title of the current page to the console.

   ```java
   System.out.println(driver.getTitle());
   ```

#### 5. **Manage Browser Window**
   - You can manipulate the browser window in multiple ways:
   
     - **Maximize the window:**
     ```java
     driver.manage().window().maximize();
     ```

     - **Fullscreen mode:**
     ```java
     driver.manage().window().fullscreen();
     ```

     - **Set custom size (e.g., mobile view):**
     ```java
     Dimension size = new Dimension(375, 812); // iPhone X size
     driver.manage().window().setSize(size);
     ```

#### 6. **Close the Browser**
   - After the test is complete, use `driver.quit()` to close the browser and end the session.

   ```java
   driver.quit();
   ```

---

### Running the Test

1. **Main Method for Execution:**
   - To run the test, include a main method that creates an instance of the `BaseTests` class and calls the `setUp` method.

   ```java
   public static void main(String[] args){
       BaseTests test = new BaseTests();
       test.setUp();
   }
   ```

2. **Run the Test:**
   - Right-click on the `BaseTests` class and select **Run**.
   - The browser will launch, navigate to the specified URL, print the page title, and then close.

---

### Example Code

```java
package base;

import org.openqa.selenium.Dimension;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.chrome.ChromeDriver;

public class BaseTests {

    private WebDriver driver;

    public void setUp() {
        // Set the path for ChromeDriver
        System.setProperty("webdriver.chrome.driver", "resources/chromedriver");

        // Initialize WebDriver
        driver = new ChromeDriver();

        // Navigate to the URL
        driver.get("https://the-internet.herokuapp.com/");

        // 1. Maximize the browser window
        driver.manage().window().maximize();

        // 2. Fullscreen the browser
        driver.manage().window().fullscreen();

        // 3. Set specific window size (iPhone X resolution)
        Dimension size = new Dimension(375, 812);
        driver.manage().window().setSize(size);

        // Print page title
        System.out.println(driver.getTitle());

        // Close the browser
        driver.quit();
    }

    public static void main(String[] args) {
        BaseTests test = new BaseTests();
        test.setUp();
    }
}
```

---

### Conclusion

This project demonstrates the basic setup for running Selenium WebDriver tests using Java. It covers:
- WebDriver setup
- Browser window management
- Navigating to a URL
- Closing the browser

You can extend this project to include more tests and browser interactions as needed!

## WebDriver Interaction with Browser Elements

WebDriver is used to interact with a browser. In order to interact with elements on the browser, WebDriver must be able to locate those elements, which are typically defined in the HTML or Document Object Model (DOM).

Every element on a webpage, whether it is a link, title, or button, can be interacted with. We need to instruct WebDriver on which element to interact with and how to interact with it.

### Key Concepts:
1. **Locating Elements**: To interact with elements on a web page, Selenium WebDriver uses the `findElement` and `findElements` methods.
    - `findElement`: Locates a single element (e.g., a link, button, etc.) based on a given locator strategy.
    - `findElements`: Returns a list of elements that match the locator, useful for scenarios where there are multiple elements of the same type (e.g., all links).

2. **Locator Strategies**: WebDriver provides several strategies to locate elements, such as:
    - By `linkText`: Find an element based on the visible text of a link.
    - By `tagName`: Finds elements based on the tag name (e.g., `<a>`, `<div>`, etc.).

3. **Example**:
    - Using `findElement(By.linkText("Input"))` to find and click a link with the text "Input".
    - Using `findElements(By.tagName("a"))` to count all `<a>` (link) elements on a page.

4. **NoSuchElementException**: This exception is thrown if WebDriver is unable to find an element on the page. Reasons include incorrect locators or trying to interact with an element that isn’t present yet.


## Identifying Web Elements
To interact with elements, WebDriver needs to locate them based on information provided in the HTML or DOM. For example, you can use browser developer tools (right-click on an element and select "Inspect") to view the HTML structure of an element.

Elements can be identified by:
- ID
- Class Name
- CSS Selector
- Link Text
- Tag Name
- XPath

## Locating an Element using `findElement`
The `findElement` method is used to locate a single web element on a page. It requires a locator strategy (e.g., `By.linkText`, `By.id`) to specify how to find the element. Once located, we can interact with the element (e.g., clicking a link).

### Example: Clicking a Link
Here’s an example where WebDriver locates a link with the text "Inputs" and clicks it:

```java
package base;

import org.openqa.selenium.By;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.WebElement;
import org.openqa.selenium.chrome.ChromeDriver;

public class BaseTests {

    private WebDriver driver;

    public void setUp(){
        System.setProperty("webdriver.chrome.driver", "resources/chromedriver");
        driver = new ChromeDriver();
        driver.get("https://the-internet.herokuapp.com/");

        WebElement inputsLink = driver.findElement(By.linkText("Input"));
        inputsLink.click();

        driver.quit();
    }

    public static void main(String args[]){
        BaseTests test = new BaseTests();
        test.setUp();
    }
}
```
In this example, the program:
1. Opens Chrome and navigates to the webpage.
2. Locates the "Input" link using `findElement(By.linkText("Input"))`.
3. Clicks the link.
4. Closes the browser.

## Locating Multiple Elements using `findElements`
The `findElements` method is used to locate multiple elements on a page. It returns a list of WebElements. This is useful when you need to interact with multiple similar elements, such as all links on a page.

### Example: Counting Links
The following example finds all links (elements with the `<a>` tag) on the page and prints the number of links found:

```java
List<WebElement> links = driver.findElements(By.tagName("a"));
System.out.println(links.size());
```
This will print the total number of links found on the page.

## Handling Non-Existent Elements
If you attempt to locate an element that does not exist on the page, WebDriver throws a `NoSuchElementException`. This occurs when the element cannot be found using the provided locator.

For example, if you try to locate a link with the text "Angie" that does not exist:

```java
WebElement inputsLink = driver.findElement(By.linkText("Angie"));
```
This will result in a `NoSuchElementException`.

### Common Causes of `NoSuchElementException`
1. The element does not exist on the page.
2. The locator is incorrect.
3. The element may not be available in the current state of the page (e.g., page hasn't fully loaded).

## Elements interactions 

In this chapter, we'll explore how to manage **element interactions** in test automation projects using the **Page Object Model (POM)** design pattern.

Typically, test automation projects consist of two layers:
1. **Framework Layer**: Contains the automation framework, including all interactions with the web browser and page elements.
2. **Test Layer**: Focuses purely on test cases.

To demonstrate this, let's look at a common project structure. Within the `src` folder, there are two subfolders: `main` for the framework and `test` for the test files. The framework is where the interactions (e.g., finding elements, clicking links) should reside, while the tests should only specify what actions are to be taken (e.g., "click the login button").

### **Example**: Using the Page Object Model
We'll use the **Page Object Model (POM)**, one of the most popular patterns for test automation, which helps keep the test and framework code clean and separate.

1. **Project Setup**:
    - The `main` folder contains a `pages` package that will hold the page object classes.
    - Each page of the web application will be represented by a corresponding class in this package.

2. **Creating a Page Object**:
    - For example, let's create a `HomePage` class to represent the homepage of an application.
    ```java
    package pages;
    
    import org.openqa.selenium.By;
    import org.openqa.selenium.WebDriver;
    
    public class HomePage {
        private WebDriver driver;
        private By formAuthenticationLink = By.linkText("Form Authentication");
    
        public HomePage(WebDriver driver) {
            this.driver = driver;
        }
    
        public LoginPage clickFormAuthentication() {
            driver.findElement(formAuthenticationLink).click();
            return new LoginPage(driver);
        }
    }
    ```

    Here, the `HomePage` class has a method to click on the "Form Authentication" link. The `clickFormAuthentication` method returns a new instance of the `LoginPage` class because the action of clicking on the link navigates to a new page.

3. **Creating a `LoginPage` Class**:
    When the link is clicked, the `LoginPage` class represents the next page in the sequence:
    ```java
    package pages;
    
    import org.openqa.selenium.By;
    import org.openqa.selenium.WebDriver;
    
    public class LoginPage {
        private WebDriver driver;
        private By usernameField = By.id("username");
        private By passwordField = By.id("password");
        private By loginButton = By.cssSelector("#login button");
    
        public LoginPage(WebDriver driver) {
            this.driver = driver;
        }
    
        public void setUsername(String username) {
            driver.findElement(usernameField).sendKeys(username);
        }
    
        public void setPassword(String password) {
            driver.findElement(passwordField).sendKeys(password);
        }
    
        public SecureAreaPage clickLoginButton() {
            driver.findElement(loginButton).click();
            return new SecureAreaPage(driver);
        }
    }
    ```

    The `LoginPage` class has methods to interact with the username, password fields, and the login button.

4. **Secure Area Page**:
    After successfully logging in, we navigate to the `SecureAreaPage`:
    ```java
    package pages;
    
    import org.openqa.selenium.By;
    import org.openqa.selenium.WebDriver;
    
    public class SecureAreaPage {
        private WebDriver driver;
        private By statusAlert = By.id("flash");
    
        public SecureAreaPage(WebDriver driver) {
            this.driver = driver;
        }
    
        public String getAlertText() {
            return driver.findElement(statusAlert).getText();
        }
    }
    ```

    The `SecureAreaPage` class contains methods to check if the login was successful, for example, by retrieving the text of the status alert.

### Key Takeaways:
- The **Page Object Model** separates the logic of interacting with the browser (framework) from the test scripts (test layer).
- Each page in your application has its own class with methods for interacting with elements on that page.
- Use encapsulation to hide the internal details of how elements are found and interacted with.

By following the POM design pattern, you ensure that your test code is clean, maintainable, and easier to scale as the application grows.

## creating a test

It looks like you've set up the full framework and test for a successful login using Selenium WebDriver with TestNG for verification. Here's a recap of the key steps and elements in this process:

### Framework Overview

1. **BaseTests Class**: 
    - Handles setup and teardown of the WebDriver.
    - Uses `@BeforeClass` to initiate the browser and `@AfterClass` to close it after tests.
    - Provides access to the `HomePage` object, which represents the main page of the application.

2. **LoginTests Class**:
    - Contains a test method `testSuccessfulLogin()`, which tests the login functionality.
    - Inherits from `BaseTests` to reuse the setup and teardown logic.
    - Uses the `homePage` object to navigate through the app and perform actions.

3. **TestNG Annotations**:
    - `@Test` to mark the test methods.
    - `@BeforeClass` and `@AfterClass` to handle setup and teardown before and after test execution.

4. **TestNG Assertions**:
    - Using assertions to verify the results, particularly `assertTrue()` to check that the login success message contains the expected text, ignoring extra elements like the "x" for closing the alert.

### Final Code Snippet

#### BaseTests.java
```java
package base;

import org.openqa.selenium.WebDriver;
import org.openqa.selenium.chrome.ChromeDriver;
import org.testng.annotations.AfterClass;
import org.testng.annotations.BeforeClass;
import pages.HomePage;

public class BaseTests {

    private WebDriver driver;
    protected HomePage homePage;

    @BeforeClass
    public void setUp(){
        System.setProperty("webdriver.chrome.driver", "resources/chromedriver");
        driver = new ChromeDriver();

        driver.get("https://the-internet.herokuapp.com/");
        homePage = new HomePage(driver);
    }

    @AfterClass
    public void tearDown(){
        driver.quit();
    }
}
```

#### LoginTests.java
```java
package login;

import base.BaseTests;
import org.testng.annotations.Test;
import pages.LoginPage;
import pages.SecureAreaPage;

import static org.testng.Assert.*;

public class LoginTests extends BaseTests {

    @Test
    public void testSuccessfulLogin() {
        LoginPage loginPage = homePage.clickFormAuthentication();
        loginPage.setUsername("tomsmith");
        loginPage.setPassword("SuperSecretPassword!");
        SecureAreaPage secureAreaPage = loginPage.clickLoginButton();
        
        // Assert that the alert contains the correct message
        assertTrue(secureAreaPage.getAlertText()
                .contains("You logged into a secure area!"), "Alert text is incorrect");
    }
}
```

### Key Selenium Methods Used

- **Clicking Elements**: `click()` is used to trigger button clicks like the login button.
- **Entering Text**: `sendKeys()` allows text input into fields like username and password.
- **Reading Text**: `getText()` retrieves the text content from an element, such as the success alert.

### Debugging & Adjustments

- Initially, the test failed due to extra space and characters like "x" in the alert message. By switching from `assertEquals()` to `assertTrue()` and checking if the alert message contains the relevant part, you avoid dealing with exact matches that can be affected by extra HTML elements.
  
### Running Tests
- You can right-click and run `LoginTests` from your IDE, and if the test passes, you will see green indicators.

This setup should now allow you to automate the login test successfully. Let me know if you need further help or clarification on any part!

## drop down 

You can continue creating your `DropdownTest` class by following the approach below. The goal is to ensure that the test inherits from `BaseTests`, uses the framework methods you've created, and performs assertions to validate the interaction with the dropdown menu.

### Step-by-Step Implementation for `DropdownTest`:

1. **Create a new test class `DropdownTest`:**

   Inside your `tests` package, create a new class called `DropdownTest.java`.

```java
package tests;

import org.testng.annotations.Test;
import static org.testng.Assert.assertEquals;
import pages.DropdownPage;

public class DropdownTest extends BaseTests {

    @Test
    public void testSelectOption() {
        // Navigate to Dropdown page from the home page
        DropdownPage dropdownPage = homePage.clickDropDown();

        // Select "Option 1" from the dropdown menu
        dropdownPage.selectFromDropDown("Option 1");

        // Assert that "Option 1" is selected
        var selectedOptions = dropdownPage.getSelectedOptions();
        assertEquals(selectedOptions.size(), 1, "Incorrect number of selections");
        assertEquals(selectedOptions.get(0), "Option 1", "Option 1 is not selected");
    }
}
```

### Explanation of the Code:

1. **Navigate to the Dropdown Page:**  
   The `homePage.clickDropDown()` method will click the "Dropdown" link, and it will return an instance of the `DropdownPage` class, allowing you to interact with the dropdown.

2. **Select an Option:**  
   The `dropdownPage.selectFromDropDown("Option 1")` method will select "Option 1" from the dropdown list using the `selectByVisibleText` method from the `Select` class.

3. **Verify the Selection:**  
   After selecting the option, the `dropdownPage.getSelectedOptions()` method will return a list of selected options. The test asserts that exactly one option was selected and that the selected option matches "Option 1".

### Add Another Test for Option 2 (Optional):

You can add another test method to check if "Option 2" can be selected in the same way.

```java
@Test
public void testSelectOptionTwo() {
    DropdownPage dropdownPage = homePage.clickDropDown();
    dropdownPage.selectFromDropDown("Option 2");

    var selectedOptions = dropdownPage.getSelectedOptions();
    assertEquals(selectedOptions.size(), 1, "Incorrect number of selections");
    assertEquals(selectedOptions.get(0), "Option 2", "Option 2 is not selected");
}
```

### Summary:

- The `DropdownPage` class provides a flexible way to interact with dropdown elements using the Selenium `Select` class.
- The test class `DropdownTest` inherits from `BaseTests`, ensuring that all common setup steps are handled.
- The test methods use assertions to validate that the correct option is selected from the dropdown. 

This structure can easily be expanded or reused for different tests involving dropdown menus.

## chapter 5

class, FigureCaption, we need to provide methods that allow the test to verify the elements within the caption (i.e., the username and the “View profile” link).

We can inspect the DOM for the specific elements we want. First, let’s check the username. In the DOM, we can see that the username is encapsulated within a heading tag (`<h5>`), and the "View profile" link is an anchor (`<a>`). We will create two methods in our `FigureCaption` class to retrieve the username text and the link.

Let’s go ahead and implement that.

The provided code is a Selenium-based Java class that represents a page where hover actions can be performed over elements (e.g., figures). When hovering over these elements, captions become visible, and the class allows you to interact with these captions.

Here's a detailed explanation and comments on the code:

```java
package pages; // This line declares the package where the class resides.

import org.openqa.selenium.By;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.WebElement;
import org.openqa.selenium.interactions.Actions;

/**
 * Represents a page where hovering over figures shows captions.
 */
public class HoversPage {
    private WebDriver driver; // WebDriver instance used to interact with the browser.

    // Locators for the figure elements and their captions.
    private By figureBox = By.className("figure"); // Locator for figure elements (divs with class "figure").
    private By boxCaption = By.className("figcaption"); // Locator for caption elements (divs with class "figcaption").

    /**
     * Constructor for initializing the HoversPage class with a WebDriver.
     * @param driver WebDriver instance used to control the browser.
     */
    public HoversPage(WebDriver driver){
        this.driver = driver;
    }

    /**
     * This method performs a hover action over a figure element.
     * @param index The figure index to hover over (starts at 1, so 1 corresponds to the first figure).
     * @return A FigureCaption object that provides access to the caption details.
     */
    public FigureCaption hoverOverFigure(int index){
        // Find the figure element by its index (index - 1 to adjust for 0-based indexing).
        WebElement figure = driver.findElements(figureBox).get(index - 1);

        // Create an Actions object to perform complex user interactions like hovering.
        Actions actions = new Actions(driver);
        actions.moveToElement(figure).perform(); // Perform the hover action.

        // Return a new FigureCaption object for the caption element related to the hovered figure.
        return new FigureCaption(figure.findElement(boxCaption));
    }

    /**
     * Nested class that represents the caption of a figure.
     * Provides methods to interact with the caption, like checking if it's displayed,
     * getting the title, or getting the link associated with the caption.
     */
    public class FigureCaption{

        private WebElement caption; // The WebElement representing the figure's caption.
        private By header = By.tagName("h5"); // Locator for the caption header (assumed to be inside an <h5> tag).
        private By link = By.tagName("a"); // Locator for the caption link (assumed to be inside an <a> tag).

        /**
         * Constructor for initializing the FigureCaption class.
         * @param caption The WebElement that represents the caption of a figure.
         */
        public FigureCaption(WebElement caption){
            this.caption = caption;
        }

        /**
         * Checks if the caption is currently displayed on the page.
         * @return true if the caption is visible, false otherwise.
         */
        public boolean isCaptionDisplayed(){
            return caption.isDisplayed();
        }

        /**
         * Retrieves the title (text inside the <h5> element) of the caption.
         * @return The caption title as a String.
         */
        public String getTitle(){
            return caption.findElement(header).getText();
        }

        /**
         * Retrieves the URL (href attribute) of the link inside the caption.
         * @return The URL as a String.
         */
        public String getLink(){
            return caption.findElement(link).getAttribute("href");
        }

        /**
         * Retrieves the link text inside the caption.
         * @return The link text as a String.
         */
        public String getLinkText(){
            return caption.findElement(link).getText();
        }
    }
}
```

### Key Features:
1. **Hovering over Figures**: The main method, `hoverOverFigure(int index)`, allows hovering over a figure on the page, identified by its index. It uses Selenium's `Actions` class to simulate the hover action.
2. **Captions**: When you hover over a figure, its caption becomes visible. The `FigureCaption` class provides methods to interact with that caption, including checking if it's displayed, retrieving its title, and extracting the link and its text.
3. **Nested Class**: The `FigureCaption` class is nested inside the `HoversPage` class. This is done because the caption is closely tied to the figure, and its behavior is only relevant in the context of this page.

### How It Works:
- **figureBox**: This locates all the figures on the page by the class name "figure".
- **boxCaption**: This locates the caption inside each figure by the class name "figcaption".
- When you call `hoverOverFigure(index)`, it finds the corresponding figure element, hovers over it using Selenium's `Actions`, and returns a `FigureCaption` object that allows interaction with the displayed caption.
- **FigureCaption**: This class allows access to details within the caption, such as the title (in an `<h5>` element), a link (in an `<a>` element), and methods to check if the caption is displayed.



### Writing a Test for Verification
Now, let’s write a test to hover over the first image and verify the username and link.

```java
package hover; // The package where the test class is located.

import base.BaseTests; // Importing the BaseTests class, which contains common setup/teardown methods for the tests.
import org.testng.annotations.Test; // Importing TestNG's @Test annotation for defining test methods.
import pages.HoversPage; // Importing the HoversPage class to interact with the page being tested.

import static org.testng.Assert.*; // Importing static assert methods from TestNG to perform assertions in the tests.

public class HoverTests extends BaseTests {

    /**
     * Test method to verify that hovering over the first figure displays the correct caption.
     */
    @Test
    public void testHoverUser1(){
        // Navigate to the Hover page using the homePage object from the BaseTests class.
        var hoversPage = homePage.clickHovers();

        // Hover over the first figure and retrieve the caption.
        var caption = hoversPage.hoverOverFigure(1);

        // Check if the caption is displayed after hovering.
        assertTrue(caption.isCaptionDisplayed(), "Caption not displayed");

        // Verify that the caption title is "name: user1".
        assertEquals(caption.getTitle(), "name: user1", "Caption title incorrect");

        // Verify that the caption link text is "View profile".
        assertEquals(caption.getLinkText(), "View profile", "Caption link text incorrect");

        // Verify that the caption link ends with "/users/1".
        assertTrue(caption.getLink().endsWith("/users/1"), "Link incorrect");
    }
}

```

### Summary:
- We created a hover interaction using the `Actions` class.
- We modeled the caption area with an inner class `FigureCaption` to verify the elements.
- We wrote a test to hover over an image and verify the username and profile link.

This setup should help you interact with the hover functionality in your test framework, making it easier to handle advanced user interactions like hovering.

## chapter 6

This example demonstrates how to use Selenium WebDriver's `sendKeys` method to simulate keyboard actions in a web application. Specifically, you're sending special keys like backspace and multiple key combinations using the `Keys` class in Selenium.

Here’s a breakdown of the process for creating the `KeyPressesPage` and `KeysTests` classes to simulate these actions:

### 1. **KeyPressesPage Class:**
   - **Setup WebDriver and Locators**: You define locators for the input field and the result text that displays after entering keys. The `By.id("target")` is used for the input field and `By.id("result")` for the result text.
   - **enterText Method**: This method takes a string input and sends it to the target input field using `sendKeys`. 
   - **getResult Method**: This retrieves the text that appears on the page after a key press.

### 2. **KeysTests Class:**
   - **testBackspace Method**: 
     - You navigate to the `KeyPressesPage` and simulate typing a character followed by the backspace key.
     - Selenium's `Keys.BACK_SPACE` constant is used to simulate the backspace action.
     - You verify the outcome with an assertion, ensuring the correct result is displayed (`"You entered: BACK_SPACE"`).
   
   - **testPi Method**:
     - You simulate typing the Pi character (`π`) by using a combination of `Keys.ALT` and `"p"`, and follow it up by typing `=3.14`.
     - The `Keys.chord` method is used to combine key presses (ALT + "p") for typing the Pi character.

### Full Code:

#### **KeyPressesPage.java**
```java
package pages; // Declares the package where the class resides.

import org.openqa.selenium.By; // Import Selenium's By class to locate elements on the webpage.
import org.openqa.selenium.Keys; // Import Selenium's Keys class to simulate keyboard key presses.
import org.openqa.selenium.WebDriver; // Import Selenium's WebDriver interface for interacting with the browser.

public class KeyPressesPage {

    private WebDriver driver; // WebDriver instance for controlling the browser.

    // Locators for the input field and the result text element on the page.
    private By inputField = By.id("target"); // Locator for the input field where keys are entered (ID: "target").
    private By resultText = By.id("result"); // Locator for the result text area (ID: "result").

    /**
     * Constructor for initializing the KeyPressesPage class.
     * @param driver WebDriver instance to interact with the browser.
     */
    public KeyPressesPage(WebDriver driver){
        this.driver = driver;
    }

    /**
     * Method to enter text into the input field.
     * @param text The string to be entered into the input field.
     */
    public void enterText(String text){
        // Find the input field using its locator and enter the specified text.
        driver.findElement(inputField).sendKeys(text);
    }

    /**
     * Method to enter the mathematical constant Pi (π) into the input field.
     * This simulates pressing ALT + P followed by "=3.14".
     */
    public void enterPi(){
        // Use the chord method to simulate pressing multiple keys at the same time (ALT + P),
        // and then add the string "=3.14" to the input.
        enterText(Keys.chord(Keys.ALT, "p") + "=3.14");
    }

    /**
     * Method to retrieve the result text that appears after key presses.
     * @return The result text as a string.
     */
    public String getResult(){
        // Find the result text element using its locator and return its text content.
        return driver.findElement(resultText).getText();
    }
}

```

#### **KeysTests.java**
```java
package keys; // Declares the package where the class resides.

import base.BaseTests; // Importing the BaseTests class to inherit common setup/teardown functionalities.
import org.openqa.selenium.Keys; // Importing Selenium's Keys class to simulate keyboard key presses.
import org.testng.annotations.Test; // Importing TestNG's @Test annotation for defining test methods.

import static org.testng.Assert.assertEquals; // Importing the static assertEquals method for assertions in the tests.

public class KeysTests extends BaseTests {

    /**
     * Test case to simulate entering the letter "A" followed by a backspace,
     * and verify that the expected result is returned.
     */
    @Test
    public void testBackspace(){
        // Navigate to the KeyPresses page.
        var keyPage = homePage.clickKeyPresses();

        // Enter the letter "A" followed by a backspace key press.
        keyPage.enterText("A" + Keys.BACK_SPACE);

        // Verify that the result message indicates the BACK_SPACE key was pressed.
        assertEquals(keyPage.getResult(), "You entered: BACK_SPACE");
    }

    /**
     * Test case to simulate entering the Pi symbol (π).
     * This test currently stops short of full validation, as noted in the comments.
     */
    @Test
    public void testPi(){
        // Navigate to the KeyPresses page.
        var keyPage = homePage.clickKeyPresses();

        // Simulate entering the Pi symbol.
        keyPage.enterPi();

        /*
            NOTE: we didn't finish this test in the video.
            We debugged to watch it enter the Pi key.
            (No assertion is present since this test is unfinished)
         */
    }
}

```

### Explanation:
- **`Keys.chord`**: This method allows you to combine multiple keys in one action. For instance, `Keys.chord(Keys.ALT, "p")` holds down the ALT key while typing the "p" key.
- **`Keys.BACK_SPACE`**: Represents the backspace key, which is used to delete a character after typing it.

### Running the Tests:
- When you run `testBackspace`, the test will:
  1. Click the "Key Presses" link.
  2. Enter the character "A" followed by a backspace key.
  3. Assert that the result text shows "You entered: BACK_SPACE".

- When you run `testPi`, the test will:
  1. Navigate to the Key Presses page.
  2. Enter the Pi character followed by "=3.14".
  3. Optionally, you could add an assertion to verify the exact input.

This method provides a flexible way to simulate various key combinations and test how web applications respond to keyboard input.

### Chapter 7 

### Overview: Popups and Interacting with Them

In this chapter, we will explore how to handle different types of popups in web automation. Specifically, we'll focus on three types of popups:
1. JavaScript Alerts
2. File Upload Popups
3. Modal Dialogs

We’ll start by writing a test that interacts with JavaScript alerts.

---

### Step 1: Identifying and Interacting with JavaScript Alerts

To begin, we'll access a test application by clicking on the "JavaScript Alerts" link. The goal is to write a test that interacts with the alert, specifically clicking the "Click for JS Alert" button.

#### Inspecting the Button
When inspecting the button, it triggers a JavaScript function that displays a popup. This is the alert that contains the message: “I am a JS Alert.”

- **Key Observation:** The alert itself does not exist in the DOM, which means we need to interact with it in a unique way, as it’s not directly inspectable.

Once we click the "OK" button on the alert, a result message is displayed on the page. We can assert this result in our test.

---

### Step 2: Writing the Test for Alerts

We’ve already created a method in our **HomePage** class to navigate to the JavaScript Alerts page:

```java
public AlertsPage clickJavaScriptAlerts() {
    clickLink("JavaScript Alerts");
    return new AlertsPage(driver);
}
```
This method will return an `AlertsPage` object, which we will use to interact with the popups.

#### Creating the AlertsPage Class

```java
package pages;

import org.openqa.selenium.WebDriver;

public class AlertsPage {
    private WebDriver driver;

    public AlertsPage(WebDriver driver) {
        this.driver = driver;
    }
}
```

Now, let’s define the element for the "Click for JS Alert" button. Since this button has no specific ID, we’ll use an XPath selector based on its text:

```java
private By triggerAlertButton = By.xpath(".//button[text()='Click for JS Alert']");
```

#### Clicking the Button and Handling the Alert

We’ll create a method to click the alert button:

```java
public void triggerAlert() {
    driver.findElement(triggerAlertButton).click();
}
```

Next, we handle the alert itself. Since the alert is not part of the DOM, we’ll use the `switchTo().alert()` method:

```java
public void acceptAlert() {
    driver.switchTo().alert().accept();
}
```

`driver.switchTo().alert()` returns a `Alert` object that can be used to perform actions like accepting, dismissing, reading text, or entering text (for prompt dialogs).

**Alert Object**:

After switching to the alert, you can use various methods provided by the Alert interface to interact with it:

- `accept()`: Clicks the "OK" button on the alert.
- `dismiss()`: Clicks the "Cancel" button (or closes the alert).
- `getText()`: Retrieves the message displayed in the alert.
- `sendKeys(String text)`: Sends input text to a prompt (used only for prompt dialogs where the user can input text).



### Step 3: Writing the Test Case

In the test class `AlertTests`, we'll create a test to interact with the alert:

```java
@Test
public void testAcceptAlert() {
    var alertsPage = homePage.clickJavaScriptAlerts();
    alertsPage.triggerAlert();
    alertsPage.acceptAlert();
    assertEquals(alertsPage.getResult(), "You successfully clicked an alert", "Results text incorrect");
}
```

#### Handling Results in AlertsPage

We’ll also add a method in `AlertsPage` to retrieve the result text that appears after the alert is accepted:

```java
private By results = By.id("result");

public String getResult() {
    return driver.findElement(results).getText();
}
```

---

### Step 4: Writing Additional Tests for Confirm and Prompt Alerts

#### Confirm Alert Test

We can now write a similar test for the "JS Confirm" button:

```java
@Test
public void testGetTextFromAlert() {
    var alertsPage = homePage.clickJavaScriptAlerts();
    alertsPage.triggerConfirm();

    String text = alertsPage.alert_getText();
    alertsPage.alert_clickToDismiss();

    assertEquals(text, "I am a JS Confirm", "Alert text incorrect");
}
```

#### Prompt Alert Test

For prompt alerts, we need to enter text and assert the result:

```java
@Test
public void testSetInputInAlert() {
    var alertsPage = homePage.clickJavaScriptAlerts();
    alertsPage.triggerPrompt();

    String text = "TAU rocks!";
    alertsPage.alert_setInput(text);
    alertsPage.alert_clickToAccept();

    assertEquals(alertsPage.getResult(), "You entered: " + text, "Results text incorrect");
}
```

---

### Step 5: Running Multiple Tests in a Class

When running multiple tests in a single class, make sure the state of the application is reset between tests. If not, subsequent tests might fail because the application is not on the expected page.

One approach is to ensure that each test starts on the home page by adding logic in the `BaseTests` class to verify the state before each test execution.

```java
@BeforeMethod
public void ensureOnHomePage() {
    // Logic to ensure we are on the home page before each test runs
}
```

---

### Summary

We’ve written tests for interacting with JavaScript alerts, including:
1. Accepting an alert.
2. Dismissing a confirmation alert.
3. Entering text into a prompt alert.

Throughout, we ensured the proper interaction with the DOM and alerts, and we utilized assertions to verify the expected results. Additionally, we’ve discussed strategies for running multiple tests and ensuring the application's state is consistent between tests.

## chapter 7.2

Let's dive into another type of pop-up—one that involves file uploads.

### File Upload Pop-up

In this scenario, we’re dealing with a Windows file upload pop-up, which is different from the typical JavaScript alert pop-ups. You can't use Selenium's `Alert` class to interact with this type of pop-up because it’s native to the operating system. Instead, we bypass the whole process by directly sending the absolute path of the file to the input field within the form.

### Inspecting the Page

When we click on the **Choose File** button, it triggers a native Windows pop-up for selecting files. Instead of automating the interaction with this pop-up, we'll pass the file path directly to the input field on the form.

Here's how we handle it:

1. **Inspect the form:** When inspecting the form, you’ll see an input field that we’re interested in. This field accepts the file path.
2. **Send the absolute path:** We send the absolute file path directly to this input field.

### File Upload Page Class

We create a new page class called `FileUploadPage` where we manage the file upload operation. Here’s the code for that:

```java
#FileUploadPage.java
package pages;

import org.openqa.selenium.By;
import org.openqa.selenium.WebDriver;

public class FileUploadPage {

    private WebDriver driver;
    private By inputField = By.id("file-upload");
    private By uploadButton = By.id("file-submit");

    public FileUploadPage(WebDriver driver){
        this.driver = driver;
    }

    public void clickUploadButton(){
        driver.findElement(uploadButton).click();
    }

    /**
     * Provides path of file to the form then clicks Upload button
     * @param absolutePathOfFile The complete path of the file to upload
     */
    public void uploadFile(String absolutePathOfFile){
        driver.findElement(inputField).sendKeys(absolutePathOfFile);
        clickUploadButton();
    }
}
```

### Key Components
- **Elements:** We've defined two elements: the file input field (`inputField`) and the upload button (`uploadButton`).
- **Methods:** We have methods to click the upload button and upload the file. The file path is passed to the `uploadFile` method, which sends it to the input field and triggers the upload button.

### Adding a Method to HomePage

In the **HomePage** class, we add a method to navigate to the File Upload page:

```java
public FileUploadPage clickFileUpload(){
    clickLink("File Upload");
    return new FileUploadPage(driver);
}
```

### Writing the Test

Now, let’s create a test class called `FileUploadTests` to verify file uploads. This class will extend `BaseTests`, just like the alert tests.

```java
#FileUploadTests.java

package alerts;

import base.BaseTests;
import org.testng.annotations.Test;

public class FileUploadTests extends BaseTests {

    @Test
    public void testFileUpload(){
        var uploadPage = homePage.clickFileUpload();
        uploadPage.uploadFile("/Users/angie/workspace/testautomationu/webdriver_java/resources/chromedriver");
    }
}
```

### Absolute File Path

We need to pass the absolute file path, which can be copied from your file system. The following line in the test will handle that:

```java
uploadPage.uploadFile("/Users/angie/workspace/testautomationu/webdriver_java/resources/chromedriver");
```

### Verifying the Upload

Once the file is uploaded, we want to verify that the correct file was uploaded. The page displays a confirmation message like **“File Uploaded!”**, along with the name of the uploaded file. We add another method in the `FileUploadPage` to check the uploaded file:

```java
private By uploadedFiles = By.id("uploaded-files");

public String getUploadedFiles(){
    return driver.findElement(uploadedFiles).getText();
}
```

### Final Test Code

Here’s the updated test with file verification:

```java
package alerts;

import base.BaseTests;
import org.testng.annotations.Test;
import static org.testng.Assert.assertEquals;

public class FileUploadTests extends BaseTests {

    @Test
    public void testFileUpload(){
        var uploadPage = homePage.clickFileUpload();
        uploadPage.uploadFile("/Users/angie/workspace/testautomationu/webdriver_java/resources/chromedriver");

        assertEquals(uploadPage.getUploadedFiles(), "chromedriver", "Uploaded files incorrect");
    }
}
```

### Running the Test

Once you run the test, Selenium will:
1. Send the file path directly to the input field.
2. Click the upload button.
3. Verify that the file uploaded correctly by checking the page content.

This method is simple and avoids the need to interact with the native Windows pop-up, making file uploads much more efficient.



## chapter7.3

Modals are indeed another type of pop-up that can appear on a web page. Unlike native OS pop-ups like file dialogs or JavaScript alerts, modals are part of the DOM (Document Object Model), meaning you can interact with them using standard Selenium techniques, just like any other element on the page.

### Key Points About Modals:
1. **Modal Behavior:**
   - A modal is a dialog box that overlays on top of the main content and often disables interaction with the main page until it is closed.
   - When a modal appears, the background page may be dimmed, and no other interaction is possible except with the modal.

2. **Handling Modals in Selenium:**
   - Since modals are part of the DOM, you can interact with their elements directly.
   - You can inspect the modal and locate the buttons or text fields within it using `By` locators like `By.id`, `By.className`, or `By.xpath`.

3. **Accessing Modal Elements:**
   - For example, to interact with the "Close" button inside the modal, you'd first locate the modal itself, then navigate to the specific button.

Let’s walk through how you can handle a modal in a Selenium test.

### Example Implementation for Handling Modals:

1. **Modal Page Object (`ModalPage.java`):**

```java
package pages;

import org.openqa.selenium.By;
import org.openqa.selenium.WebDriver;

public class ModalPage {

    private WebDriver driver;
    
    // Locators for modal components
    private By closeButton = By.cssSelector(".modal-footer .btn");
    private By modal = By.className("modal");

    public ModalPage(WebDriver driver){
        this.driver = driver;
    }

    // Method to close the modal
    public void closeModal(){
        driver.findElement(closeButton).click();
    }

    // Check if the modal is displayed
    public boolean isModalDisplayed(){
        return driver.findElement(modal).isDisplayed();
    }
}
```

In this class:
- We define the modal's close button using its CSS selector.
- The `closeModal()` method clicks the close button.
- The `isModalDisplayed()` method verifies if the modal is visible.

2. **Home Page Method for Clicking Entry Ad:**

You’ll need a method in your home page class to navigate to the Entry Ad page (where the modal appears):

```java
public ModalPage clickEntryAd(){
    clickLink("Entry Ad");
    return new ModalPage(driver);
}
```

This method navigates to the Entry Ad page and returns a new `ModalPage` object.

3. **Test for the Modal (`ModalTests.java`):**

```java
package tests;

import base.BaseTests;
import org.testng.annotations.Test;
import static org.testng.Assert.assertFalse;

public class ModalTests extends BaseTests {

    @Test
    public void testCloseModal(){
        var modalPage = homePage.clickEntryAd();

        // Verify modal is displayed
        assertTrue(modalPage.isModalDisplayed(), "Modal was not displayed");

        // Close the modal
        modalPage.closeModal();

        // Verify modal is no longer displayed
        assertFalse(modalPage.isModalDisplayed(), "Modal was still displayed after close");
    }
}
```

### Test Breakdown:
- The test navigates to the Entry Ad page where the modal appears.
- It asserts that the modal is visible using the `isModalDisplayed()` method.
- It closes the modal using `closeModal()`.
- Finally, it verifies that the modal is no longer displayed after closing it.

### Handling Modal Interaction Restrictions:
- **Interaction Blocking:** When the modal is active, you cannot interact with any other elements on the main page. If you try to click or interact with elements behind the modal, WebDriver will throw an exception. Therefore, you need to handle the modal first (close it or complete any actions inside it) before interacting with other page elements.
  
### Conclusion:
Modals are part of the page's DOM, and they can be interacted with directly using Selenium WebDriver. You can treat modal elements like any other page element by using `findElement()` to locate and manipulate them, ensuring that you close or handle the modal before continuing with interactions on the main page.

## chapter 8

The key lesson from this chapter is the importance of switching context when working with `iframe` elements using Selenium. An `iframe` is essentially an HTML document nested within another HTML document, and Selenium interacts with web elements in a hierarchy. When dealing with elements inside an `iframe`, you must switch the Selenium WebDriver’s focus to the appropriate frame, perform the action, and then switch back to the main document once done.

Here are the main steps to keep in mind when dealing with `iframe`s:

### 1. **Switching to an `iframe`**
   Before you can interact with any elements inside an `iframe`, you need to switch the WebDriver's context to the `iframe`:

   ```java
   driver.switchTo().frame(editorIframeId);
   ```

   This ensures that Selenium now looks for elements inside the `iframe` rather than in the parent document.

### 2. **Interacting with Elements inside the `iframe`**
   Once inside the frame, you can perform actions like clearing text or sending text:

   ```java
   driver.findElement(textArea).clear();
   driver.findElement(textArea).sendKeys(text);
   ```

### 3. **Switching Back to the Main Document**
   After performing actions inside the `iframe`, it’s a good practice to switch back to the parent frame to ensure that future actions are performed at the main page level:

   ```java
   driver.switchTo().parentFrame();
   ```

### 4. **Example Code Structure**

- **Switch to `iframe`:**
  
  ```java
  private void switchToEditArea() {
      driver.switchTo().frame(editorIframeId);
  }
  ```

- **Clear Text Area:**
  
  ```java
  public void clearTextArea() {
      switchToEditArea();
      driver.findElement(textArea).clear();
      switchToMainArea();
  }
  ```

- **Set Text:**

  ```java
  public void setTextArea(String text) {
      switchToEditArea();
      driver.findElement(textArea).sendKeys(text);
      switchToMainArea();
  }
  ```

- **Get Text from Editor:**

  ```java
  public String getTextFromEditor() {
      switchToEditArea();
      String text = driver.findElement(textArea).getText();
      switchToMainArea();
      return text;
  }
  ```

- **Test Scenario:**
  
  The test navigates to the WYSIWYG Editor page, clears the text area, types in two separate words ("hello " and "world"), adjusts indentation, and then verifies the final content:

  ```java
  @Test
  public void testWysiwyg() {
      var editorPage = homePage.clickWysiwygEditor();
      editorPage.clearTextArea();
  
      String text1 = "hello ";
      String text2 = "world";
  
      editorPage.setTextArea(text1);
      editorPage.decreaseIndention();
      editorPage.setTextArea(text2);
  
      assertEquals(editorPage.getTextFromEditor(), text1 + text2, "Text from editor is incorrect");
  }
  ```

### 5. **Good Practice**
   Always ensure to switch back to the main document after working with `iframe`s to avoid running into issues where Selenium remains stuck in the `iframe` context. This helps in making the test flow smoothly without unexpected errors.

### 6. **Error Scenario**
   If you forget to switch back to the main area after working in the `iframe`, Selenium might try to interact with elements that are outside the `iframe`, causing errors because it's still focused on the `iframe`.

## chapter 9

Here’s a more detailed and expanded version of the text you provided:

---

When building a website, there are times when elements take longer to load, or they may load dynamically based on user interaction. This means that the content of the page can change depending on what actions the user performs.

For example, you may click a button that triggers some background processing, and the user interface (UI) might display a spinner or loading indicator to inform the user that the action is being processed.

However, your automation script won't inherently know to wait for this loading process unless you explicitly tell it to. Without instructions, it might attempt to interact with elements that haven't fully loaded yet, leading to errors.

Thankfully, there are different strategies you can use to handle this scenario and make sure your script waits for elements to load before proceeding.

### Implicit Waits
Let's begin by discussing **implicit waits**.

Implicit waits are set once for the entire duration of the script. This means you can configure the script to wait for a specified amount of time every time it needs to interact with an element on the page.

For example, after initializing the `ChromeDriver`, you can call a method like `driver.manage().timeouts()`, which provides access to a **Timeouts** object. This object contains various methods to control waiting times, one of which is `implicitlyWait`.

The `implicitlyWait` method takes two parameters: 
1. The amount of time to wait (e.g., 30 seconds)
2. The time unit (e.g., seconds, milliseconds)

Here’s an example of how this looks in code:

```java
driver.manage().timeouts().implicitlyWait(30, TimeUnit.SECONDS);
```

This line tells **WebDriver** to poll the webpage for up to 30 seconds every time it tries to find an element. If the element is found before 30 seconds, the script will continue. Otherwise, it will keep checking for the element until the 30 seconds expire. If the element isn't found within the set time, WebDriver will throw a `NoSuchElementException`.

You can adjust the wait time to whatever fits your needs, but be cautious. Since implicit waits apply globally to every element interaction in the script, a high wait time could slow down the entire project, as every operation will wait for the specified time.

### Explicit Waits
Another, more controlled approach is using **explicit waits**.

Unlike implicit waits, explicit waits are used only when necessary, at specific points in your script. If you know certain elements or actions take time to load, you can apply an explicit wait at those moments, giving your script the flexibility to handle those particular delays without affecting the entire project.

Let’s now explore how to implement an explicit wait.

First, let's disable the implicit wait we had previously set to ensure it doesn’t interfere with our explicit waits:

```java
// driver.manage().timeouts().implicitlyWait(30, TimeUnit.SECONDS);
```

Next, let’s say our test script is working with an application that has a dynamic loading feature. When clicking a “Start” button, a loading icon appears, and after the process finishes, a message saying "Hello World!" is displayed.

Here’s a snippet of how the **DynamicLoadingPage** class might be structured to handle this scenario:

```java
public class DynamicLoadingPage {
    private WebDriver driver;

    public DynamicLoadingPage(WebDriver driver) {
        this.driver = driver;
    }

    public void clickStart() {
        driver.findElement(By.cssSelector("#start button")).click();
    }
}
```

When we click the "Start" button, we want to wait for the loading indicator to disappear before continuing with the test. We use an **explicit wait** for this.

In WebDriver, explicit waits are handled using the **WebDriverWait** class. This class waits for a specific condition to be met before continuing. The **ExpectedConditions** class offers a variety of conditions that can be used, such as waiting for an element to be clickable, visible, or no longer present.

Here’s how to use it:

```java
WebDriverWait wait = new WebDriverWait(driver, 5);
wait.until(ExpectedConditions.invisibilityOf(driver.findElement(By.id("loading"))));
```

In this example, the script clicks the "Start" button and then waits up to 5 seconds for the loading indicator to disappear. If the loading indicator becomes invisible before 5 seconds, the script will proceed immediately. If not, after 5 seconds, an exception will be thrown, signaling that the wait time has been exceeded.

This method is highly efficient since it waits only as long as necessary, rather than pausing for the maximum time every time.

### Fluent Waits
Finally, let’s discuss **Fluent Waits**, which provide even more control and flexibility than explicit waits.

With fluent waits, you can:
- Specify the total wait time.
- Define how frequently WebDriver should check for the condition.
- Choose which exceptions to ignore while waiting.

Here’s an example:

```java
FluentWait<WebDriver> wait = new FluentWait<>(driver)
    .withTimeout(Duration.ofSeconds(5))   // Maximum wait time of 5 seconds
    .pollingEvery(Duration.ofSeconds(1))  // Poll every 1 second
    .ignoring(NoSuchElementException.class);  // Ignore NoSuchElementException during polling
```

In this case, WebDriver will check every second for up to 5 seconds to see if the condition is met, and it will ignore `NoSuchElementException` during this process.

Fluent waits are particularly useful when dealing with unpredictable loading times or elements that might not always be present immediately. By customizing both the timeout and polling intervals, you can fine-tune your script to be both efficient and robust.

### Summary:

| Feature                | Fluent Wait                                                  | Explicit Wait                                      |
| ---------------------- | ------------------------------------------------------------ | -------------------------------------------------- |
| **Polling Interval**   | Customizable (e.g., every 1 second)                          | Fixed at 500ms (default)                           |
| **Timeout**            | Customizable                                                 | Customizable                                       |
| **Exception Handling** | Can ignore specified exceptions (e.g., `NoSuchElementException`) | Less flexible, no built-in exception customization |
| **Use Case**           | Complex, dynamic situations requiring custom waits           | Standard waits for visibility, clickability, etc.  |
| **Configuration**      | More advanced (withTimeout, polling, ignore exceptions)      | Simpler, easier to set up                          |

By using implicit, explicit, and fluent waits correctly, you can significantly improve the reliability and performance of your test scripts when dealing with dynamic or delayed content loading.



## chapter 10

### **Overview**
WebDriver is a powerful tool for web automation, but it doesn't have built-in methods for certain actions, such as scrolling a page. In cases like this, WebDriver allows you to execute JavaScript directly in the browser using the `JavascriptExecutor` class. A common scenario is scrolling the page to bring an element into view. In this example, we'll build a Selenium test that scrolls the page until a specific table is visible using JavaScript.

---

### **Step-by-Step Guide**

#### 1. **Navigate to the Page and Click the Link**
The first part of this automation involves clicking on a specific link on the homepage ("Large & Deep DOM") to load a page with a large, scrollable DOM structure.

**Method in HomePage Class:**
```java
public LargeAndDeepDomPage clickLargeAndDeepDom(){
    clickLink("Large & Deep DOM");  // Clicks the link on the homepage
    return new LargeAndDeepDomPage(driver);  // Returns an instance of the new page
}
```
- **What’s happening**: The `clickLink()` method clicks the link by its text ("Large & Deep DOM"), and the method returns a new instance of `LargeAndDeepDomPage`, where the scrolling action will occur.

#### 2. **Setting up the LargeAndDeepDomPage**
This class represents the "Large & Deep DOM" page and contains the logic for scrolling the page. The constructor takes the `WebDriver` instance and locates the table element by its ID (`large-table`).

**Class Definition:**
```java
package pages;

import org.openqa.selenium.By;
import org.openqa.selenium.WebDriver;

public class LargeAndDeepDomPage {

    private WebDriver driver;
    private By table = By.id("large-table");  // Locate the table by its ID

    public LargeAndDeepDomPage(WebDriver driver){
        this.driver = driver;
    }
}
```
- **What’s happening**: The `table` element is identified using the `By.id` locator, and the class holds a reference to the `WebDriver` instance for further actions.

#### 3. **Scrolling to the Table Element using JavaScript**
Since WebDriver doesn’t have built-in scrolling capabilities, we use JavaScript to scroll the page. Specifically, we want to scroll until the table is in view.

**Method to Scroll:**
```java
public void scrollToTable(){
    WebElement tableElement = driver.findElement(table);  // Find the table element
    String script = "arguments[0].scrollIntoView();";     // JavaScript code to scroll the element into view
    ((JavascriptExecutor)driver).executeScript(script, tableElement);  // Execute the JavaScript
}
```

- **Step 1**: Find the `tableElement` using the `driver.findElement()` method.
- **Step 2**: Define a JavaScript string `arguments[0].scrollIntoView();`, which calls the `scrollIntoView()` method in JavaScript.
- **Step 3**: Cast the `driver` to `JavascriptExecutor` so that we can use the `executeScript()` method. This method takes two arguments: the JavaScript code and the table element (passed as `arguments[0]`).

#### 4. **Writing the Test Case**
Now that we have the scroll logic, we need to write a test case that triggers this action.

**Test Case in `JavaScriptTests` Class:**
```java
package javascript;

import base.BaseTests;
import org.testng.annotations.Test;

public class JavaScriptTests extends BaseTests {

    @Test
    public void testScrollToTable(){
        homePage.clickLargeAndDeepDom()  // Navigate to the Large & Deep DOM page
                .scrollToTable();        // Scroll to the table
    }
}
```

- **What’s happening**: The `testScrollToTable()` method first calls `clickLargeAndDeepDom()` to navigate to the desired page, then calls `scrollToTable()` to scroll the page until the table is in view.

---

### **Detailed Explanation of Key Concepts**

#### **1. WebDriver’s Limitation and JavaScript Execution**
- **WebDriver Limitation**: While WebDriver provides many built-in methods (e.g., clicking, entering text), it lacks functionality to scroll to elements.
- **Solution**: By using JavaScript’s `scrollIntoView()` method, we can scroll the page to any element.
- **JavascriptExecutor**: Selenium provides the `JavascriptExecutor` interface to execute JavaScript code. The `executeScript()` method can run synchronous JavaScript, while `executeAsyncScript()` runs it asynchronously.

#### **2. Why Casting to `JavascriptExecutor`?**
the `JavascriptExecutor` is an interface, and you can't call its methods directly like `JavascriptExecutor.executeScript()` because interfaces in Java are just contracts, not actual objects. You need to cast the `WebDriver` instance to `JavascriptExecutor` to access its methods. 

To execute JavaScript within Selenium, the WebDriver instance must be cast to the `JavascriptExecutor` interface:

```java
((JavascriptExecutor)driver).executeScript(...);
```
This casting allows access to the `executeScript()` method, which can run JavaScript code directly in the browser context.

#### **3. scrollIntoView() in JavaScript**
- **scrollIntoView()** is a JavaScript method that scrolls an element into the visible area of the browser window.
- **arguments[0]** is a placeholder for any DOM element passed into the `executeScript()` function. In our case, the `tableElement` is passed as `arguments[0]`.

---

### **Code Organization**

1. **HomePage.java**
   - Contains a method to click the "Large & Deep DOM" link and navigate to the next page.
   
2. **LargeAndDeepDomPage.java**
   - Locates the table element by ID and provides the method to scroll to the table using JavaScript.

3. **JavaScriptTests.java**
   - A test case that clicks the link, loads the page, and scrolls to the table element.

---

### **Execution Flow**
1. **Click the link**: The `HomePage` class clicks on "Large & Deep DOM".
2. **Scroll to the table**: The `LargeAndDeepDomPage` locates the table and scrolls to it using JavaScript.
3. **Run the test**: The `JavaScriptTests` class triggers this entire process.

### **Summary**
- We used Selenium’s `JavascriptExecutor` to execute JavaScript and scroll to a table element.
- The test case is simple and modular, with separate classes for page interactions and test execution.
- This is a common way to extend WebDriver functionality using JavaScript for browser automation.

### Handling Elements That Aren’t in the DOM Yet

In some cases, a web element may not be present in the DOM when you first load a page. For example, it may only appear when the user scrolls, as in the case of pages with infinite scrolling. Here's how you can handle such scenarios using JavaScript and Selenium's `JavascriptExecutor`:

---

### Scenario

The test application has an **Infinite Scroll** link, which dynamically adds new paragraphs to the page as you scroll down. The paragraphs are not part of the DOM until the user scrolls to them. This makes it impossible to directly locate them using Selenium because they don’t exist when the test starts. We want to scroll until a specific paragraph (e.g., the 5th paragraph) is loaded.

### Problem

Since the paragraphs don't exist initially, trying to locate a specific paragraph using Selenium's WebElement will result in an exception. We need a way to scroll until that paragraph becomes visible.

---

### Steps to Solve

1. **Click the Infinite Scroll Link**: 
   - First, we need to click on the **Infinite Scroll** link to load the dynamic page.
   - The `clickInfiniteScroll()` method in the `HomePage` class navigates to the **Infinite Scroll** page:
   
   ```java
   public InfiniteScrollPage clickInfiniteScroll(){
       clickLink("Infinite Scroll");
       return new InfiniteScrollPage(driver);
   }
   ```

2. **Define a Locator for Paragraphs**:
   - The dynamically added paragraphs have the class `jscroll-added`. We’ll create a `By` locator for it in the `InfiniteScrollPage` class:
   
   ```java
   private By textBlocks = By.className("jscroll-added");
   ```

3. **Scroll Down Using JavaScript**:
   - To scroll the page, we can use the JavaScript method `window.scrollTo(x, y)`. The parameters `x` and `y` define the scroll position. Since we only want to scroll vertically, `x` is set to `0` and `y` uses `document.body.scrollHeight` to scroll down by the height of the page.
   
   ```java
   String script = "window.scrollTo(0, document.body.scrollHeight)";
   ```

4. **Keep Scrolling Until the Desired Paragraph is Loaded**:
   - We don’t want to scroll just once. We need to keep scrolling until the paragraph we want is present in the DOM. For this, we'll use a loop that continuously checks how many paragraphs are currently in the DOM. If the desired paragraph isn’t loaded yet, we keep scrolling.

   ```java
   public void scrollToParagraph(int index){
       String script = "window.scrollTo(0, document.body.scrollHeight)";
       var jsExecutor = (JavascriptExecutor) driver;
   
       while (getNumberOfParagraphsPresent() < index) {
           jsExecutor.executeScript(script);
       }
   }
   ```

   - **Get the Number of Paragraphs Present**: This helper method counts the number of paragraphs currently in the DOM:
   
   ```java
   private int getNumberOfParagraphsPresent() {
       return driver.findElements(textBlocks).size();
   }
   ```

5. **Test the Scroll Functionality**:
   - Finally, we write a test that scrolls until the fifth paragraph is in view:

   ```java
   @Test
   public void testScrollToFifthParagraph(){
       homePage.clickInfiniteScroll().scrollToParagraph(5);
   }
   ```

---

### Full Code Implementation

#### `InfiniteScrollPage.java`

```java
package pages;

import org.openqa.selenium.By;
import org.openqa.selenium.JavascriptExecutor;
import org.openqa.selenium.WebDriver;

public class InfiniteScrollPage {

    private WebDriver driver;
    private By textBlocks = By.className("jscroll-added");

    public InfiniteScrollPage(WebDriver driver){
        this.driver = driver;
    }

    /**
    * Scrolls until paragraph with index specified is in view
    * @param index 1-based
    */
    public void scrollToParagraph(int index){
        String script = "window.scrollTo(0, document.body.scrollHeight)";
        var jsExecutor = (JavascriptExecutor) driver;

        while (getNumberOfParagraphsPresent() < index) {
            jsExecutor.executeScript(script);
        }
    }

    /**
    * Returns the number of paragraphs currently present in the DOM
    */
    private int getNumberOfParagraphsPresent() {
        return driver.findElements(textBlocks).size();
    }
}
```

#### `JavaScriptTests.java`

```java
package javascript;

import base.BaseTests;
import org.testng.annotations.Test;

public class JavaScriptTests extends BaseTests {

    @Test
    public void testScrollToFifthParagraph(){
        homePage.clickInfiniteScroll().scrollToParagraph(5);
    }
}
```

---

### Key Points

- **`JavascriptExecutor`**: Allows us to execute JavaScript code from Selenium. This is useful when we need to interact with elements that are not accessible using regular WebDriver methods.
- **Scrolling Dynamically Loaded Pages**: For pages where elements are loaded dynamically (e.g., infinite scroll), you can’t directly interact with elements that aren’t yet present in the DOM. Instead, you can simulate scrolling using JavaScript and dynamically check for the existence of the desired elements.
- **Looping Until Element is Present**: In cases where you need to wait for an element to load into the DOM (such as infinite scrolling), you can repeatedly scroll and check until the element appears.

## chapter 11

In this course, we have primarily used provided links to navigate through the application. However, WebDriver offers additional navigation methods that allow more flexibility.

### Navigation Interface in WebDriver
WebDriver provides a **Navigation** interface that includes several useful methods:

- **back**: Navigates to the previous page in the browser's history.
- **forward**: Moves forward in the browser's history by one page.
- **refresh**: Reloads the current page.
- **to**: Navigates to a specific URL. It can accept either a `String` or a `URL`. The difference between the `to` method and the `get` method is that `driver.get()` waits for the page to load, while `driver.navigate().to()` does not.

### Creating a Utility Class for Navigation
We’ll create a class to utilize these navigation methods and place it in the framework. Since it is browser interaction, it belongs in a utilities package instead of the "pages" package, which is reserved for page objects.

#### Step 1: Creating the `WindowManager` Class
We'll create a new class named `WindowManager` that will manage browser navigation methods.

```java
package utils;

import org.openqa.selenium.WebDriver;

public class WindowManager {

    private WebDriver driver;
    private WebDriver.Navigation navigate;

    public WindowManager(WebDriver driver){
        this.driver = driver;
        this.navigate = driver.navigate();
    }

    public void goBack() {
        navigate.back();
    }

    public void goForward() {
        navigate.forward();
    }

    public void refreshPage() {
        navigate.refresh();
    }

    public void goTo(String url) {
        navigate.to(url);
    }
}
```

- **goBack()**: Navigates to the previous page.
- **goForward()**: Moves forward one page.
- **refreshPage()**: Refreshes the current page.
- **goTo()**: Navigates to a given URL.

### Writing Tests for the Navigation Methods
We'll now create tests that exercise these navigation methods.

#### Step 2: Setting Up the Test Class
We create a new test class `NavigationTests` under a `navigation` package.

```java
package navigation;

import base.BaseTests;
import org.testng.annotations.Test;

public class NavigationTests extends BaseTests {

    @Test
    public void testNavigator() {
        homePage.clickDynamicLoading().clickExample1();
        getWindowManager().goBack();
        getWindowManager().refreshPage();
        getWindowManager().goForward();
        getWindowManager().goTo("https://google.com");
    }
}
```

In this test:
1. We navigate through some pages using existing methods in `homePage`.
2. We then use the `WindowManager` methods to navigate back, refresh, move forward, and finally navigate to Google.

#### Step 3: Updating BaseTests
To access the `WindowManager` in the test, we need to add a method in `BaseTests` to return a `WindowManager` object.

```java
public WindowManager getWindowManager() {
    return new WindowManager(driver);
}
```

### Handling Multiple Tabs
Next, we’ll add functionality to switch between multiple browser tabs. When we click a link that opens a new tab, WebDriver provides a way to handle this using `getWindowHandles()`, which returns handles to all open windows or tabs.

#### Step 4: Extending WindowManager to Switch Tabs
We add a method in `WindowManager` to switch between tabs based on the tab's title.

```java
public void switchToTab(String tabTitle) {
    var windows = driver.getWindowHandles();
    System.out.println("Number of tabs: " + windows.size());

    for (String window : windows) {
        driver.switchTo().window(window);
        if (tabTitle.equals(driver.getTitle())) {
            break;
        }
    }
}
```

This method:
1. Retrieves all open window handles.
2. Iterates through the windows and checks their title.
3. Switches to the window if its title matches the specified `tabTitle`.

#### Step 5: Testing Tab Switching
We can now add a test to validate switching between tabs.

```java
@Test
public void testSwitchTab() {
    homePage.clickMultipleWindows().clickHere();
    getWindowManager().switchToTab("New Window");
}
```

This test:
1. Opens a new tab by clicking a link on the page.
2. Switches to the new tab titled "New Window".

### Summary
By using the `WindowManager` class, we can efficiently manage navigation actions and tab switching in our WebDriver tests. These utility methods enhance browser interaction by offering simpler and more organized code for common navigation tasks.

# chapter 12

In this scenario, you are learning how to take screenshots in Selenium WebDriver for your test automation framework and how to capture them specifically for failed tests. Here’s a breakdown of the process:

1. **Set up Screenshot Functionality:**
   You first set up a method to take screenshots after each test, using the `@AfterMethod` annotation in TestNG. This method will initially capture a screenshot regardless of whether the test passes or fails.The screenshot is taken using the `TakesScreenshot` interface, which is cast from the `driver` object. It stores the screenshot in a file and prints its location.

   ```java
   @AfterMethod
   public void takeScreenshot() {
       var camera = (TakesScreenshot) driver;
       File screenshot = camera.getScreenshotAs(OutputType.FILE);
       System.out.println("Screenshot taken: " + screenshot.getAbsolutePath());
   }
   ```

   

2. **Move Screenshot to a Specific Location:**
   Next, you move the screenshot to a folder in your project, such as `resources/screenshots/`. To achieve this, you use the `Files.move()` method from the `com.google.common.io` package. 

   You wrap this code in a `try-catch` block to handle any `IOException` that might occur while moving the file.

   ```java
   try {
       Files.move(screenshot, new File("resources/screenshots/test.png"));
   } catch (IOException e) {
       e.printStackTrace();
   }
   ```

3. **Take Screenshot Only on Failures:**
   To enhance your code and take screenshots only when tests fail, you use the `ITestResult` interface, which captures the test result. You modify the method to check if the test status is `FAILURE`. The method is renamed to `recordFailure` to reflect its purpose clearly.

   ```java
   @AfterMethod
   public void recordFailure(ITestResult result) {
       if (ITestResult.FAILURE == result.getStatus()) {
           var camera = (TakesScreenshot) driver;
           File screenshot = camera.getScreenshotAs(OutputType.FILE);
           try {
               Files.move(screenshot, new File("resources/screenshots/test.png"));
           } catch (IOException e) {
               e.printStackTrace();
           }
       }
   }
   ```

4. **Save Screenshot with Dynamic Test Name:**
   Instead of saving every screenshot as `test.png`, you make the file name dynamic by appending the test name to the screenshot file. The method `result.getName()` gets the name of the test that failed, ensuring each failure generates a uniquely named screenshot.

   ```java
   Files.move(screenshot, new File("resources/screenshots/" + result.getName() + ".png"));
   ```

5. **Testing the Implementation:**
   After implementing the screenshot functionality, you test it by running both passing and failing tests. When the test passes, no screenshot is taken, but when the test fails, a screenshot is saved with the appropriate file name, such as `testBackspace.png`.

   ```java
   @AfterMethod
   public void recordFailure(ITestResult result) {
       if (ITestResult.FAILURE == result.getStatus()) {
           var camera = (TakesScreenshot) driver;
           File screenshot = camera.getScreenshotAs(OutputType.FILE);
           try {
               Files.move(screenshot, new File("resources/screenshots/" + result.getName() + ".png"));
           } catch (IOException e) {
               e.printStackTrace();
           }
       }
   }
   ```

   Let’s go step by step and explain each line of this code snippet:

   ### 1. `@AfterMethod`
   This is an **annotation** provided by the TestNG testing framework. It tells TestNG that the method it annotates should run **after each test method** in the test class. For example, if you have a test method that checks if a button works and another that checks if a link opens correctly, the `@AfterMethod` annotated method will run after each one, no matter if the test passes or fails.

   - **Why?** In this case, it's used to trigger the screenshot capture or other actions after a test completes.

   ### 2. `public void recordFailure(ITestResult result) {`
   This is the method declaration. It defines a method named `recordFailure`, which is set to run after each test method. The method accepts one parameter:

   - `ITestResult result`: This is an object that holds information about the result of the test method that just ran (whether it passed, failed, skipped, etc.). TestNG provides this class, and it allows us to check whether the test failed.

   ### 3. `if (ITestResult.FAILURE == result.getStatus()) {`
   This line checks whether the test that just ran **failed**.

   - `ITestResult.FAILURE`: This is a constant provided by TestNG. It represents the status of a failed test.
   - `result.getStatus()`: This method checks the status of the completed test (whether it passed, failed, or was skipped). The status will be compared against `ITestResult.FAILURE`.

   - **Why?** This `if` condition ensures that the code inside the block runs **only if the test failed**.

   ### 4. `var camera = (TakesScreenshot) driver;`
   This line creates a new variable `camera` and assigns it the ability to take a screenshot. 

   - `TakesScreenshot`: This is an interface in Selenium WebDriver that provides a method to take screenshots.
   - `(TakesScreenshot) driver`: This casts the `driver` object to the `TakesScreenshot` interface. The `driver` is usually a WebDriver object that controls the browser (like ChromeDriver or FirefoxDriver), but by casting it, you are telling Java that this `driver` should now have screenshot-taking abilities.

   - **Why?** This allows you to use the `TakesScreenshot` interface to capture screenshots.

   ### 5. `File screenshot = camera.getScreenshotAs(OutputType.FILE);`
   This line takes the screenshot and stores it as a **File**.

   - `camera.getScreenshotAs(OutputType.FILE)`: This method captures the screenshot and returns it as a file. 
   - `OutputType.FILE`: This specifies that the output should be in the form of a file (the screenshot image).

   - **Why?** It’s necessary to save the screenshot as a file object in order to manipulate it later, like moving it to a specific location.

   ### 6. `try {`
   The `try` block starts here. It is used to catch and handle exceptions that might occur during the execution of the code inside it. This is necessary because moving files can fail (e.g., if the directory doesn't exist or if there are permission issues), which would throw an `IOException`.

   ### 7. `Files.move(screenshot.toPath(), new File("resources/screenshots/" + result.getName() + ".png").toPath());`
   This line moves the screenshot to a specific folder and gives it a specific name.

   - `Files.move()`: This method moves a file from one location to another.
   - `screenshot.toPath()`: Converts the `screenshot` file into a `Path` object (which is required by the `Files.move()` method).
   - `new File("resources/screenshots/" + result.getName() + ".png").toPath()`: 
       - Creates a new `File` object representing the destination path for the screenshot.
       - `"resources/screenshots/" + result.getName() + ".png"`: 
           - `resources/screenshots/`: This is the directory where the screenshot will be saved.
           - `result.getName()`: This gets the name of the test method that failed (e.g., `testLogin` or `testSignUp`), and it’s used to name the screenshot file.
           - `".png"`: This is the file extension to save the screenshot as a PNG image.

   - **Why?** This moves the screenshot to a specific folder and names it after the test method that failed, making it easy to identify which screenshot corresponds to which test.

   ### 8. `} catch (IOException e) {`
   This line starts the `catch` block, which handles exceptions that might be thrown in the `try` block.

   - `IOException`: This is a type of exception that occurs when there is an error related to input/output operations (like file handling). If something goes wrong while moving the file, this exception will be thrown.
   - `e`: This is the variable that will hold the exception details.

   ### 9. `e.printStackTrace();`
   This line prints the details of the exception if one is thrown. The `printStackTrace()` method prints the stack trace of the exception (i.e., the sequence of method calls that led to the exception), which can be useful for debugging.

   - **Why?** This helps in understanding what went wrong in case the screenshot couldn't be saved.

   ---

   ### **Summary:**
   - The `@AfterMethod` method runs after each test method finishes.
   - The `ITestResult` argument in the `recordFailure` method is passed automatically by the TestNG framework when the method is invoked after a test method execution. 
   - It checks if the test failed using `ITestResult.FAILURE`.
   - If the test failed, it casts the WebDriver `driver` to `TakesScreenshot` and captures a screenshot.
   - The screenshot is saved in a specific folder with a name based on the failed test.
   - The code inside the `try` block is protected with a `catch` block to handle any errors while moving the screenshot file.

6. **Outcome:**
   After running the tests, if a test fails, you will find a screenshot saved in the `resources/screenshots/` directory. The screenshot name corresponds to the failed test, making it easier to debug by visually inspecting the browser state when the test failed.

---

This approach ensures that you capture screenshots only for failing tests, providing valuable insights during test execution without cluttering your project with unnecessary images for passing tests. The implementation simplifies debugging, especially for complex test cases.

# chapter 13

This example demonstrates how to use Selenium's `WebDriverEventListener` interface to listen to events during test execution and perform additional actions (e.g., logging or reporting). The steps illustrate how to create an event listener that listens to certain actions on the UI (like clicks) and then logs those actions. Here’s an explanation of the code flow:

### 1. **Introduction to WebDriverEventListener**

- **WebDriverEventListener**: This interface allows you to "listen" for specific events in Selenium, such as clicks, navigation, alert handling, etc. You can add custom functionality (like logging, reporting, or taking screenshots) when those events occur.

### 2. **Setup in BaseTests Class**

In your `BaseTests` class, you modify the WebDriver setup to use an event-firing WebDriver that can listen for and respond to events:

```java
private EventFiringWebDriver driver;
```

- **EventFiringWebDriver**: A special WebDriver that listens for events. It's a wrapper around an existing WebDriver (like `ChromeDriver`) that intercepts events such as clicks, navigations, etc.

### 3. **Changing WebDriver Instance to EventFiringWebDriver**

When setting up the WebDriver, instead of directly initializing `ChromeDriver`, you wrap it inside an `EventFiringWebDriver`:

```java
driver = new EventFiringWebDriver(new ChromeDriver());
```

This step makes sure that the WebDriver can "fire" events.

### 4. **Registering the Event Listener**

Next, you need to register the event listener class, which implements the `WebDriverEventListener` interface:

```java
driver.register(new EventReporter());
```

- **driver.register()**: This method is used to register the listener (in this case, the `EventReporter` class) with the driver. It ensures that whenever an event occurs (like clicking a button), the relevant method in the listener is invoked.

### 5. **Creating the Event Listener Class (EventReporter)**

You then create a class (`EventReporter`) to handle the events. This class implements the `WebDriverEventListener` interface, meaning it can override methods to listen to events:

```java
public class EventReporter implements WebDriverEventListener {
    // Implement required methods
}
```

- When you implement the `WebDriverEventListener` interface, you are required to provide implementations for all the methods related to different WebDriver actions (like clicking, navigating, alert handling, etc.).

### 6. **Implementing the Listener Methods**

You decide to implement just the `beforeClickOn()` method to demonstrate how it works. This method is called right before an element is clicked:

```java
@Override
public void beforeClickOn(WebElement webElement, WebDriver webDriver) {
    System.out.println("Clicking on " + webElement.getText());
}
```

- **beforeClickOn()**: This method gets triggered just before a WebElement is clicked. Here, it simply prints out the text of the element that’s about to be clicked.
- **webElement.getText()**: This returns the text of the WebElement being clicked. The print statement will output this text to the console when the click happens.

### 7. **Running a Test with Event Listener**

Once the event listener is registered and the code is set up, you can run any test that involves clicking actions. For example, when running a login test that involves clicking buttons or links, you’ll see the logs:

```bash
Clicking on Login
Clicking on Submit
```

This happens because the `beforeClickOn()` method is triggered before each click event, and it logs the action in the console.

### Summary of Code Flow:

1. **EventFiringWebDriver** is set up to wrap around the `ChromeDriver`, enabling event listening.
2. You register an event listener class (`EventReporter`) that implements `WebDriverEventListener` and listens to events (e.g., clicks).
3. The `beforeClickOn()` method is implemented to log a message before every click action.
4. When a test runs, Selenium triggers the registered methods of `WebDriverEventListener` before and after actions, printing the appropriate messages for clicks.

This approach provides a mechanism for adding extra functionality (like reporting or logging) to your tests in a clean, reusable way.

# chapter 14

### ChromeOptions

First, let's discuss `ChromeOptions`. When Selenium WebDriver launches a browser, it doesn't behave exactly like your everyday browser instance. It’s a fresh instance with no logged-in sessions or browser extensions you normally use. For instance, you’ll only see an "Automation extension," and the banner saying "Chrome is being controlled by automated software."

Let's say you want to customize the browser instance WebDriver launches. This is where the `ChromeOptions` class comes into play.

### Implementing ChromeOptions

In our `BaseTests` class, we can create a method to configure Chrome's options:

```java
private ChromeOptions getChromeOptions() {
    ChromeOptions options = new ChromeOptions();
    return options;
}
```

This method is `private` because we only need it within this class. The `ChromeOptions` object provides several methods to customize the browser behavior.

Some useful methods are:

- **addArguments()**: Add custom arguments to modify browser behavior.
- **addExtensions()**: Load specific Chrome extensions.
- **setBinary()**: Specify the path to a different Chrome executable.

Let’s add an argument to disable the info bar displayed in automated browser sessions.

```java
private ChromeOptions getChromeOptions() {
    ChromeOptions options = new ChromeOptions();
    options.addArguments("disable-infobars");
    return options;
}
```

Now, when we instantiate our `ChromeDriver`, we pass this `ChromeOptions` configuration:

```java
driver = new EventFiringWebDriver(new ChromeDriver(getChromeOptions()));
// Alternatively:
// driver = new ChromeDriver(getChromeOptions());
```

Running this will launch a browser without the annoying info bar.

### Running in Headless Mode

We can also run the browser in headless mode, meaning no graphical interface will be displayed. This can speed up test execution.

```java
options.setHeadless(true);
```

Running the test in headless mode will execute the test without showing the browser window.

### Practical Use of ChromeOptions

`ChromeOptions` is particularly useful when running tests on machines other than your own (e.g., in Selenium Grid or cloud environments).

---

## Managing Cookies with WebDriver

Now, let's move on to managing cookies. In modern browsers, cookies store data about user interactions and state. With WebDriver, you can interact with cookies, for example, to save or verify certain website behaviors.

### Adding Cookies in WebDriver

We’ll create a method to add a cookie:

```java
private void setCookie() {
    Cookie cookie = new Cookie.Builder("tau", "123")
            .domain("the-internet.herokuapp.com")
            .build();
    driver.manage().addCookie(cookie);
}
```

The `Cookie.Builder` allows us to define the name (`"tau"`) and value (`"123"`) for our cookie. We also specify the domain for the cookie (`"the-internet.herokuapp.com"`). Finally, we add the cookie to the browser session using `driver.manage().addCookie(cookie)`.

### Using the Cookie Method

We’ll call `setCookie()` after navigating to the homepage in our `@BeforeClass` setup:

```java
@BeforeClass
public void setUp() {
    System.setProperty("webdriver.chrome.driver", "resources/chromedriver");
    driver = new EventFiringWebDriver(new ChromeDriver(getChromeOptions()));
    driver.register(new EventReporter());

    goHome();
    setCookie();
}
```

After running this, you can inspect the browser's cookies in the “Application” tab of the Developer Tools under the "Storage" section. After refreshing, you’ll see the new cookie `"tau"` with a value of `"123"` added to the website.

### Managing Cookies

WebDriver provides several methods to manage cookies:

- `addCookie()`: Adds a cookie.
- `deleteAllCookies()`: Deletes all cookies.
- `deleteCookie()`: Deletes a specific cookie.
- `getCookies()`: Retrieves all cookies.
- `getCookieNamed()`: Retrieves a specific cookie by name.

---

## Congratulations!

You've made it to the end of this course. Throughout the chapters, you've learned the ins and outs of Selenium WebDriver. From browser automation to managing cookies and customizing browser behavior, you now have the tools to confidently automate web testing.

Keep practicing, and good luck with your automation journey!
