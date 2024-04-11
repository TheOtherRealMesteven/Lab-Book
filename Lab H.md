# Week 8 - Lab H

## Lab Coverage
*For future review, the coverage of each task has been listed below to act as an index to the taught material.*
|Question|Learned Stuff|
|--|--|
|**1**| 🤔 Friend classes (Allow classes to access private fields)
| | 🤔 Getters and setters
|**2**| 🤔 Heap memory management
| | 🤔 Adding elements to the end of linked lists
|**3**| 🤔 Searching Linked Lists
| | 🤔 Deleting from Linked Lists
| | 🤔 Outputting Linked Lists

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

### PersonNode.h
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

### PersonNode.h
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
#### Description
The changes to the code above create getters and setters for all the private member variables of the class. Whilst keeping the `m_next` field privatised.
Furthermore, the ``friend class`` allows that class to reference the private members as if referencing them from within the current class.

</details>
</details>

----

<details> <!-- Question 2 -->
  <summary> Q2. AddressBookSLL </summary>

## Question:
The `AddressBookSLL` class is required to have the functionality to allow for manipulation of the `PersonNodes` that are contained within the SLL.  The `AddressBookSLL` class has a head `PersonNode` called `m_head`.  This will point to the first `PersonNode` in the list.

We require the functionality to add a new person’s details into  `AddressBookSLL`.  Therefore implement the functionality of a public member method using the following method prototype:

```c++
void AddPerson(const string& name, int age);
``` 

This `AddPerson()` method should add a new `PersonNode` to the SLL according to the following pseudo code (it is suggested that you draw a diagram of what is happening before you start to implement this code):

1. If the `m_head` pointer is `nullptr` (i.e. the SLL is empty) then assign a new `PersonNode` to the `m_head` pointer using the provided name and age.
2. Otherwise, if the `m_head` pointer is not `nullptr` and the `m_head` pointer has a `m_next` pointer that is `nullptr` (i.e. there is only one element in the SLL) then assign the new `PersonNode` to this `m_next` pointer.
3. Otherwise, navigate through each linked `PersonNode` in the SLL until we find a `PersonNode` that has a `m_next` pointer that is `nullptr`, then assign the new `PersonNode` to this `m_next`. 

To test your code, add the following code to your `main()` method:
```c++
	book.AddPerson("Darren", 21);
	book.AddPerson("Dawn", 42);
	book.AddPerson("Steven", 18);
	book.AddPerson("Sue", 27);
```

We are instantiating a new `PersonNode` on the heap therefore we are required to take care of our own memory management.  Therefore add the following functionality in the AddressBookSLL’s destructor that will delete any memory that has been created in the `AddressBookSLL` and linked `PersonNode`.

```c++
AddressBookSLL::~AddressBookSLL(void)
{
   while (m_head->m_next != nullptr)
   {
      PersonNode* previous = m_head;
      PersonNode* current = m_head;
      while (current->m_next != nullptr)
      {
         previous = current;
         current = current->m_next;
      }
      delete current;
      previous->m_next = nullptr;
   }
   delete m_head;
   m_head = nullptr;
}
```
## Solution:
<details>
	<summary> Code </summary>

### AddressBookSLL.h
```c++
#include "PersonNode.h"

class AddressBookSLL
{
public:
	AddressBookSLL(void);
	~AddressBookSLL(void);

	void AddPerson(const string& name, int age);

private:
	PersonNode* m_head;
};
```

### AddressBookSLL.cpp
```c++
#include "AddressBookSLL.h"

AddressBookSLL::AddressBookSLL(void) : m_head(nullptr)
{
}

AddressBookSLL::~AddressBookSLL(void)
{
    while (m_head -> m_next != nullptr)
    {
        PersonNode* prev = m_head;
        PersonNode* current = m_head;
        while (current -> m_next != nullptr)
        {
            prev = current;
            current = current -> m_next;
        }
        delete current;
        prev -> m_next = nullptr;
    }
    delete m_head;
    m_head = nullptr;
}

void AddressBookSLL::AddPerson(const string& name, int age) 
{
    PersonNode* newPerson = new PersonNode(name, age);
    if (m_head == nullptr) { m_head = newPerson; }
    else 
    {
        PersonNode* current = m_head;
        while (current -> getNext() != nullptr) { current = const_cast<PersonNode*>(current -> getNext()); }
        current -> setNext(newPerson);
    }
}


```
</details>
<details>
	<summary> Changes </summary>

