# Table of contents

1. [SOLID Principle:](#1-solid-principle)
   1. [Single Responsibility](#11-single-responsibility)
   2. [Open/Closed Principle](#12-open-for-extension-closed-for-modification)
   3. [Liskov Substitution Principle](#13-liskov-substitution-principle)
   4. [Interface Segregation Principle](#14-interface-segregation-principle)
   5. [Dependency Inversion Principle](#15-dependency-inversion-principle)
2. [Design Pattern:](#2-design-pattern)

   - Creational Design Patterns

     1. [Builder Pattern](#21-builder)

   - Structural Design Patterns

     1. [Proxy Pattern](#22-proxy)

   - Behavioral Design Patterns

     1. [Strategey Pattern](#23-strategy)


3. [Refferances](#3-referrances)

# 1. SOLID Principle

Design principles encourage us to create more maintainable, understandable, and flexible software. Consequently, as our applications grow in size, we can reduce their complexity and save ourselves a lot of headaches further down the road!

The following **five** concepts make up our SOLID principles:

1. [Single Responsibility](#11-single-responsibility)
2. [Open/Closed Principle](#12-open-for-extension-closed-for-modification)
3. [Liskov Substitution Principle](#13-liskov-substitution-principle)
4. [Interface Segregation Principle](#14-interface-segregation-principle)
5. [Dependency Inversion Principle](#15-dependency-inversion-principle)

## 1.1 Single Responsibility

[⬆️Back To Top](#table-of-contents)

> a class should only have one responsibility. Furthermore, it should only have one reason to change.

**Benifits:**

- Less Coupling
- Less Testing
- Organization

### **Example: 1** Violation of SRP;

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

## 1.2 Open for Extension Closed for Modification

[⬆️Back To Top](#table-of-contents)

> Simply put, classes should be open for extension but closed for modification.

In doing so, we stop ourselves from modifying existing code and causing potential new bugs in an otherwise happy application.

Of course, the **one exception to the rule is when fixing bugs in existing code. 🤔**

**Benefits:**

- Enhanced Maintainability: Reduces the need to modify existing code when adding new features, making the codebase easier to maintain.
- Increased Reusability: Promotes code reuse by allowing new functionality to be added through extension rather than modification.
- Improved Flexibility: Facilitates system evolution by accommodating new requirements with minimal disruption to existing code.
- Reduces the Risk of Regression:Since OCP minimizes changes to existing code, it reduces the likelihood of introducing regression bugs (bugs that occur when a new feature breaks existing functionality). 


### **Example:** Violation of OCP

Here’s an example where the **Shape class** violates the Open/Closed Principle:

```java
class Shape {
    // no extention
    public double calculateArea(Object shape) {
        // checking instance type
        if (shape instanceof Circle) {
            Circle circle = (Circle) shape; // down casting 
            return Math.PI * circle.radius * circle.radius;
        } else if (shape instanceof Rectangle) {
            Rectangle rectangle = (Rectangle) shape;
            return rectangle.length * rectangle.width;
        }

        // adding new functionality requires chage to Shape class [the current one]
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
main function
```java
public class OCP {

	public static void main(String[] args) {
		// TODO Auto-generated method stub
		Rectangle rectangle = new Rectangle(5, 10); // up casting 
		Circle circle = new Circle(3);
		AreaCalculator areaCalculator = new AreaCalculator();
		System.out.println(areaCalculator.calculateArea(rectangle));
		System.out.println(areaCalculator.calculateArea(circle)); 
		
	}

}
```
**Problems:**

- To add a new shape, like a Triangle, we need to **modify the Shape class** by adding more if or else if conditions.
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

Main Function
```java
public class Main {
    public static void main(String[] args) {
        Shape rectangle = new Rectangle(5, 10);
        Shape circle = new Circle(7);

        AreaCalculator calculator = new AreaCalculator();

        System.out.println("Rectangle area: " + calculator.calculateArea(rectangle)); // 50.0
        System.out.println("Circle area: " + calculator.calculateArea(circle));       // 153.94...
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
### Key Challenges and Considerations:
- **Complexity in Design:**
    
    - Designing a system that adheres to OCP can require a more complex and abstract design, involving interfaces or abstract classes. This can make the initial design more challenging and harder to understand.
- **Difficulty in Predicting Future Requirements:**
    
    - It can be challenging to anticipate how the system will need to evolve. If future requirements are not well understood, designing a system to be easily extensible might result in a design that doesn’t fit the actual needs.
- **Increased Development Time:**
    
    - Implementing OCP may require additional time for designing and implementing the necessary abstractions and extensions, potentially impacting development timelines.
## 1.3 Liskov Substitution Principle

[⬆️Back To Top](#table-of-contents)

> "Objects of a superclass should be replaceable with objects of a subclass without affecting the correctness of the program."

In simpler terms, this means that if you have a class B that extends class A, you should be able to replace A with B without introducing bugs or unexpected behavior. The subclass B should honor the contract established by the superclass A.

**Key Points:**

1. Substitutablity
2. Behabioral Consistency
3. No Strengthened Preconditions
4. No Weakened Postconditions

**Example:**
Let’s consider a basic example with a Rectangle class and a subclass Square.

```java
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

```java
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

[⬆️Back To Top](#table-of-contents)

It states that “do not force any client to implement an interface which is irrelevant to them“. Here main goal is to focus on avoiding fat interface and give preference to many small client-specific interfaces.

> Larger interfaces should be split into smaller ones.

By doing so, we can ensure that implementing classes only need to be concerned about the methods that are of interest to them.

**Key Points:**

- Avoid "Fat" Interfaces
- Promotes High Cohsion
- Improves Flexibility and Maintainability:
- Enhances Reusability

### Example

**Violation of ISP**

```java
interface Worker {
    void work();
    void eat();
}

class Developer implements Worker {
    @Override
    public void work() {
        System.out.println("Developer is coding.");
    }

    @Override
    public void eat() {
        System.out.println("Developer is eating.");
    }
}

class Robot implements Worker {
    @Override
    public void work() {
        System.out.println("Robot is working.");
    }

    @Override
    public void eat() {
        throw new UnsupportedOperationException("Robot does not eat.");
    }
}
```

Robot doesn't required to eat but as it implements Worker interface it has to override eat() method;

**Adherence to ISP**

```java
interface Workable {
    void work();
}

interface Eatable {
    void eat();
}

class Developer implements Workable, Eatable {
    @Override
    public void work() {
        System.out.println("Developer is coding.");
    }

    @Override
    public void eat() {
        System.out.println("Developer is eating.");
    }
}

class Robot implements Workable {
    @Override
    public void work() {
        System.out.println("Robot is working.");
    }
}
```

**Main Function**

```java
public class Main {
    public static void main(String[] args) {
        Workable developer = new Developer();
        developer.work();

        Eatable eatableDeveloper = (Eatable) developer;
        eatableDeveloper.eat();

        Workable robot = new Robot();
        robot.work();
    }
}
```

we split the Worker interface to Workable and Eatable and then classes can implement them as they please

## 1.5 Dependency Inversion Principle

[⬆️Back To Top](#table-of-contents)

> High-level modules should not depend on the low-level module but both should depend on the abstraction. Because the abstraction does not depend on detail but the detail depends on abstraction.

**Key Points:**

- DIP is obtained through **Dependency Injection**
- **Loose couplig:** By injecting dependencies, classes don’t need to know about the specific implementations of their dependencies. T
- **Reduced dependencies:** Block of code can be changed with out **affecting the other code blocks**
- **Ease of Maintenance and Extension:** Since classes depend on abstractions (interfaces) rather than concrete implementations, it's easier to change or extend functionality without modifying the dependent classes.

> **Foot Note:** > [⬆️Back To Top](#table-of-contents)

<details>
<summary><span style="color: brown; font-weight: bold">Click to expand/collapse.</span></summary>

1. **Dependency:** Any object, that another object depends on to perform its tasks. For example, if a class B uses an instance of class A, then A is a **dependency** of B.
   **can be obtained using:**

- Has - A
- Is - A

2. **Injection:** The process of providing the dependency to the dependent object. This can be done in several ways, which are known as DI types or methods.

   > _Types of Dependency Injection:_

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

   2. **Setter Injection:** Dependencies are provided through setter methods after the object is constructed.

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

   3. **Interface Injection:** The dependency is injected through an interface that the dependent class implements. _This method is less common._

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
      Dependencies are directly injected into the fields of a class, typically using **reflection in frameworks like Spring.** _This method is also less commonly used due to potential difficulties in testing and understanding the code._

   ```java
   class Service {
       @Inject
       private Repository repository;

       public void performOperation() {
           repository.saveData("data");
       }
   }
   ```

   In this case, a dependency injection framework would automatically inject the **Repository dependency** into the **Service** class.

> **Coupling vs Cohesion:**

| **Aspect**     | **Cohesion**                                                                       | **Coupling**                                                                            |
| -------------- | ---------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------- |
| **Definition** | Degree to which the elements of a module are related and focused on a single task. | Degree of interdependence between modules or components.                                |
| **Goal**       | High cohesion.                                                                     | Low coupling.                                                                           |
| **Benefits**   | Easier maintenance, better reusability.                                            | Easier maintenance, improved flexibility, easier testing.                               |
| **Example**    | A class that handles only user authentication tasks.                               | A class that interacts with a database via an interface, not a specific implementation. |

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

```java
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

# 2. Design Pattern

[⬆️Back To Top](#table-of-contents)

Design patterns are general, reusable solutions to common problems that arise in software design. They represent best practices and are based on the experiences and insights of skilled software developers. Design patterns provide a standardized approach to solving problems that can be applied across various types of software projects.

**Key Aspects of Design Patterns:**

- Reusability
- Common Language
- Best Practices
- Flexibility

### Types of Design Patterns:

1. **Creational Patterns** 
> Creational Design Pattern abstract the instantiation process. They help in making a system **independent** of how its **objects** are **created, composed and represented**.

   - a. Builder
   - b. Factory
   - c. Singleton
   - d. Prototype

2. **Structural Patterns**
> Structural patterns are concerned with how classes and objects are **composed to form larger structures.** Structural class patterns use **inheritance** to compose interfaces or implementations.

   - a. Proxy
   - b. Facade
   - c. Decorator
   - d. Adapter 

3. **Behavioral Patterns**
> Behavioral patterns are concerned with algorithms and the assignment of responsibilities between objects. Behavioral patterns **describe not just patterns of objects or classes** but also the **patterns of communication between them.**
   - a. Strategy
   - b. Observer
   - c. Command
   - d. Chain of Responsibility

## 2.1 Builder

[⬆️Back To Top](#table-of-contents)

Builder is a _creational_ design pattern, which allows _constructing complex objects_ in a step by step fashion, where the construction process can vary based on the type of product being built. The pattern separates the construction of a complex object from its representation, allowing the same construction process to create different representations.

> Unlike other creational patterns, Builder **doesn’t require** products to have **a common interface**. That makes it possible to produce **different products** using the same construction process. **[Different Concrete builder to produce different products]**

[example](#builder-more-example)

Components of the Builder Design Pattern

1. Product
2. Builder
3. ConcreteBuilder
4. Director
5. Client

**1.Product** is the `complex object` that the Builder pattern is responsible for `constructing`.

- It may consist of multiple components or parts, and its structure can vary based on the implementation.
- The Product is typically a class with attributes representing the different parts that the Builder constructs.

**2. Builder** is an `interface or an abstract class` that declares the construction steps for building a complex object.

- It typically includes methods for constructing individual parts of the product.
- By defining an interface, the Builder allows for the creation of different concrete builders that can produce variations of the product.

**3. ConcreteBuilder** classes implement the `Builder interface`, providing `specific implementations` for building each part of the product.

- Each ConcreteBuilder is tailored to create a specific variation of the product.
- It keeps track of the product being constructed and provides methods for setting or constructing each part.

**4. Director** is responsible for managing the construction process of the `complex object.`

- It collaborates with a Builder, but it doesn’t know the specific details about how each part of the object is constructed.
- It provides a high-level interface for constructing the product and managing the steps needed to create the complex object.

**5. Client** is the code that initiates the construction of the `complex object.`

- It creates a Builder object and passes it to the Director to initiate the construction process.
- The Client may retrieve the final product from the Builder after construction is complete.

### Builder Design Pattern Example:

> Scenario:

You are tasked with implementing a system for building custom computers. Each computer can have different configurations based on user preferences. The goal is to provide flexibility in creating computers with varying CPUs, RAM, and storage options.

Implement the Builder design pattern to achieve this, allowing the construction of computers through a step-by-step process. Use the provided components – Product (Computer), Builder interface, ConcreteBuilder (GamingComputerBuilder), Director, and Client

![Builder example](https://github.com/rds8rds/nsl_trainee_program/blob/main/images/solid%20and%20design%20pattern/builder-example-updated.jpg?raw=true)

1. Product (Computer):

```java
// Product
// its a mutable object creation example 

public class Computer {
    private String cpu;
    private String ram;
    private String storage;

    public void setCPU(String cpu) {
        this.cpu = cpu;
    }

    public void setRAM(String ram) {
        this.ram = ram;
    }

    public void setStorage(String storage) {
        this.storage = storage;
    }

    public void displayInfo() {
        System.out.println("Computer Configuration:");
        System.out.println("CPU: " + cpu);
        System.out.println("RAM: " + ram);
        System.out.println("Storage: " + storage);
    }
}

```

2. Builder Interface

```java
// Builder interface
public interface Builder {
    void buildCPU();
    void buildRAM();
    void buildStorage();
    Computer getResult();
}
```

3. ConcreteBuilder (GamingComputerBuilder)

```java
// ConcreteBuilder
public class GamingComputerBuilder implements Builder {
    private Computer computer = new Computer();

    @Override
    public void buildCPU() {
        computer.setCPU("Gaming CPU");
    }

    @Override
    public void buildRAM() {
        computer.setRAM("16GB DDR4");
    }

    @Override
    public void buildStorage() {
        computer.setStorage("1TB SSD");
    }

    @Override
    public Computer getResult() {
        return computer;
    }
}
```

4. Director (ComputerDirector)

```java
// Director
public class ComputerDirector {
    public void construct(Builder builder) {
        builder.buildCPU();
        builder.buildRAM();
        builder.buildStorage();
    }
}
```

5. Client

```java
// Client
public class Main {
    public static void main(String[] args) {
        GamingComputerBuilder gamingBuilder = new GamingComputerBuilder();
        ComputerDirector director = new ComputerDirector();

        director.construct(gamingBuilder);
        Computer gamingComputer = gamingBuilder.getResult();

        gamingComputer.displayInfo();
    }
}
```

Output:

```
Computer Configuration:
CPU: Gaming CPU
RAM: 16GB DDR4
Storage: 1TB SSD
```

**When to use Builder Design Pattern?**

- Complex Object Construction
- Step-by-step construction
- Avoiding constructors with multiple parameters
- Immutable Objects [no change in object attribute after creation]
- Configurable Object Creation [ we can configure the object on our requirements ]
- Common Interface for Multiple Representations

**When not to use Builder Design Pattern?**

- Simple Object Construction
  - If the object you are constructing has only a few simple parameters or configurations, and the construction process is straightforward, using a builder might be overkill. In such cases, a simple constructor or `static factory method` might be more appropriate.
- Performace Concerns
  - In performance-critical applications, the additional overhead introduced by the Builder pattern might be a concern. The extra method calls and object creations involved in the builder process could impact performance, especially if the object construction is frequent and time-sensitive.
- Increased Code Complexity

  - Introducing a builder class for every complex object can lead to an increase in code complexity. If the object being constructed is simple and doesn’t benefit significantly from a step-by-step construction process, using a builder might add unnecessary complexity to the codebase.

- Tight Coupling with Product
  - If the builder is tightly coupled with the product it constructs, and changes to the product require corresponding modifications to the builder, it might reduce the flexibility and maintainability of the code.

#### Builder more example contents

[⬆️](#21-builder)

- [no common interface](#no-common-interface-example)
- [immutable class example](#immutable-class-example)
- [configurable object creation](#configurable-object-creation)

#### no common interface example

[⬆️](#builder-more-example-contents)

```java
/*
** builder to build object with no common interface
*/

// Product: Website
class Website {
    private String homepage;
    private String aboutPage;
    private String contactPage;

    // Setters
    public void setHomepage(String homepage) {
        this.homepage = homepage;
    }

    public void setAboutPage(String aboutPage) {
        this.aboutPage = aboutPage;
    }

    public void setContactPage(String contactPage) {
        this.contactPage = contactPage;
    }

    @Override
    public String toString() {
        return "Website [Homepage=" + homepage + ", About Page=" + aboutPage + ", Contact Page=" + contactPage + "]";
    }
}

// Concrete Builder for Website
class WebsiteBuilder {
    private Website website = new Website();

    public void buildHomepage() {
        website.setHomepage("Homepage Content");
    }

    public void buildAboutPage() {
        website.setAboutPage("About Us Content");
    }

    public void buildContactPage() {
        website.setContactPage("Contact Us Content");
    }

    public Website getWebsite() {
        return website; // Returning the built website
    }
}

// Product: Meal
class Meal {
    private String mainItem;
    private String drink;
    private String dessert;

    // Setters
    public void setMainItem(String mainItem) {
        this.mainItem = mainItem;
    }

    public void setDrink(String drink) {
        this.drink = drink;
    }

    public void setDessert(String dessert) {
        this.dessert = dessert;
    }

    @Override
    public String toString() {
        return "Meal [Main Item=" + mainItem + ", Drink=" + drink + ", Dessert=" + dessert + "]";
    }
}

// Concrete Builder for Meal
class MealBuilder {
    private Meal meal = new Meal();

    public void buildMainItem() {
        meal.setMainItem("Burger");
    }

    public void buildDrink() {
        meal.setDrink("Coke");
    }

    public void buildDessert() {
        meal.setDessert("Ice Cream");
    }

    public Meal getMeal() {
        return meal; // Returning the built meal
    }
}

// Director Class
class Director {
    public void constructWebsite(WebsiteBuilder builder) {
        builder.buildHomepage();
        builder.buildAboutPage();
        builder.buildContactPage();
    }

    public void constructMeal(MealBuilder builder) {
        builder.buildMainItem();
        builder.buildDrink();
        builder.buildDessert();
    }
}

// Client Code
public class Main {
    public static void main(String[] args) {
        Director director = new Director();

        // Building a Website
        WebsiteBuilder websiteBuilder = new WebsiteBuilder();
        director.constructWebsite(websiteBuilder);
        Website website = websiteBuilder.getWebsite();
        System.out.println(website);

        // Building a Meal
        MealBuilder mealBuilder = new MealBuilder();
        director.constructMeal(mealBuilder);
        Meal meal = mealBuilder.getMeal();
        System.out.println(meal);
    }
}
```

#### Immutable class example

[⬆️](#builder-more-example-contents)

```java
// Immutable Class
public class Person {
    private final String firstName;  // Final fields
    private final String lastName;
    private final int age;

    // Private constructor accessible only by the Builder
    private Person(PersonBuilder builder) {
        this.firstName = builder.firstName;
        this.lastName = builder.lastName;
        this.age = builder.age;
    }

    // No setters, only getters
    public String getFirstName() {
        return firstName;
    }

    public String getLastName() {
        return lastName;
    }

    public int getAge() {
        return age;
    }

    // Static Builder class
    public static class PersonBuilder {
        private String firstName;  // Same fields as in the Person class
        private String lastName;
        private int age;

        // Fluent interface for setting fields
        public PersonBuilder setFirstName(String firstName) {
            this.firstName = firstName;
            return this;
        }

        public PersonBuilder setLastName(String lastName) {
            this.lastName = lastName;
            return this;
        }

        public PersonBuilder setAge(int age) {
            this.age = age;
            return this;
        }

        // Method to build the immutable Person object
        public Person build() {
            // Here, you can add validations if needed
            return new Person(this);
        }
    }
}

// Client Code
public class Main {
    public static void main(String[] args) {
        // Creating an immutable Person object using the Builder pattern
        Person person = new Person.PersonBuilder()
                .setFirstName("John")
                .setLastName("Doe")
                .setAge(30)
                .build();  // Immutable Person object

        System.out.println(person.getFirstName());  // Outputs: John
    }
}
```

#### configurable object creation

[⬆️](#builder-more-example-contents)

```java
// Product: Car
public class Car {
    private final String engineType;
    private final String color;
    private final boolean hasSunroof;
    private final boolean hasGPS;

    // Private constructor, only accessible by the Builder
    private Car(CarBuilder builder) {
        this.engineType = builder.engineType;
        this.color = builder.color;
        this.hasSunroof = builder.hasSunroof;
        this.hasGPS = builder.hasGPS;
    }

    @Override
    public String toString() {
        return "Car [Engine Type=" + engineType + ", Color=" + color + ", Sunroof=" + hasSunroof + ", GPS=" + hasGPS + "]";
    }

    // Static Builder class
    public static class CarBuilder {
        // Required parameters
        private final String engineType;

        // Optional parameters with default values
        private String color = "White";
        private boolean hasSunroof = false;
        private boolean hasGPS = false;

        // Constructor for required parameters
        public CarBuilder(String engineType) {
            this.engineType = engineType;
        }

        // Setter for optional color
        public CarBuilder setColor(String color) {
            this.color = color;
            return this;
        }

        // Setter for optional sunroof
        public CarBuilder setSunroof(boolean hasSunroof) {
            this.hasSunroof = hasSunroof;
            return this;
        }

        // Setter for optional GPS
        public CarBuilder setGPS(boolean hasGPS) {
            this.hasGPS = hasGPS;
            return this;
        }

        // Build method to create the Car object
        public Car build() {
            return new Car(this);
        }
    }
}

// Client Code
public class Main {
    public static void main(String[] args) {
        // Creating a configurable car
        Car car1 = new Car.CarBuilder("V8")
                .setColor("Red")
                .setSunroof(true)
                .build();

        System.out.println(car1);  // Outputs: Car [Engine Type=V8, Color=Red, Sunroof=true, GPS=false]

        // Creating another car with different configurations
        Car car2 = new Car.CarBuilder("Electric")
                .setGPS(true)
                .build();

        System.out.println(car2);  // Outputs: Car [Engine Type=Electric, Color=White, Sunroof=false, GPS=true]
    }
}

```

## 2.2 Proxy

[⬆️Back To Top](#table-of-contents)

The Proxy Design Pattern is a `structural design` pattern that provides a `surrogate` or `placeholder` for another object to control access to it. This pattern is useful when you want to add an `extra layer of control` over access to an object. The proxy acts as an `intermediary`, controlling access to the real object.

> Real world example:

A real-world example can be `a cheque or credit card` as a proxy for our bank account. It can be used in place of cash and provides a means of accessing that cash when required.

> 3 Components of Proxy Design Pattern

1. Subject
2. RealSubject
3. Proxy

### 2.2.1 Subject

The Subject is an `interface or an abstract class` that defines the common interface `shared by the RealSubject and Proxy classes.` It declares the `methods` that the Proxy uses to control access to the RealSubject.

- Declares the common interface for both RealSubject and Proxy.
- Usually includes the methods that the client code can invoke on the RealSubject and the Proxy.

### 2.2.2 RealSubject

The RealSubject is the `actual object` that the Proxy represents. It contains the `real implementation of the business logic` or the `resource` that the `client code wants to access.`

- It Implements the operations declared by the Subject interface.
- Represents the real resource or object that the Proxy controls access to.

### 2.2.3. Proxy

The Proxy acts as a `surrogate` or `placeholder` for the `RealSubject`. It controls access to the real object and may provide additional functionality such as `lazy loading`, `access control`, or `logging`.

- Implements the same interface as the RealSubject (Subject).
- Maintains a reference to the RealSubject.
- Controls access to the RealSubject, adding additional logic if necessary.

> Proxy Design Pattern example
#### Caching and Lazy Loading Example: 
Consider a scenario where your `application` needs to `load and display images`, and you want to `optimize` the `image loading process.` Loading images from disk or other external sources can be `resource-intensive`, especially if the images are` large or stored remotely.`

![Proxy example](https://github.com/rds8rds/nsl_trainee_program/blob/main/images/solid%20and%20design%20pattern/proxy-example.png?raw=true)

> **1. Subject (Image Interface):**

The Image interface declares the `common methods` for displaying images, acting as a `blueprint` for both the `real and proxy objects`. In this design, it defines the display() method that both RealImage and ProxyImage must implement. This ensures a uniform interface for clients interacting with image objects.

```java
// Subject
interface Image {
    void display();
}
```

> **2. RealSubject (RealImage Class):**

The RealImage class represents the `real object` that the `proxy will control access to.`

- It implements the `Image interface`, providing `concrete implementations` for loading and displaying images from disk.
- The constructor initializes the image file name, and the `display()` method is responsible `for loading the image if not already loaded` and then displaying it.

    ```java
    // RealSubject
    class RealImage implements Image {
        private String filename;

        public RealImage(String filename) {
            this.filename = filename;
            loadImageFromDisk();
        }

        private void loadImageFromDisk() {
            System.out.println("Loading image: " + filename);
        }

        public void display() {
            System.out.println("Displaying image: " + filename);
        }
    }
    ```

> **3. Proxy (ProxyImage Class)**:

The ProxyImage class acts as a `surrogate` for the RealImage. It also `implements` the Image interface,` maintaining a reference` to the real image object.

- The display() method in the proxy `checks` whether the real image has been loaded; if not, it creates a new instance of RealImage and delegates the display() call to it.
- This `lazy loading` mechanism ensures that the real image is loaded only when necessary.

  ```java
  // Proxy
  class ProxyImage implements Image {
      private RealImage realImage;
      private String filename;

      public ProxyImage(String filename) {
          this.filename = filename;
      }
      
      //caching functionality 
      public void display() {
          if (realImage == null) {
              realImage = new RealImage(filename);
          }
          realImage.display(); 
      }
  }
  ```

> **4. Client Code:**

The client code (ProxyPatternExample) demonstrates the usage of the Proxy Design Pattern. It creates an Image object, which is actually an instance of ProxyImage.

- The client invokes the display() method on the proxy.
- The proxy, in turn, controls access to the real image, ensuring that it is loaded from disk only when needed.
- Subsequent calls to display() use the cached image in the proxy, avoiding redundant loading and improving performance.

  ```java
  // Client code
  public class ProxyPatternExample {
      public static void main(String[] args) {
          Image image = new ProxyImage("example.jpg");

          // Image will be loaded from disk only when display() is called [lazy loading ]
          image.display();

          // Image will not be loaded again, as it has been cached in the Proxy
          image.display();
      }
  }

  ```

<details>
<summary><span style="color: brown; font-weight: bold">Click to expand/collapse Complete Code of the above example:</span></summary>

This code demonstrates how the Proxy Pattern efficiently manages the loading and displaying of images by introducing a proxy that controls access to the real image object, providing additional functionality such as lazy loading.

```java
// Subject
interface Image {
	void display();
}

// RealSubject
class RealImage implements Image {
	private String filename;

	public RealImage(String filename) {
		this.filename = filename;
		loadImageFromDisk();
	}

	private void loadImageFromDisk() {
		System.out.println("Loading image: " + filename);
	}

	public void display() {
		System.out.println("Displaying image: " + filename);
	}
}

// Proxy
class ProxyImage implements Image {
	private RealImage realImage;
	private String filename;

	public ProxyImage(String filename) {
		this.filename = filename;
	}

	public void display() {
		if (realImage == null) {
			realImage = new RealImage(filename);
		}
		realImage.display();
	}
}

// Client code
public class ProxyPatternExample {
	public static void main(String[] args) {
		Image image = new ProxyImage("example.jpg");

		// Image will be loaded from disk only when display() is called
		image.display();

		// Image will not be loaded again, as it has been cached in the Proxy
		image.display();
	}
}

```

</details>

Output:

```
Loading image: example.jpg
Displaying image: example.jpg
Displaying image: example.jpg

```

### 2.2.4 Why do we need Proxy Design Pattern?

The Proxy Design Pattern is employed to address various concerns and scenarios in software development, providing a way to control access to objects, add functionality, or optimize performance.

- [Lazy Loading:](#caching-and-lazy-loading-example)
  - One of the primary use cases for proxies is lazy loading. In situations where creating or initializing an object is resource-intensive, the proxy delays the creation of the real object until it is actually needed.
  - This can lead to improved performance by avoiding unnecessary resource allocation.
- [Caching:](#caching-and-lazy-loading-example)
  - Proxies can implement caching mechanisms to store results or resources.
  - This is particularly useful when repeated operations on a real object can be optimized by caching previous results, avoiding redundant computations or data fetching.
- [Access Control:](#271-access-control-example)
  - Proxies can enforce access control policies.
  - By acting as a gatekeeper to the real object, proxies can restrict access based on certain conditions, providing security or permission checks.
- [Logging and Monitoring:](#272-logging-example)
  - Proxies provide a convenient point to add logging or monitoring functionalities.
  - By intercepting method calls to the real object, proxies can log information, track usage, or measure performance without modifying the real object.


### 2.2.5 More Examples on Proxy Design Pattern

[⬆️](#table-of-contents)
- [Access Control](#2251-access-control-example)
- [Logging Example](#2252-logging-example)

Let's say you have a `SensitiveData` class that represents some sensitive information that should only be accessed by authorized users. You can use a proxy to control access to this data.


#### [2.2.5.1 Access Control Example](#225-more-examples-on-proxy-design-pattern)


##### 1\. **Subject Interface**

First, define an interface that both the real object and the proxy will implement.

```java
public interface Data {
    void displayData();
}
```
##### 2\. **Real Subject**

This is the actual object that we want to control access to.

```java
public class SensitiveData implements Data {
    private String confidentialInfo;

    public SensitiveData(String confidentialInfo) {
        this.confidentialInfo = confidentialInfo;
    }

    @Override
    public void displayData() {
        System.out.println("Displaying Sensitive Data: " + confidentialInfo);
    }
}
```
##### 3\. **Proxy**

The proxy class controls access to the real object. It can check permissions before forwarding the request to the real object.
```java
public class DataProxy implements Data {
    private SensitiveData sensitiveData;
    private String userRole;

    public DataProxy(String confidentialInfo, String userRole) {
        this.sensitiveData = new SensitiveData(confidentialInfo);
        this.userRole = userRole;
    }

    @Override
    public void displayData() {
        if (userRole.equals("ADMIN")) {
            sensitiveData.displayData();
        } else {
            System.out.println("Access Denied: Insufficient Permissions");
        }
    }
}
```
##### 4\. **Client Code**

The client interacts with the proxy, which controls access to the real object.
```java
public class Client {
    public static void main(String[] args) {
        Data adminData = new DataProxy("Secret Admin Info", "ADMIN");
        Data userData = new DataProxy("Secret User Info", "USER");

        System.out.println("Admin Access:");
        adminData.displayData(); // Should display the data

        System.out.println("\nUser Access:");
        userData.displayData(); // Should deny access
    }
}
```

[⬆️ why we need proxy design pattern](#224-why-do-we-need-proxy-design-pattern)

### [2.2.5.2 Logging Example](#2252-more-examples-on-proxy-design-pattern)
Let's consider a banking system where we want to log every transaction made by a user. We'll use a proxy to log the details of each transaction before passing the request to the real bank account object.

### 1\. **Subject Interface**

Define an interface that both the real subject and the proxy will implement.

```java
public interface BankAccount {
    void deposit(double amount);
    void withdraw(double amount);
    double getBalance();
}
```
### 2\. **Real Subject**

This class represents the actual bank account.

```java
public class RealBankAccount implements BankAccount {
    private double balance;

    public RealBankAccount(double initialBalance) {
        this.balance = initialBalance;
    }

    @Override
    public void deposit(double amount) {
        balance += amount;
        System.out.println("Deposited: " + amount);
    }

    @Override
    public void withdraw(double amount) {
        if (amount <= balance) {
            balance -= amount;
            System.out.println("Withdrew: " + amount);
        } else {
            System.out.println("Insufficient funds for withdrawal of: " + amount);
        }
    }

    @Override
    public double getBalance() {
        return balance;
    }
}
```
### 3\. **Proxy**

The proxy class will add logging functionality by logging each method call and then delegating the actual work to the real bank account.

```java
import java.util.Date;

public class LoggingBankAccountProxy implements BankAccount {
    private RealBankAccount realAccount;

    public LoggingBankAccountProxy(double initialBalance) {
        this.realAccount = new RealBankAccount(initialBalance);
    }

    @Override
    public void deposit(double amount) {
        log("Deposit", amount);
        realAccount.deposit(amount);
    }

    @Override
    public void withdraw(double amount) {
        log("Withdraw", amount);
        realAccount.withdraw(amount);
    }

    @Override
    public double getBalance() {
        double balance = realAccount.getBalance();
        log("Get Balance", balance);
        return balance;
    }

    private void log(String operation, double amount) {
        System.out.println(new Date() + " - Logging: " + operation + " of " + amount);
    }
}
```
### 4\. **Client Code**

The client interacts with the proxy, which logs the operations and then delegates them to the real object.
```java
public class Client {
    public static void main(String[] args) {
        BankAccount account = new LoggingBankAccountProxy(1000.0);

        account.deposit(200.0);  // Log and deposit
        account.withdraw(150.0); // Log and withdraw
        double balance = account.getBalance(); // Log and get balance

        System.out.println("Final Balance: " + balance);
    }
}
```
### Output:

```java
Wed Aug 27 12:00:00 UTC 2024 - Logging: Deposit of 200.0
Deposited: 200.0
Wed Aug 27 12:00:01 UTC 2024 - Logging: Withdraw of 150.0
Withdrew: 150.0
Wed Aug 27 12:00:02 UTC 2024 - Logging: Get Balance of 1050.0
Final Balance: 1050.0

```

### 2.2.6 When to use Proxy Design Pattern?

- Deferred Object Creation:
- Access Control and Permissions:
- Resource Optimization:
- Remote Object Interaction:

### 2.2.7 When not to use Proxy Design Pattern?

- Overhead for Simple Operations:
- Unnecessary Abstraction:
- Performance Impact:
- When Access Control Isn’t Needed:
- When Eager Loading is Acceptable:

## 2.3 Strategy

[⬆️Back To Top](#table-of-contents)

A strategy pattern is a behavioral design pattern that allows the `behavior` of an object to be selected at `runtime`. It is one of the `Gang of Four (GoF)` design patterns, which are widely used in object-oriented programming. 


> Characteristics of the Strategy Design Pattern?

- It defines a family of algorithms:
  - The pattern allows you to encapsulate multiple algorithms or behaviors into separate classes, known as strategies.
- It encapsulates behaviors:
  - Each strategy encapsulates a specific behavior or algorithm, providing a clean and modular way to manage different variations or implementations.
- It enables dynamic behavior switching:
  - The pattern enables clients to switch between different strategies at runtime, allowing for flexible and dynamic behavior changes.
- It promotes object collaboration:
  - The pattern encourages collaboration between a context object and strategy objects, where the context delegates the execution of a behavior to a strategy object.

### 2.3.1 Components of the Strategy Design Pattern

1. **Context:** The Context is a class or object that holds a reference to a strategy object and delegates the task to it.
2. **Strategy Interface:** The Strategy Interface is an interface or abstract class that defines a set of methods that all concrete strategies must implement.
3. **Concrete Strtegies:** Concrete Strategies are the various implementations of the Strategy Interface. Each concrete strategy provides a specific algorithm or behavior for performing the task defined by the Strategy Interface.
4. **Client:** The Client is responsible for selecting and configuring the appropriate strategy and providing it to the Context.

### 2.3.2 Communication between the Components

In the Strategy Design Pattern, communication between the components occurs in a structured and decoupled manner. Here’s how the components interact with each other:

![Strategy Components](https://github.com/rds8rds/nsl_trainee_program/blob/main/images/solid%20and%20design%20pattern/proxy-generic.png?raw=true)


Communications between components: 
- Client to Context:
  - The Client, **which knows the requirements** of the task, **interacts with the Contex**t to initiate the task execution.
  - The Client **selects an appropriate strategy** based on the task requirements and provides it to the Context.
  - The Client **may configure** the selected strategy before passing it to the Context if necessary.
- Context to Strategy:
  - The Context **holds a reference** to the selected strategy and **delegates** the task to it.
  - The Context **invokes a method on the strategy object**, triggering the execution of the specific algorithm or behavior encapsulated within the strategy.
- Strategy to Context:
  - Once the strategy completes its execution, it may return **a result** or perform any necessary actions.
  - The strategy **communicates** the result or any relevant information **back to the Context**, which may further process or utilize the result as needed.
- Strategy Interface as Contract:
  - The **Strategy Interface serves as a contract** that defines a set of methods that **all concrete strategies** must implement.
  - The Context communicates with strategies through the common interface, promoting interchangeability and **decoupling**.
- Decoupled Communication:
  - Communication between the **components** is **decoupled**, *meaning that the Context does not need to know the specific details of how each strategy implements the task.*
  - Strategies can be **swapped** or **replaced** without impacting the client or other strategies, as long as they adhere to the common interface.

Overall, communication in the Strategy Design Pattern involves the Context class invoking a method on the selected strategy object, which triggers the execution of a specific algorithm or behavior to perform a task. This separation of task execution from the selection and configuration of the strategy promotes flexibility, modularity, and code reusability within the software system.

### 2.3.3 Real-World Analogy of Strategy Design Pattern

Imagine you’re planning a trip to a new city, and you have several options for getting there: by car, by train, or by plane. Each mode of transportation offers its own set of advantages and disadvantages, depending on factors such as cost, travel time, and convenience.

- Context
  You, as the traveler, represent the context in this analogy. You have a specific goal (reaching the new city) and need to choose the best transportation strategy to achieve it.
- Strategies
  The different modes of transportation (car, train, plane) represent the strategies in this analogy. Each strategy (mode of transportation) offers a different approach to reaching your destination.

- Interface
  - The interface in this analogy is the set of common criteria you consider when choosing a transportation mode, such as cost, travel time, and convenience.
  - These criteria serve as the common interface that all strategies must adhere to.
- Flexibility:
  - Just as the Strategy Design Pattern allows you to dynamically switch between different algorithms at runtime, you have the flexibility to choose a transportation mode based on your specific requirements and constraints.
  - For example, if you value speed and are willing to pay more, you might choose to fly.
  - If you prioritize cost-effectiveness and don’t mind a longer travel time, you might opt for a train or car.
- Dynamic Selection:
  - The Strategy Design Pattern allows you to dynamically select the best strategy (transportation mode) based on changing circumstances.
  - For instance, if your initial flight is canceled due to bad weather, you can quickly switch to an alternative mode of transportation, such as taking a train or renting a car, without having to change your overall travel plans drastically.

#### 2.3.3.1 Strategy Design Pattern Example

Let’s consider a sorting application where we need to sort a list of integers. However, the **sorting algorithm** to be used may vary depending on factors such as the **size of the list** and the **desired performance characteristics**.

> Challenges Without Using Strategy Pattern:

- Limited Flexibility:
  > mplementing sorting algorithms directly within the main sorting class can make the code inflexible. Adding new sorting algorithms or changing existing ones would require modifying the main class, which violates the Open/Closed Principle.
- Code Duplicatin
  > Without a clear structure, you may end up duplicating sorting logic to handle different algorithms. This can lead to maintenance issues and inconsistency in the system.
- Hard-Coded Logic
  > Implementing sorting logic directly within the main sorting class can make the code rigid and difficult to extend or modify. Making changes to the sorting algorithm becomes cumbersome and error-prone.

![Strategy example](https://github.com/rds8rds/nsl_trainee_program/blob/main/images/solid%20and%20design%20pattern/strategy-example.png?raw=true)

> How Strategy Pattern helps to solve above challenges :

The Strategy Design Pattern addresses these challenges by encapsulating each sorting algorithm into separate classes. This allows for better organization, code reuse, and flexibility in the system. Here’s how the Strategy Pattern helps:


Complete Code of the above example:

1. Context(SortingContext)

```java
public class SortingContext {
	private SortingStrategy sortingStrategy;

	public SortingContext(SortingStrategy sortingStrategy) {
		this.sortingStrategy = sortingStrategy;
	}

	public void setSortingStrategy(SortingStrategy sortingStrategy) {
		this.sortingStrategy = sortingStrategy;
	}

	public void performSort(int[] array) {
		sortingStrategy.sort(array);
	}
}
```

2. Strategy Interface(SortingStrategy)

```java
public interface SortingStrategy {
	void sort(int[] array);
}
```

3. Concrete Strategies

```java
// BubbleSortStrategy
public class BubbleSortStrategy implements SortingStrategy {
	@Override
	public void sort(int[] array) {
		// Implement Bubble Sort algorithm
		System.out.println("Sorting using Bubble Sort");
	}
}

// MergeSortStrategy
public class MergeSortStrategy implements SortingStrategy {
	@Override
	public void sort(int[] array) {
		// Implement Merge Sort algorithm
		System.out.println("Sorting using Merge Sort");
	}
}

// QuickSortStrategy
public class QuickSortStrategy implements SortingStrategy {
	@Override
	public void sort(int[] array) {
		// Implement Quick Sort algorithm
		System.out.println("Sorting using Quick Sort");
	}
}
```

4. Client Component

```java
public class Client {
	public static void main(String[] args) {
		// Create SortingContext with BubbleSortStrategy
		SortingContext sortingContext = new SortingContext(new BubbleSortStrategy());
		int[] array1 = {5, 2, 9, 1, 5};
		sortingContext.performSort(array1); // Output: Sorting using Bubble Sort

		// Change strategy to MergeSortStrategy
		sortingContext.setSortingStrategy(new MergeSortStrategy());
		int[] array2 = {8, 3, 7, 4, 2};
		sortingContext.performSort(array2); // Output: Sorting using Merge Sort

		// Change strategy to QuickSortStrategy
		sortingContext.setSortingStrategy(new QuickSortStrategy());
		int[] array3 = {6, 1, 3, 9, 5};
		sortingContext.performSort(array3); // Output: Sorting using Quick Sort
	}
}
```

<details>
<summary><span style="color: brown; font-weight: bold">Click to expand/collapse Complete code for the above example.</span></summary>

Below is the complete code for the above example:

```java
// SortingContext.java
class SortingContext {
	private SortingStrategy sortingStrategy;

	public SortingContext(SortingStrategy sortingStrategy) {
		this.sortingStrategy = sortingStrategy;
	}

	public void setSortingStrategy(SortingStrategy sortingStrategy) {
		this.sortingStrategy = sortingStrategy;
	}

	public void performSort(int[] array) {
		sortingStrategy.sort(array);
	}
}

// SortingStrategy.java
interface SortingStrategy {
	void sort(int[] array);
}

// BubbleSortStrategy.java
class BubbleSortStrategy implements SortingStrategy {
	@Override
	public void sort(int[] array) {
		// Implement Bubble Sort algorithm
		System.out.println("Sorting using Bubble Sort");
		// Actual Bubble Sort Logic here
	}
}

// MergeSortStrategy.java
class MergeSortStrategy implements SortingStrategy {
	@Override
	public void sort(int[] array) {
		// Implement Merge Sort algorithm
		System.out.println("Sorting using Merge Sort");
		// Actual Merge Sort Logic here
	}
}

// QuickSortStrategy.java
class QuickSortStrategy implements SortingStrategy {
	@Override
	public void sort(int[] array) {
		// Implement Quick Sort algorithm
		System.out.println("Sorting using Quick Sort");
		// Actual Quick Sort Logic here
	}
}

// Client.java
public class Client {
	public static void main(String[] args) {
		// Create SortingContext with BubbleSortStrategy
		SortingContext sortingContext = new SortingContext(new BubbleSortStrategy());
		int[] array1 = {5, 2, 9, 1, 5};
		sortingContext.performSort(array1); // Output: Sorting using Bubble Sort

		// Change strategy to MergeSortStrategy
		sortingContext.setSortingStrategy(new MergeSortStrategy());
		int[] array2 = {8, 3, 7, 4, 2};
		sortingContext.performSort(array2); // Output: Sorting using Merge Sort

		// Change strategy to QuickSortStrategy
		sortingContext.setSortingStrategy(new QuickSortStrategy());
		int[] array3 = {6, 1, 3, 9, 5};
		sortingContext.performSort(array3); // Output: Sorting using Quick Sort
	}
}
```

</details>

Output

```
Sorting using Bubble Sort
Sorting using Merge Sort
Sorting using Quick Sort
```
### 2.3.3 Advantages of the Strategy Design Pattern

Below are the advantages of the strategy design pattern:

- A family of algorithms can be defined as a class hierarchy and can be used interchangeably to alter application behavior without changing its architecture.
- By encapsulating the algorithm separately, new algorithms complying with the same interface can be easily introduced.
- The application can switch strategies at run-time.
- Strategy enables the clients to choose the required algorithm, **without using a “switch” statement or a series of “if-else”** statements.
- Data structures used for implementing the algorithm are completely encapsulated in Strategy classes. Therefore, the implementation of an algorithm can be changed without affecting the Context class.

### 2.3.4 When to use the Strategy Design Pattern?

Here are some situations where you should consider using the Strategy pattern:

- Multiple Algorithms:
  > When you have multiple algorithms that can be used interchangeably based on different contexts, such as sorting algorithms (bubble sort, merge sort, quick sort), searching algorithms, compression algorithms, etc.
- Encapsulating Algorithms:
  > When you want to encapsulate the implementation details of algorithms separately from the context that uses them, allowing for easier maintenance, testing, and modification of algorithms without affecting the client code.
- Runtime Selection:
  > When you need to dynamically select and switch between different algorithms at runtime based on user preferences, configuration settings, or system states.
- Reducing Conditional Statements:
  > When you have a class with multiple conditional statements that choose between different behaviors, using the Strategy pattern helps in eliminating the need for conditional statements and making the code more modular and maintainable.
- Testing and Extensibility:
  > When you want to facilitate easier unit testing by enabling the substitution of algorithms with mock objects or stubs. Additionally, the Strategy pattern makes it easier to extend the system with new algorithms without modifying existing code.

### 2.3.5 When not to use the Strategy Design Pattern?

Here are some situations where you should consider not using the Strategy pattern:

- Single Algorithm:
  If there is only one fixed algorithm that will be used throughout the lifetime of the application, and there is no need for dynamic selection or switching between algorithms, using the Strategy pattern might introduce unnecessary complexity.
- Overhead:
  If the overhead of implementing multiple strategies outweighs the benefits, especially in simple scenarios where direct implementation without the Strategy pattern is more straightforward and clear.
- Inflexible Context:
  If the context class tightly depends on a single algorithm and there is no need for flexibility or interchangeability, using the Strategy pattern may introduce unnecessary abstraction and complexity.



### 2.3.6 Disadvantages the Strategy Design Pattern

Below are the disadvantages of the strategy design pattern:

- The application must be aware of all the strategies to select the right one for the right situation.
- Context and the Strategy classes normally communicate through the interface specified by the abstract Strategy base class. Strategy base class must expose interface for all the required behaviours, which some concrete Strategy classes might not implement.
- In most cases, the application configures the Context with the required Strategy object. Therefore, the application needs to create and maintain two objects in place of one.

> Notes:

- And that’s exactly what the Proxy pattern does – ” Controls and manages access to the object they are protecting”.
- And that’s exactly what the Proxy pattern does – ” Controls and manages access to the object they are protecting”.

# 3. Referrances

[⬆️Back To Top](#table-of-contents)

- [Uncle Bob SOLID principle](https://www.youtube.com/watch?v=zHiWqnTWsn4&t=302s)
- [Head First Design Pattern](https://github.com/rds8rds/nsl_trainee_program/blob/main/books/%5BO%60Reilly.%20Head%20First%5D%20-%20Head%20First%20Design%20Patterns%20-%20%5BFreeman%5D-1.pdf)
