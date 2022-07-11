---
layout: default
title: Ch10 Object-Oriented Programming - Polymorphism and Interface
parent: Java Programming
grand_parent: School Lecture
nav_order: 11
mathjax: true
mermaid: true
permalink: /docs/java/ch10
---

# Ch10 Object-Oriented Programming - Polymorphism and Interface
{: .no_toc }

<details markdown="block">
  <summary>
    Table of contents
  </summary>
{: .fs-3 .text-delta }
- TOC
{:toc}
</details>

---

## Objectives

- Learn the concept of polymorphism and how it enables "programming in the general"

- Use overriden methods to effect polymorphism

- Distinguish between abstract and concrete class

- Declare abstract methods to create abstract classes

- Learn how polymorphism makes systems extensible and maintainable

- Determine an object's type at execution time

- Declare and implement interfaces, and become familiar with the Java SE 8 interface enhancements

---

## 10.1 Introduction

### Polymorphism

- The same message sent to a variety of objects has differenct form of results

- Enables you to program in the general rather than program in the specific

- Enables you to write programs that process objects that share the same superclass as if they were all objects of the superclass; this can simplify programming

<div hidden>
@startuml 10-class-diagram-1
Frog -u-|> Animal
Fish -u-|> Animal
Bird -u-|> Animal
GoldFish -u-|> Fish
Frog -[hidden]> Fish
@enduml
</div>

<center markdown="block">
![class-diagram-1](/assets/java-programming/images/10-class-diagram-1.svg)

Class diagram
</center>

---

## 10.3 Demonstrating Polymorphic Behavior

### Upcasting

<div hidden>
@startuml 10-class-diagram-2
skinparam classAttributeIconSize 0
class Animal {
	+ void show()
	+ void move()
}
class Fish {
	+ void draw()
	+ void move()  // overriden
}

Fish -u-|> Animal
@enduml
</div>

<center markdown="block">
![class-diagram-2](/assets/java-programming/images/10-class-diagram-2.svg)

Class diagram
</center>

```java
public class AnimalTest {
    public static void main(String[] args) {
        Animal animal = new Animal();
        animal move();  // 1

        Fish fish = new Fish();
        fish.move();  // 2
        fish.show();

        Animal animal2 = new Fish();  // upcasting
        animal2.show();
        animal2.draw();  // error
        animal2.move();  // 2
    }
}
```

- is-a relationship에서 upcasting이 일어난다.

- Casting a subclass type to superclass type (**upcasting**)

- A superclass reference to a subclass object

	- Basically

		- You can use just the superclass type's members

	- For the overridden methods

		- The called method is determined at execution time polymorphically

		- Subclass's overridden method is called

<div hidden>
@startuml 10-class-diagram-2
skinparam classAttributeIconSize 0
class Animal {
	+ void move()
}
class Fish {
	+ void move()  // overridden
}
class Frog {
	+ void move()  // overridden
}
class Bird {
	+ void move()  // overridden
}

Fish -u-|> Animal
Frog -u-|> Animal
Bird -u-|> Animal
@enduml
</div>

<center markdown="block">
![class-diagram-2](/assets/java-programming/images/10-class-diagram-2.svg)

Class Diagram
</center>

```java
public class AnimalTest {
    public static void main(String[] args) {
        // each array element is a reference to Animal
        Animal[] animal = new Animal[3];
        animal[0] = new Fish();  // upcasting from Fish to Animal
        animal[1] = new Frog();  // upcasting from Frog to Animal
        animal[2] = new Bird();  // upcasting from Bird to Animal

        for (int i = 0; i < animal.length; i++)
            animal[i].move();  // polymorphic behavior
                               // dynamic binding or late binding
    }
}
```

- 다른 객체에게 같은 메시지를 보냄. 각 객체의 `move()`는 다른 일을 수행

### Downcasting

- Casting a superclass type to a subclass type(downcasting)

	- Needs explicit type casting

	- Enables a program to invoke subclass methods that are not in the superclass

<div hidden>
@startuml 10-class-diagram-3
class Animal {
	+ void show()
}
class Fish {
	+ void draw()
}

Fish -u-|> Animal
@enduml
</div>

<center markdown="block">
![class-diagram-3](/assets/java-programming/images/10-class-diagram-3.svg)

Class diagram
</center>

```java
public class AnimalTest {
    public static void main(String[] args) {
        Animal animal = new Fish();  // upcasting
        animal.draw();  // error

        Fish fish = (Fish)animal;  // downcasting (case 1)
        fish.draw();

        ((Fish)animal).draw();  // downcasting (case 2)
    }
}
```

