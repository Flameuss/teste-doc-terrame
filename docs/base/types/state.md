# State

A container of [Jumps](./jump.md) and [Flows](./flow.md). Every State also has an id to identify itself in the Jumps of other States within the same [Agent](./agent.md) or [Automaton](./automaton.md).  
  

### Arguments

- **id**: A string with the unique identifier of the State.

### Usage

```
State{
    id = "working"
}
```