# Log

A log file to save attributes of an object. The saved file uses the csv standard: The first line contains the attribute names and the following lines contains values according to the calls to notify().  
  

### Arguments

- **file**: A string with the file name to be saved. The default value is "result.csv".
- **overwrite**: A boolean value indicating whether the file should be overwritten. The default value is true.
- **select**: A vector of strings with the name of the attributes to be observed. If it is only a single value then it can also be described as a string. As default, it selects all the user-defined attributes of an object. In the case of [Society](./society.md), if it does not have any numeric attributes then it will use the number of agents in the Society as attribute.
- **separator**: A string with the separator. The default value is ",".
- **target**: An [Agent](./agent.md), [Cell](./cell.md), [CellularSpace](./cellularSpace.md), Society.

### Usage

```
agent = Agent{
    age = 3
}

Log{
    target = agent,
    file = "agent.csv",
    separator = ";"
}
```

---
## Functions

|                                                           |                                                      |
| --------------------------------------------------------- | ---------------------------------------------------- |
| [update](./log.md#update) | Update the Log with the latest values of its target. |


---

## **update** 

Update the Log with the latest values of its target. It is usually recommended to use the Log as action of an [Event](./event.md) instead of calling this function explicitly.  
  

### Usage

```
agent = Agent{
    age = 3
}

log = Log{
    target = agent,
    file = "agent.csv",
    separator = ";"
}

log:update()

File("agent.csv"):delete()
```