---
layout: default
title: Ch1 Introduction Number Systems and Conversion
parent: Logic Circuit
nav_order: 1
mathjax: true
---

# Ch1 Introduction Number Systems and Conversion
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

## 1.2 Number systems and conversion

- computer program은0(0V) 또는 1(5V)로 이루어져 있기 때문에 2진수를 잘 이해하는 것이 중요하다.

### 진법

##### 10진법(decimal)

- 0~9의 10가지 symbol을 사용하여 수 표현

##### 2진법(binary)

- 0~1의 2가지 symbol을 사용하여 수 표현

##### 16진법(hexadecimal)

- 0~9, A~F의 16개의 symbol을 사용하여 수 표현

- A~F는 10진수의 10~15에 대응된다.

##### R진법

- R가지 symbol을 사용하여 수 표현

### R진법에서 10진법으로 변환

##### 10진법 $\to$ 10진법

- $953.78 = 9 \cdot 10^2 + 5 \cdot 10^1 = 3 \cdot 10^0 + 7 \cdot 10^{-1} + 8 \cdot 10^{-2}$

##### 2진법 $\to$ 10진법

- $101.11_2 = 1 \cdot 2^2 + 0 \cdot 2^1 + 1 \cdot 2^0 + 1 \cdot 2^{-1} + 1 \cdot 2^{-2} = 5.75$

##### 16진법 $\to$ 10진법

- $A2F_{16} = A \cdot 16^2 + 2 \cdot 16^1 + F \cdot 16^0 = 10 \cdot 16^2 + 2 \cdot 16^1 + 15 \cdot 16^0 = 2607$

##### R진법 $\to$ 10진법

- $N = (a\_n \cdots a\_1 a\_0. a\_{-1} \cdots a\_{-m})\_R = a\_n R^n + \cdots + a\_1 R^1 + a\_0 R^0 + a\_{-1} R^{-1} + \cdots + a\_{-m} R^{-m}$

### 10진법에서 R진법으로 변환 - 정수 부분

##### 10진법 $\to$ 2진법

- $53 = 110101_2$

$$
\begin{matrix}
2)\underline{53} \\
\qquad 2)\underline{26} \cdots 1 \\
\qquad 2)\underline{13} \cdots 0 \\
\qquad 2)\underline{\,\;6} \cdots 1 \\
\qquad 2)\underline{\,\;3} \cdots 0 \\
\qquad\quad\; 1 \cdots 1
\end{matrix}
$$

##### 10진법 $\to$ 16진법

- $147 = 93_{16}$

$$
\begin{matrix}
16)\underline{147} \\
\qquad\quad\quad 9 \cdots 3
\end{matrix}
$$

##### 10진법 $\to$ R진법

- $N = (a_na{n-1} \cdots a_1a_0)_R$

$$
\begin{matrix}
R)\underline{N}\;\, \\
\qquad R)\underline{\Box} \cdots a_0 \\
\qquad R)\underline{\Box} \cdots a_1 \\
\;\;\vdots \\
\qquad\qquad\; a_n \cdots a_{n-1}
\end{matrix}
$$

##### 원리

$$
\begin{align*}
N &= (a_n a_{n-1} \cdots a_1 a_0)_R \\
  &= a_n R^n + a_{n-1}R^{n-1}+ \cdots + a_1 R^1 + a_0 \\
  &= (a_n R^{n-1} + a_{n-1}R^{n-2} + \cdots + a_1)R + a_0 \\
  &= (a_n R^{n-2} + a_{n-1}R^{n-3} + \cdots + a_2)R^2 + a_1R + a_0 \\
  &\;\;\vdots \\
  &= a_n R^{n} + a_{n-1}R^{n-1} + \cdots + a_2R^2 + a_1R + a_0
\end{align*}
$$

### 10진법에서 R진법으로 변환 - 소수 부분

##### 10진법 $\to$ 2진법

- $0.75 = 0.11_2$

$$
\begin{align*}
&\quad 0.75 \\
&\underline{\times \quad\;\,2} \\
&\quad 1.5 \\
&\underline{\times \quad2} \\
&\quad 1.0 \\
\end{align*}
$$

