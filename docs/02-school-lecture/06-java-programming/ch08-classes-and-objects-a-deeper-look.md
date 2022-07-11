---
layout: default
title: Ch8 Classes and Objects - A Deeper Look
parent: Java Programming
grand_parent: School Lecture
nav_order: 9
mathjax: true
mermaid: true
permalink: /docs/java/ch8
---

# Ch8 Classes and Objects: A Deeper Look
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

- See additional details of creating class declarations

- Use the `throw` statement to indicate that a problem has occurre

- Use keyword `this` in a constructor to call another constructor in the same class

- Use `static` variables and methods

- Import `static` members of a class

- Use the `enum` type to create sets of constants with unique identifier

- Declare `enum` constants with parameters

- Use `BigDecimal` for precise monetary calculations

---

## 8.2 Time Class Case Study

```java
// Fig. 8.1: Time1.java
// Time1 class declaration maintains the time in 24-hour format.

public class Time1 {
	// zero by default
    private int hour;  // 0 - 23
    private int minute;  // 0 - 59
    private int second;  // 0 - 59

    // set a new time value using universal time; throw an
    // exception if the hour, minute or second is invalid
    public void setTime(int hour, int minute, int second) {
        // validate hour, minute and second
        if (hour < 0 || hour >= 24 || minute < 0 || minute >= 60 ||
            second < 0 || second >= 60) {
			// a custom error message
            throw new IllegalArgumentException(
                "hour, minute and/or second was out of range");
        }

        this.hour = hour;
        this.minute = minute;
        this.second = second;
    }

    // convert to String in universal-time format (HH:MM:SS)
    public String toUniversalString() {
        return String.format("%02d:%02d:%02d", hour, minute, second);
    }

    // convert to String in standard-time format (H:MM:SS AM or PM)
    public String toString() {
        return String.format("%d:%02d:%02d %s",
            ((hour == 0 || hour == 12) ? 12 : hour % 12),
            minute, second, (hour < 12 ? "AM" : "PM"));
    }
}
```

```java
// Fig. 8.2: Time1Test.java
// Time1 object used in an app.

public class Time1Test {
    public static void main(String[] args) {
        // create and initialize a Time1 object
		// calls default constructor
        Time1 time = new Time1();  // invokes Time1 constructor

        // output string representations of the time
        displayTime("After time object is created", time);
        System.out.println();

        // change time and output updated time
        time.setTime(13, 27, 6);
        displayTime("After calling setTime", time);
        System.out.println();

        // attempt to set time with invalid values
        try {
            time.setTime(99, 99, 99);  // all values out of range
        }
        catch (IllegalArgumentException e) {
            System.out.printf("Exception: %s%n%n", e.getMessage());
        }

        // display time after attempt to set invalid values
        displayTime("After calling setTime with invalid values", time);
    }

    // displays a Time1 object in 24-hour and 12-hour formats
    private static void displayTime(String header, Time1 t) {
        System.out.printf("%s%nUniversal time: %s%nStandard time: %s%n",
            header, t.toUniversalString(), t.toString());
    }
}
```

```
After time object is created
Universal time: 00:00:00
Standard time: 12:00:00 AM

After calling setTime
Universal time: 13:27:06
Standard time: 1:27:06 PM

Exception: hour, minute and/or second was out of range

After calling setTime sith invalid values
Universal time: 13:27:06
Standard time: 1:27:06 PM
```

- `e.getMessage()`: 오류의 원인 출력

---

## 8.3 Controlling Access to Members

### Access modifiers `public` and `private`

- Control access to a class's variables and methods

- Chapter 9 introduces access modifier `protected`

##### `public` methods

- The services the class provides, or the class's `public` interface

##### `private` class members

- Are not accessible outside the class

