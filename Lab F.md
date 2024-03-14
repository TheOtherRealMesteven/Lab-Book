# Week 6 - Lab F

## Lab Coverage
*For future review, the coverage of each task has been listed below to act as an index to the taught material.*
|Question|Learned Stuff|
|--|--|
|**1**| 🤔 How to create Template Classes
|**2**| 🤔 Template class used with different datatype
|**3**| 🤔 Binary Search: Recursion and Iteration

## Lab Task Submission
*The tasks assigned to be reviewed for the weeks lab has been completed below.*

----

<details> <!-- Question 1 -->
  <summary> Q1. Template Class </summary>

## Question:
You are going to turn the Grid class into a template class so that we can store any type of number, e.g. float, int, double, into our 2D grid array.

<details>
	<summary>Before</summary>

### Main.cpp
```c++
#include <iostream>
#include "Grid.h"
using namespace std;

int main(int argn, char* argv[])
{
	Grid grid;
	grid.LoadGrid("Grid1.txt");
	grid.SaveGrid("OutGrid.txt");

	system("pause");
}
```
### Grid.cpp
```c++
#include "Grid.h"
#include "iostream"
#include "fstream"
using namespace std;

Grid::Grid()
{
}

Grid::~Grid()
{
}

void Grid::LoadGrid(const char filename[])
{
    ifstream fin(filename, ios::in);
    if (!fin) {
        cerr << "Error: Unable to open the input file.\n";
        return;
    }
    for (int i = 0; i < m_size; i++) {
        for (int j = 0; j < m_size; j++) {
            fin >> ws; // Skip whitespace characters, including spaces
            if (!(fin >> m_grid[i][j])) {
                cerr << "Error: Failed to read integer from file.\n";
                return;
            }
        }
    }
    fin.close();
}

void Grid::SaveGrid(const char filename[])
{
    ofstream fout(filename, ios::out);
    if (!fout)
    {
        cerr << "Error: Unable to open the output file.\n";
        return;
    }
    for (int i = 0; i < m_size; i++) {
        for (int j = 0; j < m_size; j++) {
            fout << m_grid[i][j] << " ";
        }
        fout << endl;
    }
    fout.close();
    cout << "Grid saved to: " << filename << endl;
}
```
### Grid.h
```c++
#pragma once

class Grid
{
public:
	Grid();
	~Grid();

	void LoadGrid(const char filename[]);
	void SaveGrid(const char filename[]);

private:
	static const int m_size = 9;
	int m_grid[m_size][m_size];
};
```
</details>
<details>
	<summary>After</summary>
	
### Main.cpp
```c++
#include <iostream>
#include "Grid.h"
using namespace std;

int main(int argn, char* argv[])
{
	Grid<int> grid;
	grid.LoadGrid("Grid1.txt");
	grid.SaveGrid("OutGrid.txt");

	system("pause");
}
```
### Grid.cpp
N/A
### Grid.h
```c++
#pragma once

#include <iostream>
#include <fstream>

using namespace std;

template<class T>
class Grid
{
public:
	void LoadGrid(const char filename[]) 
    {
        ifstream fin(filename, ios::in);
        if (!fin) {
            cerr << "Error: Unable to open the input file.\n";
            return;
        }
        for (int i = 0; i < m_size; i++) {
            for (int j = 0; j < m_size; j++) {
                fin >> ws; // Skip whitespace characters, including spaces
                if (!(fin >> m_grid[i][j])) {
                    cerr << "Error: Failed to read integer from file.\n";
                    return;
                }
            }
        }
        fin.close();
    }
	void SaveGrid(const char filename[])
	{
        ofstream fout(filename, ios::out);
        if (!fout)
        {
            cerr << "Error: Unable to open the output file.\n";
            return;
        }
        for (int i = 0; i < m_size; i++) {
            for (int j = 0; j < m_size; j++) {
                fout << m_grid[i][j] << " ";
            }
            fout << endl;
        }
        fout.close();
	}

private:
	static const int m_size = 9;
	T m_grid[m_size][m_size];
};
```
</details>

## Changes
- Moved methods and references from source file to header file.
- Changed the header file class to a Template class.

