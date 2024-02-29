# Week 4 - Lab D

## Lab Coverage
*For future review, the coverage of each task has been listed below to act as an index to the taught material.*

#### Question 1
- 🤔 Definitions and purpose of header and source files. 
#### Question 2
- 🤔 Ignoring file whitespace (Spaces and EOL's)
- 🤔 Reading integer arrays from a file.
#### Question 3
- 🤔 Further file saving (from Lab C) practices.
#### Question 4
- 🤔 Recap on pointer variable and memory locations (`*p` and `&a`)
#### Question 5
- 🤔 Recap on variable memory locations being different to code.
#### Question 6
#### Question 7

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
  <summary> Q2. Reading into Grid Class </summary>

## Question:
Implement the `Grid::LoadGrid(const char filename[])` method in `Grid.cpp`. This method should follow the following pseudo code.

```
Create an input file stream from filename
for each y value from 0 to 8 inclusive
{
   for each x value from 0 to 8 inclusive
   {
      store next value from the input file stream into grid at x,y
   }
}
Close input file stream
```

## Solution:
```c++
const int SIZE = 9;
const bool DEBUG = false;
int grid[SIZE][SIZE];

void Grid::LoadGrid(const char filename[])
{
    ifstream fin(filename, ios::in);
    if (!fin) {
        cerr << "Error: Unable to open the input file.\n";
        return;
    }
    for (int i = 0; i < SIZE; i++) {
        for (int j = 0; j < SIZE; j++) {
            fin >> ws; // Skip whitespace characters, including spaces
            if (!(fin >> grid[i][j])) {
                cerr << "Error: Failed to read integer from file.\n";
                return;
            }
        }
    }
    fin.close();
    if (!DEBUG) return; // Debug output the grid
    for (int i = 0; i < SIZE; i++)
    {
        for (int j = 0; j < SIZE; j++)
        {
            cout << grid[i][j];
        }
        cout << endl;
    }
}
```
- Using the previous lab as reference, I implemented the file reading system. `ios::in` was selected as we would be handing text file inputs.
- I added a presence check to ensure that the file was there to be loaded and didnt cause a program crash.
- I iterated through the expected size of the 2d array, skipping the whitespace characters and inserting the value into the grid. If the grid was saved incorrectly then an error would be output.

## Test data:
**Input Name:** `Grid1.txt`

**Contents:**
```
1 2 3 4 5 6 7 8 9
2 3 4 5 6 7 8 9 1
3 4 5 6 7 8 9 1 2
4 5 6 7 8 9 1 2 3
5 6 7 8 9 1 2 3 4
6 7 8 9 1 2 3 4 5
7 8 9 1 2 3 4 5 6
8 9 1 2 3 4 5 6 7
9 1 2 3 4 5 6 7 8
```

## Output:
![README-debug1](https://github.com/TheOtherRealMesteven/Lab-Book/assets/115008465/2e4c0015-6443-4e1b-b91e-d073c184cb56)

</details>
<details> <!-- Question 3 -->
  <summary> Q3. Saving the Grid </summary>

## Question:
Implement the SaveGrid(const char filename[]) method. This method will save the values of m_grid in a similar format to that of the Grid1.txt file. Please use another name for the output file so that your Grid1.txt file is not overwritten.
## Solution:
```c++
void Grid::SaveGrid(const char filename[])
{
    ofstream fout(filename, ios::out);
    if (!fout)
    {
        cerr << "Error: Unable to open the output file.\n";
        return;
    }
    for (int i = 0; i < SIZE; i++) {
        for (int j = 0; j < SIZE; j++) {
            fout << grid[i][j] << " ";
        }
        fout << endl;
    }
    fout.close();
    cout << "Grid saved to: " << filename << endl;
}
```
- Using the previous lab as reference, I implemented the file saving system. `ios::out` was selected as we would be handing text file inputs.
- I added a presence check to ensure that the file was there to be loaded and didnt cause a program crash.
- I iterated through the expected size of the 2d array, storing the values followed by a space into the file and creating a new line for when the current grid row was finished.
- **There is a slight discrepancy with the saved file where the new file has a trailing white space on the lines, however the load program handles this.**

## Test data:
**Input Name:** `Grid1.txt`

**Contents:**
```
1 2 3 4 5 6 7 8 9
2 3 4 5 6 7 8 9 1
3 4 5 6 7 8 9 1 2
4 5 6 7 8 9 1 2 3
5 6 7 8 9 1 2 3 4
6 7 8 9 1 2 3 4 5
7 8 9 1 2 3 4 5 6
8 9 1 2 3 4 5 6 7
9 1 2 3 4 5 6 7 8
```
## Sample output:
**Input Name:** `GridOut.txt`

**Contents:**
```
1 2 3 4 5 6 7 8 9 
2 3 4 5 6 7 8 9 1 
3 4 5 6 7 8 9 1 2 
4 5 6 7 8 9 1 2 3 
5 6 7 8 9 1 2 3 4 
6 7 8 9 1 2 3 4 5 
7 8 9 1 2 3 4 5 6 
8 9 1 2 3 4 5 6 7 
9 1 2 3 4 5 6 7 8 
```
**There is a slight discrepancy with the saved file where the new file has a trailing white space on the lines, however the load program handles this.**

</details>
<details> <!-- Question 4 -->
  <summary> Q4. Pointers - Basics </summary>

## Question:
Located the following code in source.cpp file:
```c++
void functionA() {
   int a = 10;
   int b = 20;
   int *p = &a;

   cout << "a= " << a << endl;
   cout << "b= " << b << endl;

   // Add your code here

   cout << "a= " << a << endl;
   cout << "b= " << b << endl;
}
```
Add a line of code, at the position indicated by the comment, to assign the value of `100` to `a`, by using only the pointer `p`.
## Solution:
```c++
void functionA() {
	int a = 10;
	int b = 20;
	int *p = &a;

	cout << "a= " << a << endl;
	cout << "b= " << b << endl;

	// Add your code here
	*p = 100;

	cout << "a= " << a << endl;
	cout << "b= " << b << endl;
}
```
## Output:
![image](https://github.com/TheOtherRealMesteven/Lab-Book/assets/115008465/3eab6a18-da40-4169-b0a1-4e1e8d08be3c)

## Question:
Now set a breakpoint at the line
```c++
int a = 10;
```
Run the code to the breakpoint, then single-step through the code whilst looking at the variables in the Local window.

Notice how `a` and `b` are initialized with values `10` and `20`, and that pointer `p` is assigned a hexadecimal value. This value is the memory location of `a`.

Open a Memory window. Copy the value of `p` into the address field of the Memory window and confirm that you are looking at variable `a` in memory.

## Solution
![image](https://github.com/TheOtherRealMesteven/Lab-Book/assets/115008465/fd22f2a9-13b6-4fce-a4e2-8a37a50704ac)

->

![image](https://github.com/TheOtherRealMesteven/Lab-Book/assets/115008465/73e0481c-5665-4bec-9072-7c35e267d3d8)


From reviewing the changing of the values, it can be confirmed that `p` is being assigned the address field of the variable `a`. This is because `&a` is the memory location of the variable `a` and the value is being passed onto the pointer variable `p` (`*p`).

## Reflection:

</details>
<details> <!-- Question 5 -->
  <summary> Q5. Pointers - False assumptions </summary>

## Question:
Comment out the call to functionA and uncomment the call to functionB.
```c++
void functionB() {
   int a = 10;
   int b = 20;
   int c = 30;
   int *p = &b;

   cout << "a= " << a << endl;
   cout << "b= " << b << endl;
   cout << "c= " << c << endl;

   *p = 100;

   cout << "a= " << a << endl;
   cout << "b= " << b << endl;
   cout << "c= " << c << endl;
} 
```
Compile and run the program.

![image](https://github.com/TheOtherRealMesteven/Lab-Book/assets/115008465/c82922f0-2e86-4eab-8dda-26ffd5a74043)

Now we’ll attempt to do a quick "hack" and advance the pointer 4 bytes in memory from the location of variable `b` to the location of variable `c`

After line
```c++
*p = 100;
```
Add
```c++
p++;
*p = 200;
```
Compile and run the program.

![image](https://github.com/TheOtherRealMesteven/Lab-Book/assets/115008465/fc88dc28-938e-4627-9d8f-d77fa0586432)

![image](https://github.com/TheOtherRealMesteven/Lab-Book/assets/115008465/2f2fad51-9a43-4f44-ad09-864ce6c4e9c0)

Is this what you expected?

- *This is not what the quick hack should have performed if it performed correctly, however it is what was expected as we dont know the precise location of variable c in memory so the change is not necessarily going to point to variable c.*

The pointer does get advanced by 4 bytes, but the memory location is invalid. Just because we list variables a, b, and c sequentially in our programme, does not guarantee that the compiler places them contiguously in memory.

If you want to do this sort of pointer arithmetic then you need to guarantee the memory layout. Arrays are a way to achieve this. We’ll look at these later in the module.

For now, just be careful using pointer arithmetic. This time we were lucky and the C++ run time checking detected the error for us. You cannot rely on the run time finding more complex errors.

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
