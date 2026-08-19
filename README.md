# Effective-Modern-C-++
These are my notes from Effective Modern C++ by Scott Myers Item by Item




# Template Functions

## What Did I Learn?

* To print output in C++, I can use `printf()` by including the `<cstdio>` library.
* `printf()` is not the only way to print output. I can also use `std::cout` by including the `<iostream>` library.
* The `main()` function is the entry point of a C++ program, and it returns an integer.
* I can define a **template function** that accepts different types of arguments.
* How I declare the parameter type (`ParamType`) in a template function matters.
* The basic syntax for declaring a template function is:

```cpp
template<typename T>
void f(ParamType param);
```

## Why Does It Matter?

Template functions allow me to write functions that work with **generic types** rather than being restricted to a specific data type.

How a parameter is passed—**by value, by reference, or by const reference**—can have different implications for:

* Performance
* Memory usage
* Whether the function can modify the original object
* How different types of arguments behave when passed to the function

Understanding these differences is important when writing efficient and reusable C++ code.

## Where Would I Use This in a Game Engine?

In a game engine, template functions can be used to create **generic and reusable systems** that operate on different data types without requiring separate implementations for each type.

For example, a generic function could potentially operate on different game objects, components, or data structures without having to rewrite the function for every individual type.

This can help reduce code duplication and make engine systems more flexible.

## What Questions Do I Still Have?

I still have questions about how C++ handles the type of a parameter when it is passed to a template function.

* How can I determine the type of a parameter when it is passed to a template function?
* How can I determine whether a parameter is a reference, const reference, or value?
* Is there a way to print or inspect whether a parameter is a reference?
* When designing generic functions for a game engine, what should I be aware of when using templates?
* Are there simpler or more effective ways to handle generic functionality in a game engine?





# `auto` Type Deduction

## What Did I Learn?

The most important takeaway from this topic was that **`auto` type deduction works similarly to template type deduction**, with an important exception involving **bracket notation**.

When using bracket notation, `auto` assumes the expression is a `std::initializer_list` in certain contexts.

For example:

```cpp
auto x = {1, 2, 3};
```

is deduced as:

```cpp
std::initializer_list<int>
```

However, the elements must be compatible with a single deduced type.

## Why Does It Matter?

Using `auto` with bracket notation containing multiple incompatible types can result in a compiler error.

For example:

```cpp
auto x = {1, 2.0, "three"};
```

cannot be deduced into a single `std::initializer_list` type.

Understanding how `auto` performs type deduction is important because it can affect whether code compiles and what type a variable actually becomes.

## Where Would I Use This in a Game Engine?

`auto` type deduction can be useful throughout a game engine when working with generic or complex types.

For example, it can make code easier to read when the type is obvious from the expression:

```cpp
auto playerHealth = 100;
auto playerName = std::string("Knight");
```

It can also be particularly useful when working with complex types such as iterators, containers, or templated engine systems.

The main caveat I learned is that I need to understand **what type the compiler will actually deduce**, especially when using brace initialization.

## What Questions Do I Still Have?

This topic was relatively straightforward. Most of my remaining questions came from the exercise I completed.

* Does the C++ compiler treat a **single quotation mark** (`'`) differently from a **double quotation mark** (`"`)?
* How can I reliably determine and report the type of a variable in C++?
* I used `typeid().name()` to inspect types. How reliable is this approach?

### Example

```cpp
#include <typeinfo>

auto value = 42;

std::cout << typeid(value).name() << std::endl;
```

I would like to better understand what `typeid().name()` actually returns and whether there is a better way to inspect types while learning C++.





# decltype

## What Did I Learn?

* Referenceness is ignored in `auto` type deduction, `decltype(auto)` deduction, and template type deduction.
* Thus, returning the value of a reference with `decltype(auto)` will dereference the value, returning an rvalue.
* A simple fix for this is to return `std::forward<T>(param)` instead when using a `decltype(auto)` return type and parameterizing the function with a global reference or `&&`.

## Why Does It Matter?

* Automatic dereferencing can create problems when attempting to set a reference to a value.
* It is important to exercise caution when using `decltype(auto)`.

## Where Would I Use This in a Game Engine?

`decltype(auto)` can be used to return a type based on the type of the return value of a function.

It should be treated with care. In a game engine, I would expect to use `decltype(auto)` for generalized function calls that may have a variance in the return type based on the input type of the function.

## What Questions Do I Still Have?

* I still cannot see the referenceness of an object using the utilities I am familiar with. It is often dereferenced before calling `typeid()`.
* How do I check the referenceness of an object in C++14 and later?





# Type Identification

## What Did I Learn?

* The **Boost library** can be used to determine the type of a variable.
* Type deduction does not always work as expected, so having a way to inspect a variable's type can be useful when debugging or working with generic code.

## Why Does It Matter?

In C++, you may need to determine what type an object actually is, especially when working with generic functions and user-defined types.

In a game engine, this can be particularly useful because **typecasting and working with user-defined types are common**. Being able to inspect a variable's type can help when debugging type deduction or determining how an object is being handled by a generic function.

## Where Would I Use This in a Game Engine?

When trying to determine the type of an object or generalize a function's input type, the Boost library can provide information about the variable's type.

This could be useful when working with generic engine systems that need to operate on different user-defined types.

## What Questions Do I Still Have?

* How do you install and configure Boost for use in a game engine?
* Can Boost report the types of user-defined classes?
* Can Boost's type information be used to help with generic functions?




# Auto vs Declared Types

# Lessons Learned

## What Did I Learn?

* `auto` can be used in contexts where previously explicit typing was required with templates and the like (`unique_ptr` and `function` were used).

## Why?

* `auto` is less cumbersome to use in memory and in typing out what you mean in the code. It can deduce complex types known only to the compiler.

## Game Engine?

* `auto` can be used in game engine code for better portability between systems.

## Questions:

* How do you use `std::unique_ptr` without getting a compiler error?
* Does the standard library even have template versions of `function` and `unique_ptr`?
* Which version of C++ am I currently working with?






# Auto Undefined Behavior

## Lessons Learned

* Understanding the behavior of `auto` under different circumstances is paramount, and it should only be used when it benefits the program.
* Some cases can create undefined behavior with a dangling pointer if you aren't careful.
* "As a general rule, 'invisible' proxy classes don't play well with `auto`."
* Explicitly Typed Initializer Idiom (ETII).

## Why?

* ETII adds transparency to a program, and understanding that proxies can lead to undefined behavior with `auto` is important to consider when designing a program.

## Game Engine Usage

* A game engine like Unreal uses C++, classes, and potentially `auto`. Understanding when to use it and when to use ETII for transparency is useful.

## Questions

1. What is a proxy?
2. What is an invisible proxy?
3. In what cases is `auto` justified?
4. In what cases is `auto` unjustified?
5. What is a proxy class?
6. What is the proxy design pattern?
7. Why would you use an Explicitly Typed Initializer Idiom?

