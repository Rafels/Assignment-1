# Assignment 1

### Rafael Gallegos S929574
***

## Exercise 1

**Write a C program that prompts a user to input 6 integers and print the largest.**

To solve the exercise the program makes use of an integer array, this simplifies the input and output of the 6 integers entered by the user. By using a for-loop the program can first scan in the input, print it out and then compare each value in the array by using an if-statement.
The if-statement compares the value in the current iteration with the variable "largest", which is initialized to '0'. This works as a fail-safe as long at least one of the six values are positive. If the current value is larger than "largest", then the current value in the array is given to "largest". When the last for-loop is finished the "largest" is displayed and the program ends.

In hindsight, it would be preferable to prompt the user to only use positive values, or at least initialize "largest" to a large negative number.


### The Code

```c++

/*
1. Write a C program that prompts a user to input 6 integers and print the largest.
*/
#include <stdio.h>

int main()
{
	int numbers[6] = {0,0,0,0,0,0};                     //The array is declared and initialized to 0.
	int largest = 0;


	printf("Please enter your six decimal numbers.\n"); //First for loop for scaning in the values
	for (int i = 0; i < 6; ++i)
	{
		scanf("%d",&numbers[i]);                    
	}
	printf("You entered the following numbers:");       //The second for loop, prints out for the user.
	for (int i = 0; i < 6; ++i)
	{
		printf(" %d ",numbers[i]);
	}

	for (int i = 0; i < 6; ++i)			    //The last foor loop, which compares the values.
	{
		if (numbers[i] > largest)
		{
			largest = numbers[i];
		}
	}
	printf("\nThe largest number is: %d", largest);

	return 0;				
}
```
### The Results:
```
Please enter inn your six decimal numbers.
12
34
23
56
70
6
You entered the following numbers: 12  34  23  56  70  6
The largest number you entered is: 70
```
## Exercise 2

**Write a C program that converts a temperature from Celsius to Fahrenheit and vice versa.**

To solve this exercise, the program uses a mathematical equation that divides, multiplies, sums and subtracts the variables. And because we are dividing values, it is easier to avoid mathematical errors by using floating number variables. Another way of getting around this is by casting the variables.

The program prompts the user to input either "f" or "c" to select which temperature standard to convert from, this character is then used to enter the correct if-statement. Each if-statement prompts the user to enter the degrees, it then converts the value and prints out the results.

The if-statements are inside a while-loop which ends if the character "choice" is equal to 'q', this allows the user to repeat the conversion or exit the program by entering "q". When the while-loop exits, the program ends.


### The code:
```c++
/*
2. Write a C program that converts a temperature from Celsius to Fahrenheit and vice versa. 
(Hint: Fahrenheit = (9/5) * Celsius + 32).
*/

#include <stdio.h>

int main()
{
	char choice;
	float fahrenheit,celcius = 0;
	
	printf("Welcome, convert from celcius to fahrenheit or vice versa.\nEnter \"c\" for celcius or \"f\" for fahrenheit.\n");
	scanf("%c",&choice);

	while(choice != 'q')
		{
			if (choice == 'c')
			{
				printf("Enter your degrees:\n");
				scanf("%f",&celcius);
				fahrenheit = ((9*celcius)/5 + 32);
				printf("%.1f degrees celcius equals %.1f degrees fahrenheit\n",celcius,fahrenheit);
			} else if (choice == 'f')
			{
				printf("Enter your degrees:\n");
				scanf("%f",&fahrenheit);
				celcius = ((fahrenheit-32)*5)/9;
				printf("%.1f degrees fahrenheit equals %.1f degrees celcius\n",fahrenheit,celcius);
			}

			printf("Try again or enter ""q"" to quit.\n");
			scanf(" %c",&choice);
		}


		return 0;
}
```
### The Results
```
Welcome, convert from celcius to fahrenheit or vice versa.
Enter "c" for celcius or "f" for fahrenheit.
c
Enter your degrees:
125
125.0 degrees celcius equals 257.0 degrees fahrenheit
Try again or enter q to quit.
f
Enter your degrees:
257
257.0 degrees fahrenheit equals 125.0 degrees celcius
Try again or enter q to quit.
q
```
## Exercise 3

