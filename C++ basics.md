# C++ Basics

## Resources
1. https://youtu.be/8jLOx1hD3_o : 06:42
2. https://youtu.be/GQp1zzTwrIg : 09:34
    - 08:40:04 - Introduction to pointers
    - 08:51:14 - Void pointers
    - 09:06:27 - Pointers and arrays
    - 09:19:18 - Return multiple values from a function using pointers
    - 09:34:50 - Dynamic arrays, create/change arrays at runtime
    - 09:48:35 - Multidimensional dynamic arrays, Two-dimensional array
    - 10:07:00 - Detecting errors in code using PVS Studio
    - 10:17:19 - Explaining Memory Leaks
    - 10:26:25 - Bloopers

## How to run C++ code?
- C++ code is written a a file with the `.cpp` extension.
- To run C++ code it needs to be compiled into an executable. For this there are many compilers the most popular of which is the `g++` compiler which is part of the `gcc` (GNU Compiler Collection).
- We are using `g++-10` for practice. There is also a `clang` compiler which we'll use later on.

## C++ Standards
- There are different versions of the C++ standard. In our case we are using c++20.
- The latest C++ standard as of Nov 2022 is c++20 and c++23 is in progress.

## Core vs Standard Library vs STL
- Core features/language of C++ is the basic syntax rules and data types that form the base of the entire language.
- Standard library provides specialized features that can be included using header files.
- These standard library features are widely used and are thus made readily available but they are not part of the core language.
- STL is part of the standard library. It includes additional data types/containers.
- STL also has algorithms that work with these containers.

## Basic Structure of a C++ Program
```cpp
#include <iostream>

int main() {
    std::cout << "Hello World!" << std::endl;
    return 0;
}
```
- Lines starting with `#` are called _directives_. They are handled by a pre-processor while compiling.
- `#include` is the directive used to include header files (libraries) in the program. There are many in-built and third-party libraries which provide additional functionality.
- `iostream` is a standard header file which contains the input-output functions.
- Program execution starts from the `main` function.
- `std::cout` and `std::endl` - these statements make use of the `cout` and `endl` functions from the `iostream` header file. We use the _scope operator_ `::` to specify that these functions are part of the `std` _namespace_.
- `return 0` - we return 0 from the `main` function. This is because it's return type is `int` and 0 is usually used to indicate successful execution.

## Comments
- Single line comments are started using double forward slash (`//`).
- Multi line comments are written between slash star (`/*`) and star slash (`*/`).
```cpp
#include <iostream>

// entry point of the program
int main() {
    /*
        Function to print "Hello World!"
    */
    std::cout << "Hello World!" << std::endl;
    return 0;
}
```

## Functions
- A function is a block of code that performs a task. It can take inputs and it may produce an output.
- Functions can be reused multiple times.
- A function needs to be declared before it is called/invoked.
- The function declaration contains the return type, function name and datatypes of parameters for the function.
- The function definition defines the parameter names and statements. The function declaration can be inferred from the function defintion.
- Syntax of function definition
```cpp
return_type functionName(type parameter_1, type parameter_2, ..., type parameter_N) {
    // statements
    return;
}
```
- Syntax of function call
```cpp
functionName(input_1, input_2, ..., input_N);
```
- Function declaration and definition can be written separately. In this case, the declaration is refered to as a function prototype. The function can also be called before it has been defined if it has been prototyped.
- Example
```cpp
void hello(std::string);  // declaration or function prototype

int main() {
    hello("human");  // call/invocation
    return 0;
}

// definition
void hello(std::string name) {
    std::cout << "hello " << name;
}
```

### Function Overloading
- Function overloading is a feature of object-oriented programming. It enables the creation of multiple functions with the same name but with different function signatures.
- The function signature is the parts of the function that the compiler uses for overload resolution, i.e., to figure out which function to call when multiple functions have the same name.
- For a non-member function the function signature contains the name and the list of parameter types. Thus functions can be overloaded by changing either the datatypes of the parameters or the number of parameters.
- Note that the return type is not part of the function signature for regular non-member functions.
- Example:
```cpp
void divide(int dividend, int divisor) {
    int remainder {dividend%divisor};
    std::cout << "quotient: " << dividend/divisor << std::endl;
    if (remainder > 0) {
        std::cout << "remainder: " << remainder << std::endl;
    }
}

void divide(double dividend, double divisor) {
    std::cout << "quotient: " << dividend/divisor << std::endl;
}
```
- Function overloading is useful when the function needs to handle different parameter lists in different ways.

