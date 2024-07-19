# Random

Type to generate random numbers. It uses Xorshift generators are among the fastest non-cryptographic random number generators. Xorshift random number generators are a class of pseudorandom number generators that was discovered by George Marsaglia ([http://www.jstatsoft.org/v08/i14/paper](http://www.jstatsoft.org/v08/i14/paper)). All the instances of Random along a given simulation have the same seed. The distribution can be inferred according to the selected arguments, as shown below.  
  

| Arguments             | Default distribution |
| --------------------- | -------------------- |
| p                     | "bernoulli"          |
| lambda                | "poisson"            |
| mean (or) sd          | "normal"             |
| min, max, step        | "step"               |
| min, max              | "continuous"         |
| (set of values)       | "discrete"           |
| (set of named values) | "categorical"        |

### Arguments

- **alpha**: Argument of beta distribution. The default value is 1.
- **beta**: Argument of beta distribution. The default value is 1.
- **distrib**: A string representing the statistical distribution to be used. See the table below.

| Distrib       | Description                                                                                                                                                                                                                                          | Compulsory Arguments | Optional Arguments |
| ------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------- | ------------------ |
| "bernoulli"   | A boolean distribution that returns true with probability p.                                                                                                                                                                                         | p                    | seed               |
| "beta"        | A family of continuous probability distributions defined on the interval [0, 1] parametrized by two positive shape parameters, denoted by alpha and beta, that appear as exponents of the random variable and control the shape of the distribution. |                      | alpha, beta, seed  |
| "categorical" | A distribution that has names associated to probabilities. Each name is an argument and has a value between zero and one, indicating the probability to be selected. The sum of all probabilities must be one.                                       | ...                  | seed               |
| "continuous"  | A continuous uniform distribition. It selects real numbers in a given interval.                                                                                                                                                                      | max, min             | seed               |
| "discrete"    | A discrete uniform distribition. Elements are described as a vector.                                                                                                                                                                                 | ...                  | seed               |
| "exponential" | Generate exponentialy distributed pseudo random numbers from a uniformly distributed number in the range [0,1]. For this purpose, it uses the Inverse Transform Samplig method                                                                       |                      | lambda, seed       |
| "lognormal"   | Generate log-normally distributed pseudo random numbers from a normaly distributed number in the range [0,1] using the Box-Muller (1978) method.                                                                                                     |                      | mean, sd, seed     |
| "none"        | No distribution. This is useful only when the modeler wants only to set seed.                                                                                                                                                                        |                      | seed               |
| "normal"      | Generate Normally (Gaussian) distributed pseudo random numbers from a uniformly distributed number in the range [0,1] using the Box-Muller (1978) method .                                                                                           |                      | mean, sd, seed     |
| "poisson"     | Generate Poisson distributed pseudo random numbers from a uniformly distributed number in the range [0,1]. For this purpose, it uses the Inverse Transform Samplig method.                                                                           |                      | lambda, seed       |
| "step"        | A discrete uniform distribution whose values belong to a given [min, max] interval using step values.                                                                                                                                                | max, min, step       | seed               |
| "weibull"     | The Weibull distribution is a real valued distribution with two parameters a and b, producing values greater than or equals to zero.                                                                                                                 |                      | k                  |

- **k**: The shape parameter for Weibull distribution. The default value is 1.
- **lambda**: An argument of some distributions. It might be interpreted as mean or as scale, according to the given distribution. The default value is 1.
- **max**: A number indicating the maximum value to be randomly selected.
- **mean**: A number indicating the mean value. The default value is 1.
- **min**: A number indicating the minimum value to be randomly selected.
- **p**: A number between 0 and 1 representing a probability.
- **sd**: A number indicating the standard deviation. The default value is 1.
- **seed**: A number to generate the pseudo-random numbers. The default value is the current time of the system, which means that every simulation will use different random numbers. Choosing a seed in interesting when the modeler wants to have the same simulation outcomes despite using random numbers. It is a good programming practice to set the seed in the beginning of the simulation and only once.
- **step**: The step where possible values are computed from minimum to maximum. When using this argument, min and max become mandatory.
- **...**: Other values to build a categorical or discrete uniform distribution.

### Attributes

Some attributes of Random have internal semantics. They can be used as **read-only** by the modeler.

- **distrib**: The distribution of the Random object. All the other parameters of the distribution are also attributes.

### Usage

```
random = Random()

bernoulli = Random{p = 0.4}
print(bernoulli:sample())

range = Random{min = 3, max = 7}
print(range:sample())

step = Random{min = 1, max = 9, step = 2}
print(step:sample())

gender = Random{male = 0.49, female = 0.51}
print(gender:sample())

age = Random{1, 2, 4, 8, 16, 32}
print(age:sample())

cover = Random{"pasture", "forest", "clearcut"}
print(cover:sample())

person = Agent{
    gender = Random{male = 0.49, female = 0.51},
    age = Random{mean = 20, sd = 2},
    contacts = Random{lambda = 5}
}

soc = Society{
    instance = person,
    quantity = 10
}

print(soc:gender().male)
```

---

## Functions

|                                                                |                                                       |
| -------------------------------------------------------------- | ----------------------------------------------------- |
| [integer](./random.md#integer) | Return an integer random number.                      |
| [number](./random.md#number)   | Return a random real number.                          |
| [reSeed](./random.md#reseed)   | Set the seed to generate random numbers.              |
| [sample](./random.md#sample)   | Return a random element from the chosen distribution. |

---

## **integer** 

Return an integer random number. It uses a discrete uniform distribution.  
  

### Arguments

- **#1**: An integer number. If abscent, integer() will return zero or one. If it is the only argument, it will return a number between zero and this value.
- **#2**: An integer number. When used, integer() will return a number between the first argument and the second, inclusive.

### Usage

```
random = Random()

value = random:integer() -- 0 or 1
value = random:integer(10) -- from 0 to 10
value = random:integer(5, 10) -- from 5 to 10
```

---

## **number** 

Return a random real number. By default number() will return a value between zero and one.  
  

### Arguments

- **#1**: A number. If it is the only argument used, it will return a number from zero to this value.
- **#2**: A number. When used, number() will return a number between the first argument and the second.

### Usage

```
random = Random()

value = random:number() -- between 0 and 1
value = random:number(10) -- between 0 and 10
value = random:number(5, 10) -- between 5 and 10
```

---

## **reSeed** 

Set the seed to generate random numbers. This seed will be used in new instances of Random. All Random objecs previously created will still use the previous seed.  
  

### Arguments

- **#1**: An integer number with the new seed.

### Usage

```
random = Random()

random:reSeed(12345)
```

---

## **sample** 

Return a random element from the chosen distribution.  
  

### Usage

```
random = Random{2, 3, 4, 6}

random:sample()
```