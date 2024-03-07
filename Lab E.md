# Week 5 - Lab E

## Lab Coverage
*For future review, the coverage of each task has been listed below to act as an index to the taught material.*
|Question|Learned Stuff|
|--|--|
|**1**| 🤔 Learnt how to override operators
|**2**| 🤔 
|**3**| 🤔 
|**4**| 🤔 
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
  <summary> Q4. </summary>

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
