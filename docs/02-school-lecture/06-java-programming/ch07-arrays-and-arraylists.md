---
layout: default
title: Ch7 Arrays and ArrayLists
parent: Java Programming
grand_parent: School Lecture
nav_order: 7
mathjax: true
mermaid: true
permalink: /docs/java/ch7
---

# Ch7 Arrays and ArrayLists
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

- Learn what arrays are

- Use arrays to store data in and retrieve data from lists and tables of values

- Declare arrays, initialize arrays and refer to individual elements of arrays

- Iterate through arrays with the enhanced `for` statement

- Pass arrays to methods

- Declare and manipulate multidimensional arrays

- Use variable-length argument lists

- Read command-line arguments into a program

- Build an object-oriented instructor gradebook class

- Perform common array mainpulatoins with the methods of class `Arrays`

- Use class `ArrayList` to manipulate a dynamically resizable array-like data structure

---

## 7.2 Arrays

- Arrays are objects, so they are reference types

- Elements can be either primitive or reference types

> Common Programming Error 7.1
>
> An index must be an `int` value or a value of a type that can be promoted to `int` - namely, `byte`, `short` or `char` but not `long`: otherwise, a compilation error occurs

---

## 7.3 Declaring and Creating Arrays

- Declaration and creation for an array of 12 `int` elements

	`int[] c = new int[12];`

	```java
	int[] c;
	c =  new int[12];
	```

	- Array variable stores the array reference

	- Array-creation expression returns a reference

- When an array is created, each element of the array receives a default value

	- Zero for the numeric primitive-type elements

	- `false` for `boolean` elements

	- `null` for references

- Declaring multiple array variables in a single declaration

	`int[] a, b, c;`

	- cf) `int a[], b, c;  // ?`

- Every element of an `in` array is an `int` value

- Every element of a `String` array is a reference to a `String` object

---

## 7.4 Examples Using Arrays

```java
// Fig. 7.2: InitArray.java
// Initializing the elements of an array to default values of zero

public class InitArray {
	public static void main(String[] argc) {
		// declare variable array and initialize it with an array object
		int[] array = new int[10];  // create the array object

		System.out.printf("%s%8s%n", "Index", "Value");  // column headings

		// output each array element's value
		for (int counter = 0; counter < array.length; counter++)
			System.out.printf("%5d%8d%n", counter, array[counter]);
	}
}
```

```
Index   Value
    0       0
    1       0
    2       0
    3       0
    4       0
    5       0
    6       0
    7       0
    8       0
    9       0
```

### Array initializer (or initializer list)

`int[] n = {10, 20, 30, 40, 50};`

### Compiler

- counts the number of initializers in the list to determine the size of the array

- sets up the appropriate `new` operation "behind the scenes"

```java
// Fig. 7.3: InitArray.java
// Initializing the elements of an array with an array initializer

public class InitArray {
	public static void main(String[] args) {
		// initializer list specifies the initializer value for each element
		int[] array = {32, 27, 64, 18, 95, 14, 90, 70, 60, 37};

		System.out.printf("%s%8s%n", "Index", "Value";);  // column headings

		// output each array element's value
		for (int counter = 0; counter < array.length; counter++)
			System.out.printf("%5d%8d%n", counter, array[counter]);
	}
}
```

```
Index   Value
    0      32
    1      27
    2      64
    3      18
    4      95
    5      14
    6      90
    7      70
    8      60
    9      37
```

```java
// Fig. 7.4: InitArray.java
// Calculating the values to be placed into the elementof an array

public class InitArray {
	public static void main(String[] args) {
		final int ARRAY_LENGTH = 10;  // declare constant
		int[] array = new int[ARRAY_LENGTH];  // create array

		// calculate value for each array element
		for (int counter = 0; counter < array.length; counter++)
			array[counter] = 2 + 2 * counter;

		System.out.printf("%s%8s%n", "Index", "Value"); // column headings

		// output each array element's value
		// output each array element's value
		for (int counter = 0; counter < array.length; counter++)
			System.out.printf("%5d%8d%n", counter, array[counter]);
	}
}
```

```
Index   Value
    0       2
    1       4
    2       6
    3       8
    4      10
    5      12
    6      14
    7      16
    8      18
    9      20
```

- `final` variables must be initialized before they are used and cannot be modified thereafter

- An attempt to modify ad `final` variable after it's initialized causes a compilation error

- An attempt to access the value of a `final` variable before it's initialized cause a compilation error

```java
// Fig. 7.5: SumArray.java
// Computing the sum of the elements of an array

public class SumArray {
	public static void main(String[] args) {
		int[] array = {87, 68, 94, 100, 83, 78, 85, 91, 76, 87};
		int total = 0;

		// add each element's value to total
		for (int counter =0; counter < array.length; counter++)
			total += array[counter];

		System.out.printf("Total of array elements: %d%n", total);
	}
}
```