```java
// Fig. 8.3: MemberAccessTest.java
// Private members of class Time1 are not accessible.

public class MemberAccessTest {
    public static void main(String[] args) {
        Time1 time = new Time1();  // create and initialize Time1 object

        // error: has private access in Time1
        time.hour = 7;
        time.minute = 15;
        time.second = 30;
    }
}
```

```
MemberAccessTest.java:9: error: hour has private access in Time1
                time.hour = 7;
                    ^
MemberAccessTest.java:10: error: minute has private access in Time1
                time.minute = 15;
                    ^
MemberAccessTest.java:11: error: second has private access in Time1
                time.second = 30;
                    ^
3 errors
```

---

## 8.4 Referring to the Current Object's Members with the `this` Reference

- Keyword `this`

    - A reference to object, itself

    - Can be used implicitly and explicitly in a non-static methods

```java
public class TimeTest {
	public static void main(String[] args) {
		Time1 t1 = new Time1();
		Time1 t2 = new Time1();

		t1.setTime(13, 30, 22);
		t2.setTime(22, 59, 10);
	}
}

class Time1 {
	...
	void setTime(int hour, int minute, int second) {
		this.hour = hour;
		...
	}
}
```

<div hidden>
@startuml 8-object-diagram-time
package stack {
	object t2
	object t1
}

package heap {
	map "Time1 object" as o1 {
		hour => 0
		minute => 0
		second => 0
	}
	map "Time1 object" as o2 {
		hour => 0
		minute => 0
		second => 0
	}
}

t1 -d-> o1::hour
t2 -d-> o2::hour
@enduml
</div>

<center markdown="block">
![object-diagram-time](/assets/java-programming/images/8-object-diagram-time.svg)

Object diagram
</center>

- Multiple class declarations in one source file(.java)

    - The compiler places the class files(.class) in the same directory

- A source-code file can contain only one `public` class

- Non-`public` classes can be used only by other classes in the same package

```java
// Fig. 8.4: ThisTest.java
// this used implicitly and explicitly to refer to members of an object.

public class ThisTest {
    public static void main(String[] args) {
        SimpleTime time = new SimpleTime(15, 30, 19);
        System.out.println(time.buildString());
    }
}

// class SimpleTime demonstrates the "this" reference
class SimpleTime {
    private int hour;  // 0-23
    private int minute;  // 0-59
    private int second;  // 0-59

    // if the constructor uses parameter names identical to
    // instance variable names the "this" reference is
    // required to distinguish between the names
    public SimpleTime(int hour, int minute, int second) {
        this.hour = hour;  // set "this" object's hour
        this.minute = minute;  // set "this" object's minute
        this.second = second;  // set "this" object's second
    }

    // use explicit and implicit "this" to call toUniversalString
    public String buildString() {
        return String.format("%24s: %s%n%24s: %s",
            "this.toUniversalString()", this.toUniversalString(),
            "toUniversalString()", toUniversalString());
    }

    // convert to String in universal-time format (HH:MM:SS)
    public String toUniversalString() {
        // "this" is not required here to access instance variables,
        // because method does not have local variables with same
        // names as instance variables
        return String.format("%02d:%02d:%02d",
            this.hour, this.minute, this.second);
    }
}
```

```
this.toUniversalString(): 02d:15:30
     toUniversalString(): 02d:15:30
```

---

## 8.5 `Time` Class Case Study: Overloaded Constructors

- Overloaded constructors with different signatures

### Signatures

- the number of parameters

- the types of the parameters

- the order of the parameter types

### Class Time2 (Fig. 8.5)

- Five overloaded constructors

