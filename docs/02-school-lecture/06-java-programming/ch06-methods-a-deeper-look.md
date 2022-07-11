---
layout: default
title: Ch6 Methods - A Deeper Look
parent: Java Programming
grand_parent: School Lecture
nav_order: 6
mathjax: true
mermaid: true
permalink: /docs/java/ch6
---

# Ch6 Methods - A Deeper Look
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

- How `static` methods and fields are associated with classes rather than objects

- How the method-call/return mechanism is supported by the method-call stack

- About argument promotion and casting

- How packages group related classes

- How to use secure random-number generation to implement game-playing applications

- How the visibility of declarations is limited to specific regions of programs

- What method overloading is and how to create overloaded methods

---

## 6.3 `static` Methods, `static` Fields and Class `Math`

### `static` method (class method)

- Applies to the class in which it's declared as a whole

- Performs a task that does not depend on any object

- Declaring a method as static

    ```java
    public static void methodName(parameters) { }
    ```

- Calling a static method

    ```java
    ClassName.methodName(arguments)
    ```

### `Math` Class Methods

- Class `Math` provides a collection of `static` methods to perform common mathematical calculations

##### `Math` Class `static` Constants `PI` and `E`

- Declared with the modifiers `public`, `final` and `static`

    ```java
    Math.PI  // 3.141592...
    Math.E  // 2.7182818...
    ```

<table>
    <caption>Math class methods</caption>
    <thead>
        <tr>
            <th>Method</th>
            <th>Description</th>
            <th>Example</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td><span markdown=1>`abs(x)`</span></td>
            <td><span markdown=1>absolute value of `x`</span></td>
            <td><span markdown=1>`abs(-23.7)` is 23.7</span></td>
        </tr>
        <tr>
            <td><span markdown=1>`ceil(x)`</span></td>
            <td><span markdown=1>rounds `x` to the smallest integer not less than `x`</span></td>
            <td><span markdown=1>`ceil(-9.2)` is -9.0</span></td>
        </tr>
        <tr>
            <td><span markdown=1>`cos(x)`</span></td>
            <td><span markdown=1>trigonometric cosine of `x` (`x` in radians)</span></td>
            <td><span markdown=1>`cos(0.0)` is 1.0</span></td>
        </tr>
        <tr>
            <td><span markdown=1>`exp(x)`</span></td>
            <td><span markdown=1>exponential method $e^x$</span></td>
            <td><span markdown=1>`exp(1.0)` is 2.71828</span></td>
        </tr>
        <tr>
            <td><span markdown=1>`floor(x)`</span></td>
            <td><span markdown=1>rounds `x` to the largest integer not greater than `x`</span></td>
            <td><span markdown=1>`floor(-9.8)` is -10.0</span></td>
        </tr>
        <tr>
            <td><span markdown=1>`log(x)`</span></td>
            <td><span markdown=1>natural logarithm of `x`(base $e$)</span></td>
            <td><span markdown=1>`log(Math.E)` is 1.0</span></td>
        </tr>
        <tr>
            <td><span markdown=1>`max(x, y)`</span></td>
            <td><span markdown=1>larger value of `x` and `y`</span></td>
            <td><span markdown=1>`max(2.3, 12.7)` is 12.7</span></td>
        </tr>
        <tr>
            <td><span markdown=1>`min(x, y)`</span></td>
            <td><span markdown=1>smaller value of `x` and `y`</span></td>
            <td><span markdown=1>`min(2.3, 12.7)` is 2.3</span></td>
        </tr>
        <tr>
            <td><span markdown=1>`pow(x, y)`</span></td>
            <td><span markdown=1>`x` raised to the power `y` (i.e. $x^y$)</span></td>
            <td><span markdown=1>`pow(2.0, 7.0)` is 128.0</span></td>
        </tr>
        <tr>
            <td><span markdown=1>`sin(x)`</span></td>
            <td><span markdown=1>trigonometric sine of `x` (`x` in radians)</span></td>
            <td><span markdown=1>`sin(0.0)` is 0.0</span></td>
        </tr>
        <tr>
            <td><span markdown=1>`sqrt(x)`</span></td>
            <td><span markdown=1>square root of `x`</span></td>
            <td><span markdown=1>`sqrt(900.0)` is 30.0</span></td>
        </tr>
        <tr>
            <td><span markdown=1>`tan(x)`</span></td>
            <td><span markdown=1>trigonometric tangent of `x` (`x` in radians)</span></td>
            <td><span markdown=1>`tan(0.0)` is 0.0</span></td>
        </tr>
    </tbody>