```
Total of array elements: 849
```

```java
// Fig. 7.7: RollDie.java
// Die-rolling program using arrays instead of switch

import java.security.SecureRandom;

public class RollDie {
	public static void main(String[] args) {
		SecureRandom randomNumbers = new SecureRandom();
		int[] frequency = new int[7];  // array of frequency counters

		// roll die 60,000,000 times: use die value as frequency index
		for (int roll = 1; roll <= 60000000; roll++)
			++frequency[1 + randomNumbers.nextInt(6)];  // Ignore frequency[0]

		System.out.printf("%s%10s%n", "Face", "Frequency");

		// output each array element's value
		for (int face = 1; face < frequency.length; face++)
			System.out.printf("%4d%10d%n", face, frequency[face]);
	}
}
```

```
Face Frequency
   1  10000245
   2   9999176
   3   9996962
   4  10004893
   5  10000380
   6   9998344
```

- Figure 7.8 uses arrays to summarize data collected in a survey
	- 20 students were asked to rate on a scale of 1 to 5 the quality of the food in the student cafeteria, with 1 being "awful" and 5 being "excellent. Place the 20 responses in an integer array and determine the frequency of each rating

```java
// Fig. 7.8: StudentPoll.java
// Poll analysis program
 public class StudentPoll {
	public static void main(String[] args) {
		// student response array (more typically, input at runtime)
		int[] responses = {1, 2, 5, 4, 3, 5, 2, 1, 3, 3, 1, 4, 3, 3, 3, 2, 3, 3, 2, 14};  // 14: incorrect value
		int[] frequency = new int[6]; // array of frequency couners. Each element is initialized to zero by defualt

		// for each answer, select responses element and use that value as frequency index to determine element to increment
		for (int answer = 0; answer < responses.length; answer++) {
			try {
				++frequency[responses[answer]];  // Ignore frequency[0]. responses[answer] correct values: 1~5
			} catch (ArrayIndexOutOfBoundsException e) {
				System.out.println(e);  // a invokes toString method
				System.out.printf("    responses[%d] = %d%n%n", answer, responses[answer]);
			}
		}

		System.out.printf("%s%10s%n", "Rating", "Frequency");

		for (int rating = 1; rating < frequency.length; rating++)
			System.out.printf("%6d%10d%n", rating, frequency[rating]);
	}
}
```

```
java.lang.ArrayIndexOutOfBoundsException: Index 14 out of bounds for length 6
    responses[19] = 14

Rating Frequency
     1         3
     2         4
     3         8
     4         2
     5         2
```

## 7.5 Exception Handling: Processing the Incorrect Response

### `++frequency[responses[answer]]`

- `++frequency[14]`

	- 14 is an invalid index for the array `frequency`

- JVM checks array indices at execution time

	- bound checking

- If a program uses an invalid index, JVM generate(`throws`) an exception object

	- `ArrayIndexOutOfBoundsException`

### Exception

- Indication of a problem that occurs while a program execute

### Exception handling

- The programs can continue executing (rather than terminating) after dealing with a problem

### `try` block

- code that might `throw` an exception

- code that should not execute if an exception occurs

### `catch` block (`catch` clause or exception handler)

- code that handles the exception

- The exception parameter identifies the exception type the handler can process

### `toString` method of the exception parameter

```java
try {
	++frequency[responses[answer]];  // Ignore frequency[0]. responses[answer] correct values: 1~5
} catch (ArrayIndexOutOfBoundsException e) {
	System.out.println(e);  //a invokes toString method
	System.out.printf("    responses[%d] = %d%n%n", answer, responses[answer]);
}
```

- Implicitly calls the exception object's `toString` method to get the error message that's implicitly stored in the exception object and display it

---

## 7.6 Case Study: Card Shuffling and Dealing Simulation

- Using an array of reference-type elements

### Class Card

- Method `toString`

	- can invoke explicitly to obtain a string representation of a `Card`

	- called implicitly when the `Card` object is used where a `String` is expected

		```java
		printf("%s", cardObject)
		```

```java
// Fig. 7.9: Card.java
// Card class represents a playing card

public class Card {
	private final String face;  // face of card ("Ace", "Duece", ...)
	private final String suit;  // suit of card ("Hearts", "Diamonds", ...)

	// two-argument constructor initializes card's face and suit
	public Card(String cardFace, String cardSuit) {
		this.face = cardFace;  // initialize face of card
		this.suit = cardSuit;  // initialize suit of card
	}

	// return String representation of Card
	public String toString() {
		return face + " of " + suit;
	}
}
```

