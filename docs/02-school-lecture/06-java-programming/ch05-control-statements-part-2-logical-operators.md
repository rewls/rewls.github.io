---
layout: default
title: Ch5 Control Statements - Part 2; Logical Operators
parent: Java Programming
grand_parent: School Lecture
nav_order: 6
mathjax: true
mermaid: true
permalink: /docs/java/ch5
---

# Ch5 Control Statements: Part 2; Logical Operators
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

- Learn the essentials of counter-controlled iteration

- Use the `for` and `do...while` iteration statements to execute statements in a program repeatedly

- Understand multiple selection using the `switch` selection statement

- Implement an object-oriented `AutoPolicy` case study using `String`s in `switch` statements

- Alter the flow of control with the `break` and `continue` program-control statements

- Use the logical operators to form complex conditional expressions in control statements

## 5.2 Essentials of counter-Controlled Iteration

```java
// Fig. 5.1: WhileCounter.java
// Counter-controlled iteration with the while iterations statement

public class WhileCounter {
    public static void main(String[] args) {
        int counter = 1;  // declare and initialize control variable

        while (counter <= 10) {  // loop-continuation condition
            System.out.printf("%d  ", counter);
            ++counter;  // increment control variable
        }

        System.out.println();
    }
}
```

```
1  2  3  4  5  6  7  8  9  10
```

> Common Programming Error 5.1
>
> Because floating-point values may be approximate, controlling loops with floating-point variables may result in imprecise counter values and inaccurate termination tests

> Error-Prevention Tip 5.1
>
> Use integers to control counting loops

## 5.3 `for` Iteration Statement

```java
// Fig. 5.2: ForCounter.java
// Counter-controlled iteration with the for iteration statement

public class ForCounter {
    public static void main(String[] args) {
        // for statement header includes initialization, loop-continuation condition and increment
        for (int counter=1; counter<=10; counter++)
            System.out.printf("%d  ", counter);

        System.out.println();
    }
}
```

```
1  2  3  4  5  6  7  8  9  10
```

- If the initialization expression in the `for` header declares the control variable, the control variable can be used only in that `for` statement

### Two equivalent counter-controlled statements

```java
for (initialization; loopcontinuationCondition; increment)
    statement;
```

```java
initialization;
while (loopcontinuationCondition) {
    statement;
    increment;
}
```

- Typically, `for` statements are used for counter-controlled repetition and `while` statements for sentinel-controlled repetition

## 5.4 Example Using the `for` Statement

```java
// Fig. 5.5: Sum.java
// Summing integers with the for statement

public class Sum {
    public static void main(String[] args) {
        int total = 0;

        // total even integers from 2 through 20
        for (int number=2; number<=20; number+=2)
            total += number;

        System.out.printf("Sum is %d%n", total);
    }
}
```

```
Sum is 110
```

### Compound interest application (Fig. 5.6)

- A person invests $1000 in a savings account yielding 5% interest. Assuming that all the interest is left on deposit, calculate and print the amount of money in the account at the end of each year for 10 years. Use the following formula to determine the amounts:

$$
a = p(1+r)^n
$$

- where

    - $p$ is the original amount invested (i.e. the principal)

    - $r$ is the annual interest rate (e.g. use 0.05 for 5%)

    - $n$ is the number of years

    - $a$ is the amount on deposit at the end of the $n$th year

```java
// Fig. 5.6: Interest.java
// compound-interest calculations with for

public class Interest {
    public static void main(String[] args) {
        double principal = 1000.0;  // initial amount before interest
        double rate = 0.05;  // interest rate

        // display headers
        System.out.printf("%s%20s%n", "Year", "Amount on deposit");

        // calculate amount on deposit for each of ten years
        for (int year=1; year<=10; ++year) {
            // calculate new amount on deposit for specified year
            double amount = principal * Math.pow(1.0+rate, year);

            // display the year and the amount
            System.out.printf("%4d%,20.2f%n", year, amount);
        }
    }
}
```

```
Year   Amount on deposit
   1            1,050.00
   2            1,102.50
   3            1,157.63
   4            1,215.51
   5            1,276.28
   6            1,340.10
   7            1,407.10
   8            1,477.46
   9            1,551.33
  10            1,628.89
```

##### Format specifier `%20s`

- a field width of 20

- right justified in the field by default

- more characters than the field width

    - the field width would be extended to the right to accommodate the entire value

##### Format specifier `%-20s`

- left justified by minus sign formatting flag

##### Calling a `static` method

- `ClassName.methodName(arguments)`

- `Math.pow(x, y)`

    - calculates the value of `x` raised to the `y`th power

    - receives two `double` arguments and returns a `double` value

##### Format specifier `%,20.2f`

- comma(`,`) formatting flag

    - output with a grouping separator

