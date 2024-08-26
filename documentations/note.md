### 2.1.1 Why we need Builder Method Design Pattern ?

**Method Chaining:**
Method chaining is a technique where multiple methods are called on the same object in a single statement. Each method returns the object itself, allowing the next method to be called on that object. For example:

```java
final class Student {

    // instance fields
    private int id;
    private String name;
    private String address;

    // Setter Methods
    // Note that all setters method
    // return this reference
    public Student setId(int id)
    {
        this.id = id;
        return this;
    }

    public Student setName(String name)
    {
        this.name = name;
        return this;
    }

    public Student setAddress(String address)
    {
        this.address = address;
        return this;
    }

    @Override public String toString()
    {
    	return "id = " + this.id + ", name = " + this.name + ", address = " + this.address;
    }
}
```

In client class's main function we create object instance with
```java
Student student = new Student()
                    .setId(1)
                    .setName("Ram")
                    .setAddress("Delhi");
```
In this example, setId(1), setName("Ram") and setAddress("Delhi") are chained together, and each method returns the Student object.

> **The Problem with Method Chaining in a Multi-Threaded Environment:**

In a `multi-threaded` environment, multiple threads can access and modify the `same object simultaneously`. If method chaining is used `without proper synchronization`, `one thread` might observe the object in an `inconsistent state` while `another thread` is still in the `process of updating it`.

For example, consider the following scenario:

1. Thread A starts creating a Student object using method chaining.
    ```java
    student.setId(1).setName("Ram").setAddress("Delhi");
    ```
2. After **Thread A** calls *setName("Ram")* but before it calls *setAddress("Delhi")*, **Thread B** reads the Student object.
3. **Thread B** sees the Student object with name set to "Ram" but with the address still unset or set to a previous value, leading to an inconsistent state.

> **Builder Pattern as a Solution:**

The `Builder Pattern` provides a way `to construct complex objects step by step`. Instead of directly modifying the object's state through method chaining, the Builder Pattern uses `a separate Builder class to collect all the parameters needed` to create an object. Only when the object is `fully built, it is created in one step,` ensuring that it `is in a consistent state when it is made available to other threads.`

> Here's how the Builder Pattern helps:

1. `Immutable Object Creation:` The Student object is only created when the build() method is called, and at this point, all necessary fields are set, ensuring consistency.
2. `Thread Safety:` Since the Student object is not exposed until it's fully constructed, there is no risk of another thread observing it in an inconsistent state.

> Example of the Builder Pattern:

```java
public class Student {
    private final String name;
    private final String address;

    private Student(Builder builder) {
        this.name = builder.name;
        this.address = builder.address;
    }

    public static class Builder {
        private String name;
        private String address;

        public Builder setName(String name) {
            this.name = name;
            return this;
        }

        public Builder setAddress(String address) {
            this.address = address;
            return this;
        }

        public Student build() {
            return new Student(this);
        }
    }
}

```
**uses:**
```java
Student student = new Student.Builder()
                     .setName("Ram")
                     .setAddress("Delhi")
                     .build();

```

**In this example:**

- The Student object is only created when build() is called, ensuring that all fields (name and address) are set.
- This avoids the risk of other threads seeing a Student object in an inconsistent state during its construction.