## Input and Output
- The header file `iostream` contains definitions for input-output functions.
- The `iostream` input-output functions are:
    - `cout`: prints data to the console.
    - `cin`: reads data from the console.
    - `cerr`: prints errors to the console.
    - `clog`: prints log messages to the console.
- Example:
```cpp
#include <iostream>
#include <string>

int main() {
    std::string name;
    int age;

    std::cout << "Enter your name: ";
    std::cin >> name;

    std::cout << "Enter your age: ";
    std::cin >> age;

    std::cout << "Hello " << name << "!" << std::endl;
    std::cout << "You are " << age << " years old." << std::endl;

    return 0;
}
```
- We can also use `cin` to take multiple inputs. The inputs will be separated by whitespaces.
```cpp
std::cin >> name >> age;
```
- Since `cin` doesn't treat whitespaces as regular text we need a different method to input data which includes whitespaces. In the following example, we can see how to do this for inputs of type `char` and `string`.
```cpp
std::string name;
char dob[11];

std::getline(std::cin >> std::ws, name);
std::cin >> std::ws;
std::cin.getline(dob, 11);
```
- Input/Output manipulation: https://en.cppreference.com/w/cpp/io/manip

## Binary, Octal and Hemadecimal
- We can represent numbers using different number systems.
- Example of storing 17<sub>10</sub> using diffrent number systems:
```cpp
int binary_num = 0b10001;
int octal_num = 021;
int hexadecimal_num = 0x11;
```

## Variables
- Variables are named pieces of memory that are used to store data.
- Variables can be declared, initialized and assigned to.
- Variable declaration just creates a named area in memory. If the variable is not initialized then it will contain garbage data.
- Variable initialization is when the initial value is assigned to the variable. Declaration and initailization can be done together or separately.
- When a value is stored in the variable it is called assignment.

## Initialization Operators
<!-- TODO: understand the use and functioning of intialization operators. -->
- There are different types of intialization operators:
    - Assignment Operator: `=`
    - Braced Assignment Operator: `{}`
    - Functional Assignment Operator: `()`

## Primitive Datatypes
- These are the built-in or predefined datatypes.

### `int`
- Stores integer numbers.
- Usually occupies 2 bytes or more in memory.
- Modifiers:
    - `signed`/`unsigned`: `int` is `signed` by default. `unsigned int` can only store positive integers.
    - `short`: decreases the size of int. Thus it also decreases the range of values that can be stored.
    - `long`: increases the size of int. Thus it also increases the range of values that can be stored.
- `sizeof()` can be used to get the size of a datatype or variable in bytes.
- Calculating range:
    1. for `signed int`: $-(2^{n-1})$ to $2^{n-1} - 1$
    2. for `unsigned int`: $0$ to $2^n - 1$
    - in `signed int` the power is $n-1$ because 1 bit is used to indicate the sign.
    - in `unsigned int` min range is always zero because it is unsigned and thus there are no negative integers.
    - We subtract $1$ from max range because of $0$.
    - **NOTE:** $n$ is size in bits.
- Table of sizes and ranges for `int`:

| modifiers and datatypes | bytes | range |
| :----: | :----: | :----: |
|`short int`|2|-32768 to 32767|
|`unsigned short int`|2|0 to 65535|
|`int`|4|-2147483648 to 2147483647|
|`unsigned int`|4|0 to 4294967295|
|`long int`|8|-9223372036854775808 to 9223372036854775807|
|`unsigned long int`|8|0 to 18446744073709551616|
|`long long int`|8|-9223372036854775808 to 9223372036854775808|
|`unsigned long long int`|8|0 to 18446744073709551616|
- **NOTE:** The above values are for the `g++-10` compiler.

### Floating Point Types
- Store fractional/floating point numbers.
- Datatypes

