# C# Notes

**Print to console:**  
```c#
Console.WriteLine("hello world");
```

<br>
<br>

**String interpolation:**  
```c#
// Example 1
string stringName = $"A is {variableA} and B is {variableB}.";

// Example 2
Console.WriteLine($"Hello, {name}! Today is {date.DayOfWeek}, it's {date:HH:mm} now.");
```

<br>
<br>

**Get input and convert input:**  
```c#
string input = Console.ReadLine();
```
```c#
// Convert input (does not account for an exception)
int input = Convert.ToInt32(Console.ReadLine());
```
```c#
// Convert input (accounts for an exception)
string consoleInput;
int input;
bool incorrect = false;

do
{
    if (incorrect)
        Console.WriteLine("Your input was not valid. Please try again.\r\n");
	
    Console.WriteLine("Enter a number: ");
    consoleInput = Console.ReadLine();
    incorrect = true;
} while (int.TryParse(consoleInput, out input) == false);

// input is now == (int)consoleInput
```

<br>
<br>

**Type conversion:**  
```c#
// Cast float to int
float x = 1234.7f;
int a = (int)x;
```

<br>
<br>

**Random:**  
```c#
Random random = new Random();

random.Next(maxValue);
random.Next(minValue, maxValue);
random.NextDouble(); //Returns a random number between 0.0 and 1.0
```

<br>
<br>

**Conditional Operator: '?:'** - Returns one of two values depending on the value of a Boolean expression.  
```c#
// The condition evaluates to true or false. If true then #1 is returned, if false then #2 is returned.
condition ? first_expression : second_expression;

classify = (input > 0) ? "positive" : "negative";  
```

<br>
<br>

**Array** - A data structure with a fixed size used to store variables of the same type.
```c#
datatype[] arrayName = new datatype[size] { value, value.. };

int[] numbers = new int[] { 1, 2, 3 };

// numbers[0] == 1
// numbers[1] == 2
// numbers[2] == 3
```

<br>
<br>

**List** - A data structure with a dynamic size used to store variables of the same type.
```c#
List<datatype> listName = new List<datatype>() { value, value.. };

List<int> numbers = new List<int>() { 1, 2, 3 };
```

<br>
<br>

**enum** - A set of name-value pairs that are constants.
```c#
public enum ShippingMethod
{
    Regular = 1,
    Priority = 2,
    Express = 3;
}

var shMethod = ShippingMethod.Express;
Console.WriteLine(shMethod); // 3

var shMethodID = 3;
Console.WriteLine((ShippingMethod)shMethodID); // Express
```

<br>
<br>

**Access modifier** - The accessibility of member or type.
```
Public - visible/accessible anywhere  
Private - only visible/accessible in the entire block where it's defined

Private is the default access modifier if none was declared.
```

<br>
<br>

---

<br>
<br>

### Class:
A template for creating objects that provides initial fields and methods for an object.

Field - A variable that is declared directly in a class.  
Member - Things that a class contains: Fields, Properties, Constructors, Methods.  
Namespace - A container for classes. "using Namespace;"

Hierarchy of a class:
```
1. Fields (available everywhere in the class)  
2. Constructor  
3. Methods
```

Declaring a class:
```c#
modifier class ClassName
{
    // Members
}
```
```c#
public class Person
{
    // Fields

    public Person()
    {
    }

    // Methods
}
```

<br>

### Constructor:
A method that is called when an object (instance of a class) is created. We use constructors to intialize fields in an object. Constructor methods have the same name as the class.
```c#
// Create a constructor of the current class:
// ctor + Tab


public class Person
{
    string first;
    string last;
    
    public Person(string firstName, string lastName)
    {
        first = firstName;
        last = lastName;
    }
}
```

<br>

### Object:
A particular instance of a class.

Create an object / Instantiate a class:
```c#
var objectName = new ClassName(arguments);
```

<br>

### Example:
```
Person:
    Fields:
        Name
        Age
        Height
    Methods:
        Walk()
        Run()
        Talk(string input)


Objects:
    var john = new Person();
    var mary = new Person();


Setting a field and calling a method:
    john.Name = "John";
    mary.Talk($"Hello {john.Name}!");
```

<br>

### Static modifier:
**Static classes:**  
To use a non-static class you need to create an object of the class. A static class cannot be instantiated, in other words, you cannot use the new keyword to create a variable of the class type. Because they are not instantiatable, you access the members of a static class by using the class name itself. Static classes are used to hold shared variables and methods. Since there will be only one instance of it everything will use that one shared set of variables and methods.

**Static members:**  
You can't access static members from objects. When an object is made anything static is removed from the object so it does not get any of the static things. Static members exist only in the class and are accessed the same way as from a static class.

Example of a static member in a non-static class:
```c#
public class Calculator
{
    public static int Add(int a, int b)
    {
        return a + b;
    }
}

int answer = Calculator.Add(1, 2);

// Since the add method in the calculator class is static
// that means you don't need to create an object to use that method.
```

<br>

### Inheritance:
A relationship between two classes that allows one to inherit code from another. A child class can inherit the existing members from a base class, then the child class can add any members to itself that are specific to the child class.
```c#
modifier class ChildClassName : BaseClassName {}
```

<br>

### Abstract and Override modifiers:
The abstract modifier enables you to create classes and class members that are incomplete and must be implemented in a derived class. Use the abstract modifier in a class declaration to indicate that a class is intended only to be a base class of other classes. An abstract class cannot be instantiated. Members marked as abstract, or included in an abstract class, must be implemented by classes that derive from the abstract class.

