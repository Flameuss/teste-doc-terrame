# Package

Functions to work with packages in TerraME.

---

## Functions

|                                                                                   |                                                                                                                    |
| --------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------ |
| [filePath](./package.md#filepath)                 | Return a [File](../types/file.md) storing the full path of a file within a given package. |
| [filesByExtension](./package.md#filesbyextension) | Return a table with the files of a package that have a given extension.                                            |
| [getPackage](./package.md#getpackage)             | Return a table with the content of a given package.                                                                |
| [import](./package.md#import)                     | Load a given package.                                                                                              |
| [isLoaded](./package.md#isloaded)                 | Return whether a given package is loaded.                                                                          |
| [packageInfo](./package.md#packageinfo)           | Return the description of a package.                                                                               |

---

## **filePath** 

Return a [File](../types/file.md) storing the full path of a file within a given package. The file must be inside the directory data of package.  
  

### Arguments

- **#1**: A string with the name of the file.
- **#2**: A string with the name of the package. As default, it uses base package.

### Usage

```
cs = CellularSpace{file = filePath("simple.pgm")}
```

---

## **filesByExtension** 

Return a table with the files of a package that have a given extension.  
  

### Arguments

- **#1**: A string with the name of the package.
- **#2**: A string with the extension.

### Usage

```
filesByExtension("base", "csv")
```

---

## **getPackage** 

Return a table with the content of a given package. If the package is not installed, it verifies if the package is in the current directory.  
  

### Arguments

- **#1**: A package name.

### Usage

```
base = getPackage("base")
cs = base.CellularSpace{xdim = 10}
```

---

## **import** 

Load a given package. If the package is not installed, it verifies if the package is available in the current directory. It shows a warning if trying to load a package that was already loaded. In this case, the package will not be loaded again. See #2 below for a different procedure.  
  

### Arguments

- **#1**: A package name.
- **#2**: A boolean value indicating whether TerraME should load the package even if it was already loaded (default is false). In this case, it also avoids a warning indicating that the package was already loaded.

### Usage

```
import("calibration")
```

---

## **isLoaded** 

Return whether a given package is loaded.  
  

### Arguments

- **#1**: A string with the name of the package.

### Usage

```
if isLoaded("base") then
    print("is loaded")
end
```

---

## **packageInfo** 

Return the description of a package. This function tries to find the package in the TerraME installation directory. If it does not exist then it checks wether the package is available in the current directory. If the package does not exist then it stops with an error. Otherwise, it reads file description.lua and returns the following string attributes.  
  

| Attribute | Description                                                                                                                                                                                         |
| --------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| authors   | Name of the author(s) of the package.                                                                                                                                                               |
| contact   | E-mail of one or more authors.                                                                                                                                                                      |
| content   | A description of the package.                                                                                                                                                                       |
| data      | A [Directory](../types/directory.md) with the path to the data directory of the package. This attribute is added by this function as it does not exist in description.lua. |
| date      | Date of the current version.                                                                                                                                                                        |
| depends   | A string containing a comma-separated list of package names which this package depends on.                                                                                                          |
| tdepends  | A table describing the dependencies of the package using internal tables containing three values: operator (a string), package (a string), and version (a vector of numbers).                       |
| license   | Name of the package's license.                                                                                                                                                                      |
| package   | Name of the package.                                                                                                                                                                                |
| path      | A [Directory](../types/directory.md) with the path where the package is stored in the computer.                                                                            |
| title     | Optional title for the HTML documentation of the package.                                                                                                                                           |
| url       | An optional value with the webpage of the package.                                                                                                                                                  |
| version   | Current version of the package, in the form [.]*. For example: 1, 0.2, 2.5.2.                                                                                                                       |

### Arguments

- **#1**: A string with the name of the package. If nil, packageInfo will return the description of TerraME.

### Usage

```
str = packageInfo().version
print(str)
```