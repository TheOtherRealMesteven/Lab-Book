# Week 3 - Lab C

## Lab Coverage
*For future review, the coverage of each task has been listed below to act as an index to the taught material.*

#### Question 1
- 🤔 Visual studio executable inputs
#### Question 2
- 🤔 File reading
- 🤔 File writing
#### Question 3
- 🤔 Debugging movement shortcuts
- 🤔 How to access codes assembly
- 🤔 How to access codes memory and registers
- 🤔 A small amount on the breakdown of assembly

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
Complete the functionality inside of the `Copy(char filenamein[], char filenameout[])` function. You need to add code that will try to open a text file given by the `filenamein` array as the name of the input file. You need to add code to create and output file using the `filenameout` array as the name of the ouput file. Then you can add code that will take each char from the input file and put it in the output file.

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
			while (true)
			{
				fin.read(c, arraySize);
				streamsize size = fin.gcount();
				if (size <= 0) break;
				fout.write(c, size);
			}
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
- If I used `fin.read` as the while loops condition like the last solution, no characters would be copied.
- `fout.write` wouldnt allow me to use an `int` for the size so I had to use `streamsize` which worked.

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
  <summary> Existing Output File Test</summary>

### Test data:
File: `input.txt`

Contents:

![image](https://github.com/TheOtherRealMesteven/Lab-Book/assets/115008465/cf19d043-d766-4899-a8c6-9b31078ac0b6)

File: `output.txt`

Contents:

![image](https://github.com/TheOtherRealMesteven/Lab-Book/assets/115008465/719ccff9-3734-4bb9-88e3-8d5e7fcc8c5c)


### Sample output:
File: `output.txt`

Contents:

![image](https://github.com/TheOtherRealMesteven/Lab-Book/assets/115008465/4a95d79e-017f-4117-88f6-6f51c21c98d1)

**Conclusion: ✅ Successfully Copied**
</details>
<details>
  <summary> Missing File Test</summary>

### Test data:
n/a
### Sample output:
![image](https://github.com/TheOtherRealMesteven/Lab-Book/assets/115008465/714d32ce-9139-412c-aed3-5ab61be3bc14)

**Conclusion: ✅ Expected Behaviour**
</details>
<details>
  <summary> Large File Test</summary>

### Test data:
File: `input.txt`

Contents: [59KB]
```
Bee Movie Script

  
  
According to all known laws
of aviation,
...
```

### Sample output:

File: `output.txt`

Contents: [59KB]
```
Bee Movie Script

  
  
According to all known laws
of aviation,
...
```
**Conclusion: ✅ Successfully Copied**
</details>
<details>
  <summary> Different File Type</summary>

### Test data:
File: `input.webp`
![image](https://github.com/TheOtherRealMesteven/Lab-Book/assets/115008465/64db552b-ca20-4bda-9e42-2dc7e3bc7d51)

### Sample output:
File: `output.webp`

![image](https://github.com/TheOtherRealMesteven/Lab-Book/assets/115008465/c667c824-b293-4863-8694-853130fca1b1)

**Conclusion: ❎ Unsuccessfully Copied**
</details>

## Summary:
|Test|Successful|
|--|--|
|Functional Test|✔|
|Existing Output File Test|✔|
|Missing File Test|✔|
|Large File Test|✔|
|Different File Type|❌|

The created code performs as it should with the initial sample data. And is programmed to withstand multiple scenarios which could occur when duplicating a text file.
However, when it attempts to copy `different file types` the code fails. I believe that is due to the way the files are opened, `ios:in` and `ios:out` are not as versatile as they are needed to be.

Therefore, the code needs to use something universal to copy the data of different file types. For example: Binary, which is the computer holds data universally.

## Final Solution:
```c++
bool Copy(char filenamein[], char filenameout[])
{
	ifstream fin(filenamein, ios::binary);
	if (fin.is_open()) {
		ofstream fout(filenameout, ios::binary);
		if (fout.is_open()) {
			const int arraySize = 4096;
			char c[arraySize];
			while (true)
			{
				fin.read(c, arraySize);
				streamsize size = fin.gcount();
				if (size <= 0) break;
				fout.write(c, size);
			}
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

With the ``ios::binary`` method of opening and writing to files, the data is copied bit by bit and so can be used across file types as far as I am aware.

<details>
  <summary> Different File Type</summary>

### Test data:
File: `input.webp`
![image](https://github.com/TheOtherRealMesteven/Lab-Book/assets/115008465/64db552b-ca20-4bda-9e42-2dc7e3bc7d51)

### Sample output:
File: `output.webp`
![image](https://github.com/TheOtherRealMesteven/Lab-Book/assets/115008465/64db552b-ca20-4bda-9e42-2dc7e3bc7d51)

**Conclusion: ✅ Successfully Copied**
</details>

## Reflection:
- With `ios::in` and `ios::out` what breakdown does it get of the file and so what data types can be copied?

</details>

> [!IMPORTANT]
> For file copying you need the following namespaces `std` and libraries `iostream` and `fstream`.

<details> <!-- Question 3 -->
  <summary> Q3. Assembly, Registers and Memory  </summary>

## Lesson:
<details>
	<summary> View: Code breakdown, Memory, Registers etc . . .</summary>

### Code in Assembly
![image](https://github.com/TheOtherRealMesteven/Lab-Book/assets/115008465/f04ed1b6-8ad3-40f4-abaf-85d84877f914)

![image](https://github.com/TheOtherRealMesteven/Lab-Book/assets/115008465/43ff1083-4daa-4246-b992-cf1e6283b4fb)

### Memory
![image](https://github.com/TheOtherRealMesteven/Lab-Book/assets/115008465/099e3772-4db0-49e1-a675-4b30f7fcfbbe)

![image](https://github.com/TheOtherRealMesteven/Lab-Book/assets/115008465/a9d2c3d9-b290-43bb-9277-e3acebce45b4)

### Registers
![image](https://github.com/TheOtherRealMesteven/Lab-Book/assets/115008465/987d770d-4e73-43e9-80f9-dff090cefc0e)

![image](https://github.com/TheOtherRealMesteven/Lab-Book/assets/115008465/ffb9bf53-0964-4c27-889e-c32b9e5d370c)

</details>

## Question:
```
0x0018FE15  cc cc cc cc cc cc cc cc cc cc cc cc cc  ÌÌÌÌÌÌÌÌÌÌÌÌÌ
0x0018FE22  cc cc cc cc cc cc cc cc cc cc cc cc cc  ÌÌÌÌÌÌÌÌÌÌÌÌÌ
0x0018FE2F  cc 0a 00 00 00 14 00 00 00 00 00 00 00  Ì............
0x0018FE3C  00 00 00 00 00 e0 fd 7e cc cc cc cc cc  .....àý~ÌÌÌÌÌ
0x0018FE49  cc cc cc cc cc cc cc cc cc cc cc cc cc  ÌÌÌÌÌÌÌÌÌÌÌÌÌ
0x0018FE56  cc cc cc cc cc cc cc cc cc cc cc cc cc  ÌÌÌÌÌÌÌÌÌÌÌÌÌ
```

###  Data sizes

**In source.cpp we use variables a and b. How many bytes do each of these variables occupy in memory? Look at the memory dump above; can you verify your answer?**

In the code above, we can see variable `a`'s value of `0a` and variable `b`'s value of `14`. These integers are hexadecimal values and so they can hold a maximum of 32 bits aka 4 bytes. Meaning they hold 4 bytes each of memory.

*Each of the registers we have used so far in this program have been 32-bits in size e.g. EAX. Look at the register window. The values in each register are represented by 8 digits; 2 digits for each byte.*
### Parameter types
**Now modify the code and add in your own function that takes 3 parameters each of a different type.**

**From what you have learnt in the previous exercises, use the Debugger and Disassembly to investigate how the C++ parameter passing mechanism deals with these new parameters.**
## Test data:
```c++
int a [4] = {10, 20, 30, 40};
const char* b = "Cheese";
float c = 3.01f;
```
## Analysis:
### Disassembly
```
	int a [4] = {10, 20, 30, 40};
00007FF64BC166CC  mov         dword ptr [a],0Ah  					// mov (move) // dword ptr (32-bit value) // into the memory location [`a`] // `0A`h (denary:10)
00007FF64BC166D3  mov         dword ptr [rbp+0Ch],14h  					// mov (move) // dword ptr (32-bit value) // into the memory location [`0C`h (denary:12) from the base pointer] // `14`h (denary:20)
00007FF64BC166DA  mov         dword ptr [rbp+10h],1Eh  					// mov (move) // dword ptr (32-bit value) // into the memory location [`10`h (denary:16) from the base pointer] // `1E`h (denary:30)
00007FF64BC166E1  mov         dword ptr [rbp+14h],28h  					// mov (move) // dword ptr (32-bit value) // into the memory location [`14`h (denary:20) from the base pointer] // `28`h (denary:40)
	const char* b = "Cheese";
00007FF64BC166E8  lea         rax,[string "Cheese" (07FF64BC1AC24h)] 			// lea (load) // rax (Register AX) // [string "Cheese" // located at memory address (07FF64BC1AC24h)]
00007FF64BC166EF  mov         qword ptr [b],rax  					// mov (move) // qword ptr (64-bit value) // into the memory location [`b`] // the value held in rax (Memory address 07FF64BC1AC24h)
	float c = 3.01f;
00007FF64BC166F3  movss       xmm0,dword ptr [__real@4040a3d7 (07FF64BC1AC2Ch)]  	// movss (move float?) // into xmmo (Register xmm0) // dword ptr (32-bit value) // [value __real@4040a3d7 // located at memory address (07FF64BC1AC2Ch)]
00007FF64BC166FB  movss       dword ptr [c],xmm0					// movss (move float?) // dword ptr (32-bit value) // into the memory location [`c`] // the value held at xmm0 (The thing above)
```

### Registers
#### Registers (Before assigning parameters)
```
RAX = 0000000000000001 RBX = 0000000000000000 RCX = 00007FF64BC23066 RDX = 00000279E637B0D0 RSI = 0000000000000000 RDI = 000000C9AD76F818 R8  = 00000279E637FAE0 R9  = 000000C9AD76F7E8 R10 = 0000000000000012 R11 = 000000C9AD76F890 R12 = 0000000000000000 R13 = 0000000000000000 R14 = 0000000000000000 R15 = 0000000000000000 RIP = 00007FF64BC166CC RSP = 000000C9AD76F760 RBP = 000000C9AD76F780 EFL = 00000200 

0x000000C9AD76F788 = CCCCCCCC 
```
#### Registers (After assigning parameters)
```
RAX = 00007FF64BC1AC24 RBX = 0000000000000000 RCX = 00007FF64BC23066 RDX = 00000279E637B0D0 RSI = 0000000000000000 RDI = 000000C9AD76F818 R8  = 00000279E637FAE0 R9  = 000000C9AD76F7E8 R10 = 0000000000000012 R11 = 000000C9AD76F890 R12 = 0000000000000000 R13 = 0000000000000000 R14 = 0000000000000000 R15 = 0000000000000000 RIP = 00007FF64BC16700 RSP = 000000C9AD76F760 RBP = 000000C9AD76F780 EFL = 00000202 

0x000000C9AD76F7D4 = 4040A3D7 
```
#### Changes
- RAX - Now contains the memory address of the string "Cheese" so that it can be constant.
- RIP - Memory location of the instruction to be executed next (instruction pointer).
- EFL
- 0x000000C9AD76F7D4

## Reflection:
 - What is movss?
 - Why is the floats value nothing like 3.01f? Is it a temporary value?
 - Is xmm0 a memory location? Or is it an unlisted register?
 - What is EFL?
 - What is 0x000000C9AD76F7D4 used for?
 - Where can I find the stack to follow the trace?
</details>

> [!NOTE]
> Debugging tools:
> `F11` - Execute the current line (If it branches anywhere, follow)
> `F10` - Execute the current line (Then move onto the next in the breakdown)
> `F5` - Continue the code until the next breakpoint / the end
