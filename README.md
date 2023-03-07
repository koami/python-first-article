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
Python is without a doubt one of the most used and robust language in the tech industry. It has a wide variety of topics from magic method to execptions, type and decorators.

In this article, we will explore the concept of decorators in Python and how they work under the hood. We will cover the theory behind decorators, practical examples of how to use them, and discuss the potential alternatives to decorators. Finally, we will also explore how decorators can be applied in data analysis use cases, making them a valuable tool in the data science toolbox.

## Concept
In object-oriented programming, the decorator pattern is a design pattern that allows behavior to be added to an individual object, dynamically, without affecting the behavior of other objects from the same class. The decorator pattern is often useful for adhering to the Single Responsibility Principle, as it allows functionality to be divided between classes with unique areas of concern as well as to the Open-Closed Principle, by allowing the functionality of a class to be extended without being modified. Decorator use can be more efficient than subclassing, because an object's behavior can be augmented without defining an entirely new object. 

## Theory
In Python, a decorator is a way to modify or enhance the behavior of a function without changing the function's code itself. Instead, decorators allow you to "wrap" a function with another function that adds functionality before or after the original function is executed.

Decorators are powerful tools in Python because they allow you to modify the behavior of functions in a modular and reusable way. This can be especially useful when working with large codebases or when trying to keep your code organized and easy to understand.

Python decorators are typically implemented as functions themselves, and they take the original function as an argument. The decorator then returns a modified version of the function that incorporates the additional functionality. This can include things like logging, caching, or authorization checks.

Decorators can be used to achieve a variety of goals, such as modifying the behavior of functions without modifying their source code, enforcing security policies, providing caching or memoization, and more. In Python, decorators are widely used in frameworks and libraries like Flask, Django, and SQLAlchemy, making them an important concept for any Python developer to understand.

- Syntax for Decorator
---
```python
@gfg_decorator
def hello_decorator():
    print("Gfg")

'''Above code is equivalent to -

def hello_decorator():
    print("Gfg")
    
hello_decorator = gfg_decorator(hello_decorator)'''
```
In the above code, **gfg_decorator** is a callable function, that will add some code on the top of some another callable function, **hello_decorator** function and return the **wrapper** function.

## Practicals examples

- Decorator step:

---
```python
# defining a decorator
def hello_decorator(func):
    # inner1 is a Wrapper function in
    # which the argument is called
    # inner function can access the outer local
    # functions like in this case "func"
    def inner1():
        print("Hello, this is before function execution")
        # calling the actual function now
        # inside the wrapper function.
        func()
        print("This is after function execution")
    return inner1
 
# defining a function, to be called inside wrapper
def function_to_be_used():
    print("This is inside the function !!")

# passing 'function_to_be_used' inside the
# decorator to control its behaviour
function_to_be_used = hello_decorator(function_to_be_used)
 
# calling the function
function_to_be_used()
```
Let’s see the behaviour of the above code and how it runs step by step when the “function_to_be_used” is called.
![Decorator step](./img/decorators_step.png)

- Change print output :

---
```python
def make_pretty(func):
    def inner():
        print("I got decorated")
        func()
    return inner

@make_pretty
def ordinary():
    print("I am ordinary")

ordinary()  
```
In this example, we define a decorator called **make_pretty** that takes a function as an argument and returns a new function called **inner**. **inner** add a print before calling the function again. We apply the decorator to the **ordinary** function using the **@** syntax.

- Logging decorator: 
A logging decorator can be used to log information about a function call. This can be useful for debugging and auditing.

---
```python
import logging

logging.basicConfig(filename='example.log', level=logging.INFO)
def logger(func):
    def wrapper(*args, **kwargs):
        logging.info(f"Executing function: {func.__name__}")
        result = func(*args, **kwargs)
        return result
    return wrapper

@logger
def any_func(x, y):
    return x + y

print(any_func(3, 5))
```
In this example, we define a decorator called **logger** that takes a function as an argument and returns a new function called **wrapper**. **wrapper** uses the logging library to save the usage of the function, **wrapper** returns the cached result instead of calling the function again. We apply the decorator to the **any_func** function using the **@** syntax.