</table>

> Software Engineering Observation 6.4
>
> Class `Math` is part of the `java.lang` package, which is implicitl imported by the compiler

### Fields of a class

- `static` variables + instance variables

##### Static variables (class variables)

- All objects of a class containing `static` fields share on copy of those fields

##### Instance variables

- Each object(instance) of the class has a separate instance of the variable in memory

### Why is method `main` declared `static`?

- The JVM attempts to invoke the `main` method of the class you specify - at this point no objects of the class have been created

- Declaring `main` as `static` allows the JVM to invoke `main` without creating an instance of the class.

---

## 6.4 Declaring Methods with Multiple Parameters

```java
// Fig 6.3: MaximumFinder.java
// Programmer-declared method maximum with three double parameters

import java.util.Scanner;

public class MaximumFinder {
    public static void main(String[] args) {
        // create Scanner for input from command window
        Scanner input = new Scanner(System.in);

        // prompt for input three floating-point values
        System.out.print("Enter three floating-point values separated by spaces: ");
        double number1 = input.nextDouble();  // read first double
        double number2 = input.nextDouble();  // read second double
        double number3 = input.nextDouble();  // read third double

        // determine the maximum value
        double result = maximum(number1, number2, number3);

        // display maximum value
        System.out.println("Maximum is: " + result);
        // String concatenation
    }

    // returns the maximum of its three double parameters
    public static double maximum(double x, double y, double z) {
        double maximumValue = x;  // assume x is the largest to start

        // determine whether y is greater than maximumValue
        if (y > maximumValue)
            maximumValue = y;

        // determine whether z is greater than maximumValue
        if (z > maximumValue)
            maximumValue = z;

        return maximumValue;
        // return Math.max(x, Math.max(y, z));
    }
}
```

```
Enter three floating-point values separated by spaces: 9.35 2.74 5.1
Maximum is: 9.35
```

> Software Engineering Observation 6.5
>
> Method can return at most one value, but the returned value could be a reference to an object that contains many values in its instance variables

> Software Engineering Observation 6.6
>
> Variables should be declared as fields only if they're required for use in more than one method of the class or if the program should save their values between calls to the class's methods

### Assembling `String`s with `String` Concatenation

##### `String` concatenation

- Operator `+` or `+=`

- `String` object + `String` object $\rightarrow$ a new `String` object

##### Concatenation with non-`String`

- Every primitive value and object has a `String` representation

- `String` object + primitive value $\rightarrow$ `String` object + `String` object

- `String` object + `boolean` $\rightarrow$ `String` object + "true/false"

- `String` object + object $\rightarrow$ `String` object + `String` object

- All objects have a `toString` method that returns a `String` representation of the object

---

## 6.5 Notes on Declaring and Using Methods

### Three ways to call a method

```java
public class MaximumFinder {
    public void determinMaximum() {
        ...
        double result = maximum(num1, num2, num3);  // (1)
    }

    public void maximum(double x, double y, double z) {
        ...
    }

    public static void stateFunction() {
        ...
    }
}

public class MaximumFinderTest {
    public static void main(String[] args) {
        MaximumFinder maximumFinder = new MaximumFinder();
        maximumFinder.determinMaximum();  // (2)
        MaximumFinder.staticFunction();  // (3)
    }
}
```

### A non-`static` method (instance method)

- Can call **any** method of the same class directly

- Can manipulate **any** of the class's fields directly

### A `static` method

- Can call **only** other `static` methods of the same class directly

- Can manipulate **only** `static` fields in he same class directly

- Must use a reference to an object of the class to access the class's non-`static` members

