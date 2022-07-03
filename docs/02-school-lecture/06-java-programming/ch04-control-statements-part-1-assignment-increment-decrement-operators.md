---
layout: default
title: Ch4 Control Statements - Part 1; Assignment, ++ and -- operators
parent: Java Programming
grand_parent: School Lecture
nav_order: 5
mathjax: true
mermaid: true
permalink: /docs/java/ch4
---

# Ch4 Control Statements - Part 1; Assignment, ++ and -- operators
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

- Learn basic problem-solvin techniques

- Develop algorithms through the process of top-down, stepwise refinement

- Use the `if` and `if ... else` selection statements to choose between alternative actions

- Use the `while` iteration statement to execute statements ni a program repeatedly

- Use counter-controlled iteration and sentinel-controlled iteration

- Learn about the portability of primitive data types

## 4.4 Control Structures

### Bohm and Jacopini

- All programs can be written in terms of only three control structures without any `goto` statements

    - sequence structure

    - selection structure

    - repeatition structure

### Implementations of three control structures in Java

##### three control statements

- sequence statement

- selection statement (3 types: `if`, `if else`, `switch`)

- repeatition statement (3 types: `for`, `while`, `do while`)

## 4.7 `Student` Class: Nested `if ... else` Statements

```java
// Fig. 4.4: Student.java
// Student class that stores a student name and average

public class Student {
    private String name;
    private double average;

    // constructor initializes instance variables
    public Student(String name, double average) {
        this.name = name;

        // validate that average is > 0.0 and <= 100.0; otherwise, keep instance variable average's default value (0.0)
        if (average > 0.0)
            if (average <= 100.0)
                this.average = average;  // assign to instance variable
    }

    // sets the Student's name
    public void setName(String name) {
        this.name = name;
    }

    //retrieves the Student's name
    public String getName() {
        return name;
    }

    // sets the Student's average
    public void setAverage(double average) {
        // validate that average is > 0.0 and <= 100.0; otherwise, kepp instance variable average's current value
        if (average > 0.0)
            if (average <= 100.0)
                this.average = average;  // assign to instance variable
    }

    // retrieves the Student's average
    public double getAverage() {
        return average;
    }

    // determines and returns the Student's letter grade
    public String getLetterGrade() {
        String letterGrade = "";  // initialized to emty String

        if (average >= 90.0)
            letterGrade = "A";
        else if (average >= 80.0)
            letterGrade = "B";
        else if (average >= 70.0)
            letterGrade = "C";
        else if (average >= 60.0)
            letterGrade = "D";
        else if (average >= 60.0)
            letterGrade = "D";
        else
            letterGrade = "f";

        return letterGrade;
    }
}
```

```java
// Fig. 4.5: StudentTest.java
// Create and test StudentTest objects

public class StudentTest {
    public static void main(String[] args) {
        Student account1 = new Student("Jane Green", 93.5);
        Student account2 = new Student("John Blue", 72.75);

        System.out.printf("%s's letter grade is: %s%n", account1.getName(), account1.getLetterGrade());
        System.out.printf("%s's letter grade is: %s%n", account2.getName(), account2.getLetterGrade());
    }
}
```

```
Jane Green's letter grade is: A
John Blue's letter grade is: C
```

## 4.9 Formulating Algorithms: Counter-Controlled Iteration

### Counter-controlled repetition

##### counter (or control variable)

- controls the number of times a set of statements will execute

### Problem statement

- A class of ten students took a quiz. The grades(integers in the range0 to 100) for this quiz are available to you. Determine the classaverage on the quiz

```java
// Fig. 4.8: ClassAverage.java
// Solving the class-average problem using counter-controlled iteration

import java.util.Scanner;  // program uses class Scanner

public class ClassAverage {
    public static void main(String[] args) {
        // create Scanner to obtain input from command window
        Scanner input = new Scanner(System.in);

        // initialization phase
        int total = 0;  // initialize sum of grades entered by the use
        int gradeCounter = 1;  // initialize # of grade to be entered next

        // processing phase uses counter-controlled iteration
        while (gradeCounter <= 10) {  // loop 10 times
            System.out.print("Enter grade: ");  // prompt
            int grade = input.nextInt();  // input next grade
            total = total+grade;  // add grade to total
            gradeCounter = gradeCounter+1;  // increment counter by 1
        }

        // termination phase
        int average = total/10;  // integer division yields integer result

        // display total and average of grades
        System.out.printf("%nTotal of all 10 grades is %d%n", total);
        System.out.printf("Class average is %d%n", average);
    }
}
```

```
Enter grade: 67
Enter grade: 78
Enter grade: 89
Enter grade: 67
Enter grade: 87
Enter grade: 98
Enter grade: 93
Enter grade: 85
Enter grade: 82
Enter grade: 100

Total of all 10 grades is 846
Class average is 84
```

