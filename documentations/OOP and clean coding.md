# Object Oriented programming

Object-Oriented Programming (OOP) is a programming paradigm where "objects" contain both data (attributes) and code (methods). It organizes code into modular units and promotes reuse through inheritance.

## 1. Class and Objects

### 1.1 Class

A class is a blueprint or prototype from which objects are created.
It defines the structure and behavior that the objects will have.

- **Components:**
  - **Attributes:** Define the properties or state of the class (e.g., brand, model, year).
  - **Methods:** Define the behaviors or actions that objects of the class can perform (e.g., startEngine()).

### 1.2 Object

- An object is an instance of a class.
- It represents a concrete entity with state and behavior.
- Memory is allocated for an object when it is instantiated from a class.
- Attributes and Methods:
  - Attributes: Store the current state or values of the object (e.g., myCar.brand, myCar.model).
  - Methods: Perform actions on the object's data or define the object’s behavior (e.g., myCar.startEngine()).

### Four Pillers of OOP

- Abstraction
- Encapsulation
- Inheritance
- Polymorphism

## 2. Abstraction

**Abstraction** is idea of hiding complex details of a class to its end user; A user might not need to know all the details of a class to use it; We can achieve this by using abstract class and interface some example:

**Focus:** Abstraction emphasizes "what" an object does rather than "how" it does it.

**Implementation:** There are two primary ways to achieve abstraction in Java:

- **Abstract Classes:** Classes that cannot be instantiated on their own and **may contain** abstract methods (methods without a body).

- **Interfaces:** Fully abstract types that can only contain abstract methods and final, static constants.

**Example:**

```java

// class based
abstract class User{

 protected String name;
 protected int age;

 abstract void createProblem();

}

class NoviceUser extends User{
 boolean isDumb = true;

    @Override
 void createProblem() {
  System.out.println("Novice always create unnecessary issues!");
 }

 public NoviceUser(String name, int age, boolean isDumb) {
  this.name = name;
  this.age = age;
  this.isDumb = isDumb;
 }
}

public class BasicOopConcepts {

 public static void main(String[] args) {
  // TODO Auto-generated method stub

  User sojib = new NoviceUser("Arafat Hossain Sojib", 25, true );
  sojib.createProblem();

 }

}
```

**Interface** based; Multiple inheritance support available;

```java
interface Animal {
    void makeSound();  // Abstract method
    void eat();        // Abstract method
}

class Dog implements Animal {
    @Override
    public void makeSound() {
        System.out.println("Woof");
    }

    @Override
    public void eat() {
        System.out.println("Dog is eating");
    }
}

public class Main {
    public static void main(String[] args) {
        Animal myDog = new Dog(); // Interface reference pointing to a Dog object
        myDog.makeSound();        // Output: Woof
        myDog.eat();              // Output: Dog is eating
    }
}


// inherit from multiple inheritance
interface Swimmable {
    void swim();
}

class Duck implements Animal, Swimmable {
    @Override
    public void makeSound() {
        System.out.println("Quack");
    }

    @Override
    public void eat() {
        System.out.println("Duck is eating");
    }

    @Override
    public void swim() {
        System.out.println("Duck is swimming");
    }
}

// we can reflect the results in main methods; like
/*
** Duck quak_quack = new Duck();
** quak_quack.makeSound(); --> outputs Quack
** quack_quack.swim(); --> Duck is swinmming;
*/

```

## 3. Encapsulation

The idea of encapsulting all the related things of a class to its scope.
It involves bundling the data (attributes) and methods (functions) into a single unit, typically a class. It restricts direct access to some of the object's components.

**Achieving Encapsulation in Java**

- **i. Declare Variables as Private**: Make the data members (variables) of the class private to restrict direct access from outside the class.

- **ii. Provide Public Getters and Setters**: Define public methods (getters and setters) to access and update the private variables. This allows controlled access to the data.

**Advantages of Encapsulation:**

- **Control Over Data:** You can add logic to setter methods to validate data before setting it, ensuring that only valid data is stored.

- **Data Hiding:** By making data members private, you hide the internal state of the object from the outside world, protecting it from unintended interference.

**Related Topic:** Class Composition, Class Aggregation

```java


class Guitarist{
	private String guitar_type, experience_days, mood; 
	private Boolean willPlayToday = false; 
	
	public Guitarist(String guitar_type, String experience_days, String mood) {
		this.guitar_type = guitar_type; 
		this.experience_days = experience_days;
		this.mood = mood; 
	}
	
	public void cheerUp() {
		willPlayToday = true; 
	}
	
	public void guitaristStatus() {
		System.out.println(this);
	}
	
	@Override
    public String toString() {
        return guitar_type + " " + experience_days + " "+willPlayToday;
    }
	
// main function

 public static void main(String[] args) {

  Guitarist mike = new Guitarist("calssical", "two years", "happy");
	mike.cheerUp(); 
	mike.guitaristStatus();

  // clearing the object;
  mike = null;
  System.gc();
 }

```

**Explanation:** Here the to access the Guitarist class attributes, we have to use a getter method and here that is guitaristStatus(); we can't get the info outside of using this very function() whick in concept wise totally in sync with the Encapsulation Idea;

### 3.1 Access Specifier

How the class variables and methods can be accessed from its instances, or from its child instances or outside of this class;

| Access Specifier        | Class | Package | Subclass | World |
| ----------------------- | ----- | ------- | -------- | ----- |
| `private`               | ✅    | ❌      | ❌       | ❌    |
| `default` (no modifier) | ✅    | ✅      | ❌       | ❌    |
| `protected`             | ✅    | ✅      | ✅       | ❌    |
| `public`                | ✅    | ✅      | ✅       | ✅    |

## 4. Inheritance

Sub class is alowed to inherit properties from its base class, [creating new sub class based on base class]

Why we need this : - code reusablity - Method overriding - Abstraction

**java doesn't support class based multiple inheritance, it supports multilevel inheritance;
** also doesn't support hybrid inheritance;

