# Files

The File and FileInfo classes provide methods for creating, copying, deleting, moving, and opening files.

Methods with no examples yet:
```
Create()
GetAttributes()
Move()
```

<br>

### File:
File provides static methods. It makes programming faster since methods are static, but it's slower to run because the operating system has to do security checks to see if you can access a file.

```c#
string pathName = @"c:\temp\myfile.txt";
```

### Read a file:
```c#
//Read the file as one string:
string text = File.ReadAllText(pathName);


//Create an array where each element is one line of the file:
string[] lines = File.ReadAllLines(pathName);

foreach (string line in lines)
{
    Console.WriteLine(line);
}
```

<br>

### Write to a file:
```c#
//Overwrite with an array of strings:
string[] lines = { "First line", "Second line", "Third line" };
File.WriteAllLines(pathName, lines);
//File.WriteAllText(pathName, string);


//Append new text to an existing file:
using (StreamWriter file = new StreamWriter(pathName, true))
{
    file.WriteLine("Fourth line");
}
```
<br>

### Other:
```c#
// File.Copy()
File.Copy(pathName, @"c:\temp\newtext.txt");


// File.Delete()
File.Delete(pathName);


// File.Exists()
if (File.Exists(pathName))
{
    //
}
```

<br>

### File.Copy()
```c#
File.Copy(pathName, @"c:\temp\newtext.txt");
```

### File.Delete()
```c#
File.Delete(pathName);
```

### File.Exists()
```c#
if (File.Exists(pathName))
{
    //
}
```

### File.ReadAllText()
Read the file as one string.
```c#
string text = File.ReadAllText(pathName);
```

### File.ReadAllLines()
Creates an array where each element is one line of the file.
```c#
string[] lines = File.ReadAllLines(pathName);

foreach (string line in lines)
{
    Console.WriteLine(line);
}
```

### File.WriteAllLines()
```c#
// There's also WriteAllText (string instead of string[])

string[] lines = { "First line", "Second line", "Third line" };
File.WriteAllLines(pathName, lines);
```

### Append new text to an existing file
```c#
using (StreamWriter file = new StreamWriter(pathName, true))
{
    file.WriteLine("Fourth line");
}
```

<br>

### FileInfo:
FileInfo provides instance methods.
```c#
// Instantiate
FileInfo file = new FileInfo(@"c:\temp\myfile.txt");


// .CopyTo()
file.CopyTo(@"c:\temp\text.txt");


// .Delete()
file.Delete();


// .Exists Property
if (file.Exists)
{
    //
}
```

<br>
<br>

---

<br>
<br>

Methods with no examples yet:
```
Delete()
Move()
GetLogicalDrives()
```

<br>

### Directory:
Directory provides static methods.
```c#
// Directory.CreateDirectory()
string directoryName = @"c:\temp\folder1";
Directory.CreateDirectory(directoryName);


// Directory.GetFiles()
string[] files = Directory.GetFiles(directoryName, *.*, SearchOption.AllDirectories); //*.jpg, *.txt, etc
foreach (string file in files)
    Console.WriteLine(file);


// Directory.GetDirectories()
string[] directories = Directory.GetDirectories(directoryName, *.*, SearchOption.AllDirectories);
foreach (string directory in directories)
    Console.WriteLine(directory);


// Directory.Exists()
if (Directory.Exists(directoryName))
{
    //
}
```

<br>

### DirectoryInfo:
DirectoryInfo provides instance methods.
```c#
// Instantiate
DirectoryInfo directory = new DirectoryInfo(@"c:\temp\folder1");


// .GetFiles()
string[] files = directory.GetFiles(*.*, SearchOption.AllDirectories); //*.jpg, *.txt, etc
foreach (string file in files)
    Console.WriteLine(file);


// .GetDirectories()
string[] directories = directory.GetDirectories(*.*, SearchOption.AllDirectories);
foreach (string dir in directories)
    Console.WriteLine(dir);


// .Exists Property
if (directory.Exists)
{
    //
}
```

<br>
<br>
<br>

### Path Class
The Path class provides static methods for working with a string that is a directory or file path.
```c#
Console.WriteLine(Path.GetFileName(pathName));
Console.WriteLine(Path.GetFileNameWithoutExtension(pathName));
Console.WriteLine(Path.GetExtension(pathName));
Console.WriteLine(Path.GetDirectoryName(pathName));
tempPath = Path.GetTempPath(); // - user's temp folder
```
