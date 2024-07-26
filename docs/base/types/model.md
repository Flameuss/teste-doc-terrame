# Model

Type that defines a model. The user can use Model to describe the arguments of a model and how it can be built. The returning value of a Model is an object that can be used directly to simulate (as long as it does not have any [Mandatory](./mandatory.md) parameter) or used to create as many instances as needed to simulate the Model with different parameters. A tutorial about Models in TerraME is available at [http://github.com/pedro-andrade-inpe/terrame/wiki/Models.](http://github.com/pedro-andrade-inpe/terrame/wiki/Models.)  
  

### Arguments

- **execute**: An optional function to define the changes of the Model in each time step. it the Model does not have a [Timer](./timer.md) after [init()](./model.md#init) but it has this function, a Timer will be automatically created and will add an [Event](./event.md) with the Model as its action.
- **finalTime**: A number with the final time of the simulation. If the Model does not have this as argument, it must be defined within function [init()](./model.md#init).
- **init**: A mandatory function to describe how an instance of Model is created.
- **interface.**: An optional function to describe how the graphical interface is displayed. See [interface()](./model.md#interface). See [init()](./model.md#init). If the Model does not have argument finalTime, this function should create the attribute finalTime to allow the Model instance to be run.
- **random**: An optional boolean value indicating that the model uses random numbers. The default value is false.
- **...**: Arguments of the Model. The values of each argument have an associated semantic. See the table below:

| Attribute type                                        | Description                                                                                                                                                                                                                                            | Default value                                                                                                        |
| ----------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | -------------------------------------------------------------------------------------------------------------------- |
| number or bool                                        | The instance has to belong to such type.                                                                                                                                                                                                               | The value itself.                                                                                                    |
| string                                                | The instance has to be a string. If it is in the format "*.a;*.b;...", it describes a file extension. The modeler then has to use a filename as argument with one of the extensions defined by this string.                                            | The value itself.                                                                                                    |
| [Choice](./choice.md) | The instance must have a value that belongs to the Choice.                                                                                                                                                                                             | The default value of the Choice.                                                                                     |
| Mandatory                                             | A mandatory argument, which means that the use must use a value witht the type defined in the Mandatory to build the model instance correctly. If Mandatory is "table", then the model instance must have all its elements belonging to the same type. | No default value.                                                                                                    |
| named table                                           | It will verify each attribute according to the rules above.                                                                                                                                                                                            | The table itself. It is possible to define only part of the table in the instance, keeping the other default values. |

### Attributes

Some attributes of Model have internal semantics. They can be used as **read-only** by the modeler.

- **parent**: The Model used to create the object. This object only exists in the Model instance, but not in the Model itself.

### Usage

```
Tube = Model{
    initialWater = 20,
    flow = 1,
    finalTime = 20,
    init = function(model)
        model.water = model.initialWater

        model.chart = Chart{target = model, select = "water"}

        model:notify()
        model.timer = Timer{
            Event{action = function()
                model.water = model.water - model.flow
             end},
            Event{action = model.chart}
        }
    end
}

print(type(Tube)) -- "Model"
Tube:run() -- One can run a Model directly...

MyTube = Tube{initialWater = 50} -- ... or create instances using it
print(type(MyTube)) -- "Tube"
print(MyTube:title()) -- "Initial Water = 50"
MyTube:run()

pcall(function() MyTube2 = Tube{initialwater = 100} end)
-- Warning: Argument 'initialwater' is unnecessary. Do you mean 'initialWater'?
-- (when executing TerraME with mode=strict)

_, err = pcall(function() MyTube2 = Tube{flow = false} end)
print(err)
-- Error: Incompatible types. Argument 'flow' expected number, got boolean.
```

---

## Functions

|                                                                           |                                                                                            |
| ------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------ |
| [configure](./model.md#configure)         | Function to show a graphical interface to configure the parameters of a given Model.       |
| [execute](./model.md#execute)             | User-defined function to execute the Model in a given time step.                           |
| [getParameters](./model.md#getparameters) | Return the parameters of the Model as they were defined.                                   |
| [init](./model.md#init)                   | User-defined function to create the objects of the Model.                                  |
| [interface](./model.md#interface)         | User-defined function to define the distribution of components in the graphical interface. |
| [isRandom](./model.md#israndom)           | Return if a Model uses random numbers.                                                     |
| [notify](./model.md#notify)               | Notify the Observers of the Model instance.                                                |
| [run](./model.md#run)                     | Run the Model instance.                                                                    |
| [title](./model.md#title)                 | Return a title for the Model instance according to its parameters.                         |

---

## **configure** 

Function to show a graphical interface to configure the parameters of a given Model. This function can be used in scripts that implement a Model. If the Model belongs to a package, then it should not be called, as TerraME will do it automatically when one selects the Model to be configured.  
  

### Usage

```
Tube = Model{
    initialWater = 20,
    flow = 1,
    finalTime = 20,
    execute = function(model)
        model.water = model.water - model.flow
    end,
    init = function(model)
        model.water = model.initialWater

        model.chart = Chart{target = model, select = "water"}

        model.timer = Timer{
            Event{action = model},
            Event{action = model.chart}
        }
    end
}

Tube:configure()
```

---

## **execute** 

User-defined function to execute the Model in a given time step. It is useful when using the Model as an action for a given [Event](./event.md).  
  

### Usage

```
Tube = Model{
    water = 20,
    flow = 1,
    finalTime = 20,
    execute = function(model)
        model.water = model.water - model.flow
    end,
    init = function (model)
        model.chart = Chart{
            target = model,
            select = "water"
        }
    end
}
```

---

## **getParameters** 

Return the parameters of the Model as they were defined. The result must not be changed, otherwise it might affect the Model itself.  
  

### Usage

```
model = Model{
    par1 = 3,
    par2 = Choice{"low", "medium", "high"},
    par3 = {min = 3, max = 5},
    finalTime = 20,
    init = function(model)
        model.timer = Timer{
            Event{action = function()
                -- ...
            end}
        }
    end
}

params = model:getParameters()
print(params.par1)
print(type(params.par2))
print(params.init) -- nil
```

---

## **init** 

User-defined function to create the objects of the Model. It is recommended that all the created objects should be placed in the model instance itself, to guarantee the content of the Model into a single object. It is also possible to verify whether the model has correct arguments. The internal verification of Model ensures that the type of the arguments is valid, acording to the definition of the Model. See [toLabel()](../functions/utils.md#tolabel), for using names of arguments in error messages when building a Model to work with graphical interfaces. This function is executed automatically when one instantiates a given Model.  
  

### Usage

```
Tube = Model{
    initialWater = 200,
    flow = 20,
    init = function(model)
        verify(model.flow < model.initialWater, toLabel("flow").." should be less than "..toLabel("initialWater")..".")
        model.finalTime = 10
        model.timer = Timer{
            Event{action = function()
                -- ...
            end}
        }
    end
}

m = Tube{initialWater = 100, flow = 10}
print(m.finalTime) -- 10
```

### See also

- [customError (ErrorHandling)](../functions/errorHandling.md#customerror)
- [verify (ErrorHandling)](../functions/errorHandling.md#verify)

---

## **interface** 

User-defined function to define the distribution of components in the graphical interface. If this function is not implemented in the Model, the components will be distributed automatically. This function should return a table with tables composed by strings. Each position of the table describes a column of components in the interface. In the example below, the first column of the graphical interface will show the string argument in the top ("mapFile") and the three arguments of "agents" in the bottom of the first column. The second column will contain the arguments of "block" in the top and the boolean argument ("showGraphics") in the bottom. The elements that do not belong to the table will not be shown in the graphical interface (in the example, "season"). Note that all Compulsory arguments must belong to the graphical interface to allow instantiate Model instances properly.  
  

### Usage

```
Sugarscape = Model{
    mapFile        = "sugar-map.csv",
    showGraphics   = true,
    agents = {
        quantity   = 10,
        wealth     = Choice{min = 5, max = 25},
        metabolism = Choice{min = 1, max = 4}
    },
    block = {
        xmin       = 0,
        xmax       = math.huge,
        ymin       = 0,
        ymax       = math.huge
    },
    season = {
        summerGrowthRate = 1,
        winterGrowthRate = 0.125
    },
    interface = function()
        return {
            {"string", "agents"},
            {"block", "boolean"}
        }
    end,
    init = function(model)
        model.timer = Timer{
            Event{action = function() end}
        }
    end
}

Sugarscape:configure()
```

---

## **isRandom** 

Return if a Model uses random numbers. This can be configured with the argument random while creating a Model.  
  

### Usage

```
RandomModel = Model{
    random = true,
    finalTime = 10,
    init = function(model)
        model.timer = Timer{
            Event{action = function()
                print(Random():number())
            end}
       }
    end
}

print(RandomModel:isRandom())
```

---

## **notify** 

Notify the Observers of the Model instance.  
  

### Arguments

- **#1**: A number representing the notification time. The default value is zero. It is also possible to use an [Event](./event.md) as argument. In this case, it will use the result of [Event:getTime()](./event.md#gettime).

### Usage

```
Tube = Model{
    water = 200,
    init = function(model)
        model.finalTime = 100

        Chart{
            target = model,
            select = "water"
        }

        model.timer = Timer{
            Event{action = function(ev)
                model.water = model.water - 1
                model:notify(ev)
            end}
        }
    end
}

scenario1 = Tube{water = 100}

scenario1:run()
```

---

## **run** 

Run the Model instance. It requires that the Model instance has attribute finalTime.  
  

### Usage

```
Tube = Model{
    initialWater = 200,
    flow = 20,
    init = function(model)
        model.finalTime = 10

        model.timer = Timer{
            Event{action = function()
                -- ...
            end}
        }
    end
}

m = Tube{initialWater = 100, flow = 10}

m:run()
```

---

## **title** 

Return a title for the Model instance according to its parameters. It uses only the parameters that are different from the default values. If the Model was instantiated without any parameter, its title will be "default".  
  

### Usage

```
Tube = Model{
    water = 200,
    init = function(model)
        model.finalTime = 100

        Chart{
            target = model,
            select = "water"
        }

        model.timer = Timer{
            Event{action = function(ev)
                model.water = model.water - 1
                model:notify(ev)
            end}
        }
    end
}

scenario1 = Tube{water = 100}
print(scenario1:title()) -- "water = 100"
```