```java
// Fig. 7.10: DeckOfCards.java
// DeckOfCards class represents a deck of playing cards.

import java.security.SecureRandom;

public class DeckOfCards {
	// random number generator
	private static final SecureRandom randomNumbers = new SecureRandom();
	private static final int NUMBER_OF_CARDS = 52;  // constant # of Cards

	private Card[] deck = new Card[NUMBER_OF_CARDS];  // Card references
	private int currentCard = 0;  // index fo next Card to be dealt (0-51)

	// constructor fills deck of Cards
	public DeckOfCards() {
		String[] faces = {"Ace", "Deuce", "Three", "Four", "Five", "Six", "Seven", "Eight", "Nine", "Ten", "Jack", "Queen", "King"};
		String[] suits = {"Hearts", "Diamonds", "Clubs", "Spades"};

		// populate deck with Card objects
		for (int count=0; count<deck.length; count++) {
			deck[count] = new Card(faces[count%13], suits[count/13]);
		}
	}

	// shuffle deck of Cards with one-pass algorithm
	public void shuffle() {
		// next call to method dealCard should start at deck[0] again
		currentCard = 0;

		// for each Card, pick another random Card (0-51) and swap tamp
		for (int first=0; first<deck.length; first++) {
			// select a random number between 0 and 51
			int second = randomNumbers.nextInt(NUMBER_OF_CARDS);

			// swap current Card with randomly selected Card
			Card temp = deck[first];
			deck[first] = deck[second];
			deck[second] = temp;
		}
	}

	public Card dealCard() {
		// determine whether Cards remain to be dealt
		if (currentCard < deck.length)
			return deck[currentCard++];  // return current Card in array
		else
			return null;  // return null to indicate that all Cards were dealt
	}
}
```

```java
// Fig. 7.11: DeckOfCardsTest.java
// Card shuffling and dealing

public class DeckOfCardsTest {
	// execute application
	public static void main(String[] args) {
		DeckOfCards myDeckOfCards = new DeckOfCards();
		myDeckOfCards.shuffle();  // place Cards in random order

		// print all 52 Cards in the order in which they are dealt
		for (int i=1; i<=52; i++) {
			// deal and display a Card
			System.out.printf("%-19s", myDeckOfCards.dealCard());  // Card's toString()

			if (i%4 == 0)  // output a newline after every fourth card
				System.out.println();
		}
	}
}
```

```
Ten of Spades      Jack of Diamonds   Six of Hearts      Nine of Spades
Three of Diamonds  Nine of Diamonds   Five of Spades     Four of Spades
Eight of Diamonds  Deuce of Hearts    Ten of Hearts      Deuce of Spades
King of Clubs      Ace of Clubs       King of Spades     Ten of Clubs
Five of Hearts     Seven of Spades    Six of Spades      Seven of Clubs
Three of Spades    Ace of Diamonds    Ace of Hearts      Five of Clubs
Deuce of Clubs     Four of Clubs      Three of Clubs     Jack of Clubs
Eight of Spades    Eight of Clubs     Deuce of Diamonds  Three of Hearts
Four of Hearts     Jack of Spades     Seven of Hearts    Five of Diamonds
Ace of Spades      Queen of Diamonds  Seven of Diamonds  Nine of Clubs
Queen of Spades    Ten of Diamonds    Queen of Hearts    King of Hearts
Six of Clubs       King of Diamonds   Four of Diamonds   Eight of Hearts
Queen of Clubs     Nine of Hearts     Six of Diamonds    Jack of Hearts
```

## 7.7 Enhanced `for` Statement

### Syntax:

```java
for (parameter:arrayName)
	statement;
```

- ex)

	```java
	for (int number:array)
		total += number;
	```

- `parameter` has a `type` and an `identifier`

	- the `type` must be consistent with the array's element type

	- the `identifier` represents successive values in the array

- `arrayName` is the array through which to iterate

```java
// Fig. 7.12: EnhancedForTest.java
// Using the enhanced for statement to total integers in an array.

public class EnhancedForTest {
	public static void main(String[] args) {
		int[] array = {87, 68, 94, 100, 83, 78, 85, 91, 76, 87};
		int total = 0;

		// add each element's value to total
		for (int number:array) {
			total += number;
		}

		System.out.printf("Total of array elements: %d%n", total);
	}
}
```

```
Total of array elements: 849
```

- The enhanced `for` statement can be used only to obtain array elements

	- it cannot be used to modify elements

	- To modify elements, use the traditional counter-controlled `for` statement

## 7.8 Passing Arrays to Methods

### Caller

```java
int[] array = {1, 2, 3, 4, 5};
modifyArray(array);
```

### Callee

