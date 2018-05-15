# C# Notes

**Print to console:**  
```c#
// C#
Console.WriteLine("hello world");

// Unity
Debug.Log("hello world");
```

<br>
<br>

**String interpolation:**  
```c#
// C#
string stringName = $"A is {a} and B is {b}"; // Example 1
Console.WriteLine($"Hello, {name}! Today is {date.DayOfWeek}, it's {date:HH:mm} now."); // Example 2

// Unity
// To enable .NET 4.6 go to Edit -> Project Settings -> Player
// Other Settings -> Configuration -> Scripting Runtime Version.
```

<br>
<br>

**Get input:**  
```c#
// C#
string input = Console.ReadLine();


// Unity
// 1. Create new project: GetInput
// 2. Create an empty GameObject, Text, and Input Field
// 3. Create script: GetInput
// 4. Attach script to GameObject
// 5. Write script
// 6. Attach Text and Input Field to the GetInput script on GameObject in the inspector

using UnityEngine;
using UnityEngine.UI;

public class GetInput : MonoBehaviour {

    public InputField inputField;
    public Text textDisplay;

    void Start ()
    {
        inputField.onEndEdit.AddListener(ProcessUserInput);
        inputField.ActivateInputField();
    }

    void ProcessUserInput(string userInput)
    {
        textDisplay.text = userInput;
        Debug.Log(userInput);
        inputField.ActivateInputField();
        inputField.text = null;
    }
}
```

<br>
<br>

**Type conversion:**  
```c#
// Cast float to int
float x = 1234.7f;
int a = (int)x;


// Convert input (does not account for an exception)
int input = Convert.ToInt32(Console.ReadLine());


// Convert input (accounts for an exception)
using System;
public class ConvertInput {
    public static void Main()
    {
        string consoleInput;
        int input;
	
        do
        {
            //Console.WriteLine("Enter a number: ");
            consoleInput = Console.ReadLine();
        } while (!int.TryParse(consoleInput, out input));
	
        // input is now == (int)consoleInput
    }
}
```

<br>
<br>

**Methods:**
```c#
// Creating a method
dataTypeMethodReturns MethodName(parameters){}

// Calling a method
Class.Method(arguments);
```

<br>
<br>

**Array** - A data structure with a fixed size used to store variables of the same type.
```c#
datatype[] arrayName = new datatype[size] { value, value.. };

int numbers = new int[] { 1, 2, 3 };

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

**Dictionary** - Holds a collection of key-value pairs called pairs.
```c#
// Create a dictionary
Dictionary<keytype, valuetype> dictName = new Dictionary<keytype, valuetype>();

// Add to a dictionary
dictName.Add(key,value);

// Access values by their keys
Console.WriteLine(dictName[key]);

// Loop through dictionary
foreach (KeyValuePair<keytype, valuetype> pair in dictName)
{
    Console.WriteLine($"Key: {pair.Key}, Value: {pair.Value}");
}
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
modifier class ClassName{}


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
    john.Talk(string "Hello!");
```

<br>

### Static modifier:
**Static classes:**  
To use a non-static class you need to create an object of the class. A static class cannot be instantiated, in other words, you cannot use the new keyword to create a variable of the class type. Because they are not instantiatable, you access the members of a static class by using the class name itself. Static classes are used to hold shared variables and methods. Since there will be only one instance of it everything will use that one shared set of variables and methods.

**Static members:**  
You can't access static members from objects. When an object is made anything static is removed from the object so it does not get any of the static things. Static members exist only in the class and are accessed the same way as from a static class.

Example of a static member:
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
public abstract class Painting
{
    public abstract void LookAtPainting();
}


public class RealismPainting : Painting
{
    public override void LookAtPainting()
    {
        ShowRealismPainting();
    }
}


public class SurrealismPainting : Painting
{
    public override void LookAtPainting()
    {
        ShowSurrealismPainting();
    }
}
```

<br>
<br>

---

<br>
<br>

### Properties:
A class member that provides access to fields of a class. A get property accessor is used to return the value, and a set property accessor is used to assign a new value.
```c#
// Create a property:
// prop + Tab


class Customer
{
    public double TotalPurchases { get; set; }
    public string Name { get; set; }
    public int CustomerID { get; set; }

    // Constructor
    public Customer(double purchases, string name, int ID)
    {
        TotalPurchases = purchases;
        Name = name;
        CustomerID = ID;
    }
}

class Program
{
    static void Main()
    {
        // Intialize a new object.
        Customer cust1 = new Customer (4987.63, "Northwind", 90108);

        //Modify a property
        cust1.TotalPurchases += 499.99;
    }
}


// Initialize an auto-implemented property:
public string FirstName { get; set; } = "Jane";
```

<br>

### Attributes:
Attributes add metadata to your program. Metadata is information about the types defined in a program.

A declarative tag that is used to convey information to runtime about the behaviors of various elements like classes, methods, structures, enumerators, etc. in your program.
```c#
// Declaring an attribute:
[attribute(positional_parameters, name_parameter = value, ...)] element;

[HideInInspector] public RoomNavigation roomNavigation;
```

<br>