- upcasting 후 downcasting해야 subclass의 method를 error 없이 call할 수 있다.

<div hidden>
@startuml 10-class-diagram-4
class CommissionEmployee {
	+ String toString()
}
class BasePlusCommissionEmployee {
	+ String toString  // overriden
}

BasePlusCommissionEmployee -u-|> CommissionEmployee
@enduml
</div>

<center markdown="block">
![class-diagram-4](/assets/java-programming/images/10-class-diagram-4.svg)

Class diagram
</center>

```java
// Fig. 10.1: PolymorphismTest.java
// Assigning superclass and subclass references to superclass and
// subclass variables.

public class PolymorphismTest {
    public static void main(String[] args) {
        // assign superclass reference to superclass variable
        CommissionEmployee commissionEmployee = new CommissionEmployee(
            "Sue", "Jones", "222-22-2222", 10000, .06);

        // assign subclass reference to subclass variable
        BasePlusCommissionEmployee basePlusCommissionEmployee =
            new BasePlusCommissionEmployee(
            "Bob", "Lewis", "333-33-3333", 5000, .04, 300);

        // invoke toString on superclass object using superclass variable
        System.out.printf("%s %s:%n%n%s%n%n",
            "Call CommissionEmployee's toString with superclass reference ",
            "to superclass object", commissionEmployee.toString());

        // invoke toString on subclass object using subclass variable
        System.out.printf("%s %s:%n%n%s%n%n",
            "Call BasePlusCommissionEmployee's toString with subclass",
            "reference to subclass object",
            basePlusCommissionEmployee.toString());

        // invoke toString on subclass object using superclass variable
        CommissionEmployee commissionEmployee2 =
            basePlusCommissionEmployee;
        System.out.printf("%s %s:%n%n%s%n",
            "Call BasePlusCommissionEmployee's toString with superclass",
            "reference to subclass object", commissionEmployee2.toString());
    }
}
```

```
Call CommissionEmployee's toString with superclass reference  to superclass object:

commission employee: Sue Jones
social security number: 222-22-2222
gross sales: 10000.00
commission rate: 0.06

Call BasePlusCommissionEmployee's toString with subclass reference to subclass object:

base-salaried commission employee: Bob Lewis
social security number: 333-33-3333
gross sales: 5000.00
commission rate: 0.04
base salary: 300.00

Call BasePlusCommissionEmployee's toString with superclass reference to subclass object:

base-salaried commission employee: Bob Lewis
social security number: 333-33-3333
gross sales: 5000.00
commission rate: 0.04
base salary: 300.00
```

---

## 10.4 Abstract Classes and Methods

### Concreate classes

- Can be used to instantiate objects

- Provide implementations of every method they declare

### Abstract classes

- Contains one or more **abstract methods**

- Do not provide implementations of the abstract methods

- Can contain some concrete(non-abstract) methods and fields

- Cannot be used to instantiate objects

- Provide superclass from which other classes can inherit and thus share a common design

- Constructors and `static` methods cannot be declare `abstract`

- Each concrete subclass of an abstract superclass also must provide concrete implementations of each of the superclass's abstract methods; otherwise, these subclasses, too, will be abstract

```java
public abstract class Employee {
	private String firstName;
	public abstract double earnings();
}
```

```java
public class CommissionEmployee extends Employee {  // error
	private double grossSales;

	public double getGrossSales() {
		return grossSales;
	}
}
```

```
CommissionEmployee.java:1: error: CommissionEmployee is not abstract and does not override abstract method earnings() in Employee
public class CommissionEmployee extends Employee {  // error
       ^
1 error
```

### You can use abstract superclass

- to declare variables

	- ex) `AbstractClass var;`

- to invoke `static` methods declared in those abstract superclasses

	- ex) `AbstractClass.staticMethod();`

---

## 10.5 Case Study: Payroll System Using Polymorphism

- Fig. 10.2 shows the inheritance hierarchy for our polymorphicemployee-payroll application

<div hidden>
@startuml 10-employee-hierarchy
skinparam classAttributeIconSize 0
abstract Employee {
 + {abstract} double earnings()
 + String toString()
}
class SalariedEmployee {
 + double earnings()
 + String toString()
}
class CommissionEmployee {
 + double earnings()
 + String toString()
}
class HourlyEmployee {
 + double earnings()
 + String toString()
}
class BasePlusCommissionEmployee {
 + double earnings()
 + String toString()
}
SalariedEmployee -u-|> Employee
CommissionEmployee -u-|> Employee
HourlyEmployee -u-|> Employee
BasePlusCommissionEmployee -u-|> CommissionEmployee
SalariedEmployee -[hidden]> CommissionEmployee
@enduml
</div>

