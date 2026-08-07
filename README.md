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
