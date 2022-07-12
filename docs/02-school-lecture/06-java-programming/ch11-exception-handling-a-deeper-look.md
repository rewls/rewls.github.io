---
layout: default
title: Ch11 Exception Handling - A Deeper Look
parent: Java Programming
grand_parent: School Lecture
nav_order: 12
mathjax: true
mermaid: true
permalink: /docs/java/ch11
---

# Ch11 Exception Handling - A Deeper Look
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

## Object

- Learn why exception handling is an effective mechanism for respeonding to runtime problems

- Use `try` blocks to delimit code in which exceptions might occur

- Use `throw` to indicate a problem

- Use `catch` blocks to specify exception handlers

- Learn when to use exception handling

- Understand the exception class hierarchy

- User the `finally` block to release resources

- Chain exceptions by catching one exception and throwing another

- Create user-defined exceptions

- Use the debugging feature `assert` to state conditions that should be true at a particular

- Learn how `try`-with-resources can automatically release a resource when the `try` block terminates

---

## 11.1 Introduction

- Exception is an indication of a problem that occurs during a program's execution

- With exception handling, a program can continue executing (rather than terminating) after dealing with a problem

- Only classes that extend `Throwable`(packcage `java.lang`) directly or indirectly can be used with exception handling

### `ArrayIndexOutOfBoundsException`

- Occurs when an attempt is made to access an element past either end of an array

### `ClassCastException`

- Occurs when an attempt is made to cast an object that does not have an is-a relationship with the type specified in the cast operator

### `NullPointerException`

- Occurs when a `null` reference is used where an object is expected

---

## 11.2 Example: Divide by Zero without Exception Handling

- Java does not allow division by zero in integer arithmetic

	- Throws an `ArithmeticException`

	- An error message provides more specific information("/ by zero");

- Java does allow division by zero with floating-point values

	- `Infinity` or `-Infinity`

	- NaN(not a number), if 0.0 is divided by 0.0

```java
// Fig. 11.2: DivideByZeroNoExceptionHandling.java
// Integer division without exception handling.
import java.util.Scanner;

public class DivideByZeroNoExceptionHandling {
    // demonstrates throwing an exception when a divide-by-zero occurs
    public static int quotient(int numerator, int denominator) {
        return numerator / denominator;  // possible division by zero
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        System.out.print("Please enter an integer numerator: ");
        int numerator = scanner.nextInt();
        System.out.print("Please enter an integer denominator: ");
        int denominator = scanner.nextInt();

        int result = quotient(numerator, denominator);
        System.out.printf(
            "%nResult: %d / %d = %d%n", numerator, denominator, result);
    }
}
```

```
Please enter an integer numerator: 100
Please enter an integer denominator: 7

Result: 100 / 7 = 14
```

```
Please enter an integer numerator: 100
Please enter an integer denominator: 0
Exception in thread "main" java.lang.ArithmeticException: / by zero  // 1
// stack trace
        at DivideByZeroNoExceptionHandling.quotient(DivideByZeroNoExceptionHandling.java:8)  // 2
        at DivideByZeroNoExceptionHandling.main(DivideByZeroNoExceptionHandling.java:19)  // 3
```

1. `ArithmeticException`: exception name

2. the top of the call chain: throw point $---$ the initial point at which the exception occurs

3. starting point of call chain

- Each line in stack trace consists of class name, method name, file name, and line number

```
Please enter an integer numerator: 100
Please enter an integer denominator: hello
Exception in thread "main" java.util.InputMismatchException
        at java.base/java.util.Scanner.throwFor(Scanner.java:943)
        at java.base/java.util.Scanner.next(Scanner.java:1598)
        at java.base/java.util.Scanner.nextInt(Scanner.java:2263)
        at java.base/java.util.Scanner.nextInt(Scanner.java:2217)
        at DivideByZeroNoExceptionHandling.main(DivideByZeroNoExceptionHandling.java:17)
```

- If a stack trace contains "Unknown Source" for a particular method

	- the debugging symbols for that method's class were not available to the JVM $---$ this is typically the case for the classes of the Java API

---

## 11.3 Example: Handling `ArithmeticException`s and `InputMismatchException`

