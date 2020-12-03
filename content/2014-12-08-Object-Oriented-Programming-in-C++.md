+++
title = "Object Oriented Programming in C++"
date = 2014-12-08

[taxonomies]
tags = ["Programming", "C++", "OOP"]
categories = ["Notes"]
+++

These notes assume you're familiar with functions, classes, inheritance and
objects. This would be a good read for those taking [INF 332] but a C++ text
book or [this wikibooks article] would be better.
I also use a lot of example code  so that it becomes easy for you (and me later)
to follow along.

<!-- more -->

## Definitions

**Data member**: (attribute) a variable accessible from within the class or
global within the class.

**Member function**: (method) a function in a class.

**Abstract class**: A class containing at least one pure virtual function.

**Getter**: (accessor) a function used to access or get the value held by a
private data member. These variable names often start with `get`.

**Setter**: (modifier) a function used to modify or set the value held by a
private data member. These variable names often start with `set`.

**Struct vs Class**: There are two ways to define a class in C++.
Using class and using struct.
When using class all that is within the braces is private by default unless
otherwise specified.
When using struct all that is within the braces is public unless otherwise
specified.

**this** It's a special pointer used to refer to the current object at the time.
To use it dereference the pointer like so `this -> memFunction()` or
`(*this).memFunction()` to call member functions of the object itself.
In a human analogy it's a pronoun the object can use to refer to itself;
among people this would be "me".

**Base class**: a class from which other classes are derived/inherit from.

**Child class**: a class that was derived from another, that class will then be
its parent class.

**Parent class**: A parent class is the closest class that we derived from to
create the one we are referencing as the child class.
The one right above in the inheritance hierarchy.


## Access Labels

These are private, public and protected.
They are used within classes to set access permissions for the members in that
section of the class.
They are also used for base classes to specify how you want the base class
inherited as shown in the table below.

**public**: This label indicates any members within the 'public' section can be
accessed freely anywhere a declared object is in scope.

**private**: Members defined as private are only accessible within the class
defining them, or friend classes. Usually the domain of member variables and
helper functions.
It's often useful to begin putting functions here and then moving them to the
higher access levels as needed so to reduce complexity.

**protected**: The protected label has a special meaning to inheritance,
protected members are accessible in the class that defines them and in classes
that inherit from that base class, or friends of it.


During inheritance things may change slightly as shown in this table.
How things were in the parent class in terms of access lables may not be so in
the child class.

By type of inheritance I mean:
 - *class childClass: private parentClass* is private inheritance
 - *class childClass: protected parentClass* is protected inheritance
 - *class childClass: public parentClass* is public inheritance


The following table indicates how the attributes are inherited in the three
different types of inheritance:

 type of inheritance  | private                    |     protected           |    public
----------------------|----------------------------|-------------------------|----------------------
Private inheritance   |The member is inaccessible. | The member is private.  | The member is private.
Protected inheritance |The member is inaccessible. | The member is protected | The member is protected
Public inheritance    |The member is inaccessible. | The member is protected | The member is public

*Table copied entirely from the [wikibooks] article*

## Constructors

A constructor is a special member function that is called *whenever* a new
instance of a class is created.
The compiler calls the  constructor *after* the new object has been allocated in
memory, and converts that "raw" memory into a proper, typed object
(typed here means the class becomes a type of the same level with int, string
and so forth).

A constructor is used to assign values to the data members that the creator of
the class choses.
If you don't declare a constructor the compiler will impicitly make one for you.

The constructor is declared much like a normal member function but it:

* Doesn't have a type annotation meaning it doesn't start with the name of a
type such as int or string.
* Has to have the same name as the class.
* Has no return value (Meaning it also has no return statement).

The constructor may or may not have arguments.
A constructor that does not take arguments is called a **default constructor**,
while a constructor that takes argument(s) is a **non-default constructor**.

**Overloading**: This is the ability to create multiple methods of the same name
but with different implementations.
Calls to an overloaded function will run a specific implementation of that
function appropriate to the context of the call, allowing one function call to
perform different tasks depending on context.

