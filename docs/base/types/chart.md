# Chart

Create a line chart showing the variation of one or more attributes (y axis) of an object. As default, x axis values come from the single argument of [update()](./chart.md#update). A Chart behaves according to its target's type. See the table below.  
  

| Type of the target  | Behavior  | Compulsory   | Unnecessary    |
| ----- | ------ | ------ | ------ |
| "[Agent](./agent.md)", "[Cell](./cell.md)", instance of a [Model](./model.md) | Plots how attributes change over time.                                                                                                                                                                                                                                                                                                                                                                           | target         | value                       |
| "[CellularSpace](./cellularSpace.md)"                                                                                                         | If the selected attributes belong to the [CellularSpace](./cellularSpace.md), it plots how attributes change over time. If only one attribute is selected and it belongs to the [Cells](./cell.md), then it plots the sum of the attribute values in the whole CellularSpace.                                                                    | select, target |                             |
| "[Map](./map.md)"                                                                                                                             | Works as a Chart created from a [CellularSpace](./cellularSpace.md), copying the values of arguments target, select, value, color, and label from the [Map](./map.md) to itself. It only works if the Map was created using grouping "uniquevalue". If some of the colors is white, the respective attribute value will be ignored by the Chart. | target         | color, label, select, value |
| "[Environment](./environment.md)"                                                                                                             | Plot how a given attribute from different [Models](./model.md).                                                                                                                                                                                                                                                                                                                  | select, target | value                       |
| "[Society](./society.md)"                                                                                                                     | Plot how attributes change over time. If no attribute is selected, it will plot the amount of [Agents](./agent.md) along the simulation.                                                                                                                                                                                                                                         | target         |                             |
| "[DataFrame](./dataFrame.md)"                                                                                                                 | Plot a set of values at once, without needing to call [Chart:update()](./chart.md#update).                                                                                                                                                                                                                                                                                       | target         | value                       |

### Arguments

- **color**: An optional table where each position is a color for the respective attribute, described as strings ("red", "green", "blue", "white", "black", "yellow", "brown", "cyan", "gray", "magenta", "orange", "purple", and their light and dark compositions, such as "lightGray" and "darkGray"), or as tables with three integer numbers representing RGB compositions.
- **label**: Vector of the same size of select that indicates the labels for each line of the Chart. The default value is the name of the attributes using [toLabel()](../functions/utils.md#tolabel).
- **pen**: The pen style for drawing lines. It can be one of "solid" (default), "dash", "dot", "dashdot", or "dashdotdot". It can be a vector or a single value.
- **select**: A vector of strings with the name of the attributes to be observed. If it is only a single value then it can also be described as a string. As default, it selects all the user-defined number attributes of the target. In the case of [Society](./society.md), if it does not have any numeric attributes then it will use the number of agents in the Society as attribute. The positions of the vector define the plot order. It draws starting from the first until the last position. When using an [Environment](./environment.md) as target, it is possible to use only one attribute name. The selected attribute must belong to the [Model](./model.md) instances it contains. Chart will then create one line for each Model instance. In this case, the selected attribute will be the default title for the Chart and the default labels will be the names of the Model instances in the Environment (if they are named) or else their [Model:title()](./model.md#title) values.
- **size**: The size of the symbol, in pixels. It can be a number to be used by all lines. or a vector of numbers, describing the size for each line. The default value is 7.
- **style**: The style of each line to be drawn. It can be a string, indicating that all lines will have the same style, or a vector of strings describing each line. The possible values are: "lines", "dots", "none", "steps", and "sticks". The default value is "lines" for all lines.
- **symbol**: The symbol to be used to draw the points of the Chart. It can be a string to be used by all lines, or a vector of strings, describing the symbol for each line. The available values are: "square", "diamond", "triangle", "ltriangle" (left), "dtriangle" (downwards triangle), "rtriangle" (right), "cross", "vcross" (vertical cross), "hline", "vline", "asterisk", "star", "hexagon", and "none" (default).
- **target**: The object to be observed.
- **title**: An overall title to the Chart. The default value is "". In the case of instances of Models, the default is [Model:title()](./model.md#title). When the title is a Model instance, it automatically uses the [Model:title()](./model.md#title) as its value.
- **value**: A vector of strings with the values to be observed. It is necessary when observing automatic functions from [CellularSpace](./cellularSpace.md) or Society that are created from string attributes. In this case, Chart will plot the quantity of each value described in this argument.
- **width**: The width of the lines to be drawn. It can be a number, indicating that all lines will be drawn with the same width, or a vector describing each line. The default value is width one for all lines.
- **xAxis**: Name of the attribute to be used as x axis (instead of time). In this case, notify() will not need its single argument for plotting Charts.
- **xLabel**: Name of the x-axis. It shows "Time" as default.
- **yLabel**: Name of the y-axis. It does not show any label as default.

### Usage

```
cs = CellularSpace{
    xdim = 10,
    value1 = 5,
    value2 = 7
}

chart = Chart{target = cs}

print(type(chart))

world = Cell{
    susceptible = 498,
    recovered = 0,
    infected = 2
}

Chart{
    target = world,
    width = 2,
    select = {"susceptible", "infected", "recovered"},
    style = {"dots", "steps", "sticks"},
    color = {"red", "green", "blue"}
}

data = DataFrame{
    first = 2000,
    step = 10,
    demand = {7, 8, 9, 10},
    limit = {0.1, 0.04, 0.3, 0.07}
}

Chart{
    target = data,
    select = "limit",
    color = "blue"
}
```

---

## Functions

|                                                               |                                                                                                                |
| ------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------- |
| [clear](./chart.md#clear)     | Clear the Chart.                                                                                               |
| [getData](./chart.md#getdata) | Return a [DataFrame](./dataFrame.md) with the values got from all its updates. |
| [restart](./chart.md#restart) | Restart the Chart keeping the old plots.                                                                       |
| [save](./chart.md#save)       | Save a Chart into a file.                                                                                      |
| [update](./chart.md#update)   | Update the Chart with the latest values of its target.                                                         |

## **clear** 

Clear the Chart.  
  

### Usage

```
cell = Cell{value = 1}
chart = Chart{target = cell}
chart:update(1)
chart:update(2)
chart:clear()
```

---

## **getData** 

Return a [DataFrame](./dataFrame.md) with the values got from all its updates.  
  

### Usage

```
cs = CellularSpace{
    xdim = 10,
    value1 = 5,
    value2 = 7
}

chart = Chart{target = cs}

chart:update(1)
chart:update(2)
chart:update(3)

data = chart:getData()
print(tostring(data))
```

---

## **restart** 

Restart the Chart keeping the old plots.  
  

### Usage

```
cell = Cell{value = 1}
chart = Chart{target = cell}
chart:update(1)
chart:update(2)
chart:restart()
chart:update(2)
chart:update(3)
```

---

## **save** 

Save a Chart into a file. Supported extensions are bmp, jpg, png, and tiff.  
  

### Arguments

- **#1**: A string with the file name.

### Usage

```
cs = CellularSpace{
    xdim = 10,
    value1 = 5,
    value2 = 7
}

chart = Chart{target = cs}

chart:update(1)
chart:update(2)
chart:update(3)
chart:save("file.bmp")
File("file.bmp"):delete()
```

---

## **update** 

Update the Chart with the latest values of its target. It is usually recommended to use the Chart as action of an [Event](./event.md) instead of calling this function explicitly.  
  

### Arguments

- **#1**: A number with the current time or an Event.

### Usage

```
cell = Cell{value = 1}
chart = Chart{target = cell}

chart:update(0)
chart:update(1)
chart:update(2)
```