| modifiers and datatypes | bytes | precision |
| :----: | :----: | :----: |
|`float`|4|7|
|`double`|8|15|
|`long double`|12|>= `double`|

| modifiers and datatypes | bytes | precision |
| :----: | :----: | :----: |
|`float`|4|7|
|`double`|8|16|
|`long double`|16|19|
- **NOTE:** The above values are for the `g++-10` compiler.

- _Precision_ is total number of digits that the datatype can represent, including digits before and after the floating/decimal point (mantissa).
- A few things unique to floating point types:
    1. division by zero
    ```cpp
    std::cout << 1.23/0 << std::endl; // Infinity (+/-)
    ```
    2. zero divided by zero
    ```cpp
    std::cout << 0.0 / 0.0 << std::endl;  // NaN (Not a Number)
    ```
- C++ assumes that all decimal numbers are of type `double`. To ensure proper interpretation of decimal numbers we need to utilize suffixes. Use the `f` suffix for `float` and the `L` suffix for `long double`.
```cpp
float float_pi{3.141592653589793238462643383279f};
double double_pi{3.141592653589793238462643383279};
long double long_double_pi{3.141592653589793238462643383279L};
```

#### Scientific Notation
- Scientific notation is used to represent very large or very small numbers in a simpler way. It is a way of writing only the most significant digits of the number.
- Examples:
    1. 123456789 can be written as 1.23456789 * 10<sup>8</sup>
    2. 0.000001678268 can be written as 1.678268 * 10<sup>-6</sup>
- Syntax of scientific notation
```cpp
double number1{1.23456e8};
double number2{1.67826e-6};
```

### `bool`
- The boolean datatype can store 2 values - `true` or `false`.
- The size of `bool` is 1 byte.
- Example:
```cpp
bool bool_var_1{true};
bool bool_var_2{false};

std::cout << bool_var_1 << std::endl;  // 1
std::cout << bool_var_2 << std::endl;  // 0

std::cout << std::boolalpha;
std::cout << bool_var_1 << std::endl;  // true
std::cout << bool_var_2 << std::endl;  // false
```

### `char`
- The character datatype can store single characters.
- The size of `char` is 1 byte. Thus it can store positive integers form 0 to 255, i.e., 256 characters.
- It uses the ASCII standard to represent characters.
- Character should be enclosed in single-quotes (`'`).
- Example:
```cpp
char char_var_1{'a'};
char char_var_2{65};

std::cout << char_var_1 << std::endl;  // a
std::cout << char_var_2 << std::endl;  // A

std::cout << int(char_var_1) << std::endl;               // 97
std::cout << static_cast<int>(char_var_2) << std::endl;  // 65
```

### `auto`
- The auto datatype allows the compiler to automatically deduce the datatype of the variable.
- Example:
```cpp
auto int_var{123};
auto float_var{1.56f};
auto double_var{1.8892};
auto long_double_var{1.9928L};
auto char_var{'a'};

auto unsigned_int_var{123u};
auto long_int_var{123l};
```

## Operators

### Arithmetic Operators
```cpp
std::cout << 4 + 6 << std::endl;     // 10
std::cout << 5 - 2 << std::endl;     // 3
std::cout << 3 * 4 << std::endl;     // 12
std::cout << 15 / 2 << std::endl;    // 7
std::cout << 15 / 2.0 << std::endl;  // 7.5
std::cout << 15 % 2 << std::endl;    // 1
```
- Operators work with integers and floating point types. Except for modulus operator (`%`) which only works with integers.

### Precedence and Associativity
- _Precendence_ is used to determine the priority of different operators. Based on this priority the compiler executes an expression. The operators with higher precedence (priority) are executed first.
- For arithmetic operators the precedence is as follows:
    1. parenthesis
    2. multiplication, division and modulus
    3. addition and subtraction
- _Associativity_ is used to evaluate expressions containing operators with the same precedence. It decides whether the expression should be executed left to right or right to left.
- Parenthesis (`()`) has a higher precedence than the arithemetic operators thus it can be used to change the order in which an arithemetic expression is evaluated.
- Precedence of operators reference: https://en.cppreference.com/w/cpp/language/operator_precedence

