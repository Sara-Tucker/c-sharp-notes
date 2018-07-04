# Programming Notes

## Visual Studio / Resharper notes:
```
Ctrl + arrow - move cursor one word at a time  
End         - move cursor to end of the line
Home        - move cursor to beginning of the line

Shift       - activate selection with ^

Ctrl + Alt + ->    - expand selection
Ctrl + Alt + <-    - shrink selection

Ctrl + BS   - delete one word left of the cursor

Ctrl + F5   - run program without heavy debug mode

Ctrl + Space - auto-detect (infer) typing

Alt + Enter - Resharper menu

cw - Type for Console.WriteLine(); shortcut


JoinLines:
Join multiple lines into a one-liner.
Highlight text, right-click in the editor and select 'Join Lines' or use the keyboard shortcut 'Alt+j'.
```

<br>

## foo
The terms foo, bar, and foobar are used as placeholder names when exact identity is unimportant.

<br>

## Recursion
Recursion - A function that calls itself.  
A recursive function must always check for a condition to determine if it should call itself again or not.

<br>

Dictionary definition:
```
recursive - characterized by recurrence (repetition)  
recursion - repeated application of a recursive procedure
```

<br>

Example:
```c#
public static long Factorial(long number)
{
    if (number <= 1)
        return 1;
    else
    {
        return number * Factorial(number - 1);
    }
}

// 4*(4-1)*(3-1)*(2-1)
// 4*3*2*1 == 24
```

<br>
<br>

## Good Compound Conditional (two end conditions) and Function examples
```c#
bool keepGoing = true;
string correct = "Csharp";
int tries = 3;

while (keepGoing == true)
{
    string guess = Console.ReadLine("Please enter the password: ");
    tries -= 1;
    
    if (guess == correct)
    {
        Console.WriteLine("You may proceed.");
        keepGoing = false;
    }
    else
    {
        Console.WriteLine("That's not correct.")

        if (tries == 0)
        {
            Console.WriteLine("Sorry, you only had three tries.")
            keepGoing = false;
        }
        else
            Console.WriteLine($"You have {tries} tries left.");
    }
}
```

<br>

```c#
static double CylinderVolume(double radius, double height)
{
    const double pi = 3.14159;
    return pi * Math.Pow(radius, 2) * height;
}
```

<br>
<br>

## Methods, Parameters, and Arguments
Parameter - A variable in the declaration of a function.  
Argument - The value of the variable that gets passed to the function.
```c#
// Creating a method:
typereturned MethodName(parameters)
{
    //code
}

// Calling a method:
Class.Method(arguments);
```

<br>
<br>

## Scope and Variables
**Explained:**  
Variables declared at top blocks can be used in downward blocks.  
Variables declared at bottom blocks can't be used in upward blocks.  
Variables declared in one function can't be accessed by another.
```python
def Outer():
    x = 1
    
    def Inner():
        print(x) #Prints 1
        x = 2
        print(x) #Prints 2
        y = 3
        
    Inner()
    print(y) #Error

def SamePlace():
    print(x) #Error

Outer()
SamePlace()
```

<br>

Scope:  
The region where variables and methods are visable/accessible.

Global scope:  
Variables or methods that are visable/accessible everywhere.

Local scope:  
Variables or methods that have local scope (this includes instances of classes) are accessible only in the current code block.

<br>

Global variable:  
A variable with global scope.

Local variable:  
A variable that is given local scope. Local variable references in the block in which it is declared override the same variable name in the larger scope.

Non-local variable:  
A variable that is not defined in the local scope. Non-local variables are used in the context of nested functions.

<br>
<br>

## Module -> Library/Package, API, Framework
**Module:**  
A module is a file containing definitions, functions, and statements. Putting code into modules is useful because of the ability to import the functionality of modules into your code. Example: import random; n = random.randint(1,5);

<br>

**Library/Package:**  
A package is a collection of modules, such as NumPy. Packages are a way of structuring Python’s module namespace by using “dotted module names”. For example: import Package.Module

<br>

**API (Application Programming Interface):**  
A software intermediary that allows two applications to talk to each other. When you use an application it connects to the Internet and sends data to a server. The API then retrieves that data, interprets it, performs the necessary actions and sends it back to your phone.

<br>

**Framework:**  
A framework is a group of classes, interfaces and other pre-compiled code that applications can be built with.  
Inversion of control: In a framework, unlike in libraries or in standard user applications, the overall program's flow of control is not dictated by the program/programmer, but by the framework.  
Extensibility: A user can extend the framework and  add code to provide specific functionality.  
Non-modifiable framework code: The framework can accept user-implemented extensions but the code of the framework itself is not modifiable.  

<br>
<br>

## Expression, Statement, State, Side effect
**Statement:**  
A complete line of code that does something and does not return a value. Ex: print 'hello'

<br>

**Expression:**  
A complete line of code that evaluates to a value. Ex: 2 * 2

<br>

**State:**  
Def 1: The data that defines the condition of an object.  
Def 2: A computer program stores data in variables which represent storage locations in the computer's memory. The contents of these memory locations, at any given point in the program's execution, is called the program's state.  

If the values of the properties attached to a given entity change over time, you say that the state of that entity is mutable. Otherwise, you say that the state is immutable.

<br>

**Side effect:**  
A function or expression produces a side effect if it modifies some state or interacts with the outside world.  
Simple: A side effect changes something somewhere.  
Examples of side effects: change the value of a variable, write data to a file, disable a button on the UI  
Functional programming avoids side effects since something should be the result of something else, not just changed.

<br>
<br>

## Programming Paradigm: (pair-a-dime)
A way of thinking about software construction based on some fundamental, defining principles.  
Examples: object oriented programming and functional programming.

<br>

**Functional programming:**  
The process of building software by composing pure functions, avoiding shared state, mutable data, and side-effects. Functional programming is declarative rather than imperative, and application state flows through pure functions. Contrast with object oriented programming, where application state is usually shared and colocated with methods in objects. Functional programming languages don’t support flow Controls like loop statements and conditional statements like If-Else and Switch Statements. They directly use the functions and recursion.

<br>

**State vs Functional programming:**  
State - storing variables and properties in your code  
Functional programming - running values through a "stream" of functions that manipulate the data being passed along

<br>
<br>

## Programming Basics:
Machine code:  
A set of instructions executed directly by the CPU. The CPU can only understand machine code.

Binary language / hexadecimal language (basically machine code):  
A representation / way of viewing machine code. If someone is refering to the binary code of program they are refering to the machine code.

Assembly language:  
A human readable representation (plain english) of machine code.  
Assembler:  
Converts assembly code to machine code.

Source code:  
Computer instructions written using a human-readable programming language.

Compiler:  
Coverts source code into machine code to create an executable program.

Interpreter:  
A computer program that directly executes source code without requiring it to have been previously compiled into machine code.  
Interpreting:  
The code is run line by line i.e. processed on the spot.