<center markdown="block">
![employee-hierarchy](/assets/java-programming/images/10-employee-hierarchy.svg)

Fig. 10.2 `Employee` hierarchy UML class diagram
</center>

- Abstract class names are italicized in the UML

### 10.5.1 Abstract Superclass `Employee`

```java
// Fig. 10.4: Employee.java
// Employee abstract superclass.

public abstract class Employee {
    private final String firstName;
    private final String lastName;
    private final String socialSecurityNumber;

    // constructor
    public Employee(String firstName, String lastName,
        String socialSecurityNumber) {
        this.firstName = firstName;
        this.lastName = lastName;
        this.socialSecurityNumber = socialSecurityNumber;
    }

    // return first name
    public String getFirstName() {return firstName;}

    // return last name
    public String getLastName() {return lastName;}

    // return social security number
    public String getSocialSecurityNumber() {return socialSecurityNumber;}

    // return String representation of Employee object
    @Override
    public String toString() {
        return String.format("%s %s%nsocial security number: %s",
            getFirstName(), getLastName(), getSocialSecurityNumber());
    }

    // abstract method must be overridden by concrete subclasses
    public abstract double earnings(); // no implementation here
}
```

### 10.5.2 Concreate Subclass `SalariedEmployee`

```java
// Fig. 10.5: SalariedEmployee.java
// SalariedEmployee concrete class extends abstract class Employee.

public class SalariedEmployee extends Employee {
    private double weeklySalary;

    // constructor
    public SalariedEmployee(String firstName, String lastName,
        String socialSecurityNumber, double weeklySalary) {
        super(firstName, lastName, socialSecurityNumber);

        if (weeklySalary < 0.0) {
            throw new IllegalArgumentException(
                "Weekly salary must be >= 0.0");
        }

        this.weeklySalary = weeklySalary;
    }

    // set salary
    public void setWeeklySalary(double weeklySalary) {
        if (weeklySalary < 0.0) {
            throw new IllegalArgumentException(
                "Weekly salary must be >= 0.0");
        }

        this.weeklySalary = weeklySalary;
    }

    // return salary
    public double getWeeklySalary() {return weeklySalary;}

    // calculate earnings; override abstract method earnings in Employee
    @Override
    public double earnings() {return getWeeklySalary();}

    // return String representation of SalariedEmployee object
    @Override
    public String toString() {
        return String.format("salaried employee: %s%n%s: $%,.2f",
            super.toString(), "weekly salary", getWeeklySalary());
    }
}
```

### 10.5.3 Concreate Subclass `HourlyEmployee`

```java
// Fig. 10.6: HourlyEmployee.java
// HourlyEmployee class extends Employee.

public class HourlyEmployee extends Employee {
    private double wage; // wage per hour
    private double hours; // hours worked for week

    // constructor
    public HourlyEmployee(String firstName, String lastName,
        String socialSecurityNumber, double wage, double hours) {
        super(firstName, lastName, socialSecurityNumber);

        if (wage < 0.0) { // validate wage
            throw new IllegalArgumentException("Hourly wage must be >= 0.0");
        }

        if ((hours < 0.0) || (hours > 168.0)) { // validate hours
            throw new IllegalArgumentException(
                "Hours worked must be >= 0.0 and <= 168.0");
        }

        this.wage = wage;
        this.hours = hours;
    }

    // set wage
    public void setWage(double wage) {
        if (wage < 0.0) { // validate wage
            throw new IllegalArgumentException("Hourly wage must be >= 0.0");
        }

        this.wage = wage;
    }

    // return wage
    public double getWage() {return wage;}

    // set hours worked
    public void setHours(double hours) {
        if ((hours < 0.0) || (hours > 168.0)) { // validate hours
            throw new IllegalArgumentException(
                "Hours worked must be >= 0.0 and <= 168.0");
        }

        this.hours = hours;
    }

    // return hours worked
    public double getHours() {return hours;}

    // calculate earnings; override abstract method earnings in Employee
    @Override
    public double earnings() {
        if (getHours() <= 40) { // no overtime
            return getWage() * getHours();
        }
        else {
            return 40 * getWage() + (getHours() - 40) * getWage() * 1.5;
        }
    }

    // return String representation of HourlyEmployee object
    @Override
    public String toString() {
        return String.format("hourly employee: %s%n%s: $%,.2f; %s: %,.2f",
            super.toString(), "hourly wage", getWage(),
            "hours worked", getHours());
    }
}
```

