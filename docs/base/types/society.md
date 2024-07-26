# Society

Type to create and manipulate a set of [Agents](./agent.md). Each Agent within a Society has a unique id, which is initialized while creating the Society. There are different ways to create a Society. See the argument source for the options. Calling [forEachAgent()](../functions/utils.md#foreachagent) traverses Societies.  
  

### Arguments

- **file**: A [File](./file.md) or a string with the name of the file where data related to the Agents is stored.
- **id**: The unique identifier attribute used when reading the Society from a file.
- **instance**: An Agent with the description of attributes and functions. When using this argument, each Agent of the Society will have attributes and functions according to the instance. The attributes of the instance will be copyed to the Agent and Society calls [Agent:init()](./agent.md#init) for each of its Agents. Every attribute from the Agent that is a [Random](./random.md) will be converted into a [Random:sample()](./random.md#sample). When using this argument, additional functions are also created to the Society. For each attribute of the its Agents (after calling [Agent:init()](./agent.md#init)), one function is created in the Society with the same name. The table below describes how each attribute is mapped from the Agent to the Society:

| Type of attribute | Function within the Society                                                                                                    |
| ----------------- | ------------------------------------------------------------------------------------------------------------------------------ |
| function          | Call the function of each of its Agents.                                                                                       |
| number            | Return the sum of the number in each of its Agents.                                                                            |
| boolean           | Return the quantity of true values in its Agents.                                                                              |
| string            | Return a table with positions equal to the unique strings and values equal to the number of occurrences in each of its Agents. |

- **quantity**: Number of Agents to be created. It is used when the Society will not be loaded from a file or database.
- **sep**: A string with the file separator for reading a CSV (default is ",").
- **source**: A string with the name of the source the Society will be read from. TerraME always converts this string to lower case. See the table below:

| source     | Description                                                                                              | Compulsory arguments | Optional arguments |
| ---------- | -------------------------------------------------------------------------------------------------------- | -------------------- | ------------------ |
| "volatile" | Create agents from scratch. This is the default value when using the argument quantity.                  | instance, quantity   | ...                |
| "shp"      | Load agents from a shapefile.                                                                            | file, instance       | ...                |
| "csv"      | Load agents from a csv file. This is the default value when value of argument database ends with ".csv". | file, id, instance   | sep, ...           |

- **...**: Any other attribute or function for the Society.

### Attributes

Some attributes of Society have internal semantics. They can be used as **read-only** by the modeler.

- **agents**: A vector of Agents pointed by the Society.
- **autoincrement**: unique identifier used to represent the last Agent added to the Society. The next Agent will have 'autoincrement + 1' as id.
- **cObj_**: A pointer to a C++ representation of the Society. Never use this object.
- **instance**: The Agent that describes attributes and functions of each Agent belonging to the Society. This Agent must not be executed.
- **messages**: A vector that contains the delayed messages.
- **parent**: The [Environment](./environment.md) it belongs.
- **placements**: A vector with the names of the placements created using this object (see [Environment:createPlacement()](./environment.md#createplacement)).


### Usage

```
instance = Agent{
    execute = function() end,
    run = function() end,
    age = Random{min = 1, max = 50, step = 1}
}

s = Society{
    instance = instance,
    quantity = 20
}

s:execute() -- call execute for each agent
s:run() -- call run for each agent
print(s:age()) -- sum of the ages of each agent
print(#s)

instance = Agent{
    execute = function() end
}

s = Society{
    instance = instance,
    file = filePath("agents.csv", "base")
}

print(#s)
```
--- 

## Functions

|                                                                                         |                                                                                                                                                                    |
| --------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| [add](./society.md#add)                                 | Add a new [Agent](./agent.md) to the Society.                                                                                      |
| [clear](./society.md#clear)                             | Remove all the [Agents](./agent.md) from the Society.                                                                              |
| [createSocialNetwork](./society.md#createsocialnetwork) | Create a directed [SocialNetwork](./socialNetwork.md) for each [Agent](./agent.md) of the Society. |
| [get](./society.md#get)                                 | Return a given [Agent](./agent.md) based on its position.                                                                          |
| [notify](./society.md#notify)                           | Notify all the [Agents](./agent.md) of the Society.                                                                                |
| [remove](./society.md#remove)                           | Remove a given [Agent](./agent.md) from the Society.                                                                               |
| [sample](./society.md#sample)                           | Return a random [Agent](./agent.md) from the Society.                                                                              |
| [split](./society.md#split)                             | Split the Society into a set of [Groups](./group.md) according to a classification strategy.                                       |
| [synchronize](./society.md#synchronize)                 | Deliver asynchronous messages sent by [Agents](./agent.md) belonging to the Society.                                               |
| [#](./society.md##)                                     | Return the number of [Agents](./agent.md) in the Society.                                                                          |

---

## **add** 

Add a new [Agent](./agent.md) to the Society. It will be the last Agent of the Society when one uses [forEachAgent()](../functions/utils.md#foreachagent).  
  

### Arguments

- **#1**: The new Agent that will be added to the Society. If nil, the Society will add a copy of its instance. In this case, the Society converts [Random](./random.md) values into samples and executes [Agent:init()](./agent.md#init).

### Usage

```
ag = Agent{
    age = Random{min = 1, max = 50, step = 1}
}

soc = Society{
    instance = ag,
    quantity = 2
}

soc:add()
print(#soc)
agent = soc:add()
print(agent.age)
```

### See also

- [init (Agent)](./agent.md#init)

---

## **clear** 

Remove all the [Agents](./agent.md) from the Society.  
  

### Usage

```
ag = Agent{}

soc = Society{
    instance = ag,
    quantity = 2
}

print(#soc)
soc:clear()
print(#soc)
```

---

## **createSocialNetwork** 

Create a directed [SocialNetwork](./socialNetwork.md) for each [Agent](./agent.md) of the Society.  
  

### Arguments

- **filter**: A function (Agent, Agent)->boolean that returns true if the first Agent will have the second Agent in its SocialNetwork. When using this argument, the default value of strategy becomes "function".
- **inmemory**: If true (default), a SocialNetwork will be built and stored for each Agent of the Society. The SocialNetworks will change only if the modeler add or remove connections explicitly. If false, a SocialNetwork will be computed every time the simulation calls [Agent:getSocialNetwork()](./agent.md#getsocialnetwork), for example when using [forEachConnection()](../functions/utils.md#foreachconnection). In this case, if any of the attributes the SocialNetwork is based on changes then the resulting SocialNetwork might be different. For instance, if the SocialNetwork of an Agent is based on its [Neighborhood](./neighborhood.md) and the Agent walks to another [Cell](./cell.md), a SocialNetwork not inmemory will also be updated. SocialNetworks not inmemory also help the simulation to run with larger datasets, as they are not explicitly represented, but they consume more time as they need to be built again and again along the simulation. Note that not inmemory relations cannot be changed manually (for example by using [SocialNetwork:add()](./socialNetwork.md#add)), because the relation is recomputed every time it is needed.
- **name**: Name of the relation.
- **neighborhood**: A string with the name of the Neighborhood that will be used to create the SocialNetwork. The default value is "1".
- **placement**: A string with the name of the placement that will be used to create the SocialNetwork. The default value is "placement".
- **probability**: A number between 0 and 1 indicating a probability. The semantics associated to the probability depends on the argument strategy. When using this argument, the default value of strategy becomes "probability".
- **quantity**: A number indicating a quantity of connections. The semantics associated to this value depends on the argument strategy. When using this argument, the default value of strategy becomes "quantity".
- **self**: A boolean value indicating whether the Agent can be connected to itself. The default value is false.
- **start**: The number of agents without any connection in the initial group. New agents are connected to agents in this group and then added to the group. This argument is useful only for "barabasi" strategy.
- **strategy**: A string with the strategy to be used for creating the SocialNetwork. See the table below.

| Strategy      | Description                                                                                                                                                                                             | Compulsory arguments            | Optional arguments                      |
| ------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------- | --------------------------------------- |
| "barabasi"    | Create a SocialNetwork according to the strategy proposed by Barabasi and Albert "Emergence of scaling in random networks" Science 286 509-512 (1999).                                                  | quantity, start, strategy       | name                                    |
| "cell"        | Create a dynamic SocialNetwork for each Agent of the Society with every Agent within the same Cell the Agent belongs.                                                                                   |                                 | inmemory, name, placement, self         |
| "erdos"       | Create a SocialNetwork with a given number of random connections. This strategy implements the algorithm proposed by Erdos and Renyi (1959) "On random graphs I". Publicationes Mathematicae 6: 290-297 | quantity, strategy              | name                                    |
| "function"    | Create a SocialNetwork according to a filter function applied to each Agent of the Society.                                                                                                             | filter                          | inmemory, name                          |
| "neighbor"    | Create a dynamic SocialNetwork for each Agent of the Society with every Agent within the neighbor Cells of the one the Agent belongs.                                                                   |                                 | inmemory, name, neighborhood, placement |
| "probability" | Applies a probability for each pair of Agents to be connected (excluding the Agent itself).                                                                                                             | probability                     | inmemory, name, symmetric               |
| "quantity"    | Each Agent will be connected to a given number of other Agents randomly taken from the Society (excluding the Agent itself).                                                                            | quantity                        | inmemory, name, symmetric               |
| "void"        | Create an empty SocialNetwork for each Agent of the Society.                                                                                                                                            |                                 | name                                    |
| "watts"       | Create a SocialNetwork according to the strategy proposed by Watts and Strogarz (1998) Collective dynamics of 'small-world' networks. Nature 393, 440-442.                                              | probability, quantity, strategy | name                                    |

- **symmetric**: A boolean value indicating that, if Agent a is connected to Agent b, then Agent b will be connected to Agent a. In practice, if this option is used, the number of connections double. For example, if one use this with 20% of probability, on average, Agents will be connected with 40% of probability. The default value is false.

### Usage

```
ag = Agent{}

soc = Society{
    instance = ag,
    quantity = 20
}

soc:createSocialNetwork{
    quantity = 2
}

soc:createSocialNetwork{
    probability = 0.15,
    name = "random"
}

cs = CellularSpace{xdim = 10}
cs:createNeighborhood()
env = Environment{soc, cs}
env:createPlacement()

soc:createSocialNetwork{
   strategy = "neighbor",
   name = "byneighbor"
}
```

---

## **get** 

Return a given [Agent](./agent.md) based on its position.  
  

### Arguments

- **#1**: The position of the Agent that will be returned. It can be a number (with the position of the Agent in the vector of Agents) or a string (with the id of the Agent).

### Usage

```
ag = Agent{}

soc = Society{
    instance = ag,
    quantity = 2
}

agent = soc:get("1")
print(agent.id)
```

---

## **notify** 

Notify all the [Agents](./agent.md) of the Society.  
  

### Arguments

- **#1**: A positive number representing the notification time. The default value is 0. It is also possible to use an [Event](./event.md) as argument. In this case, it will use the result of [Event:getTime()](./event.md#gettime).

### Usage

```
ag = Agent{}

soc = Society{
    instance = ag,
    quantity = 2
}

soc:notify()
soc:add()
soc:add()
soc:notify()
```

---

## **remove** 

Remove a given [Agent](./agent.md) from the Society.  
  

### Arguments

- **#1**: The Agent that will be removed, or a function that takes an Agent as argument and returns true if the Agent must be removed.

### Usage

```
ag = Agent{}

soc = Society{
    instance = ag,
    quantity = 2
}

print(#soc)
soc:remove(soc:sample())
print(#soc)
```

---

## **sample** 

Return a random [Agent](./agent.md) from the Society.  
  

### Usage

```
agent = Agent{}
soc = Society{
    instance = agent,
    quantity = 10
}

sample = soc:sample()
```

---

## **split** 

Split the Society into a set of [Groups](./group.md) according to a classification strategy. The Groups will have empty intersection and union equal to the whole Society (unless function below returns nil for some [Agent](./agent.md)). It works according to the type of its only and compulsory argument.  
  

### Arguments

- **#1**: A string or a function, working as follows:

| Type of argument | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| ---------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| string           | The argument must represent the name of one attribute of the Agents of the Society. Split then creates one Group for each possible value of the attribute using the value as name and fills them with the Agents that have the respective attribute value. If the Society has an instance and the respective attribute in the instance is a [Random](./random.md) value with discrete or categorical strategy, it will use the possible values to create Groups, which means that the returning Groups can have size zero in this case. |
| function         | The argument is a function that gets an Agent as argument and returns a name for the Agent, which can be a number, string, or boolean value. Groups are then named according to the returning value.                                                                                                                                                                                                                                                                                                                                                                    |

### Usage

```
ag = Agent{
    gender = Random{"male", "female"},
    age = Random{min = 1, max = 80, step = 1}
}

soc = Society{
    instance = ag,
    quantity = 50
}

groups = soc:split("gender")
print(#groups.male) -- can be zero because it comes from an instance
print(#groups.female) -- also

groups2 = soc:split(function(ag)
    if ag.age > 60 then
        return "old"
    else
        return "notold"
    end
end)

if groups2.old then -- might not exist as it does not come from an instance
    print(#groups2.old)
end
```

---

## **synchronize** 

Deliver asynchronous messages sent by [Agents](./agent.md) belonging to the Society.  
  

### Arguments

- **#1**: A number indicating the current delay to be delivered. Messages with delay less or equal this value are sent, while the others have their delays reduced by this value. The default value is one.

### Usage

```
nonFooAgent = Agent{
    received = 0,
    on_message = function(self)
        self.received = self.received + 1
    end
}

soc = Society{
    instance = nonFooAgent,
    quantity = 15
}

soc:createSocialNetwork{quantity = 5}

forEachAgent(soc, function(agent)
    forEachConnection(agent, function(friend)
        agent:message{receiver = friend, delay = 5}
    end)
end)

otheragent = soc:sample()
print(otheragent.received)
soc:synchronize(4)
print(otheragent.received)
soc:synchronize(2)
print(otheragent.received)
```

---

## **#** 

Return the number of [Agents](./agent.md) in the Society.  
  

### Usage

```
ag = Agent{}

soc = Society{
    instance = ag,
    quantity = 2
}

print(#soc)
```