```java
// Fig. 8.5: Time2.java
// Time2 class declaration with overloaded constructors.

public class Time2 {
    private int hour;  // 0 - 23
    private int minute;  // 0 - 59
    private int second;  // 0 - 59

    // Time2 no-argument constructor:
    // initializes each instance variable to zero
    public Time2() {
        this(0, 0, 0);  // invoke constructor with three arguments
    }

    // Time2 constructor: hour supplied, minute and second defaulted to 0
    public Time2(int hour) {
        this(hour, 0, 0);  // invoke constructor with three arguments
    }

    // Time2 constructor: hour and minute supplied, second defaulted to 0
    public Time2(int hour, int minute) {
        this(hour, minute, 0);  // invoke constructor with three arguments
    }

    // Time2 constructor: hour, minute and second supplied
    public Time2(int hour, int minute, int second) {
        if (hour < 0 || hour >= 24) {
            throw new IllegalArgumentException("hour must be 0-23");
        }

        if (minute < 0 || minute >= 60) {
            throw new IllegalArgumentException("minute must be 0-59");
        }

        if (second < 0 || second >= 60) {
            throw new IllegalArgumentException("second must be 0-59");
        }

        this.hour = hour;
        this.minute = minute;
        this.second = second;
    }

    // Time2 constructor: another Time2 object supplied
    public Time2(Time2 time) {
        // invoke constructor with three arguments
        this(time.hour, time.minute, time.second);
    }

    // Set Methods
    // set a new time value using universal time;
    // validate the data
    public void setTime(int hour, int minute, int second) {
        if (hour < 0 || hour >= 24) {
            throw new IllegalArgumentException("hour must be 0-23");
        }

        if (minute < 0 || minute >= 60) {
            throw new IllegalArgumentException("minute must be 0-59");
        }

        if (second < 0 || second >= 60) {
            throw new IllegalArgumentException("second must be 0-59");
        }

        this.hour = hour;
        this.minute = minute;
        this.second = second;
    }

    // validate and set hour
    public void setHour(int hour) {
        if (hour < 0 || hour >= 24) {
            throw new IllegalArgumentException("hour must be 0-23");
        }

        this.hour = hour;
    }

    // validate and set minute
    public void setMinute(int minute) {
        if (minute < 0 || minute >= 60) {
            throw new IllegalArgumentException("minute must be 0-59");
        }

        this.minute = minute;
    }

    // validate and set second
    public void setSecond(int second) {
        if (second < 0 || second >= 60) {
            throw new IllegalArgumentException("second must be 0-59");
        }

        this.second = second;
    }

    // Get Methods
    // get hour value
    public int getHour() {return hour;}

    // get minute value
    public int getMinute() {return minute;}

    // get second value
    public int getSecond() {return second;}

    // convert to String in universal-time format (HH:MM:SS)
    public String toUniversalString() {
        return String.format(
            "%02d:%02d:%02d", getHour(), getMinute(), getSecond());
    }

    // convert to String in standard-time format (H:MM:SS AM or PM)
    public String toString() {
        return String.format("%d:%02d:%02d %s",
            ((getHour() == 0 || getHour() == 12) ? 12 : getHour() % 12),
            getMinute(), getSecond(), (getHour() < 12 ? "AM" : "PM"));
    }
}
```

### Some case code

```java
// constructor
public Time2() {
    this(0, 0, 0);  // ok
    ...
}
```

```java
// constructor
public Time2() {
    ...
    this(0, 0, 0);  // error
}
```

```java
// method
public void setHour(int h) {
    this(0, 0, 0);  // error
    ...
}
```

```java
// constructor
public Time2(Time2 secondObj) {
    hour = secondObj.hour  // ok
}
```

```java
// method
public void setHour(int hour) {
    Time2 secondObj = new Time2();
    this.hour = secondObj.hour  // ok
}
```

### Class `Time2Test`(Fig. 8.5)