### AddressBookSLL.h
```diff
#include "PersonNode.h"

class AddressBookSLL
{
public:
	AddressBookSLL(void);
	~AddressBookSLL(void);

+	void AddPerson(const string& name, int age);
private:
	PersonNode* m_head;
};

```

### AddressBookSLL.cpp
```diff
#include "AddressBookSLL.h"

AddressBookSLL::AddressBookSLL(void) : m_head(nullptr)
{
}

AddressBookSLL::~AddressBookSLL(void)
{
+    while (m_head -> m_next != nullptr)
+    {
+        PersonNode* prev = m_head;
+        PersonNode* current = m_head;
+        while (current -> m_next != nullptr)
+        {
+            prev = current;
+            current = current -> m_next;
+        }
+        delete current;
+        prev -> m_next = nullptr;
+    }
+    delete m_head;
+    m_head = nullptr;
}

+void AddressBookSLL::AddPerson(const string& name, int age) 
+{
+    PersonNode* newPerson = new PersonNode(name, age);
+    if (m_head == nullptr) { m_head = newPerson; }
+    else 
+    {
+        PersonNode* current = m_head;
+        while (current -> getNext() != nullptr) { current = const_cast<PersonNode*>(current -> getNext()); }
+        current -> setNext(newPerson);
+    }
+}

```
#### Description
The coding task I had to do was implement the functionality of a public member method using the following method prototype:
```c++
void AddPerson(const string& name, int age);
```
So the header file includes the method description whilst the source file contains the code which iterates through a valid list and adds the new person to the end of the list.

</details>
</details>

----

<details> <!-- Question 3 -->
  <summary> Q3. Find, Delete, Output </summary>

## Question:
Add the following functionality to the `AddressBookSLL` class:

1. The ability to find a person from the SLL by using their name:

```c++
const PersonNode* FindPerson(const string& name) const;
```

This method should return the `PersonNode` if the `PersonNode` is found or return `nullptr` if it is not found.

<details>
	<summary> FindPerson </summary>


```c++
const PersonNode* AddressBookSLL::FindPerson(const std::string& name) const
{
    const PersonNode* current = m_head;
    while (current != nullptr)
    {
        if (current -> getName() == name) { return current; }
        current = current -> getNext();
    }
    return nullptr;
}
```
</details>

2. The ability to delete a person from the SLL by using their name:

```c++
bool DeletePerson(const string& name);
```

This method should return `true` if the `PersonNode` was deleted or return `false` if it is not deleted (i.e. not found).

<details>
	<summary> DeletePerson </summary>


```c++
bool AddressBookSLL::DeletePerson(const std::string& name)
{
    PersonNode* current = m_head;
    PersonNode* prev = nullptr;

    while (current != nullptr)
    {
        if (current -> getName() == name)
        { // Delete the node
            if (prev != nullptr) { prev -> setNext(const_cast<PersonNode*>(current -> getNext())); }
            else { m_head = const_cast<PersonNode*>(current -> getNext()); }
            delete current;
            return true;
        }
        prev = current;
        current = const_cast<PersonNode*>(current -> getNext());
    }
    return false;
}
```
</details>

3. The ability to output all of the people’s names and ages that our in the AddressBookSLL to an `ostream`.

<details>
	<summary> OutputAllPeople </summary>

```c++
void AddressBookSLL::OutputAllPeople(std::ostream& outputStream) const
{
    const PersonNode* current = m_head;
    while (current != nullptr)
    {
        outputStream << "Name: " << current -> getName() << ", Age: " << current -> getAge() << std::endl;
        current = current -> getNext();
    }
}
```
</details>

To implement the above methods, the following changes are made:
### AddressBookSLL.h
```diff

#include "PersonNode.h"
+#include <iostream>

class AddressBookSLL
{
public:
	AddressBookSLL(void);
	~AddressBookSLL(void);

	void AddPerson(const string& name, int age);
+       const PersonNode* FindPerson(const std::string& name) const;
+       bool DeletePerson(const std::string& name);
+       void OutputAllPeople(std::ostream& os) const;

private:
	PersonNode* m_head;
};
```

</details>

----