Abstract classes may also define abstract methods by adding the keyword abstract before the return type of the method. Abstract methods have no implementation, so the method definition is followed by a semicolon instead of a normal method block. Derived classes of the abstract class must implement all abstract methods.
```c#
public abstract class Animal
{
    public abstract void Speak();
    // Since abstract methods have no implementation there is no curly bracket block.
}

public class Cat : Animal
{     
    public abstract void Speak()
    {
        Console.WriteLine("Meow");
    }
}

public class Dog : Animal
{     
    public abstract void Speak()
    {
        Console.WriteLine("Bark");
    }
}
```

<br>
<br>

### Struct:
1. Within a struct declaration, fields cannot be initialized unless they are declared as const or static.  
2. A struct cannot declare a default constructor (a constructor without parameters).  
3. The struct type is suitable for representing lightweight objects such as Point, Rectangle, and Color.

```c#
public struct Point
{
    public int x, y;

    public Point(int xParam, int yParam)
    {
        x = xParam;
        y = yParam;
    }
}
```
https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/classes-and-structs/how-to-know-the-difference-passing-a-struct-and-passing-a-class-to-a-method

<br>
<br>

---

<br>
<br>

### Properties:
Explained:
```c#
using System;
public class PlayerInput
{
    private float horizontalData;
    private float verticalData;
    // We don't want other classes changing this data so it is private.
    // However, another class needs to read the data from these variables.
    // But since they are private they are only visable in this class.


    // We could write public methods that allow us to get or set these private variables:
    public float GetHorizontalData()
    {
        return horizontalData;
    }

    public void SetHorizontalData(float hData)
    {
        horizontalData = hData;
    }
}


// And then call them from another class:
public class IDK
{
    float hInput;

    public void Main()
    {
        PlayerInput PIObject = new PlayerInput();
	
	hInput = PIObject.horizontalData;
	// Error: PIObject.horizontalData is private and not accessable outside of PIObject.
        // You cannot get the private data.
	
	PIObject.horizontalData = 3.22f;
	// Error: PIObject.horizontalData is private and not accessable outside of PIObject.
        // You cannot set the private data.

        // Using the public methods to access the private data:
        hInput = PIObject.GetHorizontalData();
        PIObject.SetHorizontalData(3.22f);
	
        Console.WriteLine(hInput);
        Console.WriteLine(PIObject.GetHorizontalData());
    }
}

// But instead you could do it in a much easier way using properties.
```

<br>

Property - A class member that provides access to fields of a class.  
A get property accessor is used to return the value, and a set property accessor is used to assign a new value.

<br>

Example:
```c#
// Create a property:
// propfull + Tab
// prop + Tab


//Get input data
float m_h;
public float H { get { return m_h; } } //Read only
float m_v;
public float V { get { return m_v; } } //Read only 

bool m_inputEnabled = false;
public bool InputEnabled { get { return m_inputEnabled; } set { m_inputEnabled = value; } }


public void GetInputKey()
{
    if (m_inputEnabled)
    {
        m_h = Input.GetAxisRaw("Horizontal");
        m_v = Input.GetAxisRaw("Vertical");
    }
}



// And then from another class:
void Update ()
{
    if (playerMover.isMoving)
    {
        return;
    }

    playerInput.GetInputKey();

    if (playerInput.V == 0)
    {
        if (playerInput.H < 0)
        {
            playerMover.MoveLeft();
        }
        else if (playerInput.H > 0)
        {
            playerMover.MoveRight();
        }
    }
    else if (playerInput.H == 0)
    {
        if (playerInput.V < 0)
        {
            playerMover.MoveBackward();
        }
        else if (playerInput.V > 0)
        {
            playerMover.MoveForward();
        }
    }
}
```

<br>

Useful things you can do with properties but can't if the variables were just public:
```c#
public bool InputEnabled
{
    get { return inputEnabled; }
    set
    {
        inputEnabled = value;
        Debug.Log("Input changed to: " + inputEnabled);
        // Everytime the value is changed its value is printed to the console.
    }
}

public float Health
{
    get { return health; }
    set
    {
        health = value;
	Object.UpdateHPUI(health);
	// When hp is changed the property automatically updates the UI.
    }
}
```

<br>

Initialize an auto-implemented property:
```c#
public string FirstName { get; set; } = "Jane";
```

<br>

### Anonymous Function (lambda expression):
https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/statements-expressions-operators/lambda-expressions

A function definition that is not bound to an identifier and contains only one executable statement.

Lambdas allow you to write quick throw away functions without naming them. They also provide a nice way to write closures.

Anonymous functions are often referred to as lambdas and often are introduced using the keyword lambda.

This anonymous function allows you to create functions from functions:
```python
def add(x):
    return lambda y: x + y
foo = add(5)
foo(1)


def add**(x)**:
    return lambda y: **x** + y
# The x variable in the lambda expression is referencing the parameter x, so x = x.

def add(x):
    return lambda **y**: x + y
# The lamdba requires the parameter y.

def add(x):
    **return lambda y: x + y**
# Add() returns a lambda.

foo = add(5)
# "foo = lambda y: 5 + y"

foo(1)
# "foo = lambda 1: 5 + 1"
>>> 6
```

<br>
<br>
<br>

Closure:  
https://stackoverflow.com/a/7464475/9020002  
https://stackoverflow.com/questions/4103750/closure-because-of-what-it-can-do-or-because-it-does  
https://www.google.com/search?q=programming+closure&ie=utf-8&oe=utf-8&client=firefox-b-1-ab

<br>

### Attributes:
A declarative tag that is used to convey information to runtime about the behaviors of various elements like classes, methods, structures, enumerators, etc. in your program.

Attributes add metadata to your program. Metadata is information about the types defined in a program.
```c#
// Declaring an attribute:
[attribute(positional_parameters, name_parameter = value, ...)] element;

[HideInInspector] public RoomNavigation roomNavigation;
```

<br>
