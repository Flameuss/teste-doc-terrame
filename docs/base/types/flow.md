# Flow

A Flow describes the behavior of an automaton or [Agent](./agent.md) in a given [State](./state.md).  
  

### Arguments

- **1st**: A function(ev, agent, cell), where the arguments are: an [Event](./event.md) that activated the Flow, the [Automaton](./automaton.md) or Agent that owns the Flow, and the [Cell](./cell.md) over which the Flow will be evaluated.

### Usage

```
Flow{function(ev, agent, cell)
    agent.value = agent.value + 2
end}
```