```java
public static void modifyArray(int[] array) {
	for (int counter=0; counter<array.length; counter++)
		array[counter] *= 2;
}
```

```java
// Fig. 7.13: PassArray.java
// Passing arrays and individual array elements to methods

public class PassArray {
	// main creates array and calls modifyArray and modifyElement
	public static void main(String[] args) {
		int[] array = {1, 2, 3, 4, 5};

		System.out.printf("Effects of passing reference to entire array:%n" + "The values of the original array are %n");

		// output original array elements
		for (int value : array)
			System.out.printf("    %d", value);
		modifyArray(array);  // pass array reference
		System.out.printf("%n%nThe values of the modifies array are:%n");

		// output modified array elements
		for (int value : array)
			System.out.printf("    %d", value);

		System.out.printf("%n%nEffects of passing array elements value:%n" + "array[3] before modifyElement: %d%n", array[3]);

		modifyElement(array[3]);  // attempt to modify array[3]
		System.out.printf("array[3] after modifyElement: %d%n", array[3]);
	}

	// multiply each element of an array by 2
	public static void modifyArray(int[] array2) {
		for (int counter = 0; counter < array2.length; counter++)
			array2[counter] *= 2;
	}

	// multiply argument by 2
	public static void modifyElement(int element) {
		element *= 2;
		System.out.printf("Value of element in modifyElement: %d%n", element);
	}
}
```

```
Effects of passing reference to entire array:
The values of the original array are
    1    2    3    4    5

The values of the modifies array are:
    2    4    6    8    10

Effects of passing array elements value:
array[3] before modifyElement: 8
Value of element in modifyElement: 16
array[3] after modifyElement: 8
```

- In Java, all arguments are passed by value

- A method call can pass two types of values to a method

	- Copies of primitive values

	- Copiies of references to objects

- Objects cannot be passed to methods

## 7.10 Case Study: Class `GradeBook ` Using an Array to Store Greades

```java
// Fig. 7.14: GradeBook.java
// GradeBook class using an array to store test grades.

public class GradeBook {
   private String courseName; // name of course this GradeBook represents
   private int[] grades; // array of student grades

   // constructor
   public GradeBook(String courseName, int[] grades) {
      this.courseName = courseName;
      this.grades = grades;
   }

   // method to set the course name
   public void setCourseName(String courseName) {
      this.courseName = courseName;
   }

   // method to retrieve the course name
   public String getCourseName() {
      return courseName;
   }

   // perform various operations on the data
   public void processGrades() {
      // output grades array
      outputGrades();

      // call method getAverage to calculate the average grade
      System.out.printf("%nClass average is %.2f%n", getAverage());

      // call methods getMinimum and getMaximum
      System.out.printf("Lowest grade is %d%nHighest grade is %d%n%n",
         getMinimum(), getMaximum());

      // call outputBarChart to print grade distribution chart
      outputBarChart();
   }

   // find minimum grade
   public int getMinimum() {
      int lowGrade = grades[0]; // assume grades[0] is smallest

      // loop through grades array
      for (int grade : grades) {
         // if grade lower than lowGrade, assign it to lowGrade
         if (grade < lowGrade) {
            lowGrade = grade; // new lowest grade
         }
      }

      return lowGrade;
   }

   // find maximum grade
   public int getMaximum() {
      int highGrade = grades[0]; // assume grades[0] is largest

      // loop through grades array
      for (int grade : grades) {
         // if grade greater than highGrade, assign it to highGrade
         if (grade > highGrade) {
            highGrade = grade; // new highest grade
         }
      }

      return highGrade;
   }

   // determine average grade for test
   public double getAverage() {
      int total = 0;

      // sum grades for one student
      for (int grade : grades) {
         total += grade;
      }

      // return average of grades
      return (double) total / grades.length;
   }

   // output bar chart displaying grade distribution
   public void outputBarChart() {
      System.out.println("Grade distribution:");

      // stores frequency of grades in each range of 10 grades
      int[] frequency = new int[11];

      // for each grade, increment the appropriate frequency
      for (int grade : grades) {
         ++frequency[grade / 10];
      }

      // for each grade frequency, print bar in chart
      for (int count = 0; count < frequency.length; count++) {
         // output bar label ("00-09: ", ..., "90-99: ", "100: ")
         if (count == 10) {
            System.out.printf("%5d: ", 100);
         }
         else {
            System.out.printf("%02d-%02d: ", count * 10, count * 10 + 9);
         }

         // print bar of asterisks
         for (int stars = 0; stars < frequency[count]; stars++) {
            System.out.print("*");
         }

         System.out.println();
      }
   }

   // output the contents of the grades array
   public void outputGrades() {
      System.out.printf("The grades are:%n%n");

      // output each student's grade
      for (int student = 0; student < grades.length; student++) {
         System.out.printf("Student %2d: %3d%n",
            student + 1, grades[student]);
      }
   }
}
```

