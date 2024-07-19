# Automaton

A hybrid state machine that needs to be located on a [CellularSpace](./cellularSpace.md), and is replicated over each [Cell](./cell.md) of the space. It has independent [States](./state.md) in each Cell.  
  

### Arguments

- **id**: A string that names the Automanton.

### Attributes

Some attributes of Automaton have internal semantics. They can be used as **read-only** by the modeler.

- **parent**: The [Environment](./environment.md) it belongs.

### Usage

```
automaton = Automaton {
    id = "MyAutomaton",
    State {...},
    -- ...
    State {...}
}
```

---

## Functions

|   |    |
| ----- | ----- |
| [add](./automaton.md#add)                                 | Add a new [Trajectory](./trajectory.md) or [State](./state.md) to the Automaton. |
| [execute](./automaton.md#execute)                         | Execute the [State](./state.md) machine.                                                                         |
| [getId](./automaton.md#getid)                             | Return the unique identifier name of the Automaton.                                                                                              |
| [getState](./automaton.md#getstate)                       | Get a [State](./state.md) of the Automaton according to a given position.                                        |
| [getStateName](./automaton.md#getstatename)               | Return the name of the current [State](./state.md).                                                              |
| [getStates](./automaton.md#getstates)                     | Get all the [States](./state.md) inside the Automaton.                                                           |
| [notify](./automaton.md#notify)                           | Notify every Observer connected to the Automaton.                                                                                                |
| [setId](./automaton.md#setid)                             | Set the unique identifier of the Automaton.                                                                                                      |
| [setTrajectoryStatus](./automaton.md#settrajectorystatus) | Activate or not the [Trajectories](./trajectory.md) defined for the Automaton.                                   |

## **add** 

Add a new [Trajectory](./trajectory.md) or [State](./state.md) to the Automaton. It returns a boolean value indicating whether the new element was successfully added.  
  

### Arguments

- **#1**: A Trajectory or State.

### Usage

```
automaton:add(state)
automaton:add(trajectory)
```

---

## **execute** 

Execute the [State](./state.md) machine. First, it executes the [Jump](./jump.md) of the current State while it jumps from State to State. When the machine stops jumping, it executes all the [Flows](./flow.md) of the current State. Usually, this function is called within an [Event](./event.md), thus the time of the Event can be got from the [Timer](./timer.md). It returns a boolean value indicating whether the Jumps were executed correctly.  
  

### Arguments

- **#1**: An Event.

### Usage

```
automaton:execute(event)
```

---

## **getId** 

Return the unique identifier name of the Automaton.  

### Usage

```
automaton:getId()
```

---

## **getState** 

Get a [State](./state.md) of the Automaton according to a given position.  
  

### Arguments

- **#1**: A number indicating the position of the State to be retrieved.

### Usage

```
state = automaton:getState(1)
```

---

## **getStateName** 

Return the name of the current [State](./state.md). As an Automaton has independent States in each [Cell](./cell.md), it requires a location to return its State name.  
  

### Arguments

- **#1**: A Cell.

### Usage

```
id = automaton:getStateName(cell)
```

---

## **getStates** 

Get all the [States](./state.md) inside the Automaton. It returns a vector.  
  

### Usage

```
state = automaton:getStates()[1]
```

---

## **notify** 

Notify every Observer connected to the Automaton.  
  

### Arguments

- **#1**: An integer number representing the notification time. The default value is zero. It is also possible to use an [Event](./event.md) as argument. In this case, it will use the result of [Event:getTime()](./event.md#gettime).

### Usage

```
automaton:notify()
```

---

## **setId** 

Set the unique identifier of the Automaton. Return a boolean value indicating whether the id was changed correctly.  
  

### Arguments

- **#1**: A string that names the Automaton.

### Usage

```
automaton:setId("newid")
```

---

## **setTrajectoryStatus** 

Activate or not the [Trajectories](./trajectory.md) defined for the Automaton. Returns whether the change was successfully executed. When the Automaton is built its status is not activated.  
  

### Arguments

- **#1**: A boolean that indicates if the Trajectories will be activated.

### Usage

```
automaton:setTrajectoryStatus(true)
```