```java
// Fig. 8.6: Time2Test.java
// Overloaded constructors used to initialize Time2 objects.

public class Time2Test {
    public static void main(String[] args) {
        Time2 t1 = new Time2();  // 00:00:00
        Time2 t2 = new Time2(2);  // 02:00:00
        Time2 t3 = new Time2(21, 34);  // 21:34:00
        Time2 t4 = new Time2(12, 25, 42);  // 12:25:42
        Time2 t5 = new Time2(t4);  // 12:25:42

        System.out.println("Constructed with:");
        displayTime("t1: all default arguments", t1);
        displayTime("t2: hour specified; default minute and second", t2);
        displayTime("t3: hour and minute specified; default second", t3);
        displayTime("t4: hour, minute and second specified", t4);
        displayTime("t5: Time2 object t4 specified", t5);

        // attempt to initialize t6 with invalid values
        try {
            Time2 t6 = new Time2(27, 74, 99);  // invalid values
        }
        catch (IllegalArgumentException e) {
            System.out.printf("%nException while initializing t6: %s%n",
                e.getMessage());
        }
    }

    // displays a Time2 object in 24-hour and 12-hour formats
    private static void displayTime(String header, Time2 t) {
        System.out.printf("%s%n   %s%n   %s%n",
            header, t.toUniversalString(), t.toString());
    }
}
```

```
Constructed with:
t1: all default arguments
   00:00:00
   12:00:00 AM
t2: hour specified; default minute and second
   02:00:00
   2:00:00 AM
t3: hour and minute specified; default second
   21:34:00
   9:34:00 PM
t4: hour, minute and second specified
   12:25:42
   12:25:42 PM
t5: Time2 object t4 specified
   12:25:42
   12:25:42 PM
```

### Q. If the no-argument constructor of class `Time2` is not declared, what will happen in line 6?

- Error. constructor가 선언되어 있을 때, 컴파일러는 default constructor를 제공하지 않는다.

### Q. How to access a class's private data in the methods?

- Directly vs. by calling the set and get methods

### Consider changing the representation of the time

- From three `int` values to a single `int` value (representing the total number of seconds that have elapsed since midnight)

    - Only the bodies of the methods that access the private data directly would need to change - in particular, the three-argument constructor, the `setTime` method, the individual set and get methods for the `hour`, `minute` and `second`.

    - There would be no need to modify the bodies of methods `toUniversalString` or `toString` because they do not access the data directly.

    - Designing the class in this manner reduces the likelihood of programming errors when altering the class’s implementation.

### Q. How to write constructors?

- Including a copy of the appropriate statements from the three-argument constructor

    - Makes changing the class’s internal data representation more difficult.

vs.

- Having the `Time2` constructors call the constructor with three arguments

    - Requires any changes to the implementation of the three-argument constructor be made only once

---

## 8.6 Default and No-Argument Constructors

### Default constuctor

- If you do not provide any constuctors in a class's declaration, the compiler creates a default constructor that takes no arguments

- Initializes the instance variables

	- To the initial values specified in their declarations

	- To their default values (zero for primitive numeric types, `false` for boolean values and `null` for references).

- If your class declares constructors, the compiler will not create a default constructor.

	- You must declare a no-argument constructor if default initialization is required.

---

## 8.8 Composition

### Composition (or has-a relationship )

- Having references to objects of other classes as a class’s members

```java
// Fig. 8.7: Date.java
// Date class declaration.

public class Date {
    private int month;  // 1-12
    private int day;  // 1-31 based on month
    private int year;  // any year

    private static final int[] daysPerMonth =
        {0, 31, 28, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31};

    // constructor: confirm proper value for month and day given the year
    public Date(int month, int day, int year) {
        // check if month in range
        if (month <= 0 || month > 12) {
            throw new IllegalArgumentException(
                "month (" + month + ") must be 1-12");
        }

        // check if day in range for month
        if (day <= 0 ||
            (day > daysPerMonth[month] && !(month == 2 && day == 29))) {
            throw new IllegalArgumentException("day (" + day +
                ") out-of-range for the specified month and year");
        }

        // check for leap year if month is 2 and day is 29
        if (month == 2 && day == 29 && !(year % 400 == 0 ||
              (year % 4 == 0 && year % 100 != 0))) {
            throw new IllegalArgumentException("day (" + day +
                ") out-of-range for the specified month and year");
        }

        this.month = month;
        this.day = day;
        this.year = year;

        System.out.printf("Date object constructor for date %s%n", this);
    }

    // return a String of the form month/day/year
    public String toString() {
        return String.format("%d/%d/%d", month, day, year);
    }
}
```