```java
public class MaximumFinder {
    int nonStaticNum = 0;
    static int staticNum = 0;

    public void nonStaticMethod1() {
        ;
    }

    public void nonStaticMethod2() {
        nonStaticMethod1();
        nonStaticNum = 1;

        staticMethod1();
        staticNum = 1;
    }

    public static void staticMethod1() {
        ;
    }

    public static void staticMethod2() {
        // accessing static members directly
        staticMethod1();
        staticNum = 1;

        // accessing non-static members
        // by using a reference to the class's object
        MaximumFinder mf = new MaximumFinder();
        mf.nonStaticMethod1();

        // accessing non-static members directly
        // causes error
        nonStaticMethod1();
        nonStaticNum = 1;
    }
}
```

### Three ways to return control to the statement that calls a method:

- When the program flow reaches the method-ending right brace

- `return;`

- `return expression;`

---

## 6.6 Method-Call Stack and Activation Records

### Program-excution stack (or method-call stack)

- a series of method calls

    - `main()` $\rightarrow$ `mA()` $\rightarrow$ `mB()`

- Each activation record (or stack frame) includes

    - return address of the calling method

    - local variables

---

## 6.7 Argument Promotion and Casting

### **Promotion**

- conversions without losing data between primitive types

    - `3+4.0  // 3->3.0`

    - `Math.sqrt(4)  // 4->4.0` **argument promotion**

- Each value is promoted to the highest type in the expression

- The expression uses a temporary copy of each value

    - The types of the original values remain unchanged

<table>
    <caption>Promotions allowed for primitive types</caption>
    <thead>
        <tr>
            <th>Type</th>
            <th>Valid promotions</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td><span markdown=1>`double`</span></td>
            <td><span markdown=1>None</span></td>
        </tr>
        <tr>
            <td><span markdown=1>`float`</span></td>
            <td><span markdown=1>`double`</span></td>
        </tr>
        <tr>
            <td><span markdown=1>`long`</span></td>
            <td><span markdown=1>`float, double`</span></td>
        </tr>
        <tr>
            <td><span markdown=1>`int`</span></td>
            <td><span markdown=1>`long`, `float`, `double`</span></td>
        </tr>
        <tr>
            <td><span markdown=1>`char`</span></td>
            <td><span markdown=1>`int`, `long`, `float`, `doubled</span></td>
        </tr>
        <tr>
            <td><span markdown=1>`short`</span></td>
            <td><span markdown=1>`int`, `long`, `float`, `double` (but not `char</span></td>
        </tr>
        <tr>
            <td><span markdown=1>`byte`</span></td>
            <td><span markdown=1>`short`, `int`, `long`, `float` or `double` (but not `char`)</span></td>
        </tr>
        <tr>
            <td><span markdown=1>`boolean`</span></td>
            <td><span markdown=1>None (`boolean` values are not considered to be numbers in Java)</span></td>
        </tr>
    </tbody>
</table>

### **Casting**

- In cases where information may be lost due to conversion

    - use a cast operator to explicitly force the conversion to occur - otherwise a comiplation error occurs

    - ex1) passing `double` argument for `int` parameter

        ```java
        square((int)doubleValue)  // explicit type casting
        ```

    - ex2)

        ```java
        int number1 = input.nextDouble();  // error
        ```

        ```java
        int number1 = (int)input.nextDouble();  // ok
        ```

---

## 6.9 Secure Random-Number Generation

### Random Number Generation

<table>
    <thead>
        <tr>
            <th><span markdown=1>1. class `Random`</span></th>
            <th><span markdown=1>2. class `SecureRandom`</span></th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td><span markdown=1>`java.util`</span></td>
            <td><span markdown=1>`java.secure`</span></td>
        </tr>
        <tr>
            <td>Deterministic random numbers</td>
            <td>Nondeterministic random numbers</td>
        </tr>
        <tr>
            <td>could be predicted by malicious programmers</td>
            <td>cannot be predicted</td>
        </tr>
        <tr>
            <td colspan=2><span markdown=1>produce random `boolean`, `byte`, `float`, `double`, `int`, `long`, Gaussian values</span></td>
        </tr>
    </tbody>
</table>

3\. `static` method `random` of class `Math`

- can produce only `double` values in the range $0.0 \le x < 1.0$

