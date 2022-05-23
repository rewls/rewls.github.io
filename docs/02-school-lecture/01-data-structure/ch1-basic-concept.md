---
layout: default
title: Ch1 Basic Concept
parent: Data Structure
grand_parent: School Lecture
nav_order: 1
mathjax: true
mermaid: true
permalink: /docs/data-structure/ch1
---

# Ch1 Basic Concept
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

<details open markdown="block">
  <summary>
    Toggle
  </summary>
- TOC
{:toc}
</details>

---

## 1.2 Pointers and Dynamic Memory Allocation

### 1.2.1 Pointers

- For any type T in C, there is **a corresponding type pointer-to-T**

- **The actual value** of point type

	- 해당 변수가 저장된 주소

- Two operators used with the Pointers

	- &: Address operator

	- *: Dereferencing(or indirection) operator

	```c
	int i, *pi;
	pi = &i;

	// To assign a value 10 to i
	i = 10;
	or
	*pi = 10;
	```

- Null pointer

	- Represented by the integer 0

	- Points to no object or function

	```c
	int *pi = 0;
	```

	```c
	if (pi == NULL) ...
	if (!pi) ...
	```

### 1.2.2 Dynamic Memory Allocation

- When is it required?

	1. 필요할 때 메모리를 할당했다가 필요하지 않으면 해제하여 메모리를 효율적으로 사용할 수 있다.

	2. 일반 변수나 함수의 경우 stack에 저장되는데 동적할당은 heap에 저장되어 별도로 관리된다.

- Allocating storage at run-time

	- called **heap** mechanism

	- Using a function, **malloc**

	```c
	// Program 1.1: Allocation and deallocation of memory
	int i, *pi;
	float f, *pf;
	pi = (int *)malloc(sizeof(int));
	pf = (float *)malloc(sizeof(float));
	*pi = 1024;
	*pf = 3.14;
	printf("an integer = %d, a float = %f\n", *pi, *pf);
	free(pi);
	free(pf);
	```

- More robust version for `malloc()`

	```c
	if ((pi=(int *)malloc(sizeof(int))) == NULL || (pf=(float *)malloc(sizeof(float))) == NULL) {
		fprintf(stderr, "Insufficient memory");
		exit(EXIT_FAILURE);
	}
	```

	or by the equivalent code

	```c
	if (!(pi=malloc(sizeof(int))) || !(pf=malloc(sizeof(float)))) {
		fprintf(stderr, "Insufficient memory");
		exit(EXIT_FAILURE);
	}
	```

- A macro definition for `malloc()`

	```c
	#define MALLOC(p, s) \
		if (!((p)=malloc(s))) { \
			fprintf(stderr, "Insufficient memory"); \
			exit(EXIT_FAILURE); \
		}
	```

	```c
	MALLOC(pi, sizeof(int));
	MALLOC(pf, sizeof(float));
	```