- $0.8 = 0.\dot{1}10\dot{0}_2$

$$
\begin{align*}
&\quad 0.8 \\
&\underline{\times \quad2} \\
&\quad 1.6 \\
&\underline{\times \quad2} \\
&\quad 1.2 \\
&\underline{\times \quad2} \\
&\quad 0.4 \\
&\underline{\times \quad2} \\
&\quad 0.8 \\
&\quad \vdots \\
\end{align*}
$$

##### 10진법 $\to$ R진법

- $F = (.a_{-1}a_{-2} \cdots a_{-m+1}a_{-m})_R$

$$
\begin{align*}
&\quad F \\
&\underline{\times \,R} \\
&\quad a_{-1}.\cdots \\
&\underline{\times \,R} \\
&\quad a_{-2}.\cdots \\
&\quad \vdots \\
&\quad a_{-m}.0 \\
\end{align*}
$$

##### 원리

$$
\begin{align*}
F &= (.a_{-1} a_{-2} \cdots a_{-m+1} a_{-m})_R \\
  &= a_{-1}R^{-1} + a_{-2}R^{-2} \cdots + a_{-m+1}R^{-m+1} + a_{-m}R^{-m} \\
  &= R^{-1}(a_{-1} + a_{-2}R^{-1} + \cdots + a_{-m+1}R^{-m+2} + a_{-m}R^{-m+1}) \\
  &= a_{-1}R^{-1} + R^{-2}(a_{-2} + \cdots + a_{-m+1}R^{-m+3} + a_{-m}R^{-m+2}) \\
  &\;\;\vdots \\
  &= a_{-1}R^{-1} + a_{-2}R^{-2} + \cdots + a_{-m+1}R^{-m+1} + a_{-m}R^{-m}
\end{align*}
$$

### 2진법에서 8진법, 16진법으로 변환

##### 방법

- 2진법 $\to$ 8진법: $8 = 2^3$이기 때문에 2진수를 소수점을 기준으로 세 자리씩 끊어서 각각의 수를 8진법으로 변환하면 8진수가 된다.

- 2진법 $\to$ 16진법: $16 = 2^4$이기 때문에 2진수를 소수점을 기준으로 네 자리씩 끊어서 각각의 수를 16진법으로 변환하면 16진수가 된다.

##### 2진법 $\to$ 16진법

- $1001101.010111_2 = 4D.5C$

	- 정수 부분

		$$
		\begin{matrix}
		10000)\underline{1001101} \\
		\qquad\qquad\;\, 100 \cdots 1101
		\end{matrix}
		$$

		$$
		\begin{align*}
		1001101_2 &= 1\cdot2^6 + 0\cdot2^5 + 0\cdot2^4 + 1\cdot2^3 + 1\cdot2^2 + 0\cdot2^1 + 1\cdot2^0 \\
		          &= 2^4(1\cdot2^2 + 0\cdot2^1 + 0\cdot2^0) + 0\cdot2^4 + 1\cdot2^3 + 1\cdot2^2 + 0\cdot2^1 + 1\cdot2^0 \\
				  &= 16^1\cdot4 + 16^0\cdot D \\
				  &= 4D_{16}
		\end{align*}
		$$

		- $100\_2 = 4\_{16}$, $1101\_2 = D\_{16}$, $\therefore 1001101\_2 = 4D\_{16}$

	- 소수 부분

		$$
		\begin{matrix}
		\qquad\;\; 0.010111 \\
		\underline{\times 10000\qquad\quad\;}\; \\
		 101.11\; \\
		\underline{\times 10000\quad\;}\qquad \\
		1100\qquad
		\end{matrix}
		$$

		$$
		\begin{align*}
		0.010111_2 &= 0\cdot2^{-1} + 1\cdot2^{-2} + 0\cdot2^{-3} + 1\cdot2^{-4} + 1\cdot2^{-5} + 1\cdot2^{-6} \\
		           &= 2^{-4}(0\cdot2^3 + 1\cdot2^2 + 0\cdot2^1 + 1\cdot2^0) + 2^{-8}(1\cdot2^3 + 1\cdot2^2) \\
				   &= 16^{-1}\cdot5 + 16^{-2}\cdot C \\
				   &= 0.5C_{16}
		\end{align*}
		$$

		- $0101\_2 = 5\_{16}$, $1100\_2 = C\_{16}$, $\therefore 0.010111\_2 = 0.5C\_{16}$

