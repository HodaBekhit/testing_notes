## TestNg Notes

1. Selenium WebDriver is not a test tool, Selenium WebDriver is not a verification tool. It is only used to automate the actions on the browser. So, we need to add a verification/assertion tool to our framework to be able to actually run these as tests.

2. **Per Class Execution**: `@BeforeClass` and `@AfterClass` are executed once per class.

   **Per Method Execution**: `@BeforeMethod` and `@AfterMethod` are executed before and after each test method in the class, respectively.

3.  **inheritance** in TestNG is a practical solution for reusing methods across multiple test classes. By creating a base test class that contains shared setup and teardown methods annotated with `@BeforeClass`, `@AfterClass`, `@BeforeMethod`, and `@AfterMethod`, you can avoid code duplication and maintain cleaner, more manageable test code.

   ### Execution Order

   The execution order of these annotations is as follows when a test suite is run:

   1. `@BeforeSuite`
   2. `@BeforeTest`
   3. `@BeforeClass`
   4. `@BeforeMethod`
   5. (Execute Test Method)
   6. `@AfterMethod`
   7. `@AfterClass`
   8. `@AfterTest`
   9. `@AfterSuite`

   ### Summary of Use Cases

   - **`@BeforeSuite`**: Set up resources or configurations needed for the entire suite.
   - **`@AfterSuite`**: Clean up resources or generate reports after all tests are completed.
   - **`@BeforeTest`**: Prepare the environment specific to tests defined in a `<test>` tag in the `testng.xml`.
   - **`@AfterTest`**: Cleanup actions for tests defined in the same `<test>` tag.

4. Without any `@Before` or `@After` annotations, the execution order of test classes and methods in TestNG is strictly based on the alphabetical order of the class and method names.

5. you can control the execution order of your test methods using the `@Test` annotation's `priority` attribute. By assigning different priority values to your test methods, you can dictate the order in which they will run. TestNG executes methods with lower priority values first.

   #### How to Use the `priority` Attribute

   1. **Priority Value**: Assign an integer value to the `priority` attribute of the `@Test` annotation. The default priority is `0`. Methods with lower values will run before those with higher values.
   2. **Execution Order**: If multiple methods have the same priority, their execution order will be determined by their alphabetical order.

6. In TestNG, you can use the `<include>` and `<exclude>` tags within the `testng.xml` file to specify which test methods or classes should be included or excluded from the execution. This feature is useful when you want to run a subset of tests based on certain criteria.

   #### TestNG XML Configuration

   Here’s how you would write your `testng.xml` to include and exclude specific methods:

   ```
   xmlCopy code<!DOCTYPE suite SYSTEM "http://testng.org/testng-1.0.dtd">
   <suite name="ExampleSuite">
       <test name="ExampleTest">
           <classes>
               <class name="your.package.MyTests">
                   <include name="testMethod1"/> <!-- Include only testMethod1 -->
                   <exclude name="testMethod2"/> <!-- Exclude testMethod2 -->
                   <!-- testMethod3 will be included by default -->
               </class>
           </classes>
       </test>
   </suite>
   ```

