# Jump

Control a discrete transition between [States](./state.md). If the method in the first argument returns true, the target becomes the new active State.  
  

### Arguments

- **1st**: a function that returns a boolean value and takes as arguments an [Event](./event.md), an [Agent](./agent.md) or [Automaton](./automaton.md), and a [Cell](./cell.md), respectively.
- **target**: a string with another State id.

### Usage

```
Jump{
    function(ev, agent, c)
        return c.water > c.capInf
    end,
    target = "wet"
}
```