### Prefix and Postfix/Suffix
- Increment and decrement operators provide a way to increase and decrease the value of a variable by 1.
- Prefix increment/decrement operators change the value immediately.
- Postfix/Suffix increment/decrement operators change the value after the statement is executed.
- Example:
```cpp
int var_a{12};
float var_b{3.14f};

// Prefix
std::cout << var_a++ << std::endl;  // 12
std::cout << var_a << std::endl;    // 13
std::cout << var_b-- << std::endl;  // 3.14
std::cout << var_b << std::endl;    // 2.14

// Postfix/Suffix
std::cout << ++var_a << std::endl;  // 14
std::cout << --var_b << std::endl;  // 1.14
```

### Compound Assignment Operators
- These are modified assignment operators which perform an operation prior to assignment.
- Example:
```cpp
int var{10};

var += 3;                       // var = var + 3
std::cout << var << std::endl;  // 13

var -= 1;                       // var = var - 1
std::cout << var << std::endl;  // 12

var *= 3;                       // var = var * 3
std::cout << var << std::endl;  // 36

var /= 6;                       // var = var / 6
std::cout << var << std::endl;  // 6

var %= 4;                       // var = var % 4
std::cout << var << std::endl;  // 2
```

### Relational Operators
- These operators are used to compare the values of 2 operands.
- List of relational operators:
    1. Greater than (`>`)
    2. Less than (`<`)
    3. Greater than or equal to (`>=`)
    4. Less than or equal to (`<=`)
    5. Equality (`==`)
    6. Not equal (`!=`)

### Logical Operators
- List of logical operators:
    1. AND (`&&`)
    2. OR (`||`)
    3. NOT (`!`)
- AND and OR are binary operators, i.e., they take 2 operands. Whereas, NOT is a unary operator, it takes 1 operand.
- Precedence of logical operators:
    1. NOT
    2. AND
    3. OR

## Control Flow

### Conditional Statements
- They are used for decision making. They allow the program to follow different paths based on certain conditions.
1. `if`-`else`
- Syntax:
```cpp
if (condition) {
    // true block
} else {
    // false block
}
```

2. `if`-`else if`
- Syntax:
```cpp
if (condition1) {
    // block 1
} else if (condition2) {
    // block 2
} else  // optional
{
    // default block
}
```

3. `switch`
- Syntax:
```cpp
switch (variable) {
    case value1:
        // block 1
        break;
    case value2:
        // block2
        break;
    default:
        // optional default block
}
```
- `switch` executes statements of all cases once any one `case` is `true`. The, `break` statement is used to prevent this and execute statements of only the `case` that is `true`.
- `default` block can be used like `else`.

### Looping Statements
- They are used for repeting parts of the code without rewriting it.
1. `for`
- It is an entry-controlled loop.
- Syntax:
```cpp
for (initialization; condition; update) {
    // statements
}
```
- Example: program that prints "Hello World!" 5 times.
```cpp
for (int i = 1; i <= 5; i++)
{
    std::cout << "Hello World!" << std::endl;
}
```

2. `while`
- Also an entry-controlled loop.
- Syntax:
```cpp
while (condition) {
    // statements
}
```
- Example: same as previous example.
```cpp
int i = 1;
while (i <= 5)
{
    std::cout << "Hello World!" << std::endl;
    i++;
}
```

3. `do... while`
- It is an exit-controlled loop. Thus, its statements are executed atleast once.
- Syntax:
```cpp
do {
    // statements
} while (condition);
```
- Example: same as previous example.
```cpp
int i = 1;
do {
    std::cout << "Hello World!" << std::endl;
    i++;
} while (i <= 5);
```

## Generics and Templates
- Generics are a feature which allows type to be passed as a parameter to functions, classes, methods, etc.
- Generics can be implemented using templates.
- Example of generic function:
```cpp
template <typename T>
void swap(T& a, T& b) {
    // passing by reference, else variables won't be swapped in calling scope
    T temp = a;
    a = b;
    b = temp;
    return;
}
```

