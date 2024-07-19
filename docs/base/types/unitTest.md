# UnitTest

Type for testing packages. All its arguments are necessary only when the tests work with database access.  
  

### Arguments

- **host**: Name of the host. See [CellularSpace](./trajectory.md).
- **password**: A password. See CellularSpace.
- **port**: Number of the port. See CellularSpace.
- **source**: Name of the data source. See CellularSpace.
- **user**: A user name. See CellularSpace.

### Usage

```
unitTest = UnitTest{}
```

---

## Functions

|                                                                                |                                                                                                                                                                                       |
| ------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [assert](./unitTest.md#assert)                 | Check if a given value is true or if a given function works properly.                                                                                                                 |
| [assertEquals](./unitTest.md#assertequals)     | Check if two values are equal.                                                                                                                                                        |
| [assertError](./unitTest.md#asserterror)       | Verify if a function produces an error.                                                                                                                                               |
| [assertFile](./unitTest.md#assertfile)         | Check if a given file exists and remove it.                                                                                                                                           |
| [assertNil](./unitTest.md#assertnil)           | Check if a given value is nil.                                                                                                                                                        |
| [assertNotNil](./unitTest.md#assertnotnil)     | Check if a given value is not nil.                                                                                                                                                    |
| [assertSnapshot](./unitTest.md#assertsnapshot) | Verify whether a [Chart](./chart.md) or a [Map](./map.md) has a plot similar to the one defined in the log directory. |
| [assertType](./unitTest.md#asserttype)         | Check if a value belongs to a given type.                                                                                                                                             |
| [assertWarning](./unitTest.md#assertwarning)   | Verify if a function produces a warning.                                                                                                                                              |
| [printError](./unitTest.md#printerror)         | Internal function to print error messages along the tests.                                                                                                                            |

---

## **assert** 

Check if a given value is true or if a given function works properly. When using any other value as argument (number, string, false, nil, etc.), it shows an error. it generates an error.  
  

### Arguments

- **#1**: Any value.

### Usage

```
unitTest = UnitTest{}
unitTest:assert(2 < 3)
```

---

## **assertEquals** 

Check if two values are equal. In this function, two tables are equal only when they are the same object (if not, they would not be equal even if they share the same internal content).  
  

### Arguments

- **#1**: Any value.
- **#2**: Any value.
- **#3**: A number indicating a maximum error tolerance. This argument is optional and can be used with numbers or strings. When using string, the tolerance is measured according to the [levenshtein()](../functions/utils.md#levenshtein) distance. The default tolerance is zero.
- **#4**: A boolean to ignore path between /'s, when comparing two strings. It automatically converts a string such as "directory/sub1/sub2/file" into "directory/file". This argument is optional and can be used only with strings. The default value is false.

### Usage

```
unitTest = UnitTest{}
unitTest:assertEquals(3, 3)
unitTest:assertEquals(2, 2.1, 0.2)
unitTest:assertEquals("string [gis/data/biomassa-manaus.asc]", "string [gis/biomassa-manaus.asc]", 0, true)
```

---

## **assertError** 

Verify if a function produces an error. If there is no error in the function or the error found is not the expected error then it generates an error.  
  

### Arguments

- **#1**: A function to be tested.
- **#2**: A string describing the error message that the function should produce. This string should contain only the error message, without the description of the file name where the error was produced.
- **#3**: A number indicating the maximum number of characters that can be different between the error produced by the error function and the expected error message. This argument might be necessary in error messages that include information that can change from machine to machine, such as an username. The default value is zero (no discrepancy).
- **#4**: A boolean to ignore path between /'s, when comparing two strings. It automatically converts a string such as "directory/sub1/sub2/file" into "directory/file". The default value is false.

### Usage

```
unitTest = UnitTest{}
error_func = function() verify(2 > 3, "wrong operator") end
unitTest:assertError(error_func, "wrong operator")
```

---

## **assertFile** 

Check if a given file exists and remove it. Repeating: The file is removed when calling this assert. If the file is a directory or does not exist then it shows an error.  
  

### Arguments

- **#1**: A [File](./file.md) or a string with the file name.
- **#2**: An optional number indicating the percentage of characters in the line that can be different. The tolerance is applied to each line of the files. The default tolerance is zero.

### Usage

```
unitTest = UnitTest{}
os.execute("touch file.txt") -- create a file (only works in Linux and Mac)
unitTest:assertFile("file.txt")
```

---

## **assertNil** 

Check if a given value is nil. Otherwise it generates an error.  
  

### Arguments

- **#1**: Any value.

### Usage

```
unitTest = UnitTest{}
unitTest:assertNil()
```

---

## **assertNotNil** 

Check if a given value is not nil. Otherwise it generates an error.  
  

### Arguments

- **#1**: Any value.

### Usage

```
unitTest = UnitTest{}
unitTest:assertNotNil(2)
```

---

## **assertSnapshot** 

Verify whether a [Chart](./chart.md) or a [Map](./map.md) has a plot similar to the one defined in the log directory. Note that this function cannot be used for the same file twice in the tests of a given package.  
  

### Arguments

- **#1**: A Chart or a Map.
- **#2**: A string with the file name in the snapshot directory. If the file does not exist then it will save the file in the snapshot directory.
- **#3**: A number between 0 and 1 with the maximum difference in percentage of pixels allowed. The default value is 0.

### Usage

```
unitTest = UnitTest{}
cell = Cell{value = 2}
chart = Chart{target = cell}
unitTest:assertSnapshot(chart, "test_chart.bmp")
```

---

## **assertType** 

Check if a value belongs to a given type. If not, it generates an error.  
  

### Arguments

- **#1**: Any value.
- **#2**: A string with the name of a type.

### Usage

```
unitTest = UnitTest{}
unitTest:assertType(2, "number")
```

---

## **assertWarning** 

Verify if a function produces a warning. If there is no warning in the function or the warning found is not the expected value then it generates an error.  
  

### Arguments

- **#1**: A function to be tested.
- **#2**: A string describing the warning message that the function is expected to produce. This string should contain only the warning message, without the description of the file name where the warning was produced.
- **#3**: A number indicating the maximum number of characters that can be different between the warning produced by the warning function and the expected warning. This argument might be necessary in warnings that include information that can change from machine to machine, such as an username. The default value is zero (no discrepancy).
- **#4**: A boolean to ignore path between /'s, when comparing two strings. It automatically converts a string such as "c:/directory/sub1/sub2/file.txt" into "file.txt". The default value is false.

### Usage

```
unitTest = UnitTest{}
error_func = function() customWarning("Did you forget something?") end
unitTest:assertWarning(error_func, "Did you forget something?")
```

---

## **printError** 

Internal function to print error messages along the tests.  
  

### Arguments

- **#1**: A string with the error message.

### Usage

```
unitTest = UnitTest{}
unitTest:printError("msg")
```