# Directory

An abstract representation of a directory. When creating an instance of a Directory, it does not mean that such directory will be created. It only verifies if the directory has a valid name. Directory also converts backslashes into slashes to make sure paths are represented in the same way in different operational systems. This type provides a set of operations to handle directories, such as to verify if it exists, create, and remove.  
  

### Arguments

- **name**: A mandatory string with the directory name. It can also be a [File](./file.md). In this case, its value will be [File:path()](./file.md#path). This argument can be used as a first argument in a call to Directory without named arguments, as in the example below.
- **tmp**: An optional boolean value indicating whether the directory should be temporary. The default value is false. When creating a temporary directory, the end of its name must contain X's, which are going to be replaced by random alphanumerical values in order to guarantee that the created directory will not replace a previous one.

### Usage

```
dir = Directory("/my/path/my_dir")

tmpDir = Directory{
   name = "mytmpdir_XXX",
   tmp = true
}

print(tmpDir)
```

---

## Functions

|                                                                               |                                                                                                                           |
| ----------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------- |
| [attributes](./directory.md#attributes)       | Return a table with the file attributes corresponding to filepath (or nil followed by an error message in case of error). |
| [create](./directory.md#create)               | Create the directory.                                                                                                     |
| [delete](./directory.md#delete)               | Remove an existing directory.                                                                                             |
| [exists](./directory.md#exists)               | Return whether the directory is stored in the computer.                                                                   |
| [list](./directory.md#list)                   | Return a vector of strings with the content of the directory.                                                             |
| [name](./directory.md#name)                   | Return the name of a given directory.                                                                                     |
| [path](./directory.md#path)                   | Return the path of a given directory.                                                                                     |
| [relativePath](./directory.md#relativepath)   | Return a relative path given a small path.                                                                                |
| [setCurrentDir](./directory.md#setcurrentdir) | Set the current working directory with the directory path.                                                                |
| [..](./directory.md#..)                       | Concatenate the directory.                                                                                                |


---

## **attributes** 

Return a table with the file attributes corresponding to filepath (or nil followed by an error message in case of error). If the second optional argument is given, then only the value of the named attribute is returned. The attributes are described as follows; attribute mode is a string, all the others are numbers, and the time related attributes use the same time reference of os.time. This function uses stat internally thus if the given filepath is a symbolic link, it is followed (if it points to another link the chain is followed recursively) and the information is about the file it refers to.  
  

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
Directory(packageInfo("base").path.."data"):attributes("mode")
```

---

## **create** 

Create the directory. Returns true if the operation was successful. In case of error, it returns nil plus an error string.  
  

### Usage

```
dir = Directory("mydirectory")
dir:create()
print(dir)

tmpDir = Directory{
   name = "mytmpdir_XXX",
   tmp = true
}

print(tmpDir)

dir:delete()
tmpDir:delete()
```

---

## **delete** 

Remove an existing directory. It removes all internal files and directories recursively. If the directory does not exist or it cannot be removed, this function stops with an error.  
  

### Usage

```
dir = Directory("mydirectory")
dir:create()
dir:delete()
```

---

## **exists** 

Return whether the directory is stored in the computer.  
  

### Usage

```
if Directory("C:\\TerraME\\bin"):exists() then
    print("is dir")
end
```

---

## **list** 

Return a vector of strings with the content of the directory.  
  

### Arguments

- **#1**: A boolean value indicating whether hidden files should be returned. The default value is false.

### Usage

```
files = packageInfo("base").data:list()

forEachElement(files, function(_, file)
    print(file)
end)
```

---

## **name** 

Return the name of a given directory. It is the last directory name given a full path.  
  

### Usage

```
print(Directory("c:\\terrame\\bin\\"):name()) -- "bin"

print(Directory("/usr/local/bin"):name()) -- "bin"
```

---

## **path** 

Return the path of a given directory. In windows, it converts all backslashes into slashes.  
  

### Usage

```
print(Directory("c:\\terrame\\bin\\"):path()) -- "c:/terrame"

print(Directory("/usr/local/bin"):path()) -- "/usr/local"
```

---

## **relativePath** 

Return a relative path given a small path.  
  

### Arguments

- **#1**: A Directory or a string with a shorter path.

### Usage

```
d = Directory("/my/full/path")
print(d:relativePath("/my")) -- "full/path"
```

---

## **setCurrentDir** 

Set the current working directory with the directory path. Returns true in case of success or nil plus an error string.  
  

### Usage

```
Directory("c:\\tests"):setCurrentDir()
```

---

## **..** 

Concatenate the directory. It adds a path separator whenever needed.  
  

### Arguments

- **#1**: A string or an object that can be concatenated.

### Usage

```
path = sessionInfo().path.."data"
```