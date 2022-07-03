---
layout: default
title: Ch9 Object-Oriented Programming - Inheritance
parent: Java Programming
grand_parent: School Lecture
nav_order: 10
mathjax: true
mermaid: true
permalink: /docs/java/ch9
---

# Ch9 Object-Oriented Programming - Inheritance
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

- Understand inheritance and how to use it to develop new classes based on existing classes

- Learn the notions of wuperclasses and subclasses and the relationship between them

- Use keyword `extends` to create a class that inherits attributes and behaviors from another class

- Use access modifier `protected` in a superclass to give subclass methods access to these supterclass members

- Access superclass members with `super` from a subclss

- Learn how constructors are used in inheritance hierachies

- Learn about the methods of class `Object`, the direct or indirect superclass of all classes

---

## 9.1 Introduction

### Inheritance (or Specialization)

- a form of software reuse

<div class=mermaid>
graph BT;
    Subclass["Subclass<br>New class"] --> superclass["Superclasse<br>Existing class"];
</div>

- The new class should inherit the members of an existing class

- Each subclass can be a superclass of future subclasses

- A subclass can add its own fields and methods

- A subclass is more specific than its superclass

- The Java class hierarchy begins with class `Object` (in package `java.lang`)

    - Every class in Java directly or indirectly `extends` (or "inherits from") `Object`

- Java supports only single inheritance

##### Is-a relationship represents Inheritance

- In an is-a relationship, an object of a subclass can also be treated as an object of its superclass

##### Has-a relationship represents composition

- In a has-a relationship, an object contains as members references to other objects

---

## 9.2 Superclasses and Subclasses

<center markdown="block">
![inheritance-hierarchy-classs-diagram](/assets/java-programming/images/9-inheritance-hierarchy-classs-diagram.png)

Inheritance hierarchy class diagram
</center>

- Each arrow in the hierarchy represents an is-a relationship

- Starting from the bottom, you can follow the arrows and apply the is-a relationship up to the topmost superclass

---

## 9.3 Access Modifier

- `private`, `default`, `protected`, `public`

### Access Modifiers affect the accessibility at two levels

- Class (top level)

    - `public`, `default`

- Members (methods andfields)

    - `public`, `protected`, `default`, `private`

<center markdown="block">
![access-modifier](/assets/java-programming/images/9-access-modifier.png)

Access modifier
</center>

---

## 9.4 Relationship between Superclasses and Subclasses

- Inheritance hierarchy containinng types of employewws in a company's payroll application

    - Commission employees

        - are paid a percentage of their sales.

    - Base-salaried commission employees

        - receive a base salary plus a percentage of their sales

### 9.4.1 Creating and Using a `CommissionEmployee` Class

- Class `CommissionEmployee` (Fig. 9.4) `extends` class `Object` (from package `java.lang`)

    - `CommissionEmployee` inherits `Object`’s methods.

    - If you don’t explicitly specify which class a new class extends, the class extends `Object` implicitly

