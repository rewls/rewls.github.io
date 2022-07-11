---
layout: default
title: Ch0 Starting Java
parent: Java Programming
grand_parent: School Lecture
nav_order: 1
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

> OS: Arch linux

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

### 여러 버전 사용

- 위 과정을 통해 여러 버전의 JDK, JRE 설치

- 설치된 버전 확인

	```shell
	archlinux-java status
	```

- 원하는 버전으로 세팅

	```shell
	sudo archlinux-java set <jdk 버전>
	```

- 적용된 버전 확인

	```shell
	java -version
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
