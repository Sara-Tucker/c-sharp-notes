# C# Loops:

## for loop:
Repeats a codeblock until a condition evaluates to false. Used when you know when to stop looping because you know the condition that needs to change.
```c#
// Create a for loop:
// for + Tab + Tab

for (initializer; condition; iterator)
    codeblock

//Example:
for (i = 1; i <= 5; i++)
    codeblock
```

<br>

## foreach loop:
Executes a codeblock for each element in a collection. Used when you know when to stop looping because you know it will loop until every element has been iterated over.
```c#
foreach (datatype elementName in collectionName)
    codeblock

foreach (int purchase in myReceipt)
    codeblock
```

<br>

## while loop:
Repeats a codeblock until a condition evaluates to false.

How to make:  
The while condition should be made with: ==  or  >  or  <  
The condition should be defined outside of the loop.  
The code block will alter a variable that is part of the condition.  
Eventually the condition will evaluate to false.
```c#
defined condition;
while (condition is true)
    //codeblock


int count = 0;
while (int count < 5)
{
    Console.WriteLine(count);
    count++;
}


bool finished = false;
while (finished == false)
{
    if (condition)
        finished = true;
    else
    {
        //codeblock
    }
}
```

<br>

## do-while loop:
```c#
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

## break statement:
The break statement terminates the entire loop.

Weird example..
```c#
int[] numbers = { 0, 1, 2, 3, 4, 5, 6, 7, 8, 9 };
char[] letters = { 'a', 'b', 'c', 'd', 'e', 'f', 'g', 'h', 'i', 'j' };

for (int x = 0; x < numbers.Length; x++)
{
    Console.WriteLine("num = {0}", numbers[x]);

    for (int y = 0; y < letters.Length; y++)
    {
        if (y == x)
        {
            break;
            // the break is used only once, to skip printing the letter 'a' at 0
            // its a weird example.
        }
        Console.Write("{0}", letters[y]);
    }
    Console.WriteLine();
}

// Output:
// num = 0
// num = 1
//  a
// num = 2
//  a  b
// num = 3
//  a  b  c
```

<br>
<br>

## continue statement:
The continue statement passes control to the next iteration of the loop.
```c#
for (int i = 1; i <= 10; i++)
{
    if (i < 9)
    {
        continue;
    }
    Console.WriteLine(i);
}

// Output:
// 9
// 10
```