### 8진법, 16진법에서 2진법으로 변환

##### 방법

- 8진법 $\to$ 2진법: $8 = 2^3$이기 때문에 8진수의 각 자리수를 세 자리의 2진수로 변환하면 2진수가 된다.

- 16진법 $\to$ 2진법: $16 = 2^4$이기 때문에 8진수의 각 자리수를 네 자리의 2진수로 변환하면 2진수가 된다.

##### 16진법 $\to$ 2진법

- $1A.5E\_{16} = 11010.0101111_2$

	- 정수 부분

		$$
		\begin{align*}
		1A_{16} &= 1\cdot16^1 + A\cdot16^0 \\
				&= 1\cdot2^4 + (1\cdot2^3 + 0\cdot2^2 + 1\cdot2^1 + 0\cdot2^0)2^0 \\
				&= 1\cdot2^4 + 1\cdot2^3 + 0\cdot2^2 + 1\cdot2^1 + 0\cdot2^0 \\
				&= 11010_2
		\end{align*}
		$$

		- $1\_{16} = 0001\_{2}$, $A\_{16} = 1010\_2$, $\therefore 1A\_{16} = 11010\_2$

	- 소수부분

		$$
		\begin{align*}
		0.5E_{16} &= 5\cdot16^{-1} + E\cdot16^{-2} \\
				  &= (0\cdot2^3 + 1\cdot2^2 + 0\cdot2^1 + 1\cdot2^0)2^{-4} + (1\cdot2^3 + 1\cdot2^2 + 1\cdot2^1 + 0\cdot2^0)2^{-8} \\
				  &= 0\cdot2^{-1} + 1\cdot2^{-2} + 0\cdot2^{-3} 1\cdot2^{-4} + 1\cdot2^{-5} + 1\cdot2^{-6} + 1\cdot2^{-7} + 0\cdot2^{-8} \\
				  &= 0.0101111_2
		\end{align*}
		$$

		- $5\_{16} = 0101\_{2}$, $E\_{16} = 1110\_2$, $\therefore 0.5E\_{16} = 0.0101111\_2$

### R진법에서 S진법으로 변환

##### 방법

1. R진법 $\to$ 10진법

2. 10진법 $\to$ S진법

---

## 1.3 Binary Arithmetic

### Add

$$
\begin{matrix}
0 + 0 &=& 0 \\
0 + 1 &=& 1 \\
1 + 0 &=& 1 \\
1 + 1 &=& 0 & \text{and carry 1 to the next column}
\end{matrix}
$$

##### Example

- $1101 + 0011 = 10000$

$$
\begin{matrix}
\;\;\small 1\,1\,1 \\
\quad 1101 \\
\underline{+ \,0011} \\
\;10000
\end{matrix}
$$

- $1101 + 0101 + 1110 + 0101 = 100101$

$$
\begin{matrix}
\;\small10\,1\,1 \\
\quad 1101 \\
\quad 0101 \\
\quad 1110 \\
\underline{+ \,0101} \\
100101
\end{matrix}
$$

### Subtract

$$
\begin{matrix}
0 - 0 &=& 0 \\
0 - 1 &=& 1 & \text{and borrow 1 from the next column} \\
1 - 0 &=& 1 \\
1 - 1 &=& 0
\end{matrix}
$$

##### Example

$$
\begin{matrix}
\quad\small 10\;10 \\
\quad \cancel{1}\cancel{1}\,0\;1\;\; \\
\underline{- \,0\;1\;1\;0} \\
\qquad1\;1\;1
\end{matrix}
$$

### Multiply

$$
\begin{matrix}
0 \times 0 &=& 0 \\
0 \times 1 &=& 0 \\
1 \times 0 &=& 0 \\
1 \times 1 &=& 1
\end{matrix}
$$

