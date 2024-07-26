# DataFrame

A two dimensional table. DataFrames can be accessed by row or by column, independently on the way it was created.  
  

### Arguments

- **file**: A string or a [File](./file.md). It must have extension '.lua'.
- **first**: A number with the first index.
- **instance**: An optional object used as meta table for the rows of the DataFrame. and only used to check whether it is equals to first plus step times the size of the data vectors.
- **last**: A number with the last index. This argument is optional.
- **step**: A number with the interval between two indexes.
- **...**: Values for the DataFrame. It can be a vector of named tables or a named table with whose values are vectors.

### Usage

```
-- named table with vectors
df = DataFrame{
    x = {1, 1, 2, 2},
    y = {1, 2, 1, 2}
}

print(df.x[1]) -- 1
print(df[1].x) -- 1

-- vector of named tables
df = DataFrame{
    {x = 1, y = 1},
    {x = 1, y = 2},
    {x = 2, y = 1},
    {x = 2, y = 2},
    first = 2000,
    step = 10
}

print(df.y[2030]) -- 2
print(df[2010].y) -- 2
```

---

## Functions

|                                                                   |                                             |
| ----------------------------------------------------------------- | ------------------------------------------- |
| [add](./dataFrame.md#add)         | Add a new row.                              |
| [columns](./dataFrame.md#columns) | Return the columns of the DataFrame.        |
| [remove](./dataFrame.md#remove)   | Remove a given row.                         |
| [rows](./dataFrame.md#rows)       | Return the rows of the DataFrame.           |
| [save](./dataFrame.md#save)       | Save the DataFrame to a given file.         |
| [#](./dataFrame.md##)             | Return the number of rows in the DataFrame. |
| [[]](./dataFrame.md#[])           | Return a row or a column of the DataFrame.  |


---

## **add** 

Add a new row.  
  

### Arguments

- **#1**: A named table with the values of the row to be added.
- **#2**: An optional number describing the position of the row. As default, this function adds the new row after the last one.

### Usage

```
df = DataFrame{
    {x = 1, y = 1}
}

df:add{x = 5, y = 2}
df:add{x = 4, y = 2}

print(df[3].x) -- 4
print(df.y[2]) -- 2
```

---

## **columns** 

Return the columns of the DataFrame. It is a named table whose indexes are the column names and the values are true.  
  

### Usage

```
df = DataFrame{x = {1}, y = {2}}
print(vardump(df:columns())) -- {x = true, y = true}
```

---

## **remove** 

Remove a given row. This function only works properly when the rows are numbered from one to the quantity of elements in the DataFrame.  
  

### Arguments

- **#1**: A number with the position to be removed.

### Usage

```
df = DataFrame{
    {x = 1, y = 1},
    {x = 2, y = 1},
    {x = 3, y = 2},
    {x = 4, y = 2},
    {x = 5, y = 2}
}

df:remove(3)

print(#df) -- 4
print(df[3].x) -- 4
```

---

## **rows** 

Return the rows of the DataFrame. It is a named table whose indexes are the rows positions and the values are true.  
  

### Usage

```
df = DataFrame{x = {1}, y = {2}}
print(vardump(df:rows())) -- {true}
```

---

## **save** 

Save the DataFrame to a given file.  
  

### Arguments

- **#1**: A mandatory string with the file name or a [File](./file.md). It can be a Lua file (.lua) or a CSV (.csv).

### Usage

```
filename = "dump.lua"
df = DataFrame{x = {1}, y = {2}}
df:save(filename)

File(filename):deleteIfExists()
```

---

## **#** 

Return the number of rows in the DataFrame.  
  

### Usage

```
df = DataFrame{
    x = {1, 1, 2, 2},
    y = {1, 2, 1, 2}
}

print(#df) -- 4
```

---

## **[]** 

Return a row or a column of the DataFrame.  
  

### Arguments

- **#1**: An index. If it is a number this function returns the given row as a named table. If it is a string this function returns the entire column as a vector.

### Usage

```
df = DataFrame{
    x = {1, 1, 2, 2},
    y = {1, 2, 1, 2}
}

print(df.x[1]) -- 1

df.x[1] = 5
df[1].x = df[1].x + 1

print(df.x[1]) -- 6
```