```java
// Fig. 11.3: DivideByZeroWithExceptionHandling.java
// Handling ArithmeticExceptions and InputMismatchExceptions.
import java.util.InputMismatchException;
import java.util.Scanner;

public class DivideByZeroWithExceptionHandling {
    // demonstrates throwing an exception when a divide-by-zero occurs
    public static int quotient(int numerator, int denominator)
        throws ArithmeticException {
        return numerator / denominator;  // possible division by zero
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        boolean continueLoop = true;  // determines if more input is needed

        do {
            try { // read two numbers and calculate quotient
                System.out.print("Please enter an integer numerator: ");
                int numerator = scanner.nextInt();
                System.out.print("Please enter an integer denominator: ");
                int denominator = scanner.nextInt();

                int result = quotient(numerator, denominator);
                System.out.printf("%nResult: %d / %d = %d%n", numerator,
                    denominator, result);
                continueLoop = false;  // input successful; end looping
            }
            catch (InputMismatchException inputMismatchException) {
                System.err.printf("%nException: %s%n",
                    inputMismatchException);
                scanner.nextLine();  // discard input so user can try again
                System.out.printf(
                    "You must enter integers. Please try again.%n%n");
            }
            catch (ArithmeticException arithmeticException) {
                System.err.printf("%nException: %s%n", arithmeticException);
                System.out.printf(
                    "Zero is an invalid denominator. Please try again.%n%n");
            }
        } while (continueLoop);
    }
}
```

```
Please enter an integer numerator: 100
Please enter an integer denominator: 7

Result: 100 / 7 = 14
```

```
Please enter an integer numerator: 100
Please enter an integer denominator: 0

Exception: java.lang.ArithmeticException: / by zero
Zero is an invalid denominator. Please try again.

Please enter an integer numerator: 100
Please enter an integer denominator: 7

Result: 100 / 7 = 14
```

```
Please enter an integer numerator: 100
Please enter an integer denominator: hello

Exception: java.util.InputMismatchException
You must enter integers. Please try again.

Please enter an integer numerator: 100
Please enter an integer denominator: 7

Result: 100 / 7 = 14
```

### `try` block

- Encloses code that might `throw` an exception

- Encloses code that should not execute if an exception occurs

### `catch` block (`catch` clause or exception handler)

- Catches and handles an exception

- At least one `catch` block or a `finally` block(Section 11.6) must immediately follow the `try` block

- The exception parameter identifies the exception type the handler can process

- When an exception occurs in a `try` block, the `catch` block that executes is the first one whose type matches the type of the exception that occured

### `System.err`

- Use the `System.err` (standard error stream) object to output error messages

- By default, displays data to the command prompt

> Software Engineering Observation 11.2
>
> Exceptions may surface through
>
> 1. Explicitly mentioned code in a `try` block
>
> 2. Deeply nested method calls initiated by code in a `try` block
>
> 3. From the Java Virtual Machine as it executes Java bytecodes

### Multi-`catch` (introduced in Java SE 7)

```java
catch (Type1 | Type2 | Type3 e) {
}
```

- Any of the types (or their subclasses) can be caught in the exception handler

- Any number of `Throwable` types can be specified in a multi-`catch`

### Uncaught exception

- one for which there are no matching `catch` blocks

### multithreade model of program execution

- Each thread is a concurrent activity

- One program can have many threads

- If a program has only one thread an uncaught exception will cause the program to terminate

- If a program has multiple threads an uncaught exception will terminate only the thread where the exception ocurred

### If no exceptions are thrown in a `try` block

- The `catch` blocks are skipped

- control continues with the first statement after the `catch` blocks

### `throws` clause

- Specifies the exception a method might throws if problems occur

	- Such exceptions are typically not caught in the method's body

```java
public static int quotient(int numerator, int denominator)
  throws ArithmeticException {
return numerator / denominator;
}
```

- Contains a comma-separated list of the exceptions

	- May be thrown by statements in the method's body or by methods called from the body

- Method can throw exceptions of the classes listed in its `throws` clause or of their subclasses

### When method throws an exception

- the method terminates and does not return a value

- its local variables go out of scope

- If the local variables were references to objects and there were no other references to those objects

	- the objects would be available for garbage collection

---

## 11.5 Java Exception Hierarchy

