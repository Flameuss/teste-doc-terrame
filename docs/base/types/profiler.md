# Profiler

The type Profiler is used to measure the simulation/execution time of a model or the time to execute small blocks of a model. The user can inform Profiler how many times a block will execute. Thus it can estimate the time left to finish the execution of a block. This type also summaries all its measures and show a report containing how many times a block was executed, the time to execute all repetitions of this block and the average time of these repetitions.  
  

### Usage

```
Profiler():start("test")
Profiler():stop("test")
print(Profiler():uptime("test"))
```

---

## Functions

|                                                                  |                                                                                                                   |
| ---------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------- |
| [clean](./profiler.md#clean)     | Clean the Profiler, removing all blocks and restarting its execution time.                                        |
| [clock](./profiler.md#clock)     | Return how much time of CPU was spent on the block up to last stop.                                               |
| [count](./profiler.md#count)     | Return how many times a given block has started.                                                                  |
| [current](./profiler.md#current) | Return the current block.                                                                                         |
| [eta](./profiler.md#eta)         | Estimate and return the time to execute all repetitions of a given block.                                         |
| [report](./profiler.md#report)   | Show a report with the time and amount of times each block was executed.                                          |
| [start](./profiler.md#start)     | Create and start a new block.                                                                                     |
| [steps](./profiler.md#steps)     | Define how many times a given block will be executed.                                                             |
| [stop](./profiler.md#stop)       | Stop to measure the time of a given block and return how much time was spent with the block since it was started. |
| [uptime](./profiler.md#uptime)   | Return how much time was spent on the block up to last stop.                                                      |

---

## **clean** 

Clean the Profiler, removing all blocks and restarting its execution time.  
  

### Usage

```
Profiler():clean()
```

---

## **clock** 

Return how much time of CPU was spent on the block up to last stop. It returns two representations: a string with a human-like representation of the time and a number with the time in seconds.  
  

### Arguments

- **#1**: A string with the block name. If the name is not informed, then it returns the uptime of the current block.

### Usage

```
Profiler():start("block")
Profiler():stop("block")
stringTime, numberTime = Profiler():clock("block")
```

---

## **count** 

Return how many times a given block has started.  
  

### Arguments

- **#1**: A string with the block name. If the name is not informed, then it returns the count of the current block.

### Usage

```
Profiler():start("block")
print(Profiler():count("block")) -- 1
Profiler():stop("block")
```

---


## **current** 

Return the current block.  
  

### Usage

```
Profiler():start("block")
print(Profiler():current().name) -- block
Profiler():stop("block")
```

---

## **eta** 

Estimate and return the time to execute all repetitions of a given block. It returns in two representations: a string with a human-like representation of the time and a number with the time in seconds.  
  

### Arguments

- **#1**: A string with the block name. If the name is not informed, then it returns the "eta" of the current block.

### Usage

```
Profiler():steps("block", 5)
Profiler():start("block")
Profiler():stop("block")
eta_string, eta_number = Profiler():eta("block")
print(eta_string.." left...")
print(eta_number.." seconds to finish...")
```

---

## **report** 

Show a report with the time and amount of times each block was executed.  
  

### Usage

```
Profiler():report()
```

---

## **start** 

Create and start a new block.  
  

### Arguments

- **#1**: A string with the block name.

### Usage

```
Profiler():start("block")
Profiler():stop("block")
```

---

## **steps** 

Define how many times a given block will be executed.  
  

### Arguments

- **#1**: A string with the block name.
- **#2**: Number of steps a given block will execute.

### Usage

```
Profiler():start("block")
Profiler():steps("block", 5)
Profiler():stop("block")
```

---

## **stop** 

Stop to measure the time of a given block and return how much time was spent with the block since it was started. It returns a table with the spent time in seconds (time), a string with a human-like representation of the time (strTime), spent time of CPU in high precision (clock), a string with a human-like representation of the time of CPU (strClock).  
  

### Arguments

- **#1**: A string with the block name. If the name is not informed, then it stops and return the uptime of the current block.

### Usage

```
Profiler():start("block")
timeTable = Profiler():stop("block")
time = timeTable.time
clock = timeTable.clock
strTime = timeTable.strTime
strClock = timeTable.strClock
```

--- 

## **uptime** 

Return how much time was spent on the block up to last stop. It returns two representations: a string with a human-like representation of the time and a number with the time in seconds.  
  

### Arguments

- **#1**: A string with the block name. If the name is not informed, then it returns the uptime of the current block.

### Usage

```
Profiler():start("block")
Profiler():stop("block")
stringTime, numberTime = Profiler():uptime("block")
```