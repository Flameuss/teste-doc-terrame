# VisualTable

A window with a table to show the current attributes of an object along the simulation. Each notify() overwrites the previous values shown in the table.  
  

### Arguments

- **select**: A vector of strings with the name of the attributes to be observed. If it is only a single value then it can also be described as a string. As default, it selects all the user-defined attributes of an object. In the case of [Society](./society.md), if it does not have any numeric attributes then it will use the number of agents in the Society as attribute.
- **target**: An [Agent](./agent.md), [Cell](./cell.md), [CellularSpace](./cellularSpace.md), or Society.

### Usage

```
cell = Cell{
    temperature = 20,
    humidity = 0.4
}

VisualTable{
    target = cell,
    select = {"temperature", "humidity"}
}
```

---

## Functions

|                                                                   |                                                              |
| ----------------------------------------------------------------- | ------------------------------------------------------------ |
| [save](./visualTable.md#save)     | Save a VisualTable into a file.                              |
| [update](./visualTable.md#update) | Update the VisualTable with the latest values of its target. |

---

## **save** 

Save a VisualTable into a file. Supported extensions are bmp, jpg, png, and tiff.  
  

### Arguments

- **#1**: A string with the file name.

### Usage

```
cell = Cell{
    temperature = 20,
    humidity = 0.4
}

vt = VisualTable{
    target = cell,
    select = {"temperature", "humidity"}
}

vt:save("file.bmp")
File("file.bmp"):delete()
```

---

## **update** 

Update the VisualTable with the latest values of its target. It is usually recommended to use the VisualTable as action of an [Event](./event.md) instead of calling this function explicitly.  
  

### Usage

```
cell = Cell{
    temperature = 20,
    humidity = 0.4
}

vt = VisualTable{
    target = cell,
    select = {"temperature", "humidity"}
}

vt:update()
```