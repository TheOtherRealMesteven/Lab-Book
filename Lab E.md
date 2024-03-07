# Week 5 - Lab E

## Lab Coverage
*For future review, the coverage of each task has been listed below to act as an index to the taught material.*
|Question|Learned Stuff|
|--|--|
|**1**| 🤔 Learnt how to override operators
|**2**| 🤔 
|**3**| 🤔 
|**4**| 🤔 Practice using reference parameters
|**5**| 🤔 

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
  <summary> Q5. </summary>

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
