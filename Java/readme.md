### Q.OOP in java
- In programming, an "Oops" typically refers to Object-Oriented Programming (OOP). OOP is a programming paradigm based on the concept of "objects," which are instances of classes. These objects can contain data in the form of fields (often known as attributes or properties) and code in the form of procedures (often known as methods).
- Key concepts in OOP include:
1. Class: A blueprint for creating objects. It defines a set of attributes and methods that the created objects will have.
2. Object: An instance of a class. It is created from a class and represents an entity with attributes and behaviors defined by the class.
3. Encapsulation: The bundling of data (attributes) and methods (functions or procedures) that operate on the data into a single unit, or class. It also involves restricting direct access to some of the object's components, which is a means of preventing accidental interference and misuse.
4. Inheritance: The mechanism by which one class can inherit attributes and methods from another class. This allows for code reusability and the creation of a hierarchical relationship between classes.
5. Polymorphism: The ability of different objects to respond to the same method call in different ways. This is typically achieved through method overriding (a subclass provides a specific implementation of a method that is already defined in its superclass) and method overloading (multiple methods have the same name but different parameters).
6. Abstraction: The process of hiding the complex implementation details and showing only the essential features of the object. This helps in reducing programming complexity and effort.
- These concepts form the foundation of many modern programming languages, including Java, C++, Python, and others. OOP aims to provide a clear modular structure for programs, making it easier to manage large software systems by promoting code reuse and improving maintainability.

### Q.Give Code Example.
1. Encapsulation:
```
public class Person {
    // Private fields to encapsulate the internal state
    private String name;
    private int age;

    // Public constructor to initialize the Person object
    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }

    // Getter method for name
    public String getName() {
        return name;
    }

    // Setter method for name
    public void setName(String name) {
        this.name = name;
    }

    // Getter method for age
    public int getAge() {
        return age;
    }

    // Setter method for age
    public void setAge(int age) {
        if (age > 0) { // Adding a simple validation
            this.age = age;
        } else {
            System.out.println("Age must be a positive number.");
        }
    }

    // A method to display person details
    public void displayPersonInfo() {
        System.out.println("Name: " + name + ", Age: " + age);
    }

    public static void main(String[] args) {
        // Creating a Person object
        Person person = new Person("John Doe", 25);

        // Accessing and modifying the encapsulated fields via methods
        person.displayPersonInfo();

        person.setName("Jane Doe");
        person.setAge(30);
        
        person.displayPersonInfo();
        
        // Trying to set an invalid age
        person.setAge(-5); // This will trigger the validation in the setter method
    }
}
```
Explanation :
1. Encapsulated Fields: The fields name and age are declared private to restrict direct access from outside the class.
2. Getter and Setter Methods: Public methods getName, setName, getAge, and setAge are provided to allow controlled access and modification of the private fields.
3. Validation: The setAge method includes a simple validation to ensure that the age is a positive number, demonstrating how encapsulation allows for added control over the data.
4. Main Method: In the main method, a Person object is created and its fields are accessed and modified through the getter and setter methods.
2. Inheritance:
``
public class ElectricCar extends Car {
    private int batteryCapacity;

    public ElectricCar(String make, String model, int year, int batteryCapacity) {
        super(make, model, year);
        this.batteryCapacity = batteryCapacity;
    }

    public void chargeBattery() {
        System.out.println("Battery charging");
    }

    public int getBatteryCapacity() {
        return batteryCapacity;
    }

    public void setBatteryCapacity(int batteryCapacity) {
        this.batteryCapacity = batteryCapacity;
    }
}
Polymorphism
Polymorphism:
Polymorphism allows objects to be treated as instances of their parent class rather than their actual class. Method overriding is a key feature.
java
Copy code
public class GasolineCar extends Car {
    public GasolineCar(String make, String model, int year) {
        super(make, model, year);
    }

    @Override
    public void startEngine() {
        System.out.println("Gasoline engine started");
    }
}

public class ElectricCar extends Car {
    public ElectricCar(String make, String model, int year) {
        super(make, model, year);
    }

    @Override
    public void startEngine() {
        System.out.println("Electric motor started");
    }
}

public class Main {
    public static void main(String[] args) {
        Car car1 = new GasolineCar("Ford", "Mustang", 2022);
        Car car2 = new ElectricCar("Tesla", "Model S", 2023);

        car1.startEngine(); // Output: Gasoline engine started
        car2.startEngine(); // Output: Electric motor started
    }
}
Abstraction
Abstraction:
Abstraction hides the complex implementation details and shows only the necessary features of the object.
java
Copy code
abstract class Vehicle {
    abstract void startEngine();
    abstract void stopEngine();
}

public class Car extends Vehicle {
    private String make;
    private String model;
    private int year;

    public Car(String make, String model, int year) {
        this.make = make;
        this.model = model;
        this.year = year;
    }

    @Override
    void startEngine() {
        System.out.println("Car engine started");
    }

    @Override
    void stopEngine() {
        System.out.println("Car engine stopped");
    }
}

public class Motorcycle extends Vehicle {
    @Override
    void startEngine() {
        System.out.println("Motorcycle engine started");
    }

    @Override
    void stopEngine() {
        System.out.println("Motorcycle engine stopped");
    }
}

public class Main {
    public static void main(String[] args) {
        Vehicle car = new Car("Toyota", "Camry", 2021);
        Vehicle motorcycle = new Motorcycle();

        car.startEngine(); // Output: Car engine started
        motorcycle.startEngine(); // Output: Motorcycle engine started
    }
}
This example demonstrates how OOP concepts like classes, objects, encapsulation, inheritance, polymorphism, and abstraction can be implemented in Java.