```java
// Fig. 9.4: CommissionEmployee.java
// CommissionEmployee class represents an employee paid a
// percentage of gross sales.
public class CommissionEmployee extends Object {
   private final String firstName;
   private final String lastName;
   private final String socialSecurityNumber;
   private double grossSales; // gross weekly sales
   private double commissionRate; // commission percentage

   // five-argument constructor
   public CommissionEmployee(String firstName, String lastName,
      String socialSecurityNumber, double grossSales,
      double commissionRate) {
      // implicit call to Object's default constructor occurs here

      // if grossSales is invalid throw exception
      if (grossSales < 0.0) {
         throw new IllegalArgumentException("Gross sales must be >= 0.0");
      }

      // if commissionRate is invalid throw exception
      if (commissionRate <= 0.0 || commissionRate >= 1.0) {
         throw new IllegalArgumentException(
            "Commission rate must be > 0.0 and < 1.0");
      }

      this.firstName = firstName;
      this.lastName = lastName;
      this.socialSecurityNumber = socialSecurityNumber;
      this.grossSales = grossSales;
      this.commissionRate = commissionRate;
   }

   // return first name
   public String getFirstName() {return firstName;}

   // return last name
   public String getLastName() {return lastName;}

   // return social security number
   public String getSocialSecurityNumber() {return socialSecurityNumber;}

   // set gross sales amount
   public void setGrossSales(double grossSales) {
      if (grossSales < 0.0) {
         throw new IllegalArgumentException("Gross sales must be >= 0.0");
      }

      this.grossSales = grossSales;
   }

   // return gross sales amount
   public double getGrossSales() {return grossSales;}

   // set commission rate
   public void setCommissionRate(double commissionRate) {
      if (commissionRate <= 0.0 || commissionRate >= 1.0) {
         throw new IllegalArgumentException(
            "Commission rate must be > 0.0 and < 1.0");
      }

      this.commissionRate = commissionRate;
   }

   // return commission rate
   public double getCommissionRate() {return commissionRate;}

   // calculate earnings
   public double earnings() {return commissionRate * grossSales;}

   // return String representation of CommissionEmployee object
   @Override // indicates that this method overrides a superclass method
   public String toString() {
      return String.format("%s: %s %s%n%s: %s%n%s: %.2f%n%s: %.2f",
         "commission employee", firstName, lastName,
         "social security number", socialSecurityNumber,
         "gross sales", grossSales,
         "commission rate", commissionRate);
   }
}
```

- Constructors are not inherited

- The first task of a subclss constructor is to call its direct superclass's constructor explicitly or implicitly

    - The instance variables inherited from the superclass are initialized properly.

- If the code does not include an explicit call to the superclass constructor, Java implicitly calls the superclass’s default or no- argument constructor.

- A class’s default constructor calls the superclass’s default or no- argument constructor.

- Class `Object`'s `toString` method

    - returns a String that includes the name of the object’s class.

    - can be overridden by a subclass to specify an appropriate
String representation

    - called implicitly whenever an object must be converted to a

- Q. if the `toString` method in Fig.9.4 is omitted?
String representation.

- To override a superclass method

    - a subclass must declare a method with the same signature as the superclass method

- `@Override` annotation

    - indicates that a method should override a superclass method with the same signature

    - if it does not, a compilation error occurs

```java
// Fig. 9.5: CommissionEmployeeTest.java
// CommissionEmployee class test program.
public class CommissionEmployeeTest {
   public static void main(String[] args) {
      // instantiate CommissionEmployee object
      CommissionEmployee employee = new CommissionEmployee(
         "Sue", "Jones", "222-22-2222", 10000, .06);

      // get commission employee data
      System.out.println("Employee information obtained by get methods:");
      System.out.printf("%n%s %s%n", "First name is",
         employee.getFirstName());
      System.out.printf("%s %s%n", "Last name is",
         employee.getLastName());
      System.out.printf("%s %s%n", "Social security number is",
         employee.getSocialSecurityNumber());
      System.out.printf("%s %.2f%n", "Gross sales is",
         employee.getGrossSales());
      System.out.printf("%s %.2f%n", "Commission rate is",
         employee.getCommissionRate());

      employee.setGrossSales(5000);
      employee.setCommissionRate(.1);

      System.out.printf("%n%s:%n%n%s%n",
         "Updated employee information obtained by toString", employee);
   }
}
```

```
Employee information obtained by get methods:

First name is Sue
Last name is Jones
Social security number is 222-22-2222
Gross sales is 10000.00
Commission rate is 0.06

Updated employee information obtained by toString:

commission employee: Sue Jones
social security number: 222-22-2222
gross sales: 5000.00
commission rate: 0.10
```

```
Employee information obtained by get methods:

First name is Sue
Last name is Jones
Social security number is 222-22-2222
Gross sales is 10000.00
Commission rate is 0.06

Updated employee information obtained by toString:

CommissionEmployee@38cccef
```

- `toString` override 안했을 때

### 9.4.2 Creating and Using a `BasePlusCommissionEmployee` Class

- Class BasePlusCommissionEmployee (Fig. 9.6)

    - Most of the members are in common with class CommissionEmployee.

    - Class BasePlusCommissionEmployee implicitly extends Object.
    - The constructor invokes class Object’s default constructor implicitly.