**Write a C program that counts the number of blank scaces, new lines and tabs of an input.**

The exercise requires a program that can read an input and then count the different characters if they fit the description. The new line("\n"), the tab("\t") and the blank space (" ") are all represented by characters who have a specific integer-value.

The user is prompted to enter the sentence and end it with "Ctrl + z".
By using the getchar() function and a while-loop, the program checks the input and counts each of the characters by using an if-statement.

As the results show, the program is a bit flawed. If the user enters a newline before the exit-character, the program will count the newline. Also, if the user enters the exit-characters, the program jumps to a new line and the user needs to input the exit-character again.

### The code;

```c++
/*
3. Write a C program that counts the number of blank spaces, new lines and tabs of an input. 
For example: if the input is "Effective Programming in C and C++" - the output should be "New Lines=1, Blank Spaces=5 and Tabs=0".
*/

#include <stdio.h>

int main()
{
	int input, newLines, blankSpaces, tabs;
	input = 0;
	newLines = 0;
	blankSpaces = 0;
	tabs = 0;

	printf("Welcome \nPlease type in your sentence and end it with Ctrl + z.\n");

	while((input = getchar()) != EOF)
	{
		if (input == '\n')
		{
			++newLines;
		}
		if (input == '\t')
		{
			++tabs;
		}
		if (input == ' ')
		{
			++blankSpaces;
		}
	}

	printf("The number of blank spaces are: %d\nThe number of tabs are: %d\nThe number of new lines are: %d", blankSpaces,tabs,newLines);

	return 0;
}
```
### The Results
```
Welcome
Please type in your sentence and end it with Ctrl + z.
Hi, my name is Rafels and this is a c-program.
        I might add a tab or just a new line
^Z
The number of blank spaces are: 18
The number of tabs are: 1
The number of new lines are: 2
```
## Exercise 4
**Write a C or C++ program that counts the number of words in a given sentence**
This program is written in C and uses a character array to store the sentence. The array size is set to 200, to insure enough space. The user is prompted to input a sentence, and a scanf function reads the character array. The scanf function uses the [^\n] to skip the whitespace between the words.

When the scan is complete, a for-loop runs through the array until the character-value is equal to the null terminator (\0). While the for-loop is running an if-statement checks for blank spaces in between the words and ads 1 to the word count if the statement is true.
The statement also avoids counting double blank spaces by checking the previous character.

Before printing the count, 1 is added to have the right amount of words.
One problem with the program occurs if the user inputs a blank space before ending the sentence, this will then give the wrong word count.

### The Code
```c++
/*
4. Write a C or C++ program that counts the number of words in a given sentence.
*/

#include <stdio.h>

int main()
{
	char string[200];
	int numberOfWords = 0;

	printf("Please input a string and end with return\n");

	scanf(" %[^\n]s",string);

	for (int i = 0; string[i] != '\0'; ++i)
	{
		if (string[i] == ' ' && string[i-1] != ' ')
		{
			++numberOfWords;
		}
	}

	printf("The number of words in your string is: %d", numberOfWords + 1 );


	return 0;
}
```
### The Results:
```
Please input a string and end with return
THis is a string, not a very long one though.
The number of words in your string is: 10
```
## Exercise 5
**Write a program in either C or C++ that prints the following pattern.**
```
1 
1 2 
1 2 3 
1 2 3 4 
1 2 3 4 5
```
To solve the exercise this program uses a bubble sorter that is comprised of two for-loops that prints out the number in the given pattern.
First the user is prompted to input the number of rows for the pattern, then the value is scaned and given to "numberOfRows" variable.
This variable is then set as the maximum iteration for the first for-loop, the second for-loop uses then the current iteration of the first for-loop as it's maximum. This allows the program to print out the pattern. In the first 10 iterations, double spacing is used, then the program uses a single spacing. This is because of the size of the integer that is printed.

The obvious limitation of the program is the size of the pattern, it will print out wrong pattern if the size is too big.

