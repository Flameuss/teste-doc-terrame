# InternetSender

An Internet connection to send attribute values of an object through a TCP or UDP protocol. Every call to notify (for example, [Agent:notify()](./agent.md#notify)) in the target activates the InternetSender.  
  

### Arguments

- **compress**: Compress the data to be transfered? It might be interesting not to compress when the connection is on the localhost, or when there is a very fast connection, to make the simulation faster. The default value is true.
- **host**: A string with the host name to transfer the data. The default value is "localhost".
- **port**: A number greater or equal to 50000 indicating the port of the host to transfer the data. The default value is 456456.
- **protocol**: A string with the protocol to be used. It can be "tcp" (default) or "udp".
- **select**: A vector of strings with the name of the attributes to be observed. If it is a single value then it can also be described as a string. As default, it selects all the user-defined attributes of an object. When using a [CellularSpace](./cellularSpace.md) as subject, the values in select are related to its [Cells](./cell.md) and this argument is mandatory. In the case of [Society](./society.md), if it does not have any numeric attributes then it will use the number of agents in the Society as attribute.
- **target**: An [Agent](./agent.md), Cell, CellularSpace, or Society.
- **visible**: A boolean value indicating whether InternetSender will create a window to display the transferred data. The default value is true.

### Usage

```
cell = Cell{
    value = 5
}

InternetSender{
    target = cell,
    select = "value",
    protocol = "tcp",
    compress = false
}
```