## 4.10 Formulating Algorithms: Sentinel-Controlled Iteration

### Sentinel-controlled repetition

##### indefinite repetition

- the number of repetitions is not known befor the loop begins executing

##### sentinel value

- a special value to indicate end of data entry

- must be chosen that cannot be confused with an acceptable input value

### Problem statement

- Develop a class-averaging program that processes grades for an arbitrary number of students each time it is run

> Error-Prevention Tip 4.4
>
> When performing divisionor remainder calculations in which the right operand could be zero, test for this and handle it (e.g. display an error message) rather than allowing the error to occur

```java
// Fig. 4.10: ClassAverage.java
// Solving the class-average processes using sentinel-controlled iteration.

import java.util.Scanner;  // program uses class Scanner

public class ClassAverage {
    public static void main(String[] args) {
        // cerate Scanner to obtain input from command window
        Scanner input = new Scanner(System.in);

        // initialization phase
        int total = 0;
        int gradeCounter = 0; // initialize # of grades entered so far

        // processing phase
        // prompt for input and read grade from user
        System.out.print("Enter grade or -1 to quit: ");
        int grade = input.nextInt();
        // Reads the first value before reaching the while
        // This value determines whether the program's flow of control should enter the body of the while

        // loop until sentinel value read from user
        while (grade != -1) {
            total = total+grade;  // add grade to total
            gradeCounter = gradeCounter+1;

            // prompt for input and read next grade from user
            System.out.print("Enter grade or -1 to quit: ");
            grade = input.nextInt();
        }

        // termination phase
        // if user entered at least one grade...
        if (gradeCounter > 0) {
            // use number with decimal point to calculate average of grades
            double average = (double)total/gradeCounter;

            // display total and average (with two digits of precision)
            System.out.printf("%nTotal of the %d grades entered is %d%n", gradeCounter, total);
            System.out.printf("Class average is %.2f%n", average);
        } else  // no grades were entered, so output appropriate message
            System.out.println("No grades were entered");
    }
}
```

```
Enter grade or -1 to quit: 97
Enter grade or -1 to quit: 88
Enter grade or -1 to quit: 72
Enter grade or -1 to quit: -1

Total of the 3 grades entered is 257
Class average is 85.67
```

### Converting between primitive types

##### explicit conversion (or type cast)

- unary cast operator (double)

    - creates a temporary floating-point copy of its operand

    - The value stored in the operand is unchanged

##### implicit conversion (or promotion)

- `(double)total/gradeCounter`

<center markdown="block">
<div class=mermaid>
graph LR;
    subgraph total;
        int1[int]--type cast-->double1[double];
    end;
    subgraph gradeCounter;
        int2[int]--promotion-->double2[double];
    end;
</div>

Type cast and promotion
</center>

## 4.11 Formulating Algorithms: Nested Control Statements

### Problem statement

- A college offers a course that prepares students for the state licensing exam for real estate brokers. Last year, ten of the students who completed this course took the exam. the college wants to know how well its students did on the exam. You've been asked to write a program to summarize the results. You've been given a list of these 10 students. Next to each name is written a 1 if the student passed the exam or a 2 if the student failed

```java
// Fig. 4.12: Analysis.java
// Analysis of examination results using nested control statements

import java.util.Scanner;  // class uses class Scanner

public class Analysis {
    public static void main(String[] args) {
        // create Scanner to obtain input from commnad window
        Scanner input = new Scanner(System.in);

        // initializing variables in declarations
        int passes = 0;
        int failures = 0;
        int studentCounter = 1;

        // process 10 students usnig counter-controlled loop
        while (studentCounter <= 10) {
            // prompt user for input and obtain value from use
            System.out.print("Enter result (1 = pass, 2 = fail): ");
            int result = input.nextInt();

            // if...else is nested in the while statement
            if (result == 1)
                passes = passes+1;
            else
                failures = failures+1;

            // increment studentCounter so loop eventually terminates
            studentCounter = studentCounter+1;
        }

        // termination phase; prepare and display results
        System.out.printf("Passed: %d%nFailed: %d%n", passes, failures);

        // determine whether more than 8 students passed
        if (passes >8)
            System.out.println("Bonus to instructor!");
    }
}
```

```
Enter result (1 = pass, 2 = fail): 1
Enter result (1 = pass, 2 = fail): 2
Enter result (1 = pass, 2 = fail): 1
Enter result (1 = pass, 2 = fail): 1
Enter result (1 = pass, 2 = fail): 1
Enter result (1 = pass, 2 = fail): 1
Enter result (1 = pass, 2 = fail): 1
Enter result (1 = pass, 2 = fail): 1
Enter result (1 = pass, 2 = fail): 1
Enter result (1 = pass, 2 = fail): 1
Passed: 9
Failed: 1
Bonus to instructor!
```

