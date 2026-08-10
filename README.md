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