```java
// Fig. 7.15: GradeBookTest.java
// GradeBookTest creates a GradeBook object using an array of grades,
// then invokes method processGrades to analyze them.

public class GradeBookTest {
   public static void main(String[] args) {
      // array of student grades
      int[] gradesArray = {87, 68, 94, 100, 83, 78, 85, 91, 76, 87};

      GradeBook myGradeBook = new GradeBook(
         "CS101 Introduction to Java Programming", gradesArray);
      System.out.printf("Welcome to the grade book for%n%s%n%n",
         myGradeBook.getCourseName());
      myGradeBook.processGrades();
   }
}
```

```
Welcome to the grade book for
CS101 Introduction to Java Programming

The grades are:

Student  1:  87
Student  2:  68
Student  3:  94
Student  4: 100
Student  5:  83
Student  6:  78
Student  7:  85
Student  8:  91
Student  9:  76
Student 10:  87

Class average is 84.90
Lowest grade is 68
Highest grade is 100

Grade distribution:
00-09:
10-19:
20-29:
30-39:
40-49:
50-59:
60-69: *
70-79: **
80-89: ****
90-99: **
  100: *
```

---

## 7.11 Multidimensional Arrays

<center markdown="block">
![two-dimensional-array](/assets/java-programming/images/7-two-dimensional-array.png)

Two-dimensional array

![two-dimensional-array-structure](/assets/java-programming/images/7-two-dimensional-array-structure.png)

Two-dimensional array structure
</center>

### two-dimensional array with initializer

- `int[][] a = \{\{1, 2\}, \{3, 4\}\};`

- `int[][] b = \{\{1, 2\}, \{3, 4, 5\}\};`

### two-dimensional array with an array-creation expression

- `int[][] c = new int[3][4];`

```java
int[][] d = new int[2][];  // create 2 rows
d[0] = new int[5];  // create 5 columns for row 0
d[1] = new int[3];  // create 3 columns for row 1
```

```java
// Fig. 7.17: InitArray.java
// Initializing two-dimensional arrays

public class InitArray {
	// create and output two-dimensional arrays
	public static void main(String[] args) {
		int[][] array1 = \{\{1, 2, 3\}, \{4, 5, 6\}\};
		int[][] array2 = \{\{1, 2\}, \{3\}, \{4, 5, 6\}\};

		System.out.println("Values in array1 by row are");
		outputArray(array1);  // displays array1 by row

		System.out.printf("%nValues in array2 by row are%n");
		outputArray(array2);  // displays array2 by row
	}

	// output rows and columns of a two-dimensional array
	public static void outputArray(int[][] array) {
		// loop through array's rows
		for (int row=0; row<array.length; row++) {
			// loop through columns of current row
			for (int column=0; column<array[row].length; column++)
				System.out.printf("%d  ", array[row][column]);
			System.out.println();
		}
	}
}
```

```
Values in array1 by row are
1  2  3
4  5  6

Values in array2 by row are
1  2
3
4  5  6
```

## 7.12 Case Study: Class `GradeBook` Using a Two-Dimensional Array

