## Array
A data structure with a fixed size used to store variables of the same type.

<br>

```c#
// Create an array:
datatype[] arrayName = new datatype[size] { value, value.. };
int[] numbers = new int[] { 3, 4, 5 };


// Access an object in an array:
numbers[0]; // == 3


// Find number of objects in an array:
Console.WriteLine(arrayName.Length);


// Searches for the specified object and returns the index of its first occurrence (for 1D arrays)
int index = Array.IndexOf(arrayName, value);


// Sets a range of elements in an array to the default value of each element type:
Array.Clear(arrayName, Starting Index, Number of elements to clear);


// Copy an array:
int[] newArray = new int[3];
Array.Copy(sourceArray, newArray, Num of elements to copy);


// Sort an array from smallest to largest or alphabetically:
Array.Sort(arrayName);



// Multidimensional arrays:
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
```

<br>
<br>