```java
// Parent class
class One {
    public void printGeek()
    {
        System.out.println("Geeks");
    }
}

class Two extends One {
    public void printFor() { System.out.println("for"); }
}

// Driver class
public class Main {
      // Main function
    public static void main(String[] args)
    {
        Two g = new Two();
        g.printGeek();
        g.printFor();
        g.printGeek();
    }
}

```

### 4.1 Interface based Inheritance

What is an Interface :

- It is a **referance** type [much like a String in java!]
- similar to class can contain **only constants and method signatures**[but not implementations]
- Only **exception** is for **static** and **default methods** (where implementations are allowed)
  - defualt methods are intorduced for backward compatiblity

```java
interface Animal{
	void sleep();
	
	default void bark() {
		System.out.println("animal Barks!");
	}
}

interface Mammal extends Animal{
	public Boolean isInteligent = true; 
}


class Dog implements Mammal{
 public void sleep() {
  System.out.println("A dog is sleeping!");
 }

 public Dog() {
  System.out.println("new dog is created");
 }

 public static void main(String args[]){
  Dog husky = new Dog();

  // we can call any Dog methods:
  husky.bark();
  System.out.println(henry.isInteligent);
 }
}

```

**Explanation:** Mammal interface inherits some features from Animal interface and then we implement Mammal inside Dog class; 

## 5. Polymorphism

The main idea behind polymorphism is that a single function or method can work in different ways depending on the object it is acting upon.

- Polymorphism
- Compiletime Polymorphism
  - Function Overloading
  - Operator Overloading (not present in java)
- Runtime Polymorphism
  - Function Overriding

### 5. 1 Functional overloading example: (compiletime polymorphism)

With method overloading, multiple methods can have the same name with different parameters:

```java
// functional overloading
class ComplexNumber{
 private double real, imaginary;

 public ComplexNumber(double real, double imaginary) {
  this.real = real;
  this.imaginary = imaginary;
 }

 // add real parts
 public int add(int x) {
  return (int)this.real + x;
 }
 // add two complex number
 public ComplexNumber add(ComplexNumber x) {
  return new ComplexNumber(this.real + x.real, this.imaginary + x.imaginary);
 }

 public void printComplex() {
  System.out.println(real + "i + "+imaginary+"j" );
 }

 public static void main(String[] args) {
  // TODO Auto-generated method stub
  ComplexNumber x = new ComplexNumber(5.3, 4), y = new ComplexNumber(2.3, 5);
  ComplexNumber res = x.add(y);
  System.out.println("check operator overloading: " + res.add(3));

  res.printComplex();
 }
}
```

### 5.2 Functional Overriding (Runtime polymorhism)

Each layer of inheritance allows us to override methods from the parent class to provide more specific behavior.

``` java
class Animal {
    void sound() {
        System.out.println("The animal makes a sound");
    }
}

class Dog extends Animal {
    @Override
    void sound() {
        System.out.println("The dog barks");
    }
}

class Labrador extends Dog {
    @Override
    void sound() {
        System.out.println("The Labrador barks loudly");
    }
}

public class Main {
    public static void main(String[] args) {
        Animal myAnimal = new Animal();      // Create an Animal object
        Animal myDog = new Dog();            // Create a Dog object (but refer to it as an Animal)
        Animal myLabrador = new Labrador();  // Create a Labrador object (but refer to it as an Animal)

        myAnimal.sound();   // Outputs: The animal makes a sound
        myDog.sound();      // Outputs: The dog barks
        myLabrador.sound(); // Outputs: The Labrador barks loudly
    }
}


```

**More  Example**
<details>
  <summary><span style="color: brown; font-weight: bold">Click to expand/collapse.</span></summary>

  ## Generic Java Example on Functional Overloading
In Java, method overriding is commonly used in collections, especially with classes like List and ArrayList. The List interface defines a set of methods that any list-type class must implement, and ArrayList is one of the most commonly used implementations of the List interface.

```java
public interface List<E> {
    boolean add(E e);
    E get(int index);
    E remove(int index);
    int size();
    // Other methods
}


public class ArrayList<E> implements List<E> {
    // Internal array to store elements
    private Object[] elementData;

    @Override
    public boolean add(E e) {
        // Implementation for adding an element to the list
    }

    @Override
    public E get(int index) {
        // Implementation for getting an element at a specific index
    }

    @Override
    public E remove(int index) {
        // Implementation for removing an element at a specific index
    }

    @Override
    public int size() {
        // Implementation for getting the size of the list
    }

    // Other methods and additional functionality
}


import java.util.List;
import java.util.ArrayList;

public class Main {
    public static void main(String[] args) {
        // Using List as the reference type
        List<Integer> numbers = new ArrayList<>();

        // Adding elements (overrides List's add method)
        numbers.add(10);
        numbers.add(20);
        numbers.add(30);

        // Accessing elements (overrides List's get method)
        System.out.println("Element at index 1: " + numbers.get(1));

        // Removing an element (overrides List's remove method)
        numbers.remove(1);

        // Checking size (overrides List's size method)
        System.out.println("Size after removal: " + numbers.size());

        // Printing the final list
        System.out.println("Final List: " + numbers);
    }
}


```

</details>



## 6. Class Relations

Class Relationships: In object-oriented programming (OOP), classes can have various types of relationships that define how they interact with each other. Understanding these relationships is crucial for designing systems that are maintainable, scalable, and intuitive. Here are the key types of relationships among classes:

Class Relationships:

- Inheritance (Is - a)
- Association (Has - A)
  - Aggregation [ Weak Has - A ]
  - Compostition [ Strong Has - A ]
- Dependency - Realization

### 6.1 Inheritance (Is-A Relationship)

Inheritance is a relationship where one class (the subclass or derived class) inherits the properties and behaviors (fields and methods) of another class (the superclass or base class). This is often described as an "is-a" relationship.

Example:
Dog is a subclass of Animal.
Dog "is-a" Animal.

```java
class Animal {
    void eat() {
        System.out.println("This animal eats.");
    }
}

class Dog extends Animal {
    void bark() {
        System.out.println("The dog barks.");
    }
}

public class Main {
    public static void main(String[] args) {
        Dog dog = new Dog();
        dog.eat();  // Inherited from Animal
        dog.bark(); // Defined in Dog
    }
}

```

