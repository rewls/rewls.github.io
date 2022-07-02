---
layout: default
title: Ch1 Introduction to Computers, the Internet and Java
parent: Java Programming
grand_parent: School Lecture
nav_order: 1
mathjax: true
mermaid: true
permalink: /docs/java/ch1
---

# Ch1 Introduction to Computers, the Internet and Java
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

- Basic object-technology concepts

- A typical java program development environment

- Test-driving a jvava application

## 1.1 Intrdunction

### Java is widely used for implementing

- internet-based applications

- software for devices that communicate over a network

- enterprise programming

- mobile applications

### Java Editions: SE, EE and ME

##### Java Standard Edition (Java SE)

- is needed to develop desktop and server applications

- Programming paradigms

	- Procedural programming

	- Object-oriented programming

	- Generic programming

	- Functional programming (with lambdas and streams)

		- Java SE 8

	- Modularization of Java API classes

		- Java SE 9

##### Java Enterprise Edition (Java EE)

- geared toward developing large-scale, distributed networking applications and web-based applications

##### Java Micro Edition (Java ME)

- a subset of Java SE

- geared toward developing applications for resource-constrained embedded devices

> Java How to Program, 10th and 11th editions are based on Java SE 8 and Java SE 9

## 1.5 Introduction to Object Technology

### Class

- 같은 종류의 집단을 추상화(abstraction)하여 속성(attribute)과 행위(behavior)를 정의한 것

- 사용자 정의 데이터형

### Object

- 클래스의 인스턴스

- 고유 속성을 가지며 클래스에서 정의한 행위 수행 가능

- 객체의 행위는 클래스의 행위에 대한 정의를 공유함으로써 메모리를 경제적으로 사용할 수 있음

- class를 실체화(instantiation)한 것이 object

### Data Abstraction

- 불필요한 정보는 숨기고 중요한 정보만을 표현하는 것

- 자료추상화를 통해 정의된 자료형이 추상 자료형(ADT)

	- 자료 표현(속성)과 연산(행위)을 캡슐화(encapsulation) 함

	- 접근 제어를 통해서 자료형의 정보를 은닉(information hiding)함

### Object-Oriented Programming

- 일반적으로 추상 자료형을 클래스,

- 추상 자료형의 인스턴스를 객체,

- 추상 자료형에서 정의된 연산을 메소드(method),

- 메소드의 호출을 메시지(message)라고 한다.

	- 객체 사이의 정보전달은 메시지를 통해 일어난다.

### Inheritance

- 새로운 클래스가 기존 클래스의 속성과 행위를 이용할 수 있게 하는 것, 재사용(reuse)

- class B가 class A를 상속할 때 A는 상위 클래스, B는 하위 클래스라고 한다.

	- 상위 클래스 -(특수화)-> 하위 클래스

	- 하위 클래스 -(일반화)-> 상위 클래스

## 1.8 Java

- Microprocessors have had a profound impact in intelligent consumer-electronic devices

### 1991

- Sun Microsystems funded an internal corporate research project, green project led by James Gosling, which resulted in a C++-based object-oriented programming language that Sun called Java in 1995

- Key goal of Java

	- "write once, run anywhere."

### 2010

- Sun Microsystems was acquired by Oracle

### Java is now used

- to develop large-scale enterprise applications

- to enhance the functionality of web servers

- to provide applications for consumer devices

- to develop robotics software

- to develop Android smartphone and tablet apps

### Java Class Libraries

- rich collections of existing classes and methods

- known as the Java APIs(Application Programming Interfaces)

<center markdown="block">
![components-of-oracle-java-se-8-products](/assets/java-programming/images/1-components-of-oracle-java-se-8-products.png)

The components of Oracle's Java SE 8 products

[Java Platform Standard Edition 8 Documentation](https://docs.oracle.com/javase/8/docs/)
</center>

---

## 1.9 A Typical Java Development Environment

### Normally there are five phases

1. edit

2. compile

3. load

4. verify

5. execute

### Phase 1. Creating a Program

- Linux : vi

<div class='mermaid'>
graph LR;
	editor[Editor] --> secondaryStorage[Secondary Strorage];
	secondaryStorage --> editor;
</div>

- Editing phase: Program is created in an editor and stored in a file with a name ending in `.java`

### Phase 2. Compiling a Java Program into Bytecodes

- Use the command `javac` to compile a program

##### Java Virtual Machine (JVM)

- is a part of the JDK and the foundation of the Java platform

- executes bytecodes

- The JVM is invoked by the `java` command

##### Virtual Machine (VM)

- is a software application that simulates a computer

- hides the underlying OS and HW from the programs that interact with it

- ex) JVM or MS's .NET

##### Bytecode

- Bytecode instructions are platform independent

- Bytecodes are portable

	- The same bytecode instructions can execute on any platform containing a JVM that understands the version of Java in which the bytecode instructions were compiles

<div class='mermaid'>
graph LR;
	compiler[Compiler] --> secondaryStorage[Secondary Strorage];
	secondaryStorage --> compiler;
</div>

- Compilation phase: Compiler creates bytecodes and stores them in a file with a name ending  in `.class`

### Phase 3. Loading a Program into Memory

- the JVM places the program in memory to execute it - this is known as loading

- Class loader loads

	- the `.class` files containing the program's bytecodes

	- any of the `.class` files provided by Java that your program uses

- The `class` files can be loaded from a disk on your system or over a network

<div class='mermaid'>
graph LR;
	compiler[Compiler] --> primaryMemory[Primary Memory];
	primaryMemory --> compiler;
	compiler --> secondaryStorage[Secondary Strorage];
	secondaryStorage --> compiler;
</div>

- Loading phase: Class loader reads bytecodes from `.class` files and puts those bytecodes in memory

### Phase 4. Bytecode Verification

- As the classes are loaded, the bytecode verifier examines their bytecodes

- Ensures that they're valid and do not violate Java's secutiry restrictions

<div class='mermaid'>
graph LR;
	compiler[Compiler] --> primaryMemory[Primary Memory];
	primaryMemory --> compiler;
</div>

- Verification phase: Bytecode verifier comfirms that all bytecodes are valid and do not violate Java's secutiry restrictions

### Phase 5. Execution

- The JVM executes the program's bytecodes

- JVMs typically execute bytecodes using a combination of interpretation and so called just-in-time(JIT) compilation

	- In this process, the JVM analyzes the bytecodes as they're interpreted, searching for hot spots - bytecodes that execute frequently

	- For these parts, a just-inftime(JIT) compiler - such as Oracle's Java HotSpotTM compiler - translates the bytecodes into the underlying computer's machine language

	- When the JVM encounters these compiled parts again, the faster machine-language code executes

- Thus java programs go through two compilation phases

	- one in which source code is translated into bytecodes (for portability across JVMs on different computer platforms) and

	- a second in which, during execution, the bytecodes are translated into machine language for the computer on shich the program executes

<div class='mermaid'>
graph LR;
	JVM["Java Virtual Machine (JVM)"] --> primaryMemory[Primary Memory];
	primaryMemory --> JVM;
</div>

- Execution phase: To excute the program, the JVM reads bytecodes and just-in-time(JIT) compiles (i.e., translates) them into a language that the computer can understand. As the program executes, it may store data values in primary memory
