# OS

Functions to handle files and directories. Most of the functions bellow are taken from LuaFileSystem 1.6.2. Copyright Kepler Project 2003 ([https://keplerproject.github.io/luafilesystem](https://keplerproject.github.io/luafilesystem)).

## Functions

|                                                                    |                                                                                                          |
| ------------------------------------------------------------------ | -------------------------------------------------------------------------------------------------------- |
| [currentDir](./os.md#currentdir)   | Return a [Directory](../types/directory.md) with the current working directory. |
| [isDirectory](./os.md#isdirectory) | Return if a given path represents a directory that exists.                                               |
| [isFile](./os.md#isfile)           | Return if a given file path exists.                                                                      |
| [openWebpage](./os.md#openwebpage) | Opens a webpage in a Web Browser.                                                                        |
| [runCommand](./os.md#runcommand)   | Execute a system command and return its output.                                                          |
| [sessionInfo](./os.md#sessioninfo) | Return information about the current execution.                                                          |

---

## **currentDir** 

Return a [Directory](../types/directory.md) with the current working directory.  
  

### Usage

```
cdir = currentDir()
print(cdir)
```

---

## **isDirectory** 

Return if a given path represents a directory that exists.  
  

### Arguments

- **#1**: A string with a path.

### Usage

```
print(isDirectory("/home/user/mydirectory"))
```

---

## **isFile** 

Return if a given file path exists.  
  

### Arguments

- **#1**: A string with a file path.

### Usage

```
print(isFile("abc.lua"))
```

---

## **openWebpage** 

Opens a webpage in a Web Browser.  
  

### Arguments

- **#1**: A string with the webpage to be opened.

### Usage

```
openWebpage("www.terrame.org")
```

---

## **runCommand** 

Execute a system command and return its output. It returns two tables. The first one contains each standard output line as a position. The second one contains each error output line as a position.  
  

### Arguments

- **#1**: A command.

### Usage

```
result, error = runCommand("dir")
```

---

## **sessionInfo** 

Return information about the current execution. The result is a table with the values below. Some of them are read only, while others might be changed accordingly.  
  

| Attribute     | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     | Read only? |
| ------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------- |
| autoclose     | When a simulation creates graphical components ([Chart](../types/chart.md), [Map](../types/map.md), etc.), TerraME waits for the modeler to close them to finish its execution. This attribute is a boolean value indicating whether TerraME should be automatically closed after executing the simulation.                                                                                                                                                                                                                                                                                                                                                                                                                                                   | No         |
| color         | A boolean value indicating whether text output might be colored. If colored, errors are shown red, warnings are shown yellow, and some prints in executions like -test and -doc might be green. This option can only be set from TerraME command line (-color).                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 | Yes        |
| currentFile   | A [File](../types/file.md) with the name of the file currently being executed. This value only exists when the file is passed as argument to the command line.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         | Yes        |
| initialDir    | A [Directory](../types/directory.md) where TerraME was executed. Whenever TerraME needs to [import()](./package.md#import) a package and cannot find it in the installed packages, it tries to load from this directory.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               | Yes        |
| dbVersion     | A string with the current TerraLib version for databases.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       | Yes        |
| fullTraceback | A boolean value indicating whether TerraME should show all the stack when an error occurs. This means that the lines from base package and internal files are also going to be shown when an error occurs. As default, TerraME does not show such lines. This value can be set from TerraME command line (-ft).                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 | No         |
| graphics      | A boolean value indicating whether the graphics are enabled. If false and one creates a [Chart](../types/chart.md), [Map](../types/map.md), or any other object that has a graphical interface, it will not be shown. Because of that, it will not be possible to save the output from these objects. TerraME starts with graphics enabled (true).                                                                                                                                                                                                                                                                                                                                                                                                            | No         |
| interface     | A boolean value indicating whether a graphical interface to configure models is running. When this value is true, [toLabel()](./utils.md#tolabel) converts errors to more readable texts referring to graphical objects instead of [Model](../types/model.md) arguments.                                                                                                                                                                                                                                                                                                                                                                                                                                                                               | No         |
| mode          | A string with the current mode for warnings ("normal", "debug", "quiet", or "strict"). Run terrame -help for a description of such modes.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       | No         |
| path          | A string with the location of TerraME in the computer.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          | Yes        |
| round         | A number used whenever it is possible to have rounding problems. For instance, it works with [Events](../types/event.md) that have period less than one by rounding the execution time of an Event that is going to be scheduled to a future time if the difference between such time and the closest integer number is less then the value of this argument. In this case, if an Event that starts in time one and has period 0.1, it might execute in time 1.999999999, as we are working with real number. This argument is then useful to make sure that such Event will be executed in time exactly two. The default value is 1e-5. There is a function to compare numbers called [equals()](./utils.md#equals), that uses this value internally. | No         |
| separator     | A character with the directory separator. Each operational system has its own separator.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        | Yes        |
| silent        | A boolean value indicating whether print() calls should not be shown. This value can only be set from TerraME command line (-silent).                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           | Yes        |
| system        | A string with the operating system. It is one of "windows", "linux", or "mac".                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  | Yes        |
| time          | A number with the execution time of TerraME in seconds.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         | Yes        |
| version       | A string with the current version of TerraME.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   | Yes        |

### Usage

```
print(sessionInfo().mode)
```