7. In TestNG, **groups** allow you to organize and categorize your test methods. You can assign tests to groups and then execute specific groups based on your needs. This is particularly useful when you want to run a subset of tests for a particular scenario (e.g., smoke tests, regression tests, etc.) without modifying your test code.

   ### Defining Groups

   To use groups in TestNG, you can specify them in the `@Test` annotation with the `groups` attribute. Here’s how to define and use groups in your tests:

   #### Example Test Class with Groups

   ```
   javaCopy codeimport org.testng.annotations.Test;
   
   public class ExampleTests {
   
       @Test(groups = {"smoke"})
       public void testMethod1() {
           System.out.println("Executing Test Method 1 - Smoke Test");
       }
   
       @Test(groups = {"regression"})
       public void testMethod2() {
           System.out.println("Executing Test Method 2 - Regression Test");
       }
   
       @Test(groups = {"smoke", "regression"})
       public void testMethod3() {
           System.out.println("Executing Test Method 3 - Smoke and Regression Test");
       }
   
       @Test(groups = {"regression"})
       public void testMethod4() {
           System.out.println("Executing Test Method 4 - Regression Test");
       }
   }
   ```

   ### Configuring Groups in `testng.xml`

   You can specify which groups to include or exclude in your `testng.xml` file. This allows you to run tests that belong to specific groups.

   #### Example `testng.xml` Configuration

   ```
   xmlCopy code<!DOCTYPE suite SYSTEM "http://testng.org/testng-1.0.dtd">
   <suite name="ExampleSuite">
       <test name="SmokeTest">
           <groups>
               <run>
                   <include name="smoke"/> <!-- Include only smoke tests -->
               </run>
           </groups>
           <classes>
               <class name="your.package.ExampleTests"/>
           </classes>
       </test>
   
       <test name="RegressionTest">
           <groups>
               <run>
                   <include name="regression"/> <!-- Include only regression tests -->
               </run>
           </groups>
           <classes>
               <class name="your.package.ExampleTests"/>
           </classes>
       </test>
   </suite>
   ```

   ### Execution

   When you run the above `testng.xml`, the output will be:

   - For the **SmokeTest** test:
     - Executed: `testMethod1`
     - Executed: `testMethod3`
   - For the **RegressionTest** test:
     - Executed: `testMethod2`
     - Executed: `testMethod3`
     - Executed: `testMethod4`

8. In TestNG, **parameters** allow you to pass data to your test methods from an external source, such as an XML file. This feature enables you to run the same test method with different data sets without modifying the test code itself. Parameters are particularly useful for running tests with varying input values or configurations.

   ### Defining Parameters in `testng.xml`

   Parameters can be defined in the `<suite>` or `<test>` tags of your `testng.xml` file. Here’s how to set it up:

   #### Example `testng.xml` Configuration

   ```xml
   <!DOCTYPE suite SYSTEM "http://testng.org/testng-1.0.dtd">
   <suite name="ParameterizedSuite">
       <test name="ParameterizedTest">
           <parameter name="username" value="testuser"/>
           <parameter name="password" value="password123"/>
           <classes>
               <class name="your.package.ParameterizedTests"/>
           </classes>
       </test>
   </suite>
   ```

   ### Accessing Parameters in Test Methods

   You can access these parameters in your test methods using the `@Parameters` annotation. Here’s how you do it:

   #### Example Test Class Using Parameters

   ```java
   import org.testng.annotations.Parameters;
   import org.testng.annotations.Test;
   
   public class ParameterizedTests {
   
       @Parameters({"username", "password"})
       @Test
       public void testLogin(String username, String password) {
           System.out.println("Username: " + username);
           System.out.println("Password: " + password);
           // Add your login test logic here
       }
   }
   ```

   ### Running the Parameterized Test

   When you run the above `testng.xml`, the output will be:

   ```
   Username: testuser
   Password: password123
   ```

   ### Multiple Sets of Parameters

   You can also provide multiple sets of parameters using the `<parameter>` tags inside different `<test>` tags. This allows you to run the same test with different values.

   #### Example with Multiple Parameter Sets

   ```xml
   <!DOCTYPE suite SYSTEM "http://testng.org/testng-1.0.dtd">
   <suite name="ParameterizedSuite">
       <test name="ParameterizedTest1">
           <parameter name="username" value="testuser1"/>
           <parameter name="password" value="password123"/>
           <classes>
               <class name="your.package.ParameterizedTests"/>
           </classes>
       </test>
   
       <test name="ParameterizedTest2">
           <parameter name="username" value="testuser2"/>
           <parameter name="password" value="password456"/>
           <classes>
               <class name="your.package.ParameterizedTests"/>
           </classes>
       </test>
   </suite>
   ```

   ### Accessing Parameters with Default Values

   If a parameter is not provided in `testng.xml`, you can set a default value in your test method using the `@Optional` annotation.

   #### Example with Default Values

   ```java
   import org.testng.annotations.Optional;
   import org.testng.annotations.Parameters;
   import org.testng.annotations.Test;
   
   public class ParameterizedTests {
   
       @Parameters({"username"})
       @Test
       public void testLogin(@Optional("defaultUser") String username) {
           System.out.println("Username: " + username);
           // Add your login test logic here
       }
   }
   ```

   ### Summary

   - **Parameter Definition**: Use the `<parameter>` tag in `testng.xml` to define parameters for your tests.
   - **Accessing Parameters**: Use the `@Parameters` annotation in your test methods to receive parameter values.
   - **Multiple Sets of Parameters**: You can define multiple test sets in `testng.xml` to run the same test method with different parameters.
   - **Default Values**: Use the `@Optional` annotation to provide default values for parameters that may not always be present.

   ### Conclusion

   Using parameters in TestNG enhances your testing capabilities by allowing you to run the same test with different data inputs, making your tests more dynamic and reusable. This feature is particularly beneficial for scenarios like data-driven testing, where you want to validate the same functionality against various input values.

