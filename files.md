# Paths and directories
```
cwd - current working directory (abbreviation, not a keyword)  
./  - the cwd  
../ - the parent folder
```

<br>

#### Absolute and relative paths
```c#
// Absolute path = full path name
string pathName = "D:/zCsharp/currentfolder/subfolder/file.type"

// Relative path = the program’s cwd is inferred as the start of the path
string pathName = "./file.type"
string pathName = "./subfolder/file.type"
```

<br>

### Directory:
Directory provides static methods.
```c#
// Create Directory objects to make reusing easier
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


//Methods with no examples yet:
//Delete()
//Move()
//GetLogicalDrives()
```

<br>

### DirectoryInfo:
DirectoryInfo provides instance methods.
```c#
// Instantiate
DirectoryInfo directory = new DirectoryInfo(@"c:\temp\folder1");


// .GetFiles()
FileInfo[] files = directory.GetFiles("*.", SearchOption.AllDirectories); //*.jpg, *.txt, etc
foreach (FileInfo file in files)
    Console.WriteLine(file.Name);


// .GetDirectories()
string[] directories = directory.GetDirectories(*.*, SearchOption.AllDirectories);
foreach (string dir in directories)
    Console.WriteLine(dir);


// .Exists Property
if (directory.Exists)
{
    //
}

//Methods with no examples yet:
//Delete()
//Move()
//GetLogicalDrives()
```

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

<br>

---

<br>

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
// .ReadAllText - Returns the file content as a single string
string text = File.ReadAllText(pathName);


// .ReadAllLines - Returns an array of strings, where each string is a line in the file
string[] lines = File.ReadAllLines(pathName);

foreach (string line in lines)
    Console.WriteLine(line);
```

<br>

### Write to a file:
```c#
// .WriteLine - Append a string to an existing file
using (StreamWriter file = new StreamWriter(pathName, true))
{
    file.WriteLine("Fourth line");
}


// .WriteAllLines - Overwrite a file with an array of strings
string[] lines = { "First line", "Second line", "Third line" };
File.WriteAllLines(pathName, lines);


File.WriteAllText(pathName, string);
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

#### Save variables:
