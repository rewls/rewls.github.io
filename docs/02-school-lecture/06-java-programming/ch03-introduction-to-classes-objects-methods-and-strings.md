---
layout: default
title: Ch3 Introduction to Classes, Objects, Methods and Strings
parent: Java Programming
grand_parent: School Lecture
nav_order: 4
mathjax: true
mermaid: true
permalink: /docs/java/ch3
---

# Ch3 Introduction to Classes, Objects, Methods and Strings
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

- Declare a class and use it to create an object

- Implement a class's behaviors as methods

- Implement a class's attributes as instance variables

- Call an object's methods to make them perform their tasks

- Learn what local variables of a method are and how they differ from instance variables

- Learn what primitive types and reference types are

- Use a constructor to initialize an object's data

- Represent and use numbers containing decimal points

- Learn why classes are a natural way to model real-world things and abstract entities

---

## 3.2 Instance Variables, `set` Methods and `get` Methods

### 3.2.1 Account Class with an Instance Variable, a  `set` Method and a `get` method

```java
// Fig. 3.1: Account.java
// Account class that contains a name instance variable and methods to set and get its value

public class Account {
    private String name;  // instance variable
    // default value for an instance variable of type String - null

    // method to set the name in the object
    public void setName(String name) {
        this.name = name;  // store the name
    }

    // method to retrieve the name from the object
    public String getName() {
        return name;  // return value of name to caller
    }
}
```

##### Class `Account`

- Each class declaration with keyword `public`

    - must be stored in a file with the same name as the class

- Access modifier `public`

    - the class is available to the public

- is not an application because it does not contain `main`

- can't execute `Account`; will receive an error messge

##### Instance Variable `name`

- Each object(instance) of the class has its own copy of the class's instance variables

- Variables or methods declared with access modifier `private`

    - accessible only to methods of the class in which they're declared

> Good Programming Practice 3.1
>
> We prefer to list a class's instance variables first in the class's body. You can list the class's instance variables anywhere in the class outside ints method declarations

##### `setName` Method of Class `Account`

- access modifier `public`

    - The method is available to the public

    - It can be called from methods of other classes

##### Method names

- by convention, begin with a lowercase first letter and

- subsequent words int the name begin with a capital letter.

##### Parameters Are Local Variables

- local variables

    - Variables declared in the body of a particular method

    - are not automatically initialized

    - When a method terminates, the values of its local variables are lepost

##### `setName` Method body

- Keyword `this`

    - is used to refer to the shadowed instance variable explicitly

##### `getName` Method of Class `Account`

- Empty parentheses after the method name

    - the method does not require additional information to perform its task

### 3.2.2 AccountTest Class That Creates and Uses an Object of Class Account

##### Driver Class `AccountTest`

- A class that creates an object of another class, then calls the object's methods, is a driver class

- a separate class containing method `main` to test each new class

```java
// Fig. 3.2: AccountTest.java
// Creating and manipulating an Account object

import java.util.Scanner;

public class AccountTest {
    public static void main(String[] args) {
        // create a Scanner object to obtain input from the command window
        Scanner input = new Scanner(System.in);

        // create an Account object and assign it to myAccount
        Account myAccount = new Account();  // calls default constructor

        // display initial value of name (null)
        System.out.printf("Initial name is: %s%n%n", myAccount.getName());

        // prompt for and read name
        System.out.println("Please enter the name:");
        String theName = input.nextLine();  // read a line of text
        myAccount.setName(theName);  // put theName in myAccount
        System.out.println();  // outputs a blank line

        // display the name stored in object myAccount
        System.out.printf("Name in object myAccount is:%n%s%n", myAccount.getName());
    }
}
```

```
Initial name is: null

Please enter the name:
Jane Green

Name in object myAccount is:
Jane Green
```

##### `Scanner` object for receiging input from the user

- `Scanner` method `nextLine`

    - reads characters until a newline character is encountered, then returns the characters as `String`

    - the newline chracter is discarded

- `Scanner` method `next`

    - reads characters until any white-space character is encountered, then returns the characters a `String`

    - the white-space character is discarded

##### Instantiating an object - keyword `new` and Constructors

- A class instance creation expression begins with keyword `new` and creats a new object

- a constructor is similar to a method but is called implicitly by the new operator to initialize an object's instance variables at the time the object is created

##### Calling method

- To call a method of an object, follow the object name with a dot separator, the method name and a set of parentheses containing the method's arguments

- The argument types in the method call must be consistent with the types of the corresponding parameters in the method's declaration

##### Default initial value of instance variable

- Local variables ar not automatically initialized

- Every instance variable has a default initial value

    - a value provided by Java when you do not specify the instance variable's initial value

- The default value for an instance variable of type `String` is null

### 3.2.3 Compiling and Executing an App with Multiple Classes

- Any class can contain a `main` method

    - The JVM invokes the `main` method only in the class used to execute the application

### 3.2.4 Account UML class diagram

<center markdown="block">
![class-diagram-account](/assets/java-programming/images/3-class-diagram-account-fig_03-01.png)

