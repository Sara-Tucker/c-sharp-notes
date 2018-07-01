## Files

File, FileInfo Classes:  
Provide methods for creating, copying, deleting, moving, and opening files.

FileInfo - provides instance methods  
File - provides static methods

File:
faster to program since methods are static, but slower to run because the operating system has to do security checks to see if you can access a file.

Methods:
```
Create()
GetAttributes()
Move()
```

### File:
```c#
string pathName = @"c:\temp\myfile.txt";


// File.Copy()
File.Copy(pathName, @"c:\temp\newtext.txt");


// File.Delete()
File.Delete(pathName);


// File.Exists()
if (File.Exists(pathName))
{
    //
}

// File.ReadAllText()
string text = File.ReadAllText(pathName);
```

### FileInfo:
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


DirectoryInfo - provides instance methods
Directory - provides static methods

Methods:
```
Delete()
Move()
GetLogicalDrives()
```


### Directory:
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

### DirectoryInfo:
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




Path Class:  
Works with a string that is a directory or file path.

### Path
```c#
Console.WriteLine(Path.GetFileName(pathName));
Console.WriteLine(Path.GetFileNameWithoutExtension(pathName));
Console.WriteLine(Path.GetExtension(pathName));
Console.WriteLine(Path.GetDirectoryName(pathName));
tempPath = Path.GetTempPath(); // - user's temp folder
```
