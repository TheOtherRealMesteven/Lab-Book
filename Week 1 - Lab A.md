# Week 1 - Lab A

## Lab Coverage
#### Question 1
- 🤔 Console string output
#### Question 2
- 🤔 Creating a new project
- 🤔 Assigning variables
- 🤔 Console string input
#### Question 3
- 🤔 Variable Types
#### Question 4
#### Question 5
#### Question 6

## Lab Task Submission

<details> <!-- Question 1 -->
  <summary> Q1. Hello World </summary>

## Question:
Locate the Solution Explorer within Visual Studio and select the Hello World project. Right click on this project and select Build. This should compile and link the project. Now run the Hello World program.
Change between Debug and Release mode. Compile again and rerun the program.
## Solution:
```c++
#include <iostream>

int main(int argc, char** argv) {
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

> - `int` parameter represents the number of arguments that are passed to the program when it is executed.
> - `char**` parameter is a pointer for an array of character pointers. This can also be given as the array in question with `char* argv[]`.
> The array of strings represents the individual argument inputs when the program is executed.
>
> Dont be confused with console inputs, this is different. These are given **before** the program runs.
</details>

> [!NOTE]
> `std::cout` references a namespaces method. By including `using namespace std`; before the code, you can use the methods without writing the namespace.

> [!IMPORTANT]
> To change executing projects, set the desired project as the `default project`; do this by right clicking the project in Solution Explorer and selecting `Set as Startup Project`.

<details> <!-- Question 2 -->
  <summary> Q2. Creating a new project </summary>

## Question:
Create a new Empty C++ Console project called Temperature by using the project application wizard. 

This is done by right clicking on the 500083-Lab-A solution in the Solution Explorer Window and selecting Add » New Project. *NB: Be careful to select a C++, Empty Project*


Create a new cpp file within the temperature project by right clicking on the Temperature project in the Solution Explorer Window and select Add » Add New Item.

**Write a program to input a Fahrenheit measurement, convert it and output a Celsius value. The conversion formula is**
```c++
celsius = 5/9 * (fahrenheit-32)
```
NB: You may want to select the Temperature project as the default project; to do this right click on the Temperature project and select:

`Set as Startup Project`.

## Solution:
```c++
int main(int argc, char** argv) 
{
	float fahrenheit;
	cout << "Enter a Farenheit Temperature: ";
	cin >> fahrenheit;
	float celsius = 5.0 / 9 * (fahrenheit - 32);
	cout << "In Celcius, the temperature is: " << celsius << std::endl;
	return 0;
}
```
## Test data:
|Identifier|Fahrenheit Temp|Celcius Temp|
|--|--|--|
boiling point of water	|212 F	|100 C
body temperature	|98.6 F	|37 C
cool room temperature	|68 F	|20 C
freezing point of water	|32 F	|0 C

## Sample output:
![image](https://github.com/TheOtherRealMesteven/Lab-Book/assets/115008465/a08a8498-2a55-4d87-8b69-769ab39b76c6)


## Reflection:
|Input Value|Expected Value|Actual Value|Acceptable|
|--|--|--|--|
212|100|100|✔
98.6|37|37|✔
68|20|20|✔
32|0|0|✔

The program works as intended.

## Metadata:
Fahrenheit temperature to Celcius temperature converter.

## Further information:
Also what happens if you dividing two integers?
> If you divide two integers then the result value will be an integer regardless of if it has a decimal value attached. However, by making the return value a float or including a float in the process, it will keep the decimal value.

</details>
<details> <!-- Question 3 -->
  <summary> Q3. Types </summary>

## Question:
Using the “Hello World” program as a starting point, write a program that prints out the size in bytes of each of the fundamental data types in C++.
Hint: Make use of the `sizeof()` operator, that returns the size of any data type.
Remember to include both the signed and unsigned versions of each data type.

## Solution:
```c++
#include <iostream>
using namespace std;

int main (int argc, char **argv) {
	
	cout << "Integer Values" << endl;
	cout << "Integer: " << sizeof(int) << "\tUnsigned ver : " << sizeof(unsigned int) << endl;
	cout << "Short: " << sizeof(short) << "\tUnsigned ver: " << sizeof(unsigned short) << endl;
	cout << "Long: " << sizeof(long) << "\tUnsigned ver: " << sizeof(unsigned long) << endl;
	cout << "Long Long: " << sizeof(long long) << "\tUnsigned ver: " << sizeof(unsigned long long) << endl;
	cout << endl; cout << endl;

	cout << "Float Values" << endl;
	cout << "Float: " << sizeof(float) << endl;
	cout << "Double: " << sizeof(double) << endl;
	cout << "Long Double: " << sizeof(long double) << endl;
	cout << endl; cout << endl;

	cout << "Char Values" << endl;
	cout << "Char: " << sizeof(char) << endl;
	cout << "Signed Char: " << sizeof(signed char) << "\tUnsigned Char: " << sizeof(unsigned char) << endl;
	cout << "wchar_t: " << sizeof(wchar_t) << endl;
	cout << "Char16_t: " << sizeof(char16_t) << "\tChar32_t: " << sizeof(char32_t) << endl;
	cout << endl; cout << endl;

	cout << "Other Values" << endl;
	cout << "Bool: " << sizeof(bool) << endl;

	return 0;
}
```
## Test data:
n/a
## Sample output:
![image](https://github.com/TheOtherRealMesteven/Lab-Book/assets/115008465/41467ac2-633a-49eb-a702-250060d415df)

## Reflection:
Unsigned variants of values have the same length as their signed counterparts. Which makes sense due to the premise of signed values not increasing the range of values.
## Metadata:
Character type sizing display.
## Further information:
Char_t is used to represent extended character sets such as unicode characters as they need more than a single byte.

</details>
<details> <!-- Question 4 -->
  <summary> Q4. Floating point precision </summary>

## Question:
In the lectures we discussed the precision of floating point numbers within C++, and how due to this precision the equality operator was unreliable.
### A)
Write a simple program that includes the lines:
```c++
double x = 10.0;
double y = 10.0;
if (x == y)
      cout << “X and Y are identical” << endl;
```
Did the program execute as expected?
### B)
Now try `y = 20.0 / 2.0` and execute the program again.
### C)
Then try a more complex calculation for y e.g.
```c++
const double x = 100000.123456789;
const double a = 200000.123456789;
double y = (x + a) / x;
double z = 1.0 + (a / x);
if (y == z) 
   cout << “y and z are identical” << endl;
```
### D)
Now try different values for x and a

Printing out the values of x, y and z, may be useful in helping you form an opinion of what is happening.
### E)
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
In the lectures we have looked at constructs and iterators. Below is some C# code that calculates the factorial of a number 

(see https://www.mathsisfun.com/numbers/factorial.html for details of a factorial).
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
int main(int argn, char* argv[])
{
    int factorialNumber = 5;
    int factorialTotal = 1;
    for (int n = 2; n <= factorialNumber; n++) {
        factorialTotal *= n;
    }
    cout << factorialTotal << endl;
}
```
## Test data:
n/a
## Sample output:
120
## Reflection:
The code used in the factorial calculator is identical to the C# code, aside from the console output code and the method structure.
> Rather than having an array input for the methods arguments, it has the size and array input. This is likely due to there being less compiler safe guards to prevent errors.
> And the console output method differs from C# as the values must be inserted akin to commands rather than passed through as just a value.
## Metadata:
Factorial Calculator.
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
