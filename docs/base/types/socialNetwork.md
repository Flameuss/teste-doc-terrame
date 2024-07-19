# SocialNetwork

SocialNetwork represents relations between A gents. It is a set of pairs (connection, weight), where connection is an A gent and weight is a number storing the relation's strength.  
  
This type is used to create relations from scratch to be used by [Agent:addSocialNetwork()](./agent.md#addsocialnetwork). To create well-established SocialNetworks see [Society:createSocialNetwork()](./society.md#createsocialnetwork). It is recommended that a SocialNetwork should contain only [Agents](./agent.md) that belong to the same [Society](./society.md), as it guarantees that all its Agents have unique identifiers. Calling [forEachConnection()](../functions/utils.md#foreachconnection) from an Agent traverses one of its SocialNetworks.  
  

### Attributes

Some attributes of SocialNetwork have internal semantics. They can be used as **read-only** by the modeler.

- **connections**: The connections with the Agents of the SocialNetWork.
- **count**: The number of Agents in the SocialNetwork.
- **weights**: The weights of the Agents in the SocialNetwork.

### Usage

```
sn = SocialNetwork()
sn = SocialNetwork{}
```

### See also

- [createSocialNetwork (Society)](./society.md#createsocialnetwork)

---

## Functions

|                                                                                 |                                                                                                            |
| ------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------- |
| [add](./socialNetwork.md#add)                   | Add a new connection to the SocialNetwork.                                                                 |
| [clear](./socialNetwork.md#clear)               | Remove all [Agents](./agent.md) from the SocialNetwork.                    |
| [getWeight](./socialNetwork.md#getweight)       | Return a number with the weight of a given connection.                                                     |
| [isConnection](./socialNetwork.md#isconnection) | Return whether a given [Agent](./agent.md) belongs to the SocialNetwork.   |
| [isEmpty](./socialNetwork.md#isempty)           | Return whether the SocialNetwork does not contain any [Agent](./agent.md). |
| [remove](./socialNetwork.md#remove)             | Remove an [Agent](./agent.md) from the SocialNetwork.                      |
| [sample](./socialNetwork.md#sample)             | Return a random [Agent](./agent.md) from the SocialNetwork.                |
| [setWeight](./socialNetwork.md#setweight)       | Update the weight of a connection.                                                                         |
| [#](./socialNetwork.md##)                       | Retrieve the number of connections in the SocialNetwork.                                                   |

---

## **add** 

Add a new connection to the SocialNetwork.  
  

### Arguments

- **#1**: An [Agent](./agent.md).
- **#2**: A number representing the weight of the connection). The default value is 1.

### Usage

```
sn = SocialNetwork()
agent1 = Agent{id = "1"}
agent2 = Agent{id = "2"}

sn:add(agent1)
sn:add(agent2, 0.5)
print(#sn)
```

---

## **clear** 

Remove all [Agents](./agent.md) from the SocialNetwork. In practice, it has the same behavior of calling SocialNetwork() again if the SocialNetwork was not added to any Agent.  
  

### Usage

```
sn = SocialNetwork()
agent1 = Agent{id = "1"}
agent2 = Agent{id = "2"}

sn:add(agent1)
sn:add(agent2)

sn:clear()
print(#sn)
```

---

## **getWeight** 

Return a number with the weight of a given connection.  
  

### Arguments

- **#1**: An [Agent](./agent.md).

### Usage

```
sn = SocialNetwork()
agent1 = Agent{id = "1"}
agent2 = Agent{id = "2"}

sn:add(agent1)
sn:add(agent2, 0.5)

print(sn:getWeight(agent1))
print(sn:getWeight(agent2))
```

---

## **isConnection** 

Return whether a given [Agent](./agent.md) belongs to the SocialNetwork.  
  

### Arguments

- **#1**: An Agent.

### Usage

```
sn = SocialNetwork()
agent = Agent{id = "1"}

sn:add(agent)

if sn:isConnection(agent) then
    print("connected")
end
```

---

## **isEmpty** 

Return whether the SocialNetwork does not contain any [Agent](./agent.md).  
  

### Usage

```
sn = SocialNetwork()

if sn:isEmpty() then
    print("empty")
end
```

---

## **remove** 

Remove an [Agent](./agent.md) from the SocialNetwork.  
  

### Arguments

- **#1**: An Agent.

### Usage

```
sn = SocialNetwork()
agent1 = Agent{id = "1"}
agent2 = Agent{id = "2"}

sn:add(agent1)
sn:add(agent2)

sn:remove(agent1)
print(#sn)
```

---

## **sample** 

Return a random [Agent](./agent.md) from the SocialNetwork.  
  

### Usage

```
sn = SocialNetwork()
agent1 = Agent{id = "1"}
agent2 = Agent{id = "2"}

sn:add(agent1)
sn:add(agent2)

agent = sn:sample()
```

---

## **setWeight** 

Update the weight of a connection.  
  

### Arguments

- **#1**: An [Agent](./agent.md).
- **#2**: A number with the new weight.

### Usage

```
sn = SocialNetwork()
agent1 = Agent{id = "1"}
agent2 = Agent{id = "2"}

sn:add(agent1)
sn:add(agent2, 0.5)
sn:setWeight(agent1, 0.001)

print(sn:getWeight(agent1))
```

---

## **#** 

Retrieve the number of connections in the SocialNetwork.  
  

### Usage

```
sn = SocialNetwork()
print(#sn)
```