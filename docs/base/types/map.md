# Map

Create a map with the spatial distribution of a given [CellularSpace](./cellularSpace.md), [Agent](./agent.md), or [Society](./society.md). It draws each element into the screen, according a given attribute. Each notify() draws the Map again in the screen.  
  

### Arguments

- **background**: A Map that can be used as background to plot a Society. It can also be a string with a color to be used as background.
- **color**: A table with the colors for the attributes. Colors can be described as strings ("red", "green", "blue", "white", "black", "yellow", "brown", "cyan", "gray", "magenta", "orange", "purple", and their light and dark compositions, such as "lightGray" and "darkGray"), as tables with three integer numbers representing RGB compositions, such as {0, 0, 0}, or even as a string with a ColorBrewer format (see [http://colorbrewer2.org/](http://colorbrewer2.org/)). The colors available and the maximum number of slices for each of them are:

| Name                                                                                                                         | Max |
| ---------------------------------------------------------------------------------------------------------------------------- | --- |
| Accent, Dark, Pastel2, Set2                                                                                                  | 8   |
| Pastel1, Set1                                                                                                                | 9   |
| BrBG, PRGn, RdYlGn, Spectral                                                                                                 | 11  |
| PiYG, PuOr, RdBu, RdGy, RdYlBu                                                                                               | 11  |
| Paired, Set3                                                                                                                 | 12  |
| Blues, BuGn, BuPu, GnBu, Greens, Greys, Oranges, OrRd, PuBu, PuBuGn, PuRd, Purples, RdPu, Reds, YlGn, YlGnBu, YlOrBr, YlOrRd | 20  |

- **font**: A string with a font name to draw Agents.
- **grid**: Draw a grid around the [Cells](./cell.md)? The default value is false.
- **grouping**: A string with the strategy to slice and color the data. See below.

| Grouping      | Description                                                                                                                                                                                                                                                                                                 | Compulsory arguments                    | Optional arguments                                         |
| ------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------- | ---------------------------------------------------------- |
| "equalsteps"  | The values are divided into a set of slices with the same range. Each slice is associated to a given color. Equalsteps require only two colors in the argument color, one for the minimum and the other for the maximum value. The other colors are computed from a linear interpolation of the two colors. | color, max, min, select, slices, target | grid, invert, precision, title                             |
| "placement"   | Observe a CellularSpace showing the number of Agents in each Cell. Values can be grouped in the same way of uniquevalue or equalsteps.                                                                                                                                                                      | color, target                           | grid, max, min, slices, title, value                       |
| "quantil"     | Aggregate the values into slices with approximately the same size. Values are ordered from lower to higher and then sliced. This strategy uses two colors in the same way of equalsteps.                                                                                                                    | color, max, min, select, slices, target | grid, invert, precision, title                             |
| "stdeviation" | Define slices according to the distribution of a given attribute. Values with similar positive or negative distances to the average will belong to the same slice.                                                                                                                                          | color, select, stdColor, target         | grid, precision, stdDeviation, title                       |
| "uniquevalue" | Associate each attribute value to a given color. Attributes with type string can only be sliced with this strategy. It can be used for CellularSpaces as well as for Society.                                                                                                                               | color, select, target, value            | background, font, grid, label, size, symbol, title         |
| "none"        | Does not execute any color slicing. It can be used for CellularSpaces as well as for Society.                                                                                                                                                                                                               |                                         | background, color, font, grid, size, symbol, target, title |

- **invert**: Invert the order of the colors when using ColorBrewer. The default value is false.
- **label**: A table with the labels for the attributes.
- **max**: The maximum value of the attribute (used only for numbers).
- **min**: The minimum value of the attribute (used only for numbers).
- **precision**: The number of decimal digits for slicing. It must be an integer number greater than zero. It indicates that differences less than 10^(-digits) will not be considered. It means that, for instance, if a slice is in the interval [1.0, 2.0] and precision is 2 (0.01), a value 0.99 might belong to such slice.
- **select**: A string with the name of the attribute to be visualized.
- **size**: The size of the font to be used to draw agents in space.
- **slices**: Number of colors to be used for plotting. It must be an integer number greater than one.
- **stdColor**: A table just as argument color. It is needed only when standard deviation is the chosen strategy.
- **stdDeviation**: When the grouping mode is stddeviation, it has to be one of "full", "half" "quarter", or "none".
- **symbol**: A string to be used to draw Agents in space. They can be any string, but there are some predefined symbols available. See the link Font in the left menu.
- **target**: A CellularSpace, Agent, or Society.
- **title**: A title for the Map to be shown on the top of the screen. Whenever the argument select is used, it is the default value for title.
- **value**: A table with the possible values for the selected attributes.

### Usage

```
cell = Cell{
    temperature = Random{min = 0, max = 50},
    seggregation = Random{0, 1, 2},
    forest = Random{min = 0, max = 1}
}

cs = CellularSpace{
    xdim = 10,
    instance = cell
}

Map{
    target = cs,
    select = "temperature",
    min = 0,
    max = 50,
    slices = 10,
    color = {"blue", "red"}
}

Map{
    target = cs,
    select = "seggregation",
    value = {0, 1, 2},
    color = {"blue", "green", "red"},
    label = {"low", "medium", "high"}
}

Map{
    target = cs,
    select = "forest",
    color  = "RdYlGn",
    min = 0,
    max = 1,
    slices = 10
}

-- Visualizing the result of a functiont.md
cell = Cell{
    cover = function(cell)
        if Random():number() > 0.2 then
            return "pasture"
        else
            return "soil"
        end
    end
}

cs = CellularSpace{
    xdim = 30,
    instance = cell
}

Map{
    target = cs,
    select = "cover",
    value = {"soil", "pasture"},
    color = {"brown", "green"}
}

-- Visualizing the agents of a Society
soc = Society{
    instance = Agent{},
    quantity = 20
}

cs = CellularSpace{
    xdim = 10
}

e = Environment{
    cs,
    soc
}

e:createPlacement{}

m = Map{
    target = soc,
    symbol = "smile",
    color = "yellow",
    background = "darkGreen",
    grid = true,
    size = 25
}
```

---

## Functions

|                                                           |                                                      |
| --------------------------------------------------------- | ---------------------------------------------------- |
| [save](./map.md#save)     | Save a Map into a file.                              |
| [update](./map.md#update) | Update the Map with the latest values of its target. |


---
## **save** 

Save a Map into a file. Supported extensions are bmp, jpg, png, and tiff.  
  

### Arguments

- **#1**: A string with the file name.

### Usage

```
cs = CellularSpace{
    xdim = 10
}

map = Map{
    target = cs,
    select = "x",
    min = 0,
    max = 10,
    slices = 4,
    color = "Blues"
}

map:save("file.bmp")
File("file.bmp"):delete()
```

---

## **update** 

Update the Map with the latest values of its target. It is usually recommended to use the Map as action of an [Event](./event.md) instead of calling this function explicitly.  
  

### Arguments

- **#1**: An optional argument that can be a number with the current time or an Event.

### Usage

```
cs = CellularSpace{
    xdim = 10
}

map = Map{
    target = cs,
    select = "x",
    min = 0,
    max = 10,
    slices = 4,
    color = "Blues"
}

map:update()
```