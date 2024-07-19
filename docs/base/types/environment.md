# Environment

A container that encapsulates space, time, behavior, and other Environments. Objects can be added directly when the Environment is declared or after it has been instantiated. It can control the simulation engine, synchronizing all the [Timers](./timer.md) within it, or instantiate relations between sets of objects. Calling [forEachElement()](../functions/utils.md#foreachelement) traverses each object of an Environment. If the Environment has a set of [Model](./model.md) instances, it is possible to call [forEachModel()](../functions/utils.md#forEachModel) to traverse them.  
  

### Arguments

- **...**: [Agents](./agent.md), [Automatons](./automaton.md), [Cells](./cell.md), [CellularSpaces](./cellularSpace.md), [Societies](./society.md), [Trajectories](./trajectory.md), [Groups](./group.md), Timers, Environments, or instances of Models.

### Attributes

Some attributes of Environment have internal semantics. They can be used as **read-only** by the modeler.

- **cObj_**: A pointer to a C++ representation of the Environment. Never use this object.

### Usage

```
environment = Environment{
    cs1 = CellularSpace{xdim = 10},
    ag1 = Agent{},
    t1 = Timer{}
}
```

---

## Functions

|                                                                                       |                                                                                                                                                                                 |
| ------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [add](./environment.md#add)                           | Add an element to the Environment.                                                                                                                                              |
| [createPlacement](./environment.md#createplacement)   | Create relations between behavioural entities ([Agents](./agent.md)) and spatial entities ([Cells](./cell.md)). |
| [getTime](./environment.md#gettime)                   | Return the older simulation time of its [Timers](./timer.md).                                                                                   |
| [loadNeighborhood](./environment.md#loadneighborhood) | Load a [Neighborhood](./neighborhood.md) between two different [CellularSpaces](./cellularSpace.md).            |
| [notify](./environment.md#notify)                     | Notify every Observer connected to the Environment.                                                                                                                             |
| [run](./environment.md#run)                           | Run the Environment until a given time.                                                                                                                                         |

## **add** 

Add an element to the Environment.  
  

### Arguments

- **#1**: An [Agent](./agent.md), [Automaton](./automaton.md), [Cell](./cell.md), [CellularSpace](./cellularSpace.md), [Society](./society.md), [Trajectory](./trajectory.md), [Group](./group.md), [Event](./event.md), [Timer](./timer.md), Environment, or table. When adding a table, this function converts the table into an Event. When adding an Event, this function converts the Event into a Timer that contains the Event itself.

### Usage

```
environment = Environment{}

cs1 = CellularSpace{xdim = 10}
ag1 = Agent{}
t1 = Timer{}

environment:add(cs1)
environment:add(ag1)
environment:add(t1)
```

---


## **createPlacement** 

Create relations between behavioural entities ([Agents](./agent.md)) and spatial entities ([Cells](./cell.md)). It is possible to have more than one behavioural entity within the Environment, but it must have only one [CellularSpace](./cellularSpace.md), [Trajectory](./trajectory.md), or Cell. When distributing Agents over a Trajectory or a Cell, the Agents will be able to move over the whole CellularSpace. Note that this function uses rules that will be used only to build the placement. It is up to the modeler to implement such rules for the rest of the simulation if needed. For example, one can use argument max equals to one to indicate that the placement must have at most one Agent per Cell, but it works only to create the placement, having no effect along the simulation.  
  

### Arguments

- **max**: A number representing the maximum number of Agents that can enter in the same Cell when creating the placement. As default it will add at most one Agent per Cell. Note that using this argument does not ensure a maximum number of agents inside Cells along the simulation - controlling the maximum is always up to the modeler.
- **name**: A string with the name of the relation. The default value is "placement", which means that the modeler can use [Agent:enter()](./agent.md#enter), [Agent:move()](./agent.md#move), and [Agent:leave()](./agent.md#leave) without needing to refer to the name of the placement. If the name is different from the default value, the modeler will have to use the last argument of these functions with the name of the placement.
- **strategy**: A string containing the strategy to be used to create a placement between Agents and Cells. See the options below:

| Strategy          | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        | Arguments |
| ----------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------- |
| "random"(default) | Choose a Cell randomly and put max agents also chosen randomly. Repeat this process until allocate all Agents. The last Cell chosen might have less than max Agents. All the Cells that were not chosen in this process will remain empty.                                                                                                                                                                                                                                                                                                         | max, name |
| "spread"          | Choose a Cell randomly and put one agent also chosen randomly. Repeat this process until allocate all Agents. This strategy guarantees that the quantity of agents in each cell is up to max Agents.                                                                                                                                                                                                                                                                                                                                               | max, name |
| "uniform"         | Create placements uniformly. The first Agent enters in the first Cell, the second one in the second Cell, and so on. If it reaches the last Cell of the CellularSpace or Trajectory then it starts again in the first Cell. The last Cells will contain fewer Agents if the number of Agents is not proportional to the number of Cells. For example, placing a [Society](./society.md) with four Agents into a CellularSpace of three Cells will put two Agents in the first Cell and one in the other two Cells. | name      |
| "void"            | This strategy creates an empty placement in each Cell and Agent. It is necessary to use this strategy if the modeler needs to establish the relations between Agents and Cells by himself/herself. In this case, Agents cannot use [Agent:move()](./agent.md#move) or [Agent:walk()](./agent.md#walk) before calling [Agent:enter()](./agent.md#enter) explicitly.                                                                                 | name      |

### Usage

```
ag = Agent{}

soc = Society{
    instance = ag,
    quantity = 20
}

cs = CellularSpace{xdim = 10}
env = Environment{soc, cs}
env:createPlacement()
```

---

## **getTime** 

Return the older simulation time of its [Timers](./timer.md).  
  

### Usage

```
env = Environment{
    Timer{Event{action = function() end}}
}

env:run(10)
print(env:getTime())
```

---

## **loadNeighborhood** 

Load a [Neighborhood](./neighborhood.md) between two different [CellularSpaces](./cellularSpace.md).  
  

### Arguments

- **bidirect**: A boolean value. If true then, for each relation from [Cell](./cell.md) a to Cell b loaded from the file, it will also create a relation from b to a. The default value is false.
- **file**: A [File](./file.md) or a string with the name of the file to be loaded.
- **name**: A string with the name of the relation to be created. The default value is "1".

### Usage

```
river = CellularSpace{
    file = filePath("river.shp")
}

emas = CellularSpace{
    file = filePath("emas.shp")
}

env = Environment{emas, river}
env:loadNeighborhood{file = filePath("gpmlinesDbEmas.gpm", "base")}
```

### See also

- [filePath (Package)](../functions/package.md#filepath)

---

## **notify** 

Notify every Observer connected to the Environment.  
  

### Arguments

- **#1**: A number representing the notification time. The default value is zero. It is also possible to use an [Event](./event.md) as argument. In this case, it will use the result of [Event:getTime()](./event.md#gettime).

### Usage

```
env = Environment{}
env:notify()
```

---

## **run** 

Run the Environment until a given time. It activates the [Timers](./timer.md) it contains, the Timers of the Environments it contains, and so on.  
  

### Arguments

- **#1**: A number representing the final time. This funcion will stop when there is no [Event](./event.md) scheduled to a time less or equal to the final time. When using instances of [Models](./model.md) within the Environment (to simulate them at the same time), this argument is optional. In this case, the default value is the greater final time amongst all instances.

### Usage

```
env = Environment{
    Timer{Event{action = function()
        print("execute 1")
    end}},
    Timer{Event{action = function()
        print("execute 2")
    end}}
}
env:run(10)
```