##### Creating of a new random number generator object

- `SecureRandom randomNumbers = new SecureRandom();`

##### Generating of random `int` value

- `int randomValue = randomNumbers.nextInt();`

- `int randomValue = randomNumbers.nextInt(2);  // the range 0 to 1`

### Rolling a Six-Sided Die

- `int face = 1 + randomNumbers.nextInt(6);

##### scaling factor

- represents the number of unique values that `nextInt` should produce(0-5)

##### shifting value

- specifies the first value in the desired range of random integers

- Shifting value 1 shifts (0-5) to (1-6)

```java
// Fig. 6.6: RandomIntegers.java
// Shifted and scaled random integers

import java.security.SecureRandom;  // program uses class SecureRandom

public class RandomIntegers {
    public static void main(String[] args) {
        // randomNumbers object will produce secure random numbers
        SecureRandom randomNumbers = new SecureRandom();

        // loop 20 times
        for (int counter =1; counter <= 20; counter++) {
            // pick random integer from 1 to 6
            int face = 1 + randomNumbers.nextInt(6);

            System.out.printf("%d  ", face);  // display generated value

            // if counter is divisible by 5, start a new line of output
            if (counter % 5 == 0)
                System.out.println();
        }
    }
}
```

```
3  5  1  5  6
5  3  5  3  6
2  5  6  5  5
1  3  3  5  6
```

```
1  4  4  6  2
5  3  3  5  1
1  6  5  4  4
5  1  4  5  3
```

- Different sequence of random values

```java
// Fig. 6.7: RollDie.java
// Roll a six-sided die 60,000,000 times

import java.security.SecureRandom;

public class RollDie {
    public static void main(String[] args) {
        // randomNumbers object will produce secure random numbers
        SecureRandom randomNumbers = new SecureRandom();

        int frequency1 = 0;  // count of 1s rolled
        int frequency2 = 0;  // count of 2s rolled
        int frequency3 = 0;  // count of 3s rolled
        int frequency4 = 0;  // count of 4s rolled
        int frequency5 = 0;  // count of 5s rolled
        int frequency6 = 0;  // count of 6s rolled

        // tally counts for 60,000,000 rolls of a die
        for (int roll = 1; roll <= 60000000; roll++) {
            int face = 1 + randomNumbers.nextInt(6);  // number from 1 to 6
            // use face value 1-6 to determine which counter to increment
            switch (face) {
                case 1:
                    ++frequency1;  // increment the 1s counter
                    break;
                case 2:
                    ++frequency2;  // increment the 2s counter
                    break;
                case 3:
                    ++frequency3;  // increment the 3s counter
                    break;
                case 4:
                    ++frequency4;  // increment the 4s counter
                    break;
                case 5:
                    ++frequency5;  // increment the 5s counter
                    break;
                case 6:
                    ++frequency6;  // increment the 6s counter
            }
        }

        System.out.println("Face\tFrequency");  // output headers
        System.out.printf("1\t%d%n2\t%d%n3\t%d%n4\t%d%n5\t%d%n6\t%d%n",
            frequency1, frequency2, frequency3, frequency4, frequency5, frequency6);
    }
}
```

```
Face    Frequency
1       10000549
2       10005015
3       9997940
4       10000631
5       10000617
6       9995248
```

### Generalized Scaling and Shifting of Random Numbers

`int number = shiftingValue + randomNumbers.nextInt(scalingFactor);`

`int number = shiftingValue + differenceBetweenValues * randomNumbers.nextInt(scalingFactor);`

- `shiftingValue` specifies the first number in the desired range of values

- `differenceBetweenValues` represents the constant difference between consectutive number in the sequence

- `scalingFactor` specifies how many numbers are in the range

---

## 6.10 A Game of Chance; Introducing `enum` Types

### Basic rules for the dice game Craps

- You roll two dice. Each die has six faces, which contain one, two, three, four, five and six spots, respectively. After the dice have come to rest, the sum of the spots on the two upward faces is calculated

    - If the sum is 7 or 11 on the first throw, you win

    - If the sum is 2, 3 or 12 on the first throw (called "craps"), you lose (i.e. the "house" wins)

    - If the sum is 4, 5, 6, 8, 9 or 10 on the first throw, that sum becaomes your "point"

    - To win, you must continux rolling the dice until you "make your point" (i.e. roll that same point value

    - You lose by rolling a 7 befor making your point

```java
// Fig. 6.8: Craps.java
// Craps class simulates the dice game craps

