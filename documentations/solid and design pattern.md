# 1. SOLID Principle  

Design principles encourage us to create more maintainable, understandable, and flexible software. Consequently, as our applications grow in size, we can reduce their complexity and save ourselves a lot of headaches further down the road!

The following **five** concepts make up our SOLID principles:

### Table of contents

1. [Single Responsibility](#11-single-responsibility)
2. [Open/Closed Principle](#12-open-for-extension-closed-for-modification)
3. [Liskov Substitution Principle](#13-liskov-substitution-principle)
4. [Interface Segregation Principle](#14-interface-segregation-principle)
5. [Dependency Inversion Principle](#15-dependency-inversion-principle)




## 1.1 Single Responsiblity
[Back to Table of Contents](#Table-of-contents)

> a class should only have one responsibility. Furthermore, it should only have one reason to change.

**Benifits:**
- Less Coupling
- Less Testing 
- Organization 


### **Example: 1** Violation of SRP; 
``` java
public class Report {
    private String content;

    public Report(String content) {
        this.content = content;
    }

    // Method to generate the report content
    public void generateReport() {
        System.out.println("Generating report content: " + content);
    }

    // Method to print the report
    public void printReport() {
        System.out.println("Printing report: " + content);
    }

    // Method to save the report to a file
    public void saveToFile(String filename) {
        // Code to save the report content to a file
        System.out.println("Saving report to file: " + filename);
    }
}
```
**Problems:**
- The Report class has multiple responsibilities: generating, printing, and saving the report.
- If you need to change how the report is saved (e.g., to a database instead of a file), you would need to modify this class, violating SRP.

> **SRP-Compliant Design**
```java
public class Report {
    private String content;

    public Report(String content) {
        this.content = content;
    }

    // Method to generate the report content
    public void generateReport() {
        System.out.println("Generating report content: " + content);
    }

    public String getContent() {
        return content;
    }
}

// Separate class for printing the report
public class ReportPrinter {
    public void print(Report report) {
        System.out.println("Printing report: " + report.getContent());
    }
}

// Separate class for saving the report
public class ReportSaver {
    public void saveToFile(Report report, String filename) {
        // Code to save the report content to a file
        System.out.println("Saving report to file: " + filename);
    }
}

```
## 1.2 Open for Extention Closed for Modification


> Simply put, classes should be open for extension but closed for modification. 

In doing so, we stop ourselves from modifying existing code and causing potential new bugs in an otherwise happy application.

Of course, the **one exception to the rule is when fixing bugs in existing code. 🤔**

**Benefits:**

- Class hierarchy remains untouched, 
- ensuring stability and reduce risk of bugs 

### **Example:** Violation of OCP
Here’s an example where the **Shape class** violates the Open/Closed Principle:
```java
public class Shape {
    // no extention 
    public double calculateArea(Object shape) {
        // checking instance type 
        if (shape instanceof Circle) {
            Circle circle = (Circle) shape;
            return Math.PI * circle.radius * circle.radius;
        } else if (shape instanceof Rectangle) {
            Rectangle rectangle = (Rectangle) shape;
            return rectangle.length * rectangle.width;
        }
        return 0;
    }
}

class Circle {
    public double radius;

    public Circle(double radius) {
        this.radius = radius;
    }
}

class Rectangle {
    public double length;
    public double width;

    public Rectangle(double length, double width) {
        this.length = length;
        this.width = width;
    }
}

```
**Problems:**
- To add a new shape, like a Triangle, you need to modify the Shape class by adding more if or else if conditions.
- This violates the Open/Closed Principle because the class is not closed for modification.

**OCP-Compliant Design:**

Now, let’s refactor the code to comply with the Open/Closed Principle:
```java
abstract class Shape {
    abstract double calculateArea();
}

class Circle extends Shape {
    private double radius;

    public Circle(double radius) {
        this.radius = radius;
    }

    @Override
    public double calculateArea() {
        return Math.PI * radius * radius;
    }
}

class Rectangle extends Shape {
    private double length;
    private double width;

    public Rectangle(double length, double width) {
        this.length = length;
        this.width = width;
    }

    @Override
    public double calculateArea() {
        return length * width;
    }
}
```
**Adding new shape Triangle**
```java
class Triangle extends Shape {
    private double base;
    private double height;

    public Triangle(double base, double height) {
        this.base = base;
        this.height = height;
    }

    @Override
    public double calculateArea() {
        return 0.5 * base * height;
    }
}

```

## 1.3 Liskov Substitution Principle
[Back to Table of Contents](#Table-of-contents)

> "Objects of a superclass should be replaceable with objects of a subclass without affecting the correctness of the program."

In simpler terms, this means that if you have a class B that extends class A, you should be able to replace A with B without introducing bugs or unexpected behavior. The subclass B should honor the contract established by the superclass A.

**Key Points:** 
1. Substitutablity
2. Behabioral Consistency
3. No Strengthened Preconditions
4. No Weakened Postconditions 

**Example:**
Let’s consider a basic example with a Rectangle class and a subclass Square.

``` java
// Superclass
class Rectangle {
    protected int width;
    protected int height;

    public void setWidth(int width) {
        this.width = width;
    }

    public void setHeight(int height) {
        this.height = height;
    }

    public int getArea() {
        return width * height;
    }
}

// Subclass that violates LSP
class Square extends Rectangle {
    @Override
    public void setWidth(int width) {
        this.width = width;
        this.height = width; // Ensuring both sides are equal
    }

    @Override
    public void setHeight(int height) {
        this.height = height;
        this.width = height; // Ensuring both sides are equal
    }
}

```
In this case:

- The Square class overrides the setWidth and setHeight methods to ensure that the width and height are always equal, maintaining the square’s properties.
- This, however, violates the Liskov Substitution Principle because if we substitute a Square object where a Rectangle is expected, the behavior changes.

**Problem Demonstration:**

``` java
public class Main {
    public static void main(String[] args) {
        Rectangle rect = new Rectangle();
        rect.setWidth(5);
        rect.setHeight(10);
        System.out.println(rect.getArea()); // Outputs 50

        Rectangle square = new Square();
        square.setWidth(5);
        square.setHeight(10);
        System.out.println(square.getArea()); // Outputs 100, but expected 50
    }
}
```
**In this example:**

The Rectangle behaves as expected, but when we replace it with a Square, the result is different. The Square changes the behavior of the getArea() method due to its constraints on width and height being equal. This violates LSP, as the client code expects the behavior of Rectangle but gets the unexpected behavior of Square.

### Example: Correct Use of **LSP**; 

To adhere to LSP, Square should not extend Rectangle if it cannot honor the rectangle’s contract. Instead, you might treat Square and Rectangle as separate classes with a common interface or abstract class.

```java
interface Shape {
    int getArea();
}

class Rectangle implements Shape {
    protected int width;
    protected int height;

    public void setWidth(int width) {
        this.width = width;
    }

    public void setHeight(int height) {
        this.height = height;
    }

    public int getArea() {
        return width * height;
    }
}

class Square implements Shape {
    private int side;

    public void setSide(int side) {
        this.side = side;
    }

    public int getArea() {
        return side * side;
    }
}

```
**In this correct design:**

Both Rectangle and Square implement the Shape interface, but they are not in a parent-child relationship.
Now, each shape maintains its own integrity without violating LSP.

### Summary: 
- Violations of LSP **often occur when a subclass overrides** or extends methods in a way that changes the expected behavior, leading to unexpected results.
- To adhere to LSP, ensure that subclasses truly represent the superclass and don't introduce changes that break the established contract.


## 1.4 Interface Segregation Principle
It states that “do not force any client to implement an interface which is irrelevant to them“. Here main goal is to focus on avoiding fat interface and give preference to many small client-specific interfaces. 

> Larger interfaces should be split into smaller ones. 

By doing so, we can ensure that implementing classes only need to be concerned about the methods that are of interest to them.

**Key Points:**
- Avoid "Fat" Interfaces
- Promotes High Cohsion
- Improves Flexibility and Maintainability: 
- Enhances Reusability

## 1.5 Dependency Inversion Principle (DIP)

> High-level modules should not depend on the low-level module but both should depend on the abstraction. Because the abstraction does not depend on detail but the detail depends on abstraction.


**Key Points:**
- DIP is obtained through **Dependency Injection**
- **Loose couplig:** By injecting dependencies, classes don’t need to know about the specific implementations of their dependencies. T
- **Reduced dependencies:** Block of code can be changed with out **affecting the other code blocks**
- **Ease of Maintenance and Extension:** Since classes depend on abstractions (interfaces) rather than concrete implementations, it's easier to change or extend functionality without modifying the dependent classes.



> **Foot Note:**
<details>
<summary><span style="color: brown; font-weight: bold">Click to expand/collapse.</span></summary>

1. **Dependency:** Any object, that another object depends on to perform its tasks. For example, if a class B uses an instance of class A, then A is a **dependency** of B.
**can be obtained using:**
 - Has - A
 - Is - A

2. **Injection:** The process of providing the dependency to the dependent object. This can be done in several ways, which are known as DI types or methods.

    >*Types of Dependency Injection:*
    
    1. **Constructor Injection:** Dependencies are provided through the class's constructor. This is the most common form of DI.

    ```java
    class Service {
        private Repository repository;

        // Constructor Injection 
        public Service(Repository repository) {
            this.repository = repository;
        }

        public void performOperation() {
            repository.saveData("data");
        }
    }
    ```
    2. **Setter Injection:**  Dependencies are provided through setter methods after the object is constructed.

    ```java
    class Service {
        private Repository repository;

        // setter DI
        public void setRepository(Repository repository) {
            this.repository = repository;
        }

        public void performOperation() {
            repository.saveData("data");
        }
    }
    ```

    3. **Interface Injection:** The dependency is injected through an interface that the dependent class implements. *This method is less common.*

    ```java
    interface RepositoryInjector {
        void injectRepository(Repository repository);
    }

    class Service implements RepositoryInjector {
        private Repository repository;

        @Override
        public void injectRepository(Repository repository) {
            this.repository = repository;
        }

        public void performOperation() {
            repository.saveData("data");
        }
    }
    ```

    4. **Field Injection:**
    Dependencies are directly injected into the fields of a class, typically using **reflection in frameworks like Spring.** *This method is also less commonly used due to potential difficulties in testing and understanding the code.*

    ``` java 
    class Service {
        @Inject
        private Repository repository;

        public void performOperation() {
            repository.saveData("data");
        }
    }
    ```
    In this case, a dependency injection framework would automatically inject the **Repository dependency** into the **Service** class.


>**Coupling vs Cohesion:**

| **Aspect**      | **Cohesion**                                  | **Coupling**                              |
|-----------------|-----------------------------------------------|-------------------------------------------|
| **Definition**  | Degree to which the elements of a module are related and focused on a single task. | Degree of interdependence between modules or components. |
| **Goal**        | High cohesion.                                | Low coupling.                             |
| **Benefits**    | Easier maintenance, better reusability.       | Easier maintenance, improved flexibility, easier testing. |
| **Example**     | A class that handles only user authentication tasks. | A class that interacts with a database via an interface, not a specific implementation. |
  
    

</details>

### **Example 1**: Payment Processing System
Problem Without Dependency Inversion
Imagine a simple e-commerce application where payments can be processed through different payment gateways like PayPal or Stripe. Initially, the payment processing might be **tightly coupled** to a specific payment gateway:

```java
// Low-level module
class PayPalPaymentGateway {
    public void processPayment(double amount) {
        System.out.println("Processing payment via PayPal: $" + amount);
    }
}

// High-level module
class PaymentProcessor {
    private PayPalPaymentGateway payPalPaymentGateway;

    public PaymentProcessor() {
        this.payPalPaymentGateway = new PayPalPaymentGateway();
    }

    public void process(double amount) {
        payPalPaymentGateway.processPayment(amount);
    }
}
```
**Here:**
- The PaymentProcessor class is tightly coupled to PayPalPaymentGateway.
- Adding support for a new payment gateway (e.g., Stripe) would require modifying the PaymentProcessor class.


**Applying Dependency Inversion:**
To apply DIP, we introduce an interface that both the high-level and low-level modules depend on some abstraction like **interface**

```java
// Abstraction
interface PaymentGateway {
    void processPayment(double amount);
}

// Low-level module 1
class PayPalPaymentGateway implements PaymentGateway {
    public void processPayment(double amount) {
        System.out.println("Processing payment via PayPal: $" + amount);
    }
}

// Low-level module 2
class StripePaymentGateway implements PaymentGateway {
    public void processPayment(double amount) {
        System.out.println("Processing payment via Stripe: $" + amount);
    }
}

// High-level module
class PaymentProcessor {
    private PaymentGateway paymentGateway;

    // Constructor injection
    public PaymentProcessor(PaymentGateway paymentGateway) {
        this.paymentGateway = paymentGateway;
    }
    // we can use this same code to implement diff paymentGateway 
    public void process(double amount) {
        paymentGateway.processPayment(amount);
    }
}
```
With this design:

- The PaymentProcessor class depends on the PaymentGateway interface rather than a specific implementation.
- You can easily switch between PayPalPaymentGateway, StripePaymentGateway, or any other gateway without changing the PaymentProcessor class.

**Main Function:**
```java
public class Main {
    public static void main(String[] args) {
        // Use PayPalPaymentGateway
        PaymentGateway payPal = new PayPalPaymentGateway();
        PaymentProcessor paymentProcessor = new PaymentProcessor(payPal);
        paymentProcessor.process(100.00);

        // Use StripePaymentGateway
        PaymentGateway stripe = new StripePaymentGateway();
        PaymentProcessor anotherProcessor = new PaymentProcessor(stripe);
        anotherProcessor.process(200.00);
    }
}
```

### Example 2: Logger in an Application
**Problem Without Dependency Inversion**

Consider an application that logs messages to a file. Initially, the logging functionality might be directly tied to a file-based logger:

```java
// Low-level module
class FileLogger {
    public void log(String message) {
        System.out.println("Logging to file: " + message);
    }
}

// High-level module
class Application {
    private FileLogger logger;

    public Application() {
        this.logger = new FileLogger();
    }

    public void run() {
        logger.log("Application started");
    }
}

```
In this case:

- The Application class is tightly coupled to FileLogger.
- If you want to switch to a different logging mechanism (e.g., logging to a database or console), you'd need to modify the Application class.

**Applying Dependency Inversion**
By introducing a Logger interface, we decouple the Application class from the specific logging implementation:
``` java
// Abstraction
interface Logger {
    void log(String message);
}

// Low-level module 1
class FileLogger implements Logger {
    public void log(String message) {
        System.out.println("Logging to file: " + message);
    }
}

// Low-level module 2
class ConsoleLogger implements Logger {
    public void log(String message) {
        System.out.println("Logging to console: " + message);
    }
}

// High-level module
class Application {
    private Logger logger;

    // Constructor injection
    public Application(Logger logger) {
        this.logger = logger;
    }

    public void run() {
        logger.log("Application started");
    }
}

```

**Main Function:**
```java
public class Main {
    public static void main(String[] args) {
        // Use FileLogger
        Logger fileLogger = new FileLogger();
        Application appWithFileLogger = new Application(fileLogger);
        appWithFileLogger.run();

        // Use ConsoleLogger
        Logger consoleLogger = new ConsoleLogger();
        Application appWithConsoleLogger = new Application(consoleLogger);
        appWithConsoleLogger.run();
    }
}
```
**With this design:**

- The Application class depends on the Logger interface, making it easy to switch or extend logging mechanisms without modifying the high-level logic


