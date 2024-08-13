## OOP topics (Java Based): 

### Four Piller of OPP

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
#### Inheritance
#### Polymorphism

Abstraction: 
