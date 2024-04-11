# Week 8 - Lab H

## Lab Coverage
*For future review, the coverage of each task has been listed below to act as an index to the taught material.*
|Question|Learned Stuff|
|--|--|
|**1**| 🤔 Friend classes (Allow classes to access private fields)
| | 🤔 Getters and setters
|**2**| 🤔 

## Lab Task Submission
*The tasks assigned to be reviewed for the weeks lab has been completed below.*

----

<details> <!-- Question 1 -->
  <summary> Q1. PersonNode </summary>

## Question:
We are going to implement an Address Book as a Single Linked List (SLL).

The `PersonNode` class will be instantiated to create nodes for our SLL that will hold the name `m_name` and age `m_age` of each person, and will also hold a pointer to the next `m_next` `PersonNode` in the SLL.

This class already has a constructor that can set a name and age.

Add member methods to `PersonNode` so that the name and age can be changed and returned (setters and getters).

We will be required to set and return the `m_next` pointer to the `AddressBookSLL` class so that we can navigate through the SLL. The `m_next` data member pointer is private, which means that if we add the functionality for `PersonNode` class to return this pointer then it should be returned as a `const` pointer. This will unfortunately mean that we cannot navigate through the SLL very easily. Therefore, on this occasion the use of the keyword `friend` is applicable, especially as these two classes are clearly coupled together and cannot be used without each other. Therefore, inside of the `PersonNode.h` file make the `AddressBookSLL` class a friend of the `PersonNode` class, so that `AddressBookSLL` can access the private data members of `PersonNode`.
## Solution:
<details>
  <summary> Code </summary>

## PersonNode.h
```c++
#include <string>
using namespace std;

class PersonNode
{
	friend class AddressBookSLL; // Allows AddressBookSLL to access private members
public:
	PersonNode(void);
	PersonNode(const string& name, int age);
	~PersonNode(void);

	// Member setters
	void setName(const string& name) { m_name = name; }
	void setAge(int age) { m_age = age; }

	// Member getters
	string getName() const { return m_name; }
	int getAge() const { return m_age; }

private:
	string m_name;
	int m_age;
	PersonNode* m_next;

	// Member setters
	void setNext(PersonNode* next) { m_next = next; }

	// Member getters
	const PersonNode* getNext() const { return m_next; }
};
```
</details>
<details>
  <summary> Changes </summary>

```diff
#include <string>
using namespace std;

class PersonNode
{
+	friend class AddressBookSLL; // Allows AddressBookSLL to access private members
public:
	PersonNode(void);
	PersonNode(const string& name, int age);
	~PersonNode(void);

+	// Member setters
+	void setName(const string& name) { m_name = name; }
+	void setAge(int age) { m_age = age; }
+
+	// Member getters
+	string getName() const { return m_name; }
+	int getAge() const { return m_age; }

private:
	string m_name;
	int m_age;
	PersonNode* m_next;

+	// Member setters
+	void setNext(PersonNode* next) { m_next = next; }
+
+	// Member getters
+	const PersonNode* getNext() const { return m_next; }
};
```
### Description
The changes to the code above create getters and setters for all the private member variables of the class. Whilst keeping the `m_next` field privatised.
Furthermore, the ``friend class`` allows that class to reference the private members as if referencing them from within the current class.

</details>
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