**Grid.h**
```diff
+ template<class T>
class Grid
{
...
}
```
- Changed the grid variable to use the template properly.

**Main.cpp**
```diff
int main (int, char**) {
- 	Grid grid;
+ 	Grid<int> grid;
	grid.LoadGrid("Grid1.txt");
	grid.SaveGrid("OutGrid.txt");
	return 0;
}
```

**Grid.h**
```diff
private:
	static const int m_size = 9;
-	int m_grid[m_size][m_size];
+	T m_grid[m_size][m_size];
```
</details>

----

<details> <!-- Question 2 -->
  <summary> Q2. Template Grid (Float) </summary>

## Question:
Change the code in `main()` so that you can store `float` values instead of `int` values, i.e. `Grid<float> grid`

Change some of the values in the `Grid1.txt` to floating point values and you should see the output is now correct.
## Solution:
**Main.cpp**
```c++
int main (int, char**)
{
	Grid<float> grid;
	grid.LoadGrid("Grid1.txt");
	grid.SaveGrid("OutGrid.txt");

	return 0;
}
```
**Grid1.txt**
```
1.1 2 3 4 5 6 7 8 9
2 3 4 5 6 7 8 9 1.1
3 4 5 6 7 8 9 1.1 2
4 5 6 7 8 9 1.1 2 3
5 6 7 8 9 1.1 2 3 4
6 7 8 9 1.1 2 3 4 5
7 8 9 1.1 2 3 4 5 6
8 9 1.1 2 3 4 5 6 7
9 1.1 2 3 4 5 6 7 8
```
**OutGrid.txt**
```
1.1 2 3 4 5 6 7 8 9 
2 3 4 5 6 7 8 9 1.1 
3 4 5 6 7 8 9 1.1 2 
4 5 6 7 8 9 1.1 2 3 
5 6 7 8 9 1.1 2 3 4 
6 7 8 9 1.1 2 3 4 5 
7 8 9 1.1 2 3 4 5 6 
8 9 1.1 2 3 4 5 6 7 
9 1.1 2 3 4 5 6 7 8 
```
## Debugger:
![image](https://github.com/TheOtherRealMesteven/Lab-Book/assets/115008465/234b37e6-5c70-4687-9554-05ca3f6b35e2)

</details>

----

<details> <!-- Question 3 -->
  <summary> Q3. Binary Search </summary>

## Question:
In this exercise, you'll implement two versions of a binary search, one using iteration, the other using a recursive function.

The text file `binarysearchIn.txt` contains 100 integers, ordered from small to large.

Create a 100 element 1D array and read the numbers from the file into the array, using the streaming operators.

Implement this process using a recursive function, with the following prototype
```c++
bool binarySearch(int *list, int size, int value);
```
Now create a second implementation, replacing the recursive function with a single while loop

Which implementation do you prefer, in terms of both readability and design intent?
## Solution:
<details>
	<summary>Recursive</summary>

```c++
bool binarySearch(int* list, int size, int value)
{
	if (size == 0) return false;
	int mid = size / 2;
	if (list[mid] == value) return true;
	else if (list[mid] > value) return binarySearch(list, mid, value);
	else return binarySearch(list + mid + 1, size - mid - 1, value);
}
```
</details>
<details>
	<summary>While Loop</summary>

```c++
bool binarySearch(int* list, int size, int value) {
    int left = 0;
    int right = size - 1;

    while (left <= right) {
        int mid = left + size / 2;
        if (list[mid] == value) return true;
        else if (list[mid] < value) left = mid + 1;
        else right = mid - 1;
        size = right - left + 1;
    }
    return false;
}
```
</details>

## Analysis
***Readability:***
- Recursion might be more confusing for people to follow with the self-method calls. However, the overall code is more simplistic and more readable.

***Design Intent:***
- The iterative implementation is more efficient in both storage and performance.
	- This is due to each method in recursion using stack space for storing local variables, function arguments, and the return address.
	- It is especially impactful if the recursive methods iterate excessively.
- The recursive implementation is more maintainable due to its simplicity.

***Conclusion:***

Iteration is probably used more than recursion due to efficiency being a priority over readability. Especially as if code is less readable, it can still eventually be read.
</details>

----