```java
// Fig. 7.18: GradeBook.java
// GradeBook class using a two-dimensional array to store grades.

public class GradeBook {
   private String courseName; // name of course this grade book represents
   private int[][] grades; // two-dimensional array of student grades

   // two-argument constructor initializes courseName and grades array
   public GradeBook(String courseName, int[][] grades) {
      this.courseName = courseName;
      this.grades = grades;
   }

   // method to set the course name
   public void setCourseName(String courseName) {
      this.courseName = courseName;
   }

   // method to retrieve the course name
   public String getCourseName() {
      return courseName;
   }

   // perform various operations on the data
   public void processGrades() {
      // output grades array
      outputGrades();

      // call methods getMinimum and getMaximum
      System.out.printf("%n%s %d%n%s %d%n%n",
         "Lowest grade in the grade book is", getMinimum(),
         "Highest grade in the grade book is", getMaximum());

      // output grade distribution chart of all grades on all tests
      outputBarChart();
   }

   // find minimum grade
   public int getMinimum() {
      // assume first element of grades array is smallest
      int lowGrade = grades[0][0];

      // loop through rows of grades array
      for (int[] studentGrades : grades) {
         // loop through columns of current row
         for (int grade : studentGrades) {
            // if grade less than lowGrade, assign it to lowGrade
            if (grade < lowGrade) {
               lowGrade = grade;
            }
         }
      }

      return lowGrade;
   }

   // find maximum grade
   public int getMaximum() {
      // assume first element of grades array is largest
      int highGrade = grades[0][0];

      // loop through rows of grades array
      for (int[] studentGrades : grades) {
         // loop through columns of current row
         for (int grade : studentGrades) {
            // if grade greater than highGrade, assign it to highGrade
            if (grade > highGrade) {
               highGrade = grade;
            }
         }
      }

      return highGrade;
   }

   // determine average grade for particular set of grades
   public double getAverage(int[] setOfGrades) {
      int total = 0;

      // sum grades for one student
      for (int grade : setOfGrades) {
         total += grade;
      }

      // return average of grades
      return (double) total / setOfGrades.length;
   }

   // output bar chart displaying overall grade distribution
   public void outputBarChart() {
      System.out.println("Overall grade distribution:");

      // stores frequency of grades in each range of 10 grades
      int[] frequency = new int[11];

      // for each grade in GradeBook, increment the appropriate frequency
      for (int[] studentGrades : grades) {
         for (int grade : studentGrades) {
            ++frequency[grade / 10];
         }
      }

      // for each grade frequency, print bar in chart
      for (int count = 0; count < frequency.length; count++) {
         // output bar label ("00-09: ", ..., "90-99: ", "100: ")
         if (count == 10) {
            System.out.printf("%5d: ", 100);
         }
         else {
            System.out.printf("%02d-%02d: ",
               count * 10, count * 10 + 9);
         }

         // print bar of asterisks
         for (int stars = 0; stars < frequency[count]; stars++) {
            System.out.print("*");
         }

         System.out.println();
      }
   }

   // output the contents of the grades array
   public void outputGrades() {
      System.out.printf("The grades are:%n%n");
      System.out.print("            "); // align column heads

      // create a column heading for each of the tests
      for (int test = 0; test < grades[0].length; test++) {
         System.out.printf("Test %d  ", test + 1);
      }

      System.out.println("Average"); // student average column heading

      // create rows/columns of text representing array grades
      for (int student = 0; student < grades.length; student++) {
         System.out.printf("Student %2d", student + 1);

         for (int test : grades[student]) { // output student's grades
            System.out.printf("%8d", test);
         }

         // call method getAverage to calculate student's average grade;
         // pass row of grades as the argument to getAverage
         double average = getAverage(grades[student]);
         System.out.printf("%9.2f%n", average);
      }
   }
}
```

```java
// Fig. 7.19: GradeBookTest.java
// GradeBookTest creates GradeBook object using a two-dimensional array
// of grades, then invokes method processGrades to analyze them.
public class GradeBookTest {
   // main method begins program execution
   public static void main(String[] args) {
      // two-dimensional array of student grades
      int[][] gradesArray = \{\{87, 96, 70\},
                             \{68, 87, 90\},
                             \{94, 100, 90\},
                             \{100, 81, 82\},
                             \{83, 65, 85\},
                             \{78, 87, 65\},
                             \{85, 75, 83\},
                             \{91, 94, 100\},
                             \{76, 72, 84\},
                             \{87, 93, 73\}\};

      GradeBook myGradeBook = new GradeBook(
         "CS101 Introduction to Java Programming", gradesArray);
      System.out.printf("Welcome to the grade book for%n%s%n%n",
         myGradeBook.getCourseName());
      myGradeBook.processGrades();
   }
}
```

```
Welcome to the grade book for
CS101 Introduction to Java Programming

The grades are:

            Test 1  Test 2  Test 3  Average
Student  1      87      96      70    84.33
Student  2      68      87      90    81.67
Student  3      94     100      90    94.67
Student  4     100      81      82    87.67
Student  5      83      65      85    77.67
Student  6      78      87      65    76.67
Student  7      85      75      83    81.00
Student  8      91      94     100    95.00
Student  9      76      72      84    77.33
Student 10      87      93      73    84.33

Lowest grade in the grade book is 65
Highest grade in the grade book is 100

Overall grade distribution:
00-09:
10-19:
20-29:
30-39:
40-49:
50-59:
60-69: ***
70-79: ******
80-89: ***********
90-99: *******
  100: ***
```

---

## 7.13 Variable-Length Argument Lists

```java
public static double average(int num, double... number) {
}
```

- `average(3, d1, d2, d3);`

- `average(3, d1, d2, d3, d4);  // variable-length argument lists`

- The ellipsis can occur only onece at the end of a parameter list