```java
// Fig. 9.6: BasePlusCommissionEmployee.java
// BasePlusCommissionEmployee class represents an employee who receives
// a base salary in addition to commission.
public class BasePlusCommissionEmployee {
   private final String firstName;
   private final String lastName;
   private final String socialSecurityNumber;
   private double grossSales; // gross weekly sales
   private double commissionRate; // commission percentage
   private double baseSalary; // base salary per week

   // six-argument constructor
   public BasePlusCommissionEmployee(String firstName, String lastName,
      String socialSecurityNumber, double grossSales,
      double commissionRate, double baseSalary) {
      // implicit call to Object's default constructor occurs here

      // if grossSales is invalid throw exception
      if (grossSales < 0.0) {
         throw new IllegalArgumentException("Gross sales must be >= 0.0");
      }

      // if commissionRate is invalid throw exception
      if (commissionRate <= 0.0 || commissionRate >= 1.0) {
         throw new IllegalArgumentException(
            "Commission rate must be > 0.0 and < 1.0");
      }

      // if baseSalary is invalid throw exception
      if (baseSalary < 0.0) {
         throw new IllegalArgumentException("Base salary must be >= 0.0");
      }

      this.firstName = firstName;
      this.lastName = lastName;
      this.socialSecurityNumber = socialSecurityNumber;
      this.grossSales = grossSales;
      this.commissionRate = commissionRate;
      this.baseSalary = baseSalary;
   }

   // return first name
   public String getFirstName() {return firstName;}

   // return last name
   public String getLastName() {return lastName;}

   // return social security number
   public String getSocialSecurityNumber() {return socialSecurityNumber;}

   // set gross sales amount
   public void setGrossSales(double grossSales) {
      if (grossSales < 0.0) {
         throw new IllegalArgumentException("Gross sales must be >= 0.0");
      }

      this.grossSales = grossSales;
   }

   // return gross sales amount
   public double getGrossSales() {return grossSales;}

   // set commission rate
   public void setCommissionRate(double commissionRate) {
      if (commissionRate <= 0.0 || commissionRate >= 1.0) {
         throw new IllegalArgumentException(
            "Commission rate must be > 0.0 and < 1.0");
      }

      this.commissionRate = commissionRate;
   }

   // return commission rate
   public double getCommissionRate() {return commissionRate;}

   // set base salary
   public void setBaseSalary(double baseSalary) {
      if (baseSalary < 0.0) {
         throw new IllegalArgumentException("Base salary must be >= 0.0");
      }

      this.baseSalary = baseSalary;
   }

   // return base salary
   public double getBaseSalary() {return baseSalary;}

   // calculate earnings
   public double earnings() {
      return baseSalary + (commissionRate * grossSales);
   }

   // return String representation of BasePlusCommissionEmployee
   @Override
   public String toString() {
      return String.format(
         "%s: %s %s%n%s: %s%n%s: %.2f%n%s: %.2f%n%s: %.2f",
         "base-salaried commission employee", firstName, lastName,
         "social security number", socialSecurityNumber,
         "gross sales", grossSales, "commission rate", commissionRate,
         "base salary", baseSalary);
   }
}
```

```java
// Fig. 9.7: BasePlusCommissionEmployeeTest.java
// BasePlusCommissionEmployee test program.

public class BasePlusCommissionEmployeeTest {
   public static void main(String[] args) {
      // instantiate BasePlusCommissionEmployee object
      BasePlusCommissionEmployee employee =
         new BasePlusCommissionEmployee(
         "Bob", "Lewis", "333-33-3333", 5000, .04, 300);

      // get base-salaried commission employee data
      System.out.printf(
         "Employee information obtained by get methods:%n");
      System.out.printf("%s %s%n", "First name is",
         employee.getFirstName());
      System.out.printf("%s %s%n", "Last name is",
         employee.getLastName());
      System.out.printf("%s %s%n", "Social security number is",
         employee.getSocialSecurityNumber());
      System.out.printf("%s %.2f%n", "Gross sales is",
         employee.getGrossSales());
      System.out.printf("%s %.2f%n", "Commission rate is",
         employee.getCommissionRate());
      System.out.printf("%s %.2f%n", "Base salary is",
         employee.getBaseSalary());

      employee.setBaseSalary(1000);

      System.out.printf("%n%s:%n%n%s%n",
         "Updated employee information obtained by toString",
          employee.toString());
   }
}
```

