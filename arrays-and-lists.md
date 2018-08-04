# Array
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
    int max = arrayName.Max();
    int min = arrayName.Min();

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


// Operations with two arrays:
    int[] a = new int[3] { 1, 2, 3 };
    int[] b = new int[3] { 4, 5, 6 };
    int[] aTimesB = new int[3];
    
    for (int i; i <= a.Length; i++)
        aTimesB[i] = a[i] * b[i];
    //prints 4, 10, 18
```

<br>

#### Multidimensional arrays:
```c#
// Rectangular: (3x5)
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

// Declare the Jagged array above:
int[] numbers = int[3][];
numbers[0] = new int[4];
numbers[1] = new int[5];
numbers[2] = new int[3];
```

<br>
<br>
<br>

# List
A data structure with a dynamic size used to store variables of the same type.  
List\<T\> &nbsp;&nbsp;T = element type (data type)

<br>

#### Create a list:
```c#
// Create a list:
    List<T> listName = new List<T>() { item1, item2, itemN };
    List<T> listName = new List<T>();
    
// Shallow copy a list:
    List<T> newList = new List<T>(sourceList);
```

<br>

#### Access objects in a list:
```c#
// Access an object in a list:
    list[0];
    
// Last indices:
    list[list.Count - 1];

// Print all items in a list on seperate lines:
    foreach (elementName in collectionName)
        Console.WriteLine(elementName);

// Access lists in a list: ?
```

<br>

#### Find:
```c#
// Find number of objects in a list:
    listName.Count;

// Find the largest and smallest elements in a list:
    int max = listName.Max();
    int min = listName.Min();

// Search for a specified object and return the index of its first occurrence:
    int index = listName.IndexOf(value);
```

<br>

#### Other:
```c#
// Add an object to the end of a list:
    numbers.Add(6);

// Remove the first occurrence of an object:
    listName.Remove(value);

// Remove the object at an index:
    listName.RemoveAt(index);


// Sort a list from smallest to largest or alphabetically:
    listName.Sort();

// Remove duplicates from a list:
    var newList = new HashSet<T>(oldList).ToList();


// Operations with two lists:
    List<int> a = new List<int>() { 1, 2, 3 };
    List<int> b = new List<int>() { 4, 5, 6 };
    List<int> aTimesB = new List<int>();
    
    for (int i; i <= a.Count; i++)
        aTimesB.Add(a[i] * b[i]);
    //prints 4, 10, 18
```

<br>

#### List Comprehensions:  
Create new lists where each item is the result of some operation applied to each member of another list
```python
a = [1, 2, 3]
doubled_a = [i * 2 for i in a]
#prints 2, 4, 6

# Take a list where elements are a fucked up float decimal and
# change to 2 decimals while still remaining a float type
list_name = [float('%.2f' % i) for i in list_name]


# Remove items from a list while iterating
new_list = [x for x in old_list if determine(x)]
new_list = [x for x in old_list if not determine(x)]

same_list[:] = [x for x in same_list if determine(x)]
same_list[:] = [x for x in same_list if not determine(x)]
# same but makes a copy of the list, then overwrites it

for (int i = 0; i < numbers.Count; i++)
{
    if (numbers[i] == 1)
        numbers.Remove(numbers[i]);
}
```