### 10.5.4 Concreate Subclass `CommissionEmployee`

```java
// Fig. 10.7: CommissionEmployee.java
// CommissionEmployee class extends Employee.

public class CommissionEmployee extends Employee {
    private double grossSales; // gross weekly sales
    private double commissionRate; // commission percentage

    // constructor
    public CommissionEmployee(String firstName, String lastName,
        String socialSecurityNumber, double grossSales,
        double commissionRate) {
        super(firstName, lastName, socialSecurityNumber);

        if (commissionRate <= 0.0 || commissionRate >= 1.0) { // validate
            throw new IllegalArgumentException(
                "Commission rate must be > 0.0 and < 1.0");
        }

        if (grossSales < 0.0) { // validate
            throw new IllegalArgumentException("Gross sales must be >= 0.0");
        }

        this.grossSales = grossSales;
        this.commissionRate = commissionRate;
    }

    // set gross sales amount
    public void setGrossSales(double grossSales) {
        if (grossSales < 0.0) { // validate
            throw new IllegalArgumentException("Gross sales must be >= 0.0");
        }

        this.grossSales = grossSales;
    }

    // return gross sales amount
    public double getGrossSales() {return grossSales;}

    // set commission rate
    public void setCommissionRate(double commissionRate) {
        if (commissionRate <= 0.0 || commissionRate >= 1.0) { // validate
            throw new IllegalArgumentException(
                "Commission rate must be > 0.0 and < 1.0");
        }

        this.commissionRate = commissionRate;
    }

    // return commission rate
    public double getCommissionRate() {return commissionRate;}

    // calculate earnings; override abstract method earnings in Employee
    @Override
    public double earnings() {
        return getCommissionRate() * getGrossSales();
    }

    // return String representation of CommissionEmployee object
    @Override
    public String toString() {
        return String.format("%s: %s%n%s: $%,.2f; %s: %.2f",
            "commission employee", super.toString(),
            "gross sales", getGrossSales(),
            "commission rate", getCommissionRate());
    }
}
```

### 10.5.5 Indirect Concrete Subclass `BasePlusCommissionEmployee`

```java
// Fig. 10.8: BasePlusCommissionEmployee.java
// BasePlusCommissionEmployee class extends CommissionEmployee.

public class BasePlusCommissionEmployee extends CommissionEmployee {
    private double baseSalary; // base salary per week

    // constructor
    public BasePlusCommissionEmployee(String firstName, String lastName,
        String socialSecurityNumber, double grossSales,
        double commissionRate, double baseSalary) {
        super(firstName, lastName, socialSecurityNumber,
            grossSales, commissionRate);

        if (baseSalary < 0.0) { // validate baseSalary
            throw new IllegalArgumentException("Base salary must be >= 0.0");
        }

        this.baseSalary = baseSalary;
    }

    // set base salary
    public void setBaseSalary(double baseSalary) {
        if (baseSalary < 0.0) { // validate baseSalary
            throw new IllegalArgumentException("Base salary must be >= 0.0");
        }

        this.baseSalary = baseSalary;
    }

    // return base salary
    public double getBaseSalary() {return baseSalary;}

    // calculate earnings; override method earnings in CommissionEmployee
    @Override
    public double earnings() {return getBaseSalary() + super.earnings();}

    // return String representation of BasePlusCommissionEmployee object
    @Override
    public String toString() {
        return String.format("%s %s; %s: $%,.2f",
            "base-salaried", super.toString(),
            "base salary", getBaseSalary());
    }
}
```

### 10.5.6 Polymorphic Processing, Operator `instanceof` and Downcasting