```java
// Fig. 8.8: Employee.java
// Employee class with references to other objects.

public class Employee {
    // composition
    private String firstName;
    private String lastName;
    private Date birthDate;
    private Date hireDate;

    // constructor to initialize name, birth date and hire date
    public Employee(String firstName, String lastName, Date birthDate,
        Date hireDate) {
        this.firstName = firstName;
        this.lastName = lastName;
        this.birthDate = birthDate;
        this.hireDate = hireDate;
    }

    // convert Employee to String format
    public String toString() {
        return String.format("%s, %s  Hired: %s  Birthday: %s",
            lastName, firstName, hireDate, birthDate);
    }
}
```

```java
// Fig. 8.9: EmployeeTest.java
// Composition demonstration.

public class EmployeeTest {
    public static void main(String[] args) {
        Date birth = new Date(7, 24, 1949);
        Date hire = new Date(3, 12, 1988);
        Employee employee = new Employee("Bob", "Blue", birth, hire);

        System.out.println(employee);
    }
}
```

```
Date object constructor for date 7/24/1949
Date object constructor for date 3/12/1988
Blue, Bob  Hired: 3/12/1988  Birthday: 7/24/1949
```

---

## 8.9 `enum` Types

- The basic `enum` type defines a set of constants represented as unique identifiers

- Like classes, all `enum` types are reference types

### Each `enum` declaration's restrictions

1. `enum` constants are implicitly `final`

2. `enum` constants are implicitly `static`

3. Any attempt to create an object of an `enum` type with operator `new` results in a compilation error

### For every `enum`

- The compiler generates the `static` method values

	- That returns an array of the enum’s constants.

### When an `enum` constant is converted to a `String`

- The constant’s identifier is used as the `String` representation.

```java
// Fig. 8.10: Book.java
// Declaring an enum type with a constructor and explicit instance fields
// and accessors for these fields

public enum Book {
    // declare constants of enum type
    JHTP("Java How to Program", "2018"),
    CHTP("C How to Program", "2016"),
    IW3HTP("Internet & World Wide Web How to Program", "2012"),
    CPPHTP("C++ How to Program", "2017"),
    VBHTP("Visual Basic How to Program", "2014"),
    CSHARPHTP("Visual C# How to Program", "2017");

    // instance fields
    private final String title;  // book title
    private final String copyrightYear;  // copyright year

    // enum constructor can be overloaded
    // can't use public
    Book(String title, String copyrightYear) {
        this.title = title;
        this.copyrightYear = copyrightYear;
    }

    // accessor for field title
    public String getTitle() {
        return title;
    }

    // accessor for field copyrightYear
    public String getCopyrightYear() {
        return copyrightYear;
    }
}
```

```java
// Fig. 8.11: EnumTest.java
// Testing enum type Book.
import java.util.EnumSet;

public class EnumTest {
    public static void main(String[] args) {
        System.out.println("All books:");

        // print all books in enum Book
        for (Book book : Book.values()) {
            System.out.printf("%-10s%-45s%s%n", book,
                 book.getTitle(), book.getCopyrightYear());
        }

        System.out.printf("%nDisplay a range of enum constants:%n");

        // print first four books
        for (Book book : EnumSet.range(Book.JHTP, Book.CPPHTP)) {
            System.out.printf("%-10s%-45s%s%n", book,
                 book.getTitle(), book.getCopyrightYear());
        }
    }
}
```

