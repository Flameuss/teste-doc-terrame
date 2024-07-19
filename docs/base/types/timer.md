# Timer

A Timer is an event-based scheduler that runs the simulation. It contains a set of [Events](./event.md), allowing the simulation to work with processes that start independently and act in different periodicities. As default, it execute the Events in the order they were declared, but the arguments of Event (start, priority, and period) can change this order. Once a Timer has a given simulation time, it ensures that all the Events before that time were already executed. See [run()](./timer.md#run) for more details.  
  

### Arguments

- **...**: A set of Events.

### Attributes

Some attributes of Timer have internal semantics. They can be used as **read-only** by the modeler.

- **cObj_**: A pointer to a C++ representation of the Timer. Never use this object.
- **events**: An ordered vector with the Events.
- **time**: The current simulation time.

### Usage

```
timer = Timer{
    Event{action = function()
        print("each time step")
    end},
    Event{period = 2, action = function()
        print("each two time steps")
    end},
    Event{priority = "high", period = 4, action = function()
        print("each four time steps")
    end}
}

timer:run(10)
```

---

## Functions

|                                                                   |                                                                                                                     |
| ----------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------- |
| [add](./timer.md#add)             | Add a new [Event](./event.md) to the timer.                                         |
| [clear](./timer.md#clear)         | Remove all the [Events](./event.md) from the Timer.                                 |
| [getEvents](./timer.md#getevents) | Return a vector with the [Events](./event.md) of the Timer.                         |
| [getTime](./timer.md#gettime)     | Return the current simulation time.                                                                                 |
| [notify](./timer.md#notify)       | Notify every Observer connected to the Timer.                                                                       |
| [reset](./timer.md#reset)         | Reset the Timer to time minus infinite, keeping the same [Event](./event.md) queue. |
| [run](./timer.md#run)             | Run the Timer until a given final time.                                                                             |
| [#](./timer.md##)                 | Return the number of [Events](./event.md) in the Timer.                             |


---

## **add** 

Add a new [Event](./event.md) to the timer. If the Event has a start time less than the current simulation time then add() will prompt a warning (but the Event will be added).  
  

### Arguments

- **#1**: An Event or table. When adding a table, this function converts the table into an Event.

### Usage

```
timer = Timer{}

timer:add(Event{action = function() end})
```

---

## **clear** 

Remove all the [Events](./event.md) from the Timer. Note that, when this function is called within an action of an Event, if such function does not return false, it will be added to the Timer again after the end of its execution. This means that the simulation will continue with a single Event until its final time.  
  

### Usage

```
timer = Timer{
    Event{action = function() print("step") end}
}

timer:clear()
```

---

## **getEvents** 

Return a vector with the [Events](./event.md) of the Timer.  
  

### Usage

```
timer = Timer{
    Event{action = function() print("step") end}
}

print(timer:getEvents()[1]:getTime())
```

---

## **getTime** 

Return the current simulation time.  
  

### Usage

```
timer = Timer{
    Event{action = function() print("step") end}
}

timer:run(10)
print(timer:getTime())
```

---

## **notify** 

Notify every Observer connected to the Timer.  
  

### Usage

```
timer = Timer{
    Event{action = function() print("step") end}
}

Clock{target = timer}

timer:run(10)

timer:notify()
```

---

## **reset** 

Reset the Timer to time minus infinite, keeping the same [Event](./event.md) queue.  
  

### Usage

```
timer = Timer{
    Event{action = function() print("step") end}
}

Clock{target = timer}

timer:run(10)

timer:reset()
print(timer:getTime())
```

---

## **run** 

Run the Timer until a given final time. It manages the [Event](./event.md) queue according to their execution times and priorities. The Event with lower time will be executed in each step. If there are two Events to be executed at the same time, it executes the one with lower priority. If both have the same priority, it executes the one that was scheuled first for that time. In order to activate an Event, the Timer executes its action, passing the Event itself as argument. If the action of the Event does not return false, the Event is scheduled to execute again according to its period. The Timer then repeats its execution again and again. It stops only when all its Events are scheduled to execute after the final time, or when there are no remaining Events.  
  

### Arguments

- **#1**: A number representing the final time of the simulation. This argument is mandatory.

### Usage

```
timer = Timer{
    Event{action = function() print("step") end}
}

timer:run(10)
```
---

## **#** 

Return the number of [Events](./event.md) in the Timer.  
  

### Usage

```
timer = Timer{
    Event{action = function()
        print("each time step")
    end},
    Event{period = 2, action = function()
        print("each two time steps")
    end}
}

print(#timer)
```