##### Example

$$
\begin{matrix}
\quad 1101 \\
\underline{\times \,0110} \\
\quad0000 \\
1101 \\
\underline{+1101\quad\;}\; \\
1001110\;
\end{matrix}
$$

### Devide

##### Example

$$
\begin{matrix}
\qquad\qquad\;1101 \\
1011)\overline{10010001} \\
\qquad\quad\underline{1011\quad\;\;} \\
\qquad\quad\;\;111001 \\
\qquad\quad\;\;\underline{1011\quad} \\
\qquad\qquad\;\;1101 \\
\qquad\qquad\;\;\underline{1011} \\
\qquad\qquad\quad\;\;10
\end{matrix}
$$

---

- 프로그램은 SSD, 하드디스크에 저장된다.

- 프로그램이 실행되면 메모리에 올라간다.

- 덧셈을 하는 프로그램이라면 피연산자를 binary 형태로 지정된 크기의 메모리에 저장한 후 덧셈이 수행된다.

---

## 1.4 Representation of Negative Numbers

### 1. Sign and magnitude numbers

- $n$-bit sign and magnitude system은 최상위 비트 sign bit와 $n-1$개의 magnitude를 나타낼 수 있는 비트로 이루어진다.

- sign bit가 0이면 양수, 1이면 음수

- 표현범위: n-bit에서 $-(2^{n-1}-1) \sim 2^{n-1}-1$

##### Example

- 4-bit

	|0|0000|-0|1000|
	|1|0001|-1|1001|
	|2|0010|-2|1010|
	|3|0011|-3|1011|
	|4|0100|-4|1100|
	|5|0101|-5|1101|
	|6|0110|-6|1110|
	|7|0111|-7|1111|

	- 표현범위: -7~7

### 보수(complement)