```java
// Fig. 7.20: VarargsTest.java
// Using variable-length argument lists.

public class VarargsTest {
   // calculate average
   public static double average(double... numbers) {
      double total = 0.0;

      // calculate total using the enhanced for statement
	  // Variable arguments are automatically placed in an array referenced by the parameter
      for (double d : numbers) {
         total += d;
      }

      return total / numbers.length;
   }

   public static void main(String[] args) {
      double d1 = 10.0;
      double d2 = 20.0;
      double d3 = 30.0;
      double d4 = 40.0;

      System.out.printf("d1 = %.1f%nd2 = %.1f%nd3 = %.1f%nd4 = %.1f%n%n",
         d1, d2, d3, d4);

      System.out.printf("Average of d1 and d2 is %.1f%n",
         average(d1, d2));
      System.out.printf("Average of d1, d2 and d3 is %.1f%n",
         average(d1, d2, d3));
      System.out.printf("Average of d1, d2, d3 and d4 is %.1f%n",
         average(d1, d2, d3, d4));
   }
}
```

```
d1 = 10.0
d2 = 20.0
d3 = 30.0
d4 = 40.0

Average of d1 and d2 is 15.0
Average of d1, d2 and d3 is 20.0
Average of d1, d2, d3 and d4 is 25.0
```

## 7.14 Using Command-Line Arguments

```java
// Fig. 7.21: InitArray.java
// Initializing an array using command-line arguments.

public class InitArray {
   public static void main(String[] args) {
      // check number of command-line arguments
      if (args.length != 3) {
         System.out.printf(
            "Error: Please re-enter the entire command, including%n" +
            "an array size, initial value and increment.%n");
      }
      else {
         // get array size from first command-line argument
         int arrayLength = Integer.parseInt(args[0]);
         int[] array = new int[arrayLength];

         // get initial value and increment from command-line arguments
         int initialValue = Integer.parseInt(args[1]);
         int increment = Integer.parseInt(args[2]);

         // calculate value for each array element
         for (int counter = 0; counter < array.length; counter++) {
            array[counter] = initialValue + increment * counter;
         }

         System.out.printf("%s%8s%n", "Index", "Value");

         // display array index and value
         for (int counter = 0; counter < array.length; counter++) {
            System.out.printf("%5d%8d%n", counter, array[counter]);
         }
      }
   }
}
```

```
java InitArray
Error: Please re-enter the entire command, including
```

```
javat InitArray 5 0 4
Index   Value
    0       0
    1       4
    2       8
    3      12
    4      16
```

---

## 7.15 Class `Arrays`

### `Arrays` class

- provides `static` methods for common array manipulations

##### Methods include

