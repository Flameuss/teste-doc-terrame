# CellularSpace

A multivalued set of [Cells](./cell.md). It can be retrieved from databases, files, or created directly within TerraME. Each spatial object read from a data source becomes a Cell, be it a point, a polygon, a line, or a pixel. If the Cells have attributes "row" and "col" (the name can be set by argument xy, as shown below), they can be used to [createNeighborhood()](./cellularSpace.md#createneighborhood) and to draw the CellularSpace in the screen by using a [Map](./map.md). The Cell with lower (row, col) represents the upper left location (see argument zero below). See the table below with the description and the arguments of each data source. Calling [forEachCell()](../functions/utils.md#foreachcell) traverses CellularSpaces.  
  

### Arguments

- **as**: A table with string indexes and values. It renames the loaded attributes of the CellularSpace from the values to its indexes.
- **attrname**: A string with an attribute name. It is useful for files that have only one attribute value for each cell but no attribute name. The default value is the name of the file being read.
- **directory**: A directory. It opens a set of tif files using the file names as attribute names. The directory must contains at least two tif files and they must have the same number of columns and rows.
- **file**: A string with a file name (if it is stored in the current directory), or the complete path to a given file.
- **geometry**: A boolean value indicating whether the geometry should also be loaded. The default value is true. If true, each cell will have an attribute called geom with a TerraLib object.
- **instance**: A Cell with the description of attributes and functions. When using this argument, each Cell will have attributes and functions according to the instance. It also calls [Cell:init()](./cell.md#init) from the instance for each of its Cells. Every attribute from the Cell that is a [Random](./random.md) will be converted into [Random:sample()](./random.md#sample). Additional functions are also created to the CellularSpace, according to the attributes of the instance. For each attribute of the instance, one function is created in the CellularSpace with the same name (note that attributes declared exclusively in [Cell:init()](./cell.md#init) will not be mapped, as they do not belong to the instance). The table below describes how each attribute is mapped:

| Type of attribute | Function within the CellularSpace                                                                                             |
| ----------------- | ----------------------------------------------------------------------------------------------------------------------------- |
| function          | Call the function of each of its Cells.                                                                                       |
| number            | Return the sum of the number in each of its Cells.                                                                            |
| boolean           | Return the quantity of true values in its Cells.                                                                              |
| string            | Return a table with positions equal to the unique strings and values equal to the number of occurrences in each of its Cells. |

- **layer**: A string with the name of the layer stored in a GIS project, or a [Layer (gis package)](http://localhost:5500/gis/doc/files/Layer.html).
- **missing**: An optional number that replaces all numeric attributes read from a data source that do not have any value. If this argument is not set and TerraME finds some attribute without a value, the simulation will stop with an error.
- **project**: A string with the name of the GIS project to be used. It can also be a [Project (gis package)](http://localhost:5500/gis/doc/files/Project.html).
- **sep**: A string with the file separator. The default value is ",".
- **source**: A string with the name of the data source. It tries to infer the data source according to the arguments passed to the function.

| source      | Description                                                                                                                                                                                                                                                                   | Compulsory arguments | Optional arguments                           |
| ----------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------- | -------------------------------------------- |
| "asc"       | Load an asc file. The name of the attribute will be b0.                                                                                                                                                                                                                       | file                 | as, ...                                      |
| "csv"       | Load from a Comma-separated value (.csv) file. Each column will become an attribute. It requires at least two attributes: x and y.                                                                                                                                            | file                 | as, geometry, sep, source, ...               |
| "directory" | Reads a set of tif files within a given directory. The name of the tif files will be the name of the attributes in the Cells.                                                                                                                                                 | directory            | as, ...                                      |
| "geojson"   | Load a GeoJSON file.                                                                                                                                                                                                                                                          | file                 | as, ...                                      |
| "nc"        | Load a nc file. The name of the attribute will be b0. It only works in Windows.                                                                                                                                                                                               | file                 |                                              |
| "pgm"       | Load from a text file where Cells are stored as numbers with its attribute value.                                                                                                                                                                                             |                      | as, attrname, sep, ...                       |
| "proj"      | Load from a layer within a GIS project. See the documentation of package gis for more information.                                                                                                                                                                            | layer, project       | as, geometry, missing, source, ...           |
| "shp"       | Load data from a shapefile. It requires three files with the same name and different extensions: .shp, .shx, and .dbf. The argument file must end with ".shp". As default, each Cell will have its (x, y) location according to the attributes (row, col) from the shapefile. | file                 | as, geometry, missing, source, xy, zero, ... |
| "tif"       | Load a tif file. The name of the attributes will be b0, b1, etc., according to the number of bands in the file.                                                                                                                                                               | file                 | as, ...                                      |
| "virtual"   | Create a rectangular CellularSpace from scratch. Cells will be instantiated with only two attributes, x and y, starting from (0, 0).                                                                                                                                          | xdim                 | as, geometry, ydim, ...                      |

- **xdim**: Number of columns, in the case of creating a CellularSpace without needing to load from a database.
- **xy**: An optional table with two strings describing the names of the column and row attributes, in this order. The default value is {"col", "row"}, representing the attribute names created by TerraLib for CellularSpaces. A Map can only be created from a CellularSpace if each Cell has a (x, y) location. This argument can also be a function that gets a Cell as argument and returns two values with the (x, y) location.
- **ydim**: Number of lines, in the case of creating a CellularSpace without needing to load from a database. The default value is equal to xdim.
- **zero**: A string value describing where the zero in the y axis starts. The default value is "bottom". When one uses argument xy, the default value is "top", which is the most common representation in different data formats. When zero is "bottom", the y values of each cell is inverted according to the maximum and minimum values: newy = y maximum - y + y minimum. All cellular data created using package gis will have their y values inverted.
- **...**: Any other attribute or function for the CellularSpace.

### Attributes

Some attributes of CellularSpace have internal semantics. They can be used as **read-only** by the modeler.

- **cells**: A vector of Cells pointed by the CellularSpace.
- **cObj_**: A pointer to a C++ representation of the CellularSpace. Never use this object.
- **parent**: The [Environment](./environment.md) it belongs.
- **xMax**: The maximum value of the attribute x of its Cells.
- **xMin**: The minimum value of the attribute x of its Cells.
- **yMax**: The maximum value of the attribute y of its Cells.
- **yMin**: The minimum value of the attribute y of its Cells.

### Usage

```
cs = CellularSpace{
    xdim = 20,
    ydim = 25
}

states = CellularSpace{
    file = filePath("brazilstates.shp", "base")
}

cabecadeboi = CellularSpace{
    file = filePath("cabecadeboi.shp")
}
```

---

## Functions

|   |    |
| --- | --- |
| [add](./cellularSpace.md#add)                               | Add a new [Cell](./cell.md) to the CellularSpace.                                                                           |
| [createNeighborhood](./cellularSpace.md#createneighborhood) | Create a [Neighborhood](./neighborhood.md) for each [Cell](./cell.md) of the CellularSpace. |
| [cut](./cellularSpace.md#cut)                               | Cut the CellularSpace according to maximum and minimum coordinates.                                                                                         |
| [get](./cellularSpace.md#get)                               | Return a [Cell](./cell.md) from the CellularSpace, given its unique identifier or its location.                             |
| [load](./cellularSpace.md#load)                             | Load the CellularSpace from the database.                                                                                                                   |
| [loadNeighborhood](./cellularSpace.md#loadneighborhood)     | Load a [Neighborhood](./neighborhood.md) stored in an external source.                                                      |
| [notify](./cellularSpace.md#notify)                         | Notify every Observer connected to the CellularSpace.                                                                                                       |
| [sample](./cellularSpace.md#sample)                         | Return a random [Cell](./cell.md) from the CellularSpace.                                                                   |
| [save](./cellularSpace.md#save)                             | Save the attributes of a CellularSpace into [Project (gis package)](http://localhost:5500/gis/doc/files/Project.html) or a tif file.                        |
| [split](./cellularSpace.md#split)                           | Split the CellularSpace into a table of [Trajectories](./trajectory.md) according to a classification strategy.             |
| [synchronize](./cellularSpace.md#synchronize)               | Synchronize the CellularSpace, calling the function synchronize() for each of its [Cells](./cell.md).                       |
| [#](./cellularSpace.md##)                                   | Return the number of [Cells](./cell.md) in the CellularSpace.                                                               |

## **add** 

Add a new [Cell](./cell.md) to the CellularSpace. It will be the last Cell of the CellularSpace when one uses [forEachCell()](../functions/utils.md#foreachcell).  
  

### Arguments

- **#1**: A Cell.

### Usage

```
cs = CellularSpace{
    xdim = 10
}

cell = Cell{x = 10, y = 11}
cs:add(cell)
```

---

## **createNeighborhood** 

Create a [Neighborhood](./neighborhood.md) for each [Cell](./cell.md) of the CellularSpace. Most of the available strategies require that each Cell has attributes with (x, y) locations. It is possible to set the attributes that represent (x, y) locations while creating the CellularSpace.  
  

### Arguments

- **filter**: A function(Cell, Cell)->bool, where the first argument is the Cell itself and the other represent a possible neighbor. It returns true when the neighbor will be included in the relation. In the case of two CellularSpaces, this function is called twice for e ach pair of Cells, first filter(c1, c2) and then filter(c2, c1), where c1 belongs to cs1 and c2 belongs to cs2. The default value is a function that returns true.
- **inmemory**: If true (default), a Neighborhood will be built and stored for each Cell of the CellularSpace. The Neighborhoods will change only if the modeler add or remove neighbors explicitly. If false, a Neighborhood will be computed every time the simulation calls [Cell:getNeighborhood()](./cell.md#getneighborhood), for example when using [forEachNeighbor()](../functions/utils.md#foreachneighbor). In this case, if any of the attributes the Neighborhood is based on changes then the resulting Neighborhood might be different. Neighborhoods not in memory also help the simulation to run with larger datasets, as they are not explicitly represented, but they consume more time as they need to be built again and again along the simulation.
- **m**: Number of columns. If m is even then it will be increased by one to keep the Cell in the center of the Neighborhood. The default value is 3.
- **n**: Number of rows. If n is even then it will be increased by one to keep the Cell in the center of the Neighborhood. The default value is m.
- **name**: A string with the name of the Neighborhood to be created. The default value is "1".
- **self**: Add the Cell as neighbor of itself? The default value is false. Note that the functions that do not require this argument always depend on a filter function, which will define whether the Cell can be neighbor of itself.
- **strategy**: A string with the strategy to be used for creating the Neighborhood. See the table below.

| Strategy         | Description                                                                                                      | Compulsory Arguments | Optional Arguments                                 |
| ---------------- | ---------------------------------------------------------------------------------------------------------------- | -------------------- | -------------------------------------------------- |
| "3x3"            | A 3x3 (Couclelis) Neighborhood (Deprecated. Use mxn instead).                                                    |                      | filter, inmemory, name, weight                     |
| "coord"          | A bidirected relation between two CellularSpaces connecting Cells with the same (x, y) coordinates.              | target               | inmemory, name                                     |
| "diagonal"       | Connect each Cell to its (at most) four diagonal neighbors.                                                      |                      | inmemory, name, self, wrap                         |
| "function"       | A Neighborhood based on a function where any other Cell can be a neighbor.                                       | filter               | inmemory, name, weight                             |
| "moore"(default) | A Moore (queen) Neighborhood, connecting each Cell to its (at most) eight touching Cells.                        |                      | inmemory, name, self, wrap                         |
| "mxn"            | A m (columns) by n (rows) Neighborhood within the CellularSpace or between two CellularSpaces if target is used. |                      | filter, inmemory, m, n, name, target, weight, wrap |
| "vonneumann"     | A von Neumann (rook) Neighborhood, connecting each Cell to its (at most) four ortogonally surrounding Cells.     |                      | inmemory, name, self, wrap                         |

- **target**: Another CellularSpace whose Cells will be used to create neighborhoods.
- **weight**: A function (Cell, Cell)->number, where the first argument is the Cell itself and the other represent its neighbor. It returns the weight of the relation. This function will be called only if filter returns true.
- **wrap**: Will the Cells in the borders be connected to the Cells in the opposite border? The default value is false.

### Usage

```
cell = Cell{
    height = Random{min = 0, max = 100}
}

cs = CellularSpace{
    xdim = 10,
    instance = cell
}

cs:createNeighborhood() -- moore

cs:createNeighborhood{
    name = "moore"
}

cs:createNeighborhood{
    strategy = "vonneumann",
    name = "vonneumann",
    self = true
}

cs:createNeighborhood{
    strategy = "mxn",
    m = 5,
    name = "5",
    filter = function(cell, candidate)
        return cell.height > candidate.height
    end,
    weight = function(cell, candidate)
        return (cell.height - candidate.height) / 100
    end
}


cs2 = CellularSpace{
    xdim = 10
}

cs:createNeighborhood{
    strategy = "mxn",
    target = cs2,
    m = 5,
    name = "spatialCoupling"
}
```

---

## **cut** 

Cut the CellularSpace according to maximum and minimum coordinates. It returns a [Trajectory](./trajectory.md) with the selected [Cells](./cell.md).  
  

### Arguments

- **xmax**: A number with the maximum value of x.
- **xmin**: A number with the minimum value of x.
- **ymax**: A number with the maximum value of y.
- **ymin**: A number with the minimum value of y.

### Usage

```
cs = CellularSpace{xdim = 10}

cs2 = cs:cut{xmin = 3, ymax = 8}
print(#cs2)
```

---

## **get** 

Return a [Cell](./cell.md) from the CellularSpace, given its unique identifier or its location. If the Cell does not belong to the CellularSpace then it will return nil.  
  

### Arguments

- **#1**: A number indicating an x coordinate. It can also be a string with the object id.
- **#2**: A number indicating a y coordinate. This argument is unnecessary when the first argument is a string.

### Usage

```
cs = CellularSpace{xdim = 10}

cell = cs:get(2, 2)
print(cell.x)
print(cell.y)

cell = cs:get("5")
print(cell:getId())
```


---

## **load** 

Load the CellularSpace from the database. TerraME automatically executes this function when the CellularSpace is created, but one can execute this to load the attributes again, erasing all attributes and relations created by the modeler.  
  

### Usage

```
cs = CellularSpace{xdim = 10}
cs:load()
```

---

## **loadNeighborhood** 

Load a [Neighborhood](./neighborhood.md) stored in an external source. Each [Cell](./cell.md) receives its own set of neighbors.  
  

### Arguments

- **check**: A boolean value indicating whether this function should match the layer name of the CellularSpace with the one described in the file. The default value is true.
- **file**: A [File](./file.md) or a string with the location of the Neighborhood file to be loaded.
- **name**: A string with the name of the Neighborhood to be loaded within TerraME. The default value is "1".

| Extension | Description                                                                |
| --------- | -------------------------------------------------------------------------- |
| "gal"     | Load a Neighborhood from contiguity relationships described as a GAL file. |
| "gwt"     | Load a Neighborhood from a GWT (generalized weights) file.                 |
| "gpm"     | Load a Neighborhood from a GPM (generalized proximity matrix) file.        |

### Usage

```
cs = CellularSpace{
    file = filePath("cabecadeboi800.shp", "base")
}

cs:loadNeighborhood{file = filePath("cabecadeboi-neigh.gpm", "base")}
```

---

## **notify** 

Notify every Observer connected to the CellularSpace.  
  

### Arguments

- **#1**: A number representing the notification time. The default value is zero. It is also possible to use an [Event](./event.md) as argument. In this case, it will use the result of [Event:getTime()](./event.md#gettime).

### Usage

```
cs = CellularSpace{
    xdim = 10,
    value = 5
}

Chart{target = cs}

cs:notify(1)
cs:notify(2)
```

---

## **sample** 

Return a random [Cell](./cell.md) from the CellularSpace.  
  

### Usage

```
cs = CellularSpace{
    xdim = 10
}

cell = cs:sample()
print(type(cell))
```

---

## **save** 

Save the attributes of a CellularSpace into [Project (gis package)](http://localhost:5500/gis/doc/files/Project.html) or a tif file.  
  

### Arguments

- **#1**: Name of the [Layer (gis package)](http://localhost:5500/gis/doc/files/Layer.html) or a tif file to store the saved attributes. If the original data comes from a shapefile layer, it will create another shapefile using the name of the new layer as file name and will save it in the same directory where the original shapefile is stored. If the data comes from a PostGIS database, it will create another table with name equals to the the layer's name. If the data come from a tif directory, it must be used a file with '.tif' extension.
- **#2**: A vector with the names of the attributes to be saved. If the data come from a layer, these attributes should be only the attributes that were created or modified. The other attributes of the layer will also be saved in the new output. If the data come from a tif directory, it is only possible save one attribute at a time. The attribute value saved will have the same type of the loaded tif files, it means, if the tif is 8 bits the new tif will be 8 bits as well. When saving a single attribute, you can use a string "attribute" instead of a table {"attribute"}.

### Usage

```
import("gis")

proj = Project{
    file = "amazonia.tview",
    clean = true,
    amazonia = filePath("amazonia.shp")
}

cs = CellularSpace{
    project = proj,
    layer = "amazonia"
}

forEachCell(cs, function(cell)
    cell.distweight = 1 / cell.distroad
end)

cs:save("myamazonia", "distweight")
```

---

## **split** 

Split the CellularSpace into a table of [Trajectories](./trajectory.md) according to a classification strategy. The Trajectories will have empty intersection and union equal to the whole CellularSpace (unless function below returns nil for some [Cell](./cell.md)). It works according to the type of its only and compulsory argument.  
  

### Arguments

- **#1**: A string or a function, as follows:

| Type of argument | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| ---------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| string           | The argument must represent the name of one attribute of the Cells of the CellularSpace.   Split then creates one Trajectory for each possible value of the attribute using the value as name and fills them with the Cells that have the respective attribute value. If the CellularSpace has an instance and the respective attribute in the instance is a [Random](./random.md) value with discrete or categorical strategy, it will use the possible values to create Trajectories, which means that the returning Trajectories can have size zero in this case. |
| function         | The argument is a function that gets a Cell as argument and returns a name for the Cell, which can be a number, string, or boolean value. Trajectories are then named according to the returning value.                                                                                                                                                                                                                                                                                                                                                                                            |

### Usage

```
cell = Cell{
    cover = Random{"pasture", "forest"},
    forest = Random{min = 0, max = 1}
}

cs = CellularSpace{
    xdim = 20,
    instance = cell
}

ts = cs:split("cover")
print(#ts.forest) -- can be zero because it comes from an instance
print(#ts.pasture) -- also

ts2 = cs:split(function(cell)
    if cell.forest > 0.5 then
        return "gt"
    else
        return "lt"
    end
end)

if ts2.gt then -- might not exist as it does not come from an instance
    print(#ts2.gt)
end
```

---

## **synchronize** 

Synchronize the CellularSpace, calling the function synchronize() for each of its [Cells](./cell.md).  
  

### Arguments

- **#1**: A string or a vector of strings with the attributes to be synchronized. If empty, TerraME synchronizes every attribute of the Cells but the (x, y) coordinates. If the CellularSpace has an instance and it implements [Cell:on_synchronize()](./cell.md#on_synchronize) then it will be called for each Cell.

### Usage

```
cell = Cell{
    forest = Random{min = 0, max = 1}
}

cs = CellularSpace{
    xdim = 10,
    instance = cell
}

cs:synchronize()
c = cs:sample()
print(c.forest)
print(c.past.forest)
```

---

## **#** 

Return the number of [Cells](./cell.md) in the CellularSpace.  
  

### Usage

```
cs = CellularSpace{xdim = 5}

print(#cs)
```