```
All books:
JHTP      Java How to Program                          2018
CHTP      C How to Program                             2016
IW3HTP    Internet & World Wide Web How to Program     2012
CPPHTP    C++ How to Program                           2017
VBHTP     Visual Basic How to Program                  2014
CSHARPHTP Visual C# How to Program                     2017

Display a range of enum constants:
JHTP      Java How to Program                          2018
CHTP      C How to Program                             2016
IW3HTP    Internet & World Wide Web How to Program     2012
CPPHTP    C++ How to Program                           2017
```

### Method of `Enum` class

- `values`: 상수를 저장한 배열을 생성하여 반환

### Method of `EnumSet` class

- `java.util.EnumSet`

- `range(start, end)`: 지정된 범위의 열거형 세트 생성

> Common Programming Error 8.4
>
> In an `enum` declaration, it's a syntax error to declare `enum` constans after the `enum` type's constructors, fields and methods

---

## 8.10 Garbage Collection

- Every object uses system resources, such as memory

- The JVM performs automatic garbage collection to reclaim the memory occupied by objects that are no longer used.

    - Collection typically occurs when the JVM executes its garbage collector, which may not happen for a while, or even at all before a program terminates.

### `static` members of class

- A `static` variable represents classwide information - all objects of the class share the same piece of data.

- `static` class members are available as soon as the class is loaded into memory at execution time.

- The `this` reference cannot be used in a static method.

### Class `Employee` and `EmployeeTest` (Fig. 8.12, 8.13)

- If a `static` variable is not initialized, the compiler assigns it a default value

- `String` objects in Java are immutable

	- They cannot be modified after they are created

	- String-concatenation operations result in a new concatenated `String` object

```java
// Fig. 8.12: Employee.java
// static variable used to maintain a count of the number of
// Employee objects in memory.

public class Employee {
    private static int count = 0;  // number of Employees created
    private String firstName;
    private String lastName;

    // initialize Employee, add 1 to static count and
    // output String indicating that constructor was called
    public Employee(String firstName, String lastName) {
        this.firstName = firstName;
        this.lastName = lastName;

        ++count;  // increment static count of employees
        System.out.printf("Employee constructor: %s %s; count = %d%n",
            firstName, lastName, count);
    }

    // get first name
    public String getFirstName() {
        return firstName;
    }

    // get last name
    public String getLastName() {
        return lastName;
    }

    // static method to get static count value
    public static int getCount() {
        return count;
    }
}
```

```java
// Fig. 8.13: EmployeeTest.java
// static member demonstration.

public class EmployeeTest {
    public static void main(String[] args) {
        // show that count is 0 before creating Employees
        System.out.printf("Employees before instantiation: %d%n",
            Employee.getCount());

        // create two Employees; count should be 2
        Employee e1 = new Employee("Susan", "Baker");
        Employee e2 = new Employee("Bob", "Blue");

        // show that count is 2 after creating two Employees
        System.out.printf("%nEmployees after instantiation:%n");
        System.out.printf("via e1.getCount(): %d%n", e1.getCount());
        System.out.printf("via e2.getCount(): %d%n", e2.getCount());
        System.out.printf("via Employee.getCount(): %d%n",
            Employee.getCount());

        // get names of Employees
        System.out.printf("%nEmployee 1: %s %s%nEmployee 2: %s %s%n",
            e1.getFirstName(), e1.getLastName(),
            e2.getFirstName(), e2.getLastName());
    }
}
```

```
Employees before instantiation: 0
Employee constructor: Susan Baker; count = 1
Employee constructor: Bob Blue; count = 2

Employees after instantiation:
via e1.getCount(): 2
via e2.getCount(): 2
via Employee.getCount(): 2

Employee 1: Susan Baker
Employee 2: Bob Blue
```

---

## 8.12 `static` import

- The following syntax imports a paricular `static` member:

    ```java
	import static packageName.ClassName.staticMemberName;
	```

- The following syntax imports all `static` member of a class:

    ```java
	import static packageName.ClassName.*;
	```