- `20`

    - right justified in a field width of 20 characters

- `.2`

    - the formatted number's precision

## 5.5 `do...while` Iteration Statement

```java
// Fig. 5.7: DoWhileTest.java
// do...while iteration statement

public class DoWhileTest {
    public static void main(String[] args) {
        int counter = 1;

        do {
            System.out.printf("%d  ", counter);
            ++counter;
        } while (counter <= 10);

        System.out.println();
    }
}
```

```
1  2  3  4  5  6  7  8  9  10
```

## 5.6 `switch` Multiple-Selection Statement

```java
switch (controlling expression) {
    case label:
        statements;
        break;
    case label:
        statements;
        break;
    ...
    default:
        statements;
        break;
}
```

### Controlling expression

- an integral value of type `byte`, `char`, `short` or `int`

- a `String`

- enumeration value

### Label

- constant integral expression of type `byte`, `char`, `short` or `int`

- a `String`

- enumeration constant

```java
switch (controlling expression) {
    case label:
        statements;
    case label:
        statements;
        break;
    ...
    default:
        statements;
        break;
}
```

```java
import java.util.Scanner;

public class Switch {
    public static void main(String[] argc) {
        Scanner input = new Scanner(System.in);
        int num;
        String number = input.next();

        switch (number) {
            case "one":
                num = 1;
                break;
            case "two":
                num = 2;
                break;
            case "three":
                num = 3;
                break;
            default:
                num = 0;
                break;
        }
    }
}
```

```java
// Fig. 5.9: LetterGrades.java
// LetterGrades class uses the switch statements to count letter grades

import java.util.Scanner;

public class LetterGrades {
    public static void main(String[] args) {
        int total = 0;  // sum of grades
        int gradeCounter = 0;  // number of grades entered
        int aCount = 0;  // count of A grades
        int bCount = 0;  // count of B grades
        int cCount = 0;  // count of C grades
        int dCount = 0;  // count of D grades
        int fCount = 0;  // count of F grades

        Scanner input = new Scanner(System.in);

        System.out.printf("%s%n%s%n   %s%n   %s%n",
            "Enter the integer grades in the range 0-100.",
            "Type the end-of-file indicator to terminate input:",
            "On UNIX/Linux/macOS type <Ctrl> d then press Enter",
            "On Windows type <Ctrl> z then press Enter");

        // loop until user enters the end-of-file indicator
        while (input.hasNext()) {
            int grade = input.nextInt();  // read grade
            total += grade; // add grade to total
            ++gradeCounter;  // increment number of grades

            // increment appropriate letter-grade counter
            switch (grade/10) {
                case 9:  // grade was between 90
                case 10: // and 100, inclusive
                    ++aCount;
                    break;  // exits switch
                case 8:  // grade was between 80 and 89
                    ++bCount;
                    break;  // exits switch
                case 7: // grade was beween 70 and 79
                    ++cCount;
                    break;  // exits switch
                case 6: // grade was beween 60 and 69
                    ++dCount;;
                    break;
                default: // grade was less than 60
                    ++fCount;
                    break;  // optional; exits switch anyway
            }
        }

        // display grade report
        System.out.printf("%nGrade Report:%n");

        // if user entered at least one grade
        if (gradeCounter > 0) {
            // calculate average of all grades entered
            double average = (double)total / gradeCounter;

            // output summary of results
            System.out.printf("Total of the Td grades entered is %d%n", gradeCounter, total);
            System.out.printf("Class average is %.2f%n", average);
            System.out.printf("%n%s%n%s%d%n%s%d%n%s%d%n%s%d%n%s%d%n",
                "Number of students who received each grade:",
                "A: ", aCount,  // display nGrade of A grades
                "B: ", bCount,  // display nGrade of B grades
                "C: ", cCount,  // display nGrade of C grades
                "D: ", dCount,  // display nGrade of D grades
                "F: ", fCount);  // display nGrade of F grades
        } else  // no grades were entered, so output appropriate message
            System.out.println("No grades were entered");
    }
}
```

```
Enter the integer grades in the range 0-100.
Type the end-of-file indicator to terminate input:
   On UNIX/Linux/macOS type <Ctrl> d then press Enter
   On Windows type <Ctrl> z then press Enter
99
92
45
57
63
71
76
85
90
100

Grade Report:
Total of the Td grades entered is 10
Class average is 77.80

Number of students who received each grade:
A: 4
B: 1
C: 2
D: 1
F: 2
```

### `Scanner` method `hasNext`

- determine whether there is more data to input

- it returns `true` if there is more data

- it return `false` if the end-of-file indicator has been typed

- 입력 대기 상태로 기다리며 프로그램이 진행 되지 않음

- 입력을 하고 엔터키를 누른 경우, 버퍼에 데이터가 있으면 버퍼는 그대로 둔 채 `true` 반환

