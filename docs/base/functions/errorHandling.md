# ErrorHandling

Some basic and useful functions to handle errors and error messages.

## Functions

|                                                                                                                             |                                                                                                                                                          |
| --------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [customError](../functions/errorHandling.md#customerror)                                               | Stop the simulation with an error.                                                                                                                       |
| [customWarning](../functions/errorHandling.md#customwarning)                                           | Print a warning.                                                                                                                                         |
| [defaultTableValue](../functions/errorHandling.md#defaulttablevalue)                                   | Verify the default value of a given attribute of a named table.                                                                                          |
| [defaultValueMsg](../functions/errorHandling.md#defaultvaluemsg)                                       | Return a message indicating that the modeler is using the default value for a given argument and therefore it could be removed.                          |
| [defaultValueWarning](../functions/errorHandling.md#defaultvaluewarning)                               | Show a strict warning if the attribute of a table has the default value.                                                                                 |
| [deprecatedFunction](../functions/errorHandling.md#deprecatedfunction)                                 | Show an error indicating a deprecated function.                                                                                                          |
| [deprecatedFunctionMsg](../functions/errorHandling.md#deprecatedfunctionmsg)                           | Return a message indicating that a function is deprecated and must be replaced.                                                                          |
| [incompatibleTypeError](../functions/errorHandling.md#incompatibletypeerror)                           | Stop the simulation with an error of a wrong type for an argument of a function.                                                                         |
| [incompatibleTypeMsg](../functions/errorHandling.md#incompatibletypemsg)                               | Return an error message for incompatible types.                                                                                                          |
| [incompatibleValueError](../functions/errorHandling.md#incompatiblevalueerror)                         | Stop the simulation with an error of a wrong value for an argument of a function.                                                                        |
| [incompatibleValueMsg](../functions/errorHandling.md#incompatiblevaluemsg)                             | Return an error message for incompatible values.                                                                                                         |
| [integerArgument](../functions/errorHandling.md#integerargument)                                       | Verify whether a given argument is integer.                                                                                                              |
| [integerArgumentMsg](../functions/errorHandling.md#integerargumentmsg)                                 | Return a message indicating that a given argument of a function should be integer.                                                                       |
| [integerTableArgument](../functions/errorHandling.md#integertableargument)                             | Verify whether a given argument of a named function is integer.                                                                                          |
| [invalidFileExtensionError](../functions/errorHandling.md#invalidfileextensionerror)                   | Stop the simulation with an error indicating that the function does not support a given file extension.                                                  |
| [invalidFileExtensionMsg](../functions/errorHandling.md#invalidfileextensionmsg)                       | Return a message indicating that a given file extension is incompatible.                                                                                 |
| [mandatoryArgument](../functions/errorHandling.md#mandatoryargument)                                   | Verify whether a given argument of a function with non-named arguments belongs to the correct type.                                                      |
| [mandatoryArgumentError](../functions/errorHandling.md#mandatoryargumenterror)                         | Stop the simulation with an error indicating that a given argument is mandatory.                                                                         |
| [mandatoryArgumentMsg](../functions/errorHandling.md#mandatoryargumentmsg)                             | Return a message indicating that a given argument of a function is mandatory.                                                                            |
| [mandatoryTableArgument](../functions/errorHandling.md#mandatorytableargument)                         | Verify whether a named table contains a mandatory argument.                                                                                              |
| [namedArgumentsMsg](../functions/errorHandling.md#namedargumentsmsg)                                   | Return a message indicating that the arguments of a function must be named.                                                                              |
| [optionalArgument](../functions/errorHandling.md#optionalargument)                                     | Verify whether an optional argument of a function with non-named arguments belongs to the correct type.                                                  |
| [optionalTableArgument](../functions/errorHandling.md#optionaltableargument)                           | Verify whether a named table contains an optional argument.                                                                                              |
| [positiveArgument](../functions/errorHandling.md#positiveargument)                                     | Verify whether a given argument is positive.                                                                                                             |
| [positiveArgumentMsg](../functions/errorHandling.md#positiveargumentmsg)                               | Return a message indicating that a given argument of a function should be positive.                                                                      |
| [positiveTableArgument](../functions/errorHandling.md#positivetableargument)                           | Verify whether a given argument of a function with named arguments is positive.                                                                          |
| [resourceNotFoundError](../functions/errorHandling.md#resourcenotfounderror)                           | Stop the simulation with an error indicating that a given resource was not found.                                                                        |
| [resourceNotFoundMsg](../functions/errorHandling.md#resourcenotfoundmsg)                               | Return a message indicating that a given resource could not be found.                                                                                    |
| [strictWarning](../functions/errorHandling.md#strictwarning)                                           | Print a strict warning.                                                                                                                                  |
| [suggestion](../functions/errorHandling.md#suggestion)                                                 | Return a suggestion for a wrong string value.                                                                                                            |
| [suggestionMsg](../functions/errorHandling.md#suggestionmsg)                                           | Return the arguments of suggestion within a question " Do you mean '#1'?".                                                                               |
| [switchInvalidArgument](../functions/errorHandling.md#switchinvalidargument)                           | Stop the simulation with an error because the user did not choose a correct option.                                                                      |
| [switchInvalidArgumentMsg](../functions/errorHandling.md#switchinvalidargumentmsg)                     | Return a message for a wrong argument value showing the options.                                                                                         |
| [switchInvalidArgumentSuggestionMsg](../functions/errorHandling.md#switchinvalidargumentsuggestionmsg) | Return a message for a wrong argument value showing the most similar option.                                                                             |
| [tableArgumentMsg](../functions/errorHandling.md#tableargumentmsg)                                     | Return a message indicating that the argument of a function must be a table.                                                                             |
| [unnecessaryArgumentMsg](../functions/errorHandling.md#unnecessaryargumentmsg)                         | Return a message indicating that a given argument is unnecessary.                                                                                        |
| [valueNotFoundError](../functions/errorHandling.md#valuenotfounderror)                                 | Stop the simulation with an error due to a wrong value for an argument.                                                                                  |
| [valueNotFoundMsg](../functions/errorHandling.md#valuenotfoundmsg)                                     | Return a message indicating that a given argument of a function is mandatory.                                                                            |
| [verify](../functions/errorHandling.md#verify)                                                         | Verify a given condition, otherwise it stops the simulation with an error.                                                                               |
| [verifyNamedTable](../functions/errorHandling.md#verifynamedtable)                                     | Verify if a given object is a named table.                                                                                                               |
| [verifyUnnecessaryArguments](../functions/errorHandling.md#verifyunnecessaryarguments)                 | Verify whether the user has passed only the allowed arguments for a function, removing the unnecessary arguments and showing a strict warning otherwise. |

---

## **customError** 

Stop the simulation with an error.  
  

### Arguments

- **#1**: A string describing the error message.

### Usage

```
_, err = pcall(function() customError("error message") end)
print(err)
```

---

## **customWarning** 

Print a warning. If TerraME is executing in the debug mode, it stops the simulation with an error.  
  

### Arguments

- **#1**: A string describing the warning.

### Usage

```
customWarning("warning message")
```

---

## **defaultTableValue** 

Verify the default value of a given attribute of a named table. It adds the attribute with the default value in the table if it does not exist, stops with an error ([incompatibleTypeMsg()](../functions/errorHandling.md#incompatibletypemsg)) if the value has a different type, or shows a warning ([defaultValueWarning()](../functions/errorHandling.md#defaultvaluewarning)) if it is equal to the default value.  
  

### Arguments

- **#1**: A named table (which can be an argument for a function).
- **#2**: A string with the name of an attribute (or argument) from #1.
- **#3**: The default value (any type).

### Usage

```
function integrate(attrs)
    defaultTableValue(attrs, "method", "euler")
    return attrs
end

t = integrate{}
print(t.method)
```

---

## **defaultValueMsg** 

Return a message indicating that the modeler is using the default value for a given argument and therefore it could be removed. The string is "Argument '#1' could be removed as it is the default value ('#2').".  
  

### Arguments

- **#1**: A string with the name of the argument.
- **#2**: A number or string or boolean value with the default value for the argument.

### Usage

```
str = defaultValueMsg("dbtype", "mysql")
print(str)
```

---

## **defaultValueWarning** 

Show a strict warning if the attribute of a table has the default value. If TerraME is running in the debug mode, the simulation stops with an error. The warning message comes from [defaultValueMsg()](../functions/errorHandling.md#defaultvaluemsg).  
  

### Arguments

- **#1**: A string with the name of the argument.
- **#2**: The default value.

### Usage

```
str = defaultValueWarning("size", 2)
print(str)
```

---

## **deprecatedFunction** 

Show an error indicating a deprecated function. The error comes from [deprecatedFunctionMsg()](../functions/errorHandling.md#deprecatedfunctionmsg).  
  

### Arguments

- **#1**: A string with the name of the deprecated function.
- **#2**: A string indicating how to proceed to replace the deprecated function call.

### Usage

```
deprecatedFunc = function()
    deprecatedFunction("abc", "def")
end

_, err = pcall(function() deprecatedFunc() end)
print(err)
```

---

## **deprecatedFunctionMsg** 

Return a message indicating that a function is deprecated and must be replaced. The string is "Function '#1' is deprecated. Use '#2' instead.".  
  

### Arguments

- **#1**: A string with the name of the deprecated function.
- **#2**: A string indicating how to proceed to replace the deprecated function call.

### Usage

```
str = deprecatedFunctionMsg("abc", "def")
print(str)
```

---

## **incompatibleTypeError** 

Stop the simulation with an error of a wrong type for an argument of a function. The error message is the return value of [incompatibleTypeMsg()](../functions/errorHandling.md#incompatibletypemsg).  
  

### Arguments

- **#1**: A string with the name of the argument, or a number with its the position.
- **#2**: A string with the possible type (or types).
- **#3**: The value wrongly passed as argument.

### Usage

```
_, err = pcall(function() incompatibleTypeError("cell", "Cell", Agent{}) end)
print(err)
```


---

## **incompatibleTypeMsg** 

Return an error message for incompatible types. The string is "Incompatible types. Argument '#1' expected #2, got type(#3).".  
  

### Arguments

- **#1**: A string with the name of the argument, or a number with its the position.
- **#2**: A string with the possible type (or types). The default value is "nil".
- **#3**: The value wrongly passed as argument.

### Usage

```
str = incompatibleTypeMsg("source", "string", 2)
print(str)
```

---

## **incompatibleValueError** 

Stop the simulation with an error of a wrong value for an argument of a function. The error message comes from [incompatibleValueMsg()](../functions/errorHandling.md#incompatiblevaluemsg).  
  

### Arguments

- **#1**: A string with the name of the argument or a number with its position.
- **#2**: A string with the expected value(s) for the argument.
- **#3**: The value wrongly passed as argument.

### Usage

```
_, err = pcall(function() incompatibleValueError("position", "one of {1, 2, 3}", 4) end)
print(err)
```

---

## **incompatibleValueMsg** 

Return an error message for incompatible values. The string is "Incompatible values. Argument '#1' expected #2, got #3.".  
  

### Arguments

- **#1**: A string with the name of the argument or a number with its position.
- **#2**: A string with the expected value(s) for the argument.
- **#3**: The value wrongly passed as argument.

### Usage

```
str = incompatibleValueMsg("source", "one of {1, 3, 4}", 2)
print(str)
```

---

## **integerArgument** 

Verify whether a given argument is integer. It is useful only for functions with non-named arguments. The error message comes from [integerArgumentMsg()](../functions/errorHandling.md#integerargumentmsg).  
  

### Arguments

- **#1**: A number with the position of the argument in the function.
- **#2**: The value used as argument to the function call.

### Usage

```
sum = function(a, b)
    integerArgument(1, a)
    integerArgument(2, b)
    return a + b
end

_, err = pcall(function() sum(5) end)
print(err)
```

---

## **integerArgumentMsg** 

Return a message indicating that a given argument of a function should be integer. It returns [incompatibleValueMsg()](../functions/errorHandling.md#incompatiblevaluemsg) with "integer number" as #2.  
  

### Arguments

- **#1**: A string with the name of the argument or a number with the position of the argument.
- **#2**: The value used as argument to the function call.

### Usage

```
str = integerArgumentMsg("target", 7.4)
print(str)

str = integerArgumentMsg(2, 5.1)
print(str)
```

---

## **integerTableArgument** 

Verify whether a given argument of a named function is integer. The error message comes from [integerArgumentMsg()](../functions/errorHandling.md#integerargumentmsg).  
  

### Arguments

- **#1**: A named table.
- **#2**: A string with the name of the argument.

### Usage

```
myFunction = function(mtable)
    integerTableArgument(mtable, "value")
end

_, err = pcall(function() myFunction{value = false} end)
print(err)
```

---

## **invalidFileExtensionError** 

Stop the simulation with an error indicating that the function does not support a given file extension. The error message comes from [invalidFileExtensionMsg()](../functions/errorHandling.md#invalidfileextensionmsg).  
  

### Arguments

- **#1**: A string with the name of the argument or a number with its position.
- **#2**: A string with the incompatible file extension.

### Usage

```
_, err = pcall(function() invalidFileExtensionError("file", ".txt") end)
print(err)
```

---

## **invalidFileExtensionMsg** 

Return a message indicating that a given file extension is incompatible. The string is "Argument '#1' does not support extension '#2'.".  
  

### Arguments

- **#1**: A string with the name of the argument (for functions with named arguments), or its position (for functions with non-named arguments).
- **#2**: A string with the incompatible file extension.

### Usage

```
str = invalidFileExtensionMsg("file", "csv")
print(str)
```

---

## **mandatoryArgument** 

Verify whether a given argument of a function with non-named arguments belongs to the correct type. The error message comes from [mandatoryArgumentMsg()](../functions/errorHandling.md#mandatoryargumentmsg) and [incompatibleTypeMsg()](../functions/errorHandling.md#incompatibletypemsg).  
  

### Arguments

- **#1**: A number with the position of the argument in the function.
- **#2**: A string with the required type for the argument.
- **#3**: The value used as argument to the function call.

### Usage

```
myFunction = function(value)
    mandatoryArgument(1, "string", value)
end

_, err = pcall(function() myFunction(2) end)
print(err)
```

---

## **mandatoryArgumentError** 

Stop the simulation with an error indicating that a given argument is mandatory. The error message comes from [mandatoryArgumentMsg()](../functions/errorHandling.md#mandatoryargumentmsg).  
  

### Arguments

- **#1**: A string with name of the argument or a number with its position in the function.

### Usage

```
_, err = pcall(function() mandatoryArgumentError(2) end)
print(err)
```

---

## **mandatoryArgumentMsg** 

Return a message indicating that a given argument of a function is mandatory. The string is "Argument '#1' is mandatory.".  
  

### Arguments

- **#1**: The name of the argument. It can be a string or a number.

### Usage

```
str = mandatoryArgumentMsg("target")
print(str)

str = mandatoryArgumentMsg(2)
print(str)
```

---

## **mandatoryTableArgument** 

Verify whether a named table contains a mandatory argument. It stops with an error if the value is nil or if it does not belong to the required type. The error message comes from [mandatoryArgumentMsg()](../functions/errorHandling.md#mandatoryargumentmsg) or [incompatibleTypeMsg()](../functions/errorHandling.md#incompatibletypemsg).  
  

### Arguments

- **#1**: A named table.
- **#2**: A string with the argument name.
- **#3**: A string with the required type for the argument, or a vector of strings with the allowed types. This argument is optional. If not used, then this function will check only if the argument is not nil.

### Usage

```
myFunction = function(mtable)
    mandatoryTableArgument(mtable, "value", "string")
end

_, err = pcall(function() myFunction{value = 2} end)
print(err)
```

---

## **namedArgumentsMsg** 

Return a message indicating that the arguments of a function must be named. The string is "Arguments must be named.".  
  

### Usage

```
str = namedArgumentsMsg()
print(str)
```

---

## **optionalArgument** 

Verify whether an optional argument of a function with non-named arguments belongs to the correct type. If the argument is nil then no error is created. The error message comes from [incompatibleTypeMsg()](../functions/errorHandling.md#incompatibletypemsg).  
  

### Arguments

- **#1**: A number with the position of the argument in the function.
- **#2**: A string with the required type for the argument.
- **#3**: The value used as argument to the function call.

### Usage

```
myFunction = function(value)
    optionalArgument(1, "string", value)
end

_, err = pcall(function() myFunction(2) end)
print(err)
```

---

## **optionalTableArgument** 

Verify whether a named table contains an optional argument. It stops with an error if the value is not nil and it has a type different from the required type. The error comes from [incompatibleTypeError()](../functions/errorHandling.md#incompatibletypeerror).  
  

### Arguments

- **#1**: A named table.
- **#2**: A string with the name of the argument.
- **#3**: A string with the required type for the argument or a table with strings describing the allowed types.

### Usage

```
myFunction = function(mtable)
    optionalTableArgument(mtable, "value", "string")
end

_, err = pcall(function() myFunction{value = 2} end)
print(err)
```

---

## **positiveArgument** 

Verify whether a given argument is positive. It is useful only for functions with non-named arguments. The error message comes from [positiveArgumentMsg()](../functions/errorHandling.md#positiveargumentmsg).  
  

### Arguments

- **#1**: A number with the position of the argument in the function.
- **#2**: The value used as argument to the function call.
- **#3**: A boolean value indicating whether zero should be included (the default value is false).

### Usage

```
positiveSum = function(a, b)
    positiveArgument(1, a)
    positiveArgument(2, b)
    return a + b
end

_, err = pcall(function() positiveSum(5, -2) end)
print(err)
```

---

## **positiveArgumentMsg** 

Return a message indicating that a given argument of a function should be positive. It returns [incompatibleValueMsg()](../functions/errorHandling.md#incompatiblevaluemsg) with "positive number (including/excluding zero)" as #2.  
  

### Arguments

- **#1**: The name of the argument. It can be a string or a number.
- **#2**: The value used as argument to the function call.
- **#3**: A boolean value indicating whether zero should be included (the default value is false).

### Usage

```
str = positiveArgumentMsg("target", -5)
print(str)

str = positiveArgumentMsg(2, -2, true)
print(str)
```

---

## **positiveTableArgument** 

Verify whether a given argument of a function with named arguments is positive. The error message comes from [positiveArgumentMsg()](../functions/errorHandling.md#positiveargumentmsg).  
  

### Arguments

- **#1**: A named table.
- **#2**: A string with the name of the argument.
- **#3**: A boolean value indicating whether zero should be included (the default value is false).

### Usage

```
myFunction = function(mtable)
    positiveTableArgument(mtable, "value")
end

_, err = pcall(function() myFunction{value = -2} end)
print(err)
```

---

## **resourceNotFoundError** 

Stop the simulation with an error indicating that a given resource was not found. The error message comes from [resourceNotFoundMsg()](../functions/errorHandling.md#resourcenotfoundmsg).  
  

### Arguments

- **#1**: A string with the name of the argument, or its position.
- **#2**: A string with the location of the resource.

### Usage

```
_, err = pcall(function() resourceNotFoundError("file", "file.txt") end)
print(err)
```

---

## **resourceNotFoundMsg** 

Return a message indicating that a given resource could not be found. The string is "[File](../types/file.md)/Resource '#1' was not found for argument '#2'.".  
  

### Arguments

- **#1**: A string with the name of the argument, or its position.
- **#2**: A File or a string with the location of the resource.

### Usage

```
str = resourceNotFoundMsg("file", "c:\\myfiles\\file.csv")
print(str)
```

---

## **strictWarning** 

Print a strict warning. This warning is shown only in the strict mode. If TerraME is executing in the debug mode, it stops the simulation with an error.  
  

### Arguments

- **#1**: A string describing the warning.

### Usage

```
strictWarning("warning message")
```

---

## **suggestion** 

Return a suggestion for a wrong string value. The suggestion must have a Levenshtein's distance of less than 60% the size of the string, otherwise it returns nil.  
  

### Arguments

- **#1**: A string.
- **#2**: A named table with the possible suggestions. It can also be a vector of strings.

### Usage

```
t = {
    blue = true,
    red = true,
    green = true
}

str = suggestion("gren", t)
print(str)
```

---

## **suggestionMsg** 

Return the arguments of suggestion within a question " Do you mean '#1'?".  
  

### Arguments

- **#1**: A string.

### Usage

```
t = {
    blue = true,
    red = true,
    green = true
}

str = suggestionMsg(suggestion("gren", t))
print(str)
```

---

## **switchInvalidArgument** 

Stop the simulation with an error because the user did not choose a correct option. This function supposes that there is a set of available options described as string idexes of a table so it tries to find an approximate string to be shown as a suggestion. Otherwise, it shows all the available options. The error messages come from [switchInvalidArgumentSuggestionMsg()](../functions/errorHandling.md#switchinvalidargumentsuggestionmsg) and [switchInvalidArgumentMsg()](../functions/errorHandling.md#switchinvalidargumentmsg).  
  

### Arguments

- **#1**: A string with the name of the argument.
- **#2**: A string with wrong value passed as argument.
- **#3**: A named table describing the available options.

### Usage

```
t = {
    blue = true,
    red = true,
    green = true
}

_, err = pcall(function() switchInvalidArgument("attribute", "gren", t) end)
print(err)
```

---

## **switchInvalidArgumentMsg** 

Return a message for a wrong argument value showing the options. The string is "'#1' is an invalid value for argument '#2'. It must be a string from the set [#3].".  
  

### Arguments

- **#1**: A string with the value of the argument.
- **#2**: A string with the name of the argument.
- **#3**: A named table indicating the available options.

### Usage

```
local options = {
    aaa = true,
    bbb = true,
    ccc = true
}

str = switchInvalidArgumentMsg("ddd", "attr", options)
print(str)
```

---

## **switchInvalidArgumentSuggestionMsg** 

Return a message for a wrong argument value showing the most similar option. The string is "'#1' is an invalid value for argument '#2'. suggestionMsg(#3)".  
  

### Arguments

- **#1**: A string with the value of the argument.
- **#2**: A string with the name of the argument.
- **#3**: A string with a suggestion to replace the wrong value.

### Usage

```
str = switchInvalidArgumentSuggestionMsg("aab", "attr", "aaa")
print(str)
```

---

## **tableArgumentMsg** 

Return a message indicating that the argument of a function must be a table. The string is "Argument must be a table.".  
  

### Usage

```
str = tableArgumentMsg()
print(str)
```

---

## **unnecessaryArgumentMsg** 

Return a message indicating that a given argument is unnecessary. The string is "Argument '#1' is unnecessary. suggestionMsg(#2)".  
  

### Arguments

- **#1**: A string or number or boolean value.
- **#2**: A possible suggestion for the argument. This argument is optional.

### Usage

```
str = unnecessaryArgumentMsg("file")
print(str)

str = unnecessaryArgumentMsg("filf", "file")
print(str)
```

---


## **valueNotFoundError** 

Stop the simulation with an error due to a wrong value for an argument. The error message comes from [valueNotFoundMsg()](../functions/errorHandling.md#valuenotfoundmsg).  
  

### Arguments

- **#1**: A string with the name of the argument or a number with its position.
- **#2**: The value used as argument to the function call.

### Usage

```
_, err = pcall(function() valueNotFoundError(1, "neighborhood") end)
print(err)
```

---

## **valueNotFoundMsg** 

Return a message indicating that a given argument of a function is mandatory. The string is "Value '#2' not found for argument '#1'.".  
  

### Arguments

- **#1**: A string with the name of the argument or a number with its position.
- **#2**: The valued used as argument to the function call.

### Usage

```
str = valueNotFoundMsg(1, "neighborhood")
print(str)
```


---

## **verify** 

Verify a given condition, otherwise it stops the simulation with an error.  
  

### Arguments

- **#1**: A value of any type. If it is false or nil, the function generates an error.
- **#2**: A string with the error to be displayed.

### Usage

```
greater = function(a, b)
    verify(a > b, "#1 is not greater than #2.")
end

_, err = pcall(function() greater(5, 7) end)
print(err)
```

---

## **verifyNamedTable** 

Verify if a given object is a named table. It generates errors if it is nil, if it is not a table, or if it has numeric names. The error messages come from [tableArgumentMsg()](../functions/errorHandling.md#tableargumentmsg) and [namedArgumentsMsg()](../functions/errorHandling.md#namedargumentsmsg).  
  

### Arguments

- **#1**: A value of any type.

### Usage

```
myFunction = function(mtable)
    verifyNamedTable(mtable)
end

_, err = pcall(function() myFunction{1, 2, 3} end)
print(err)
```

---

## **verifyUnnecessaryArguments** 

Verify whether the user has passed only the allowed arguments for a function, removing the unnecessary arguments and showing a strict warning otherwise. The warning comes from [unnecessaryArgumentMsg()](../functions/errorHandling.md#unnecessaryargumentmsg). It is recommended that this function should be called as early as possible, in order to show the warning before any error that might be related to it. This function removes each unnecessary argument from #1.  
  

### Arguments

- **#1**: A named table with the arguments used in the function call. The names of this table will be verified.
- **#2**: A vector with the allowed arguments.

### Usage

```
myFunction = function(mtable)
    verifyUnnecessaryArguments(mtable, {"aaa", "bbb", "ccc"})
end

_, err = pcall(function() myFunction{aaa = 3, value = 2} end)
print(err)
```