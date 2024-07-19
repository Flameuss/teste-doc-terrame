# Choice

Type to define options to be used by the modeler. It can get a vector a argument or named arguments as follows. This type is useful to define parameters of a [Model](./model.md).  
  

### Arguments

- **default**: The default value for the choice. The default value for this argument depends on the other arguments used. If using min then it is the default value. Otherwise, if using max then it is the default value. If using a vector as argument, the default value is the first element of the table.
- **max**: The maximum value (optional).
- **min**: The minimum value (optional).
- **slices**: An optional argument with the number of values between minimum and maximum. It must be an integer number greater than two. When using this argument, min and max become mandatory.
- **step**: An optional argument with the step from minimum to maximum. Note that max should be equals to min plus k times step, where k is an integer number. When using this argument, min and max become mandatory.

### Attributes

Some attributes of Choice have internal semantics. They can be used as **read-only** by the modeler.

- **values**: A vector with the possible values for the Choice.

### Usage

```
c1 = Choice{1, 2, 3}
c2 = Choice{"low", "medium", "high"}
c3 = Choice{min = 2, max = 5, step = 0.1}
c4 = Choice{min = 2, max = 20, slices = 4}
```

---

## Functions

|                                                              |                                                     |
| ------------------------------------------------------------ | --------------------------------------------------- |
| [sample](./choice.md#sample) | Return a random element from the available options. |


---
## **sample** 

Return a random element from the available options. If the Choice was built from a vector or it has a step, it returns a random value following a discrete uniform distribution. If it has maximum and minimum then it returns a random value using a continuous uniform distribution. When sampling from Choices that have maximum but not minimum, or minimum but not maximum, it uses 2^52 as maximum or -2^52 as minimum.  
  

### Usage

```
c = Choice{1, 2, 5, 6}
c:sample()
```