So let's rewrite this in a way that combines constructors and contructor
overloading.
Don't focus on what the code in the constructors does since I haven't yet
covered it.
However, take note that the constructors were called depending on the arguments
that the objects passed to them.

```cpp
#include <iostream>
using namespace std;

class employee {

  int emp_num;
  string emp_name;

public:
  employee () { cout << "Default constructor of employee ran." << endl; }

  employee (string name, int num): emp_num (num), emp_name (name) {
    cout << "Employee " << this -> getName()
         <<" created. With number " << this -> getNum()
         << endl;
  }

  employee (int num, string name): emp_num (num), emp_name (name) {
    cout << "Employee " << this -> getName()
         << " created. With number " << this -> getNum()
         << endl;
  }

  string getName() { return emp_name; }
  int getNum() { return emp_num; }
};

int main() {
  employee jack; // It's not "objectName ()" but "objectName". No empty brackets.
  employee mo (123, "Nikki");
  employee jackie ("Jackson", 254);
  return 0;
}

/*
   Output:

   Default constructor of employee ran.
   Employee Nikki created. With number 123
   Employee Jackson created. With number 254
*/
```
> A constructor has the same name as the class, doesn't begin with
> a type annotation and returns nothing.

### Default parameters

It's a good idea to read on the below constructor initialization lists first
then read this before looking at the example code.
Sometimes we may want to have a default value initialised to a data member in
case the creator of an object doesn't give it a value.
In such situations we have default parameters.
In the code below (the one under constructor initialization lists) we see that
the constructor assumes that any phone that hasn't had a parameter passed to it
is a Phablet.
Note that we have applied overloading to the constructor.

### Constructor initalization lists

These are also called *member initialization lists*.
They are used to initialize data members and base classes in the cases of
non-default constructors.

Why do we need constructor initialization lists?

* We save by not having to do an assignment.
* The compiler knows to construct the object with that value in memory.

It would otherwise construct the object in memory and then start assigning
values to it's member functions.
This would lead be bad for performance.

Explained further: the difference between using constructor initialization list
and custom constructors through assignment is run-time speed.
If you have a class with a few large data members, assignment construction
(or constructing by assignment) can create a lot of extra overhead.

Constructors are used to assign values to data members however the
initialization isn't done within the body of constructors; such kind of
initialization would actually be *assignment* and not initialization and would
have the drawbacks stated above.
Keep in mind that data members are initialized in the order they are
*declared*, not the order they appear in the constructor initialisation list.
It is therefore good practice to add the data members to the initializer list
in the same order they're declared.

To quote the wikibook on C++ classes under constructor initialization lists:
*The C++ standard defines that all initialization of data members are done
before entering the body of constructors.
This is the reason why certain types (const types and references) cannot be
assigned to and must be initialized in the constructor initialization list.*

Note: *we didn't assign. The values look like paramters being passed to data
members.*

```cpp
#include <iostream>
using namespace std;

class phones {
  //Much thanks to crazypyro in ##programming freenode irc
  string my_name;
public:
  // A default crazypro argument.
  phones() : my_name( "Phablet" ) {
    cout << "Default name is: " << this -> get_name () << endl;
  }
  phones(string name) : my_name( name ) {
    cout << "Non default name is: " << this -> get_name () << endl;
  }
  string get_name() {return my_name;};
};

int main() {
  phones xiamoi;
  phones samsung ("Samsung");
  return 0;
}

/*
  Output:

  Default name is: Phablet
  Non default name is: Samsung
*/
```

We've overloaded the constructor but used constructor initialization lists
instead of assigning values. We also passed a default parameter "phablet" to
the class phones.

### Destructors

The Destructor is a special function that is invoked AFTER an object has been
destroyed to restore the system to a desired state.
Destructors, like constructors, are declared like any normal member function but
will share the same name as the class and also lack a type annotation and a
return value.
What distinguishes them from constructors is that the destructor's name is
preceded by a "~".
A destructor also can not have arguments and therefore doesn't require brackets
after the destructor name.
It also can't be overloaded.
Destructors are called whenever an object of the class it belongs to is
destroyed.
Destructors are crucial in avoiding resource leaks (by deallocating memory) and
in implementing the [RAII idiom].

