# Clock

Create a display with the current time and [Event](./event.md) queue of a given [Timer](./timer.md).  
  

### Arguments

- **target**: A Timer.

### Usage

```
timer = Timer{
    Event{action = function() end},
    Event{period = 2, action = function() end}
}

Clock{target = timer}

timer:run(3)
timer:notify()
```
---

## Functions

|                                                             |                                                        |
| ----------------------------------------------------------- | ------------------------------------------------------ |
| [save](./clock.md#save)     | Save a Clock into a file.                              |
| [update](./clock.md#update) | Update the Clock with the latest values of its target. |

---

## **save** 

Save a Clock into a file. Supported extensions are bmp, jpg, png, and tiff.  
  

### Arguments

- **#1**: A string with the file name.

### Usage

```
timer = Timer{
    Event{action = function() end}
}

clock = Clock{target = timer}

clock:save("file.bmp")
File("file.bmp"):delete()
```

---

## **update** 

Update the Clock with the latest values of its target. It is usually recommended to use the Clock as action of an [Event](./event.md) instead of calling this function explicitly.  
  

### Usage

```
timer = Timer{
    Event{action = function() end}
}

clock = Clock{target = timer}

clock:update()
```