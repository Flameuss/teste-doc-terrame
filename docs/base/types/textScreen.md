# TextScreen

A window with a table to show the attributes of an object along the simulation. Each call to notify() add one more line to the content of the window.  
  

### Arguments

- **select**: A vector of strings with the name of the attributes to be observed. If it is only a single value then it can also be described as a string. As default, it selects all the user-defined attributes of an object. In the case of [Society](./society.md), if it does not have any numeric attributes then it will use the number of agents in the Society as attribute.
- **target**: An [Agent](./agent.md), [Cell](./cell.md), [CellularSpace](./cellularSpace.md), Society.

### Usage

```
agent = Agent{
    size = 5,
    age = 1
}

TextScreen{
    target = agent,
    select = {"size" , "age"}
}
```

---

## Functions

|                                                                  |                                                             |
| ---------------------------------------------------------------- | ----------------------------------------------------------- |
| [save](./textScreen.md#save)     | Save a TextScreen into a file.                              |
| [update](./textScreen.md#update) | Update the TextScreen with the latest values of its target. |

---

## **save** 

Save a TextScreen into a file. Supported extensions are bmp, jpg, png, and tiff.  
  

### Arguments

- **#1**: A string with the file name.

### Usage

```
agent = Agent{
    size = 5,
    age = 1
}

ts = TextScreen{
    target = agent,
    select = {"size" , "age"}
}

ts:save("file.bmp")
File("file.bmp"):delete()
```

---

## **update** 

Update the TextScreen with the latest values of its target. It is usually recommended to use the TextScreen as action of an [Event](./event.md) instead of calling this function explicitly.  
  

### Arguments

- **#1**: An optional argument that can be a number with the current time or an Event.

### Usage

```
agent = Agent{
    size = 5,
    age = 1
}

ts = TextScreen{
    target = agent,
    select = {"size" , "age"}
}

ts:update()
```