- `sort` for sorting an array (ascending order by deault

- `binarySearch` for searching a sorted array

- `equals` for comparing arrays

- `fill` for placing values into an array

##### Methods are overloaded

- for primitive-type arrays and for arrays of objects

### `System` class

- `static` `arraycopy` method

	- Copies contents of one array into another

```java
// Fig. 7.22: ArrayManipulations.java
// Arrays class methods and System.arraycopy.
import java.util.Arrays;

public class ArrayManipulations {
   public static void main(String[] args) {
      // sort doubleArray into ascending order
      double[] doubleArray = {8.4, 9.3, 0.2, 7.9, 3.4};
      Arrays.sort(doubleArray);
      System.out.printf("%ndoubleArray: ");

      for (double value : doubleArray) {
         System.out.printf("%.1f ", value);
      }

      // fill 10-element array with 7s
      int[] filledIntArray = new int[10];
      Arrays.fill(filledIntArray, 7);
      displayArray(filledIntArray, "filledIntArray");

      // copy array intArray into array intArrayCopy
      int[] intArray = {1, 2, 3, 4, 5, 6};
      int[] intArrayCopy = new int[intArray.length];
      System.arraycopy(intArray, 0, intArrayCopy, 0, intArray.length);
      displayArray(intArray, "intArray");
      displayArray(intArrayCopy, "intArrayCopy");

      // compare intArray and intArrayCopy for equality
      boolean b = Arrays.equals(intArray, intArrayCopy);
      System.out.printf("%n%nintArray %s intArrayCopy%n",
         (b ? "==" : "!="));

      // compare intArray and filledIntArray for equality
      b = Arrays.equals(intArray, filledIntArray);
      System.out.printf("intArray %s filledIntArray%n",
         (b ? "==" : "!="));

      // search intArray for the value 5
      int location = Arrays.binarySearch(intArray, 5);

      if (location >= 0) {
         System.out.printf(
            "Found 5 at element %d in intArray%n", location);
      }
      else {
         System.out.println("5 not found in intArray");
      }

      // search intArray for the value 8763
      location = Arrays.binarySearch(intArray, 8763);

      if (location >= 0) {
         System.out.printf(
            "Found 8763 at element %d in intArray%n", location);
      }
      else {
         System.out.println("8763 not found in intArray");
      }
   }

   // output values in each array
   public static void displayArray(int[] array, String description) {
      System.out.printf("%n%s: ", description);

      for (int value : array) {
         System.out.printf("%d ", value);
      }
   }
}
```

```
doubleArray: 0.2 3.4 7.9 8.4 9.3
filledIntArray: 7 7 7 7 7 7 7 7 7 7
intArray: 1 2 3 4 5 6
intArrayCopy: 1 2 3 4 5 6

intArray == intArrayCopy
intArray != filledIntArray
Found 5 at element 4 in intArray
8763 not found in intArray
```

## 7.16 Introduction to Collections and Class `ArrayList`

### Collections

- Predefined data structures provided by Java API

- Collection indices start at zero

### `ArrayList<T>` (package `java.util`)

- can dynamically change its size to accommodate more elements

- `T` is a placeholder for the type of element stored in the collection

	- This kind of classes are generic classes

- only non-primitive types can be used with these collections classes

- A new empty `ArrayList` of `String`

	- with a default initial capacity of 10 elements

	`ArrayList<String> items = new ArrayList<String>();`

	or

	```java
	ArrayList<String> items = new ArrayList<>();
	// diamond(<>) notation in Java SE7 and higher
	```

<table>
	<caption><span markdown=1>Some methods of class `ArrayList<E>`</span></caption>
	<thead>
		<tr>
			<th>Method</th>
			<th>Decription</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td><span markdown=1>`add`</span></td>
			<td><span markdown=1>Overloaded to add an element to the end of the `ArrayList` or at a specific index in the `ArrayList`</span></td>
		</tr>
		<tr>
			<td><span markdown=1>`clear`</span></td>
			<td><span markdown=1>Removes all the elements from the `ArrayList`</span></td>
		</tr>
		<tr>
			<td><span markdown=1>`contains`</span></td>
			<td><span markdown=1>Returns `true` if the `ArrayList` contains the specified element; otherwise return `false`</span></td>
		</tr>
		<tr>
			<td><span markdown=1>`get`</span></td>
			<td><span markdown=1>Returns the element at the specified index</span></td>
		</tr>
		<tr>
			<td><span markdown=1>`indexOf`</span></td>
			<td><span markdown=1>Returns the index of the first occurrence of the specified element in the `ArrayList`</span></td>
		</tr>
		<tr>
			<td><span markdown=1>`remove`</span></td>
			<td><span markdown=1>Overloaded. Removes the first occurrence of the specified value or the element at the specified index</span></td>
		</tr>
		<tr>
			<td><span markdown=1>`size`</span></td>
			<td><span markdown=1>Returns the number of element stored in the `ArrayList`</span></td>
		</tr>
		<tr>
			<td><span markdown=1>`trimToSize`</span></td>
			<td><span markdown=1>Trims the capacity of the `ArrayList` to the current number of elements</span></td>
		</tr>
	</tbody>
</table>

```java
// Fig. 7.24: ArrayListCollection.java
// Generic ArrayList<E> collection demonstration.
import java.util.ArrayList;

public class ArrayListCollection {
   public static void main(String[] args) {
      // create a new ArrayList of Strings with an initial capacity of 10
      ArrayList<String> items = new ArrayList<String>();

      items.add("red"); // append an item to the list
      items.add(0, "yellow"); // insert "yellow" at index 0

      // header
      System.out.print(
         "Display list contents with counter-controlled loop:");

      // display the colors in the list
      for (int i = 0; i < items.size(); i++) {
         System.out.printf(" %s", items.get(i));
      }

      // display colors using enhanced for in the display method
      display(items,
         "%nDisplay list contents with enhanced for statement:");

      items.add("green"); // add "green" to the end of the list
      items.add("yellow"); // add "yellow" to the end of the list
      display(items, "List with two new elements:");

      items.remove("yellow"); // remove the first "yellow"
      display(items, "Remove first instance of yellow:");

      items.remove(1); // remove item at index 1
      display(items, "Remove second list element (green):");

      // check if a value is in the List
      System.out.printf("\"red\" is %sin the list%n",
         items.contains("red") ? "": "not ");

      // display number of elements in the List
      System.out.printf("Size: %s%n", items.size());
   }

   // display the ArrayList's elements on the console
   public static void display(ArrayList<String> items, String header) {
      System.out.printf(header); // display header

      // display each element in items
	  // Can use the enhanced for statement with collections
      for (String item : items) {
         System.out.printf(" %s", item);
      }

      System.out.println();
   }
}
```

```
Display list contents with counter-controlled loop: yellow red
Display list contents with enhanced for statement: yellow red
List with two new elements: yellow red green yellow
Remove first instance of yellow: red green yellow
Remove second list element (green): red yellow
"red" is in the list
Size: 2
```