### 6.2 Association (Has-A Relationship)

Association is a relationship where one class uses or is associated with another class. This can be further broken down into aggregation and composition.

#### 6.2.1 Aggregation (Weak Has-A Relationship)

Aggregation is a form of association where one class contains a reference to another class, but the contained object can exist independently of the container.

Example:
**Library** has **Books**.
**Books** can exist without the **Library**.

```java
class Book {
    private String title;

    public Book(String title) {
        this.title = title;
    }

    public String getTitle() {
        return title;
    }
}

class Library {
    private List<Book> books;

    public Library(List<Book> books) {
        this.books = books;
    }

    public void displayBooks() {
        for (Book book : books) {
            System.out.println(book.getTitle());
        }
    }
}

```

#### 6.2.2 Composition (Strong Has-A Relationship)

Composition is a form of association where one class is composed of other classes. The composed objects cannot exist independently of the container.

Example:
Car has an Engine.
Engine cannot exist without the Car.

```java
class Engine {
    private String type;

    public Engine(String type) {
        this.type = type;
    }

    public String getType() {
        return type;
    }
}

class Car {
    private Engine engine;

    public Car(String engineType) {
        this.engine = new Engine(engineType);
    }

    public void start() {
        System.out.println("Car with " + engine.getType() + " engine is starting.");
    }
}

```

### 6.3. Dependency (Uses-A Relationship)

Dependency is a relationship where one class depends on another class. This relationship is often described as a "uses-a" relationship. The dependent class needs the other class to function, typically by calling its methods or using its data.

Example:
Driver uses Car.
Driver "uses-a" Car to drive.

```java
class Car {
    public void drive() {
        System.out.println("Car is being driven.");
    }
}

class Driver {
    public void driveCar(Car car) {
        car.drive();
    }
}

```

### 6.4. Realization (Implements Relationship)

```java
interface Flyable {
    void fly();
}

class Bird implements Flyable {
    public void fly() {
        System.out.println("Bird is flying.");
    }
}

```

### 6.5. Generalization

Generalization is a relationship where a general concept or class is defined, and other classes inherit from this general class. This is closely related to inheritance but focuses on the abstraction aspect, where the superclass is a generalized form of the subclasses.

Example:
Vehicle is a general class.
Car, Bike, and Truck are specific forms of Vehicle.

```java
class Vehicle {
    void move() {
        System.out.println("Vehicle is moving.");
    }
}

class Car extends Vehicle {
    void drive() {
        System.out.println("Car is driving.");
    }
}

class Bike extends Vehicle {
    void pedal() {
        System.out.println("Bike is pedaling.");
    }
}

```

#### Summary of Relationships

- **Inheritance (Is-A):** A subclass inherits from a superclass.
- **Association (Has-A):** A class is associated with another class.
- **Aggregation:** The associated object can exist independently.
- **Composition:** The associated object cannot exist independently.
- **Dependency (Uses-A):** A class uses another class to perform its functions.
- **Realization (Implements):** A class implements an interface.
- **Generalization:** A general concept or class is inherited by more specific

### Why Association is preferred over Aggregation ?

1. **Flexibility**:

- Inheritance: When you use inheritance, you're creating a tightly coupled relationship between a superclass and a subclass. The subclass inherits the implementation of the superclass, which can lead to rigid structures where changes to the superclass may have unintended consequences on all subclasses.
- Association: Association, on the other hand, allows one class to use another class without establishing a rigid hierarchy. This relationship is more flexible, as it allows you to compose objects in various ways without enforcing a strict "is-a" relationship.

2. **Maintainability**:

- Inheritance: Changes in a superclass can impact all subclasses, which can lead to more maintenance overhead. In a large or complex hierarchy, this can make the system more difficult to understand and modify.
- Association: Because association implies a "has-a" relationship rather than an "is-a" relationship, it's easier to modify or replace components without affecting the entire system. This makes the codebase more maintainable and adaptable to change.

3. **Avoiding Hierarchical Complexity**:

- Inheritance: Overusing inheritance can lead to deep inheritance hierarchies, which can be hard to manage and understand. This can also lead to issues like the "fragile base class" problem, where changes to a base class can inadvertently break subclasses.
- Association: Association avoids these issues by promoting composition over inheritance. By associating classes, you can create complex behaviors by combining simpler, well-defined components. This promotes a more modular and understandable design.

4. **Reusability**:

- Inheritance: Code reuse through inheritance is limited to a single hierarchy. If you need to reuse functionality across different hierarchies, you might end up with code duplication or forced, unnatural hierarchies.
- Association: Through association and composition, you can reuse components across different contexts without being bound by an inheritance structure. This enhances code reusability and can reduce duplication.

5. **Liskov Substitution Principle (LSP)**:

- Inheritance: If not carefully designed, inheritance can violate the Liskov Substitution Principle, which states that objects of a superclass should be replaceable with objects of a subclass without affecting the correctness of the program. Violating this principle can lead to bugs and unexpected behavior.
- Association: Association encourages using objects in a way that doesn’t tightly couple them to a specific hierarchy, which makes it easier to adhere to LSP.

6. **Favor Composition Over Inheritance**:

- This is a common design principle that encourages developers to use association (composition/aggregation) to combine behaviors rather than relying on inheritance. This leads to more flexible and dynamic designs.


**Example:** Imagine you are designing a system for a library. You have classes for Book and Library.

**Using Inheritance:**
If you use inheritance, you might create a structure like this:

```
class LibraryBook extends Book {
    private Library library;

    // Other attributes and methods
}

```
In this case, LibraryBook is a Book and also directly inherits from it. This can be problematic because LibraryBook now inherits all characteristics of Book, even those that might not be relevant to a library context. It also creates a strong dependency on the Book class.

**Using Association:** Instead, using association, you can design it like this:

```java
class Book {
    private String title;
    private String author;

    // Constructor, getters, setters
}

class Library {
    private List<Book> books;

    public void addBook(Book book) {
        books.add(book);
    }

    // Other attributes and methods
}

```