> [참고](https://johngrib.github.io/wiki/complement-number/)

- R진법에서 두 가지의 보수가 정의된다.

	- R의 보수(R's complement)

	- (R-1)의 보수((R-1)'s complement)

##### R의 보수와 R-1의 보수의 관계

정수 r진수 N에 대하여

$$
R\text{'s complement of }N = \text{(R-1)'s complement of }N + 1
$$

##### R의 보수

정수 부분이 n개의 자리로 구성된 R진수 N에 대한 R의 보수는 다음과 같이 정의된다.

$$
R\text{'s complement of } N =
\begin{cases}
R^n - N & \text{if }N \ne 0 \\
0 & \text{if }N = 0
\end{cases}
$$

- 더해서 R^n이 되는 수가 R의 보수가 된다.

##### R-1의 보수

정수 부분이 n개의 자리로 구성되고 소수점 아래가 m개의 자리로 구성된 R진수 N에 대한 (R-1)의 보수는 다음과 같이 정의된다.

$$
(R-1)\text{'s complement of }N = R^n - R^{-m} - N
$$

- 정수의 경우 더해서 R^n - 1이 되는 수가 R-1의 보수가 된다.

##### Example

- 10진법

	- 7의 10의 보수 = 3

	- 27의 10의 보수 = 73

	- 123의 10의 보수 = 877

	- 7의 9의 보수 = 2

	- 27의 9의 보수 = 72

- 2진법

	- 101의 2의 보수 = 11

	- 101의 1의 보수 = 10

##### 사용 예

- $-35 + 40 = 5$

$$
\begin{align*}
-35 + 40 &= (100-35) + 40 - 100 \\
         &= 65 + 40 - 100 \\
		 &= 105 - 100 \\
		 &= 5
\end{align*}
$$

### 2. 1's complement

- 최상위 비트가 0이면 양수, 1이면 음수

- 표현범위: n-bit에서 $-(2^{n-1}-1) \sim 2^{n-1}-1$

- sign and magnitude 방법과 비교했을 때 음수의 앞뒤가 반점됨

##### Example

- 4-bit

	|0|0000|-0|1111|
	|1|0001|-1|1110|
	|2|0010|-2|1101|
	|3|0011|-3|1100|
	|4|0100|-4|1011|
	|5|0101|-5|1010|
	|6|0110|-6|1001|
	|7|0111|-7|1000|

	- 표현범위: -7~7

### 3. 2's complement

- 최상위 비트가 0이면 양수, 1이면 음수

- 표현범위: n-bit에서 $-(2^{n-1}) \sim 2^{n-1}-1$

- 1's complement 방법과 비교했을 때 음수가 한칸씩 밀림

- 대부분의 컴퓨터는 2's complement 방법을 이용하여 음수를 표현한다.

##### Example

- 4-bit

	|0|0000| | |
	|1|0001|-1|1111|
	|2|0010|-2|1110|
	|3|0011|-3|1101|
	|4|0100|-4|1100|
	|5|0101|-5|1011|
	|6|0110|-6|1010|
	|7|0111|-7|1001|
	| | |-8|1000|

	- 표현범위: -8~7

##### 장점

1. 0이 중복되어 표현되지 않는다.

2. 음수를 하나 더 표현할 수 있다.

3. 음수의 덧셈이 양수의 덧셈처럼 단순하게 수행된다.

---

- 대부분의 컴퓨터는 2's complement 방법을 이용하여 음수를 표현한다.

- 프로그래밍할 때 자료형의 표현범위를 고려하여 오버플로우가 생기지 않도록 자료형을 지정해야 한다.

---

## HW1

### 1.7

- Add in binary using 2's complement to represent negative numbers.

- Use a word length of 6 bits (including sign)

- Indicate if an overflow occurs

##### a

- $21 + 11 = 32$이므로 overflow

	- 2's complement로 음수를 표현할 때 6-bit 공간에서 수의 표현 범위는 -32~31

##### b

- $(-14) + (-32) = -46$이므로 overflow

	- 2's complement로 음수를 표현할 때 6-bit 공간에서 수의 표현 범위는 -32~31

##### c

- $(-25) + 18 = -7$

- $25 = 011001_2;\,-25 = 100111_2$

- $18 = 010010_2$

$$
\begin{matrix}
\quad100111 \\
\underline{+ \,010010} \\
\quad111001
\end{matrix}
$$

- $000111_2 =7; \,111001_2 = -7$

##### d

- $(-12)+13=1$

- $12 = 001100_2; \,-12 = 110100_2$

- $13 = 001101_2$

$$
\begin{matrix}
\quad 110100\\
\underline{+ \,001101} \\
\quad 000001
\end{matrix}
$$

##### e

- $(-11)+(-21)=-32$

- $11 = 001011_2; \,-11 = 110101_2$

- $21 = 010101_2; \,-21 = 101011_2$

$$
\begin{matrix}
\quad 110101\\
\underline{+ \,101011} \\
\quad 100000
\end{matrix}
$$

- $100000 = -32$

### 1.46

- $B = b_{n-1}b_{n-2}\cdots b_1b_0$, $B$는 n-bit 2's complement integer

- $B = -b_{n-1}2^{n-1} + b_{n-2}2^{n-2} + b_{n-3}2^{n-3} + \cdots + b_12 + b_0$

- Hint: $b_{n-1} = 0$, $b_{n-1} =1$ 나눠서 2's complement 정의 생각

##### Answer

- $b_{n-1} = 0$

	- $0b_{n-2}\cdots b_1b_0 = b_{n_2}2^{n-2} + b_{n-3}2^{n-3} + \cdots + b_12 + b_0$

- $b_{n-1} = 1$

	$$
	\begin{align*}
	1b_{n-2}\cdots b_1b_0 &= -2^{n-1} + b_{n_2}2^{n-2} + b_{n-3}2^{n-3} + \cdots + b_12 + b_0 \\
	                      &= -(2^{n-2} + 2^{n-3} + \cdots + 2 + 1 - 1) + b_{n_2}2^{n-2} + b_{n-3}2^{n-3} + \cdots + b_12 + b_0 \\
						  &= 2^{n-2}(b_{n-2}-1) + 2^{n-3}(b_{n-3}-1) + \cdots + 2(b_1-1) + 1(b_0-1) + 1
	\end{align*}
	$$

