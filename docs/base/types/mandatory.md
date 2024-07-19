# Mandatory

Type to define a mandatory argument for a given [Model](./model.md).  
  

### Arguments

- **#1**: A string with the type of the argument. It cannot be boolean, string, nor userdata. Note that Mandatory does not get named arguments as the other TerraME types.

### Attributes

Some attributes of Mandatory have internal semantics. They can be used as **read-only** by the modeler.

- **value**: The required type.

### Usage

```
Mandatory("number")
```