# Week 4 - Lab D

## Lab Coverage
*For future review, the coverage of each task has been listed below to act as an index to the taught material.*

#### Question 1
- 🤔 Definitions and purpose of header and source files. 
#### Question 2
#### Question 3
#### Question 4
#### Question 5
#### Question 6

## Lab Task Submission
*The tasks assigned to be reviewed for the weeks lab has been completed below.*

<details> <!-- Question 1 -->
  <summary> Q1. Linker Errors </summary>

## Question:
Describe what is required in the `.h` and `.cpp` files of a class so that you can define a constructor or method
## Answer:
- The header files `.h` act as blueprints for the code, containing class declarations, constants and method signatures. This allows the compiler to know the details of classes, constants and methods which are being referenced - without seeing the code behind it - allowing the compiler to know if references are being done properly.

- The source files `.cpp` contain the actual code of the classes and methods declared in the header files. They use header files to reference other source file methods and classes but they contain the code that will actually be executed.

<details>
  <summary> Example </summary>

### Main File
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
### Source File
```c++
#include "Grid.h"
Grid::Grid()
{
}

Grid::~Grid()
{
}

void Grid::LoadGrid(const char filename[])
{
}

void Grid::SaveGrid(const char filename[])
{
}
```
### Header File
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
	int m_grid[9][9];
};
```

</details>

## Reflection:
- Whats the difference between `.h` files and `.hpp` files?
</details>

> [!NOTE]
> `Add -> New Item` creates a `.cpp` file whilst `Add -> New Class` creates both a `.cpp` files and a `.h` file.

> [!IMPORTANT]
> `LNK2019` Errors are caused by the compiler not being able to link files together. This can be caused by missing method declarations in header files or the source files.

> [!NOTE]
> Constructors and Deconstructors dont have to be included in the header file, they can purely be defined in the source files.

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
<details> <!-- Question 6 -->
  <summary> Q6. </summary>

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
<details> <!-- Question 7 -->
  <summary> Q7. </summary>

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