- 버퍼에 ctrl+d가 있으면 버퍼를 비우고 `false` 반환

## 5.8 `break` and `continue` Statements

- `break` in a `while`, `for`, `do...while` or `switch`

<div class=mermaid>
graph LR;
    break-->next;
</div>

```java
for (; ; ) {
    ...
    break;
    ...
}
next;
```

```java
while (...) {
    ...
    break;
    ...
}
next;
```

```java
do {
    ...
    break;
    ...
} while (...);
next;
```

<div class=mermaid>
graph LR;
    break2[break in for]-->next1;
    break1[break out of for]-->next2;
</div>

```java
while (...) {
    ...
    break;
    for (; ; ) {
        ...
        break;
        ...
    }
    next1;
}
next2;
```

```java
// Fig. 5.13: BreakTest.java
// break statement exiting a for statement

public class BreakTest {
    public static void main(String[] args) {
        int count; // control variable also used after loop terminates
        for (count=1; count<=10; count++) {  // loop 10 times
            if (count == 5)
                break;  // terminates loop if count is 5
            System.out.printf("%d ", count);
        }
        System.out.printf("%nBroke out of loop at count = %d%n", count);
    }
}
```

```
BreakTest
1 2 3 4
Broke out of loop at count = 5
```

- `continue` in `while`, `for` or `do...while`

<div class=mermaid>
graph LR;
    continue-->inc;
    subgraph noExecute[No execute];
        stmt1;
        stmt2;
    end;
</div>

```java
for (init; cond; inc) {
    ...
    continue;

    stm1;
    stm2;
}
```

```java
while (cond) {
    ...
    continue;

    stmt1;
    stmt2;
}
```

```java
do {
    ...
    continue;

    stmt1;
    stmt2;
} while (cond);
```

<div class=mermaid>
graph LR;
    continue1[continue out of for]-->cond1;
    continue2[continue in for]-->inc;
    subgraph noExecute[No execute];
        stmt1;
        stmt2;
    end;
</div>

```java
while (cond1) {
    ...
    continue;

    for (init; cond2; inc) {
        ...
        continue;

        stmt1;
        stmt2;
    }
}
```

```java
// Fig. 5.14: ContinueTest.java
// continue statement terminating an iteration of a for statement

public class ContinueTest {
    public static void main(String[] args) {
        for (int count=1; count<=10; count++) {  // loop 10 times
            if (count == 5)
                continue;  // skip remaining code loop body if count is 5
            System.out.printf("%d ", count);
        }
        System.out.printf("%nUsed continue to skip printing 5%n");
    }
}
```

```
1 2 3 4 6 7 8 9 10
Used continue to skip printing 5
```

## 5.9 Logical Operators

### Logical operators

- short-circuit evaluation

    - `&&` (conditional AND)

    - `||` (conditional OR)

- always evaluate both of its operands

    - `&` (boolean logical AND)

    - `|` (boolean logical inclusive OR)

    - `^` (boolean logical exclusive OR)

