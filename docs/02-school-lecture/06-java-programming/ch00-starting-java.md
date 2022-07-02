---
layout: default
title: Ch0 Starting Java
parent: Java Programming
grand_parent: School Lecture
nav_order: 0
mathjax: true
mermaid: true
permalink: /docs/java/ch0
---

# Ch0 Starting Java
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

- OS: Arch linux

## Java 시작하기

```shell
java -version
```

### JRE 설치

- JRE (Java Runtime Environment)

```shell
sudo pacman -sS java | grep jre
```

```shell
sudo pacman -S jre-openjdk
```

### JDK 설치

- JDK (Java Development Kit)

```shell
sudo pacman -sS java | grep jdk
```

```shell
sudo pacman -S jdk-openjdk
```

### Test

```java
// HelloWorldTest.java

public class HelloWorldTest {
	public static void main(String[] args) {
		System.out.println("Hello World!");
	}
}
```

```java
javac HelloWorldTest.java
```

```java
java HelloWorldTest
```
