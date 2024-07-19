# File

An abstract representation of a file. Whenever an instance of File is created, it only verifies whether it is possible to have a file with the given name and if its directory exists (in case of explicitly specified). It will not stop with an error if the file does not exist. The file is only opened when a read function is called. The file is only created if a write function is called.  
  

### Arguments

- **name**: A string with the file name. This argument is mandatory.

### Usage

```
file = File("agents.csv")
```

---

## Functions

|                                                                            |                                                                                                                           |
| -------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------- |
| [attributes](./file.md#attributes)         | Return a table with the file attributes corresponding to filepath (or nil followed by an error message in case of error). |
| [close](./file.md#close)                   | Close an opened file.                                                                                                     |
| [copy](./file.md#copy)                     | Copy the file to a given destination.                                                                                     |
| [delete](./file.md#delete)                 | Remove an existing file.                                                                                                  |
| [deleteIfExists](./file.md#deleteifexists) | Remove a file if it exists.                                                                                               |
| [exists](./file.md#exists)                 | Return whether the file stored in the computer.                                                                           |
| [extension](./file.md#extension)           | Return the extension of the file.                                                                                         |
| [hasExtension](./file.md#hasextension)     | Return a boolean value if the file has an extension.                                                                      |
| [name](./file.md#name)                     | Return the file name removing its path.                                                                                   |
| [open](./file.md#open)                     | Open the file for reading or writing.                                                                                     |
| [path](./file.md#path)                     | Return the path to the file.                                                                                              |
| [read](./file.md#read)                     | Read a file.                                                                                                              |
| [readLine](./file.md#readline)             | Read a line from the file.                                                                                                |
| [split](./file.md#split)                   | Split the path, name, and extension of the file into three returning values.                                              |
| [touch](./file.md#touch)                   | Set access and modification times for the file.                                                                           |
| [write](./file.md#write)                   | Write a given [DataFrame](./dataFrame.md) into the file.                                  |
| [writeLine](./file.md#writeLine)           | Write a given string or table into the file.                                                                              |
| [..](./file.md#..)                         | Concatenate the file.                                                                                                     |

---

## **attributes** 

Return a table with the file attributes corresponding to filepath (or nil followed by an error message in case of error). The attributes are described as follows; attribute mode is a string, all the others are numbers, and the time related attributes use the same time reference of os.time. This function uses stat internally thus if the given filepath is a symbolic link, it is followed (if it points to another link the chain is followed recursively) and the information is about the file it refers to.  
  

### Arguments

- **#1**: A string with the name of the attribute to be read.

| Attribute      | Description                                                                                                                                            |
| -------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------ |
| "dev"          | on Unix systems, this represents the device that the inode resides on. On Windows systems, represents the drive number of the disk containing the file |
| "ino"          | on Unix systems, this represents the inode number. On Windows systems this has no meaning                                                              |
| "mode"         | string representing the associated protection mode (the values could be file, directory, link, socket, named pipe, char device, block device or other) |
| "nlink"        | number of hard links to the file                                                                                                                       |
| "uid"          | user-id of owner (Unix only, always 0 on Windows)                                                                                                      |
| "gid"          | group-id of owner (Unix only, always 0 on Windows)                                                                                                     |
| "rdev"         | on Unix systems, represents the device type, for special file inodes. On Windows systems represents the same as dev                                    |
| "access"       | time of last access                                                                                                                                    |
| "modification" | time of last data modification                                                                                                                         |
| "change"       | time of last file status change                                                                                                                        |
| "size"         | file size, in bytes                                                                                                                                    |
| "blocks"       | block allocated for file; (Unix only)                                                                                                                  |
| "blksize"      | optimal file system I/O blocksize; (Unix only)                                                                                                         |

### Usage

```
filePath("river.shp"):attributes("mode")
```

---

## **close** 

Close an opened file.  
  

### Usage

```
file = File("abc.txt")
file:close()
```

---

## **copy** 

Copy the file to a given destination.  
  

### Arguments

- **#1**: A [Directory](./directory.md) or a string with the destination path. It can also be a File with the destination. If the file to be copied is a shapefile, it also copies the respective dbf, shx, prj, and qix files if they exist.

### Usage

```
path = Directory("c:/mypath")
file = File(path.."file.lua")
file:copy(File(path.."file2.lua")) -- from c:/mypath/file.lua to c:/mypath/file2.lua
```

---

## **delete** 

Remove an existing file. If the file does not exist or it cannot be removed, this function stops with an error. If the file to be removed is a shapefile, it also removes the respective dbf, shx, prj, and qix files if they exist.  
  

### Usage

```
filename = "myfile.txt"
file = File(filename)
file:writeLine("Some text..")
file:close()
file:delete()
```

---

## **deleteIfExists** 

Remove a file if it exists. It does not stop with an error when the file does not exist. This function returns the File itself.  
  

### Usage

```
filename = "myfile.txt"
file = File(filename)
file:writeLine("Some text..")
file:close()
file:deleteIfExists()

file = File(filename):deleteIfExists() -- ensure that "myfile.txt" does not exist when 'file' is created
```

---

## **exists** 

Return whether the file stored in the computer.  
  

### Usage

```
file = filePath("agents.csv", "base")
print(file:exists())
```

---

## **extension** 

Return the extension of the file. It returns the substring after the last dot. If it does not have a dot, an empty string is returned.  
  

### Usage

```
file = filePath("agents.csv", "base")
print(file:extension()) -- "csv"
```

---

## **hasExtension** 

Return a boolean value if the file has an extension.  
  

### Usage

```
file = filePath("agents.csv", "base")
print(file:hasExtension()) -- true
```

---

## **name** 

Return the file name removing its path.  
  

### Usage

```
file = filePath("agents.csv", "base")
print(file:name()) -- "agents.csv"
```

---

## **open** 

Open the file for reading or writing. An opened file must be closed after being used.  
  

### Arguments

- **#1**: A string with the mode. It can be "w" for writing or "r" for reading.

### Usage

```
file = File("myfile.txt")
file:open()
```

### See also

- [close](./file.md#close)

---

## **path** 

Return the path to the file.  
  

### Usage

```
file = filePath("agents.csv", "base")
print(file:path())
```

---

## **read** 

Read a file. It returns a vector (whose indexes are line numbers) containing named tables (whose indexes are attribute names). The first line of the file list the attribute names. This function automatically closes the file.  
  

### Arguments

- **#1**: A string with the separator. The default value is ','.

### Usage

```
file = filePath("agents.csv", "base")
csv = file:read()
print(csv[1].age) -- 20
```

---

## **readLine** 

Read a line from the file. It stores the position of the line internally in case of some error occur. Therefore no line number will be used as argument for this function.  
  

### Arguments

- **#1**: A string with the separator. Parse a single CSV line. It returns a vector of strings with the i-th value in the position i. This function was taken from [http://lua-users.org/wiki/LuaCsv.](http://lua-users.org/wiki/LuaCsv.)

### Usage

```
file = filePath("agents.csv", "base")
line = file:readLine(",")
print(line[1]) -- john
print(line[2]) -- 20
print(line[3]) -- 200

line = file:readLine()
print(line) -- "mary",18,100,3,1,false
```

---

## **split** 

Split the path, name, and extension of the file into three returning values.  
  

### Usage

```
file = filePath("agents.csv", "base")
directory, name, extension = file:split()
print(directory) -- "/base/data/"
print(name) -- "agents",
print(extension) -- "csv"
```

---

## **touch** 

Set access and modification times for the file. Times are provided in seconds (which should be generated with Lua standard function os.time). If the modification time is omitted, the access time provided is used; if both times are omitted, the current time is used. Returns true if the operation was successful; in case of error, it returns nil plus an error string.  
  

### Arguments

- **#1**: The new access time (in seconds).
- **#2**: The new modification time (in seconds).

### Usage

```
filePath("river.shp"):touch(0, 0)
```

---

## **write** 

Write a given [DataFrame](./dataFrame.md) into the file. It automatically closes the file after writing it.  
  

### Arguments

- **#1**: A DataFrame.
- **#2**: A string with the separator. The default value is ','.

### Usage

```
mytable = DataFrame{
    {age = 1, wealth = 10, vision = 2},
    {age = 3, wealth =  8, vision = 1},
    {age = 3, wealth = 15, vision = 2}
}

file = File("file.csv")
file:write(mytable, ";")
file:deleteIfExists()
```

---

## **writeLine** 

Write a given string or table into the file. The file must be closed afterwards. It automatically adds an end of line to the file after the string.  
  

### Arguments

- **#1**: A string or table to be saved. A table it must be a vector with the values to be saved in a given line.
- **#2**: A string with the separator. The default value is ','.

### Usage

```
mytable = {"x", "y", "z"}

file = File("file.csv")
file:writeLine(mytable, ";")
file:writeLine("Some text..")
file:close()
file:deleteIfExists()
```

---

## **..** 

Concatenate the file.  
  

### Arguments

- **#1**: A string or an object that can be concatenated.

### Usage

```
print(File("abcd1234").." does not exist.")
```