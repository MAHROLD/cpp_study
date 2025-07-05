
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

