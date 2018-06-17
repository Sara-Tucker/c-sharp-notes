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
using System.Linq;

// Arrays:
var dictName = Enumerable.Range(0, keysArray.Length).ToDictionary(i => keysArray[i], i => valuesArray[i]);

// Lists:
var dictName = Enumerable.Range(0, keysList.Count).ToDictionary(i => keysList[i], i => valuesList[i]);
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
