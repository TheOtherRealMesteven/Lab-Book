# Week 7 - Lab G

## Lab Coverage
*For future review, the coverage of each task has been listed below to act as an index to the taught material.*
|Question|Learned Stuff|
|--|--|
|**1**| 🤔 How to install Parasoft
| | 🤔 How to install the Parasoft test rule set
|**2**| 🤔 How to use Parasoft for testing

## Lab Task Submission
*The tasks assigned to be reviewed for the weeks lab has been completed below.*

----

<details> <!-- Question 1 -->
  <summary> Q1. Parasoft </summary>

<details>
  <summary> Installation </summary>

### Installing Parasoft C/C++ Test

This section is not required if running Parasoft in any CS Lab.

Follow the instructions on [Canvas - 500083](https://canvas.hull.ac.uk/courses/69663/files/5257139?module_item_id=1102569)  

### Installing Parasoft C++ Test Rule Set

Follow the instructions on [Canvas - 500083](https://canvas.hull.ac.uk/courses/69663/files/5257139?module_item_id=1102569)  

### Using Parasoft C/C++ Test

**To run Parasoft when not in a CS Lab you'll need to connect to the University VPN (see [Canvas - CS General](https://canvas.hull.ac.uk/courses/17835/pages/setting-up-your-pc)) so that Parasoft is able to contact its license server.**

Follow the instructions on [Canvas - 500083](https://canvas.hull.ac.uk/courses/69663/files/5257139?module_item_id=1102569)
</details>

### Parasoft Screenshots
![image](https://github.com/TheOtherRealMesteven/Lab-Book/assets/115008465/66608031-aaa5-449c-8043-d60815c45f0b)

![image](https://github.com/TheOtherRealMesteven/Lab-Book/assets/115008465/b4012b61-11e7-4c74-952c-425261043376)

![image](https://github.com/TheOtherRealMesteven/Lab-Book/assets/115008465/c46ef1ce-9ff8-42f3-a2ca-a51c38ddee96)

![image](https://github.com/TheOtherRealMesteven/Lab-Book/assets/115008465/dc4849e0-de7c-48f1-acad-8f2242d5df5d)


</details>

----

<details> <!-- Question 2 -->
  <summary> Q2. Testing with Parasoft </summary>

### Errors to fix
![image](https://github.com/TheOtherRealMesteven/Lab-Book/assets/115008465/8d2d9a5b-c555-46a5-af2d-eda5d3ed0981)

<details>
  <summary>[Severity 1] Declare a copy constructor</summary>

### Brief
The copy constructor is used to copy the classes details from one instance to a new instance of the class and this method is usually handled by the compiler.
### Changes
#### Errors
![image](https://github.com/TheOtherRealMesteven/Lab-Book/assets/115008465/7f2d89a8-f671-415a-ae31-3bd4dceb635c)
⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇
![image](https://github.com/TheOtherRealMesteven/Lab-Book/assets/115008465/d44a9d76-300a-41d4-a904-33b1a0160980)

#### Code
**Utility.h**
```diff
#pragma once
class Utility
{
public:
	Utility(void);
	~Utility(void);

+	Utility(const Utility& other); // Copy Constructor
	void SetSize(const int size);
	...
```
**Utility.cpp**
```c++
// Copy Constructor
Utility::Utility(const Utility& other) : m_numberArray(nullptr), m_size(other.m_size)
{
	if (!other.m_numberArray) return;
	m_numberArray = new int[m_size];
	for (int i = 0; i < m_size; i++) m_numberArray[i] = other.m_numberArray[i];
}
```

</details>
<details>
  <summary>[Severity 1] Declare a copy assignment operator</summary>

We are going to fix the first Severity 1 rule violation in `Utility.h` that Parasoft displays `A class 'Utility' must declare a copy assignment operator`

1. Go to the line of code (line 6 of `Utility.h`); this can be done by double-clicking on the violation.
2. Change this line appropriately.
3. Re-run Parasoft on the whole project, and you should see that there are now 10 violations, as we have now fixed the one on line 6.
   
### Brief
The copy assignment operator is used to copy the contents from one instance to another and this method is usually handled by the compiler.
### Changes
#### Errors
![image](https://github.com/TheOtherRealMesteven/Lab-Book/assets/115008465/d44a9d76-300a-41d4-a904-33b1a0160980)
⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇
![image](https://github.com/TheOtherRealMesteven/Lab-Book/assets/115008465/64120513-6821-4bc5-bed2-888acda3fe92)


#### Code
**Utility.h**
```diff
#pragma once
class Utility
{
public:
	Utility(void);
	~Utility(void);

	Utility(const Utility& other); // Copy Constructor
+	Utility& operator = (const Utility& other); // Copy Assignment Operator

	void SetSize(const int size);
	...
```
**Utility.cpp**
```c++
// Copy Assignment Operator
Utility& Utility::operator=(const Utility& other)
{
	if (this != &other)
	{
		delete[] m_numberArray;
		m_size = other.m_size;
		m_numberArray = new int[m_size];
		for (int i = 0; i < m_size; i++) m_numberArray[i] = other.m_numberArray[i];
	}
	return *this;
}
```

</details>

<details>
  <summary>[Severity 3] Void Parameters</summary>

### Brief
Void represents nothing in the programming language. And by leaving the parameters blank, it is implied that there are no parameters.
### Changes
#### Errors
![image](https://github.com/TheOtherRealMesteven/Lab-Book/assets/115008465/64120513-6821-4bc5-bed2-888acda3fe92)
⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇
![image](https://github.com/TheOtherRealMesteven/Lab-Book/assets/115008465/b25f7b48-3b19-4ec4-8848-b679f1247d91)


#### Code
**Utility.h**
```diff
-	Utility(void);
-	~Utility(void);
+	Utility();
+	~Utility();
```
**Utility.cpp**
```diff
-Utility::Utility(void) : m_numberArray(nullptr), m_size(0)
+Utility::Utility() : m_numberArray(nullptr), m_size(0)
{
}

-Utility::~Utility(void)
+Utility::~Utility() 
```

</details>

<details>
  <summary>[Severity 3] Declare Unity class as final</summary>

### Brief
By defining the class as final, it prevents users from inheriting from the class and misusing it.
### Changes
#### Errors
![image](https://github.com/TheOtherRealMesteven/Lab-Book/assets/115008465/b25f7b48-3b19-4ec4-8848-b679f1247d91)
⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇
![image](https://github.com/TheOtherRealMesteven/Lab-Book/assets/115008465/344cefaa-b0e8-4488-aa0d-2a7855d0f426)



#### Code
**Utility.h**
```diff
#pragma once
-class Utility
+class Utility final
{
```
</details>

</details>

----