- Dangling reference

	```c
	int i, *pi;
	float f, *pf;
	pi = (int *)malloc(sizeof(int));
	pf = (float *)malloc(sizeof(float));
	*pi = 1024;
	*pf = 3.14;
	printf("an integer = %d, a float = %f\n", *pi, *pf);

	pf = (float *)malloc(sizeof(float));
	...

### 1.2.3 Pointers Can Be Dangerous

- Why?

	- 사용하면 안 되는 공간을 가리킬 수 있기 때문에 오작동 가능성이 높다.

- Set all pointers to NULL

	- When they are not actually point ingto an object

- Explicit type cast

	- when converting between pointer types

```c
pi = malloc(sizeof(int));
pf = (float *)pi;
```

---

## 1.3 Algorithm Specification

### 1.3.1 Introduction

- **Algofithm** is a finite set of instructions that accomplishes a particular task

- All algorithms must satisfy the following criteria:

	1. **Input**. There are zero or more quantities that are externally supplied.

	2. **Output**. At least one quantity is produced.

	3. **Definiteness**. Each instruction is clear and unambiguous.

	4. **Finiteness**. If we trace out the instructions of an algorithm, then for all cases, the algorithm terminates after a finite number of steps.

	5. **Effectiveness**. Every instruction must be basic enough to be carried out in principle. It is not enough that each that each operation be definite as in (3); it also must be feasible.

- How to describe an algorithm?

	- Use a **natural language** like English

	- Use graphic representations called **flowcharts**

	- Here, we use Mostly in C

		- Occasionally in a combination of English and C

- How to translating a problem into an algorithm?

	- Ex 1.1, Ex 1.2

##### Ex 1.1

- Devise a program that sorts a set of $n \ge 1$ integers

- A simple soluthon **selection sort**

	- **Find the smallest** from those integers that are currently unsorted

	- Place it next in the sorted list

	```c
	// Program 1.2: Selection sort algorithm
	for (i=0;i<n;i++) {
		Examine list[i] to list[n-1] and suppose that the smallest integer is at list[min];

		Interchange list[i] and list[min];
	}
	```

- Two subtasks for a real C program

	- Find the smallest integer in `list`

	- Interchange `list[i]` and `list[min]`

- Interchanging `list[i]` and `list[min]`

	```c
	// Program 1.3: Swap function
	void swap(int *x, int *y) {
	// both parameters are pointers to ints
		int temp = *x;  // declares temp as an int and assigns to it the contents of what x points to
		*x = *y;  // stores what y points to into the location where x points
		*y = temp;  // places the contents of temp in location pointed to by y
	}
	```

	```c
	#define SWAP(x, y, t) ((t)=(x), (x)=(y), (y)=(t))
	```

	- Using the function, suppose `a` and `b` are declared as `int`s

	- The macro works with any data type

```c
// Program 1.4: Selection sort
#define MAX_SIZE 101
#define SWAP(x, y, t) ((t)=(x), (x)=(y), (y)=(t))

void sort(int [], int);  // selection sort

int main() {
	int i, n;
	int list[MAX_SIZE];
	printf("Enter the number of numbers to generate: ");
	scanf("%d", &n);
	if (n<1 || n>MAX_SIZE) {
		fprintf(stderr, "Improper value of n\n");
		exit(EXIT_FAILURE);
	}
	for (i=0;i<n;i++) {
		list[i] = rand() % 1000;
		printf("%d ", list[i]);
	}
	sort(list, n);
	printf("\nSorted array:\n");
	for (i=0;i<n;i++)
		printf("%d ", list[i]);
	printf("\n");

	return 0;
}

