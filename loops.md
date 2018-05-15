### For Loop:
Repeats a codeblock until a condition evaluates to false. Used when you know when to stop looping because you know the condition that needs to change.
```c#
// Create a for loop:
// for + Tab + Tab

for (initializer; condition; iterator)
    codeblock

for (i = 1; i <= 5; i++)
    codeblock
```

<br>

### foreach Loop:
Executes a codeblock for each element in an array. Used when you know when to stop looping because you know it will loop until every element has been iterated over.
```c#
foreach (Datatype elementName(i) in listName)
    codeblock

foreach (int purchase in myReceipt)
    codeblock
```

<br>

### While Loop:
Repeats a codeblock until a condition evaluates to false.

How to make:  
The while condition should be made with: ==  or  >  or  <  
The condition should be defined outside of the loop.  
The code block will alter a variable that is part of the condition.  
Eventually the condition will evaluate to false.
```c#
defined condition;
while (condition is true)
    codeblock

int count = 0;
while (int count < 5)
    Console.WriteLine(count);
    count++;
```

<br>
<br>

### Use break statements !!