### The Code:
```c++
/*
5. Write a program in either C or C++ that prints the following pattern. 
1 
1 2 
1 2 3 
1 2 3 4 
1 2 3 4 5
*/

#include <iostream>
using namespace std;

int main()
{
	int numberOfRows = 0;
	cout<<"Please enter the number of rows for your pattern\n";
	cin>>numberOfRows;
	for (int i = 0; i < numberOfRows+1;++i)
	{
		for (int j = 0; j < i; ++j)
		{
			if(j >= 9)
			{
				cout<<(j+1)<<" ";
			}else
			{

				cout<<(j+1)<<"  ";
			}
		}
		cout<<endl;
	}
	return 0;
}
```
### The Results:
```
Please enter the number of rows for your pattern
20

1
1  2
1  2  3
1  2  3  4
1  2  3  4  5
1  2  3  4  5  6
1  2  3  4  5  6  7
1  2  3  4  5  6  7  8
1  2  3  4  5  6  7  8  9
1  2  3  4  5  6  7  8  9  10
1  2  3  4  5  6  7  8  9  10 11
1  2  3  4  5  6  7  8  9  10 11 12
1  2  3  4  5  6  7  8  9  10 11 12 13
1  2  3  4  5  6  7  8  9  10 11 12 13 14
1  2  3  4  5  6  7  8  9  10 11 12 13 14 15
1  2  3  4  5  6  7  8  9  10 11 12 13 14 15 16
1  2  3  4  5  6  7  8  9  10 11 12 13 14 15 16 17
1  2  3  4  5  6  7  8  9  10 11 12 13 14 15 16 17 18
1  2  3  4  5  6  7  8  9  10 11 12 13 14 15 16 17 18 19
1  2  3  4  5  6  7  8  9  10 11 12 13 14 15 16 17 18 19 20
```
## Exercise 6
***Write a C++ function which takes a single integer parameter, and returns the boolean "True" if the given number is even and "False" otherwise***

This program uses a function to check if the value is even, in order to use functions i C++ the function must be initialized at the start. 
At the start the user is prompted to input a positive integer value, the value is then used in the function "evenOrUneven" and returns the value to the bool "even".
The function works by using an if-else-statement that checks it the number with modulo 2 is equal to zero. The function then returns a Boolean value, 1 if the number is even or 0 if the value is uneven.

After the function is finished, the program runs "even" through an if-else-statement and prints out the result accordingly.

### The Code
```c++
/*
6.  Write a C++ function which takes a single integer parameter, and returns the boolean ”True” if the given 
	number is even and ”False” otherwise.
*/

#include "iostream"
using namespace std;

bool evenOrUneven (int number);

int main()
{
	int number = 0;
	bool even;
	cout<<"Is your number even?\nPlease input your integer number:\n";
	cin>>number;
	even = evenOrUneven(number);

	if (even == 1)
	{
		cout<<"True: Your number is even!";
	} else
	{
		cout<<"False: Your number is un-even..";
	}
	return 0;
}
bool evenOrUneven (int number)
{
	bool even;
	if (number%2 == 0)
	{
		even = 1;
	}else
	{
		even = 0;
	}
	return even;
}
```
### The Results
```
Is your number even?
Please input your integer number:
124
True: Your number is even!

Is your number even?
Please input your integer number:
123
False: Your number is un-even..
```
## Exercise 7
***In number theory, a perfect number is a positive integer that is equal to the sum of its proper positive divisors, that 
is, the sum of its positive divisors excluding the number itself. The smallest perfect number is 6, which is the sum of 1, 2,and 3. 
Other perfect numbers are 28, 496, and 8,128. Write a program in either C or C++ to print all perfect numbers in given range 
using a function.***


This exercise is quite a challenge because it uses a mathematical concept which is difficult to understand and therefore difficult to implement in a code. 

To solve the problem, the program uses a function with a double for-loop that checks the current value with all the previous values. An if-statement then checks if the current value is dividable with the previous values, and adds the value together with "sum" and adds it to "sum". If the sum of all the values equals to the current iteration of the first for-loop, it prints out the iteration as a perfect number. The function then sets the sum to zero before starting to look for the next number.

The main program is quite simple, as it only prompts the user to select the range. It also warns the user to avoid zero and values over 10k, as the program will use quite some time to find the larger numbers. As a precaution the function aborts if the range is out of bounds.

