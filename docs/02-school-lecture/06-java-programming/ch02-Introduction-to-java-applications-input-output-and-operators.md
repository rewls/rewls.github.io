---
layout: default
title: Ch2 Introduction to Java Applications - Input/Output and Operators
parent: Java Programming
grand_parent: School Lecture
nav_order: 1
mathjax: true
mermaid: true
permalink: /docs/java/ch2
---

# Ch2 Introduction to Java Applications - Input/Output and Operators
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

- Write simple Java applications

- Use input and output statements

- Learn about Java's primitive types

- Understand basic memory concepts

- Use arithmetic operators

- Learn the precedence of arithmetic operators

- Write decision-making statements

- Use relational and equality operators

## 2.2 Your First Program in Java: Printing a Line of Text

```java
// Fig. 2.1: Welcome1.java
// Text-printing program

public class Welcome1 {
    // main method begins execution of Java application
    public static void main(String[] args) {
        System.out.println("Welcome to Java Programming!");
    }  // end method main
}  // end class Welcome1
```

```
Welcome to Java Programming!
```

### Class declaration

- Every Java program consists of at least one class that you define

### Class names

- By conventions, begin with a capital letter and capitalize the first letter of each word they include

    - ex) `SampleClassName`

- A class name is an identifier

    - consists of letters, digits, underscores(_) and dollar signs($)

    - does not begin with a digit

    - does not contain spaces

- Java is case sensitive

### `main` method

- starting point of every Java application

### Java Keywords

- always spelled with all lowercase letters