public class Craps {
    // create secure random number generator for use in method rollDice
    private static final SecureRandom randomNumbers = new SecureRandom();

    // enum type with constants that represent the game status
    private enum Status {CONTINUE, WON, LOST};  // enumeration constants

    // constants that represent common rolls of the dice
    private status final int SNAKE_EYES = 2;
    private status final int TREY = 3;
    private status final int SEVEN = 7;
    private status final int YO_LEVEN = 11;
    private status final int BOX_CARS = 12;

    public static void main(tring[] args) {
        // Q1
        int myPoint = 0;  // point if no win or loss on first roll
		// Q2
        Status gameStatus;  // can contain CONTINUE, WON or LOST

        int sumOfDice = rollDice();  // first roll of the dice

        // determine game status and point based on first roll
        switch (sumOfDice) {  // int
			// Q3
            case SEVEN:  // int constant. win with 7 on first roll
            case YO_LEVEN:  // win with 11 on first roll
                gameStatus = Status.WON;
                break;
            case SNAKE_EYES:  // lose with 2 on first roll
            case TREY:  // lose with 3 on first roll
            case BOX_CARS:  // lose with 12 on first roll
                gameStatus = Status.LOST;
                break;
            default:  // did not win or lose, so remember point
                gameStatus = Status.CONTINUE;  // game is not over
                myPoint = sumOfDice;  // remember the point
                System.over.printf("Point is %d%n", myPoint);
                break;
        }

        // while game is not complete
        while (gameStatus == Status.CONTINUE) {  // not WON or LOST
            sumOfDice = rollDice();  // roll dice again

            // determine game statuc
            if (sumOfDice == myPoint)  // win by making point
                gameStatus = Status.WON;
            else
                if (sumOfDice == SEVEN)  // lose by rolling 7 before point
                    gameStatus = Status.LOST;
        }

        // display won or lose message
        if (gameStatus == Status.WON)
            System.out.println("Player wins");
        else
            System.out.println("Player loses");
    }

    // roll dice, calculate sum and display results
    public static int rollDice() {
        // pick random die values
        int die1 = 1 + randomNumbers.nextInt(6);  // first die roll
        int die2 = 1 + randomNumbers.nextInt(6);  // second die roll

        int sum = die1 + die2;  // sum of die values

        // display results of this roll
        System.out.printf("Player rolled %d + %d = %d%n", die1, die2, sum);

        return sum;
    }
}
```

```
Player rolled 4 + 6 = 10
Point is 10
Player rolled 5 + 6 = 11
Player rolled 5 + 6 = 11
Player rolled 4 + 6 = 10
Player wins
```

```
Player rolled 1 + 6 = 7
Player wins
```

### Q1. If `myPoint` is not initialized?

- A1) If you do not initialize `myPoint`, the compiler issues an error, because `myPoint` is not assiged a value in every case of of the `switch` statement, and thus the program could try to use `myPoint` beore it is assigned a value

### Q2. Why is it OK that `gameStatus` is not initialized?

- A2) `gameStatus` is assigned a value in every case of the `switch` statement. Thus, it's guaranteed to be initialized before it's used and does not need to be initialized

### `enum` type `Status`

`private enum Status {CONTINUE, WON, LOST};`

- A special kind of class with the keyword `enum` and a type name

- Variables of an `enum` type can be assigned only the constants declared in the enumeration

	- `Status gameStatus = Status.WON;`

### Q3. Why should not `SEVEN` be `enum` constant

- A3) Java does not allow an `int` to be compared to an enumeration constant

```java
public class Craps {
    private enum Status {CONTINUE, WON, LOST};
    private enum Numbers {ZERO, ONE, TWO};