- `!` (logical NOT, logical negation or logical complement

> NOTE
>
> The `&`, `|` and `^` operators are also bitwise operators when they are applied to integral operands.

<table>
    <caption><span markdown=1>`&&` (conditional AND) operator truth table</span></caption>
    <thead>
        <tr>
            <th><span markdown=1>`expression1`</span></th>
            <th><span markdown=1>`expression2`</span></th>
            <th><span markdown=1>`expression1 && expression2`</span></th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td><span markdown=1>`false`</span></td>
            <td><span markdown=1>`false`</span></td>
            <td><span markdown=1>`false`</span></td>
        </tr>
        <tr>
            <td><span markdown=1>`false`</span></td>
            <td><span markdown=1>`true`</span></td>
            <td><span markdown=1>`false`</span></td>
        </tr>
        <tr>
            <td><span markdown=1>`true`</span></td>
            <td><span markdown=1>`false`</span></td>
            <td><span markdown=1>`false`</span></td>
        </tr>
        <tr>
            <td><span markdown=1>`true`</span></td>
            <td><span markdown=1>`true`</span></td>
            <td><span markdown=1>`true`</span></td>
        </tr>
    </tbody>
</table>

<table>
    <caption><span markdown=1>`||` (conditional OR) operator truth table</span></caption>
    <thead>
        <tr>
            <th><span markdown=1>`expression1`</span></th>
            <th><span markdown=1>`expression2`</span></th>
            <th><span markdown=1>`expression1 || expression2`</span></th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td><span markdown=1>`false`</span></td>
            <td><span markdown=1>`false`</span></td>
            <td><span markdown=1>`false`</span></td>
        </tr>
        <tr>
            <td><span markdown=1>`false`</span></td>
            <td><span markdown=1>`true`</span></td>
            <td><span markdown=1>`true`</span></td>
        </tr>
        <tr>
            <td><span markdown=1>`true`</span></td>
            <td><span markdown=1>`false`</span></td>
            <td><span markdown=1>`true`</span></td>
        </tr>
        <tr>
            <td><span markdown=1>`true`</span></td>
            <td><span markdown=1>`true`</span></td>
            <td><span markdown=1>`true`</span></td>
        </tr>
    </tbody>
</table>

<table>
    <caption><span markdown=1>`^` (boolean logical exclusive OR) operator truth table</span></caption>
    <thead>
        <tr>
            <th><span markdown=1>`expression1`</span></th>
            <th><span markdown=1>`expression2`</span></th>
            <th><span markdown=1>`expression1 ^ expression2`</span></th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td><span markdown=1>`false`</span></td>
            <td><span markdown=1>`false`</span></td>
            <td><span markdown=1>`false`</span></td>
        </tr>
        <tr>
            <td><span markdown=1>`false`</span></td>
            <td><span markdown=1>`true`</span></td>
            <td><span markdown=1>`true`</span></td>
        </tr>
        <tr>
            <td><span markdown=1>`true`</span></td>
            <td><span markdown=1>`false`</span></td>
            <td><span markdown=1>`true`</span></td>
        </tr>
        <tr>
            <td><span markdown=1>`true`</span></td>
            <td><span markdown=1>`true`</span></td>
            <td><span markdown=1>``</span></td>
        </tr>
    </tbody>
</table>

<table>
    <caption><span markdown=1>`!` (logical NOT) operator truth table</span></caption>
    <thead>
        <tr>
            <th><span markdown=1>`expression1`</span></th>
            <th><span markdown=1>`!expression1`</span></th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td><span markdown=1>`false`</span></td>
            <td><span markdown=1>`true`</span></td>
        </tr>
        <tr>
            <td><span markdown=1>`true`</span></td>
            <td><span markdown=1>`false`</span></td>
        </tr>
    </tbody>
</table>

```java
// Fig. 5.19: LogicalOperators.java
// Logical operators

public class LogicalOperators {
    public static void main(String[] args) {
        // create truth table for && (conditional AND) operator
        System.out.printf("%s%n%s: %b%n%s: %b%n%s: %b%n%s: %b%n%n",
            "Conditional AND (&&)", "false && false", (false && false),
            "false && true", (false && true),
            "true && false", (true && false),
            "true && true", (true && true));

        // create truth table for || (conditional OR) operator
        System.out.printf("%s%n%s: %b%n%s: %b%n%s: %b%n%s: %b%n%n",
            "Conditional OR (||)", "false || false", (false || false),
            "false || true", (false || true),
            "true || false", (true || false),
            "true || true", (true || true));

        // create truth table for & (boolean logical AND) operator
        System.out.printf("%s%n%s: %b%n%s: %b%n%s: %b%n%s: %b%n%n",
            "Boolean logical AND (&)", "false & false", (false & false),
            "false & true", (false & true),
            "true & false", (true & false),
            "true & true", (true & true));

        // create truth table for | (boolean logical inclusive OR) operator
        System.out.printf("%s%n%s: %b%n%s: %b%n%s: %b%n%s: %b%n%n",
            "Boolean logical inclusive OR (|)", "false | false", (false | false),
            "false | true", (false | true),
            "true | false", (true | false),
            "true | true", (true | true));

        // create truth table for ^ (boolean logical exclusive OR) operator
        System.out.printf("%s%n%s: %b%n%s: %b%n%s: %b%n%s: %b%n%n",
            "Boolean logical exclusive OR (^)", "false ^ false", (false ^ false),
            "false ^ true", (false ^ true),
            "true ^ false", (true ^ false),
            "true ^ true", (true ^ true));

        // create truth table for ! (boolean negation) operator
        System.out.printf("%s%n%s: %b%n%s: %b%n", "Logical NOT (!)",
            "!false", (!false), "!true", (!true));
    }
}
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
            <td><span markdown=1>`&`</span></td>
            <td>$\leftarrow$</td>
            <td>boolean logical AND</td>
        </tr>
        <tr>
            <td><span markdown=1>`^`</span></td>
            <td>$\leftarrow$</td>
            <td>boolean logical exclusive OR</td>
        </tr>
        <tr>
            <td><span markdown=1>`|`</span></td>
            <td>$\leftarrow$</td>
            <td>boolean logical inclusive OR</td>
        </tr>
        <tr>
            <td><span markdown=1>`&&`</span></td>
            <td>$\leftarrow$</td>
            <td>conditional AND</td>
        </tr>
        <tr>
            <td><span markdown=1>`||`</span></td>
            <td>$\leftarrow$</td>
            <td>conditional OR</td>
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
