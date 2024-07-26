# Neighborhood

A Neighborhood is a set of pairs (cell, weight), where cell is a neighbor [Cell](./cell.md) and weight is a number storing the relation's strength. Each Cell can have one or more Neighborhoods to represent its proximity relations.  
  
This type is used to create Neighborhoods from scratch to be used by [Cell:addNeighborhood()](./cell.md#addneighborhood). To create well-established Neighborhoods see [CellularSpace:createNeighborhood()](./cellularSpace.md#createneighborhood). Neighborhoods can also be loaded from external soures using [CellularSpace:loadNeighborhood()](./cellularSpace.md#loadneighborhood). It is recommended that a Neighborhood should contain only Cells that belong to the same [CellularSpace](./cellularSpace.md), as it guarantees that all its Cells have unique identifiers. Calling [forEachNeighbor()](../functions/utils.md#foreachneighbor) from a Cell traverses one of its Neighborhoods.  
  

### Usage

```
n = Neighborhood()
n = Neighborhood{}
```

---

## Functions

|                                                                            |                                                                                                            |
| -------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------- |
| [add](./neighborhood.md#add)               | Add a new [Cell](./cell.md) to the Neighborhood.                           |
| [clear](./neighborhood.md#clear)           | Remove all [Cells](./cell.md) from the Neighborhood.                       |
| [getWeight](./neighborhood.md#getweight)   | Return the weight of the connection to a given neighbor [Cell](./cell.md). |
| [isEmpty](./neighborhood.md#isempty)       | Return whether the Neighborhood does not contain any [Cell](./cell.md).    |
| [isNeighbor](./neighborhood.md#isneighbor) | Return whether a given [Cell](./cell.md) belongs to the Neighborhood.      |
| [remove](./neighborhood.md#remove)         | Remove a [Cell](./cell.md) from the Neighborhood.                          |
| [sample](./neighborhood.md#sample)         | Return a random [Cell](./cell.md) from the Neighborhood.                   |
| [setWeight](./neighborhood.md#setweight)   | Update a weight of the connection to a given neighbor [Cell](./cell.md).   |
| [#](./neighborhood.md##)                   | Return the number of [Cells](./cell.md) in the Neighborhood.               |


---

## **add** 

Add a new [Cell](./cell.md) to the Neighborhood. If the Neighborhood already contains such Cell then it will stop with an error.  
  

### Arguments

- **#1**: A Cell to be added.
- **#2**: A number representing the weight of the connection. The default value is 1.

### Usage

```
n = Neighborhood()
c = Cell{}
n:add(c, 0.02)
```

---

## **clear** 

Remove all [Cells](./cell.md) from the Neighborhood. In practice, it has the same behavior as calling Neighborhood() again if the Neighborhood was not added to any Cell.  
  

### Usage

```
n = Neighborhood()
n:clear()
```

---

## **getWeight** 

Return the weight of the connection to a given neighbor [Cell](./cell.md). It returns nil when the Cell is not a neighbor.  
  

### Arguments

- **#1**: A Cell.

### Usage

```
c = Cell{}
n = Neighborhood()
n:add(c, 0.5)

print(n:getWeight(c))
```

---

## **isEmpty** 

Return whether the Neighborhood does not contain any [Cell](./cell.md).  
  

### Usage

```
n = Neighborhood()

if n:isEmpty() then
    print("is empty")
end
```

---

## **isNeighbor** 

Return whether a given [Cell](./cell.md) belongs to the Neighborhood.  
  

### Arguments

- **#1**: A Cell.

### Usage

```
n = Neighborhood()
c = Cell{}

n:add(c)
if n:isNeighbor(c) then
    print("is neighbor")
end
```


---

## **remove** 

Remove a [Cell](./cell.md) from the Neighborhood.  
  

### Arguments

- **#1**: The Cell that is going to be removed.

### Usage

```
c1 = Cell{id = "1"}
c2 = Cell{id = "2"}

n = Neighborhood()
n:add(c1)
n:add(c2)

print(#n)
n:remove(c1)
print(#n)
```

---

## **sample** 

Return a random [Cell](./cell.md) from the Neighborhood.  
  

### Usage

```
c1 = Cell{id = "1"}
c2 = Cell{id = "2"}

n = Neighborhood()
n:add(c1)
n:add(c2)

cell = n:sample()
print(type(cell))
```

---

## **setWeight** 

Update a weight of the connection to a given neighbor [Cell](./cell.md).  
  

### Arguments

- **#1**: A Cell.
- **#2**: A number with the new weight.

### Usage

```
c = Cell{}
n = Neighborhood()
n:add(c, 0.5)

print(n:getWeight(c))
n:setWeight(c, 0.01)
print(n:getWeight(c))
```

---

## **#** 

Return the number of [Cells](./cell.md) in the Neighborhood.  
  

### Usage

```
n = Neighborhood()

print(#n)
```