<div hidden>
@startuml 11-portion-throwable-inheritance-hierarchy
package unchecked as uc1 {
	class RuntimeException
	class ClassCastException
	class IndexOutOfBoundsException
	class NullPointerException
	class NoSuchElementException
	class ArithmeticException
	class ArrayIndexOutOfBoundsException
	class InputMismatchException
}
package unchecked as uc2 {
	class Error
	class AWTError
	class ThreadDeath
	class VirtualMachineError
}
package checked {
	class Exception
	class IOException
}
class Exception extends Throwable
class Error extends Throwable
class RuntimeException extends Exception
class IOException extends Exception
class AWTError extends Error
class ThreadDeath extends Error
class VirtualMachineError extends Error
class ClassCastException extends RuntimeException
class IndexOutOfBoundsException extends RuntimeException
class NullPointerException extends RuntimeException
class NoSuchElementException extends RuntimeException
class ArithmeticException extends RuntimeException
class ArrayIndexOutOfBoundsException extends IndexOutOfBoundsException
class InputMismatchException extends NoSuchElementException
Exception -[hidden]> Error
RuntimeException -u[hidden]-> IOException
@enduml
</div>

<center markdown="block">
![portion-throwable-inheritance-hierarchy](/assets/java-programming/images/11-portion-throwable-inheritance-hierarchy.svg)

Fig. 11.4 Portion of class `Throwable`'s inheritance hierarchy
</center>

### Class `Throwable`

- Figure 11.4 shows a small portion of the inheritance hierarchy for class `Throwable`

- Only `Throwable` objects can be used with the exception- handling metchanism

- Class `Throwable` has two subclasses: `Exception` and `Error`

### Class `Exceiption` and its subclasses

- represent exceptional situations that can occur in a Java program

- These can be caught and handled by the application

### Class `Error` and its subclasses

- represent abnormal situations that happen in the JVM

- `Error`s happen infrequently

- These should not be caught by application

- Applications usually cannot recover from `Error`s

### Checked Exceptions

- Compiler enforces a catch-or-declare requirement for checked exceptions

- Subclasses of `Exception` but not `RuntimeException` are checked exceptions

	- Caused by conditions that are not in the control of the program

	- e.g. in file processiong, the program can't open a file because the file does not exist

### Unchecked Exceptions

- The compiler does not check the code to determine whether an unchecked

- Unchecked exceptions are not required to be listed in a method's `throws` clause

	- Even if they are, it's not required that such exceptions be caught by an applications

- Subclasses of class `RuntimeException` are unchecked exceptions

	- Typically caused by defects in your program's code

	- ex) `ArrayIndexOutOfBoundsException`, `ArithmeticException`s

- Subclasses of class `Error` are unchecked

### Catch-or-declare requirement

- The compiler checks each method call and method declaration to determine whether the method throws checked exceptions

- If so, the compiler verifies that the checked exception is caught or is declared in a `throws` clause

- If the catch-or-declare requirement is not satisfied

	- the compiler will issue an error message indicating that the exception must be caught or declared

##### To satisfy the `catch` part of the catch-or-declare requirement

- the code that generates the exception

	- must be wrapped in a `try` block

	- must provide a `catch` handler for the checked-exception type (or one of its superclasses)

##### To satisfy the declare part of the catch-of-declare requirement

- the method must provide a `throws` clause containing the checked-exception type after its parameter list and before its method body

> Error-Prevention Tip 11.2
>
> You must deal with checked exceptions. This results in more robust code than would be created if you were able to simply ignore them

> Common Programming Error 11.2
>
> If a subclass method overrides a superclass method, it's an error for the subclass method to list more exceptions in its `throws` clause than the superclass method does. However, a subclass's `throws` clause can contain a subset of a superclass's `throws` clause

> Software Engineering Observation 11.9
>
> Although the compiler does not enforce the catch-or-declare requirement for unchecked exceptions, provide appropriate exception-handling code when it's known that such exceptions might occur. For example, a program should process the `NumberFormatException` from `Integer` method `parseInt`, even though `NumberFormatException` is an indirect subclass of `RuntimeException` (and thus an unchecked exception). This makes your programs more robust

### `catch`

- a `catch` parameter of a superclass-type can also catch all of that exception type's subclass types

	- This enables catch to handle related exceptions polymorphically

<div hidden>
@startuml 11-polymorphic-catch
class ExceptionA extends Exception
class ExceptionB extends ExceptionA
class ExceptionC extends ExceptionB
@enduml
</div>