## Recursion
- Recursion is when a function calls itself. Recursion can be used to repeat a block of code like loops.
- Example of recursion:
```cpp
long int factorial(int n) {
    if (n == 0) {
        return 1;
    }
    return n * factorial(n - 1);
}
```

## Object Oriented Programming

### Introduction
1. Class
    - It is a user-defined datatype. It is the building block of object oriented programming.
    - Class is a blueprint for an object. E.g.: `class Car`.
    - Class can have attributes (data members/class variables) and behaviours (member functions/methods).
    - Attribute e.g.: brand, model, year, color, etc.
    - Behaviours e.g.: start engine, honk horn, open trunk, etc.
2. Object
    - Object is an instance of a class. E.g.: 2002 Toyota Corrolla.
3. Constructor
    - It is a special method of a class which is invoked at the time of object creation.
    - Constructor must have the same name as the class.
    - Constructor does not have a return value, thus, they don't have a return type.
    - When a class has no constructor, a defualt constructor which takes no arguments is created by the compiler.
4. Destructor
    - It is a special method of a class which is invoked at the time of object destruction.
    - Destructor must have the same name as the class but the name is prefixed with a tilde sign `~`.
    - Destructor does not have a return value, thus, they don't have a return type.
    - There can only be one destructor in a class. It can not be overloaded.
    - The purpose of the destructor is to release the memory occupied by objects created by the constructor.
5. Encapsulation
    - Encapsulation is a OOP concept which refers to the wrapping of data in separate containers or "capsules". It is defined as binding together the data and the functions that manipulate it.
6. Access Modifiers
    - Encapsulation has been implemented in C++ using access modifiers. There are 3 access modifiers: `private` (default), `public` and `protected`.
7. Polymorphism
    - Polymorphism is the ability of changing forms. Function overloading is an example of polymorphism.

## Array
- Array is a group of variables (elements) of the same datatype. An array is stored in a contiguous memory location.
- Array is essentially a pointer to the 0th element of the array.
```cpp
int arr[5]{1, 2, 3, 4, 5};
std::cout << arr << std::endl;      // address of 0th element
std::cout << &arr[0] << std::endl;  // address of 0th element

std::cout << arr[3] << std::endl;      // 4
std::cout << *(arr + 3) << std::endl;  // 4
```
- When you pass an array to a function using pass by value only the pointer is passed.
- Once an array is created you can't assign a value to it. You can assign values to the elements but not the array.
- In C++ there is no index out of bounds checking. Thus, if you have an array of size 5 you can still access the element on index 5 like so `arr[5]`. Out of bounds index will not give an error it will just return a garbage value.

## Pointers
- Pointers are variables which store a memory address.
- The _address of operator_ `&` can be used to get the memory address of a variable. Note that the ampersand sign `&` is also used as a symbol for references in C++.
```cpp
int var;
std::cout << &var << std::endl;  // 0x7ffd0f8b4b94
```
- Pointers can be created for any datatype. The datatype of a pointer helps the compiler identify the size of the variable which enables features like pointer arithematic.
- The asterix sign `*` is used to declare pointers. In expressions a unary asterix (`*`) is used to dereference the pointer, i.e., to access the value stored in the variable the pointer points to.
```cpp
int var;
int *ptr = &var;

std::cout << ptr << std::endl;  // address of var

*ptr = 8;                        // var = 8
std::cout << var << std::endl;   // 8
std::cout << *ptr << std::endl;  // 8

// address of (&) and dereferencing (*) operators cancel out
std::cout << &*ptr << std::endl;  // address of var
std::cout << *&var << std::endl;  // 8
```

### `void` Pointer
- A `void` pointer can be used to store the address of a variable of any datatype. But `void` pointers can not be dereferenced directly. To dereference a `void` pointer it needs to be cast into the correct type.
```cpp
void print(void *ptr, int size) {
    switch (size) {
        case sizeof(int):
            std::cout << *((int *)ptr) << std::endl;
            break;
        case sizeof(char):
            std::cout << *((char *)ptr) << std::endl;
            break;
    }
}

int main() {
    int var = 12;
    char var2 = 'e';

    print(&var, sizeof(var));
    print(&var2, sizeof(var2));

    return 0;
}
```
