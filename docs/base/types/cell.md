# Cell

A spatial location with homogeneous internal content. It is a table that may contain nearness relations as well as persistent and runtime attributes. Persistent attributes can be loaded from databases using [CellularSpace](./cellularSpace.md), while runtime attributes can be created along the simulation.  
  

### Arguments

- **init**: An optional function that describes how to initialize a Cell that is going to be used as an instance of a CellularSpace. See [init()](./cell.md#init).
- **x**: An integer number with the x location of the Cell. The default value is 0.
- **y**: An integer number with the y location of the Cell. The default value is 0.
- **...**: Any other attribute or function for the Cell.

### Attributes

Some attributes of Cell have internal semantics. They can be used as **read-only** by the modeler.

- **agents**: A vector with the [Agents](./agent.md) representing the default placement of the Cell. It is necessary to use [forEachAgent()](../functions/utils.md#foreachagent). This value is the same of "cell.placement.agents".
- **cObj_**: A pointer to a C++ representation of the Cell. Never use this object.
- **parent**: The CellularSpace it belongs.
- **past**: A copy of the attributes at the time of the last synchronization.
- **placement**: A [SocialNetwork](./socialNetwork.md) representing the default placement of the Cell (only when a call to [Environment:createPlacement()](./environment.md#createplacement) use the Cell).

### Usage

```
cell = Cell {
    cover = "forest",
    soilWater = 0
}
```

### See also

- [forEachNeighborhood (Utils)](../functions/utils.md#foreachneighborhood)

## Functions

|                                                                              |                                                                                                                                                       |
| ---------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------- |
| [addNeighborhood](./cell.md#addneighborhood) | Add a new [Neighborhood](./neighborhood.md) to the Cell.                                                              |
| [area](./cell.md#area)                       | Return the Cell area.                                                                                                                                 |
| [distance](./cell.md#distance)               | Returns the shortest distance between the cells.                                                                                                      |
| [getAgent](./cell.md#getagent)               | Return an [Agent](./agent.md) that belongs to the Cell.                                                               |
| [getAgents](./cell.md#getagents)             | Return the [Agents](./agent.md) that belong to the Cell.                                                              |
| [getId](./cell.md#getid)                     | Return a string with the unique identifier of the Cell.                                                                                               |
| [getNeighborhood](./cell.md#getneighborhood) | Return a [Neighborhood](./neighborhood.md) of the Cell.                                                               |
| [init](./cell.md#init)                       | User-defined function that is used to initialize a Cell when a [CellularSpace](./cellularSpace.md) is created.        |
| [isEmpty](./cell.md#isempty)                 | Return whether the cell is empty according to a given placement.                                                                                      |
| [notify](./cell.md#notify)                   | Notify every Observer connected to the Cell.                                                                                                          |
| [on_synchronize](./cell.md#on_synchronize)   | An optional user-defined function that is activated just after one calls [Cell:synchronize()](./cell.md#synchronize). |
| [sample](./cell.md#sample)                   | Return a random Cell from a [Neighborhood](./neighborhood.md) of the Cell.                                            |
| [setId](./cell.md#setid)                     | Update the unique identifier of the Cell.                                                                                                             |
| [synchronize](./cell.md#synchronize)         | Synchronizes the Cell.                                                                                                                                |
| [#](./cell.md#)                             | Return the number of [Neighborhoods](./neighborhood.md) in the Cell.                                                  |

---

## **addNeighborhood** 

Add a new [Neighborhood](./neighborhood.md) to the Cell. This function replaces previous Neighborhood with the same name (if it exists) without showing any warning message.  
  

### Arguments

- **#1**: A Neighborhood.
- **#2**: Neighborhood's name. The default value is "1".

### Usage

```
c1 = Cell{}
c2 = Cell{}
n = Neighborhood()

n:add(c2)
c1:addNeighborhood(n)
```

### See also

- [Neighborhood](./neighborhood.md)

---

## **area** 

Return the Cell area.  
  

### Usage

```
cell:area()
```

---

## **distance** 

Returns the shortest distance between the cells. If the cell do not have geometry, it calculates the Euclidean distance to a given Cell using the attributes x and y of both Cells.  
  

### Arguments

- **#1**: Other Cell.

### Usage

```
c1 = Cell{x = 5, y = 5}
c2 = Cell{x = 10, y = 10}
dist = c1:distance(c2)
print(dist)
```

---

## **getAgent** 

Return an [Agent](./agent.md) that belongs to the Cell. It assumes that there is at most one Agent per Cell. If there is no Agent within the cell then it returns nil.  
  

### Arguments

- **#1**: A string with the name of the placement. The default value is "placement".

### Usage

```
ag = Agent{}
s = Society{instance = ag, quantity = 2}
ag1 = s.agents[1]
cs = CellularSpace{xdim = 3}
c = cs.cells[1]
myEnv = Environment{cs, ag1}

myEnv:createPlacement{strategy = "void"}

ag1:enter(c)
if c:getAgent() == ag1 then
    print("equal")
end
```

---

## **getAgents** 

Return the [Agents](./agent.md) that belong to the Cell. The returning vector.  
  

### Arguments

- **#1**: A string with the name of the placement. The default value is "placement".

### Usage

```
ag = Agent{}
s = Society{instance = ag, quantity = 2}
ag1 = s.agents[1]
cs = CellularSpace{xdim = 3}
c = cs.cells[1]
myEnv = Environment{cs, ag1}

myEnv:createPlacement{strategy = "void"}

ag1:enter(c)
if c:getAgents()[1] == ag1 then
    print("equal")
end
```

---

## **getId** 

Return a string with the unique identifier of the Cell. Note that any Cell that belongs to a [CellularSpace](./cellularSpace.md) has an id.  
  

### Usage

```
cell = Cell{id = "2"}
id = cell:getId()
print(id)
```

---

## **getNeighborhood** 

Return a [Neighborhood](./neighborhood.md) of the Cell. If the Neighborhood does not exist then it returns nil.  
  

### Arguments

- **#1**: A string with the neighborhood's name to be retrieved. The default value is "1".

### Usage

```
cs = CellularSpace{
    xdim = 10
}

cs:createNeighborhood()

n = cs:sample():getNeighborhood()
print(#n)
```

---

## **init** 

User-defined function that is used to initialize a Cell when a [CellularSpace](./cellularSpace.md) is created. This function gets the Cell itself as argument.  
  

### Usage

```
cell = Cell{
    init = function(self)
        self.population = Random():integer(1, 100) -- initial population chosen randomly
    end,
    -- ...
}

cs = CellularSpace{
    xdim = 10,
    instance = cell
}

print(cs:sample().population)
```

### See also

- [Random](./random.md)

---

## **isEmpty** 

Return whether the cell is empty according to a given placement. An empty Cell does not contain any [Agent](./agent.md).  
  

### Arguments

- **#1**: A string with the name of the placement. The default value is "placement".

### Usage

```
ag = Agent{}
s = Society{instance = ag, quantity = 2}
ag1 = s.agents[1]
cs = CellularSpace{xdim = 3}
c = cs.cells[1]
myEnv = Environment{cs, ag1}

myEnv:createPlacement{strategy = "void"}

ag1:enter(c)
if not c:isEmpty() then
    print("not empty")
end
```

---

## **notify** 

Notify every Observer connected to the Cell.  
  

### Arguments

- **#1**: A positive number representing the notification time. The default value is zero. It is also possible to use an [Event](./event.md) as argument. In this case, it will use the result of [Event:getTime()](./event.md#gettime).

### Usage

```
cell = Cell{value = 5}
Chart{target = cell}

cell:notify(1)
cell:notify(2)
```

---

## **on_synchronize** 

An optional user-defined function that is activated just after one calls [Cell:synchronize()](./cell.md#synchronize).  
  

### Usage

```
cell = Cell{
    value = 3,
    on_synchronize = function(self)
        self.value = 0
    end
}

cell:synchronize()
print(cell.value) -- 0
```

---

## **sample** 

Return a random Cell from a [Neighborhood](./neighborhood.md) of the Cell.  
  

### Arguments

- **#1**: A string with the name of the Neighborhood. The default value is "1".

### Usage

```
cs = CellularSpace{
    xdim = 10
}

cs:createNeighborhood()

cell = cs:sample()
neigh = cell:sample()
print(type(neigh))
```

### See also

- [getNeighborhood](./cell.md#getneighborhood)

---

## **setId** 

Update the unique identifier of the Cell.  
  

### Arguments

- **#1**: A string with the new unique identifier.

### Usage

```
cell = Cell{id = "2"}
cell:setId("newid")
id = cell:getId()
print(id)
```

---

## **synchronize** 

Synchronizes the Cell. TerraME can keep two copies of the attributes of a Cell in memory: one stores the past values and the other stores the current (present) values. Synchronize copies the current values to a table named past, within the Cell. The previous past is therefore overwritten. In the end synchronize, it calls [Cell:on_synchronize()](./cell.md#on_synchronize) if it exists.  
  

### Usage

```
cell = Cell{value = 5}

cell:synchronize()
print(cell.past.value)
```

### See also

- [synchronize (CellularSpace)](./cellularSpace.md#synchronize)

---

## **#** 

Return the number of [Neighborhoods](./neighborhood.md) in the Cell.  
  

### Usage

```
cell = Cell{}
cell:addNeighborhood(Neighborhood())
cell:addNeighborhood(Neighborhood())

size = #cell
print(size)
```