```java
// Fig. 10.9: PayrollSystemTest.java
// Employee hierarchy test program.

public class PayrollSystemTest {
    public static void main(String[] args) {
        // create subclass objects
        // no type casting
        SalariedEmployee salariedEmployee =
            new SalariedEmployee("John", "Smith", "111-11-1111", 800.00);
        HourlyEmployee hourlyEmployee =
            new HourlyEmployee("Karen", "Price", "222-22-2222", 16.75, 40);
        CommissionEmployee commissionEmployee =
            new CommissionEmployee(
            "Sue", "Jones", "333-33-3333", 10000, .06);
        BasePlusCommissionEmployee basePlusCommissionEmployee =
            new BasePlusCommissionEmployee(
            "Bob", "Lewis", "444-44-4444", 5000, .04, 300);

        System.out.println("Employees processed individually:");

        System.out.printf("%n%s%n%s: $%,.2f%n%n",
            salariedEmployee, "earned", salariedEmployee.earnings());
        System.out.printf("%s%n%s: $%,.2f%n%n",
            hourlyEmployee, "earned", hourlyEmployee.earnings());
        System.out.printf("%s%n%s: $%,.2f%n%n",
            commissionEmployee, "earned", commissionEmployee.earnings());
        System.out.printf("%s%n%s: $%,.2f%n%n",
            basePlusCommissionEmployee,
            "earned", basePlusCommissionEmployee.earnings());

        // create four-element Employee array
        Employee[] employees = new Employee[4];

        // initialize array with Employees
        // upcasting
        employees[0] = salariedEmployee;
        employees[1] = hourlyEmployee;
        employees[2] = commissionEmployee;
        employees[3] = basePlusCommissionEmployee;

        System.out.printf("Employees processed polymorphically:%n%n");

        // generically process each element in array employees
        for (Employee currentEmployee : employees) {
            System.out.println(currentEmployee); // invokes toString

            // determine whether element is a BasePlusCommissionEmployee
            // upcasting 여부 확인
            if (currentEmployee instanceof BasePlusCommissionEmployee) {
                // downcast Employee reference to
                // BasePlusCommissionEmployee reference
                BasePlusCommissionEmployee employee =
                    // downcasting
                    (BasePlusCommissionEmployee) currentEmployee;

                employee.setBaseSalary(1.10 * employee.getBaseSalary());

                System.out.printf(
                    "new base salary with 10%% increase is: $%,.2f%n",
                    employee.getBaseSalary());
            }

            // polymorphic method call
            System.out.printf(
                "earned $%,.2f%n%n", currentEmployee.earnings());
        }

        // get type name of each object in employees array
        for (int j = 0; j < employees.length; j++) {
            System.out.printf("Employee %d is a %s%n", j,
                employees[j].getClass().getName());
        }
    }
}
```

- `getClass()`(from `java.lang.Object`) returns an object of type `Class`(from `java.lang`), which contains information about the object's type including its class name

```
Employees processed individually:

salaried employee: John Smith
social security number: 111-11-1111
weekly salary: $800.00
earned: $800.00

hourly employee: Karen Price
social security number: 222-22-2222
hourly wage: $16.75; hours worked: 40.00
earned: $670.00

commission employee: Sue Jones
social security number: 333-33-3333
gross sales: $10,000.00; commission rate: 0.06
earned: $600.00

base-salaried commission employee: Bob Lewis
social security number: 444-44-4444
gross sales: $5,000.00; commission rate: 0.04; base salary: $300.00
earned: $500.00

Employees processed polymorphically:

salaried employee: John Smith
social security number: 111-11-1111
weekly salary: $800.00
earned $800.00

hourly employee: Karen Price
social security number: 222-22-2222
hourly wage: $16.75; hours worked: 40.00
earned $670.00

commission employee: Sue Jones
social security number: 333-33-3333
gross sales: $10,000.00; commission rate: 0.06
earned $600.00

base-salaried commission employee: Bob Lewis
social security number: 444-44-4444
gross sales: $5,000.00; commission rate: 0.04; base salary: $300.00
new base salary with 10% increase is: $330.00
earned $530.00

Employee 0 is a SalariedEmployee
Employee 1 is a HourlyEmployee
Employee 2 is a CommissionEmployee
Employee 3 is a BasePlusCommissionEmployee
```

##### Dynamic binding (or late binding)

- All calls to method `toString` and `earnings` are resolved at execution time, based on the type of the object to which `currentEmployee` refers

- polymorphism을 사용하면 코드가 더 깔끔해진다.

### Exercise

<div hidden>
@startuml 10-class-diagram-5
skinparam classAttributeIconSize 0
class Animal {
	+ void show()
	+ void move()
}
class Fish {
	+ void show()
	+ void draw()
	+ void move()
}
class GoldFish {
	+ void draw()
	+ void move()
}

Fish -u-|> Animal
GoldFish -u-|> Fish
@enduml
</div>

<center markdown="block">
![class-diagram-5](/assets/java-programming/images/10-class-diagram-5.svg)

Class diagram
</center>

