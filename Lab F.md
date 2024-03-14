# Week 6 - Lab F

## Lab Coverage
*For future review, the coverage of each task has been listed below to act as an index to the taught material.*
|Question|Learned Stuff|
|--|--|
|**1**| 🤔 
|**2**| 🤔 
|**3**| 🤔 

## Lab Task Submission
*The tasks assigned to be reviewed for the weeks lab has been completed below.*

----

<details> <!-- Question 1 -->
  <summary> Q1. Template Class </summary>

## Question:
You are going to turn the Grid class into a template class so that we can store any type of number, e.g. float, int, double, into our 2D grid array.

## Before:
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
## After:
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