void sort(int list[], int n) {
	int i, j, min, temp;
	for (i=0;i<n-1;i++) {
		min = i;
		for (j=i+1;j<n;j++)
			if (list[j] < list[min])
				min = j;
		SWAP(list[i], list[min], temp);
	}
}
```

> #define SQUARE(x) (x*x)
> vs
> #define SQUARE(x) ((x)*(x))

##### Ex 1.2

- Assume that we have $n$ distinct  **integers** that are already **sorted** and stored in the array list.

- Figure out if an integer searchnum is in list

	- If it is in list, return its index

	- If it is not present, return -1

- A Solution: **Binary Search**

	- Compare `list[middle]` with `searchnum`

		1. searchnum < list[middle]:

			right = middle-1

		2. serchnum = list[middle]:

			return middle

		3. searchnum > list[middle]:

			left = middle+1

	```c
	// Program 1.5: Searching a sorted list
	while (there are more integers to check) {
		middle = (left+right)/2;
		if (searchnum < list[midlle])
			right = middle-1;
		else if (searchnum == list[middle])
			return middle;
		else
			left = middle+1;
	}
	```

- Algorithm contains two **subtasks**

	- determining if there are any integers left to check

	- comparing `searchnum` to `list[middle]`

- comparing `searchnum` to `list[middle]`

```c
// Program 1.6: Comparison of two integers
int compare(int x, int y) {
// compare x and y, return -1 for less than, 0 for equal, 1 for greater
	if (x < y)
		return -1;
	else if (x == y)
		return 0;
	else
		return 1;
}
```

```c
#define COMPARE(x, y) (((x) < (y)) ? -1 : ((x)==(y)))?0:1)
```

- The macro works with any data type

```c
// Program 1.7: Searching an ordered list
int binsearch(int list[], int searchnum, int left, int right) {
	int middle;
	while (left <= right) {
		middle = (left+right)/2;
		switch (COMPARE(list[middle], searchnum)) {
			case -1:
				left = middle+1;
				break;
			case 0:
				return middle;
			case 1:
				right = middle-1;
		}
	}
	return -1;
}
```

- Ex) Search for the value 37

	|index|0|1|2|3|4|5|6|7|8|
	|-|-|-|-|-|-|-|-|-|-|
	|value|20|35|37|40|45|50|51|55|67|

	|order|1|2|3|
	|-|-|-|-|-|
	|left|0|0|2|
	|right|8|3|3|
	|middle|4|1|2|

- Ex) Search for the value 41

	|index|0|1|2|3|4|5|6|7|8|
	|-|-|-|-|-|-|-|-|-|-|
	|value|20|35|37|40|45|50|51|55|67|

	|order|1|2|3|4|5|
	|-|-|-|-|-|-|
	|left|0|0|2|3|4|
	|right|8|3|3|3|3|
	|middle|4|1|2|3| |

### 1.3.2 Recursive Algorithms

```c
// Program 1.8: Recursive implementation of binary search
int binsearch(int list[], int searchnum, int left, int right) {
	int middle;
	if (left <= right) {
		middle = (left+right)/2;
		switch(COMPARE(list[middle], searchnum)) {
			case -1:
				return binsearch(list, searchnum, middle+1, right);
			case 0:
				return middle;
			case 1:
				return binsearch(list, searchnum, left, middle-1);
		}
	}
	return -1;
}
```

---

## 1.4 Data Abstraction

### Data type

- Kinds of data type

	- Basic data types in C: **char, int, float, double**

		- Modifier keywords: short, long, unsigned

	- For grouping data: **array, structure**

		```c
		int list[5];
		struct student {
			char lastName;
			int studentId;
			char grade;
		};
		```

	- **Pointer** data types: **int \*, ...**

	- **User-defined** data types: **typedef ...**

- **Definition**: A **data type** is a collection of objects and a set of operations that act on those objects.

- Ex) data type int in C

	- Objects

		- {0, +1, -1, ..., INT_MAX, INT_MIN}

		- Representation: 2 bytes or 4 bytes of memory

	- Operations

		- Arithmetic operators {+, -, *, /, %}

		- Testing for equality/inequality

		- Operation that assigns an integer to a variable

### Abstract Data Type (ADT)

- **Definition**: An abstract Data Type (ADT) is a data type that is organized in such a way that the specification of the objects and the specification of the operations on the objects **is separated from** the representation of the objects and the implementation of the operations.

- ADT is **implementation-independent**

- Typically, an **ADT definition** will include at least one **function** from each of these three categories:

	- Creeator/constructor: These functions creaete a new instance of the designated type.

	- Transformers: These functions also create an instance of the designated type, generally by using one or more other nistances.

	- Observers/reporters: These functions provide information about an instance of the type, but they do not change the instance.

	![adt-naturalnumber](./img/adt-naturalnumber.png)

---

## 1.5 Performance Analysis

- Criterias:

	- Does the program meet the original specifications of the task?

	- Does it work correctly?

	- ...

	- Does the program efficiently  use primary and secondary **storage**?

	- Is the program's **running time** acceptable for the task?

##### Performance Evaluation

- Performance Analysis

	- Focuses on obtaining **estimates of time and space** that are **machine independent**

	- Known as complexity theory

- Performance Measurement

	- Machine dependent running times

##### Complexity: Space and Time

- Space complexity

	- The amount of **memory** that a program needs to run to completion

- Time complexity

	- The amount of **computation time** that a program needs to run to completion

### 1.5.1 Space Complexity

- The space needed by a program:

	1. Fixed Space Requirements (c)

		- <u>Independent on the number and size of the program's inputs and outputs</u>

		- Space for instruction(code), simple variables, fixed-size structured variables, and constants

	2. Variable Space Requirements ($S_p(I)$)

		- <u>Depends on the characteristics of particular instance $I$</u>

		- The number, size and values of the inputs and outputs

		- Space required when a function uses recursion

- Total space requiement $S(P)$ of any program:

	$S(P) = c + S_P(I)$

- Usually concerned with only the **variable space requirements**

	- When we want to compare the space complexity of several programs

- Ex 1.6 $S_{abc}(I)$?

	```c
	// Program 1.10: Simple arithmetic function
	float abc(float a float b, float c) {
		return a + b + b * c + (a + b = c) / (a + b) + 4.00;
	}
	```

	- This function has only fixed space requirements

	- $S_{abc}(I) = 0$

- Ex 1.7 $S_{sum}(I)$?

	```c
	// Program 1.11: Iterative function for summing a list of numbers
	float sum(float list[], int n) {
		float tempsum =0;
		int i;
		for (i=0;i<n;i++)
			tempsum += list[i];
		trturn tempsum;
	}
	```

	- Passcal may pass arrays by value. This means that the entire array is copied into temporary storage before the function is executed. In these languages the **variable space requirement** for this program is $S_{sum}(I) = S_{sum}(n) = n$, where $n$ is the sizeof the array

	- C passes all parameters by value. When an array is passed as an argument to a function, C interprets it as passing the address of the first element of the array. C does not copy the array. Therefore $S_{sum}(n)=0$

- Ex 1.8 $S_{rsum}(I)$?

	```c
	// Program 1.12: Recursive function for summing a list of numbers
	float rsum(float list[], int n) {
		if (n)
			return rsum(list, n-1) + list[n-1];
		return 0;
	}
	```

	- For each recursive call, compiler must save **the parameters, local variables, the return address** for each recursive call

	- If the array has $n = MAX\_SIZE$ numbers, the total variable space needed for the recursive version is $S_{rsum}(MAX\_SIZE) = (sizeof(float) + sizeof(int))*MAX_SIZE$

	|Type|Name|Number of bytes|
	|-|-|-|
	|parameter: float|list[]|4|
	|parameter: integer|n|4|
	|return address: (used internally)| |4(unless a far address)|
	|TOTAL per recursive call| |12|

- The iterative version  has no **variable space requirement**. The recursive version has a far greater overhead than its iterative counterpart.

### 1.5.2 Time Complexity

- Time $T(P)$ taken by a program $P$: $T(P) = C + T_P(I)$

	- $C$: compile time

	- $T_P(I)$: run (or eexecution) time

- Compile time

	- Fixed

	- Independent of instance characteristics

- Determining $T_P$ is not an easy task

	- It requires a detailed knowledge of the compiler's attributes

- Ex)

	- Suppose we have a simple program that adds and subtracts numbers:

	- $T_P(n) = c_aADD(n) + c_sSUB(n) + c_lLDA(n) + c_{st}STA(n)$

		- $n$: instance characteristic

		- $c_a, c_s, c_l, c_{st}$: constants(time needed to perform each operation)

		- $ADD, SUB, LDA, STA$ are the number of additions, subtractions, loads, and stores that are performed when the program is run with instance characteristic $n$

- Alternative:

	- Count **#(The number) of operations** the program performs

	- Machine-independent estimate

	- But we must know how to divide the program into distinct steps

- **Definition**: A **program step** is a syntactically or semantically meaningful program segment whose execution time is independent of the instance characteristics.

- Ex)

	- Each executable statement is counted as one step:

	```c
	a = 2;  // 1 step
	a = a+b+b*c+(a+b-c)/(a+b)+4.0  // 1 step
	```

- How to count program steps?

	1. Using a global **variable**, `count`

	2. Using a **tabular** method

1. Using a global **variable**, `count`

	```c
	// Program 1.13: Program 1.11 with count statements
	float sum(float list[], int n) {
		float tempsum = 0; count++;  // for assignment
		int i;
		for (i=0;i<n;i++) {
			count++;  // for the for loop
			tempsum += list[i]; count++;  // for assignment
		}
		count++;  // last execution of for
		count++;  // for return
		return tempsum;
	}
	```

	```c
	// Program 1.15: Program 1.12 with count statements added
	float rsum(float list[], int n) {
		count++;  // for if conditional
		if (n) {
			count++;  // for return and rsum invocation
			return rsum(list, n-1) + list[n-1];
		}
		count++;
		return 0;
	}
	```

2. Using a **tabular** method

|Statement|steps/execution|Frequency|Total steps|
|-|-|-|-|
|float sum(float list[], int n) {|0|0|0|
|float tempsum = 0;|1|1|1|
|int i;|0|0|0|
|for (i=0;i<n;i++)|1|n+1|n+1|
|tempsum += list[i];|1|1|n|
|}|0|0|0|
|Total| | |2n+3|

|Statement|steps/execution|Frequency|Total steps|
|-|-|-|-|
|float rsum(float list[], int n) {|0|0|0|
|if (n)|1|n+1|n+1|
|return rsum(list, n-1) + list[n-1];|n|n|n|
|return 0;|1|1|1|
|}|0|0|0|
|Total| | |2n+2|

$2n+3(iterative) > 2n+2(recursive)$

|Statement|steps/execution|Frequency|Total steps|
|-|-|-|-|
|void add(int a[][MAX_SIZE] ...) {|0|0|0|
|int i, j;|0|0|0|
|for (i=0;i<rows;i++)|1|rows+1|rows+1|
|for (i=0;j<cols;j++)|1|rows*(cols+1)|rows*cols+rows|
|c[i][j] = a[i][j]+b[i][j];|1|rows*cols|rows*cols|
|Total| | |2rows*cols+2rows+1|

### 1.5.3 Asymptotic Notation($\text{O}, \Omega, \Theta$)

- Motivation to determine step counts:

	- To compare the time complexities of two programs for the same function

	- To predict the growth in run time **as the instance characteristics change**

- Determining the exact step count is exceedingly difficult task for most of the programs

	- The notion of a step is itself inexact

	- Not very useful for comparative purposes

- **Asymptotic complexity**

	- Provides meaningful(but inexact) statements about the time and space complexities of a program

	- Determined quite easily without determining the exact step count

- Notations: $\text{O}, \Omega, \Theta$

	- $\text{O}$(Big "oh"): Upper bound

	- $\Omega$(Omega): Lower bound

	- $\Theta$(Theta): Upper and lower bound

- **Definition**: [Big "oh"] $f(n) = O(g(n))$

	- iff there exist positive constants $c$ and $n_0$ such that $f(n) \le cg(n)$ for all $n$, $n \ge n_0$

	- $\forall n, n \ge n_0$, $g(n)$ is an **upper bound** on the value of $f(n)$

- Ex 1.15

	- $3n+2 \le 4n~\forall n \ge 2$, $3n+2=O(n)$

	- $3n+3 \le 4n~\forall n \ge 3$, $3n+3=O(n)$

	- $100n+6 \le 101n~\forall n \ge 10$, $100n+6=O(n)$

	- $10n^2+4n+2 \le 11n^2~\forall n \ge 5$, $10n^2+4n+2=O(n^2)$

	- $6\cdot 2^n+n^2 \le 7 \cdot 2^n~\forall n \ge 4$, $6\cdot 2_n + n^2 = O(2^n)$

- $O(1)$

	- means a computing time is a constant

- $O(1) < O(\log n) < O(n\log n) < O(n^2) < O(n^3) < O(2^n)$

- **Theorem** 1.2:

	- if $f(n) = a_mn^m + \cdot + a_1n + a_0$,

	- then $f(n) = O(n^m)$

- **Definition** [Omega] $f(n) = \Omega(g(n))$

	- iff $\exist c, n_0 > 0, s.t.(subject~to) f(n) \ge cg(n)~\forall n, n \ge n_0$

	- $\forall n, n \ge n_0$, $g(n)$ is a **lower bound** on the value of $f(n)$

- Ex 1.16)

	- $n \ge 1$, $3n +2 \ge 3n$, $\Rightarrow 3n + 2 = \Omega(n)$

	- $n \ge 1$, $3n +2 \ge 100n$, $\Rightarrow 100n + 6 = \Omega(n)$

	- $n \ge 1$, $10n^2 + 4n +2 \ge n^2$, $\Rightarrow 10n^2 + 4n + 2 = \Omega(n^2)$

- **Definition**: [Theta] $f(n) = \Theta(g(n))$

	- iff $\exist c_1, c_2, n_0 > 0, s.t. c_1g(n) \le f(n) \le c_2g(n)~\forall n, n\ge n_0$

	- $g(n)$: both an upper and lower bound on the value of $f(n)$

- Ex 1.17)

	- $n \ge 2, 3n \le 3n+2 \le 4n$, $3n+2 = \Theta(n)$

	- $10n^2 + 4n + 2 = \Theta(n^2)$

	- $6 \cdot 2^n+n^2=\Theta(2^n)$

- **Theorem** 1.3:

	- if $f(n) = a_mn^m + \cdot + a_1n + a_0$ and $a_m > 0$, then $f(n) = \Omega(n^m)$


- **Theorem** 1.4:

	- if $f(n) = a_mn^m + \cdot + a_1n + a_0$ and $a_m > 0$, then $f(n) = \Theta(n^m)$

- Ex 1.18 [Complexity of matrix addition]:

	|Statement|Asymptotic complexity|
	|-|-|
	|void add(int a[][MAX_SIZE] ...) {|0|
	|int i, j;|0|
	|for (i=0;i<rows;i++)|Theta(rows)|
	|for (j=0;j<cols;j++)|Theta(rows.cols)
	|c[i][j] = a[i][j] + b[i][j];|Theta(rows.cols)|
	|}|0|
	|Total|Theta(rows.cols)|

### 1.5.4 Practical Complexities

---

## 1.6 Performance Measurement

### 1.6.1 Clocking

- Timing events in C

	- Use `clock()` or `time()` function in the C standard library.

	- `#include <time.h>`