```java
public class AnimalTest {
    public static void main(String[] args) {
        // case 1.
        GoldFish goldFish = new GoldFish();
        goldFish.show();  // GoldFish: show()

        // case 2.
        Animal animal = new Fish();  // upcasting
        animal.draw();  // error

        // case 3.
        Animal animal2 = new Fish();  // upcasting
        animal2.show();  // Fish: show()
        animal2.move();  // Fish: move()

        // case 4.
        Animal animal3 = new GoldFish();  // upcasting
        ((Fish)animal3).draw();  // GoldFish: draw()
    }
}
```

> Common Programming Error 10.3
>
> Assigning a superclass variable to a subclass variable is a compilation error

> Common Programming Error 10.4
>
> When downcasting a reference, a `ClassCastException` occurs if the referenced object at execution time does not have an is-a relationship with the type specified in the cast operator

---

## 10.7 `final` Methods and Classes

### `final` method

- A `final` method in a superclass cannot  be overridden in a subclass

- `private` methods are implicitly `final`

- `static` methods are implicitly `final`

- Calls to `final` methods are resolved at compile time

	- static binding

### `final` class

- A `final` class cannot be a superclass

- All methods in a `final` class are implicitly `final`

- Class `String` is an example of a `final` class

	- Programs that use `String`s can rely on the functionality of `String` objects as specified in the Java API

- Making the class `final` also prevents programmers from creating subclasses that might bypass security restirctions

---

## 10.9 Creating and Using Interfaces

### Interface

- begins with the keyword `interface`

- conatains only constants and `abstract` methods

- All interface members must be `public`

	- All methods are implicitly `public abstract` methods

	- All fields are implicitly `public static final`

- An interface is often used when unrelated classes need to share common methods and constants

	- Allows objects of unrelated classes to be processed polymorphically by responding to the same method calls

- Interfaces are typically `public` types

	- A `public` interface must be declared in a file with the same name as the interface and the `.java` file-name extension

```java
public interface Payable {
	public static final int pay = 1000;
	public abstract double getPaymentAmount();
}
```

- `public static final`, `public abstract` is redundant

```java
public interface Payable {
	int pay = 1000;
	double getPaymentAmount();
}
```

### Implementing interface

- Implementing an interface with keyword implements

##### concrete class

- A class that implements all the methods in the interface with specified signature

##### abstract class

- A class that does not implements all the methods of the interface

- must be declared `abstract`

- An interface should be used in place of an `abstract` class

	- when there is no default implementation to inherit - that is, no fields and no concrete method implementations

### 10.9.1 Developing a `Payable` Hierarchy

<div hidden>
@startuml 10-payable-interface-hierachy
interface Payable
class Invoice implements Payable
abstract Employee implements Payable
class SalariedEmployee extends Employee
@enduml
</div>

<center markdown="block">
![payable-interface-hierachy](/assets/java-programming/images/10-payable-interface-hierachy.svg)

`Payable` interface hierarchy UML class diagram
</center>

### 10.9.2 Interface `Payable`

```java
// Fig. 10.11: Payable.java
// Payable interface declaration

public interface Payable {
	public abstract double getPaymentAmount();  // no implementation
}
```

- 관례적으로 모든 멤버가 `abstract`일 경우 `interface`를 사용한다.

### 10.9.3 Class `Invoice`

- Java allows a class to inherit from one superclass and impement as many interfaces as it needs

```java
public class ClassName extends SuperclassName implements Firstinterface, SecondInterface
```

```java
// Fig. 10.12: Invoice.java
// Invoice class that implements Payable.

public class Invoice implements Payable {
    private final String partNumber;
    private final String partDescription;
    private final int quantity;
    private final double pricePerItem;

    // constructor
    public Invoice(String partNumber, String partDescription, int quantity,
        double pricePerItem) {
        if (quantity < 0) { // validate quantity
            throw new IllegalArgumentException("Quantity must be >= 0");
        }

        if (pricePerItem < 0.0) { // validate pricePerItem
            throw new IllegalArgumentException(
                "Price per item must be >= 0");
        }

        this.quantity = quantity;
        this.partNumber = partNumber;
        this.partDescription = partDescription;
        this.pricePerItem = pricePerItem;
    }

    // get part number
    public String getPartNumber() {return partNumber;}

    // get description
    public String getPartDescription() {return partDescription;}

    // get quantity
    public int getQuantity() {return quantity;}

    // get price per item
    public double getPricePerItem() {return pricePerItem;}

    // return String representation of Invoice object
    @Override
    public String toString() {
        return String.format("%s: %n%s: %s (%s) %n%s: %d %n%s: $%,.2f",
            "invoice", "part number", getPartNumber(), getPartDescription(),
            "quantity", getQuantity(), "price per item", getPricePerItem());
    }

    // method required to carry out contract with interface Payable
    @Override
    public double getPaymentAmount() {
        return getQuantity() * getPricePerItem(); // calculate total cost
    }
}
```