Class diagram for class `Account` of Fig. 3.1.
</center>

- Top compartment: class's name

- Middle compartment: class's attributes - instance variables

- Bottom compartment: class's operations - methods

- -: corresponds to the `private`

- +: corresponds to the `public`

### 3.2.5 Additional Notes on Class AccountTest

##### static Method `main`

- A key part of enabling the JVM to locate and call method `main` to begin the app's execution is the `static` keyword, which indicates that `main` is a `static` method that can be called without first creating an object of the class in which the method is declared

##### Notes on `import` declarations

- Most classes you'll use must be imported explicitly

- Classes taht ar implicitly imported

    - The classes in package `java.lang`

        - ex) `System` and `String`

    - Class that are compiled in the same directory are consideredto be in the samd package - known as the default package

- An `import` declaration is not required if you always refer to a class via its fully qualified class name

    - `java.util.Scanner input = new java.util.Scanner(System.in);`

### 3.2.6 Software Engineering with `private` Insctance Variables and `public` `set` and `get` Methods

##### Data hiding or information hiding

- `private` instance variables are hidden inside the object and can be accessed only by methods of the object's class

---

## 3.3 Account Class: Initializing Objects with Constructors

```java
// Fig. 3.5: Account.java
// Account class with a constructor that initializes the name

public class Account {
    private String name;  // instance variable

    // constructor initializes name sith parameter name. no return type
    public Account(String name) {  // constructor name is class name
        this.name = name;
    }

    // method to set the name
    public void setName(String name) {
        this.name = name;  // store the name
    }

    // method to retrieve the name
    public String getName() {
        return name;  // return value of name to caller
    }
}
```

```java
// Fig. 3.6: AccountTest.java
// Using the Account constructor to initialize th name instance variable at the time each Account object is created

public class AccountTest {
	public static void main(String[] args) {
		// create two Account objects
		Account account1 = new Account("Jan Green");
		Account account2 = new Account("John Blue");

		// display initial value of tpname for each Account
		System.out.printf("account1 name is: %s%n", account1.getName());
		System.out.printf("account2 name is: %s%n", account2.getName());
	}
}
```

```
account1 name is: Jan Green
account2 name is: John Blue
```

### Constructors cannot return values

- Constructors can specify parameters but ont return types

### Default constructor

- If a class does not define constructors, the compiler provides a default constructor with no parameters, and the class's instance variables are initialized to their default values

### There's no default constructor in a class that declares a constructor

- If you declare a constructor for a class, the compiler will not create a default constructor for that class

<center markdown="block">
![class-diagram-account-fig_03-05](/assets/java-programming/images/3-class-diagram-account-fig_03-05.png)

Class diagram for class `Account` of Fig. 3.5
</center>

---

## 3.4 Account Class with a Balance; Floating-Point Numbers

```java
// Fig. 3.8: Account.java
// Account class with a double instance variable balance and a constructor and deposit method that perform validation

public class Account {
	private String name;  // instance varialbe
	private double balance;  // instancee variable

	// Account constructor that receives two parameters
	public Account(String name, double balance) {
		this.name = name;  // assign name to instance variable name

		// validate that the balance is greater than 0.0; if it's not, instance variable balance keeps its default initial value of 0.0
		if (balance > 0.0)  // if the balance is valid
			this.balance = balance;  // assign it to instance variable
	}

	// method that deposits (adds) only a valid amount to the balance
	public void deposit(double depositAmount) {
		if (depositAmount > 0.0)  // if the depositAmount is valid
			balance = balance+depositAmount;  // add it to the balance
	}

	// method returns the account balance
	public double getBalance() {
		return balance;
	}

	// method that sets the name
	public void setName(String name) {
		this.name = name;
	}

	// method that returns the name
	public String getName() {
		return name;
	}
}
```

### 3.4.2 AccountTest Class to Use Class Account

```java
// Fig. 3.9: AccountTest.java
// Inputting and outputting floating-ponit numbers with Account objects

import java.util.Scanner;

public class AccountTest {
	public static void main(String[] args) {
		Account account1 = new Account("Jane Green", 50.00);
		Account account2 = new Account("John Blue", -7.53);

		// display initial balance of each object
		System.out.printf("%s balance: $%.2f%n", account1.getName(), account1.getBalance());
		System.out.printf("%s balance: $%.2f%n%n", account2.getName(), account2.getBalance());

		// create a Scanner to obtain input from the command window
		Scanner input = new Scanner(System.in);

		System.out.print("Enter deposit amount for account1: ");  // prompt
		double depositAmount = input.nextDouble();  // obtain user input
		System.out.printf("%nadding %.2f to account balance%n%n", depositAmount);
		account1.deposit(depositAmount);  // add to account1's balance

		// display balances
		System.out.printf("%s balances: $%.2f%n", account1.getName(), account1.getBalance());
		System.out.printf("%s balances: $%.2f%n%n", account2.getName(), account2.getBalance());

		System.out.print("Enter deposit amount for account2: ");  // prompt
		depositAmount = input.nextDouble();  // obtain user input
		System.out.printf("%nadding %.2f to account balance%n%n", depositAmount);
		account2.deposit(depositAmount);  // add to account2's balance

		// display balances
		System.out.printf("%s balances: $%.2f%n", account1.getName(), account1.getBalance());
		System.out.printf("%s balances: $%.2f%n%n", account2.getName(), account2.getBalance());
	}
}
```