    public void play() {
        // syntax errors
        int intNum1 = Status.CONTINUE;
        int intNum2 = (int)Status.CONTINUE;
        Status enmNum1 = 1;
        Status enmNum2 = (Status)1;

        // correct statement
        Nubers enumNum a = Numbers.ZERO;
        switch (enumNum) {
            case ZERO:
                break;
            case ONE:
                break;
            case TWO:
                break;

        }

        // correct statement
        final int intConsNume = 0;
        int intNum3 = 0;
        switch (intNum3) {
            case intConsNum:
                break;
        }

        // syntax error
        int intConsNum4 = 0;
        switch (intNum4); {
            case ZERO:
                break;
        }
    }
}
```

## 6.11 Scope of Declarations

- The scope of a declaration is the portion of the program that can refer to the declared entity by its name

### Basic scope rules

- The scope of a parameter declaration is the body of the method in which the declaration appears

- The scope of a local-variable declaration is from the point at which the declaration appears to the end of that block

- The scope of a local-variable declaration in the initialization section of a `for` statement's header is the body of the `for` statement and the other expressions in the header;

- <b><i>A method or field's scope</i></b> is the entire body of the class

- Any block may contain variable declaration

- If a local variable or parameter in a method has the same name as a field of the class, the field is "hidden" until the block terminates execution - this is called shadowing

```java
// Fig. 6.9: Scope.java
// Scope class demonstrates field and local-variable scopes

public class Scope {
    // field that is accessibe to all methods of this class
    private static int x = 1;

    // method main creates and initializes local variable x and calls methods useLocalVarTable and useField
    public static void main(String[] args) {
        int x = 5;  // method's local variables x shadows field x

        System.out.printf("local x in main is %d%n", x);

        useLocalVariable();  // useLocalVariable has local x
        useField();  // useField uses class Scope's field x
        useLocalVariable();  // useLocalVariable reintializes local x
        useField();  // clas Scope's field x retains its value

        System.out.printf("%nlocal x in the %d%n", x);
    }

    // craete and initializes local varialbe x during each call
    public static void useLocalVariable() {
        int x = 25;  // initialized each time useLocalVariable is called

        System.out.printf("%nlocal x on entering method useLocalVariable is %d%n", x);
        ++x;  // modifiers this method's local variable x
        System.out.printf("local x before exiting method useLocalVariable is %d%n", x);
    }

    // modify class Scope's field x during each call
    public static void useField() {
        System.out.printf("%nfield x on entering method useField is %d%n", x);
        x *= 10;  // modifiers class Scop's field x
        System.out.printf("field x befor exiting method useField is %d%n", x);
    }
}
```

```
local x in main is 5

local x on entering method useLocalVariable is 25
local x before exiting method useLocalVariable is 26

field x on entering method useField is 1
field x befor exiting method useField is 10

local x on entering method useLocalVariable is 25
local x before exiting method useLocalVariable is 26

field x on entering method useField is 10
field x befor exiting method useField is 100

local x in the 5
```

---

## 6.12 Method Overloading

### <b><i>Method overloading</i></b>

- Methods of the same name declared in the same class

- Must have different sets of parameters

- The compiler distinguishes overloaded methods by their signatures

##### Signatures

- the method's names

- the number, types and order of their parameters

> NOTE
>
> Method calls cannot be distinguished by return type

### Usage

- Used to create several methods with the same name

- That perform the same or similar tasks

- But on different types or different number of arguments

```java
// Fig. 6.10: MethodOverload.java
// Overloaded method declarations

public class MethodOverload {
    // test overloaded square method
    public static void main(String[] args) {
        System.out.printf("Square of integer 7 is %d%n", square(7));
        System.out.printf("Square of double 7.5 is %f%n", square(7.5));
    }

    // square method with int argument
    public static int square(int intValue) {
        System.out.printf("%nCalled square with int argument: %d%n", intValue);
        return intValue * intValue;
    }

    // square method with double argument
    public static double square(double doubleValue) {
        System.out.printf("%nCalled square with double argument: %f%n", doubleValue);
        return doubleValue * doubleValue;
    }
}
```

```
Called square with int argument: 7
Square of integer 7 is 49

Called square with double argument: 7.500000
Square of double 7.5 is 56.250000
```
