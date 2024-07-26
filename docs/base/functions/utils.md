# Utils

Some basic and useful functions for modeling.

---

## Functions

|                                         |                                                               |
| --------------------------------------- | ------------------------------------------------------------- |
| [belong](./utils.md#belong)                                       | Return whether a given value belong to a table.                                                                                                                                                                                                                                                                                    |
| [call](./utils.md#call)                                           | Return a function that executes a given function of an object.                                                                                                                                                                                                                                                                     |
| [clean](./utils.md#clean)                                         | Remove all graphical interfaces ([Chart](../types/chart.md), [Map](../types/map.md), etc.).                                                                                                                                                                                      |
| [clone](./utils.md#clone)                                         | Return a copy of a given table.                                                                                                                                                                                                                                                                                                    |
| [d](./utils.md#d)                                                 | Constructor for an ordinary differential equation.                                                                                                                                                                                                                                                                                 |
| [delay](./utils.md#delay)                                         | Pause the simulation for a given time.                                                                                                                                                                                                                                                                                             |
| [equals](./utils.md#equals)                                       | Return whether two numbers are equals.                                                                                                                                                                                                                                                                                             |
| [forEachAgent](./utils.md#foreachagent)                           | Second order function to traverse a [Society](../types/society.md), [Group](../types/group.md), or [Cell](../types/cell.md), applying a function to each of its [Agents](../types/agent.md).                                   |
| [forEachAttribute](./utils.md#foreachattribute)                   | Second order function to traverse the attributes of a [Cell](../types/cell.md) or [Agent](../types/agent.md) defined by the user.                                                                                                                                                |
| [forEachCell](./utils.md#foreachcell)                             | Second order function to traverse a given [CellularSpace](../types/cellularSpace.md), [Trajectory](../types/trajectory.md), or [Agent](../types/agent.md), applying a given function to each of its [Cells](../types/cell.md). |
| [forEachCellPair](./utils.md#foreachcellpair)                     | Second order function to traverse two [CellularSpaces](../types/cellularSpace.md) with the same resolution and size.                                                                                                                                                                                      |
| [forEachConnection](./utils.md#foreachconnection)                 | Second order function to traverse the connections of a given [Agent](../types/agent.md), applying a function to each of them.                                                                                                                                                                             |
| [forEachDirectory](./utils.md#foreachdirectory)                   | Second order function to traverse a given directory, applying a given function on each of its internal directories.                                                                                                                                                                                                                |
| [forEachElement](./utils.md#foreachelement)                       | Second order function to traverse a given object, applying a function to each of its elements.                                                                                                                                                                                                                                     |
| [forEachFile](./utils.md#foreachfile)                             | Second order function to traverse a given directory, applying a given function on each of its files.                                                                                                                                                                                                                               |
| [forEachModel](./utils.md#foreachmodel)                           | Second order function to traverse the instances of [Models](../types/model.md) within a given [Environment](../types/environment.md).                                                                                                                                            |
| [forEachNeighbor](./utils.md#foreachneighbor)                     | Second order function to traverse a given [Neighborhood](../types/neighborhood.md) of a [Cell](../types/cell.md), applying a function in each of its neighbors.                                                                                                                  |
| [forEachNeighborAgent](./utils.md#foreachneighboragent)           | Second order function to traverse the [Agents](../types/agent.md) within the neighbor [Cells](../types/cell.md) fom the current location of a given Agent, applying a function to each of them.                                                                                  |
| [forEachNeighborhood](./utils.md#foreachneighborhood)             | Second order function to traverse all [Neighborhoods](../types/neighborhood.md) of a [Cell](../types/cell.md), applying a given function on them.                                                                                                                                |
| [forEachOrderedElement](./utils.md#foreachorderedelement)         | Second order function to traverse a given object, applying a function to each of its elements according to their alphabetical order.                                                                                                                                                                                               |
| [forEachRecursiveDirectory](./utils.md#foreachrecursivedirectory) | Second order function to traverse a given directory recursively, applying a given function on each of its internal files.                                                                                                                                                                                                          |
| [forEachSocialNetwork](./utils.md#foreachsocialnetwork)           | Second order function to traverse all [SocialNetworks](../types/socialNetwork.md) of an [Agent](../types/agent.md), applying a given function on them.                                                                                                                           |
| [getConfig](./utils.md#getconfig)                                 | Return a table with the content of the file config.lua, stored in the current directory of the simulation.                                                                                                                                                                                                                         |
| [getLuaFile](./utils.md#getluafile)                               | Load a lua file and return its global values as a Lua table.                                                                                                                                                                                                                                                                       |
| [getn](./utils.md#getn)                                           | Return the number of elements of a table, be them named or not.                                                                                                                                                                                                                                                                    |
| [getNames](./utils.md#getnames)                                   | Return the names of a given object derived from a table.                                                                                                                                                                                                                                                                           |
| [greaterByAttribute](./utils.md#greaterbyattribute)               | Return a function that compares two tables (which can be, for instance, [Agents](../types/agent.md) or [Cells](../types/cell.md)).                                                                                                                                               |
| [greaterByCoord](./utils.md#greaterbycoord)                       | Return a function that compares two tables with x and y attributes (basically two regular [Cells](../types/cell.md)).                                                                                                                                                                                     |
| [integrate](./utils.md#integrate)                                 | A second order function to numerically solve ordinary differential equations with a given initial value.                                                                                                                                                                                                                           |
| [integrationEuler](./utils.md#integrationeuler)                   | Implements the Euler (Euler-Cauchy) Method to integrate ordinary differential equations.                                                                                                                                                                                                                                           |
| [integrationHeun](./utils.md#integrationheun)                     | Implements the Heun (Euler Second Order) Method to integrate ordinary differential equations.                                                                                                                                                                                                                                      |
| [integrationRungeKutta](./utils.md#integrationrungekutta)         | Implements the Runge-Kutta Method (Fourth Order) to integrate ordinary differential equations.                                                                                                                                                                                                                                     |
| [isModel](./utils.md#ismodel)                                     | Return whether a given value is a [Model](../types/model.md) or an instance of a Model.                                                                                                                                                                                                                   |
| [isTable](./utils.md#istable)                                     | Return whether an object can be used as a table.                                                                                                                                                                                                                                                                                   |
| [levenshtein](./utils.md#levenshtein)                             | Return the Levenshtein's distance between two strings.                                                                                                                                                                                                                                                                             |
| [replaceLatinCharacters](./utils.md#replacelatincharacters)       | This function converts latin characters to hexadecimal code by the characters bytes.                                                                                                                                                                                                                                               |
| [round](./utils.md#round)                                         | Round a number given a precision.                                                                                                                                                                                                                                                                                                  |
| [string.endswith](./utils.md#string.endswith)                     | Return whether a string ends with a given substring (no case sensitive).                                                                                                                                                                                                                                                           |
| [switch](./utils.md#switch)                                       | Implement a switch case function, where functions are associated to the available options.                                                                                                                                                                                                                                         |
| [toLabel](./utils.md#tolabel)                                     | Convert a string into a more readable name.                                                                                                                                                                                                                                                                                        |
| [type](./utils.md#type)                                           | Return the type of an object.                                                                                                                                                                                                                                                                                                      |
| [vardump](./utils.md#vardump)                                     | Function that returns a string describing the internal content of an object.                                                                                                                                                                                                                                                       |

---

## **belong** 

Return whether a given value belong to a table.  
  

### Arguments

- **#1**: A value.
- **#2**: A table with a set of values.

### Usage

```
belong(2, {1, 2, 3})
```

---

## **call** 

Return a function that executes a given function of an object. It is particularly useful as argument action for an [Event](../types/event.md).  
  

### Arguments

- **#1**: Any TerraME object.
- **#2**: A string with the function to be executed.

### Usage

```
a = Agent{exec = function(self, ev) print(ev:getTime()) end}

t = Timer{
    Event{action = call(a, "exec")}
}

t:run(10)
```

---

## **clean** 

Remove all graphical interfaces ([Chart](../types/chart.md), [Map](../types/map.md), etc.). This function is particularly useful when one wants to simulate a [Model](../types/model.md) repeated times.  
  

### Usage

```
clean()
```

---

## **clone** 

Return a copy of a given table. It does not copy metatables.  
  

### Arguments

- **#1**: A table.

### Usage

```
animal = {
    age = 5,
    height = 10,
    weight = 8
}

copy = clone(animal)
copy.age = 2

print(animal.age)
``` 

---

## **d** 

Constructor for an ordinary differential equation. It works in the same way of [integrate()](./utils.md#integrate), but it is more efficient as it does not get a table as argument. The default integration method is Euler but the modeler can declare a global variable INTEGRATION_METHOD to change the default method.  
  

### Arguments

- **1**: A differential equation or a vector of differential equations. Each equation is described as a function of one or two arguments that returns a value of its derivative f(t, y), where t is the time instant, and y starts with the value of attribute initial and changes according to the result of f() and the chosen method. The calls to f will use the first argument (t) in the interval [a,b[, according to the argument step.
- **2**: The initial condition, or a vector of initial conditions, which must be satisfied. Each initial condition represents the value of y when t (first argument of f) is equal to the value of argument a.
- **3**: A number with the beginning of the interval.
- **4**: A number with the end of the interval.
- **5**: A positive number with the step within the interval. The default value is 0.2, but the user can change it by declaring a global variable DELTA.

### Usage

```
df = function(x, y) return y - x ^ 2 + 1 end
a = 0
b = 2
init = 0.5
delta = 0.2

result = d{df, init, a, b, delta}
print(result)
```

---

## **delay** 

Pause the simulation for a given time.  
  

### Arguments

- **#1**: A number indicating how long in seconds should the model pause. The default value is 1.

### Usage

```
delay(0.1)
```

---

## **equals** 

Return whether two numbers are equals. It supposes that there can exist a maximum difference of sessionInfo().round between them.  
  

### Arguments

- **#1**: A number.
- **#2**: Another number.

### Usage

```
print(equals(2, 2.0000001))
```

### See also

- [sessionInfo() (OS)](./os.md#sessioninfo)

---

## **forEachAgent** 

Second order function to traverse a [Society](../types/society.md), [Group](../types/group.md), or [Cell](../types/cell.md), applying a function to each of its [Agents](../types/agent.md). It returns true if no call to the function taken as argument returns false, otherwise it returns false.  
  

### Arguments

- **#1**: A Society, Group, or Cell. Cells need to have a placement in order to execute this function.
- **#2**: (Optional) A string with the name of the placement to be traversed. The default value is "placement". This argument can only be used when the first argument is a Cell.
- **#3**: A function that takes one single Agent as argument. If some call to it returns false, forEachAgent() stops and does not process any other Agent. This function can optionally get a second argument with a positive number representing the position of the Agent in the vector of Agents. In the case where the second argument is missing, this function becomes the second argument.

### Usage

```
ag = Agent{age = Random{min = 0, max = 2}}
soc = Society{
    instance = ag,
    quantity = 5
}

forEachAgent(soc, function(agent)
    agent.age = agent.age + 1
end)
```

### See also

- [createPlacement (Environment)](../types/environment.md#createplacement)


---

## **forEachAttribute** 

Second order function to traverse the attributes of a [Cell](../types/cell.md) or [Agent](../types/agent.md) defined by the user. It hides all the attributes and functions automatically created by TerraME. Note that, if the Agent (Cell) belongs to a [Society](../types/society.md) ([CellularSpace](../types/cellularSpace.md)) created with an instance, those attributes from the instance that were not yet updated will not be captured by this function.  
  

### Arguments

- **#1**: An Agent or a Cell.
- **#2**: A function that takes two arguments. The first argument is the attribute name and the second is its value.

### Usage

```
ag = Agent{
    age = 5,
    color = "blue"
}

forEachAttribute(ag, function(att)
    print(att)
end)
```

---

## **forEachCell** 

Second order function to traverse a given [CellularSpace](../types/cellularSpace.md), [Trajectory](../types/trajectory.md), or [Agent](../types/agent.md), applying a given function to each of its [Cells](../types/cell.md). If any of the function calls returns false, forEachCell() stops and returns false, otherwise it returns true.  
  

### Arguments

- **#1**: A CellularSpace, Trajectory, or Agent. Agents need to have a placement in order to execute this function.
- **#2**: (Optional) A string with the name of the placement to be traversed. The default value is "placement". This argument can only be used when the first argument is an Agent.
- **#3**: A user-defined function that takes a Cell as argument. It can optionally have a second argument with a positive number representing the position of the Cell in the vector of Cells. If it returns false when processing a given Cell, forEachCell() stops and does not process any other Cell. In the case where the second argument is missing, this function becomes the second argument.

### Usage

```
cellularspace = CellularSpace{xdim = 10}

forEachCell(cellularspace, function(cell)
    cell.water = 0
end)
```

### See also

- [createPlacement (Environment)](../types/environment.md#createplacement)

---

## **forEachCellPair** 

Second order function to traverse two [CellularSpaces](../types/cellularSpace.md) with the same resolution and size. It applies a function that gets two [Cells](../types/cell.md) as arguments, one from each CellularSpace. Both Cells share the same (x, y) location. It returns true if no call to the function taken as argument returns false, otherwise it returns false.  
  

### Arguments

- **#1**: A CellularSpace.
- **#2**: Another CellularSpace.
- **#3**: A user-defined function that takes two Cells as arguments, one coming from the first argument and the other from the second one. If some call returns false, forEachCellPair() stops and does not process any other pair of Cells.

### Usage

```
cs1 = CellularSpace{
    xdim = 10,
    instance = Cell{water = Random{min = 0, max = 20}}
}
cs2 = CellularSpace{xdim = 10}

forEachCellPair(cs1, cs2, function(cell1, cell2)
    cell2.water = cell1.water
    cell1.water = 0
end)
```

---

## **forEachConnection** 

Second order function to traverse the connections of a given [Agent](../types/agent.md), applying a function to each of them. It returns true if no call to the function taken as argument returns false, otherwise it returns false. There are two ways of using this function because the second argument is optional.  
  

### Arguments

- **#1**: An Agent.
- **#2**: (Optional) A string with the name of the [SocialNetwork](../types/socialNetwork.md) to be traversed. The default value is "1".
- **#3**: A function that takes three arguments: A connection (Agent), the connection weight, and the Agent itself. If some call to f returns false, forEachConnection() stops and does not process any other connection. In the case where the second argument is missing, this function becomes the second argument.

### Usage

```
ag = Agent{
    value = 2,
    on_message = function() print("thanks") end
}

soc = Society{instance = ag, quantity = 10}

soc:createSocialNetwork{quantity = 3}

agent = soc:sample()
forEachConnection(agent, function(conn)
    agent:message{receiver = conn}
end)
```

### See also

- [createSocialNetwork (Society)](../types/society.md#createsocialnetwork)

---

## **forEachDirectory** 

Second order function to traverse a given directory, applying a given function on each of its internal directories. If any of the function calls returns false, forEachDirectory() stops and returns false, otherwise it returns true.  
  

### Arguments

- **#1**: A string with the path to a directory, or a vector of files.
- **#2**: A user-defined function that takes a file name as argument. Note that the name does not include the directory where the file is placed.

### Usage

```
forEachDirectory(packageInfo("base").path, function(dir)
    print(dir)
end)
```

### See also

- [list (Directory)](../types/directory.md#list)

---

## **forEachElement** 

Second order function to traverse a given object, applying a function to each of its elements. It can be used for instance to traverse all the elements of an [Agent](../types/agent.md) or an [Environment](../types/environment.md). According to the current Lua version, if one uses this function twice, Lua does not guarantee that the objects will be traversed in the same order. If you need to guarantee this, it is recommended to use [forEachOrderedElement()](./utils.md#foreachorderedelement) instead. This function returns true if no call to the function taken as argument returns false, otherwise it returns false.  
  

### Arguments

- **#1**: A TerraME object or a table.
- **#2**: A user-defined function that takes three arguments: the name of the element, the element itself, and the type of the element. If some call to this function returns false then forEachElement() stops.

### Usage

```
cell = Cell{
    value1 = 10,
    value2 = 5
}

forEachElement(cell, function(idx, _, etype)
    print(idx.."\t"..etype)
end)
```

---

## **forEachFile** 

Second order function to traverse a given directory, applying a given function on each of its files. Internal directories are ignored. If any of the function calls returns false, forEachFile() stops and returns false, otherwise it returns true.  
  

### Arguments

- **#1**: A string with the path to a directory, or a vector of files.
- **#2**: A user-defined function that takes a file name as argument. Note that the name does not include the directory where the file is placed.

### Usage

```
forEachFile(packageInfo("base").path, function(file)
    print(file)
end)
```

### See also

- [list (Directory)](../types/directory.md#list)

---

## **forEachModel** 

Second order function to traverse the instances of [Models](../types/model.md) within a given [Environment](../types/environment.md). It applies a given function on each of its instances. If any of the function calls returns false, forEachModel() stops and returns false, otherwise it returns true.  
  

### Arguments

- **#1**: An Environment.
- **#2**: A user-defined function that takes an instance of Model as first argument and its name within the Environment as second argument.

### Usage

```
MyTube = Model{
    water = 200,
    sun = Choice{min = 0, default = 10},
    init = function(model)
        model.finalTime = 100

        model.timer = Timer{
            Event{action = function()
                -- ...
            end}
        }
    end
}

e = Environment{
    scenario0 = MyTube{},
    scenario1 = MyTube{water = 100},
    scenario2 = MyTube{water = 100, sun = 5},
    scenario3 = MyTube{water = 100, sun = 10}
}

forEachModel(e, function(model, name)
    print(name.."  "..model:title())
end)
```

---

## **forEachNeighbor** 

Second order function to traverse a given [Neighborhood](../types/neighborhood.md) of a [Cell](../types/cell.md), applying a function in each of its neighbors. It returns true if no call to the function taken as argument returns false, otherwise it returns false. There are two ways of using this function because the second argument is optional.  
  

### Arguments

- **#1**: A Cell.
- **#2**: (Optional) A string with the name of the Neighborhood to be traversed. The default value is "1".
- **#3**: A user-defined function that takes three arguments: the neighbor Cell, the connection weight, and the Cell itself. If some call to it returns false, forEachNeighbor() stops and does not process any other neighbor. In the case where the second argument is missing, this function becomes the second argument.

### Usage

```
cs = CellularSpace{
    xdim = 10,
    instance = Cell{deforestation = Random{min = 0, max = 1}}
}

cs:createNeighborhood()
cell = cs:sample()

forEachNeighbor(cell, function(neighbor)
    if neighbor.deforestation > 0.9 then
        cell.deforestation = cell.deforestation * 1.01
    end
end)

cs:createNeighborhood{
    strategy = "vonneumann",
    name = "vonneumann",
    self = true
}

forEachNeighbor(cell, "vonneumann", function(neighbor)
    if cell.deforestation <= neighbor.deforestation then
        cell.deforestation = neighbor.deforestation
    end
end)
```

### See also

- [createNeighborhood (CellularSpace)](../types/cellularSpace.md#createneighborhood)
- [loadNeighborhood (CellularSpace)](../types/cellularSpace.md#loadneighborhood)

---

## **forEachNeighborAgent** 

Second order function to traverse the [Agents](../types/agent.md) within the neighbor [Cells](../types/cell.md) fom the current location of a given Agent, applying a function to each of them. This function requires that the Agent has a default placement ("placement") and its Cell has a default [Neighborhood](../types/neighborhood.md) ("1"). More complex placements and neighborhoods need to be traversed manually using [Agent:getCell()](../types/agent.md#getcell) and [Cell:getNeighborhood()](../types/cell.md#getneighborhood). It returns true if no call to the function taken as argument returns false, otherwise it returns false.  
  

### Arguments

- **#1**: An Agent.
- **#2**: A function that takes one single Agent as argument. This function is called once for each agent within a neighbor cell of the current cell where the Agent belongs. If some call to it returns false, forEachNeighborAgent() stops and does not process any other Agent.

### Usage

```
ag = Agent{age = Random{min = 0, max = 2}}
soc = Society{
    instance = ag,
    quantity = 5
}

cs = CellularSpace{xdim = 5}
cs:createNeighborhood{}

env = Environment{soc, cs}
env:createPlacement{}

forEachNeighborAgent(soc:sample(), function(agent)
    print("Found Agent "..agent.id)
end)
```

### See also

- [createNeighborhood (CellularSpace)](../types/cellularSpace.md#createneighborhood)
- [createPlacement (Environment)](../types/environment.md#createplacement)

---

## **forEachNeighborhood** 

Second order function to traverse all [Neighborhoods](../types/neighborhood.md) of a [Cell](../types/cell.md), applying a given function on them. It returns true if no call to the function taken as argument returns false, otherwise it returns false.  
  

### Arguments

- **#1**: A Cell.
- **#2**: A function that receives a Neighborhood name as argument.

### Usage

```
cs = CellularSpace{
    xdim = 10
}

cs:createNeighborhood()
cs:createNeighborhood{
    name = "2"
}

cell = cs:sample()
forEachNeighborhood(cell, function(idx)
    print(idx)
    print(#cell:getNeighborhood(idx))
end)
```

---

## **forEachOrderedElement** 

Second order function to traverse a given object, applying a function to each of its elements according to their alphabetical order. It can be used for instance to traverse all the elements of an [Agent](../types/agent.md) or an [Environment](../types/environment.md). This function executes first the positions with numeric names and then the string ones, with upper case characters having priority over lower case. This function returns true if no call to the function taken as argument returns false, otherwise it returns false.  
  

### Arguments

- **#1**: A TerraME object or a table.
- **#2**: A user-defined function that takes three arguments: the name of the element, the element itself, and the type of the element. If some call to this function returns false then forEachElement() stops.

### Usage

```
cell = Cell{
    value1 = 10,
    value2 = 5
}

forEachOrderedElement(cell, function(idx, _, etype)
    print(idx.."\t"..etype)
end)
```

---


## **forEachRecursiveDirectory** 

Second order function to traverse a given directory recursively, applying a given function on each of its internal files. If any of the function calls returns false, forEachRecursiveDirectory() stops and returns false, otherwise it returns true.  
  

### Arguments

- **#1**: A string with the path to a directory, or a [Directory (base package)](../types/directory.md).
- **#2**: A user-defined function that takes a file path as argument.

### Usage

```
forEachRecursiveDirectory(packageInfo("base").path.."data", function(file)
    print(file)
end)
```

---

## **forEachSocialNetwork** 

Second order function to traverse all [SocialNetworks](../types/socialNetwork.md) of an [Agent](../types/agent.md), applying a given function on them. It returns true if no call to the function taken as argument returns false, otherwise it returns false.  
  

### Arguments

- **#1**: An Agent.
- **#2**: A function that receives a SocialNetwork name as argument.

### Usage

```
ag = Agent{value = 2}
soc = Society{instance = ag, quantity = 20}

soc:createSocialNetwork{quantity = 3}
soc:createSocialNetwork{
    quantity = 5,
    name = "2"
}

agent = soc:sample()
forEachSocialNetwork(agent, function(idx)
    print(idx)
    print(#agent:getSocialNetwork(idx))
end)
```

---

## **getConfig** 

Return a table with the content of the file config.lua, stored in the current directory of the simulation. All the global variables of the file are elements of the returned table. Some packages require specific variables in this file in order to be tested or executed. Additional calls to getConfig will return the same output of the first call even if the current directory changes along the simulation.  
  

### Usage

```
getConfig()
```

---

## **getLuaFile** 

Load a lua file and return its global values as a Lua table.  
  

### Arguments

- **#1**: A [File](../types/file.md) or a string with a file name.
- **#2**: An optional table where the new values will be placed.

### Usage

```
print(getLuaFile(packageInfo("base").path.."description.lua").version)
```

---

## **getn** 

Return the number of elements of a table, be them named or not. It is a substitute for the old Lua function table.getn. It can also be used to compute the number of elements of any TerraME object, such as [Agent](../types/agent.md) or [Environment](../types/environment.md).  
  

### Arguments

- **#1**: A table.

### Usage

```
getn{name = "john", age = 20}
```

---

## **getNames** 

Return the names of a given object derived from a table. The output is a vector with the names as values alphabetically ordered.  
  

### Arguments

- **#1**: Any table or TerraME type that works as a table.

### Usage

```
t = {
    cover = "forest",
    area = 200,
    water = false
}

getNames(t) -- {"area", "cover", "water"}
```

### See also

- [isTable](./utils.md#isTable)

---

## **greaterByAttribute** 

Return a function that compares two tables (which can be, for instance, [Agents](../types/agent.md) or [Cells](../types/cell.md)). The function returns which one has a priority over the other, according to an attribute of the objects and a given operator. If the function was not successfully built it returns nil.  
  

### Arguments

- **#1**: A string with the name of the attribute.
- **#2**: A string with the operator, which can be ">", "<", "<=", or ">=". The default value is "<".

### Usage

```
cs = CellularSpace{
    xdim = 10,
    instance = Cell{cover = Random{min = 0, max = 1}}
}

t = Trajectory{
    target = cs,
    greater = greaterByAttribute("cover")
}
```

### See also

- [Group](../types/group.md)
- [Trajectory](../types/trajectory.md)

---

## **greaterByCoord** 

Return a function that compares two tables with x and y attributes (basically two regular [Cells](../types/cell.md)). The function returns which one has a priority over the other, according to a given operator.  
  

### Arguments

- **#1**: A string with the operator, which can be ">", "<", "<=", or ">=". The default value is "<".

### Usage

```
cs = CellularSpace{
    xdim = 10
}

t = Trajectory{
    target = cs,
    greater = greaterByCoord()
}
```

### See also

- [Trajectory](../types/trajectory.md)

---

## **integrate** 

A second order function to numerically solve ordinary differential equations with a given initial value.  
  

### Arguments

- **a**: A number with the beginning of the interval.
- **b**: A number with the end of the interval.
- **equation**: A differential equation or a vector of differential equations. Each equation is described as a function of one or two arguments that returns a value of its derivative f(t, y), where t is the time instant, and y starts with the value of attribute initial and changes according to the result of f() and the chosen method. The calls to f will use the first argument (t) in the interval [a,b[, according to the argument step.
- **event**: An [Event](../types/event.md) that can be used to set arguments a and b with values event:getTime() - event:getPeriodicity() and event:getTime(), respectively. The period of the event must be a multiple of step. Note that the first execution of the event will compute the equation relative to a time interval between event.time - event.period and event.time. Be careful about that, as it can start before the initial Event of the simulation.
- **initial**: The initial condition, or a vector of initial conditions, which must be satisfied. Each initial condition represents the value of y when t (first argument of f) is equal to the value of argument a.
- **method**: the name of a numeric algorithm to solve the ordinary differential equations. See the options below.

| Method            | Description                       |
| ----------------- | --------------------------------- |
| "euler" (default) | Euler integration method          |
| "heun"            | Heun (Second Order Euler)         |
| "rungekutta"      | Runge-Kutta Method (Fourth Order) |

- **step**: A positive number with the step within the interval. It must satisfy the condition that (b - a) is a multiple of step.

### Usage

```
v = integrate{
    equation = function(t, y)
        return t - 0.1 * y
    end,
    initial = 0,
    a = 0,
    b = 100,
    step = 0.1
}
```

---

## **integrationEuler** 

Implements the Euler (Euler-Cauchy) Method to integrate ordinary differential equations.  
  

### Arguments

- **#1**: The differential equation.
- **#2**: The initial condition that must be satisfied.
- **#3**: The value of 'a' in the interval [a,b[.
- **#4**: The value of 'b' of in the interval [a,b[.
- **#5**: The step of the independent variable.

### Usage

```
f = function(x) return x^3 end
v = integrationEuler(f, 0, 0, 3, 0.1)
```

---

## **integrationHeun** 

Implements the Heun (Euler Second Order) Method to integrate ordinary differential equations. It is a method of type Predictor-Corrector.  
  

### Arguments

- **#1**: The differential equation.
- **#2**: The initial condition that must be satisfied.
- **#3**: The value of 'a' in the interval [a,b[.
- **#4**: The value of 'b' of in the interval [a,b[.
- **#5**: The step of the independent variable.

### Usage

```
f = function(x) return x^3 end
v = integrationHeun(f, 0, 0, 3, 0.1)
```

---

## **integrationRungeKutta** 

Implements the Runge-Kutta Method (Fourth Order) to integrate ordinary differential equations.  
  

### Arguments

- **#1**: The differential equation.
- **#2**: The initial condition that must be satisfied.
- **#3**: The value of 'a' in the interval [a,b[.
- **#4**: The value of 'b' of in the interval [a,b[.
- **#5**: The step of the independent variable.

### Usage

```
f = function(x) return x^3 end
v = integrationRungeKutta(f, 0, 0, 3, 0.1)
```

---

## **isModel** 

Return whether a given value is a [Model](../types/model.md) or an instance of a Model.  
  

### Arguments

- **#1**: A value.

### Usage

```
print(isModel(2)) -- false
```

---

## **isTable** 

Return whether an object can be used as a table. This includes tables themselves as well as all TerraME types ([Cell](../types/cell.md), [CellularSpace](../types/cellularSpace.md), etc.).  
  

### Arguments

- **#1**: A value of any type.

### Usage

```
c = Cell{}
print(isTable(c))
```

### See also

- [type](./utils.md#type)

---

## **levenshtein** 

Return the Levenshtein's distance between two strings. See [http://en.wikipedia.org/wiki/Levenshtein_distance](http://en.wikipedia.org/wiki/Levenshtein_distance) for more details.  
  

### Arguments

- **#1**: A string.
- **#2**: Another string.

### Usage

```
levenshtein("abc", "abb")
```

---

## **replaceLatinCharacters** 

This function converts latin characters to hexadecimal code by the characters bytes. It is necessary to Windows [OS](./os.md) works correctly with latin characters. Also, it is necessary to set Lua locale as the same as the system locale. See os.setlocale() for more details. The list of unicode characters can be found in [https://en.wikipedia.org/wiki/List_of_Unicode_characters.](https://en.wikipedia.org/wiki/List_of_Unicode_characters.)  
  

### Arguments

- **#1**: A string.

### Usage

```
print(replaceLatinCharacters(��guia))
-- \xE1guia
```

---

## **round** 

Round a number given a precision.  
  

### Arguments

- **#1**: A number.
- **#2**: The number of decimal places to be used. The default value is zero.

### Usage

```
round(2.34566, 3)
```

---

## **string.endswith** 

Return whether a string ends with a given substring (no case sensitive).  
  

### Arguments

- **#1**: A string.
- **#2**: A substring describing the end of #1.

### Usage

```
string.endswith("abcdef", "def")
```

---

## **switch** 

Implement a switch case function, where functions are associated to the available options. This function returns a table that contains a function called caseof, that gets a named table with functions describing what to do for each case (which is the name for the respective function). This table can have a field "default" that is executed when the selected value is not one of the available options within caseof. The error messages of this function come from [switchInvalidArgumentMsg()](http://localhost:5500/old/files/ErrorHandling.html#switchInvalidArgumentMsg) and [switchInvalidArgumentSuggestionMsg()](http://localhost:5500/old/files/ErrorHandling.html#switchInvalidArgumentSuggestionMsg).  
  

### Arguments

- **#1**: A named table.
- **#2**: A string with the chosen attribute of the named table.

### Usage

```
data = {protocol = "udp"}

switch(data, "protocol"):caseof{
    tcp = function() print("tcp") end,
    udp = function() print("udp") end
}
```

---

## **toLabel** 

Convert a string into a more readable name. It is useful to work with [Model:init()](../types/model.md#init) when the model will be available through a graphical interface. In graphical interfaces (see [sessionInfo()](./os.md#sessioninfo)), if the string contains underscores, it replaces them by spaces and convert the next characters to uppercase. Otherwise, it adds a space before each uppercase character. It also converts the first character of the string to uppercase.  
  

### Arguments

- **#1**: A string with the parameter name.
- **#2**: A string with the name of the table the parameter belongs to. This parameter is optional.

### Usage

```
toLabel("maxValue") -- 'Max Value' (with graphical interface) or 'maxValue' (without)
```

---

## **type** 

Return the type of an object. It extends the original Lua type() to support TerraME objects, whose type name (for instance "[CellularSpace](../types/cellularSpace.md)" or "[Agent](../types/agent.md)") is returned instead of "table".  
  

### Arguments

- **#1**: Any object or value.

### Usage

```
c = Cell{value = 3}
print(type(c)) -- "Cell"
```

### See also

- [isTable](./utils.md#istable)

---

## **vardump** 

Function that returns a string describing the internal content of an object. It converts a table into a string that represents a Lua code that declares such table. If some internal object is named "parent", it will be converted into a string with the type of the object. It avoids infinite loops due to the internal cyclic representation of TerraME.  
  

### Arguments

- **#1**: The object to be converted into a string.
- **#2**: A string to be placed in the beginning of each line of the returning string.

### Usage

```
vardump{name = "john", age = 20}
-- {
--     age = 20,
--     name = "john"
-- }
```