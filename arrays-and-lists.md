## Array
A data structure with a fixed size used to store variables of the same type.

<br>

#### Create an array:
```c#
// Create an array:
    datatype[] arrayName = new datatype[size] { item1, item2, itemN };
    datatype[] arrayName = new datatype[size];

// Copy an array:
    Array.Copy(sourceArray, newArray, Num of elements to copy);
```

<br>

#### Access objects in an array:
```c#
// Access an object in a array:
    array[0];
    
// Last indices:
    array[array.Length - 1];

// Print all items in an array on seperate lines:
    foreach (elementName in collectionName)
        Console.WriteLine(elementName);
```

<br>

#### Find:
```c#
// Find number of objects in an array:
    arrayName.Length;

// Find the largest and smallest elements in an array:
    int max = array.Max();
    int min = array.Min();

// Search for a specified object and return the index of its first occurrence:
    int index = Array.IndexOf(arrayName, value);
```

<br>

#### Other:
```c#
// Sort an array from smallest to largest or alphabetically:
    Array.Sort(arrayName);

// Set a range of elements in an array to the default value of its element type:
    Array.Clear(arrayName, Starting Index, Number of elements to clear);
```

<br>

#### Multidimensional arrays:
```c#
// Rectangular: (5x3)
 0 1 2 3 4
 0 1 2 3 4
 0 1 2 3 4

// 2D and 3D arrays
int[] matrixNums = int[3, 5];
int[] matrixNums = int[3, 5, 2];

// Jagged: (an array of arrays) (each row is an array)
 0 1 2 3
 0 1 2 3 4
 0 1 2

// Declare above Jagged array:
int[] numbers = int[3][];
number[0] = new int[4];
number[1] = new int[5];
number[2] = new int[3];
```

<br>
<br>
<br>

## List
A data structure with a dynamic size used to store variables of the same type.

<br>

```c#
// Create a list:
List<datatype> listName = new List<datatype>() { value, value.. };
List<int> numbers = new List<int>() { 3, 4, 5 };


// Access an object in a list:
numbers[0]; // == 3


// Add an object to the end of a list:
numbers.Add(6);


// Find number of objects in a list:
Console.WriteLine(numbers.Count);


// Searches for the specified object and returns the index of the first occurrence within the entire list:
listName.IndexOf(value);


// Remove an object from a list:
listName.Remove(value);


// You can't use a foreach loop on lists in C#, you have to use a for loop.
for (int i = 0; i < numbers.Count; i++)
{
    if (numbers[i] == 1)
        numbers.Remove(numbers[i]);
}
```

<br>
<br>