<center markdown="block">
![polymorphic-catch](/assets/java-programming/images/11-polymorphic-catch.svg)

Class diagram
</center>

```java
try {
    throw new _________;
} catch (Exception exception) {
    ...
}
```

- You can also catch each subclass type individually if those exceptions require different processing

```java
try {
    throw new _________;
} catch (ExceptionC exception) {
    ...
} catch (ExceptionB exception) {
    ...
} catch (ExceptionA exception) {
    ...
} catch (Exception exception) {
    ...
}
```

- If there multiple `catch` blocks match a particular exception type

	- only the first matching `catch` block executes

> Common Programming Error 11.3
>
> Placing a `catch` block for a superclass exception type before other `catch` blocks that catch subclass exception types would prevent those `catch` blocks from executing, so a compilation error occurs

---

## 11.6 `finally` Block

### Resouce leaks

- Programs that obtain resources must return them to the system explicitly to avoid so-called resource leaks

##### Memory leak

- Java automatically garbage collects memory no longer used by programs, thus avoiding most memory leaks

##### Other types of resource leak

- Files, database connections and network connections that are not closed properly might not be available for use in other programs

```java
try {
    statements
    resource-acquisition statements
} catch ( AKindOfException exception1) {
    exception-handling statements
}
...
catch (AutherKindOfException exception2) {
    exception-handling statements
} finally {
    statements
    resource-release statements
}
```

### `finally` block will execute

- whether or not an exception is thrown in the corresponding `try` block

- If a `try` block exits by using a `return`, `break` or `continue` statement or simply by reaching its closing right brace

### `finally` block will not execute

- If the application exits early from a `try` block by calling method `System.exit`

```java
// Fig. 11.5: UsingExceptions.java
// try...catch...finally exception handling mechanism.

public class UsingExceptions {
    public static void main(String[] args) {
        try {
            throwException();
        }
        catch (Exception exception) { // exception thrown by throwException
            System.err.println("Exception handled in main");
        }

        doesNotThrowException();
    }

    // demonstrate try...catch...finally
    public static void throwException() throws Exception {
        try { // throw an exception and immediately catch it
            System.out.println("Method throwException");
            throw new Exception();  // generate exception
        }
        catch (Exception exception) { // catch exception thrown in try
            System.err.println(
                "Exception handled in method throwException");
            throw exception;  // rethrow for further processing

            // code here would not be reached; would cause compilation errors

        }
        finally { // executes regardless of what occurs in try...catch
            System.err.println("Finally executed in throwException");
        }

        // code here would not be reached; would cause compilation errors
    }

    // demonstrate finally when no exception occurs
    public static void doesNotThrowException() {
        try { // try block does not throw an exception
            System.out.println("Method doesNotThrowException");
        }
        catch (Exception exception) { // does not execute
            System.err.println(exception);
        }
        finally { // executes regardless of what occurs in try...catch
            System.err.println("Finally executed in doesNotThrowException");
        }

        System.out.println("End of method doesNotThrowException");
    }
}
```

```
Method throwException
Exception handled in method throwException
Finally executed in throwException
Exception handled in main
Method doesNotThrowException
Finally executed in doesNotThrowException
End of method doesNotThrowException
```

### `System.out`, `System.err`

- Both `System.out` and `System.err` are streams $---$ a sequence of bytes

	- `System.out` (standard output stream) displays output

	- `System.err` (standard error stream) displays errors

- Output from these streams can be redirected

	- e.g., to a file

- Using two different streams enables you to easily separated error messages from other output

	- Data output from `System.err` could be sent to a log file

	- Data output from `System.out` can be displayed on the screen

### `throw` statement

- Used to throw exceptions

- Indicates that an error has occurred

- The operand of a `throw` can be an object of any class derived from class `Throwable`

### Rethrow an exception

- Done when a `catch` block cannot process that exceptions or can only parially process it

- Defers the exception handling (or perhaps a portion of it) to another `catch` block associated with an outer `try`

```java
try {
    ...
} catch (Exception exception) {
    throw exception;  // rethrow
}
```

---

## 11.7 Stack Unwinding and Obtaining Information from an Exception Object

### Stack unwinding

- When an exceptions is thrown but not caught in a particular scope, the method-call stack is "unwound"

