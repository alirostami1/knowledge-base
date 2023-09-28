It is better to compose what an object can do than extend what it is. Compose when there is a "has a" (or "uses a") relationship, inherit when "is a".

- Why
	- Less coupling between classes.
	- Using inheritance, subclasses easily make assumptions, and break [[L - Liskov substitution principle|LSP]] .
	- Increase flexibility: accommodate future requirements changes, otherwise requiring restructuring of business-domain classes in the inheritance model.
	- Avoid problems often associated with relatively minor changes to an inheritance-based model including several generations of classes.
- How
	- Identify system object behaviors in separate interfaces, instead of creating a hierarchical relationship to distribute behaviors among business-domain classes via inheritance.
	- Test for [[L - Liskov substitution principle|LSP]] to decide when to inherit.

## Explain more

"Composition over Inheritance" is a principle in object-oriented programming that suggests favoring composition (building complex objects by combining simpler ones) over inheritance (creating new classes by inheriting properties and behaviors from existing classes). This approach promotes more flexible, maintainable, and modular code by avoiding the potential pitfalls of deep inheritance hierarchies.

Inheritance allows a class to inherit properties and methods from a parent class, but it can lead to issues like the fragile base class problem and tight coupling. Composition, on the other hand, involves creating instances of other classes within a class to achieve the desired functionality.

Here's an example in Java to illustrate the concept of Composition over Inheritance:

Let's consider a scenario where you're designing a system for different types of vehicles: cars, bicycles, and motorcycles.

**Using Inheritance:**
#wrongExample 

```java
class Vehicle {
    // Common properties and methods for all vehicles
}

class Car extends Vehicle {
    // Car-specific properties and methods
}

class Bicycle extends Vehicle {
    // Bicycle-specific properties and methods
}

class Motorcycle extends Vehicle {
    // Motorcycle-specific properties and methods
}
```

While this approach might seem reasonable at first, it can lead to problems if the hierarchy becomes more complex. For instance, if you need to add a feature common to both bicycles and motorcycles, you'd have to duplicate the code in both classes, violating the [[DRY]] (Don't Repeat Yourself) principle.

**Using Composition:**
#correctExample 

```java
class Engine {
    // Properties and methods for the engine
}

class Vehicle {
    private Engine engine;
    
    public Vehicle(Engine engine) {
        this.engine = engine;
    }
    
    // Common properties and methods for all vehicles
}

class Car {
    private Vehicle vehicle;
    
    public Car(Engine engine) {
        this.vehicle = new Vehicle(engine);
    }
    
    // Car-specific properties and methods
}

class Bicycle {
    private Vehicle vehicle;
    
    public Bicycle(Engine engine) {
        this.vehicle = new Vehicle(engine);
    }
    
    // Bicycle-specific properties and methods
}

class Motorcycle {
    private Vehicle vehicle;
    
    public Motorcycle(Engine engine) {
        this.vehicle = new Vehicle(engine);
    }
    
    // Motorcycle-specific properties and methods
}
```

In this composition-based approach, each vehicle type contains a reference to a `Vehicle` object, which itself contains an instance of an `Engine`. This allows you to encapsulate the common behavior and properties within the `Vehicle` class, while still being able to easily extend and modify the behavior of specific vehicle types.

Composition provides more flexibility, as you can easily add new features or change the behavior of a specific vehicle type without affecting others. It also avoids the pitfalls of deep inheritance hierarchies and promotes a more modular and maintainable codebase.