```java
// Fig. 8.14: StaticImportTest.java
// Static import of Math class methods.
import static java.lang.Math.*;

public class StaticImportTest {
    public static void main(String[] args) {
        System.out.printf("sqrt(900.0) = %.1f%n", sqrt(900.0));
        System.out.printf("ceil(-9.8) = %.1f%n", ceil(-9.8));
        System.out.printf("E = %f%n", E);
        System.out.printf("PI = %f%n", PI);
    }
}
```

```
sqrt(900.0) = 30.0
ceil(-9.8) = -9.0
E = 2.718282
PI = 3.141593
```

---

## 8.13 `final` Instance Variables

- Initialization of final instance variables

    ```java
	private final int INCREMENT = 5;  // ok
	```

    or

    ```java
    private final int INCREMENT;
    public Increment(int increment) {  // constructor
        INCREMENT = increment;  // ok
    }
    ```

- Initialization of `static final` variables

    ```java
	private static final int INCREMENT = 3;  // ok
	```

    or

    ```java
    private static final int INCREMENT;
    public Increment(int increment) {  // constructor
        INCREMENT = increment;  // error
    }
    ```

---

## 8.14 Package Access

- A method or variable with no access modifier in a class is considered to have package access

```java
// Fig. 8.15: PackageDataTest.java
// Package-access members of a class are accessible by other classes
// in the same package.

public class PackageDataTest {
    public static void main(String[] args) {
        PackageData packageData = new PackageData();

        // output String representation of packageData
        System.out.printf("After instantiation:%n%s%n", packageData);

        // change package access data in packageData object
        packageData.number = 77;
        packageData.string = "Goodbye";

        // output String representation of packageData
        System.out.printf("%nAfter changing values:%n%s%n", packageData);
    }
}

// class with package access instance variables
class PackageData {
    int number = 0;  // package-access instance variable
    String string = "Hello";  // package-access instance variable

    // return PackageData object String representation
    public String toString() {
        return String.format("number: %d; string: %s", number, string);
    }
}
```

```
After instantiation:
number: 0; string: Hello

After changing values:
number: 77; string: Goodbye
```

---

## 8.15 Using `BigDecimal` for Precise Monetary Calculations

- Monetary calculations using values of type `double`

    - Some `double` values are represented approximately

- Any application that requires precise floating-poinrt calculations should instead use class `BigDecimal` (from package `java.math`)

```java
// Fig. 8.16: Interest.java
// Compound-interest calculations with BigDecimal.
import java.math.BigDecimal;
import java.text.NumberFormat;

public class Interest {
    public static void main(String args[]) {
        // initial principal amount before interest
        BigDecimal principal = BigDecimal.valueOf(1000.0);
        BigDecimal rate = BigDecimal.valueOf(0.05);  // interest rate

        // display headers
        System.out.printf("%s%20s%n", "Year", "Amount on deposit");

        // calculate amount on deposit for each of ten years
        for (int year = 1; year <= 10; year++) {
            // calculate new amount for specified year
            BigDecimal amount =
                principal.multiply(rate.add(BigDecimal.ONE).pow(year));

            // display the year and the amount
            System.out.printf("%4d%20s%n", year,
                NumberFormat.getCurrencyInstance().format(amount));
        }
    }
}
```

```
Year   Amount on deposit
   1           $1,050.00
   2           $1,102.50
   3           $1,157.62
   4           $1,215.51
   5           $1,276.28
   6           $1,340.10
   7           $1,407.10
   8           $1,477.46
   9           $1,551.33
  10           $1,628.89
```

### Some members of class `BigDecimal`

- `BigDecimal.valueOf(1000.0)`

	- `valueOf`

- `principal.multiply(rate.add(BigDecimal.ONE.pow(year))`

	- `multiply`

	- `add`

	- `ONE`

	- `pow`

### `NumberFormat`

- `getCurrencyInstance`: 현재 지역의 화폐 양식을 나타내는 `NumberFormat` 객체 반환
