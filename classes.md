# Classes and inheritance:

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

    // Constructor
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
    public override void Speak()
    {
        Console.WriteLine("Meow");
    }
}

public class Dog : Animal
{     
    public override void Speak()
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
