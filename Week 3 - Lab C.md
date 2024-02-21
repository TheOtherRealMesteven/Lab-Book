# Week 3 - Lab C

## Lab Coverage
*For future review, the coverage of each task has been listed below to act as an index to the taught material.*

#### Question 1
- 🤔 Visual studio executable inputs
#### Question 2
- 🤔 File reading
- 🤔 File writing
#### Question 3
#### Question 4
#### Question 5
#### Question 6

## Lab Task Submission
*The tasks assigned to be reviewed for the weeks lab has been completed below.*

<details> <!-- Question 1 -->
  <summary> Q1. Passing Command Arguments</summary>

## Question:
Passing Command Arguments

**[LAB BOOK - Record the steps required to enter arguments into Visual Studio]**

## Solution:
### Step 1 - Project properties
![image](https://github.com/TheOtherRealMesteven/Lab-Book/assets/115008465/bedfeff8-8ecf-4a94-a429-75753a20a99e)

Defining visual studios input for executing the project is done via the projects properties.

### Step 2 - Debugging
![image](https://github.com/TheOtherRealMesteven/Lab-Book/assets/115008465/207af20b-8b2e-4be9-9a16-799c02dc1acc)

Under `Configuration Properties` select `Debugging`

### Step 3 - Command Arguments
![image](https://github.com/TheOtherRealMesteven/Lab-Book/assets/115008465/d790fbe7-3f16-4a84-964a-de551c2387d4)

Under the `Command Arguments` row, you can supply command arguments seperated by spaces.

## Test data:
Project: File Input Output

Arguments: `input.txt` `output.txt`

![image](https://github.com/TheOtherRealMesteven/Lab-Book/assets/115008465/d790fbe7-3f16-4a84-964a-de551c2387d4)
## Sample output:
![image](https://github.com/TheOtherRealMesteven/Lab-Book/assets/115008465/7365b0ad-163c-41b7-89ac-4644f77284ff)

As you can see the program did not error nor output the Usage prompt. Therefore, there were three total inputs passed through as expected.

## Reflection:
- If you want to pass in a command argument with a space in the name, do you use speech marks to indicate the selection similar to command prompt?

</details>

> [!NOTE]
> `argv[0]` (The first parameter) contains the filepath to the executable running the code.



<details> <!-- Question 2 -->
  <summary> Q2. Copying a Text File </summary>

## Question:
Complete the functionality inside of the `Copy(char filenamein[], char filenameout[])` function. You need to add code that will try to open a text file given by the `filenamein` array as the name of the input file. You need to add code to create and output file using the filenameout array as the name of the ouput file. Then you can add code that will take each char from the input file and put it in the output file.

Make sure that you check for the input and output files existence before trying to copy.

Test your code thoroughly, e.g. try providing filenames that do not exist.

**[LAB BOOK - Add you code to your lab book and reflect on how you tested your code]**

## Solution:
<details>
  <summary> Copied character by character </summary>

```c++
bool Copy(char filenamein[], char filenameout[])
{
	ifstream fin(filenamein, ios::in);
	if (fin.is_open()) {
		ofstream fout(filenameout, ios::out);
		if (fout.is_open()) {
			char c;
			while (fin.get(c)) fout << c; 
			fin.close();
			fout.close();
			return true;
		}
		cout << "Error creating the output file " << filenameout << endl;
		fin.close();
		return false;
	}
	cout << "Input file " << filenamein << " does not exist" << endl;
	return false;
}
```

My first attempt at C++ file copying.
- The characters are copied across individually.

</details>
<details>
  <summary> Copied via array </summary>

```c++
bool Copy(char filenamein[], char filenameout[])
{
	ifstream fin(filenamein, ios::in);
	if (fin.is_open()) {
		ofstream fout(filenameout, ios::out);
		if (fout.is_open()) {
			const int arraySize = 4096;
			char c[arraySize];
			while (fin.read(c, arraySize)) fout.write(c, arraySize); 
			fin.close();
			fout.close();
			return true;
		}
		cout << "Error creating the output file " << filenameout << endl;
		fin.close();
		return false;
	}
	cout << "Input file " << filenamein << " does not exist" << endl;
	return false;
}
```

My second attempt at C++ file copying.
- The characters are copied across using an array allowing strings of characters to be copied across.

</details>

## Testing:

<details>
  <summary> Functional Test </summary>
  
### Test data:
File: `input.txt`

Contents:

![image](https://github.com/TheOtherRealMesteven/Lab-Book/assets/115008465/cf19d043-d766-4899-a8c6-9b31078ac0b6)

### Sample output:
File: `output.txt`

Contents:

![image](https://github.com/TheOtherRealMesteven/Lab-Book/assets/115008465/4a95d79e-017f-4117-88f6-6f51c21c98d1)

**Conclusion: ✅ Successfully Copied**
</details>
<details>
  <summary> Missing File Test</summary>
</details>
<details>
  <summary> Large File Test</summary>
</details>
<details>
  <summary> Different File Type</summary>
</details>

## Summary:

## Reflection:

</details>

> [!IMPORTANT]
> For file copying you need the following namespaces `std` and libraries `iostream` and `fstream`.

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
