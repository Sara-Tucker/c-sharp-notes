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
Copy()
Delete()
Exists()
GetAttributes()
Move()
ReadAllText()
```

DirectoryInfo - provides instance methods
Directory - provides static methods

Methods:
```
CreateDirectory()
Delete()
Exists()
GetCurrentDirectory()
GetAllFiles()
Move()
GetLogicalDrives()
```


Path Class:  
Works with a string that is a directory or file path.

Methods:
```
GetDirectoryName()
GetFileName()
GetExtension()
GetTempPath() - user's temp folder
```