```
Employee information obtained by get methods:
First name is Bob
Last name is Lewis
Social security number is 333-33-3333
Gross sales is 5000.00
Commission rate is 0.04
Base salary is 300.00

Updated employee information obtained by toString:

base-salaried commission employee: Bob Lewis
social security number: 333-33-3333
gross sales: 5000.00
commission rate: 0.04
base salary: 1000.00
```

- Much of BasePlusCommissionEmployee’s code is similar, or identical, to that of CommissionEmployee.

    - This “copy-and-paste” approach is often error prone and time consuming.

### 9.4.3 Creating a CommissionEmployee-BasePlusCommissionEmployee Inheritance Hierarchy

```java
// Fig. 9.8: BasePlusCommissionEmployee.java
// private superclass members cannot be accessed in a subclass.
public class BasePlusCommissionEmployee extends CommissionEmployee {
   private double baseSalary; // base salary per week

   // six-argument constructor
   public BasePlusCommissionEmployee(String firstName, String lastName,
      String socialSecurityNumber, double grossSales,
      double commissionRate, double baseSalary) {
      // explicit call to superclass CommissionEmployee constructor
      super(firstName, lastName, socialSecurityNumber,
         grossSales, commissionRate);

      // if baseSalary is invalid throw exception
      if (baseSalary < 0.0) {
         throw new IllegalArgumentException("Base salary must be >= 0.0");
      }

      this.baseSalary = baseSalary;
   }

   // set base salary
   public void setBaseSalary(double baseSalary) {
      if (baseSalary < 0.0) {
         throw new IllegalArgumentException("Base salary must be >= 0.0");
      }

      this.baseSalary = baseSalary;
   }

   // return base salary
   public double getBaseSalary() {return baseSalary;}

   // calculate earnings
   @Override
   public double earnings() {
      // not allowed: commissionRate and grossSales private in superclass
      return baseSalary + (commissionRate * grossSales);
   }

   // return String representation of BasePlusCommissionEmployee
   @Override
   public String toString() {
      // not allowed: attempts to access private superclass members
      return String.format(
         "%s: %s %s%n%s: %s%n%s: %.2f%n%s: %.2f%n%s: %.2f",
         "base-salaried commission employee", firstName, lastName,
         "social security number", socialSecurityNumber,
         "gross sales", grossSales, "commission rate", commissionRate,
         "base salary", baseSalary);
   }
}
```

```
BasePlusCommissionEmployee.java:38: error: commissionRate has private access in CommissionEmployee
      return baseSalary + (commissionRate * grossSales);
                           ^
BasePlusCommissionEmployee.java:38: error: grossSales has private access in CommissionEmployee
      return baseSalary + (commissionRate * grossSales);
                                            ^
BasePlusCommissionEmployee.java:47: error: firstName has private access in CommissionEmployee
         "base-salaried commission employee", firstName, lastName,
                                              ^
BasePlusCommissionEmployee.java:47: error: lastName has private access in CommissionEmployee
         "base-salaried commission employee", firstName, lastName,
                                                         ^
BasePlusCommissionEmployee.java:48: error: socialSecurityNumber has private access in CommissionEmployee
         "social security number", socialSecurityNumber,
                                   ^
BasePlusCommissionEmployee.java:49: error: grossSales has private access in CommissionEmployee
         "gross sales", grossSales, "commission rate", commissionRate,
                        ^
BasePlusCommissionEmployee.java:49: error: commissionRate has private access in CommissionEmployee
         "gross sales", grossSales, "commission rate", commissionRate,
                                                       ^
7 errors
```

- If the subclass constructor did not invoke the superclass’s
constructor explicitly, Java would attempt to invoke the
superclass’s no-argument or default constructor.

    - Class CommissionEmployee does not have such a constructor, so the compiler would issue an error.

### 9.4.4 `CommissionEmployee-BasePlusCommissionEmployee` Inheritance Hierarchy Using `protected` Inheritance Variables

- New CommissionEmployee class

    ```java
    protected String firstName;
    protected String lastName;
    protected String socialSecurityNumber;
    protected double grossSales;
    protected double commissionRate;
    ```

- with `protected` instance variables, the subclass gets access to the instance variables

```java
// Fig. 9.9: BasePlusCommissionEmployee.java
// BasePlusCommissionEmployee inherits protected instance
// variables from CommissionEmployee.

public class BasePlusCommissionEmployee extends CommissionEmployee {
   private double baseSalary; // base salary per week

   // six-argument constructor
   public BasePlusCommissionEmployee(String firstName, String lastName,
      String socialSecurityNumber, double grossSales,
      double commissionRate, double baseSalary) {
      super(firstName, lastName, socialSecurityNumber,
         grossSales, commissionRate);

      // if baseSalary is invalid throw exception
      if (baseSalary < 0.0) {
         throw new IllegalArgumentException("Base salary must be >= 0.0");
      }

      this.baseSalary = baseSalary;
   }

   // set base salary
   public void setBaseSalary(double baseSalary) {
      if (baseSalary < 0.0) {
         throw new IllegalArgumentException("Base salary must be >= 0.0");
      }

      this.baseSalary = baseSalary;
   }

   // return base salary
   public double getBaseSalary() {return baseSalary;}

   // calculate earnings
   @Override // indicates that this method overrides a superclass method
   public double earnings() {
      return baseSalary + (commissionRate * grossSales);
   }

   // return String representation of BasePlusCommissionEmployee
   @Override
   public String toString() {
      return String.format(
         "%s: %s %s%n%s: %s%n%s: %.2f%n%s: %.2f%n%s: %.2f",
         "base-salaried commission employee", firstName, lastName,
         "social security number", socialSecurityNumber,
         "gross sales", grossSales, "commission rate", commissionRate,
         "base salary", baseSalary);
   }
}
```

### Problems with protected instance variables

1. The subclass object can set an inherited variable’s value
directly without using a set method.

    - A subclass object can assign an invalid value to the variable.

2. Subclass methods depend on the superclass’s data
implementation.

    - Subclass should depend only on the superclass service and not on the superclass data implementation.

3. A class’s protected members are visible to all classes in the same package.

- In most cases, it’s better to use private instance variables

    - Code will be easier to maintain, modify and debug.

### 9.4.5 `CommissionEmployee-BasePlusCommissionEmployee` Inheritance Hierarchy Use `private` Inheritance Variables

- Class `CommissionEmployee`

    ```java
    private String firstName;
    private String lastName;
    private String socialSecurityNumber;
    private double grossSales;
    private double commissionRate;
    ```

    - `public` methods for manipulating these private instance variables

```java
// Fig. 9.10: CommissionEmployee.java
// CommissionEmployee class uses methods to manipulate its
// private instance variables.
public class CommissionEmployee {
   private final String firstName;
   private final String lastName;
   private final String socialSecurityNumber;
   private double grossSales; // gross weekly sales
   private double commissionRate; // commission percentage

   // five-argument constructor
   public CommissionEmployee(String firstName, String lastName,
      String socialSecurityNumber, double grossSales,
      double commissionRate) {
      // implicit call to Object constructor occurs here

      // if grossSales is invalid throw exception
      if (grossSales < 0.0) {
         throw new IllegalArgumentException("Gross sales must be >= 0.0");
      }

      // if commissionRate is invalid throw exception
      if (commissionRate <= 0.0 || commissionRate >= 1.0) {
         throw new IllegalArgumentException(
            "Commission rate must be > 0.0 and < 1.0");
      }

      this.firstName = firstName;
      this.lastName = lastName;
      this.socialSecurityNumber = socialSecurityNumber;
      this.grossSales = grossSales;
      this.commissionRate = commissionRate;
   }

   // return first name
   public String getFirstName() {return firstName;}

   // return last name
   public String getLastName() {return lastName;}

   // return social security number
   public String getSocialSecurityNumber() {return socialSecurityNumber;}

   // set gross sales amount
   public void setGrossSales(double grossSales) {
      if (grossSales < 0.0) {
         throw new IllegalArgumentException("Gross sales must be >= 0.0");
      }

      this.grossSales = grossSales;
   }

   // return gross sales amount
   public double getGrossSales() {return grossSales;}

   // set commission rate
   public void setCommissionRate(double commissionRate) {
      if (commissionRate <= 0.0 || commissionRate >= 1.0) {
         throw new IllegalArgumentException(
            "Commission rate must be > 0.0 and < 1.0");
      }

      this.commissionRate = commissionRate;
   }

   // return commission rate
   public double getCommissionRate() {return commissionRate;}

   // calculate earnings
   public double earnings() {
      return getCommissionRate() * getGrossSales();
   }

   // return String representation of CommissionEmployee object
   @Override
   public String toString() {
      return String.format("%s: %s %s%n%s: %s%n%s: %.2f%n%s: %.2f",
         "commission employee", getFirstName(), getLastName(),
         "social security number", getSocialSecurityNumber(),
         "gross sales", getGrossSales(),
         "commission rate", getCommissionRate());
   }
}
```

