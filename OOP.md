
- access modifiers:
-public : members can be accessed everywhere
-private : can be accessed by class members of its friends
-protected : can be accessed with using inheritance 

include guards ?
- type of guard used to protect from duplicate declaration of .hpp file 

```C++
#ifndef _guard_
#define _guard_
//header file contents
#endif
```
also there is similar approach for header guards which is
``` cpp
#pragma once
```

#include 
```cpp
#include <> --> includes system header files and lib files

#include "" --> includes local files to the project which copiler also knows
```

- when creating constructors its most common to create them in public section of the class and other access is modifiers used for special cases like deisn patterns to limit instances made from the class like in singlton pattern
- if constructors for obj1 , obj2 , obj3 is called , the destructors for them once out of scope is called in reverse order   obj3 , obj2 ,obj1
- default no args constructor is only generated when no other constructor provided
- to initialize obj members use #constructor_initialization_lists which will initialize members in the order of declaration in class and before constructor body { }
```cpp
class::class(int name) : name{"None"}
{
//constructor body
}
```

- delegating constructor to avoid code duplication and delegated constructor does :
	a- initializes passed parameters using initialization list only
	b- its body is executed before the delegating constructor

- to assign value to default constructor parameters only assignment with "=" can be used not initialization list "{ }"
```cpp
class MyClass {
public:
    MyClass(int x = 10);
};

```

- a copy of an object is made when :
	a- passed / return obj by value
	b- construct obj based on another of the same class

- then either compiler will generate a copy constructor or you can defeine your own one

like this :
```cpp
MyClass(const MyClass& other);
```

|Part|Reason|
|---|---|
|`&` (reference)|Avoids infinite recursion and improves efficiency|
|`const`|Ensures original object isn't modified and allows copying from const|

- you **cannot** use the class name prefix (`Dog::`) inside the **class body** when you're defining a member function — including the **copy constructor**.
- just use Dog() without the prefix

### **Shallow Copy vs Deep Copy in Programming**

Understanding the difference between **shallow copy** and **deep copy** is crucial when working with **objects**, **lists**, or **other compound data structures** like dictionaries or custom classes.

or in simple terms
shallow copies pointer value
deep allocates new pointer and allocates the pointer value to it

| Feature      | Deep Copy Constructor                   | Move Constructor                             |
| ------------ | --------------------------------------- | -------------------------------------------- |
| Purpose      | Make a **true copy** (duplicate)        | **Transfer ownership** of resources          |
| Copies what? | Allocates new memory & copies data      | Just takes over the resource pointer         |
| Performance  | Slower (new allocation + copy)          | Faster (no copying, just pointer move)       |
| Use case     | When you need a full, independent clone | When object is temporary or no longer needed |
| Syntax       | `T(const T& other)`                     | `T(T&& other)`                               |

-deep copy const example:

```cpp
class DeepCopy {
    int* data;

public:
    DeepCopy(int val) {
        data = new int(val);
    }

    // Deep copy constructor
    DeepCopy(const DeepCopy& other) {
        data = new int(*other.data); // Allocate and copy value
    }

    ~DeepCopy() {
        delete data;
    }

    void print() const {
        std::cout << "Value: " << *data << "\n";
    }
};

```

-move const

```cpp
class MoveExample {
    int* data;

public:
    MoveExample(int val) {
        data = new int(val);
    }

    // Move constructor
    MoveExample(MoveExample&& other) noexcept {
        data = other.data;     // Steal the pointer
        other.data = nullptr;  // Leave source in valid state
    }

    ~MoveExample() {
        delete data;
    }

    void print() const {
        if (data)
            std::cout << "Value: " << *data << "\n";
        else
            std::cout << "No data\n";
    }
};

```

- this keyword can be used as pointer to the current object 
  and can only be used inside  #class_scope

- to work with #const obj therough methods make sure to use const keyword with method it self 
```cpp
void get_name() const
{
return name;
}
```

- ### static variables

if defined with in class they can
- be initialized with class definition
- belong to class it self not a copy "obj"
- be referenced using classname :: var


- if you try to use a **non-static member variable** inside a **static method**, the compiler will give you an **error** — because **static methods do not have access to the `this` pointer**, which is required to access non-static members.

### structs vs classes

- members are public by default in structs 
- members are private by default in classes


friend of a class

friendship is not inherited for a to b to c
and not symmetric as if a is friend of b doesnt mean b friend of a

friend of class/fn is done to grant an access to all private members of that class