- An attempt is made to `catch` the exception in the next outer `try` block

<center markdown="block">
![unwinding](/assets/java-programming/images/11-unwinding.png)

unwinding
</center>

```java
// Fig. 11.6: UsingExceptions.java
// Stack unwinding and obtaining data from an exception object.

public class UsingExceptions {
    public static void main(String[] args) {
        try {
            method1();
        }
        catch (Exception exception) { // catch exception thrown in method1
            System.err.printf("%s%n%n", exception.getMessage());
            exception.printStackTrace();

            // obtain the stack-trace information
            StackTraceElement[] traceElements = exception.getStackTrace();

            System.out.printf("%nStack trace from getStackTrace:%n");
            System.out.println("Class\t\tFile\t\t\tLine\tMethod");

            // loop through traceElements to get exception description
            // Each StackTraceElement represents one method call on the method-call stack
            for (StackTraceElement element : traceElements) {
                System.out.printf("%s\t", element.getClassName());
                System.out.printf("%s\t", element.getFileName());
                System.out.printf("%s\t", element.getLineNumber());
                System.out.printf("%s%n", element.getMethodName());
            }
        }
    }

    // call method2; throw exceptions back to main
    public static void method1() throws Exception {
        method2();
    }

    // call method3; throw exceptions back to method1
    public static void method2() throws Exception {
        method3();
    }

    // throw Exception back to method2
    public static void method3() throws Exception {
        throw new Exception("Exception thrown in method3");
    }
}
```

```
Exception thrown in method3

java.lang.Exception: Exception thrown in method3
        at UsingExceptions.method3(UsingExceptions.java:41)
        at UsingExceptions.method2(UsingExceptions.java:36)
        at UsingExceptions.method1(UsingExceptions.java:31)
        at UsingExceptions.main(UsingExceptions.java:7)

Stack trace from getStackTrace:
Class           File                    Line    Method
UsingExceptions UsingExceptions.java    41      method3
UsingExceptions UsingExceptions.java    36      method2
UsingExceptions UsingExceptions.java    31      method1
UsingExceptions UsingExceptions.java    7       main
```

### `Throwable` methods

<table>
	<caption><span markdown=1>`Throwable`</span></caption>
	<thead>
		<tr>
			<th>Method</th>
			<th>Discription</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td><span markdown=1>`printStackTrace`</span></td>
			<td>Outputs the stack trace to the standard error stream. Helpful in testing and debugging</td>
		</tr>
		<tr>
			<td><span markdown=1>`getStackTrace`</span></td>
			<td>Retrieve the stack-trace information</td>
		</tr>
		<tr>
			<td><span markdown=1>`getMessage`</span></td>
			<td>returns the desctiptive string stored in an exception</td>
		</tr>
	</tbody>
</table>

---

## 11.8 Chained Exceptions

- If a `catch` block throws a new exception, the original exception's information and stack trace are lost

<center markdown="block">
![stack-trace-lost](/assets/java-programming/images/11-stack-trace-lost.png)
</center>

- Chained exceptions enalbe an exception object to maintain the complete stack-trace information from the original exception

<center markdown="block">
![chained-exceptions](/assets/java-programming/images/11-chained-exceptions.png)

Chained Exception
</center>

```java
// Fig. 11.7: UsingChainedExceptions.java
// Chained exceptions.

public class UsingChainedExceptions {
    public static void main(String[] args) {
        try {
            method1();
        }
        catch (Exception exception) { // exceptions thrown from method1
            exception.printStackTrace();
        }
    }

    // call method2; throw exceptions back to main
    public static void method1() throws Exception {
        try {
            method2();
        }
        catch (Exception exception) { // exception thrown from method2
            // Chained exception
            throw new Exception("Exception thrown in method1", exception);
        }
    }

    // call method3; throw exceptions back to method1
    public static void method2() throws Exception {
        try {
            method3();
        }
        catch (Exception exception) { // exception thrown from method3
            // Chained exception
            throw new Exception("Exception thrown in method2", exception);
        }
    }

    // throw Exception back to method2
    public static void method3() throws Exception {
        // Original exception
        throw new Exception("Exception thrown in method3");
    }
}
```

