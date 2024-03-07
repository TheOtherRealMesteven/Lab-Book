# Week 5 - Lab E

## Lab Coverage
*For future review, the coverage of each task has been listed below to act as an index to the taught material.*
|Question|Learned Stuff|
|--|--|
|**1**| 🤔 Learnt how to override operators
|**2**| 🤔 
|**3**| 🤔 
|**4**| 🤔 Practice using reference parameters
|**5**| 🤔 More practice with memory locations not being values.

## Lab Task Submission
*The tasks assigned to be reviewed for the weeks lab has been completed below.*

----

<details> <!-- Question 1 -->
  <summary> Q1. Operators in Grid </summary>

## Question:
Extend your code from Q2 and Q3 in Lab D.

Add the following functionality to your program:

 - The ability to write the Grid to an ostream using the auxiliary operator<<
 - The ability to read in the values from an istream into the Grid using the auxiliary operator>>

**[LAB BOOK - Copy your code for these functions into your lab book]**
## Solution:
```c++
const int _size = 9;
int grid[_size][_size];

// Overload the insert operator (<<) to write the grid to an ostream
ostream& operator<<(ostream& os, const Grid& grid) {
    for (int i = 0; i < _size; i++) {
        for (int j = 0; j < _size; j++) {
            os << grid[i][j] << " ";
        }
        os << endl;
    }
    return os;
}

// Overload the extract operator (>>) to read the grid from an istream
istream& operator>>(istream& is, Grid& grid) {
    for (int i = 0; i < _size; i++) {
        for (int j = 0; j < _size; j++) {
            if (!(is >> ws >> grid[i][j])) {
                cerr << "Error: Failed to read integer from stream.\n";
                return is;
            }
        }
    }
    return is;
}
```
</details>

----

<details> <!-- Question 2 -->
  <summary> Q2. </summary>

## Question:

## Solution:
```c++
```
## Test data:
n/a
## Sample output:
n/a
## Reflection:

</details>

----

<details> <!-- Question 3 -->
  <summary> Q3. </summary>

## Question:

## Solution:
```c++
```
## Test data:
n/a
## Sample output:
n/a
## Reflection:

</details>

----

<details> <!-- Question 4 -->
  <summary> Q4. Parameters </summary>

## Question:
Open and build the Parameters project. We want our program to swap the values of the two variables a and b.

Compile and run the program.

It does not give the correct answer; a and b are not swapped.

**[LAB BOOK - Copy your code for pass-by-value and pass-by-ref into your lab book. Reflect on the difference between them]**

## Solution:
**Pass by value:** 
Functional Solution: ❎

```c++
#include <iostream>
using namespace std;

void myswap(int lhs, int rhs) {
    int temp = lhs;
    lhs = rhs;
    rhs = temp;
}
 
int main(int, char**) { 
    int a = 10;
    int b = 20;

    cout << "a=" << a << ", b=" << b << endl;

    myswap(a, b);

    cout << "a=" << a << ", b=" << b << endl;

    system("PAUSE");
    return 0;
}
```

When passing the parameters by value, the function creates copies of the parameter values meaning the `lhs` and `rhs` variables have no affect on the original parameter values. And so `a` and `b` cannot be passed correctly unless it is returned through the function.

**Pass by reference:**
Functional Solution: ✅

```c++
#include <iostream>
using namespace std;

void myswap(int &lhs, int &rhs) {
    int temp = lhs;
    lhs = rhs;
    rhs = temp;
}
 
int main(int, char**) { 
    int a = 10;
    int b = 20;

    cout << "a=" << a << ", b=" << b << endl;

    myswap(a, b);

    cout << "a=" << a << ", b=" << b << endl;

    system("PAUSE");
    return 0;
}
```

When passing the parameters by reference, the function stores pointers to the parameters original variables. Meaning the `lhs` and `rhs` variables have an affect on the original parameter values and so `a` and `b` can be swapped properly.

</details>

----

<details> <!-- Question 5 -->
  <summary> Q5. Return by value </summary>

## Question:
### Return by value
Replace the myswap function with the clamp function
```c++
int clamp(int value, int low, int high) {
    if (value < low)
        return low;
    if (value > high)
        return high;
    return value;
}
```
This function clamps or limits a value between an upper and lower bound.
### Return by reference

Add this alternative clamp function
```c++
int& clamp(int& value, int low, int high) {
    if (value < low)
        return low;
    if (value > high)
        return high;
    return value;
}
```
Try calling your function using the following code
```c++
    int value1 = 10;
    int value2 = 20;
    int result1 = clamp(value1, 0, 30) + clamp(value2, 0, 30); 
```
Does result1 hold the correct value?

Now try:
```c++
    int result2 = clamp(value1, 0, 5) + clamp(value2, 0, 10);
```
Does result2 hold the correct value?
Can you explain what is happening?

**[LAB BOOK - Copy your code for return-by-value and return-by-ref into your lab book. Reflect on the difference between them]**
## Solution:

**Return by value:**
Functional Solution: ✅

```c++
int clamp(int value, int low, int high) {
	if (value < low)
		return low;
	if (value > high)
		return high;
	return value;
}

int main(int, char**) {

	int a = 10;
	int b = 20;
	
	cout << "a=" << a << ", b=" << b << endl;

	int result1 = clamp(a, 0, 30) + clamp(b, 0, 30);
	cout << "Result 1: " << result1 << endl;

	int result2 = clamp(a, 0, 5) + clamp(b, 0, 10);
	cout << "Result 2: " << result2 << endl;
	
	return 0;
}
```

With the above code, the value passed in `value` is a copy of the original value. In the scenario, it is either 10 for `a` or 20 for `b`. It then returns the value if within the range suggested or the maximum and minimum. This works as intended as the value being passed in is clamped within the range of values which are also being passed in.

**Return by reference:**
Functional Solution: ❎

```c++
int& clamp(int& value, int low, int high) {
    if (value < low)
        return low;
    if (value > high)
        return high;
    return value;
}

int main(int, char**) {

	int a = 10;
	int b = 20;
	
	cout << "a=" << a << ", b=" << b << endl;

	int result1 = clamp(a, 0, 30) + clamp(b, 0, 30);
	cout << "Result 1: " << result1 << endl;

	int result2 = clamp(a, 0, 5) + clamp(b, 0, 10);
	cout << "Result 2: " << result2 << endl;
	
	return 0;
}
```

With the above code, the value passed in `value` is the memory address of the original value. In this scenario, it is likely a value very different to the assigned values. It then returns the memory location if within the range suggested or the maximum and minimum as memory locations. This means the returned value can be completely unassociated to the program depending on the values stored in the memory locations at the time.

With the two results, the first one does not return the correct result as they are both clamped to be the same value based on memory location.
Whilst the second one returns the correct result as the clamped range is smaller and more relevant to the value due to the memory location being closer to the supplied clamp range.
</details>

----
