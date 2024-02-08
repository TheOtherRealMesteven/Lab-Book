# Week 1 - Lab A

<details> <!-- Question 1 -->
  <summary> Q1. Hello World </summary>

## Question:
Locate the Solution Explorer within Visual Studio and select the Hello World project. Right click on this project and select Build. This should compile and link the project. Now run the Hello World program.
Change between Debug and Release mode. Compile again and rerun the program.
## Solution:
```c++
#include <iostream>

int main(int, char**) {
	std::cout << "Hello World" << std::endl;
	return 0;
} 
```
## Test data:
n/a
## Sample output:
n/a
## Reflection:
This is the base getting started script used in programming lessons.
## Metadata:
Hello World
## Further information:
What are purpose are the parameters in main?

- `int` represents the number of arguments that are passed to the program when it is executed.
- `char**` is a pointer for an array of character pointers. This can also be given as the array in question with `char* args[]`.
The array of strings represents the individual argument inputs when the program is executed.

Dont be confused with console inputs, this is different. These are given **before** the program runs.
</details>
<details> <!-- Question 2 -->
  <summary> Q2. Creating a new project </summary>

## Question:
Create a new Empty C++ Console project called Temperature by using the project application wizard. This is done by right clicking on the 500083-Lab-A solution in the Solution Explorer Window and selecting Add » New Project.
NB: Be careful to select a C++, Empty Project
Create a new cpp file within the temperature project by right clicking on the Temperature project in the Solution Explorer Window and select Add » Add New Item.
Write a program to input a Fahrenheit measurement, convert it and output a Celsius value. The conversion formula is
```c++
celsius = 5/9 * (fahrenheit-32)
```
NB: You may want to select the Temperature project as the default project; to do this right click on the Temperature project and select Set as Startup Project.

## Solution:
```c++
 
```
## Test data:
n/a
## Sample output:
n/a
## Reflection:

## Metadata:

## Further information:
Also what happens if you dividing two integers?

</details>
<details> <!-- Question 3 -->
  <summary> Q3. Types </summary>

## Question:
Using the “Hello World” program as a starting point, write a program that prints out the size in bytes of each of the fundamental data types in C++.
Hint: Make use of the `sizeof()` operator, that returns the size of any data type.
Remember to include both the signed and unsigned versions of each data type.

## Solution:
```c++
 
```
## Test data:
n/a
## Sample output:
n/a
## Reflection:

## Metadata:

## Further information:


</details>
<details> <!-- Question 4 -->
  <summary> Q4. Floating point precision </summary>

## Question:
In the lectures we discussed the precision of floating point numbers within C++, and how due to this precision the equality operator was unreliable.
Write a simple program that includes the lines:
```c++
double x = 10.0;
double y = 10.0;
if (x == y)
      cout << “X and Y are identical” << endl;
```
Did the program execute as expected?
Now try `y = 20.0 / 2.0` and execute the program again.
Then try a more complex calculation for y e.g.
```c++
const double x = 100000.123456789;
const double a = 200000.123456789;
double y = (x + a) / x;
double z = 1.0 + (a / x);
if (y == z) 
   cout << “y and z are identical” << endl;
```
Now try different values for x and a
Printing out the values of x, y and z, may be useful in helping you form an opinion of what is happening.
Once you’re confident you understand the logic, investigate:
```c++
double z = x / y;
```
How small does y have to be before you get a “divide by zero” error? Does the value of x affect the result?

## Solution:
```c++
 
```
## Test data:
n/a
## Sample output:
n/a
## Reflection:

## Metadata:

## Further information:


</details>
<details> <!-- Question 5 -->
  <summary> Q5. C#/C++ Iteration Comparison (for loop) </summary>

## Question:
In the lectures we have looked at constructs and iterators.
Below is some C# code that calculates the factorial of a number (see https://www.mathsisfun.com/numbers/factorial.html for details of a factorial).
```c++
static void Main(string[] args)
{
   int factorialNumber = 5;
   int factorialTotal = 1;

   for(int n = 2; n <= factorialNumber; ++n)
   {
      factorialTotal *= n;
   }

   System.Console.WriteLine(factorialTotal);
}
```
Port the above C# code in to C++ using the provided Main.cpp file.
[LAB BOOK - Add your C++ code to your lab book. Then reflect on what you have to change (or not change) from C# to C++ in terms of the iteration]

## Solution:
```c++
 
```
## Test data:
n/a
## Sample output:
n/a
## Reflection:

## Metadata:

## Further information:


</details>
<details> <!-- Question 6 -->
  <summary> Q6. Calculate Average using Iteration (while loop) </summary>

## Question:
Using a while loop (or do-while loop), calculate the average value of values provided by the user from the console (cin). You should calculate the average after the user either enters a negative number or the user enters a non-number value (e.g. a letter).
The following C++ code will get an int value from the user.
```c++
cout << "Please enter an int value, then press Enter" << endl;
int n = 0;
cin >> n;
```
[LAB BOOK - Add your C++ code to your lab book. Then reflect on what you have learnt]

## Solution:
```c++
 
```
## Test data:
n/a
## Sample output:
n/a
## Reflection:

## Metadata:

## Further information:


</details>
