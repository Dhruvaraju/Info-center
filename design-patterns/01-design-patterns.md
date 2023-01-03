# What are design patterns?

- An elegant solution for repeating problems.
- A design pattern should  structure your classes, and define how this classes should talk to each other.

Design patterns elements of reusable object-oriented software is a book by Gang of Four, which defines 23 design patterns, classified in to 3 categories.

- Creational
	- Ways to create objects
- Structural
	- Defining relations between objects
- Behavioral
	- Interactions and communications between these objects.

- What is an interface
	- A contract that specifies the capabilities that a class should provide.
```java
public interface TaxCalculator {  
    float calculateTax();  
}
```

Implementations:
```java
public class TaxCalculator2022 implements TaxCalculator{  
    @Override  
    public float calculateTax() {  
        return 1;  
    }  
}

public class TaxCalculator2023 implements TaxCalculator{  
    @Override  
    public float calculateTax() {  
        return 2;  
    }  
}
```
- Encapsulation
	- Bundling the data, the methods that operate on the data within one unit or class.
	- Hiding the values or state of a class inside an object.
	- This prevents data from invalid state.
	- 
- Abstraction
- Inheritance
- Polymorphism