Sadly in this section there are some concepts of memory management that you may
not be familiar with.
You can ignore them and just focus on how to declare a destructor but it might
be better if you read this [wikibooks page on memory management in C++].

```cpp
#include <iostream>
using namespace std;

class first {
int random;
public:
  first() {
    cout << "first created." << endl;
  }
  ~first() {
    cout << "first destroyed." << endl;
  }
};

class composition {
first* firstObj;
public:
  composition () {
    firstObj = new first;
    if (firstObj != NULL) {
      cout << "firstObj points to an object of first" << endl;
      }
    cout << "An object of composition has been created." << endl;
  }

  ~composition() {
    delete firstObj;
    cout << "composition destroyed." << endl;
  }
};

int main() {
  composition com;
  return 0;
}

/*
Output:

first created.
firstObj points to an object of first
An object of composition has been created.
first destroyed.
composition destroyed.


With delete firsObj ommited:

first created.
firstObj points to an object of first
An object of composition has been created.
composition destroyed.

*/
```

We created the object firstObj on the heap and therefore had to destroy it in
class composition's destructor (~composition () ).
If the line delete firstObj was ommited that would lead to a memory leak
(memory is held by the program that it shouldn't hold).
You can try it out yourself.

### Static

The static keyword can be used to:
* create permanent storage for local variables in a function
* specify internal linkage
* declare member functions that act like non-member functions
* create a single copy of a data member


**Static member functions**
Member functions or variables declared static are shared between all instances
of an object type.
Meaning that only one copy of the member function or variable exists for any object type

**Member functions callable without an object**
These member functions are callable even without an object.
This means that static member functions can be called without creating instances
of the class. Normally member functions seem to take an implicit *this*
parameter. However, in the case of static member functions this isn't the case,
since they behave as some sort of free (not tied to a class) function.

To initialize an a static data member you initialize it in the scope right
outside of the class and refer to it using double semi colons.
In the below code we see the static data member, citizens::citizenship, being
initialized in line 19.
We use the double colon `::` to show [scope] that is, the level of abstraction
that a part of our program (class, function, variable) belongs to.
In this case citizenship and functions inside citizens are declared in a
different level of abstraction (in class citizens) than where they are being
called in the case of funtions or initialized in the case of data members
(citizenship).

```cpp
#include <iostream>
using namespace std;

class citizens {
  static string citizenship;

public:
  citizens () {
    cout << "New citizen created.";
  }
  static void setCitizenship(string ctzn) {
    citizenship = ctzn;
  }

  static string getCitizenship() {return citizenship;}

};

string citizens::citizenship = ""; // Initalizing citizenship to an empty string.

int main() {
  citizens::setCitizenship ("Kenyan");
  cout << citizens::getCitizenship();
  return 0;
}

/*
  Output:

  Kenyan
*/
```

We are interacting with citizenship without having created a citizen.
Note that the constructor for citizenship never ran or else we would've seen
the output "New citizen created."

**Named constructors**

Named constructors are functions used to create an object of a class without
(directly) using it's constructors.
Going by how we said that static member functions can be called without
belonging to an object it means we can use static member functions to make a
call to a named constructor.
This can be translated to manually calling the constructor.
Consequently, we chose the contructor we want to call.

Other reasons we may want to use named constructors:
* to circumvent the restriction that constructors can be overloaded only if
their signatures differ.
* making the class non-inheritable by making the constructors private.
* preventing stack allocation by making constructors private

In the code below we're taking different doubles but we are passing them
differently to the constructor of the class `Temperature`.
If this was part of an API it would give the programmer more freedom since the
internal representation of temparature would be the same but they can think of
temperature in the way they are most comfortable.

```cpp
#include <iostream>
using namespace std;

class Temperature
{
    public:
        //these static functions return a temporary object of type Temperature
        static Temperature Fahrenheit (double f);
        static Temperature Celsius (double c);
        static Temperature Kelvin (double k);
        //A static member function can't refer to non-static data.
        double getTemperature() { return _temp; }
    private:
        Temperature (double temp); //Constructor is private.
        double _temp;
};

//_temp instantiated outside of Temparature class.
Temperature::Temperature (double temp):_temp (temp) {}

Temperature Temperature::Fahrenheit (double f)
{ return Temperature ((f + 459.67) / 1.8); }

Temperature Temperature::Celsius (double c)
{ return Temperature (c + 273.15); }

Temperature Temperature::Kelvin (double k)
{ return Temperature (k); }

int main() {
  // We are initializing the objects created here via kelvin(), celsius() and fahrenheit()
  // to objects
  // kelvin, celsius and fahrenheit.
  Temperature kelvin = Temperature::Kelvin (300.0);
  Temperature celsius = Temperature::Celsius (26.85);
  Temperature fahrenheit = Temperature::Fahrenheit(80.33);

  cout << "Entered kelvin " << kelvin.getTemperature () << endl;
  cout << "Entered celsius " << celsius.getTemperature () << endl;
  cout << "Entered fahrenheit " << fahrenheit.getTemperature () << endl;

  return 0;
}

/*
Output:

Entered kelvin 300
Entered celsius 300
Entered fahrenheit 300
*/
```

One cannot define a static function ( or a member function) that refers to
non-static data.
We are initializing the objects created here via functions Kelvin(), Celsius()
and Fahrenheit() to objects kelvin, celsius and fahrenheit so these objects will
be created holding these objects.
The static functions in this code example return a temporary object of type
Temperature each.

### Composition

A composition is a class which has at least one of it's data members being an
object of another class.
For example below the class composition is a composition.

```cpp
#include <iostream>
using namespace std;

class bird {
  string species;

public:
  bird () {
    cout << "New bird created." << endl;
  }
  void setSpecies (string sp) {
    species = sp;
  }
  string getSpecies () {
    return species;
  }
};

class composition {
  bird chicken;
};

int main() {
  composition newComposition;
  return 0;
}

/*
  Output:

  New bird created.
*/
```

### Inheritance

So inheritance is a rather huge topic for me to explain here.
It's best you read it elsewhere.
I shall just explain how to do inheritance in C++.
Multiple inheritance to be specific.
In the below case we shall have 3 classes
 * two base classes
   - baseClassA
   - baseClassB;
 * one child class that will inherit from both classes
   - childClass.

We shall see the use of constructor initialization lists with multiple
inheritance and regarding constructors of parent classes.

```cpp
#include <iostream>
using namespace std;

class baseClassA {
  string aString;
public:
  baseClassA (string aStr): aString(aStr) {
    cout << "Base class A object created." << endl;
  }
};

class baseClassB {
  int bInt;
public:
  baseClassB (int bin): bInt(bin) {
    cout << "Base class B object created" << endl;
  }
};

class childClass: public baseClassA, public baseClassB {
  bool cBool;
public:
  childClass(bool bul, string aStr, int bIn): cBool(bul), baseClassA(aStr), baseClassB (bIn) {
    cout << "Child class of multiple inheritance object created." << endl;
  }
};

int main() {
  childClass kid (true, "cats", 3);
  return 0;
}

/*
  Output:

  Base class A object created.
  Base class B object created
  Child class of multiple inheritance object created.
*/
```

### Dynamic Polymorphism
It would do you better to read this [Dynamic polymorphism] but since I already
read it I'll just give you the part that I feel is most relevant.

Suppose that we have two classes, A and B. B derives from A and redefines the
implementation of a method c() that resides in class A.
Now suppose that we have an object b of class B. How should the instruction
b.c() be interpreted?

If b is declared in the stack (not declared as a pointer or a reference) the
compiler applies **static binding**, this means it interprets (at compile time)
that we refer to the implementation of c() that resides in B.

However, if we declare b as a pointer or a reference of class A, the compiler
could not know which method to call at compile time, because b can be of type
A or B.
If this is resolved at run time, the method that resides in B will be called.
This is called **dynamic binding**. If this is resolved at compile time, the
method that resides in A will be called. This is again, **static binding**.


### Virtual Member Funtions
Virtual member functions are member functions, that can be overridden in any
class derived from the one where they were declared.
Sort of like you can "overwrite" the funtion in the derived class.
This is done by placing the keyword virtual before the method declaration.
For example

```cpp
virtual memberFunc() {
    /*Member function code*/
}
```

The point is that when the compiler has to decide between applying static
binding or dynamic binding it will apply dynamic binding. Otherwise, static
binding will be applied.
If the base class function is virtual all subclass overrides of it will also be
virtual.
However it is still good practice to add the virtual keyword before function
definitions in subclasses, clarity and all.

In this case assume we were simulating marketing companies in the world so.
The new one will redefine marketing. (There's a mutifaceted joke here btw :'-D )

```cpp
#include <iostream>
using namespace std;

class oldCompany {
public:
  virtual void marketing () {
    cout << "How old company does marketing." << endl;
  }
};

class newCompany: public oldCompany {
public:
  virtual void marketing () {
    cout << "Redefing marketing :D" << endl;
  }
};


int main() {
  newCompany newish;
  oldCompany oldish;
  oldish.marketing ();
  newish.marketing();
  return 0;
}

/*
  Output:

  How old company does marketing.
  Redefing marketing :D
*/
```

#### Pure Virtual Member Functions

Sometimes we don't want to provide an implementation of our function at all,
but want to **force** people sub-classing our class to provide an implementation
on their own.

To create a pure virtual function:


* Include the keyword "virtual" before the "void" type annotation for the pure virtual member function.
* Don't write the function code (not even the braces {} however, just add '= 0' after function declaration.

For example: *virtual void pureFunc() = 0;*

In the code below the pure virtual function "divorce ()" makes "person" an abstact class.
This way anyone deriving from class person will have to implement *divorce ()* or their code won't compile.
Assumption: This is by assumption that a person without a gender can't undergo divorce.
If that is offensive to anyone I'm sorry and I believe anyone should be able to marry anyone and divorce them if they want.

```cpp
#include <iostream>

using namespace std;

class person {
  string names, spouse, gender;
public:
  person (string nm): names (nm) {
    // To demonstrate that the parent object is called before the child object.
    cout << "New person created. " ;
  }

  //pure virtual function "divorce ()" makes "person" an abstact class
  virtual void divorce () = 0;

  string getGender() {return gender;}

  void resetSpouse() {spouse.clear();}

  string getSpouse() {return spouse;}
};

class man: public person {
  string manGen;
public:
  man (string name): manGen ("Male"), person(name) {
    cout << "Male added." << endl;
  }
  void divorce() {resetSpouse ();}
};

class trans: public person {
string transGen;
public:
  trans (string name): transGen ("Trans"), person(name) {
    cout << "Trans added." << endl;
  }
  void divorce() {resetSpouse ();}
};

class woman: public person {
  string womanGen;
public:
  woman (string name): womanGen ("Female"), person(name) {
    cout << "Female added." << endl;
  }
  void divorce () {resetSpouse ();}

};

int main () {
  woman jane ("Jane");
  man notJane ("Jack");
  trans notJack ("Unicorn");
    return 0;
}

/*
Output:

New person created. Male added.
New person created. Male added.
New person created. Trans added.
*/
```

## References
Basically every link here is a reference but the main ones are:
 - [1] Wikibooks classes: [Wikibooks]
 - [2] Wikibooks memory management in C++: [wikibooks page on memory management in C++]

Hail Stallman and may the FOSS be with you.

[Wikipedia]: https://en.m.wikipedia.org/wiki/Function_overloading
[Dynamic polymorphism]: https://en.wikibooks.org/wiki/C%2B%2B_Programming/Classes#Dynamic_polymorphism_.28Overrides.29
[table]: https://en.wikibooks.org/wiki/C%2B%2B_Programming/Classes#Inheritance_.28Derivation.29
[Wikibooks]: https://en.wikibooks.org/wiki/C%2B%2B_Programming/Classes
[this wikibooks article]: https://en.wikibooks.org/wiki/C%2B%2B_Programming/Classes
[RAII idiom]: https://en.wikipedia.org/wiki/Resource_Acquisition_Is_Initialization
[wikibooks page on memory management in C++]: https://en.wikibooks.org/wiki/C%2B%2B_Programming/Memory_Management
[INF 332]: http://www.mu.ac.ke/informationscience/index.php/academic-prorammes/bachelor-programmes/bachelor-of-science-in-informatics#second-semester