### The Code
```c++
/*
7. In number theory, a perfect number is a positive integer that is equal to the sum of its proper positive divisors, that 
is, the sum of its positive divisors excluding the number itself. The smallest perfect number is 6, which is the sum of 1, 2,and 3. 
Other perfect numbers are 28, 496, and 8,128. Write a program in either C or C++ to print all perfect numbers in given range 
using a function.
*/
#include "iostream"

using namespace std;

void perfectNumber(int minRange, int maxRange);


int main()
{
	int max;
	int min;
	cout<<"Please specify your range, min 1 and max 10k\n";
	cout<<"Minimal range: ";
	cin>>min;
	cout<<"Maximum range: ";
	cin>>max;

	perfectNumber(min,max);

	return 0;
}

void perfectNumber(int minRange, int maxRange)
{
	if (maxRange > 10000 || minRange < 1)
	{
		cout<<"Your max range is to high or the min is to low, the program can't handle it";
		return;
	}
	int sum = 0,i,j;
	for(i = minRange; i <= maxRange; ++i)
	{
		for(j = 1; j <= maxRange; j++)
		{
			if (j<i)
			{
				if (i%j == 0)
				{
					sum = sum + j;
				}
			}
		}
		if (sum == i)
		{
			cout<<i<<" ";
		}
		sum = 0;
	}
}


```
## The Results
```
Please specify your range, min 1 and max 10k
Minimal range: 1
Maximum range: 5000
6 28 496
```
## Exercise 8
***Write a program either in C or C++ that checks whether a given triangle is equilateral, isosceles or scalene.***

The program starts by prompting the user to enter the length of the three sides. When the values have been entered, they are compared to each other by using several if-else statements. 
The first if-else statement is checks if all the values are equal, then prints out if it is equilateral.
The second if-else statement checks if two of the values are equal and different from the third value.
The third and final if-statement checks if all the values are un-equal.
Each of the statements print out the result if the statement is true.

## The Code
```c++
/*
8. In mathematics, a triangle is a polygon with three edges and three vertices. 
Triangles can be classified according to the lengths of their sides. 
• An equilateral triangle has all sides the same length. 
• An isosceles triangle has two sides of equal length. 
• A scalene triangle has all its sides of different lengths. 
Write a program either in C or C++ that checks whether a given triangle is equilateral, isosceles or scalene.
*/

#include "iostream"

using namespace std;

int main()
{
	int x,y,z;
	cout<<"Please enter the length of the three siden of your triangle\n";
	cout<<"Side X:";
	cin>>x;
	cout<<"Side y:";
	cin>>y;
	cout<<"Side Z:";
	cin>>z;

	if (x == y && x == z)
	{
		cout<<"Your triangle is equilateral";
	} else if ((x == y && x != z)||(y == z && y != x)||(x == z && x != y))
	{
		cout<<"Your triangle is isosceles";
	} else if (x != y && x != z && y != z)
	{
		cout<<"Your triangle is scalene";
	}

	return 0;
}
```
### The Results
```
Please enter the length of the three siden of your triangle
Side X:12
Side y:23
Side Z:50
Your triangle is scalene
```
```
Please enter the length of the three siden of your triangle
Side X:10
Side y:10
Side Z:10
Your triangle is equilateral
```
```
Please enter the length of the three siden of your triangle
Side X:10
Side y:10
Side Z:15
Your triangle is isosceles
```
## Exercise 9
**Implement a C++ function to compute and display the first n numbers of the Fibonacci list, 
where n is provided as an input by the user.**

To solve the exercise the program uses a function that calculates the sum of the two preceding values in an array and sets the sum of the two values as the current value. By initializing the array with the two first Fibonacci numbers; {1,1}, it is easier to calculate the next numbers in the array. 
At the beginning of the program the user is prompted to input the desired number of Fibonacci number in the list. the number is scanned and inserted in the function.

The function uses a for-loop which runs through the array and prints out the current value. To have a cleaner output, the function uses an if statement that ads a new line if the iteration is at a certain point.

