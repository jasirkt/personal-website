---
title: "Abstract Factory Pattern"
permalink: /2019/09/abstract-factory-pattern.html
published: true
---

The Abstract Factory Pattern adds another layer of abstraction over the Factory Pattern. It has an Abstract Factory Interface which is implemented by several Factory classes. A Super Factory decides which Factory should be used based on the requirement. Abstract Factory Pattern is one the creational design patterns.

### Participants
- **AbstractFactory**<br/>
    An interface which for creating AbstractProduct objects.
- **ConcreteFactory**<br/>
    Implements AbstractFactory and creates ConcreteProduct objects.
- **AbstractProduct**<br/>
    An interface for type of products.
- **ConcreteProduct**<br/>
    Implements AbstractProduct object. Here is where the actual product code is defined.
- **Client**<br/>
  Uses methods provided by AbstractFactory and AbstractProduct interfaces to create objects.
 
### UML Diagram

<img style="max-width:100%" src="https://1.bp.blogspot.com/-CzoaZl5oRok/XWc3ehjHuRI/AAAAAAABh_0/sTHw8wWjcbM-TdjK4kh1QzInUkuIqT0qwCLcBGAs/s1600/abstract_factory.png" />

As you can see in the diagram, There is an AbstractFactory interface which is implemented by 2 factory classes. Client doesn't access the concrete factory classes directly, instead uses the methods provided by AbstractFactory interface.

### Example
```java
abstract class Computer {
    public abstract void powerOn();
}

class PC extends Computer {

    public void powerOn() {
        System.out.print("Powering on PC...");
    }
}

class Server extends Computer {

    public void powerOn() {
        System.out.print("Powering on server...");
    }
}

interface AbstractComputerFactory {
    Computer createComputer();
}

class PCFactory implements AbstractComputerFactory {

    public Computer createComputer() {
        return new PC();
    }
}

class ServerFactory implements AbstractComputerFactory {

    public Computer createComputer() {
        return new Server();
    }
}

class ComputerFactory {
    public static Computer createComputer(String type) {
        AbstractComputerFactory factory;
        switch (type) {
            case "pc" : factory = new PCFactory(); break;
            case "server" : factory = new ServerFactory(); break;
            default: throw new IllegalArgumentException();
        }

        return factory.createComputer();
    }
}

class Main {
    public static void main(String[] args) {
        ComputerFactory.createComputer("pc").powerOn();
        ComputerFactory.createComputer("server").powerOn();
    }
}
```