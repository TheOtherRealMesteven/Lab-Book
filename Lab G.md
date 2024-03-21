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
  <summary>[Severity 1] Declare a copy assignment operator</summary>

We are going to fix the first Severity 1 rule violation in `Utility.h` that Parasoft displays `A class 'Utility' must declare a copy assignment operator`

1. Go to the line of code (line 6 of `Utility.h`); this can be done by double-clicking on the violation.
2. Change this line appropriately.
3. Re-run Parasoft on the whole project, and you should see that there are now 10 violations, as we have now fixed the one on line 6.

### Brief
Normally, the copy constructor and copy assignment operator features are handled by the compiler. But, they have been flagged by Parasoft as it could be used incorrectly and therefore, it is preferable for the programmers to define it themselves.

*Due to the two features not being used, it is easier to delete them so they have no functionality rather than implement it and waste time.*
### Changes
#### Errors
![image](https://github.com/TheOtherRealMesteven/Lab-Book/assets/115008465/7f2d89a8-f671-415a-ae31-3bd4dceb635c)
⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇
![image](https://github.com/TheOtherRealMesteven/Lab-Book/assets/115008465/a79dc386-7d32-4ed5-9102-e62b814f11e3)

#### Code
**Utility.h**
```diff
#pragma once
class Utility
{
public:
	Utility(void);
-	~Utility(void);
+	~Utility(void) = delete;
	void SetSize(const int size);
	void Process() const;
	int Mult(int a, int b) const;

private:
	int *m_numberArray;
	int m_size;
};
```

</details>

<details>
  <summary>[Severity 3] Void Parameters</summary>

### Brief
Void represents nothing in the programming language. And by leaving the parameters blank, it is implied that there are no parameters.
### Changes
#### Errors
![image](https://github.com/TheOtherRealMesteven/Lab-Book/assets/115008465/500b63c3-0757-4bcd-9283-e949759878ca)
⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇
![image](https://github.com/TheOtherRealMesteven/Lab-Book/assets/115008465/a3c7ba2b-6392-4dcf-8957-b71b65fbbde4)

#### Code
**Utility.h**
```diff
-	Utility(void);
-	~Utility(void) = delete;
+	Utility();
+	~Utility() = delete;
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
![image](https://github.com/TheOtherRealMesteven/Lab-Book/assets/115008465/a3c7ba2b-6392-4dcf-8957-b71b65fbbde4)
⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇
![image](https://github.com/TheOtherRealMesteven/Lab-Book/assets/115008465/8270af61-070f-45f9-adc7-4471060e6522)


#### Code
**Utility.h**
```diff
#pragma once
-class Utility
+class Utility final
{
```
</details>
<details>
  <summary>[Severity 3] Declare assignment operator and copy constructor</summary>

### Brief
Normally, the copy constructor and copy assignment operator features are handled by the compiler. But, they have been flagged by Parasoft as it could be used incorrectly and therefore, it is preferable for the programmers to define it themselves.

*Due to the two features not being used, it is easier to delete them so they have no functionality rather than implement it and waste time.*
### Changes
#### Errors
![image](https://github.com/TheOtherRealMesteven/Lab-Book/assets/115008465/8270af61-070f-45f9-adc7-4471060e6522)
⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇⬇
![image](https://github.com/TheOtherRealMesteven/Lab-Book/assets/115008465/7365a2e8-fdac-48fe-b789-b510acdabd33)


#### Code
**Utility.h**
```diff
#pragma once
class Utility final
{
public:
	Utility();
	~Utility() = delete;
+	Utility(const Utility&) = delete;		// Delete the copy constructor
+	Utility& operator=(const Utility&) = delete;	// Delete the copy assignment operator
	void SetSize(const int size);
	void Process() const;
	int Mult(int a, int b) const;

private:
	int *m_numberArray;
	int m_size;
};
```
</details>

</details>

----

