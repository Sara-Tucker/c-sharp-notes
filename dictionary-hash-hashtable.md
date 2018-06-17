# Dictionary / Hash / Hash Table:
Holds a collection of key-value pairs called pairs.

using System.Collections.Generic;

<br>

#### Create a dictionary:
```c#
Dictionary<keytype, valuetype> dictName = new Dictionary<keytype, valuetype>();

var dictName = new Dictionary<string, int>
{
    ["one"] = 1,
    ["two"] = 2,
    ["three"] = 3
};
```


// Add to a dictionary
dictName.Add(key,value);

// Access values by their keys
Console.WriteLine(dictName[key]);

// Loop through dictionary
foreach (KeyValuePair<keytype, valuetype> pair in dictName)
{
    Console.WriteLine($"Key: {pair.Key}, Value: {pair.Value}");
}

if (dict.ContainsKey("four") == true)
{
    MessageBox.Show(dict["four"].ToString ());
}
    else
    {
        MessageBox.Show("Key does not exist");
    }
}

        if (values.TryGetValue("cat", out test)) // Returns true.
        {
            Console.WriteLine(test); // This is the value at cat.
        }

if (phonebook.ContainsKey("Alex"))
{
    Console.WriteLine("Alex's number is " + phonebook["Alex"]);
}

phonebook["Jessica"] = 4159484588;

var dictionary = new Dictionary<string, int>();
// Acquire keys and sort them.
var list = dictionary.Keys.ToList();
list.Sort();

https://msdn.microsoft.com/en-us/library/xfhwa508(v=vs.110).aspx?f=255&MSPPError=-2147217396&cs-save-lang=1&cs-lang=csharp#code-snippet-2



<br>

#### Create a dictionary from arrays or lists:
```c#
using System.Collections.Generic;

string[] keysArray = new string[] { "a", "b", "c" };
int[] valuesArray = new int[] { 1, 2, 3 };

List<string> keysList = new List<string>() { "a", "b", "c" };
List<int> valuesList = new List<int>() { 1, 2, 3 };


// Arrays: Only difference is array.Length
var dictName = new Dictionary<string, int>();
for (int index = 0; index < keysArray.Length; index++)
{
    dictName.Add(keysArray[index], valuesArray[index]);
}

// Lists: Only difference is list.count
var dictName = new Dictionary<string, int>();
for (int index = 0; index < keysList.Count; index++)
{
    dictName.Add(keysList[index], valuesList[index]);
}

// Simple version for either arrays or lists, but needs Linq imported.
using System.Linq;
var dictName = Enumerable.Range(0, array1.Length).ToDictionary(i => array1[i], i => array2[i]);

// All result in the same thing:
// Key: a, Value: 1
// Key: b, Value: 2
// Key: c, Value: 3
```

<br>

#### Access a value using its key:
```python
dictionaryName[key]
# outputs the value for that key
```

<br>

#### Delete a pair:
```c#
dictName.Remove(Key);
```

<br>

### Check if a key is in a dictionary: ???
```python
if key in dictionary.keys():
    print('dictionary[key])

# ????
print(value in dictionaryName.keys())
```

<br>

### Check if a value is in a dictionary: ???
```python
print(key in dictionaryName.values())
```

<br>

### Loop through dictionary:
All items will be processed but in random order.
```python
for key in dictionaryName:
	print('The value for {} is {}.'.format(key, dictionaryName[key]))
# actually use the word key instead of i
```

<br>

### Loop with two variables: (same as above)
```python
for key, value in dictionaryName.items():
	print('The value for {} is {}.'.format(key, value))
# actually use the words key and value instead of i
```

<br>

Advanced dictionary stuff, like web and idk- https://www.datacamp.com/community/tutorials/python-dictionary-tutorial