- Conditional Decorators:
In the following program, the program takes user input to decide on the condition. If the user enters 1, the decorator is called and the string is returned in uppercase. If the user enters 2, again a decorator is called and the given string is returned in lowercase. Apart from this if any other number is entered the function is returned as it is without any modification.

---
```python
def decorator1(func):
      
    def wrapper():
        oldstring = func()
        newstring = oldstring.upper()
        return newstring
      
    return wrapper
  
def decorator2(func):
      
    def wrapper():
        oldstring = func()
        newstring = oldstring.lower()
        return newstring
      
    return wrapper
  
cond = 1
  
if cond == 1:
    @decorator1
    def func():
        return 'GeeksFORGeeKs'
elif cond == 2:
    @decorator2
    def func():
        return 'GeeksFORGeeKs'
else:
    def func():
        return 'GeeksFORGeeKs'
      
print(func())
```

## Potentials alternatives
While decorators are a usefull feature in Python that allow us to modify the behavior of functions or classes, there are some alternative approaches that can achieve similar results:

- Higher-Order Functions: In Python, functions are first-class objects, which means they can be passed as arguments to other functions and returned as values. We can use higher-order functions to wrap or modify existing functions without using decorators. For example, we can define a function that takes a function as an argument, modifies its behavior, and returns the modified function.

- Inheritance and Composition: Inheritance and composition are object-oriented programming techniques that allow us to reuse code and modify the behavior of existing classes. By creating subclasses or composing classes, we can add or override methods and properties to change the behavior of an existing class.

- Context Managers: Context managers provide a way to manage resources and ensure that they are properly initialized and cleaned up. We can use context managers to modify the behavior of functions or classes by wrapping them in a with statement.

- Function Factories: Function factories are functions that create other functions. We can use function factories to create customized versions of a function with different behavior or parameters. This approach is similar to using higher-order functions but can be more flexible and modular.

While decorators are a powerful and widely used feature in Python, it's important to understand that they are not the only way to modify the behavior of functions and classes. By choosing the right approach for the problem at hand, we can write more flexible and maintainable code.

## Data analysis use cases

- Performance check:
Timing our function is great and all but we want more info. In addition to duration, this next decorator provides information on the function, including the name and docstring, as well as performance information such as memory usage:

---
```python
def performance_check(func):
    """Measure performance of a function"""

    @wraps(func)
    def wrapper(*args, **kwargs):
      tracemalloc.start()
      start_time = time.perf_counter()
      res = func(*args, **kwargs)
      duration = time.perf_counter() - start_time
      current, peak = tracemalloc.get_traced_memory()
      tracemalloc.stop()

      print(f"\nFunction:             {func.__name__} ({func.__doc__})"
            f"\nMemory usage:         {current / 10**6:.6f} MB"
            f"\nPeak memory usage:    {peak / 10**6:.6f} MB"
            f"\nDuration:             {duration:.6f} sec"
            f"\n{'-'*40}"
      )
      return res
    return wrapper
```
It is pretty similar to the previous function, only we print out more information:

---
```python
@performance_check
def is_prime_number(number: int):
    """ Checks whether a number is a prime number """
    ....rest of the function
```
Calling is_prime_number(number=9843861881) will print out the following:

---
```sh
Function:             is_prime_number ( Checks whether a number is a prime number )
Memory usage:         0.000432 MB
Peak memory usage:    0.000622 MB
Duration:             0.000015 sec
----------------------------------------
```

- Timing Function Execution:
When working with large datasets, it can be useful to time how long certain operations take. We can use a decorator to add timing functionality to a function. Here's an example:

---
```python
import time

def timing_decorator(func):
    def wrapper(*args, **kwargs):
        start_time = time.time()
        result = func(*args, **kwargs)
        end_time = time.time()
        print(f"{func.__name__} took {end_time - start_time:.5f} seconds to execute")
        return result
    return wrapper

@timing_decorator
def slow_function():
    # perform some time-consuming operation
    time.sleep(3)

slow_function() # output: slow_function took 3.00322 seconds to execute
```
In this example, we define a decorator called **timing_decorator** that takes a function as an argument and returns a new function called **wrapper**. **wrapper** measures the time it takes to execute the function and prints the result to the console. We apply the decorator to the **slow_function** using the **@** syntax.


- Data Validation: 
Decorators can be used to validate the input and output of functions. This can be particularly useful when working with large datasets, where errors can be costly and time-consuming to fix.

---
```python
def validate_input_decorator(func):
    def wrapper(*args, **kwargs):
        for arg in args:
            if not isinstance(arg, int):
                raise TypeError("Input must be an integer")
        result = func(*args, **kwargs)
        if not isinstance(result, int):
            raise TypeError("Output must be an integer")
        return result
    return wrapper

@validate_input_decorator
def double_number(n):
    return n*2
```
In this example, we define a decorator called **validate_input_decorator** that takes a function as an argument and returns a new function called **wrapper**. **wrapper** checks if all the arguments to the function are integers and raises an exception if they are not. We apply the decorator to the **double_number** function using the **@** syntax.


- Memoization: 
Memoization is a technique used to speed up the execution of functions by caching the results of previous computations. Decorators can be used to implement memoization, which can be particularly useful when working with functions that are computationally expensive.

---
```python
def memoize_decorator(func):
    cache = {}
    def wrapper(*args):
        if args in cache:
            return cache[args]
        result = func(*args)
        cache[args] = result
        return result
    return wrapper

@memoize_decorator
def fibonacci(n):
    if n < 2:
        return n
    return fibonacci(n-1) + fibonacci(n-2)

```
In this example, we define a decorator called **cache_decorator** that takes a function as an argument and returns a new function called **wrapper**. **wrapper** uses a cache dictionary to store the results of the function and checks the cache before calling the function. If the result is already in the cache, **wrapper** returns the cached result instead of calling the function again. We apply the decorator to the **fibonacci** function using the **@** syntax.

## Conclusion
In conclusion, decorators are a robust feature in Python that allow developers to modify or enhance the functionality of existing functions or classes without changing their original code. By wrapping functions or classes with additional functionality, decorators can help to keep code clean, modular, and reusable.

In this article, we have covered the basics of decorators, including their concept and theory, and provided several practical examples that illustrate their usefulness. Additionally, we explored some potential alternatives to decorators, such as subclassing and function composition.

Finally, we discussed how decorators can be applied in the context of data analysis, highlighting their usefulness for tasks such as debugging, profiling, and caching. Overall, decorators are an essential tool in the Python developer's toolkit and can greatly improve the efficiency and maintainability of code.

## Sources 
- [Decorator Pattern](https://en.wikipedia.org/wiki/Decorator_pattern)
- [Python syntax and semantics](https://en.wikipedia.org/wiki/Python_syntax_and_semantics#Decorators)
- [Decorators in Python](https://www.geeksforgeeks.org/decorators-in-python)
- [Python Decorators](https://www.programiz.com/python-programming/decorator)
- [5 real handy python decorators for analyzing/debugging your code](https://towardsdatascience.com/5-real-handy-python-decorators-for-analyzing-debugging-your-code-c22067318d47)
- [Conditional Decorators in Python](https://www.geeksforgeeks.org/conditional-decorators-in-python/?ref=rp)
- [Python - measure function execution time with decorator](https://stackoverflow.com/questions/70642928/python-measure-function-execution-time-with-decorator)
- [Memoization using decorators in Python](https://www.geeksforgeeks.org/memoization-using-decorators-in-python/?ref=rp)
- [Timing Functions With Decorators – Python](https://www.geeksforgeeks.org/timing-functions-with-decorators-python/)