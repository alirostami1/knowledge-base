The Liskov Substitution Principle states that subclasses should be substitutable for their base classes.

This means that, given that class B is a subclass of class A, we should be able to pass an object of class B to any method that expects an object of class A and the method should not give any weird output in that case.

![[1_yKk2XKJaCLNlDxQMx1r55Q.webp]]

### Code example
There are several example that violates Liskov substitution principle. Important common point in these example is child can not work properly like its parent.
#### wrong example
This code violates the Liskov substitution principle.
#wrongExample 

```java
class Bird {
    public void fly() {
        System.out.println("A bird is flying.");
    }
}

class Penguin extends Bird {
    @Override
    public void fly() {
        throw new UnsupportedOperationException("Penguin can't fly.");
    }
}
```

As you see if you call `fly` method of `Bird` class it will throw an error when the bird is penguin.
#### Correct example
To fix this example we have to create non-flying bird class.
#correctExample 

```java
class Bird {
    public void makeSound() {
        System.out.println("A bird is making a sound.");
    }
}

class FlyingBird extends Bird {
    public void fly() {
        System.out.println("A flying bird is flying.");
    }
}

class Penguin extends Bird {
    @Override
    public void makeSound() {
        System.out.println("An Penguin is making a sound.");
    }
}

```