```
java.lang.Exception: Exception thrown in method1
        at UsingChainedExceptions.method1(UsingChainedExceptions.java:20)
        at UsingChainedExceptions.main(UsingChainedExceptions.java:7)
Caused by: java.lang.Exception: Exception thrown in method2
        at UsingChainedExceptions.method2(UsingChainedExceptions.java:30)
        at UsingChainedExceptions.method1(UsingChainedExceptions.java:17)
        ... 1 more
Caused by: java.lang.Exception: Exception thrown in method3
        at UsingChainedExceptions.method3(UsingChainedExceptions.java:36)
        at UsingChainedExceptions.method2(UsingChainedExceptions.java:27)
        ... 2 more
```

---

## 11.9 Declaring New Exception Types

- A new exception class must extend an existing exception class to ensure that the class can be used with the exception-handling mechanism

```java
class MyException extends Throwable {
    public MyException() {
        super("error message:");
    }

    public MyException(String string) {
        super(string)
    }

    public MyException(MyException exception) {
        super(exception);
    }

    public MyException(String string, MyException exception) {
        super(string, exception);
    }
}
```

- A typical new exception class contains only four constructors

	1. One that takes no arguments and passes a default erre message `String` to the superclass constructor

	2. One that receives a customized error message as a `String` and passes it to the superclass constructor

	3. One that receives a `Throwable` (for chaining exceptions) and passes it to the superclass constructor

	4. one that receives a customized error message as a `String` and a `Throwable` (for chaining exceptions) and passes both to the superclass constructor

---

## 11.10 Preconditions and Postconditions

- Programmers spend significant amounts of time maintaining and debugging code

- To facilitate these tasks and to improve the overall design, they can specify the expected states before and after a method's execution

- These states are called preconditions and postconditions, respectively

- A preconditions must be true when a method is invoked

- A postcondition is true after the method successfully

- When preconditions or postconditions are not met, methods typically throw exception

---

## 11.11 Assertions

- `assert` evaluates a `boolean` expression and, if `false`, throws an `AssertionError` (a subclass of `Error`)

	```java
	assert expression;
	```

	- throws an `AssertionError` if `expression` is `false`

	```java
	assert expression1: expression2;
	```

	- throws an `AssertionError` with `expression2` as the error message if expression1 is `false`

### Usage

- To programmatically implement preconditions and postconditions

- To verify any other intermediate states that help you ensure your code is working correctly

- You use assertions primarily for debugging and identifying logic errors in an application

```java
// Fig. 11.8: AssertTest.java
// Checking with assert that a value is within range
import java.util.Scanner;

public class AssertTest {
    public static void main(String[] args) {
        Scanner input = new Scanner(System.in);

        System.out.print("Enter a number between 0 and 10: ");
        int number = input.nextInt();

        // assert that the value is >= 0 and <= 10
        assert (number >= 0 && number <= 10) : "bad number: " + number;

        System.out.printf("You entered %d%n", number);
    }
}
```

```
Enter a number between 0 and 10: 5
You entered 5
```

```
Enter a number between 0 and 10: 50
Exception in thread "main" java.lang.AssertionError: bad number: 50
        at AssertTest.main(AssertTest.java:13)
```

- You must explicitly *e*nable *a*ssertions when executing a program

	```shell
	java -ea AssertTest
	```

	- They reduce performance

	- They are unneccessary for the program's user

---

## 11.12 `try`-with-Resources: Automatic Resuource Deallocation

- `try`-with`-resources statement (introduced in Java SE 7)

	```java
	try (ClassName theObject = new className()) {
	    // use theObject here
	} catch (Exception e) {
	    // catch exceptions that occur while using the resource
	}
	```

- `ClassName` is a class that implements the `AutoCloseable` interface

- This code creates an object of type `ClassName` and uses it in the `try` block, then calls its `close` method to release any resources used by the object

- The `try`-with-resources statement implicitly calls the Object's `close` method at the end of the `try` block

- You can allocate multiple resources in the parentheses following try by separating them with a semicolon

> Software Engineering Observation 11.16
>
> Users shouldn't encounter `AssertionError`s $---$ these should be used only during program development. For this reason, you should't catch `AssertionError`s. Instead, allow the program to terminate, so you can see the error message, then locate and fix the source of the problem. You should not use `assert` to indicate runtime problems in produnction code (as we did in Fig. 11.8 for demonstration purposes) $---$ use the exception mechanism for this purpose