As the program uses integer numbers, it is limited to a list of only 46 Fibonacci numbers.

### The Code
```c++
/*
9. In mathematics, the Fibonacci numbers are the sequence of numbers {Fn}∞ n=1 deﬁned by the linear recurrence 
equation Fn = Fn−1 + Fn−2 with F1 = F2 = 1, and conventionally deﬁning F0 = 0. 
The ﬁrst few Fibonacci numbers are 1, 1, 2, 3, 5, 8, 13, 21,...etc. 
Implement a C++ function to compute and display the ﬁrst n numbers of the Fibonacci list, 
where n is provided as an input by the user.
*/


#include "iostream"

using namespace std;

void fibonacci(int n);

int main()
{
	int n;
	cout<<"Please enter the n-number of Fibonacci numbers you wish to calculate.\n";
	cout<<"Please note that the program can't compute numbers over n = 46.\n";
	cin>>n;
	fibonacci(n);


	return 0;
}

void fibonacci(int n)
{
	int fn[n] = {1,1};
	cout<<"The fibonacci sequence is: "<<fn[0]<<", "<<fn[1]<<", ";
	int fib = 0;
	for (int i = 0; i < (n-2); ++i)
	{
		if (i==25 || i == 42) //only used to make it easier to read in cmd.
		{
			cout<<"\n";
		}
		fn[i+2] = fn[i+1] + fn[i];
		fib = fn[i+2]; 
		cout<<fib<<", ";
		
	}
}
```
### The Results
```
Please enter the n-number of Fibonacci numbers you wish to calculate.
Please note that the program can't compute numbers over n = 46.
30
The fibonacci sequence is: 1, 1, 2, 3, 5, 8, 13, 21, 34, 55, 89, 144, 233, 377, 610, 987, 1597, 2584, 4181, 6765, 10946, 17711, 28657, 46368, 75025, 121393, 196418,
317811, 514229, 832040,
```
## Exercise 10
This exercise is meant to illustrate the difference of swapping values by reference and by value.
To complete the exercise the program uses two functions that swap values, which requires a variable "inbetween" that stores one of the values before the swap, this is done to not lose the value. Both functions print out the values before ending, the values are then printed in main to illustrate how the functions work.

The functions are quite similar in how they work, the difference is that swap_2 uses the address of the variables and not the actual value, this result in the values being swapped globally and not only locally in the function, like in the function swap_1.


### The Code
```c++
/*
10. Implement two C++ functions called swap 1(int,int) and swap 2(int&,int&) that are supposed to swap two values. 
Display the ﬁnal values just before the end of each function, and display the results from the main function before and after the call. 
What do you make of these two functions? (Hint: refer to Friday’s lecture note)
*/
#include "iostream"

using namespace std;

void swap_1(int a, int b);
void swap_2(int& a, int& b);

int main()
{
	int a,b;
	cout<<"Please input to integers\n";
	cout<<"Integer a:";
	cin>>a;
	cout<<"Integer b:";
	cin>>b;
	cout<<"Your integers are: a = "<<a<<" and b = "<<b<<"\n";

	swap_1(a,b);
	cout<<"After being swapped by value your integers are now: a = "<<a<<" and b = "<<b<<"\n";

	swap_2(a,b);
	cout<<"After being swapped by referanse your integers are now: a = "<<a<<" and b = "<<b;

	return 0;
}

void swap_1(int a, int b)
{
	int inbetween;
	inbetween = a;
	a = b;
	b = inbetween;
	cout<<"Before the swap_1 function ends: a = "<<a<<" and b = "<<b<<"\n";
}
void swap_2(int& a, int& b)
{
	int inbetween;
	inbetween = a;
	a = b;
	b = inbetween;
	cout<<"Before the swap_2 function ends: a = "<<a<<" and b = "<<b<<"\n";
}
```
### The Results
```
Please input to integers
Integer a:20
Integer b:15
Your integers are: a = 20 and b = 15
Before the swap_1 function ends: a = 15 and b = 20
After being swapped by value your integers are now: a = 20 and b = 15
Before the swap_2 function ends: a = 15 and b = 20
After being swapped by referanse your integers are now: a = 15 and b = 20
```