```java 
import java.util.ArrayList;
import java.util.List;

// Book class
class Book {
    private String title;
    private String author;

    public Book(String title, String author) {
        this.title = title;
        this.author = author;
    }

    // Getters and setters
    public String getTitle() { return title; }
    public String getAuthor() { return author; }
}

// Library class
class Library {
    private List<Book> books = new ArrayList<>();

    public void addBook(Book book) {
        books.add(book);
    }

    public void listBooks() {
        for (Book book : books) {
            System.out.println(book.getTitle() + " by " + book.getAuthor());
        }
    }
}

// Main class to test association
public class Main {
    public static void main(String[] args) {
        Library myLibrary = new Library();
        Book book1 = new Book("1984", "George Orwell");
        Book book2 = new Book("To Kill a Mockingbird", "Harper Lee");

        myLibrary.addBook(book1);
        myLibrary.addBook(book2);

        myLibrary.listBooks();
    }
}


```

## Clean Coding

### Clean Code Notes

### Table of contents

- [Chapter 1 - Clean Code](#chapter1)
- [Chapter 2 - Meaningful Names](#chapter2)
- [Chapter 3 - Functions](#chapter3)
- [Chapter 4 - Comments](#chapter4)

<a name="chapter1">
<h1>Chapter 1 -  Clean Code</h1>
</a>
This Book is about good programming. It's about how to write good code, and how to transform bad code into good code.

The code represents the detail of the requirements and the details cannot be ignored or abstracted. We may create languages that are closer to the requirements. We can create tools that help us parse and assemble those requirements into formal structures. But we will never eliminate necessary precision.

### Why write bad code?

- Are you in a rush?
- Do you try to go "fast"?
- Do not you have time to do a good job?
- Are you tired of work in the same program/module?
- Does your Boss push you to finish soon?

The previous arguments could create a swamp of senseless code.

If you say "I will back to fix it later" you could fall in the [LeBlanc's law](https://en.wikipedia.org/wiki/Talk%3AList_of_eponymous_laws#Proposal_to_add_LeBlanc.27s_law) "Later equals never"

You are a professional and the code is your responsibility. Let's analyze the following anecdote:

> What if you were a doctor and had a patient who demanded that you stop all the silly hand-washing in preparation for surgery because it was taking too much time? Clearly the patient is the boss; and yet the doctor should absolutely refuse to comply. Why? Because the doctor knows more than the patient about the risks of disease and infection. It would be unprofessional (never mind criminal) for the doctor to comply with the patient.

So too it is unprofessional for programmers to bend to the will of managers who don’t understand the risks of making messes.

Maybe sometime you think in go fast to make the deadline. The only way to go fast is to keep the code as clean as possible at all times.

### What is Clean Code?

Each experienced programmer has his/her own definition of clean code, but something is clear, a clean code is a code that you can read easily. The clean code is code that has been taken care of.

In his book Uncle Bob says the next:

> Consider this book a description of the Object Mentor School of Clean Code. The techniques and teachings within are the way that we practice our art. We are willing to claim that if you follow these teachings, you will enjoy the benefits that we have enjoyed, and you will learn to write code that is clean and professional. But don’t make the mistake of thinking that we are somehow “right” in any absolute sense. There are other schools and other masters that have just as much claim to professionalism as we. It would behoove you to learn from them as well.

### The boy Scout Rule

It’s not enough to write the code well. The code has to be kept clean over time. We have all seen code rot and degrade as time passes. So we must take an active role in preventing this degradation.

It's a good practice apply the [Boy Scout Rule](http://programmer.97things.oreilly.com/wiki/index.php/The_Boy_Scout_Rule)

> Always leave the campground cleaner than you found it.

<a name="chapter2">
<h1>Chapter 2 -  Meaningful Names</h1>
</a>

Names are everywhere in software. Files, directories, variables functions, etc. Because we do so much of it. We have better do it well.

### Use Intention-Revealing Names

It is easy to say that names reveal intent. Choosing good names takes time, but saves more than it takes. So take care with your names and change them when you find better ones.

The name of a variable, function or class, should answer all the big questions. It should tell you why it exists, what it does, and how is used. **If a name requires a comment, then the name does not reveals its intent**.

| Does not reveals intention       | Reveals intention       |
| -------------------------------- | ----------------------- |
| `int d; // elapsed time in days` | `int elapsedTimeInDays` |

Choosing names that reveal intent can make much easier to understand and change code. Example:

```java
public List<int[]> getThem() {
  List<int[]> list1 = new ArrayList<int[]>();
  for (int[] x : theList)
    if (x[0] == 4)
      list1.add(x);
  return list1;
}
```

This code is simple, but create many questions:

1. What is the content of `theList`?
2. What is the significance of the item `x[0]` in the list?.
3. Why we compare `x[0]` vs `4`?
4. How would i use the returned list?

The answers to these questions are not present in the code sample, but they could have been. Say that we’re working in a mine sweeper game. We can refactor the previous code as follows:

```java
public List<int[]> getFlaggedCells() {
  List<int[]> flaggedCells = new ArrayList<int[]>();
  for (int[] cell : gameBoard)
    if (cell[STATUS_VALUE] == FLAGGED)
      flaggedCells.add(cell);
  return flaggedCells;
}
```

Now we know the next information:

1. `theList` represents the `gameBoard`
2. `x[0]` represents a cell in the board and `4` represents a flagged cell
3. The returned list represents the `flaggedCells`

Notice that the simplicity of the code has not changed. It still has exactly the same number of operators and constants, with exactly the same number of nesting levels. But the code has become much more explicit.

We can improve the code writing a simple class for cells instead of using an array of `ints`. It can include an **intention-revealing function** (called it `isFlagged`) to hide the magic numbers. It results in a new function of the function.

```java
public List<Cell> getFlaggedCells() {
  List<Cell> flaggedCells = new ArrayList<Cell>();
  for (Cell cell : gameBoard)
    if (cell.isFlagged())
      flaggedCells.add(cell);
  return flaggedCells;
}
```

### Avoid Disinformation

Programmers must avoid leaving false clues that obscure the meaning of code. We should avoid words whose entrenched meaning vary from our intended meaning.

Do not refer to a grouping of accounts as an `accountList` unless it's actually a `List`. The word `List` means something specific to programmers. If the container holding the accounts is not actually a List, it may lead to false conclusions. So `accountGroup` or `bunchOfAccounts` or just plain `accounts` would be better.

Beware of using names which vary in small ways. How long does it take to spot the subtle difference between a `XYZControllerForEfficientHandlingOfStrings` in one module and, somewhere a little more distant, `XYZControllerForEfficientStorageOfStrings`? The words have frightfully similar shapes

### Make Meaningful Distinctions

Programmers create problems for themselves when they write code solely to satisfy a compiler or interpreter. For example because you can't use the same name to refer two different things in the same scope, you might be tempted to change one name in an arbitrary way. Sometimes this is done by misspelling one, leading to the surprising situation where correcting spelling errors leads to an inability to compile. Example, you create the variable `klass`because the name `class` was used for something else.

In the next function, the arguments are noninformative, `a1` and `a2` doesn't provide clues to the author intention.

```java
public static void copyChars(char a1[], char a2[]) {
  for (int i = 0; i < a1.length; i++) {
    a2[i] = a1[i];
  }
}
```

We can improve the code selecting more explicit argument names:

```java
public static void copyChars(char source[], char destination[]) {
  for (int i = 0; i < source.length; i++) {
    destination[i] = source[i];
  }
}
```

Noise words are another meaningless distinction. Imagine that you have a Product class. If you have another called `ProductInfo` or `ProductData`, you have made the names different without making them mean anything different. Info and Data are indistinct noise words like a, an, and the.

Noise words are redundant. The word variable should never appear in a variable name. The word table should never appear in a table name.

### Use Pronounceable Names

Imagine you have the variable `genymdhms` (Generation date, year, month, day, hour, minute and second) and imagine a conversation where you need talk about this variable calling it "gen why emm dee aich emm ess". You can consider convert a class like this:

```java
class DtaRcrd102 {
  private Date genymdhms;
  private Date modymdhms;
  private final String pszqint = "102";
  /* ... */
};
```

To

```java
class Customer {
  private Date generationTimestamp;
  private Date modificationTimestamp;;
  private final String recordId = "102";
  /* ... */
};
```

### Use Searchable Names

Single-letter names and numeric constants have a particular problem in that they are not easy to locate across a body of text.

### Avoid Encoding

We have enough encodings to deal with without adding more to our burden. Encoding type or scope information into names simply adds an extra burden of deciphering. Encoded names are seldom pronounceable and are easy to mis-type. An example of this, is the use of the [Hungarian Notation](https://en.wikipedia.org/wiki/Hungarian_notation) or the use of member prefixes.

#### Interfaces and Implementations

These are sometimes a special case for encodings. For example, say you are building an ABSTRACT FACTORY for the creation of shapes. This factory will be an interface and will be implemented by a concrete class. What should you name them? `IShapeFactory` and `ShapeFactory`? Is preferable to leave interfaces unadorned.I don’t want my users knowing that I’m handing them an interface. I just want them to know that it’s a `ShapeFactory`. So if I must encode either the interface or the implementation, I choose the implementation. Calling it `ShapeFactoryImp`, or even the hideous `CShapeFactory`, is preferable to encoding the interface.

### Avoid Mental Mapping

Readers shouldn't have to mentally translate your names into other names they already know.

One difference between a smart programmer and a professional programmer is that the professional understands that clarity is king. Professionals use their powers for good and write code that others can understand.

### Class Names

Classes and objects should have noun or noun phrase names like `Customer`, `WikiPage`, `Account`, and `AddressParser`. Avoid words like `Manager`,`Processor`, `Data`, or `Info` in the name of a class. A class name should not be a verb.

### Method Names

Methods should have verb or verb phrase names like `postPayment`, `deletePage` or `save`. Accessors, mutators, and predicates should be named for their value and prefixed with get, set, and is according to the javabean standard.

When constructors are overloaded, use static factory methods with names that describe the arguments. For example:

```java
Complex fulcrumPoint = Complex.FromRealNumber(23.0);
```

Is generally better than

```java
Complex fulcrumPoint = new Complex(23.0);
```

Consider enforcing their use by making the corresponding constructors private.

### Don't Be Cute

| Cute name         | Clean name    |
| ----------------- | ------------- |
| `holyHandGranade` | `deleteItems` |
| `whack`           | `kill`        |
| `eatMyShorts`     | `abort`       |

### Pick one word per concept

Pick one word for one abstract concept and stick with it. For instance, it’s confusing to have fetch, retrieve, and get as equivalent methods of different classes.

### Don’t Pun

Avoid using the same word for two purposes. Using the same term for two different ideas is essentially a pun.

Example: in a class use `add` for create a new value by adding or concatenating two existing values and in another class use `add` for put a simple parameter in a collection, it's a better options use a name like `insert` or `append` instead.

### Use Solution Domain Names

Remember that the people who read your code will be programmers. So go ahead and use computer science (CS) terms, algorithm names, pattern names, math terms, and so forth.

### Use Problem Domain Names

When there is no “programmer-eese” for what you’re doing, use the name from the problem domain. At least the programmer who maintains your code can ask a domain expert what it means.

### Add Meaningful context

There are a few names which are meaningful in and of themselves—most are not. Instead, you need to place names in context for your reader by enclosing them in well-named classes, functions, or namespaces. When all else fails, then prefixing the name may be necessary as a last resort

Variables like: `firstName`, `lastName`, `street`, `city`, `state`. Taken together it's pretty clear that they form an address, but, what if you saw the variable state being used alone in a method?, you could add context using prefixes like: `addrState` at least readers will understand that the variable is part of a large structure. Of course, a better solution is to create a class named `Address` then even the compiler knows that the variables belong to a bigger concept

### Don’t Add Gratuitous Context

In an imaginary application called “Gas Station Deluxe,” it is a bad idea to prefix every class with GSD. Example: `GSDAccountAddress`

Shorter names are generally better than longer ones, so long as they are clear. Add no more context to a name than is necessary.

<a name="chapter3">
<h1>Chapter 3 -  Functions</h1>
</a>

Functions are the first line of organization in any topic.

### Small

The first rule of functions is that they should be small. The second rule of functions is that they should be smaller than that.

#### Blocks and Indenting

This implies that the blocks within `if` statements, `else` statements, `while` statements, and so on should be one line long. Probably that line should be a function call. Not only does this keep the enclosing function small, but also adds documentary value because the function called within the block can have a nicely descriptive name.

This also implies that functions should not be large enough to hold nested structures. Therefore, the indent level of a function should not be greater than one or two. This, of course, makes the functions easy to read and understand.

### Do One Thing

**FUNCTIONS SHOULD DO ONE THING. THEY SHOULD DO IT WELL. THEY SHOULD DO IT ONLY.**

#### Sections within Functions

If you have a function divided in sections like _declarations_, _initialization_ etc, it's a obvious symptom of the function is doing more than one thing. Functions that do one thing cannot be reasonably divided into sections.

### One Level of Abstraction per Function

In order to make sure our functions are doing "one thing", we need to make sure that the statements within our function are all at the same level of abstraction.

#### Reading Code from Top to Bottom: _The Stepdown Rule_

We want the code to read like a top-down narrative. 5 We want every function to be followed by those at the next level of abstraction so that we can read the program, descending one level of abstraction at a time as we read down the list of functions.

To say this differently, we want to be able to read the program as though it were a set
of TO paragraphs, each of which is describing the current level of abstraction and referencing subsequent TO paragraphs at the next level down.

```
- To include the setups and teardowns, we include setups, then we include the test page content, and then we include the teardowns.
- To include the setups, we include the suite setup if this is a suite, then we include the regular setup.
- To include the suite setup, we search the parent hierarchy for the “SuiteSetUp” page and add an include statement with the path of that page.
- To search the parent...
```

It turns out to be very difficult for programmers to learn to follow this rule and write functions that stay at a single level of abstraction. But learning this trick is also very important. It is the key to keeping functions short and making sure they do “one thing.” Making the code read like a top-down set of TO paragraphs is an effective technique for keeping the abstraction level consistent.

### Switch Statements

It’s hard to make a small switch statement. 6 Even a switch statement with only two cases is larger than I’d like a single block or function to be. It’s also hard to make a switch statement that does one thing. By their nature, switch statements always do N things. Unfortunately we can’t always avoid switch statements, but we can make sure that each switch statement is buried in a low-level class and is never repeated. We do this, of course, with polymorphism.

### Use Descriptive Names

> You know you are working on clean code when each routine turns out to be pretty much what you expected

Half the battle to achieving that principle is choosing good names for small functions that do one thing. The smaller and more focused a function is, the easier it is to choose a descriptive name.

Don’t be afraid to make a name long. A long descriptive name is better than a short enigmatic name. A long descriptive name is better than a long descriptive comment. Use a naming convention that allows multiple words to be easily read in the function names, and then make use of those multiple words to give the function a name that says what it does.

Choosing descriptive names will clarify the design of the module in your mind and help you to improve it. It is not at all uncommon that hunting for a good name results in a favorable restructuring of the code.

### Function arguments

The ideal number of arguments for a function is zero (niladic). Next comes one (monadic), followed closely by two (dyadic). Three arguments (triadic) should be avoided where possible. More than three (polyadic) requires very special justification—and then shouldn’t be used anyway.

Arguments are even harder from a testing point of view. Imagine the difficulty of writing all the test cases to ensure that all the various combinations of arguments work properly. If there are no arguments, this is trivial. If there’s one argument, it’s not too hard. With two arguments the problem gets a bit more challenging. With more than two arguments, testing every combination of appropriate values can be daunting.

Output arguments are harder to understand than input arguments. When we read a function, we are used to the idea of information going in to the function through arguments and out through the return value. We don’t usually expect information to be going out through the arguments. So output arguments often cause us to do a double-take.

#### Common Monadic Forms

There are two very common reasons to pass a single argument into a function. You may be asking a question about that argument, as in `boolean fileExists(“MyFile”)` . Or you may be operating on that argument, transforming it into something else and returning it. For example, `InputStream fileOpen(“MyFile”)` transforms a file name `String` into an `InputStream` return value. These two uses are what readers expect when they see a function. You should choose names that make the distinction clear, and always use the two forms in a consistent context.

#### Flag Arguments

Flag arguments are ugly. Passing a boolean into a function is a truly terrible practice. It immediately complicates the signature of the method, loudly proclaiming that this function does more than one thing. It does one thing if the flag is `true` and another if the flag is `false`!

#### Dyadic Functions

A function with two arguments is harder to understand than a monadic function. For example, `writeField(name)` is easier to understand than `writeField(output-Stream, name)`

There are times, of course, where two arguments are appropriate. For example, `Point p = new Point(0,0);` is perfectly reasonable. Cartesian points naturally take two arguments.

Even obvious dyadic functions like assertEquals(expected, actual) are problematic. How many times have you put the actual where the expected should be? The two arguments have no natural ordering. The expected, actual ordering is a convention that requires practice to learn.

Dyads aren’t evil, and you will certainly have to write them. However, you should be aware that they come at a cost and should take advantage of what mechanims may be available to you to convert them into monads. For example, you might make the writeField method a member of outputStream so that you can say outputStream. writeField(name) . Or you might make the outputStream a member variable of the current class so that you don’t have to pass it. Or you might extract a new class like FieldWriter that takes the outputStream in its constructor and has a write method.

#### Triads

Functions that take three arguments are significantly harder to understand than dyads. The issues of ordering, pausing, and ignoring are more than doubled. I suggest you think very carefully before creating a triad.

#### Argument Objects

Compare:

```java
Circle makeCircle(double x, double y, double radius);
```

vs

```java
Circle makeCircle(Point center, double radius);
```

#### Verbs and Keywords

Choosing good names for a function can go a long way toward explaining the intent of the function and the order and intent of the arguments. In the case of a monad, the function and argument should form a very nice verb/noun pair. For example, `write(name)` is very evocative. Whatever this “name” thing is, it is being “written.” An even better name might be `writeField(name)` , which tells us that the "name" thing is a "field".

This last is an example of the keyword form of a function name. Using this form we encode the names of the arguments into the function name. For example, `assertEquals` might be better written as `assertExpectedEqualsActual(expected, actual)`. This strongly mitigates the problem of having to remember the ordering of the arguments.

### Output Arguments

In general output arguments should be avoided. If your function must change the state of something, have it change the state of its owning object.

### Command Query Separation

Functions should either do something or answer something, but not both. Either your function should change the state of an object, or it should return some information about that object. Doing both often leads to confusion.

### Prefer Exceptions to Returning Error Codes

Returning error codes from command functions is a subtle violation of command query separation.

### Don't Repeat Yourself

Duplication may be the root of all evil in software. Many principles and practices have been created for the purpose of controlling or eliminating it.

### Structured Programming

Some programmers follow Edsger Dijkstra’s rules of structured programming. Dijkstra said that every function, and every block within a function, should have one entry and one exit. Following these rules means that there should only be one return statement in a function, no `break` or `continue` statements in a loop, and never, _ever_, any `goto` statements.

While we are sympathetic to the goals and disciplines of structured programming, those rules serve little benefit when functions are very small. It is only in larger functions that such rules provide significant benefit.

So if you keep your functions small, then the occasional multiple `return` , `break` , or `continue` statement does no harm and can sometimes even be more expressive than the single-entry, single-exit rule. On the other hand, `goto` only makes sense in large functions, so it should be avoided

<a name="chapter4">
<h1>Chapter 4 -  Comments</h1>
</a>

Nothing can be quite so helpful as a well-placed comment. Nothing can clutter up a module more than frivolous dogmatic comments. Nothing can be quite so damaging as an old comment that propagates lies and misinformation.

If our programming languages were expressive enough, or if we had the talent to subtly wield those languages to express our intent, we would not need comments very much—perhaps not at all.

### Comments Do Not Make Up for Bad Code

Clear and expressive code with few comments is far superior to cluttered and complex code with lots of comments. Rather than spend your time writing the comments that explain the mess you’ve made, spend it cleaning that mess.

### Explain Yourself in Code

```java
// Check to see if the employee is eligible for full benefits
if ((employee.flags & HOURLY_FLAG) && (employee.age > 65))
```

vs

```java
if (employee.isEligibleForFullBenefits())
```

### Good Comments

Some comments are necessary or beneficial. However the only truly good comment is the comment you found a way not to write.

#### Legal Comments

Sometimes our corporate coding standards force us to write certain comments for legal reasons. For example, copyright and authorship statements are necessary and reasonable things to put into a comment at the start of each source file.

#### Informative Comments

It is sometimes useful to provide basic information with a comment. For example, consider this comment that explains the return value of an abstract method:

```java
// Returns an instance of the Responder being tested.
protected abstract Responder responderInstance();
```

A comment like this can sometimes be useful, but it is better to use the name of the function to convey the information where possible. For example, in this case the comment could be made redundant by renaming the function: `responderBeingTested`.

#### Explanation of Intent

Sometimes a comment goes beyond just useful information about the implementation and provides the intent behind a decision. Example:

```java
public int compareTo(Object o)
{
  if(o instanceof WikiPagePath)
  {
    WikiPagePath p = (WikiPagePath) o;
    String compressedName = StringUtil.join(names, "");
    String compressedArgumentName = StringUtil.join(p.names, "");
    return compressedName.compareTo(compressedArgumentName);
  }
  return 1; // we are greater because we are the right type.
}
```

#### Clarification

Sometimes it is just helpful to translate the meaning of some obscure argument or return value into something that's readable. In general it is better to find a way to make that argument or return value clear in its own right; but when its part of the standard library, or in code that you cannot alter, then a helpful clarifying comment can be useful.

#### Warning of concequences

Sometimes it is useful to warn other programmers about certain consequences.

```java
// Don't run unless you
// have some time to kill.
public void _testWithReallyBigFile() {
  writeLinesToFile(10000000);
  response.setBody(testFile);
  response.readyToSend(this);
  String responseString = output.toString();
  assertSubString("Content-Length: 1000000000", responseString);
  assertTrue(bytesSent > 1000000000);
}
```

#### TODO Comments

It is sometimes reasonable to leave “To do” notes in the form of //TODO comments. In the
following case, the TODO comment explains why the function has a degenerate implementation and what that function's future should be.

```java
//TODO-MdM these are not needed
// We expect this to go away when we do the checkout model
protected VersionInfo makeVersion() throws Exception {
  return null;
}
```

TODOs are jobs that the programmer thinks should be done, but for some reason can’t do at the moment. It might be a reminder to delete a deprecated feature or a plea for someone else to look at a problem. It might be a request for someone else to think of a better name or a reminder to make a change that is dependent on a planned event. Whatever else a TODO might be, it is not an excuse to leave bad code in the system.

#### Amplification

A comment may be used to amplify the importance of something that may otherwise seem inconsequential.

```java
String listItemContent = match.group(3).trim();
// the trim is real important. It removes the starting
// spaces that could cause the item to be recognized
// as another list.
new ListItemWidget(this, listItemContent, this.level + 1);
return buildList(text.substring(match.end()));
```

#### Javadocs in Public APIs

There is nothing quite so helpful and satisfying as a well-described public API. The javadocs for the standard Java library are a case in point. It would be difficult, at best, to write Java programs without them.

### Bad Comments

Most comments fall into this category. Usually they are crutches or excuses for poor code or justifications for insufficient decisions, amounting to little more than the programmer talking to himself.

#### Mumbling

Plopping in a comment just because you feel you should or because the process requires it, is a hack. If you decide to write a comment, then spend the time necessary to make sure it is the best comment you can write. Example:

```java
public void loadProperties() {

  try {
    String propertiesPath = propertiesLocation + "/" + PROPERTIES_FILE;
    FileInputStream propertiesStream = new FileInputStream(propertiesPath);
    loadedProperties.load(propertiesStream);
  }
  catch(IOException e) {
    // No properties files means all defaults are loaded
  }
}
```

What does that comment in the catch block mean? Clearly meant something to the author, but the meaning not come though all that well. Apparently, if we get an `IOException`, it means that there was no properties file; and in that case all the defaults are loaded. But who loads all the defaults?

#### Redundant Comments

```java
// Utility method that returns when this.closed is true. Throws an exception
// if the timeout is reached.
public synchronized void waitForClose(final long timeoutMillis) throws Exception {
  if(!closed) {
    wait(timeoutMillis);
    if(!closed)
      throw new Exception("MockResponseSender could not be closed");
  }
}
```

What purpose does this comment serve? It’s certainly not more informative than the code. It does not justify the code, or provide intent or rationale. It is not easier to read than the code. Indeed, it is less precise than the code and entices the reader to accept that lack of precision in lieu of true understanding.

#### Misleading comments

Sometimes, with all the best intentions, a programmer makes a statement in his comments that isn't precise enough to be accurate. Consider for another moment the example of the previous section. The method does not return when `this.closed` becomes `true`. It returns if `this.closed` is `true`; otherwise, it waits for a blind time-out and then throws an exception if `this.closed` is still not true.

#### Mandated Comments

It is just plain silly to have a rule that says that every function must have a javadoc, or every variable must have a comment. Comments like this just clutter up the code, propagate lies, and lend to general confusion and disorganization.

```java
/**
*
* @param title The title of the CD
* @param author The author of the CD
* @param tracks The number of tracks on the CD
* @param durationInMinutes The duration of the CD in minutes
*/
public void addCD(String title, String author, int tracks, int durationInMinutes) {
  CD cd = new CD();
  cd.title = title;
  cd.author = author;
  cd.tracks = tracks;
  cd.duration = duration;
  cdList.add(cd);
}
```

#### Journal Comments

Sometimes people add a comment to the start of a module every time they edit it. Example:

```java
* Changes (from 11-Oct-2001)
* --------------------------
* 11-Oct-2001 : Re-organised the class and moved it to new package com.jrefinery.date (DG);
* 05-Nov-2001 : Added a getDescription() method, and eliminated NotableDate class (DG);
* 12-Nov-2001 : IBD requires setDescription() method, now that NotableDate class is gone (DG); Changed getPreviousDayOfWeek(),
getFollowingDayOfWeek() and getNearestDayOfWeek() to correct bugs (DG);
* 05-Dec-2001 : Fixed bug in SpreadsheetDate class (DG);
```

Today we have source code control systems, we don't need this type of logs.

#### Noise Comments

The comments in the follow examples doesn't provides new information.

```java
/**
* Default constructor.
*/
protected AnnualDateRule() {
}
```

```java
/** The day of the month. */
private int dayOfMonth;
```

Javadocs comments could enter in this category. Many times they are just redundant noisy comments written out of some misplaced desire to provide documentation.

#### Don’t Use a Comment When You Can Use a Function or a Variable

Example:

```java
// does the module from the global list <mod> depend on the
// subsystem we are part of?
if (smodule.getDependSubsystems().contains(subSysMod.getSubSystem()))
```

vs

```java
ArrayList moduleDependees = smodule.getDependSubsystems();
String ourSubSystem = subSysMod.getSubSystem();
if (moduleDependees.contains(ourSubSystem))
```

#### Position Markers

This type of comments are noising

```java
// Actions //////////////////////////////////
```

#### Closing Brace Comments

Example:

```java
public class wc {
  public static void main(String[] args) {
    BufferedReader in = new BufferedReader(new InputStreamReader(System.in));
    String line;
    int lineCount = 0;
    int charCount = 0;
    int wordCount = 0;
    try {
      while ((line = in.readLine()) != null) {
        lineCount++;
        charCount += line.length();
        String words[] = line.split("\\W");
        wordCount += words.length;

      } //while
      System.out.println("wordCount = " + wordCount);
      System.out.println("lineCount = " + lineCount);
      System.out.println("charCount = " + charCount);

    } // try
    catch (IOException e) {
      System.err.println("Error:" + e.getMessage());

    } //catch

  } //main
```

You could break the code in small functions instead to use this type of comments.

#### Attributions and Bylines

Example:

`/* Added by Rick */`

The VCS can manage this information instead.

#### Commented-Out Code

```java
InputStreamResponse response = new InputStreamResponse();
response.setBody(formatter.getResultStream(), formatter.getByteCount());
// InputStream resultsStream = formatter.getResultStream();
// StreamReader reader = new StreamReader(resultsStream);
// response.setContent(reader.read(formatter.getByteCount()));
```

If you don't need anymore, please delete it, you can back later with your VCS if you need it again.

#### HTML Comments

HTML in source code comments is an abomination, as you can tell by reading the code below.

```java
/**
* Task to run fit tests.
* This task runs fitnesse tests and publishes the results.
* <p/>
* <pre>
* Usage:
* &lt;taskdef name=&quot;execute-fitnesse-tests&quot;
* classname=&quot;fitnesse.ant.ExecuteFitnesseTestsTask&quot;
* classpathref=&quot;classpath&quot; /&gt;
* OR
* &lt;taskdef classpathref=&quot;classpath&quot;
* resource=&quot;tasks.properties&quot; /&gt;
* <p/>
* &lt;execute-fitnesse-tests
* suitepage=&quot;FitNesse.SuiteAcceptanceTests&quot;
* fitnesseport=&quot;8082&quot;
* resultsdir=&quot;${results.dir}&quot;
* resultshtmlpage=&quot;fit-results.html&quot;
* classpathref=&quot;classpath&quot; /&gt;
* </pre>
*/
```

#### Nonlocal Information

If you must write a comment, then make sure it describes the code it appears near. Don't offer systemwide information in the context of a local comment.

#### Too Much Information

Don't put interesting historical discussions or irrelevant descriptions of details into your comments.

#### Inobvious Connection

The connection between a comment and the code it describes should be obvious. If you are going to the trouble to write a comment, then at least you'd like the reader to be able to look at the comment and the code and understand what the comment is talking about

#### Function Headers

Short functions don’t need much description. A well-chosen name for a small function that does one thing is usually better than a comment header.

#### Javadocs in Nonpublic Code

Javadocs are for public APIs, in nonpublic code could be a distraction more than a help.
