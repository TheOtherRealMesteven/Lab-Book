# Week 6 - Lab F

## Lab Coverage
*For future review, the coverage of each task has been listed below to act as an index to the taught material.*
|Question|Learned Stuff|
|--|--|
|**1**| 🤔 How to create Template Classes
|**2**| 🤔 Template class used with different datatype
|**3**| 🤔 

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
