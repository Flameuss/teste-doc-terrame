# Agent

An autonomous entity that is capable of performing actions as well as interacting with other Agents and the spatial representation of the model. The Agent constructor gets a table containing the attributes and functions of the Agent. It can be described as a simple table or as a hybrid [State](./state.md) machine that has a unique internal state. When the Agent has a set of States, the initial State will be the one declared first. When the agent does not have States, there is a set of user-defined functions that have an associated semantics in TerraME. An Agent can belong to a [Society](./society.md) and can have [SocialNetworks](./socialNetwork.md).  
  

### Arguments

- execute: An optional function to describe the behavior of the agent each time step it is executed. See [execute()](./agent.md#execute).
- id: A string with the unique identifier of the Agent. Agents used as instance for a Society cannot have id as the Society will create the ids for each of its Agents.
- init: An optional function to be executed when the Agent enters in a Society. See [init()](./agent.md#init).
- on_message: An optional function describing the behavior of the agent when it receives a message. See [on_message()](./agent.md#on_message).
- ...: Any other attribute or function for the Agent. It can have, for instance, other "on_x" functions to get messages with subject "x" (see [message()](./agent.md#message)).

### Attributes

Some attributes of Agent have internal semantics. They can be used as read-only by the modeler.

- cells: A vector with the [Cells](./cell.md) representing the default placement of the Agent. It is necessary to use [forEachCell()](../functions/utils.md#foreachcell). This value is the same of "agent.placement.cells".
- cObj_: A pointer to a C++ representation of the Agent. Never use this object.
- id: The unique identifier of the Agent. This attribute only exists when the agent belongs to a Society.
- parent: The Society it belongs (if any).
- placement: A [Trajectory](./trajectory.md) representing the default placement of the Agent (only when a call to [Environment:createPlacement()](./environment.md#createplacement) use the Agent).
- socialnetworks: A set of SocialNetworks with the connections of the Agent. This value only exists if the Agent has at least one SocialNetwork.
- state_: An internal state for the Agent. Never use this object.

### Usage

```lua
singleFooAgent = Agent{
    size = 10,
    name = "foo",
    execute = function(self)
        self.size = self.size + 1
        self:walk()
    end,
    on_hello = function(self, m)
        self:message{
            receiver = m.sender,
            content = "hi"
        }
    end
}
```

---

## Functions

|         |         |
| ------- | ------- |
| [add](./agent.md#add)                                 | Add a [Trajectory](./trajectory.md) or a [State](./state.md) to the Agent.                                        |
| [addSocialNetwork](./agent.md#addsocialnetwork)       | Add a [SocialNetwork](./socialNetwork.md) to the Agent.                                                           |
| [die](./agent.md#die)                                 | Kill the agent and remove it from the [Society](./society.md) it belongs.                                         |
| [emptyNeighbor](./agent.md#emptyneighbor)             | Return an empty Neighbor [Cell](./cell.md).                                                                       |
| [enter](./agent.md#enter)                             | Put the Agent into a [Cell](./cell.md).                                                                           |
| [execute](./agent.md#execute)                         | The entry point for executing a given Agent.                                                                      |
| [getCell](./agent.md#getcell)                         | Return the [Cell](./cell.md) where the Agent is located according to its placement.                               |
| [getCells](./agent.md#getcells)                       | Return a vector with the [Cells](./cell.md) pointed by the Agent.                                                 |
| [getLatency](./agent.md#getlatency)                   | Return the time when the [State](./state.md) machine executed the transition to the current state.                |
| [getSocialNetwork](./agent.md#getsocialnetwork)       | Return a [SocialNetwork](./socialNetwork.md) of the Agent given its name.                                         |
| [getStateName](./agent.md#getstatename)               | Return a string with the current [State](./state.md) name.                                                        |
| [getTrajectoryStatus](./agent.md#gettrajectorystatus) | Return the status of the [Trajectories](./trajectory.md) of the Agent.                                            |
| [init](./agent.md#init)                               | User-defined function that is used to initialize an Agent when it enters in a given [Society](./society.md) (e.g. |
| [leave](./agent.md#leave)                             | Remove the Agent from its current [Cell](./cell.md).                                                              |
| [message](./agent.md#message)                         | Send a message to another Agent.                                                                                  |
| [move](./agent.md#move)                               | Move the Agent to a new [Cell](./cell.md).                                                                        |
| [notify](./agent.md#notify)                           | Notify the Observers of the Agent.                                                                                |
| [on_message](./agent.md#on_message)                   | User-defined function that can be implemented to allow Agents to exchange messages.                               |
| [reproduce](./agent.md#reproduce)                     | Create an Agent with the same behavior in the same [Cell](./cell.md) where the original Agent is (according to its placement).  |
| [sample](./agent.md#sample)                           | Return a random Agent from a [SocialNetwork](./socialNetwork.md) of the Agent.                                    |
| [setTrajectoryStatus](./agent.md#settrajectorystatus) | Activate or not the [Trajectories](./trajectory.md) defined for a given Agent.                                    |
| [walk](./agent.md#walk)                               | Execute a random walk to a neighbor [Cell](./cell.md).                                                            |
| [walkIfEmpty](./agent.md#walkifempty)                 | Choose a random Neighbor [Cell](./cell.md) and move if it is empty.                                               |
| [walkToEmpty](./agent.md#walktoempty)                 | Walk to one of the available empty [Cells](./cell.md) in the [Neighborhood](./neighborhood.md).                   |

---

## add 

Add a [Trajectory](./trajectory.md) or a [State](./state.md) to the Agent.  
  

### Arguments

- **#1**: A State or a Trajectory.

### Usage

```
ag = Agent{}
cs = CellularSpace{xdim = 5}
traj = Trajectory{target = cs}

ag:add(traj)
```

---

## addSocialNetwork

Add a [SocialNetwork](./socialNetwork.md) to the Agent. This function replaces previous SocialNetwork with the same id (if it exists) without showing any warning message.  
  

### Arguments

- **#1**: A SocialNetwork.
- **#2**: Name of the relation. The default value is "1".

### Usage

```
agent = Agent{}

soc = Society{
    instance = agent,
    quantity = 30
}

agent = soc:sample()
friend1 = soc:sample()
friend2 = soc:sample()

sn = SocialNetwork()
sn:add(friend1)

if friend2 ~= friend1 then
    sn:add(friend2)
end

agent:addSocialNetwork(sn)
```

### See also

- [forEachConnection (Utils)](../functions/utils.md#foreachconnection)

---

## die 

Kill the agent and remove it from the [Society](./society.md) it belongs. It also removes any basic placements from the agents (those used by [Agent:enter()](./agent.md#enter), [Agent:leave()](./agent.md#leave), and [Agent:move()](./agent.md#move)). After executing this function, it will not be possible to call any function from the Agent anymore. Therefore, if there is any complex placement in the model, it should be removed manually before calling this function.  
  

### Usage

```
agent = Agent{
    execute = function(self)
        if self.energy <= 0 then
            agent:die()
        end
    end
}
```

---

## emptyNeighbor 

Return an empty Neighbor [Cell](./cell.md). If there is no empty neighbor, it returns nil. The Agent needs to have a placement to be able to use this function, and the [CellularSpace](./cellularSpace.md) must have a [Neighborhood](./neighborhood.md). This function is recommended to be used only when it is possible to have only one Agent per Cell.  
  

### Arguments

- **#1**: A string representing the placement to be used. The default value is "placement".
- **#2**: A string representing the Neighborhood to be used. The default value is "1.

### Usage

```
singleFooAgent = Agent{}

cs = CellularSpace{xdim = 10}
cs:createNeighborhood()

e = Environment{cs, singleFooAgent}
e:createPlacement()

singleFooAgent:move(singleFooAgent:emptyNeighbor()) -- same as singleFooAgent:moveToEmpty()
```

### See also

- [createPlacement (Environment)](./environment.md#createplacement)

---

## enter 

Put the Agent into a [Cell](./cell.md). This function supposes that each Agent can be in one and only one Cell along the simulation. If the Agent is already inside of a Cell, use [Agent:move()](./agent.md#move) instead. The agent needs to have a placement to be able to use [Agent:enter()](./agent.md#enter), [Agent:leave()](./agent.md#leave), [Agent:move()](./agent.md#move), or [Agent:walk()](./agent.md#walk).  
  

### Arguments

- **#1**: A Cell.
- **#2**: A string representing the name of the placement to be used. The default value is "placement".

### Usage

```
soc = Society{
    instance = Agent{},
    quantity = 30
}

cs = CellularSpace{
    xdim = 10
}

env = Environment{soc, cs}
env:createPlacement{strategy = "void"}

agent = soc:sample()
agent:enter(cs:sample())
```

### See also

- [createPlacement (Environment)](./environment.md#createplacement)

---

## execute 

The entry point for executing a given Agent. When the Agent is not defined as a composition of [States](./state.md), it is an user-defined function to describe the behavior of an Agent.When the Agent is described as a State machine, execute is automatically defined by TerraME. It activates the [Jump](./jump.md) of the current State while it jumps from State to State. After that, it executes all the [Flows](./flow.md) of the current State. Usually, this function is called within an [Event](./event.md), thus the time of the Event can be got directly from the [Timer](./timer.md).  
  

### Arguments

- **#1**: An Event.

### Usage

```
agent = Agent{
    size = 5,
    execute = function(self)
        self.size = self.size + 1
    end
}

agent:execute()
```

---

## getCell 

Return the [Cell](./cell.md) where the Agent is located according to its placement. It assumes that each Agent belongs to at most one Cell.  
  

### Arguments

- **#1**: A string representing the name of the placement to be used. The default value is "placement".

### Usage

```
soc = Society{
    instance = Agent{},
    quantity = 30
}

cs = CellularSpace{
    xdim = 10
}

env = Environment{soc, cs}
env:createPlacement{}

agent = soc:sample()
cell = agent:getCell()
```

---

## getCells 

Return a vector with the [Cells](./cell.md) pointed by the Agent.  
  

### Arguments

- **#1**: A string representing the name of the placement to be used. The default value is "placement".

### Usage

```
soc = Society{
    instance = Agent{},
    quantity = 30
}

cs = CellularSpace{
    xdim = 10
}

env = Environment{soc, cs}
env:createPlacement{}

agent = soc:sample()

cell = agent:getCells()[1]
```

---


## getLatency 

Return the time when the [State](./state.md) machine executed the transition to the current state. Before executing for the first time, the latency is zero. This function is useful only when the Agent is described as a State machine.  
  

### Usage

```
-- latency = agent:getLatency()
```

---

## getSocialNetwork 

Return a [SocialNetwork](./socialNetwork.md) of the Agent given its name.  
  

### Arguments

- **#1**: Name of the SocialNetwork.

### Usage

```
agent = Agent{}

soc = Society{
    instance = agent,
    quantity = 100
}

soc:createSocialNetwork{probability = 0.5, name = "friends"}
ag = soc:sample()
ag:getSocialNetwork("friends")
```

### See also

- [createSocialNetwork (Society)](./society.md#createsocialnetwork)
- [forEachConnection (Utils)](../functions/utils.md#foreachconnection)


---

## getStateName 

Return a string with the current [State](./state.md) name. This function is useful only when the Agent is described as a state machine.  
  

### Usage

```
name = agent:getStateName()
```


---

## getTrajectoryStatus 

Return the status of the [Trajectories](./trajectory.md) of the Agent. This function is useful only when the Agent is described as a [State](./state.md) machine.  
  

### Usage

```
agent:getTrajectoryStatus()
```

### See also

- [setTrajectoryStatus](./agent.md#settrajectorystatus)


---

## init 

User-defined function that is used to initialize an Agent when it enters in a given [Society](./society.md) (e.g. when the Society is created, or when one calls [Society:add()](./society.md#add)).  
  

### Usage

```
agent = Agent{
    age = Random{min = 1, max  = 50, step = 1},
    init = function(self)
        if self.age > 40 then
            self.wealth = Random():integer(50, 100)
        else
            self.wealth = Random():integer(5, 10)
        end
    end
}

soc = Society{
    instance = agent,
    quantity = 10
}

print(soc:sample().age)
```

### See also

- [Random](./random.md)


---

## leave 

Remove the Agent from its current [Cell](./cell.md). If the Agent does not belong to any Cell then it will stop with an error. This function supposes that each Agent can be in one and only one Cell along the simulation. The Agent needs to have a placement to be able to use [Agent:enter()](./agent.md#enter), [Agent:leave()](./agent.md#leave), [Agent:move()](./agent.md#move), and [Agent:walk()](./agent.md#walk).  
  

### Arguments

- **#1**: A string representing the name of the placement to be used. The default value is "placement".

### Usage

```
ag1 = Agent{}
cs = CellularSpace{xdim = 3}
myEnv = Environment{cs, ag1}
myEnv:createPlacement()
ag1:leave()
```

### See also

- [createPlacement (Environment)](./environment.md#createplacement)


---

## message 

Send a message to another Agent. The receiver will get a message as a table through its [Agent:on_message()](./agent.md#on_message) (as default). Messages can arrive exactly after they are sent (synchronous) or have some delay (asynchronous). In the latter case, it is necessary to call function [Society:synchronize()](./society.md#synchronize) from the [Society](./society.md) they belong to deliver the messages.  
  

### Arguments

- delay: A number indicating temporal delay before activating this message. The efault value is zero (no delay, no synchronization required). Whenever a delayed message is received, it comes with an attribute delay equals to true.
- receiver: The Agent that will get the message.
- subject: A string describing the function that will be called in the receiver. Given a string x, the receiver will get the message in a function called on_x. The default value is "message". The function to receive the message must be implemented by the modeler. See [Agent:on_message()](./agent.md#on_message) for more details.
- ...: Other arguments are allowed to this function, as the message is a table. The receiver will get all the attributes sent plus an attribute called sender.

### Usage

```
agent1 = Agent{
    on_message = function(self, message)
        print("Got money:"..message.quantity)
    end
}

agent2 = Agent{}

agent2:message{
    receiver = agent1,
    content = "money",
    quantity = 20
}
```

---

## move 

Move the Agent to a new [Cell](./cell.md). This function supposes that each Agent can be in one and only one Cell along the simulation. The agent needs to have a placement to be able to use [Agent:enter()](./agent.md#enter), [Agent:leave()](./agent.md#leave), [Agent:move()](./agent.md#move), or [Agent:walk()](./agent.md#walk).  
  

### Arguments

- **#1**: The new Cell.
- **#2**: A string representing the placement to be used. The default value is "placement".

### Usage

```
ag1 = Agent{}
cs = CellularSpace{xdim = 3}
soc = Society{
    instance = ag1,
    quantity = 5
}

myEnv = Environment{cs, soc}
myEnv:createPlacement()

ag = soc:sample()
cell = cs:sample()
ag:move(cell)
```

### See also

- [createPlacement (Environment)](./environment.md#createplacement)


---

## notify 

Notify the Observers of the Agent.  
  

### Arguments

- **#1**: A number representing the notification time. The default value is zero. It is also possible to use an [Event](./event.md) as argument. In this case, it will use the result of [Event:getTime()](./event.md#gettime).

### Usage

```
agent = Agent{
    value = 1
}

Chart{target = agent}
agent:notify(1)
agent:notify(2)
```

---

## on_message 

User-defined function that can be implemented to allow Agents to exchange messages. It is executed every time a receiver gets a message. The received message has the same content of the sent message, plus an attribute called sender with the Agent that sent the message. In the case of non-delayed messages, the returning value of this function (executed by the receiver) is also returned as the result of message (executed by the sender). Note that, although in the description below on_message has only one argument, the signature has two arguments, the first one being the agent itself. This function is usually called internally by TerraME, as result of calls of [Agent:message()](./agent.md#message) by the modeler. Other functions on_ can be defined by the modeler, and will be called by TerraME according to the subject of the message.  
  

### Arguments

- **#1**: A table with the received message. It has an attribute called sender with the Agent that sent the message.

### Usage

```
agent = Agent{
    money = 0,
    on_message = function(self, message)
        self.money = self.money + message.quantity
        self:message{receiver = message.sender, subject = "thanks"}
    end,
    on_thanks = function(self, message)
        print("thanks")
        self:message{receiver = message.sender, subject = "yourewelcome"}
    end,
    on_yourewelcome = function()
        print("yourewelcome")
    end
}

soc = Society{
    instance = agent,
    quantity = 10
}

soc:sample():message{
    receiver = soc:sample(),
    quantity = 20
}
```

### See also

- [message](./agent.md#message)
- [synchronize (Society)](./society.md#synchronize)


---

## reproduce 

Create an Agent with the same behavior in the same [Cell](./cell.md) where the original Agent is (according to its placement). The new Agent is pushed into the same [Society](./society.md) the original Agent belongs and placements created using the Society are instantiated with size zero if the only argument of reproduce does not contain such placements. This function returns the new Agent.  
  

### Arguments

- **#1**: An optional table with attributes of the new Agent. If this table do not contay some of the placements registered in its Society, then they are instantiated and the newborn will be placed in the same Cell of its parent. This functionality supposes that an Agent can be in one and only one Cell for each placement along the simulation.

### Usage

```
agent = Agent{}

soc = Society{
    instance = agent,
    quantity = 100
}

soc.agents[1]:reproduce()
print(#soc)
```

---

## sample 

Return a random Agent from a [SocialNetwork](./socialNetwork.md) of the Agent.  
  

### Arguments

- **#1**: A string with the name of the SocialNetwork. The default value is "1".

### Usage

```
ag = Agent{}
soc = Society{instance = ag, quantity = 5}

sn = SocialNetwork()
forEachAgent(soc, function(agent)
    sn:add(agent)
end)

ag:addSocialNetwork(sn)
friend = ag:sample()
```

### See also

- [getSocialNetwork](./agent.md#getSocialNetwork)


---

## setTrajectoryStatus 

Activate or not the [Trajectories](./trajectory.md) defined for a given Agent.  
  

### Arguments

- **#1**: Use or not the Trajectories. As default, Trajectories are turned off. If status is true, when executed, the Agent that contains [States](./state.md) will automatically traverse all trajectories defined within it, which means that [Agent:execute()](./agent.md#execute) will be executed once for each of its [Cells](./cell.md). This function is useful only when the Agent is described as a State machine.

### Usage

```
-- agent:setTrajectoryStatus(true)
```

---

## walk 

Execute a random walk to a neighbor [Cell](./cell.md). This function supposes that each Agent can be in one and only one Cell along the simulation. The Agent needs to have a placement to be able to use [Agent:enter()](./agent.md#enter), [Agent:leave()](./agent.md#leave), [Agent:move()](./agent.md#move), and [Agent:walk()](./agent.md#walk).  
  

### Arguments

- **#1**: A string representing the placement to be used. The default value is "placement".
- **#2**: A string representing the [Neighborhood](./neighborhood.md) to be used. The default value is "1.

### Usage

```
singleFooAgent = Agent{}

cs = CellularSpace{xdim = 10}
cs:createNeighborhood()

e = Environment{cs, singleFooAgent}
e:createPlacement()

singleFooAgent:walk()
singleFooAgent:walk()
```

### See also

- [createPlacement (Environment)](./environment.md#createplacement)


---

## walkIfEmpty 

Choose a random Neighbor [Cell](./cell.md) and move if it is empty. Note that if it selects a non-empty Cell the Agent will not move, even if there are empty Cells in the [Neighborhood](./neighborhood.md). The Agent needs to have a placement to be able to use this function, and the [CellularSpace](./cellularSpace.md) must have a Neighborhood. This function is recommended to be used only when it is possible to have only one Agent per Cell.  
  

### Arguments

- **#1**: A string representing the placement to be used. The default value is "placement".
- **#2**: A string representing the Neighborhood to be used. The default value is "1.

### Usage

```
singleFooAgent = Agent{}

cs = CellularSpace{xdim = 10}
cs:createNeighborhood()

e = Environment{cs, singleFooAgent}
e:createPlacement()

singleFooAgent:walkIfEmpty()
```

### See also

- [createPlacement (Environment)](./environment.md#createplacement)


---

## walkToEmpty 

Walk to one of the available empty [Cells](./cell.md) in the [Neighborhood](./neighborhood.md). If there is no empty neighbor, the Agent will not move. The Agent needs to have a placement to be able to use this function, and the [CellularSpace](./cellularSpace.md) must have a Neighborhood. This function is recommended to be used only when it is possible to have only one Agent per Cell.  
  

### Arguments

- **#1**: A string representing the placement to be used. The default value is "placement".
- **#2**: A string representing the Neighborhood to be used. The default value is "1.

### Usage

```
singleFooAgent = Agent{}

cs = CellularSpace{xdim = 10}
cs:createNeighborhood()

e = Environment{cs, singleFooAgent}
e:createPlacement()

singleFooAgent:walkToEmpty()
```

### See also

- [createPlacement (Environment)](./environment.md#createplacement)