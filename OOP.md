## OOP topics (Java Based): 

### Four Piller of OPP

- Abstraction 
- Encapsulation
- Inheritance 
- Polymorphism 

#### Abstraction
Abstraction is idea of hiding complex details of a class to its end user; A user might not need to know all the details of a class to use it; We can achieve this by using abstract class and interface some example: 

note : java doesn't allow multiple inheritance, but allows multilevel inheritance; [famous issue: Diamond problem ]

``` java

// class based 
abstract class User{
	
	String name;
	int age; 
	
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

public class Basic_oop_concepts {

	public static void main(String[] args) {
		// TODO Auto-generated method stub
		
		User sojib = new NoviceUser("Arafat Hossain Sojib", 25, true );
		sojib.createProblem();
		
	}

}
```
**Interface** based; Multiple inheritance support available; 
``` java
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

#### Encapsulation

The idea of encapsulting all the related things of a class to its scope, Encapsulation makes the code more organized.
Related Topic: Class Composition

``` java 

class Guitarist{
	public String guitar_type, experience_days, mood; 
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
		System.out.println("Guitar Type: "+ guitar_type + "\n Experience Days: " + experience_days + "\n mood: "+ mood + "willPlayToday: " + willPlayToday    );
	}
	
}

// main function 

	public static void main(String[] args) {

		Guitarist dhruba = new Guitarist("calssical", "two years", "happy");
		dhruba.cheerUp(); 
		dhruba.guitaristStatus();
		

		// clearing the object; 
		dhruba = null; 
		System.gc();
	}

```
##### Access Specifier:

how the class variables and methods can be accessed from its instance, or from its child instance or outside of this class;

| Access Specifier | Class | Package | Subclass | World |
|------------------|-------|---------|----------|-------|
| `private`        | ✅    | ❌      | ❌       | ❌    |
| `default` (no modifier) | ✅    | ✅      | ❌       | ❌    |
| `protected`      | ✅    | ✅      | ✅       | ❌    |
| `public`         | ✅    | ✅      | ✅       | ✅    |

#### Inheritance

Sub class is alowed to inherit properties from its base class, [creating new sub class based on base class]

Why we need this : 
    - code reusablity
    - Method overriding
    - Abstraction 

** java doesn't support class based multiple inheritance, it suporrts multilevel inheritance; 
** also doesn't support hybrid inheritance; 

``` java
// Parent class
class One {
    public void print_geek()
    {
        System.out.println("Geeks");
    }
}

class Two extends One {
    public void print_for() { System.out.println("for"); }
}

// Driver class
public class Main {
      // Main function
    public static void main(String[] args)
    {
        Two g = new Two();
        g.print_geek();
        g.print_for();
        g.print_geek();
    }
}

```

##### Interface based Inheritance: 
What is an Interface ?
---> It is a **referance** type [much like a String in java!]
---> similar to class can contain **only constants and method signatures**[but not implementations]
---> Only **exception** is for **static** and **default methods** (where implementations are allowed); 
    ---> defualt methods are intorduced for backward compatiblity 

``` java 
interface Animal{
	void sleep();
	
	default void bark() {
		System.out.println("animal Barks!");
	}
}

interface Mammal{
	Boolean isInteligent = true; 
}


class Dog implements Animal, Mammal{
	public void sleep() {
		System.out.println("A dog is sleeping!");
	}
	
	@Override
	public void bark() {
		System.out.println("Now Dog Barks Barks!");
	}
	
	public Dog() {
		System.out.println(isInteligent);
	}

	public static void main(String args[]){
		Dog husky = new Dog();

		// we can call any Dog methods: 
		husky.bark(); 
	}
}

```

#### Polymorphism
- Polymorphism
 - Compiletime Polymorphism 
    - Function Overloading 
    - Operator Overloading (not present in java)
 - Runtime Polymorphism
    - Function Overriding 

##### Functional overloading example: (compiletime polymorphism)

``` java 
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
##### Functional Overriding (Runtime polymorhism):
In Java, method overriding is commonly used in collections, especially with classes like List and ArrayList. The List interface defines a set of methods that any list-type class must implement, and ArrayList is one of the most commonly used implementations of the List interface.

``` java
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










## Next Topics to work on:

Class Relationships: 
	- Inheritance (Is - a)
	- Association (Has - A)
		- Aggregation  [ Weak   Has - A ]
		- Compostition [ Strong Has - A ]
	- Dependency 
	- Realization

Presentation and Clean Code; 
Slide and Doc, 
Agggregation, Composition
abstraction better than polymorhism 