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
		
		NoviceUser nibaron = new NoviceUser("Nibaron Kumar Das", 25, true );
		nibaron.createProblem();
		
	}

}
```
Interface based; Multiple inheritance support available; 
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

// we can see the results in main methods; 

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
		
		dhruba = null; 
		System.gc();
	}


```
#### Inheritance

Sub class is alowed to inherit properties from its base class, [creating new class based on another class]

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
---> its a referance type [much like a string!]
---> similar to class can contain only constants and method signatures[but not implementations]
---> Only exception is for static and default methods; 
    ---> defualt methods are intorduced for backwar compatiblity 

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
}

```

#### Polymorphism
- Polymorphism
 - Runtime Polymorphism
    - Function Overriding 
 - Compiletime Polymorphism 
    - Function Overloading 
    - Operator Overloading 

Functional overloading example: 
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
}
```

Abstraction: 










### Requirements:

sychronised
null handling 

Presentation and Clean Code; 
Slide and Doc, 
Agggregation, Composition
abstraction better than polymorhism 