> Software Engineering Observation 10.9
>
> All objects of a class that implements multiple interfaces have the is-a relationship with each implemented interface type

<div hidden>
@startuml 10-software-engineering-observation-9
interface A
interface B
class ExClass implements A
class ExClass implements B
@enduml
</div>

<center markdown="block">
![software-engineering-observation-9](/assets/java-programming/images/10-software-engineering-observation-9.svg)

An `ExClass` is an `A`

An `ExClass` is a `B`
</center>

### 10.9.4 Modifying Class `Employee` to Implement Interface `Payable`

```java
// Fig. 10.13: Employee.java
// Employee abstract superclass that implements Payable.

public abstract class Employee implements Payable {
    private final String firstName;
    private final String lastName;
    private final String socialSecurityNumber;

    // constructor
    public Employee(String firstName, String lastName,
        String socialSecurityNumber) {
        this.firstName = firstName;
        this.lastName = lastName;
        this.socialSecurityNumber = socialSecurityNumber;
    }

    // return first name
    public String getFirstName() {return firstName;}

    // return last name
    public String getLastName() {return lastName;}

    // return social security number
    public String getSocialSecurityNumber() {return socialSecurityNumber;}

    // return String representation of Employee object
    @Override
    public String toString() {
        return String.format("%s %s%nsocial security number: %s",
            getFirstName(), getLastName(), getSocialSecurityNumber());
    }

    // abstract method must be overridden by concrete subclasses
    public abstract double earnings(); // no implementation here

    // implementing getPaymentAmount here enables the entire Employee
    // class hierarchy to be used in an app that processes Payables
    public double getPaymentAmount() {return earnings();}
}
```

```java
// Fig. 10.5: SalariedEmployee.java
// SalariedEmployee concrete class extends abstract class Employee.

public class SalariedEmployee extends Employee {
    private double weeklySalary;

    // constructor
    public SalariedEmployee(String firstName, String lastName,
        String socialSecurityNumber, double weeklySalary) {
        super(firstName, lastName, socialSecurityNumber);

        if (weeklySalary < 0.0) {
            throw new IllegalArgumentException(
                "Weekly salary must be >= 0.0");
        }

        this.weeklySalary = weeklySalary;
    }

    // set salary
    public void setWeeklySalary(double weeklySalary) {
        if (weeklySalary < 0.0) {
            throw new IllegalArgumentException(
                "Weekly salary must be >= 0.0");
        }

        this.weeklySalary = weeklySalary;
    }

    // return salary
    public double getWeeklySalary() {return weeklySalary;}

    // calculate earnings; override abstract method earnings in Employee
    @Override
    public double earnings() {return getWeeklySalary();}

    // return String representation of SalariedEmployee object
    @Override
    public String toString() {
        return String.format("salaried employee: %s%n%s: $%,.2f",
            super.toString(), "weekly salary", getWeeklySalary());
    }
}
```

> Software Engineering Observation 10.11
>
> The is-a relationship that exists between superclasses and subclasses, and between interfaces and the classes that implement them, holds when passing an object to a method. When a method parameter receives an argument of a superclass or interface type, the method polymorphically processes the object received as an argument

### How to polymorphically invoke methods

1. Using a superclass reference, we can polymorphically invoke

	1. Any method declared in the superclass

	2. any method declared its supclasses(e.g., `Oject`)

<div hidden>
@startuml 10-class-diagram-6
interface TestInterface
class Object
class Invoice
abstract Employee
class OffInvoice
class ComInvoice
class SalariedEmployee

Payable -u-|> TestInterface
class Invoice implements Payable
abstract Employee implements Payable
Invoice -u-|> Object
Employee -u-|> Object
OffInvoice -u-|> Invoice
ComInvoice -u-|> Invoice
SalariedEmployee -u-|> Employee

Invoice -[hidden]> Employee
@enduml
</div>

<center markdown="block">
![class-diagram-6](/assets/java-programming/images/10-class-diagram-6.svg)

Class diagram
</center>

2. Using aninterface reference, we can polymorphically invoke

	1. Any method declared in the interface

	2. Any method declared its superinterfaces

	3. Any method declared in class `Object`

