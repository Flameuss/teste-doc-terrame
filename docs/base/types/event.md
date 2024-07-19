# Event

An Event represents a time instant when the simulation engine must execute some computation. In order to be executed, Events must belong to a [Timer](./timer.md). An Event is usually rescheduled to be executed again according to its period, unless its action explicitly returns false.  
  

### Arguments

- **action**: A function that will be executed when the Event is activated. It has one single argument, the Event itself. If the action returns false, the Event is removed from the Timer and will not be executed again. When the action will execute a single function of a TerraME object, it is possible to use [call()](../functions/utils.md#call). Action can also be a TerraME object. In this case, each type has its own set of functions that will be activated by the Event. See below how the objects are activated. Arrows indicate the execution order:

| Object                                                                                                                                                                                                                                                                                                                                                                                                      | Function(s) activated by the Event       | Default priority |
| --------------------------------------------------------------------------------------------------- | ---------------------------------------- | ---------------- |
| [Agent](./agent.md)/[Automaton](./automaton.md)                                                                                                                     | execute                                  | 0 ("medium")     |
| [CellularSpace](./cellularSpace.md)/[Cell](./cell.md)                                                                                              | synchronize and then execute (if exists) | -5 ("high")      |
| [Chart](./chart.md)/[Map](./map.md)/[Clock](./clock.md)/[Log](./log.md)/[InternetSender](./internetSender.md)/[VisualTable](./visualTable.md)/[TextScreen](./textScreen.md) | update                                   | 10 ("verylow")   |
| function                                                                                                                                                                                                                                                                                                                                                                                                    | the function itself                      | 0 ("medium")     |
| [Model](./model.md)                                               | execute (if exists)                      | 0 ("medium")     |
| [Society](./society.md)                                                                                                   | synchronize and then execute (if exists) | 0 ("medium")     |
| [Trajectory](./trajectory.md)/[Group](./group.md)                                                                                                                                       | rebuild and then execute (if exists)     | 0 ("medium")     |

- **period**: A positive number representing the periodicity of the Event. The default value is 1. If it is zero or false, the Event will execute only once and then it will be removed from its Timer.
- **priority**: A number with the priority of the Event over other Events. Smaller values have higher priority. The default value depends on the type of its action. Priorities can also be defined as strings:

| Value      | Priority |
| ---------- | -------- |
| "verylow"  | 10       |
| "low"      | 5        |
| "medium"   | 0        |
| "high"     | -5       |
| "veryhigh" | -10      |

- **start**: A number representing the time instant when the Event will occur for the first time. The default value is one, except when using graphics (Chart, Map, Clock, etc.) as action. In this case the default value is zero, plotting the initial state of the simulation.

### Usage

```
event = Event {start = 1985, period = 2, priority = -1, action = function(event)
    print(event:getTime())
end}

agent = Agent{
    execute = function()
        print("executing")
    end
}

event2 = Event{
    start = 2000,
    action = agent
}

timer = Timer{event, event2}
timer:run(10)
```

---

## Functions

|                                                                       |                                                                                                                      |
| --------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------- |
| [config](./event.md#config)           | Change the attributes of the Event.                                                                                  |
| [getParent](./event.md#getparent)     | Return the [Timer](./timer.md) that contains the Event.                              |
| [getPeriod](./event.md#getperiod)     | Return the period of the Event.                                                                                      |
| [getPriority](./event.md#getpriority) | Return the priority of the Event.                                                                                    |
| [getTime](./event.md#gettime)         | Return the current simulation time, according to the [Timer](./timer.md) it belongs. |


---

## **config** 

Change the attributes of the Event. It will be rescheduled according to its new attributes if this function is called while the action is being executed. Be careful when using this function outside the events's action, because the scheduler will not update its queue. In this case, it is recommended to replace the Event by another one.  
  

### Arguments

- **period**: The new periodicity of the Event.
- **priority**: The new priority of the Event.
- **time**: The time instant the Event will occur.

### Usage

```
event = Event{start = 2, action = function() end}

event:config{priority = -1}
event:config{time = 10, period = 2}
```

---

## **getParent** 

Return the [Timer](./timer.md) that contains the Event.  
  

### Usage

```
event = Event {action = function(event)
    print(event:getTime())
end}

timer = Timer{event}

parent = event:getParent()
if parent == timer then
    print("equal")
end
```

---

## **getPeriod** 

Return the period of the Event.  
  

### Usage

```
event = Event {start = 1985, period = 2, priority = -1, action = function(event)
    print(event:getTime())
end}

period = event:getPeriod()
print(period)
```

---

## **getPriority** 

Return the priority of the Event.  
  

### Usage

```
event = Event {start = 1985, period = 2, priority = -1, action = function(event)
    print(event:getTime())
end}

priority = event:getPriority()
print(priority)
```

---

## **getTime** 

Return the current simulation time, according to the [Timer](./timer.md) it belongs.  
  

### Usage

```
event = Event {start = 1985, period = 2, priority = -1, action = function(event)
    print(event:getTime())
end}

time = event:getTime()
print(time)
```