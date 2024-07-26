# Group (inherits [Society](./society.md))

Type that defines an ordered selection over a [Society](./society.md). It inherits Society; therefore it is possible to apply all functions of such type to a Group. For instance, calling [forEachAgent()](../functions/utils.md#foreachagent) also traverses Groups.  
  

### Arguments

- **build**: A boolean value indicating whether the Group should be computed when created. The default value is true.
- **greater**: A function ([Agent](./agent.md), Agent)->boolean to sort the Group. Such function must return true if the first Agent has priority over the second one. When using this argument, Group compares each pair of Agents to establish an execution order to be used by [forEachAgent()](../functions/utils.md#foreachagent). As default, the Group will not be ordered and so [forEachCell()](../functions/utils.md#foreachcell) will run in the order the Agents were pushed into the Society. See [greaterByAttribute()](../functions/utils.md#greaterbyattribute) for predefined options for this argument.
- **random**: A boolean value indicating that the Group must be shuffled. The Group will be shuffled every time one calls [rebuild()](./group.md#rebuild) or when the Group is an action of an [Event](./event.md). This argument cannot be combined with argument greater.
- **select**: A function (Agent)->boolean indicating whether an Agent of the Society should belong to the Group. If this function returns anything but false or nil for a given Agent, it will be added to the Group. If this argument is missing, all Agents will be included in the Group.
- **target**: The Society over which the Group will take place.

### Attributes

Some attributes of Group have internal semantics. They can be used as **read-only** by the modeler.

- **agents**: A vector with Agents of the Group.
- **greater**: The last function used to sort the Group.
- **parent**: The Society used by the Group (its target).
- **select**: The last function used to filter the Group.

### Usage

```
agent = Agent{
    age = Random{min = 10, max = 50, step = 1}
}

soc = Society{
    instance = agent,
    quantity = 20
}

group = Group{
    target = society,
    select = function(agent)
        return agent.age > 20
    end
}

groupBySize = Group{
    target = society,
    greater = function(a1, a2)
        return a1.age > a2.age
    end
}
```

---

## Functions

|                                                                   |                                                                                                                       |
| ----------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------- |
| [add](./group.md#add)             | Add a new [Agent](./agent.md) to the Group.                                           |
| [clone](./group.md#clone)         | Return a copy of the Group.                                                                                           |
| [filter](./group.md#filter)       | Apply the filter again over the [Society](./society.md) used as target for the Group. |
| [randomize](./group.md#randomize) | Randomize the [Agents](./agent.md) of the Group.                                      |
| [rebuild](./group.md#rebuild)     | Rebuild the Group.                                                                                                    |
| [sort](./group.md#sort)           | Sort the current [Society](./society.md) subset.                                      |
| [#](./group.md##)                 | Return the number of [Agents](./agent.md) in the Group.                               |

---

## **add** 

Add a new [Agent](./agent.md) to the Group. It will be added to the end of the list of Agents.  
  

### Arguments

- **#1**: An Agent.

### Usage

```
agent = Agent{}
group = Group{}

group:add(agent)
```

---

## **clone** 

Return a copy of the Group. It has the same parent, select, greater and [Agents](./agent.md). Any change in the cloned Group will not affect the original one.  
  

### Usage

```
agent = Agent{
    age = Random{min = 0, max = 50, step = 1}
}

soc = Society{
    instance = agent,
    quantity = 20
}

group = Group{
    target = soc,
    select = function(agent) return agent.age < 10 end
}

group2 = group:clone()
print(#group)
print(#group2)
```


---

## **filter** 

Apply the filter again over the [Society](./society.md) used as target for the Group. [Agents](./agent.md) that belong to the Society but do not belong to the Group are ignored. This way, this function creates a subset over the subset of the Society.  
  

### Usage

```
agent = Agent{
    age = Random{min = 0, max = 50, step = 1},
    execute = function(self)
        self.age = self.age + 1
    end
}

soc = Society{
    instance = agent,
    quantity = 20
}

group = Group{target = soc, select = function(agent)
    return agent.age >= 18
end}

group:execute()
group:filter()
```

---

## **randomize** 

Randomize the [Agents](./agent.md) of the Group. It will change the traversing order used by [forEachAgent()](../functions/utils.md#foreachagent).  
  

### Usage

```
agent = Agent{
    age = Random{min = 0, max = 50, step = 1}
}

soc = Society{
    instance = agent,
    quantity = 20
}

group = Group{
    target = soc
}

group:randomize()
```

---

## **rebuild** 

Rebuild the Group. It works as if the Group was declared again with the same arguments.  
  

### Usage

```
agent = Agent{
    age = Random{min = 0, max = 50, step = 1}
}

soc = Society{
    instance = agent,
    quantity = 20
}

group = Group{
    target = soc,
    select = function(agent) return agent.age < 10 end,
    greater = function(a1, a2) return a1.age > a2.age end
}

forEachAgent(group, function(agent)
    agent.age = agent.age + 5
end)

group:rebuild()
```


---

## **sort** 

Sort the current [Society](./society.md) subset. It updates the traversing order of the Group.  
  

### Usage

```
agent = Agent{
    age = Random{min = 0, max = 50, step = 1},
    execute = function(self)
        self.age = self.age + Random{min = 0, max = 2}:sample()
    end
}

soc = Society{
    instance = agent,
    quantity = 20
}

group = Group{target = soc, greater = function(ag1, ag2)
    return ag1.age > ag2.age
end}

group:execute()
group:sort()
```


---

## **#** 

Return the number of [Agents](./agent.md) in the Group.  
  

### Usage

```
agent = Agent{
    age = Random{min = 0, max = 50, step = 1}
}

soc = Society{
    instance = agent,
    quantity = 20
}

group = Group{
    target = soc,
    select = function(agent) return agent.age < 10 end
}

print(#group)
```