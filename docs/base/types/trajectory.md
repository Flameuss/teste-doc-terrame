# Trajectory (inherits [CellularSpace](./cellularSpace.md))

Type that defines an ordered selection over a [CellularSpace](./cellularSpace.md). It inherits CellularSpace; therefore it is possible to apply all functions of such type to a Trajectory. For instance, calling [forEachCell()](../functions/utils.md#foreachcell) also traverses Trajectories.  
  

### Arguments

- **build**: A boolean value indicating whether the Trajectory should be computed when created. The default value is true.
- **greater**: A function ([Cell](./cell.md), Cell)->boolean to sort the Trajectory. Such function must return true if the first Cell has priority over the second one. When using this argument, Trajectory compares each pair of Cells to establish an execution order to be used by [forEachCell()](../functions/utils.md#foreachcell). As default, the Trajectory will not be ordered and so [forEachCell()](../functions/utils.md#foreachcell) will run in the order the Cells were pushed into the CellularSpace. See [greaterByAttribute()](../functions/utils.md#greaterbyattribute) for predefined options for this argument.
- **random**: A boolean value indicating that the Trajectory must be shuffled. The Trajectory will be shuffled every time one calls [rebuild()](./trajectory.md#rebuild) or when the Trajectory is an action of an [Event](./event.md). This argument cannot be combined with argument greater.
- **select**: A function (Cell)->boolean indicating whether an Cell of the CellularSpace should belong to the Trajectory. If this function returns anything but false or nil for a given Cell, it will be added to the Trajectory. If this argument is missing, all Cells will be included in the Trajectory.
- **target**: The CellularSpace over which the Trajectory will take place.

### Attributes

Some attributes of Trajectory have internal semantics. They can be used as **read-only** by the modeler.

- **cells**: A vector of Cells pointed by the Trajectory.
- **cObj_**: A pointer to a C++ representation of the Trajectory. Never use this object.
- **greater**: The last function used to sort the Trajectory.
- **parent**: The CellularSpace where the Trajectory takes place.
- **select**: The last function used to filter the Trajectory.

### Usage

```
cell = Cell{
    cover = Random{"forest", "deforested"},
    dist = Random{min = 0, max = 50}
}

cs = CellularSpace{
    xdim = 10,
    instance = cell
}

traj = Trajectory{
    target = cs,
    select = function(c)
        return c.cover == "forest"
    end,
    greater = function(c, d)
        return c.dist < d.dist
    end
}

traj = Trajectory{
    target = cs,
    greater = function(c, d)
        return c.dist < d.dist
    end
}

traj = Trajectory{
    target = cs,
    build = false
}
```

---

## Functions

|                                                                        |                                                                                                                |
| ---------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------- |
| [add](./trajectory.md#add)             | Add a new [Cell](./cell.md) to the Trajectory.                                 |
| [clear](./trajectory.md#clear)         | Remove all [Cells](./cell.md) from the Trajectory.                             |
| [clone](./trajectory.md#clone)         | Return a copy of the Trajectory.                                                                               |
| [filter](./trajectory.md#filter)       | Apply the filter over the [Cells](./cell.md) of the Trajectory.                |
| [get](./trajectory.md#get)             | Return a [Cell](./cell.md) from the Trajectory given its x and y locations.    |
| [randomize](./trajectory.md#randomize) | Randomize the [Cells](./cell.md) of the Trajectory.                            |
| [rebuild](./trajectory.md#rebuild)     | Rebuild the Trajectory.                                                                                        |
| [save](./trajectory.md#save)           | Save a subset from the target [CellularSpace](./cellularSpace.md) into a file. |
| [sort](./trajectory.md#sort)           | Sort the current [CellularSpace](./cellularSpace.md) subset.                   |
| [#](./trajectory.md##)                 | Retrieve the number of [Cells](./cell.md) in the Trajectory.                   |

---

## **add** 

Add a new [Cell](./cell.md) to the Trajectory. It will be added to the end of the list of Cells.  
  

### Arguments

- **#1**: A Cell.

### Usage

```
cs = CellularSpace{
    xdim = 10
}

traj = Trajectory{
    target = cs,
    select = function(c)
        return c.x > 3
    end
}

traj:add(cs:get(1, 1))
```

---

## **clear** 

Remove all [Cells](./cell.md) from the Trajectory.  
  

### Usage

```
cs = CellularSpace{
    xdim = 10
}

traj = Trajectory{
    target = cs
}

traj:clear()

print(#traj)
```

---

## **clone** 

Return a copy of the Trajectory. It has the same parent, select, greater and [Cells](./cell.md). Any change in the cloned Trajectory will not affect the original one.  
  

### Usage

```
cell = Cell{
    cover = Random{"forest", "deforested"}
}

cs = CellularSpace{
    xdim = 10,
    instance = cell
}

traj = Trajectory{
    target = cs,
    select = function(c)
        return c.cover == "forest"
    end
}

copy = traj:clone()
print(#copy)
print(#traj)
```

---

## **filter** 

Apply the filter over the [Cells](./cell.md) of the Trajectory. Cells that belong to the [CellularSpace](./cellularSpace.md) but do not belong to the Trajectory are ignored. This way, this function creates a subset over the subset of the CellularSpace.  
  

### Usage

```
cell = Cell{
    dist = Random{min = 0, max = 50},
    increase = function(self)
        self.dist = self.dist + 2
    end
}

cs = CellularSpace{
    xdim = 10,
    instance = cell
}

traj = Trajectory{target = cs, select = function(c)
    return c.dist > 20
end}

traj:increase()
traj:filter()
```

---

## **get** 

Return a [Cell](./cell.md) from the Trajectory given its x and y locations. If the Cell does not belong to the Trajectory then it will return nil.  
  

### Arguments

- **#1**: The x location.
- **#2**: The y location.

### Usage

```
cs = CellularSpace{xdim = 10}

traj = Trajectory{target = cs}

traj:get(1, 1)
```

---

## **randomize** 

Randomize the [Cells](./cell.md) of the Trajectory. It will change the traversing order used by [forEachCell()](../functions/utils.md#foreachcell).  
  

### Usage

```
cs = CellularSpace{xdim = 10}

traj = Trajectory{target = cs}

traj:randomize()
```

---

## **rebuild** 

Rebuild the Trajectory. It works as if the Trajectory was declared again with the same arguments.  
  

### Usage

```
cell = Cell{
    dist = Random{min = 0, max = 50}
}

cs = CellularSpace{
    xdim = 10,
    instance = cell
}

traj = Trajectory{
    target = cs,
    select = function(cell) return cell.dist < 20 end,
    greater = function(c1, c2) return c1.dist < c2.dist end
}

print(#traj)
forEachCell(cs, function(cell)
    cell.dist = cell.dist + 10
end)

traj:rebuild()
print(#traj)
```

---

## **save** 

Save a subset from the target [CellularSpace](./cellularSpace.md) into a file.  
  

### Arguments

- **#1**: A [File](./file.md) which can be a .shp or .geojson extension.
- **#2**: A vector with the names of the attributes to be saved. If attrs is nil, all attributes will be saved.

### Usage

```
cs = CellularSpace{
    file = filePath("test/sampa.shp", "gis")
}

t = Trajectory{
    target = cs,
    select = function(cell)
        return cell.ID % 2 == 0
    end
}

t:save("odd.shp")
```

---

## **sort** 

Sort the current [CellularSpace](./cellularSpace.md) subset. It updates the traversing order of the Trajectory.  
  

### Usage

```
cell = Cell{
    dist = Random{min = 0, max = 50},
    increase = function(self)
        self.dist = self.dist + Random{min = 0, max = 3}:sample()
    end
}

cs = CellularSpace{
    xdim = 10,
    instance = cell
}

traj = Trajectory{target = cs, greater = function(c, d)
    return c.dist < d.dist
end}

traj:increase()
traj:sort()
```

---

## **#** 

Retrieve the number of [Cells](./cell.md) in the Trajectory.  
  

### Usage

```
cs = CellularSpace{
    xdim = 10
}

traj = Trajectory{
    target = cs
}

print(#traj)
```