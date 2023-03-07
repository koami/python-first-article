![N|DIT Logo](./img/Logo.png)

# Python Exam for Master I DIT Session of November 2022

# Theme : Decorators in Python

# Writen by : _Koami R. AZIABOU_

## Contents : 
- Introduction
- Concept
- Theory
- Practical examples
- Potentials alternatives
- Data analysis use cases
- Conclusion

## Introduction
Everything started during the python course for my MSC in Data Science and Big Data at DIt. Things were going well until the exam. Well, you know it goes wrong and we end up having to write an article on an advance subject in python. Well, why not right. Then the list of topics, we were all like : 

![Alt Text](./img/surprisecat.gif)


And as the masochiste that I'm I took decorators. Why.? Good question. I invite you to read the rest of this article to discover what I discover and maybe learn a few new tricks.

PS i : You will have a lot of post scriptum in this article, be ready. Sorry for the so not conventional intro. Let's move on.

## Concept
In object-oriented programming, the decorator pattern is a design pattern that allows behavior to be added to an individual object, dynamically, without affecting the behavior of other objects from the same class. The decorator pattern is often useful for adhering to the Single Responsibility Principle, as it allows functionality to be divided between classes with unique areas of concern as well as to the Open-Closed Principle, by allowing the functionality of a class to be extended without being modified. Decorator use can be more efficient than subclassing, because an object's behavior can be augmented without defining an entirely new object. 

## Theory
In Python, a decorator is a way to modify or enhance the behavior of a function without changing the function's code itself. Instead, decorators allow you to "wrap" a function with another function that adds functionality before or after the original function is executed.

Decorators are powerful tools in Python because they allow you to modify the behavior of functions in a modular and reusable way. This can be especially useful when working with large codebases or when trying to keep your code organized and easy to understand.

Python decorators are typically implemented as functions themselves, and they take the original function as an argument. The decorator then returns a modified version of the function that incorporates the additional functionality. This can include things like logging, caching, or authorization checks.

Decorators can be used to achieve a variety of goals, such as modifying the behavior of functions without modifying their source code, enforcing security policies, providing caching or memoization, and more. In Python, decorators are widely used in frameworks and libraries like Flask, Django, and SQLAlchemy, making them an important concept for any Python developer to understand.

## Practicals examples

- Timing Function Execution:
Decorators can be used to time how long a function takes to execute. This is useful when you want to optimize the performance of your code or debug slow-running functions.

---
```python
import time

def timing_decorator(func):
    def wrapper(*args, **kwargs):
        start = time.time()
        result = func(*args, **kwargs)
        end = time.time()
        print(f"Function {func.__name__} took {end - start} seconds to execute.")
        return result
    return wrapper

@timing_decorator
def slow_function():
    time.sleep(2)
```
In this example, we define a decorator called **timing_decorator** that takes a function as an argument and returns a new function called **wrapper**. **wrapper** measures the time it takes to execute the function and prints the result to the console. We apply the decorator to the **slow_function** using the **@** syntax.


- Validate Function Input:
Decorators can be used to validate the input to a function. This is useful when you want to make sure that the input to your function is correct before executing the code.

---
```python
def validate_input_decorator(func):
    def wrapper(*args, **kwargs):
        if not all(isinstance(arg, int) for arg in args):
            raise TypeError("All arguments must be integers.")
        result = func(*args, **kwargs)
        return result
    return wrapper

@validate_input_decorator
def add_numbers(a, b):
    return a + b
```
In this example, we define a decorator called **validate_input_decorator** that takes a function as an argument and returns a new function called **wrapper**. **wrapper** checks if all the arguments to the function are integers and raises an exception if they are not. We apply the decorator to the **add_numbers** function using the **@** syntax.


- Cache Function Results:
Decorators can be used to cache the results of a function to avoid recomputing the same results multiple times. This is useful when you have a function that takes a long time to compute and you want to avoid repeating the computation unnecessarily.

---
```python
def cache_decorator(func):
    cache = {}
    def wrapper(*args, **kwargs):
        key = str(args) + str(kwargs)
        if key not in cache:
            result = func(*args, **kwargs)
            cache[key] = result
        else:
            result = cache[key]
        return result
    return wrapper

@cache_decorator
def fibonacci(n):
    if n == 0:
        return 0
    elif n == 1:
        return 1
    else:
        return fibonacci(n-1) + fibonacci(n-2)
```
In this example, we define a decorator called **cache_decorator** that takes a function as an argument and returns a new function called **wrapper**. **wrapper** uses a cache dictionary to store the results of the function and checks the cache before calling the function. If the result is already in the cache, **wrapper** returns the cached result instead of calling the function again. We apply the decorator to the **fibonacci** function using the **@** syntax.


## Potentials alternatives
While decorators are a usefull feature in Python that allow us to modify the behavior of functions or classes, there are some alternative approaches that can achieve similar results:

Higher-Order Functions: In Python, functions are first-class objects, which means they can be passed as arguments to other functions and returned as values. We can use higher-order functions to wrap or modify existing functions without using decorators. For example, we can define a function that takes a function as an argument, modifies its behavior, and returns the modified function.

Inheritance and Composition: Inheritance and composition are object-oriented programming techniques that allow us to reuse code and modify the behavior of existing classes. By creating subclasses or composing classes, we can add or override methods and properties to change the behavior of an existing class.

Context Managers: Context managers provide a way to manage resources and ensure that they are properly initialized and cleaned up. We can use context managers to modify the behavior of functions or classes by wrapping them in a with statement.

Function Factories: Function factories are functions that create other functions. We can use function factories to create customized versions of a function with different behavior or parameters. This approach is similar to using higher-order functions but can be more flexible and modular.

While decorators are a powerful and widely used feature in Python, it's important to understand that they are not the only way to modify the behavior of functions and classes. By choosing the right approach for the problem at hand, we can write more flexible and maintainable code.

## Data analysis use cases

## Sources
https://en.wikipedia.org/wiki/Decorator_pattern
https://www.geeksforgeeks.org/decorators-in-python/