```
Enter result (1 = pass, 2 = fail): 1
Enter result (1 = pass, 2 = fail): 2
Enter result (1 = pass, 2 = fail): 1
Enter result (1 = pass, 2 = fail): 2
Enter result (1 = pass, 2 = fail): 1
Enter result (1 = pass, 2 = fail): 2
Enter result (1 = pass, 2 = fail): 2
Enter result (1 = pass, 2 = fail): 1
Enter result (1 = pass, 2 = fail): 1
Enter result (1 = pass, 2 = fail): 1
Passed: 6
Failed: 4
```

## 4.12 Compound Assignment Operators

<table>
    <caption>Arithmetic compound assignment operators</caption>
    <thead>
        <tr>
            <th>Assignment operator</th>
            <th>Sample expression</th>
            <th>Explanation</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td><span markdown=1>`+=`</span></td>
            <td><span markdown=1>`x += n`</span></td>
            <td><span markdown=1>`x = x+n`</span></td>
        </tr>
        <tr>
            <td><span markdown=1>`-=`</span></td>
            <td><span markdown=1>`x -= n`</span></td>
            <td><span markdown=1>`x = x-n`</span></td>
        </tr>
        <tr>
            <td><span markdown=1>`*=`</span></td>
            <td><span markdown=1>`x *= n`</span></td>
            <td><span markdown=1>`x = x*n`</span></td>
        </tr>
        <tr>
            <td><span markdown=1>`/=`</span></td>
            <td><span markdown=1>`x /= n`</span></td>
            <td><span markdown=1>`x = x/n`</span></td>
        </tr>
        <tr>
            <td><span markdown=1>`%=`</span></td>
            <td><span markdown=1>`x %= n`</span></td>
            <td><span markdown=1>`x = x%n`</span></td>
        </tr>
    </tbody>
</table>

## 4.13 Increment and Decrement Operators

<table>
    <caption>Increment and decrement operators</caption>
    <thead>
        <tr>
            <th>Operator</th>
            <th>Sample expression</th>
            <th>Explanation</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td><span markdown=1>`++`(prefix increment)</span></td>
            <td><span markdown=1>`a++`</span></td>
            <td><span markdown=1>Increment `a` by 1, then use the new value of `a` in the expression in which `a` resides</span></td>
        </tr>
        <tr>
            <td><span markdown=1>`++`(postfix increment)</span></td>
            <td><span markdown=1>`++a`</span></td>
            <td><span markdown=1>Use the current value of `a` in the expression in which `a` resides, then increment `a` by 1</span></td>
        </tr>
        <tr>
            <td><span markdown=1>`--`(prefix decrement)</span></td>
            <td><span markdown=1>`a--`</span></td>
            <td><span markdown=1>Decrement a by 1, then use the new value of a in the expression in which a resides</span></td>
        </tr>
        <tr>
            <td><span markdown=1>`--`(postfix decrement)</span></td>
            <td><span markdown=1>`--a`</span></td>
            <td><span markdown=1>Use the current value of `a` in the expression in which `a` resides, then decrement `a` by 1</span></td>
        </tr>
    </tbody>
</table>

```java
// Fig. 4.15; Increment.java
// Prefix increment and postfix increment operators

public class Increment {
    public static void main(String[] args) {
        // demonstrate postfix increment operator
        int c = 5;
        System.out.printf("c before postincrement: %d%n", c);  // prints 5
        System.out.printf("       postincrement c: %d%n", c++);  // printf 5
        System.out.printf(" c after postincrement: %d%n", c);  // printf 6

        System.out.println();  // skip a line

        // demonstrate prefix increment operator
        c = 5;
        System.out.printf("c before postincrement: %d%n", c);  // prints 5
        System.out.printf("       postincrement c: %d%n", ++c);  // printf 6
        System.out.printf(" c after postincrement: %d%n", c);  // printf 6
    }
}
```

```
c before postincrement: 5
       postincrement c: 5
 c after postincrement: 6

c before postincrement: 5
       postincrement c: 6
 c after postincrement: 6
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
            <td><span markdown=1>`++` `--`</span></td>
            <td>$\leftarrow$</td>
            <td>unary postfix</td>
        </tr>
        <tr>
            <td><span markdown=1>`++` `--` `+` `-` `(type)`</span></td>
            <td>$\leftarrow$</td>
            <td>unary prefix</td>
        </tr>
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
            <td><span markdown=1>`?:`</span></td>
            <td>$\leftarrow$</td>
            <td>conditional</td>
        </tr>
        <tr>
            <td><span markdown=1>`=` `+=` `-=` `*=` `/=` `%=`</span></td>
            <td>$\leftarrow$</td>
            <td>assignment</td>
        </tr>
    </tbody>
</table>

## 4.14 Primitive Types

- Java requires all variables to have a type, like C and C++

    - Java is referred to as a strongly type language

- Primitive types in Java are portable across all platfrom that support for Java