- Q. Methods `earnings` and `toString` use the class’s get methods to obtain the values of its instance variables. Why is this better?

    - A. Localizing the effects of changes to instance variable

- Class BasePlusCommissionEmployee (Fig. 9.11)

    -  Methods earnings and toString

        - each invoke their superclass versions and

        - do not access instance variables directly.

    - inherits its superclass’s non-private methods and can
access the private superclass members via those methods.

```java
// Fig. 9.11: BasePlusCommissionEmployee.java
// BasePlusCommissionEmployee class inherits from CommissionEmployee
// and accesses the superclass s private data via inherited
// public methods.
public class BasePlusCommissionEmployee extends CommissionEmployee {
   private double baseSalary; // base salary per week

   // six-argument constructor
   public BasePlusCommissionEmployee(String firstName, String lastName,
      String socialSecurityNumber, double grossSales,
      double commissionRate, double baseSalary) {
      super(firstName, lastName, socialSecurityNumber,
         grossSales, commissionRate);

      // if baseSalary is invalid throw exception
      if (baseSalary < 0.0) {
         throw new IllegalArgumentException("Base salary must be >= 0.0");
      }

      this.baseSalary = baseSalary;
   }

   // set base salary
   public void setBaseSalary(double baseSalary) {
      if (baseSalary < 0.0) {
         throw new IllegalArgumentException("Base salary must be >= 0.0");
      }

      this.baseSalary = baseSalary;
   }

   // return base salary
   public double getBaseSalary() {return baseSalary;}

   // calculate earnings
   @Override
   public double earnings() {return getBaseSalary() + super.earnings();}

   // return String representation of BasePlusCommissionEmployee
   @Override
   public String toString() {
      return String.format("%s %s%n%s: %.2f", "base-salaried",
         super.toString(), "base salary", getBaseSalary());
   }
}
```

- Q. If super is omitted?

    - A. Infinite recursion

- Q. `super.earnings()`, why is this better?

    - A. To aoid duplication the code an d reduce maintenance problems

---

## 9.5 Constructors in Subclasses

- Instantiating a subclass object begins a chain of constructor calls

    - The subclass constructor, before performing its own tasks, invokes its direct superclass’s constructor.

- The last constructor called in the chain is always class Object’s constructor.

- Original subclass constructor’s body finishes executing last.

- Each superclass’s constructor manipulates the superclass instance variables that the subclass object inherits.


---

## 9.6 `Object` Class

- all classes in Java inherit directly or indirectly from Object, so its 11 methods are inherited by all other classes.

- Every array has an overridden clone method that copies the
array.

    - If the array stores references to objects, the objects are not copied—a shallow copy is performed

<center markdown="block">
![object-methods1](/assets/java-programming/images/9-object-methods1.png)

![object-methods2](/assets/java-programming/images/9-object-methods2.png)

![object-methods3](/assets/java-programming/images/9-object-methods3.png)

Object methods
</center>
