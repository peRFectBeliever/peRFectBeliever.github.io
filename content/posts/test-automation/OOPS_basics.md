
+++
authors = ["Devendran Nehru"]
title = "OOPS in Simple Terms"
date = "2025-09-16"
description = "Basic Object Oriented Programming Concepts simplified"
tags = [
    "SDET",
    "automation",
    "java",
]
categories = [
    "QA",
    "Automation",
]
series = ["Test Automation Frameworks"]
+++

### Core OOP Concepts: Similarities and Differences in Java

#### Encapsulation

**Encapsulation** is the process of bundling data (variables) and the methods that operate on that data into a single unit, a class. It also involves restricting direct access to some of the object's components, which is known as **data hiding**.

**Key Idea:** It's like a capsule where the contents (data) are protected and can only be accessed through specific methods. This ensures the integrity of the data.

**Similarity:** It works in tandem with **abstraction** to hide implementation details.

**Difference:** Unlike **inheritance** and **polymorphism**, encapsulation is more about **controlling access** and **data protection**, not about defining relationships between classes or enabling flexible method calls.

**Code Example:**

Java

```
// Encapsulation
class Student {
    // private data (hidden from outside access)
    private String name;
    private int age;

    // public methods (getters and setters) to access and modify the private data
    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        // Validation logic can be added here
        if (age > 0) {
            this.age = age;
        }
    }
}

```

----------

#### Inheritance

**Inheritance** is a mechanism where one class acquires the properties and behaviors of another class. The class that inherits is called the **subclass** or **child class**, and the class being inherited from is the **superclass** or **parent class**. This promotes code reusability.

**Key Idea:** A child class is a more specialized version of its parent. It inherits the parent's traits and can also have its own unique ones.

**Similarity:** It's a prerequisite for **polymorphism** because polymorphism relies on a hierarchical relationship between classes.

**Difference:** Unlike **encapsulation** (data protection) and **abstraction** (hiding details), inheritance is about **establishing a hierarchical relationship** between classes to reuse code.

**Code Example:**

Java

```
// Inheritance
class Animal { // Superclass
    void eat() {
        System.out.println("This animal eats food.");
    }
}

class Dog extends Animal { // Subclass
    void bark() {
        System.out.println("The dog barks.");
    }
}

```

----------

#### Abstraction

**Abstraction** is the concept of hiding the complex implementation details and showing only the essential features of the object. It focuses on "what" the object does rather than "how" it does it. This is achieved using **abstract classes** and **interfaces**.

**Key Idea:** It provides a blueprint or a contract for other classes to implement. Think of a TV remote—you use the buttons without knowing the complex circuitry inside.

**Similarity:** It is often used with **encapsulation** to hide details and with **polymorphism** to achieve dynamic behavior.

**Difference:** While **encapsulation** hides data for protection, **abstraction** hides **implementation logic** to simplify the design and usage of an object. **Inheritance** is about code reuse, while abstraction is about defining a common structure.

**Code Example:**

Java

```
// Abstraction
abstract class Vehicle {
    abstract void run(); // Abstract method (no implementation)
}

class Car extends Vehicle {
    // Providing implementation for the abstract method
    void run() {
        System.out.println("Car is running safely.");
    }
}

```

----------

#### Polymorphism

**Polymorphism** means "many forms." It is the ability of an object to take on many forms. In Java, this is achieved through **method overriding** (runtime polymorphism) and **method overloading** (compile-time polymorphism). It allows a single interface to represent a number of different types of objects.

**Key Idea:** A single method call can behave differently depending on the object it is called on. This is what allows you to treat a `Dog` object as an `Animal` object and still have the correct method called at runtime.

**Similarity:** It heavily relies on **inheritance** to work. Without a parent-child class relationship, you cannot achieve runtime polymorphism.

**Difference:** While **inheritance** defines the parent-child relationship, **polymorphism** leverages that relationship to enable dynamic behavior. It's the "action" part of the relationship.

**Code Example:**

Java

```
// Polymorphism
class Animal { // Parent class
    void makeSound() {
        System.out.println("The animal makes a sound.");
    }
}

class Dog extends Animal { // Child class 1
    @Override
    void makeSound() {
        System.out.println("The dog barks.");
    }
}

class Cat extends Animal { // Child class 2
    @Override
    void makeSound() {
        System.out.println("The cat meows.");
    }
}

// In the main method:
// Animal myDog = new Dog();
// myDog.makeSound(); // Output: The dog barks.
// Animal myCat = new Cat();
// myCat.makeSound(); // Output: The cat meows.

```