- [Java Language Keywords](https://docs.oracle.com/javase/tutorial/java/nutsandbolts/_keywords.html)

### `System.out.println("...");`

- `System.out` object

    - Standard output object

- `System.out.println` method

    - prints a string in the command window

    - positions the output cursor at the beginning of the next line

> Common Programming Error 2.2
>
> A compilations error occurs if a `public` class's file name is not exactly the same name as the class (in terms of both spelling and capitalization) followed by the `java` extension

## 2.3 Modifying your First Java Program

```java
// Fig. 2.3: Welcome2.java
// Printing a line of text with multiple statements

public class Welcome2 {
    // main method begins excution of Java application
    public static void main(String[] args) {
        System.out.print("Welcome to ");
        System.out.println("Java Programming!");
    }  // end method main
}  // end class Welcome2
```

```
Welcome to Java Programming!
```

```java
// Fig. 2.4: Welcome3.java
// Printing multiple lines of text with a single statement

public class Welcome3 {
    // main method begins execution of Java application
    public static void main(String[] args) {
        System.out.println("Welcome\nto\nJava\nProgramming!");
    }  // end method main
}  // end class Welcome3
```

```
Welcome
to
Java
Programming!
```

<table>
    <caption>Some common escape sequences</caption>
    <thead>
        <tr>
            <th>Escape sequence</th>
            <th>Description</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td><span markdown=1>`\n`</span></td>
            <td>Newline. Position the screen cursor at the beginning of the next line</td>
        </tr>
        <tr>
            <td><span markdown=1>`\r`</span></td>
            <td>Carriage return. Position the screen cursor at the beginning of the current line - do not advance to the next line. Any characters output after the carriage return overwrite the characters previously output on that line</td>
        </tr>
        <tr>
            <td><span markdown=1>`\\`</span></td>
            <td>Backslash. Used to print a backslash character</td>
        </tr>
        <tr>
            <td><span markdown=1>`\"`</span></td>
            <td>Double quote. Used to print a double-quote character</td>
        </tr>
    </tbody>
</table>

## 2.4 Displaying text with `printf`

```java
// Fig. 2.6: Welcome4.java
// Displaying muliple lines with method System.out.printf

public class Welcome4 {
    // main method begins execution of Java application
    public static void main(String[] args) {
        System.out.printf("%s%n%s%n", "Welcome to", "Java Programming!");
    }  // end method main
}  // end class Welcome4
```

```
Welcome to
Java Programming!
```

## 2.5 Another Application: Adding Integers

```java
// Fig. 2.7: Addition.java
// Addition program that inputs two numbers then displays their sum

import java.util.Scanner;  // program uses class Scanner

public class Addition {
    // main method begins execution of Java application
    public static void main(String[] args) {
        // create a Scanner to obtain input from the command window
        Scanner input = new Scanner(System.in);

        System.out.print("Enter first integer: ");  // prompt
        int number1 = input.nextInt();  // read first number from user

        System.out.print("Enter second integer: ");  // prompt
        int number2 = input.nextInt();  // read second number from uwer

        int sum = number1+number2;  // add numbers, then store total in sum

        System.out.printf("Sum is %d%n", sum);  // display sum
    }  // end method main
}  // end class Addition
```

```
Enter first integer: 45
Enter second integer: 72
Sum is 117
```

### `import` declaration

- helps the compiler locate a class that is used in this program

### Packages

- named groups of predefined and related classes

> Common Programming Enter 2.5
>
> All `import` declaration must appear before the first class declaration in the file. Placing an `import` declaration inside or after a class declaration is a syntax error.

### `new` keyword

- creates an object

### `Scanner` object

- enables a program to read data comming from the user at the keyboard or a file on disk

- translates these bytes into types that can be used in a program

##### Standard input object, `System.in`

- enables applications to read bytes of information typed by the user

> Good Programming Practice 2.9
>
> By convention, variable-name identifiers use the camel-case naming convention with a lowercase first letter

### `System`

- a class of package `java.lang`

- not imported with an `import` declaration

> Software Engineering Observation 2.1
>
> By default, package `java.lang` is imported in every Java program; thus, classes in `java.lang` are the only ones in the Java API that do not require an `import` declaration

## 2.7 Arithmetic

<table>
    <caption>Arithmetic operators</caption>
    <thead>
        <tr>
            <th>Java operation</th>
            <th>Operator</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>Addition</td>
            <td><span markdown=1>`+`</span></td>
        </tr>
        <tr>
            <td>Subttraction</td>
            <td><span markdown=1>`-`</span></td>
        </tr>
        <tr>
            <td>Multiplication</td>
            <td><span markdown=1>`*`</span></td>
        </tr>
        <tr>
            <td>Division</td>
            <td><span markdown=1>`/`</span></td>
        </tr>
        <tr>
            <td>Rdmainder</td>
            <td><span markdown=1>`%`</span></td>
        </tr>
    </tbody>
</table>

- Integer division yields an integer quotient

- The remainder operator yields the remainder after division

<table>
    <caption>Precedence of arithmetic operators</caption>
    <thead>
        <tr>
            <th>Operator</th>
            <th>Associativity</th>
            <th>Java operation</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td class="bottom-none"><span markdown=1>`*`</span></td>
            <td class="bottom-none">$\rightarrow$</td>
            <td class="bottom-none">Multiplication</td>
        </tr>
        <tr>
            <td class="bottom-none"><span markdown=1>`/`</span></td>
            <td class="bottom-none">$\rightarrow$</td>
            <td class="bottom-none">Division</td>
        </tr>
        <tr>
            <td><span markdown=1>`%`</span></td>
            <td>$\rightarrow$</td>
            <td>Rdmainder</td>
        </tr>
        <tr>
            <td class="bottom-none"><span markdown="1">`+`</span></td>
            <td class="bottom-none">$\rightarrow$</td>
            <td class="bottom-none">Addition</td>
        </tr>
        <tr>
            <td><span markdown=1>`-`</span></td>
            <td>$\rightarrow$</td>
            <td>Subttraction</td>
        </tr>
        <tr>
            <td><span markdown=1>`=`</span></td>
            <td>$\leftarrow$</td>
            <td>Assignment</td>
        </tr>
    </tbody>
</table>

## 2.8 Decision Making: Equality and Relational Operators

### `if` selection statement

- allows a program to make a decision based on a condition's value

### A condition

- is an expressiont that can be `true` or `false`

- can be formed by equality operators and relational operators

- Equality operators are lower than relational operators in the levels of precedence

<table>
    <caption>Equality and relational operators</caption>
    <thead>
        <tr>
            <th colspan=2>Standard algebraic equality or relational operator</th>
            <th>Java equality or relational operator</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <th rowspan=2>Equality operators</th>
            <td>$=$</td>
            <td><span markdown=1>`==`</span></td>
        </tr>
        <tr>
            <td>$\ne$</td>
            <td><span markdown=1>`!=`</span></td>
        </tr>
        <tr>
            <th rowspan=4>Relational operators</th>
            <td>$>$</td>
            <td><span markdown=1>`>`</span></td>
        </tr>
        <tr>
            <td>$<$</td>
            <td><span markdown=1>`<`</span></td>
        </tr>
        <tr>
            <td>$\ge$</td>
            <td><span markdown=1>`>=`</span></td>
        </tr>
        <tr>
            <td>$\le$</td>
            <td><span markdown=1>`<=`</span></td>
        </tr>
    </tbody>
</table>

```java
// Fig. 2.15: Comparison.java
// Compare integers using if statements, relational operators and equality operators

import java.util.Scanner;  // program uses class Scanner

public class Comparison {
    // main method begins execution of Java application
    public static void main(String[] args) {
        // create Scanner to obtain input from command line
        Scanner input = new Scanner(System.in);

        System.out.print("Enter first integer: ");  // prompt
        int number1 = input.nextInt();  // read first number from user

        System.out.print("Enter second integer: ");  // prompt
        int number2 = input.nextInt();  // read second number from user

        if (number1 == number2)
            System.out.printf("%d == %d%n", number1, number2);
        if (number1 != number2)
            System.out.printf("%d != %d%n", number1, number2);
        if (number1 < number2)
            System.out.printf("%d < %d%n", number1, number2);
        if (number1 > number2)
            System.out.printf("%d > %d%n", number1, number2);
        if (number1 <= number2)
            System.out.printf("%d <= %d%n", number1, number2);
        if (number1 >= number2)
            System.out.printf("%d >= %d%n", number1, number2);
    }  // end method main
}  // end class Comparison
```

```
Enter first integer: 777
Enter second integer: 777
777 == 777
777 <= 777
777 >= 777
```

```
Enter first integer: 1000
Enter second integer: 2000
1000 != 2000
1000 < 2000
1000 <= 2000
```

```
Enter first integer: 2000
Enter second integer: 1000
2000 != 1000
2000 > 1000
2000 >= 1000
```

<table>
	<caption>Precedence and associativity of operators discussed</caption>
	<thead>
		<tr>
			<th>Operators</th>
			<th>Associativity</th>
			<th>Type</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td><span markdown=1>`*` `/` `%`</span></td>
			<td>$\rightarrow$</td>
			<td>multiplicative</td>
		</tr>
		<tr>
			<td><span markdown=1>`+` `-`</span></td>
			<td>$\rightarrow$</td>
			<td>additive</td>
		</tr>
		<tr>
			<td><span markdown=1>`<` `<=` `>` `>=`</span></td>
			<td>$\rightarrow$</td>
			<td>relational</td>
		</tr>
		<tr>
			<td><span markdown=1>`==` `!=`</span></td>
			<td>$\rightarrow$</td>
			<td>equality</td>
		</tr>
		<tr>
			<td><span markdown=1>`=`</span></td>
			<td>$\leftarrow$</td>
			<td>equality</td>
		</tr>
	</tbody>
</table>