### 10.9.5 Using Interface `Payable` to Process `Invoice`s and `Employee`s Polymorphically

```java
// Fig. 10.14: PayableInterfaceTest.java
// Payable interface test program processing Invoices and
// Employees polymorphically.
public class PayableInterfaceTest {
   public static void main(String[] args) {
      // create four-element Payable array
      Payable[] payableObjects = new Payable[] {
         new Invoice("01234", "seat", 2, 375.00),
         new Invoice("56789", "tire", 4, 79.95),
         new SalariedEmployee("John", "Smith", "111-11-1111", 800.00),
         new SalariedEmployee("Lisa", "Barnes", "888-88-8888", 1200.00)
      };

      System.out.println(
         "Invoices and Employees processed polymorphically:");

      // generically process each element in array payableObjects
      for (Payable currentPayable : payableObjects) {
         // output currentPayable and its appropriate payment amount
         System.out.printf("%n%s %npayment due: $%,.2f%n",
            currentPayable.toString(), // could invoke implicitly
            currentPayable.getPaymentAmount());
      }
   }
}
```

<div hidden>
@startuml 10-class-diagram-7
skinparam classAttributeIconSize 0
interface Payable {
	+ {abstract} double getPaymentAmount()
}
class Object {
	+ String toString()
}
class Invoice {
	+ String toString()
	+ double getPaymentAmount()
}
abstract Employee {
	+ {abstract} double earnings()
	+ String toString()
	+ double getPaymentAmount()
}
class SalariedEmployee {
	+ double earnings()
	+ String toString()
}

class Invoice implements Payable
abstract Employee implements Payable
Invoice -u-|> Object
Employee -u-|> Object
SalariedEmployee -u-|> Employee

Invoice -[hidden]> Employee
@enduml
</div>

<center markdown="block">
![class-diagram-7](/assets/java-programming/images/10-class-diagram-7.svg)

Class diagram
</center>

```
Invoices and Employees processed polymorphically:

invoice:
part number: 01234 (seat)
quantity: 2
price per item: $375.00
payment due: $750.00

invoice:
part number: 56789 (tire)
quantity: 4
price per item: $79.95
payment due: $319.80

salaried employee: John Smith
social security number: 111-11-1111
weekly salary: $800.00
payment due: $800.00

salaried employee: Lisa Barnes
social security number: 888-88-8888
weekly salary: $1,200.00
payment due: $1,200.00
```

### 10.9.6 Some Common Interfaces of the Java API

- The Java API's interfaces enable you to use your own classes within the frameworks provided by Java

- Figure 10.15 presents a brief overview of a few of the more popular interfaces of the Java API

<table>
	<thead>
		<tr>
			<th>Interface</th>
			<th>Description</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td><span markdown=1>`Comparable`</span></td>
			<td><span markdown=1>Intreface `Comparable` is used to allow objects of a class that `implements` the interface to be compared to one another.</span></td>
		</tr>
		<tr>
			<td><span markdown=1>`Serializable`</span></td>
			<td><span markdown=1>An interface used to identify classes whose objects can be written to (i.e., serialized) or read from (i.e., deserialized) some type of storage (e.g., file on disk, database field) or transmitted across a network</span></td>
		</tr>
		<tr>
			<td><span markdown=1>`Runnable`</span></td>
			<td><span markdown=1>Implemented by any class that represents a taskto perform. Objects of such a class areoften executed in parallel using a technique called multithreading. The interface contains one method, `run`, which specifies the behavior of an object when executed</span></td>
		</tr>
		<tr>
			<td><span markdown=1>GUI event-listener interfaces</span></td>
			<td><span markdown=1>Interactions in gui is known as an event, and the code that is used to respond to an event is known as an event handler. Event handlers are declared in classes that implement an appropriate event-listener interface.</span></td>
		</tr>
		<tr>
			<td><span markdown=1>`AutoCloseable`</span></td>
			<td><span markdown=1>Implemented by classes that can be used with the `try`-with-resources statement to help prevent resource leaks.</span></td>
		</tr>
	</tbody>
</table>

## 10.10 Java SE 8 Interfaces Enhancements

- This section introduces interface features that were added in Java SE 8. We discuss these in more detail in later chapters

### 10.10.1 `default` Interface Methods

### 10.10.2 `static` Interface Methods

### 10.10.3 Functional Interfaces

## 10.11 Java SE 9 `private` Interfaces Methods

## 10.12 `private` Constructors