```
Jane Green balance: $50.00
John Blue balance: $0.00

Enter deposit amount for account1: 25.53

adding 25.53 to account balance

Jane Green balances: $75.53
John Blue balances: $0.00

Enter deposit amount for account2: 123.45

adding 123.45 to account balance

Jane Green balances: $75.53
John Blue balances: $123.45
```

##### Floating-point number

- A number with a decimal point

- `float`

	- represents single-precision floating-point numbers

	- up to 7 sinificant digits

- `double`

	- represents double-precision floating-point numbers

	- reauire twice as much memory as `float`

	- provide 15 significant digits - approximately double the precision of `float` variables

- floating-point literals are `double` values

<table>
	<caption>Java primitive types</caption>
	<thead>
		<tr>
			<th>Type</th>
			<th>Size in bits</th>
			<th colspan=2>Values</th>
			<th>Standard</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td><span markdown=1>`boolean`</span></td>
			<td></td>
			<td colspan=2><span markdown=1>`true` or `false`</span></td>
			<td></td>
		</tr>
		<tr>
			<td><span markdown=1>`char`</span></td>
			<td>16</td>
			<td colspan=2>'\u0000' to '\uFFFF' (0 to 65535)</td>
			<td>ISO Unicode character set</td>
		</tr>
		<tr>
			<td><span markdown=1>`byte`</span></td>
			<td>8</td>
			<td colspan=2>-128 to +127 ($-2^7$ to $2^7-1$)</td>
			<td></td>
		</tr>
		<tr>
			<td><span markdown=1>`short`</span></td>
			<td>16</td>
			<td colspan=2>-32,768 to +32,767 ($-2^{15}$ to $2^{15}-1$)</td>
			<td></td>
		</tr>
		<tr>
			<td><span markdown=1>`int`</span></td>
			<td>32</td>
			<td colspan=2>-2,147,283,648 to +2,147,483,647 ($-2^{31}$ to $2^{31}-1$)</td>
			<td></td>
		</tr>
		<tr>
			<td><span markdown=1>`long`</span></td>
			<td>64</td>
			<td colspan=2>-9,223,372,036,854,775,808 to +9,223,372,036,854,775,807 ($-2^{63}$ to $2^{63}-1$)</td>
			<td></td>
		</tr>
		<tr>
			<td rowspan=2><span markdown=1>`float`</span></td>
			<td rowspan=2>32</td>
			<td>Negative range</td>
			<td>-3.4028234663852886E+38 to -1.40129846432481707e-45</td>
			<td rowspan=2>IEEE 754 floating point</td>
		</tr>
		<tr>
			<td>Positive range</td>
			<td>1.40129846432481707e-45 to 3.4028234663852886E+38</td>
		</tr>
		<tr>
			<td rowspan=2><span markdown=1>`double`</span></td>
			<td rowspan=2>64</td>
			<td>Negative range</td>
			<td>-1.7976931348623157E+308 to -4.94065645841246544e-324</td>
			<td rowspan=2>IEEE 754 floating point</td>
		</tr>
		<tr>
			<td>Positive range</td>
			<td>4.94065645841246544e-324 to 1.7976931348623157E+308</td>
		</tr>
	</tbody>
</table>

> Note: A `boolean`'s representation is specific to the Java Virtual Machine on each platform

##### `System.out.printf`

- Format specifier `%.2f`

	- `%f` is used to output values of type `float` or `double`

	- `.2` represents the number of decimal places 2 to output to the right of the decimal point

	- The output values will be rounded

##### `Scanner` method `nextDouble`

- returns a `double value entered by the user

<center markdown="block">
![class-diagram-account-fig_03-08](/assets/java-programming/images/3-class-diagram-account-fig_03-08.png)

Class diagram for class `Account` of Fig. 3.8.
</center>

---

## 3.5 Primitive Types vs. Reference Types

### Primitive types

- `boolean`, `byte`, `char`, `short`, `int`, `long`, `float`, `double`

- A primitive-type variable can store exactly one value of its declared type at a time

- Primitive-type instance variables are initialized by default

	- `boolean`: `false`

	- `byte`, `char`, `short`, `int`, `long`, `float` and `double`: 0

- specifying your own initial value for a primitive-type variable

### Reference types

- All non-primitive types, that is, class types

- Variables of reference types (normally called references) store the locations of objects in the computer's memory

- Objects that are referenced may each contain many instance variables and methods

- Reference-type instance variables are initialized by default to the value `null` - represents a "reference to nothing"

- When using an object of another class, a reference to the object is required to invoke(i.e. call) its methods. Also known as sending messages to an object