| |Method 1|Method 2|
|-|-|-|
|Start timing|start = clock();|start=time(NULL);
|Stop timning|stop = clock();|stop=time(NULL);|
|Type returned|clock_t|time_t|
|Result in seconds|duration = ((double)(stop-start)) / CLOCKS_PER_SEC;|duration = (double)difftime(stop, start);|

- Ex 1.22 [Worst-case perfomance of selection sort]:

```c
// Program 1.24: First timing program for selection sort
#include <stdio.h>
#include <time.h>
#include "data-structure.h"
#define MAX_SIZE 1001

int main() {
	int i, n, step = 10;
	int a[MAX_SIZE];
	double duration;
	clock_t start;

	// times for n= 0, 10, ..., 100, 200, ..., 1000
	printf("     n time\n");
	for (n=0;n<=1000;n+=step) {
	// get time for size n
		// initialize with worst-case data
		for (i=0;i<n;i++)
			a[i] = n-i;

		start = clock();
		sort(a, n);
		duration = ((double) (clock() - start)) / CLOCKS_PER_SEC;

		printf("%6d %f\n", n, duration);
		if (n == 100)
			step = 100;
	}
}
```

```c
// Program 1.25: More accurate timing program for selection sort
int main() {
	int i, n, step = 10;
	int a[MAX_SIZE];
	double duration;

	// times for n = 0, 10, ..., 100, 200, ..., 1000
	printf("     n repetitions time\n");
	for (n=0;n<=1000;n+=step) {
		// get time for size n
		long  repetitions = 0;
		clock_t start = clock();
		do {
			repetitions++;

			// initialize with worst-case data
			for (i=0;i<n;i++)
				a[i] = n-i;
			sort(a, n);
		} while(clock()-start < 1000);
		// repeat until enough time has elapsed

		duration = ((double)(clock() - start))/CLOCKS_PER_SEC;
		duration /= repetitions;
		printf("%6d %9d %f\n", n, repetitions, duration);
		if (n == 100)
			step = 100;
	}
}
```
