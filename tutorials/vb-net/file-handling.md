---
PermaID: 100037
Name: File Handling
---

# File Handling

In most of the applications, you will see that file is used to store the data. The file handling term is used when different operations are performed, such as;

 - Creating the file
 - Opening the file
 - Reading data from the file
 - Writing data to the file
 - Appending data to the file, etc. 
 
VB.NET provides `System.IO.File`class, which contains static methods for operations the creation, copying, deletion, moving, and opening of a single file.

Here are the most commonly used methods of the `File` class which are very useful for creating and getting information about files.

| Method          | Description                                            |
|:----------------|:-------------------------------------------------------|
| AppendAllLines()| Appends lines to a file, and then closes the file. If the specified file does not exist, this method creates a file, writes the specified lines to the file, and then closes the file. |
| AppendAllText() | Opens a file, appends the specified string to the file, and then closes the file. If the file does not exist, this method creates a file, writes the specified string to the file, then closes the file. |
| AppendText()    | Appends text at the end of an existing file, or to a new file if the specified file does not exist.            |
| Copy()          | Copies an existing file to a new file.                 |
| Create()        | Creates or overwrites a file in the specified path.    |
| Delete()        | Deletes the specified file.                            |
| Exists()        | Determines whether the specified file exists.          |
| Move()          | Moves a specified file to a new location, providing the option to specify a new file name. |
| Open()          | Opens a FileStream on the specified path with reading/write access with no sharing. |
| ReadAllLines()  | Opens a text file, reads all lines of the file, and then closes the file. |
| ReadAllText()   | Opens a text file, reads all the text in the file, and then closes the file. |
| ReadLines()     | Reads the lines of a file.                             |
| Replace()       | Replaces the contents of a specified file with the contents of another file, deleting the original file, and creating a backup of the replaced file. |
| WriteAllLines() | Creates a new file, writes a collection of strings to the file, and then closes the file. |
| WriteAllText()  | Creates a new file and writes the contents to it. If the file already exists, it will be overwritten.|

Let's consider the following simple example, where the simple string is written to the file using the `WriteAllText()` method and then reads all the contents from the file using the `ReadAllText()` method.

```csharp
Private Sub Example1()
    Dim writeText As String = "This is a VB.NET Tutorial, and you are learning file handling."

    'Create a file and write the content of writeText to it
    File.WriteAllText("test.txt", writeText)

    'Read the contents from the file
    Dim readText As String = File.ReadAllText("test.txt")
    Console.WriteLine(readText)
End Sub
```

Let's run the above code, and you will see the following output.

```csharp
This is a VB.NET Tutorial, and you are learning file handling.
```

Let's take another example in which we will use the `File` class to check whether a file exists or not, if a file exists we will open the file and read data from it, if the file doesn't exist we will create a new file, write some data to it and then read all the data from that file.

```csharp
Public Sub Example2()
    Dim path As String = "D:\MyTest.txt"

    If Not File.Exists(path) Then
        Console.WriteLine("File doesn't exist, we will create a file first." & vbLf)

        Using sw As StreamWriter = File.CreateText(path)
            sw.WriteLine("This is a VB.NET Tutorial,")
            sw.WriteLine("and you are learning")
            sw.WriteLine("file handling.")
        End Using
    Else
        Console.WriteLine("File already exists, no need to create it." & vbLf)
    End If

    Using sr As StreamReader = File.OpenText(path)
        Dim s As String
        s = sr.ReadLine()
        While (s IsNot Nothing)
            Console.WriteLine(s)
            s = sr.ReadLine()
        End While
    End Using
End Sub
```

Let's run the above code and you will see the following output.

```csharp
File doesn't exist, we will create a file first.

This is a VB.NET Tutorial,
and you are learning
file handling.
```

As you can see, the file doesn't exist for the first time, so first the file is created. Now, if you rerun the code, you will see that it won't create a file.

```csharp
File already exists, no need to create it.

This is a VB.NET Tutorial,
and you are learning
file handling.
```