9. In testing frameworks like TestNG and JUnit, assertions are crucial for verifying that the expected results match the actual outcomes during test execution. Assertions can be categorized into two types: **soft assertions** and **hard assertions**.

   ### Hard Assertions

   **Hard assertions** immediately stop the test execution when an assertion fails. If a hard assertion fails, the rest of the test case is aborted, and no further steps are executed. This is useful when the continuation of the test depends on the validity of the previous checks.

   #### Example of Hard Assertions in TestNG

   In TestNG, you typically use methods from the `Assert` class for hard assertions:

   ```java
   import org.testng.Assert;
   import org.testng.annotations.Test;
   
   public class HardAssertionExample {
   
       @Test
       public void testHardAssertion() {
           String actualResult = "Hello, World!";
           String expectedResult = "Hello, World!";
           
           // Hard assertion
           Assert.assertEquals(actualResult, expectedResult, "The messages do not match!");
           
           // This line will not be executed if the assertion above fails
           System.out.println("Hard Assertion Passed!");
       }
   }
   ```

   ### Soft Assertions

   **Soft assertions** allow the test to continue executing even if one or more assertions fail. All assertions are collected, and at the end of the test, you can see the results of all assertions. This is useful for scenarios where you want to verify multiple conditions without halting the test execution immediately upon failure.

   #### Example of Soft Assertions in TestNG

   To use soft assertions in TestNG, you typically use the `SoftAssert` class:

   ```java
   import org.testng.annotations.Test;
   import org.testng.asserts.SoftAssert;
   
   public class SoftAssertionExample {
   
       @Test
       public void testSoftAssertion() {
           SoftAssert softAssert = new SoftAssert();
           
           String actualResult1 = "Hello";
           String expectedResult1 = "Hello";
           
           // Soft assertion
           softAssert.assertEquals(actualResult1, expectedResult1, "The first messages do not match!");
   
           String actualResult2 = "World";
           String expectedResult2 = "Earth";
           
           // Soft assertion
           softAssert.assertEquals(actualResult2, expectedResult2, "The second messages do not match!");
   
           // This line will be executed regardless of the previous assertions
           System.out.println("Soft Assertion Checks Completed!");
   
           // Assert all soft assertions
           softAssert.assertAll(); // This will report all collected failures
       }
   }
   ```

   ### Key Differences

   | Feature                 | Hard Assertions                                              | Soft Assertions                                              |
   | ----------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
   | **Behavior on Failure** | Stops test execution immediately.                            | Continues execution regardless of failure.                   |
   | **Error Reporting**     | Only reports the first failure encountered.                  | Reports all failures at the end of the test.                 |
   | **Usage Scenario**      | Use when subsequent code should not run if a critical check fails. | Use when you want to check multiple conditions in a single test and report all failures. |

   ### Summary

   - **Hard Assertions**: Stop execution immediately upon failure, useful for critical checks.
   - **Soft Assertions**: Continue execution, collecting all assertion results to report at the end, useful for scenarios where multiple checks are desired.

   ### Conclusion

   Understanding the difference between soft and hard assertions is essential for effective testing. Depending on your testing needs, you can choose the appropriate assertion method to ensure comprehensive and reliable test coverage.

10. JUnit and TestNG are both popular testing frameworks for Java, but they have different features, capabilities, and use cases. Here’s a comparison of the two:

    ### 1. **Annotations**

    - **JUnit**: Uses simple annotations like `@Test`, `@Before`, `@After`, etc. JUnit 5 introduced additional annotations like `@BeforeEach`, `@AfterEach`, `@BeforeAll`, and `@AfterAll`.
    - **TestNG**: Offers a wider variety of annotations, such as `@Test`, `@BeforeMethod`, `@AfterMethod`, `@BeforeClass`, `@AfterClass`, `@BeforeSuite`, and `@AfterSuite`. This provides more control over test execution and setup.

    ### 2. **Test Configuration**

    - **JUnit**: Supports basic configuration through its annotations but is less flexible when it comes to complex test setups.
    - **TestNG**: Provides a more comprehensive configuration system through XML files, allowing users to define test suites, groups, and test dependencies.

    ### 3. **Parallel Testing**

    - **JUnit**: JUnit supports parallel test execution starting from JUnit 5, but it requires additional configuration and is less straightforward.
    - **TestNG**: Has built-in support for parallel test execution, making it easier to run tests concurrently by simply specifying parameters in the XML configuration.

    ### 4. **Data-Driven Testing**

    - **JUnit**: Provides parameterized tests, but they require some setup and are not as straightforward.
    - **TestNG**: Offers a powerful and flexible mechanism for data-driven testing through the `@DataProvider` annotation, allowing for easy testing with multiple sets of data.

    ### 5. **Dependency Testing**

    - **JUnit**: Does not support test dependencies natively; tests are generally independent of each other.
    - **TestNG**: Allows defining test dependencies, enabling tests to be executed based on the success or failure of other tests.

    ### 6. **Grouping Tests**

    - **JUnit**: Offers no direct support for grouping tests; tests are typically run in a single class or package.
    - **TestNG**: Supports grouping of tests, allowing users to run a specific group of tests based on categories defined in the XML configuration.

    ### 7. **Exception Handling**

    - **JUnit**: Uses `@Test(expected = Exception.class)` to indicate that a specific exception is expected during test execution.
    - **TestNG**: Provides a more flexible approach using the `expectedExceptions` attribute in the `@Test` annotation or the `@Test` with `invocationCount` to handle exceptions and retries.

    ### 8. **Test Suites**

    - **JUnit**: Supports test suites, but they are defined in code and are less flexible.
    - **TestNG**: Provides a robust suite configuration using XML files, allowing for easy grouping and execution of multiple test classes.

    ### 9. **Integration**

    - **JUnit**: Often integrated with various build tools like Maven and Gradle, and is the default framework for many IDEs.
    - **TestNG**: Also integrates well with build tools and IDEs, but it’s particularly popular in Selenium WebDriver tests for automated testing in web applications.

    ### Summary

    - **JUnit** is ideal for simple unit testing and is widely used due to its ease of use and integration with various tools.
    - **TestNG** is more suitable for complex testing scenarios that require advanced features like parallel execution, data-driven testing, and test configuration.

    In conclusion, the choice between JUnit and TestNG largely depends on the specific requirements of the project. For straightforward unit tests, JUnit may suffice, while TestNG is better suited for more complex testing needs.

11. 