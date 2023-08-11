> - High-level modules should not depend on low-level modules. Both should depend on the abstraction.
> 
> - Abstractions should not depend on details. Details should depend on abstractions.

**High-level Module(or Class)**: Class that executes an action with a tool.

**Low-level Module (or Class)**: The tool that is needed to execute the action

**Abstraction**: Represents an interface that connects the two Classes.

**Details**: How the tool works

This principle says a Class should not be fused with the tool it uses to execute an action. Rather, it should be fused to the interface that will allow the tool to connect to the Class.

It also says that both the Class and the interface should not know how the tool works. However, the tool needs to meet the specification of the interface.

![[1_Qk8tDmjQlyvwKxNTfXIo0Q.webp]]

### Code example
#### Wrong example
This code violates dependency inversion principle.
#wrongExample 

```java
class LightBulb {
    public void turnOn() {
        // implementation
    }
}

class Switch {
    private LightBulb bulb;

    public Switch() {
        this.bulb = new LightBulb();
    }

    public void operate() {
        bulb.turnOn();
    }
}
```

In this example, the `Switch` class directly depends on the `LightBulb` class. If we want to change the type of bulb, we'd have to modify the `Switch` class, violating the DIP.

#### Correct example
To fix this example we have to remove direct dependency of high-level class to low-level class.
#correctExample 

```java
interface Switchable {
    void turnOn();
}

class LightBulb implements Switchable {
    @Override
    public void turnOn() {
        // implementation
    }
}

class Switch {
    private Switchable device;

    public Switch(Switchable device) {
        this.device = device;
    }

    public void operate() {
        device.turnOn();
    }
}

```

Dependency inversion principle examples are similar to [[O - Open close principle\|open close principle]].