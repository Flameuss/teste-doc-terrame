# Examples

|                                                                                                |                                                                                       |
| ---------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------- |
| [barros](./examples.md#barros)                                 | Implementation of Barros urban dynamics model.                                        |
| [beer](./examples.md#beer)                                     | Implementation of beer economic chain model.                                          |
| [continuous-rain](./examples.md#continuous-rain)               | A simple continuous rain model.                                                       |
| [deforestation](./examples.md#deforestation)                   | Amazonia deforestation models.                                                        |
| [discrete-rain](./examples.md#discrete-rain)                   | A simple discrete rain model.                                                         |
| [drainage](./examples.md#drainage)                             | A simple drainage model.                                                              |
| [el-farol](./examples.md#el-farol)                             | Implementation of El Farol model.                                                     |
| [fire-spread](./examples.md#fire-spread)                       | A simple spread model that uses geospatial data.                                      |
| [game-of-life](./examples.md#game-of-life)                     | Implementation of Conway's Game of Life.                                              |
| [growing-moving-society](./examples.md#growing-moving-society) | A model with 100 moving and growing Agents.                                           |
| [growing-society](./examples.md#growing-society)               | A model with static Agents that can reproduce to neighbor Cells.                      |
| [ipd](./examples.md#ipd)                                       | Iterated Prisoner's dilemma model.                                                    |
| [leontief](./examples.md#leontief)                             | Implementation of a model to study scenarios for the economy of Southeast Para state. |
| [predator-prey](./examples.md#predator-prey)                   | Implementation of a spatial predator-prey model.                                      |
| [runoff](./examples.md#runoff)                                 | Implementation of a simple runoff model using geospatial data.                        |
| [schelling](./examples.md#schelling)                           | Implementation of Schelling's segregation model.                                      |
| [single-agent](./examples.md#single-agent)                     | A simple example with one Agent that moves randomly in space.                         |
| [single-agents-society](./examples.md#single-agents-society)   | Simulation of a Society with 30 moving Agents.                                        |
| [sir-abm](./examples.md#sir-abm)                               | SIR model implemented with agents.                                                    |
| [sir-basic](./examples.md#sir-basic)                           | A simple Susceptible-Infected-Recovered (SIR) model.                                  |
| [sir-campaign](./examples.md#sir-campaign)                     | A Susceptible-Infected-Recovered (SIR) model with a public campaign.                  |
| [sir-improved](./examples.md#sir-improved)                     | A Susceptible-Infected-Recovered (SIR) model.                                         |
| [spatial-game](./examples.md#spatial-game)                     | Implementation of the model proposed by Nowak and Sigmund.                            |
| [tube-discrete](./examples.md#tube-discrete)                   | A model that describes water flowing out of a tube.                                   |
| [tube-inflow-outflow](./examples.md#tube-inflow-outflow)       | A model that describes water flowing in and out of a tube.                            |
| [tube](./examples.md#tube)                                     | A simple model that describes water flowing out of a tube.                            |

---

## [barros](http://localhost:5500/examples/barros.lua)

![](http://localhost:5500/images/barros.png)

  
  
Implementation of Barros urban dynamics model. It simulates a virtual city composed by poor, middle class, and rich people. The simulation starts with the city having only one inhabitant in the center of space. At each time step, a new inhabitant arrives in the center. As it is not possible to have more than one inhabitant in the same cell, the arriving inhabitants with higher income can replace those with lower income, which in turn need to search for a new cell to leave, moving randomly. Empty cells can be occupied by any kind of agent.  
  
Reference: Barros, J. "Simulating urban dynamics in Latin American cities." GeoDynamics (2005): 313-328.  
  

### Arguments (global variables)

- **P_POOR**: Percentage of poor agents.
- **P_MIDDLE**: Percentage of middle class agents.
- **P_RICH**: Percentage of rich agents. Note that the sum of the three percentages must be one.
- **DIM**: The x and y dimensions of space.
- **AGENTS**: The number of agents in the simulation.

---

## [beer](http://localhost:5500/examples/beer.lua)

![](http://localhost:5500/images/beer.png)

  
  
Implementation of beer economic chain model. This model represents an economic chain with a manufacturer, some intermediate nodes (such as a distributor and a supplier), and a retailer. The agents in the economic chain need to fill their demand by requesting beer to the previous agent of the chain. The retailer has a random demand, while the others have a demand requested by the next agent of the chain. Each requested beer takes three time steps to be delivered from one agent to the next one (as long as there is some stock to fulfil the demand). The objective of the game is to minimize expenditure from back orders and inventory.  
  
For more information, see [https://en.wikipedia.org/wiki/Beer_distribution_game.](https://en.wikipedia.org/wiki/Beer_distribution_game.)  
  

### Arguments (global variables)

- **NUMBER_OF_AGENTS**: Number of agents in the chain, excluding the manufacturer and the retailer. The default value is three.

---

## [continuous-rain](http://localhost:5500/examples/continuous-rain.lua)

A simple continuous rain model. It uses three differential equations to simulate rain, soil water, and drainage dynamics.  
  

### Arguments (global variables)

- **C**: The amount of rain per unit of time. The default value is 2.
- **K**: The flow coefficient. The default value is 0.4.
- **dt**: The step used in the numerical integration. The default value is 0.01.


---

## [deforestation](http://localhost:5500/examples/deforestation.lua)

![](http://localhost:5500/images/deforestation.png)

  
  
Amazonia deforestation models. It uses a top-down approach with three strategies to compute deforestation potential. The first strategy compute the deforestation potential based on the deforestation of neighbor cells. The second one uses the result of a statistical regression using distance to urban areas, connection to markets, and coverage of protected areas as parameters. The last strategies mixes the other two. It adds the average deforestation of the neighborhood to the statistical regression.  
  

 --- 

## [discrete-rain](http://localhost:5500/examples/discrete-rain.lua)

A simple discrete rain model. It simply computes the amount of water according to the rain and a flow coefficient.  
  

### Arguments (global variables)

- **C**: The amount of rain per unit of time. The default value is 2.
- **K**: The flow coefficient. The default value is 0.4.

---

## [drainage](http://localhost:5500/examples/drainage.lua)

![](http://localhost:5500/images/drainage.png)

  
  
A simple drainage model. It uses a Chart to show the output of the simulation.  
  

---

## [el-farol](http://localhost:5500/examples/el-farol.lua)

![](http://localhost:5500/images/el-farol.png)

  
  
Implementation of El Farol model. It is based on Brian Arthur's paper available at [http://www.santafe.edu/~wbarthur/Papers/El_Farol.](http://www.santafe.edu/~wbarthur/Papers/El_Farol.) In this model, there is a city with a given population. Everybody wants to go to an entertainment offered once a week by a bar called El Farol. However, if the bar is too crowded, it is not enjoyable. Each agent decides on whether to go to the bar based on its expectations on how much people the bar will have. Decisions are taken independently from each other. Agents can have different ways of thinking, based on the amount of people that went to the bar in the last weeks.  
  

### Arguments (global variables)

- **N**: Number of people in the city. The default value is 100.
- **K**: number of strategies each individual has (if only one then the agent will never change its strategy). The default value is 3.
- **MAX**: Maximum number of people in the bar. The default value is 60.

---

## [fire-spread](http://localhost:5500/examples/fire-spread.lua)

![](http://localhost:5500/images/fire-spread.png)

  
  
A simple spread model that uses geospatial data. It simulates a fire in Parque Nacional das Emas, in Goias state, Brazil. It has probabilities for fire spread according to the biomass stored in each cell.  
  
This model was proposed by Almeida, Rodolfo M., et al. (in portuguese) 'Simulando padroes de incendios no Parque Nacional das Emas, Estado de Goias, Brasil.' X Simposio Brasileiro de Geoinfoamatica (2008).  
  

### Arguments (global variables)

- **STEPS**: The final simulation time. The default value is 35.

---

## [game-of-life](http://localhost:5500/examples/game-of-life.lua)

![](http://localhost:5500/images/game-of-life.png)

  
  
Implementation of Conway's Game of Life. It is a classical Cellular Automata model that simulates changes in a society using very simple rules. Each cell represents an individual that can have two states: alive or dead. Using its own state and the state of its neighbors, each individual decides its next state. The model has four rules. First, an alive cell with fewer than two alive neighbors dies by loneliness. Second, an alive cell with two or three alive neighbors stays alive. Third, an alive cell with more than three alive neighbors dies by over-population. Fourth, a dead cell with three alive neighbors becomes alive by reproduction.  
  
This implementation creates the initial distribution of alive cells randomly.  
  
For more information, see [https://en.wikipedia.org/wiki/Conway](https://en.wikipedia.org/wiki/Conway)'s_Game_of_Life.  
  

### Arguments (global variables)

- **PROBABILITY**: The probability of a Cell to be alive in the beginning of the simulation. The default value is 0.15.
- **TURNS**: The number of simulation steps. The default value is 20.

---

## [growing-moving-society](http://localhost:5500/examples/growing-moving-society.lua)

![](http://localhost:5500/images/growing-moving-society.png)

  
  
A model with 100 moving and growing Agents. An Agent moves to an empty random cell in each time step and reproduces if it finds another empty random cell, given a probability.  
  

### Arguments (global variables)

- **GROWTH_PROB**: The probability of an agent to reproduce in an empty neighbor cell. The default value is 0.3.


---

## [growing-society](http://localhost:5500/examples/growing-society.lua)

![](http://localhost:5500/images/growing-society.png)

  
  
A model with static Agents that can reproduce to neighbor Cells. An Agent reproduces if it finds another empty random cell, given a probability.  
  

### Arguments (global variables)

- **GROWTH_PROB**: The probability of an agent to reproduce in an empty neighbor cell. The default value is 0.3.

---

## [ipd](http://localhost:5500/examples/ipd.lua)

Iterated Prisoner's dilemma model. It implements a championship with a set of Agents where they play with each other a non-cooperative game repeatedly. Some of the available strategies are Pavlov and Tit-for-tat. In the end, the model shows the results for each strategy.  
  
For more information, see Axelrod, R. (1984) The Evolution of Cooperation. Basic Books. See also Nowak, M., and Sigmund, K. (1993) A strategy of win-stay, lose-shift that outperforms tit-for-tat in the Prisoner's Dilemma game. Nature 364.6432: 56-58.  
  

### Arguments (global variables)

- **TURNS**: The number of times an Agent plays with each opponent.
- **CHAMPIONSHIP**: A vector with the strategies used in the championship.

---

## [leontief](http://localhost:5500/examples/leontief.lua)

Implementation of a model to study scenarios for the economy of Southeast Para state. This model solves the inversion of an input-output matrix using an agent-based model. It implements a set of investment scenarios for the region and simulates the impacts over salaries, employment, and carbon emissions.  
  
For more information, see Andrade et al. (2010) From input-output matrixes to agent-based models: A case study on carbon credits in a local economy. BWSS 2010.  
  

### Arguments (global variables)

- **scenario**: Number of the scenario. It can be an integer value between 1 and 5. The default value is 1.

---

## [predator-prey](http://localhost:5500/examples/predator-prey.lua)

![](http://localhost:5500/images/predator-prey.png)

  
  
Implementation of a spatial predator-prey model. This model has two Societies. One composed by preys that feed grass and the other composed by predators that feed preys. Agents move randomly in space and can reproduce. The output is similar to Lotka-Volterra equations.  
  

---

## [runoff](http://localhost:5500/examples/runoff.lua)

![](http://localhost:5500/images/runoff.png)

  
  
Implementation of a simple runoff model using geospatial data. There is an initial rain in the highest cells. The Neighborhood of a Cell is composed by its Moore neighbors that have lower height. Each cell then sends its water equally to all neighbors.  
  

---

## [schelling](http://localhost:5500/examples/schelling.lua)

![](http://localhost:5500/images/schelling.png)

  
  
Implementation of Schelling's segregation model. In this model, a Society is composed by two types of Agents, reds and blacks, which live in Cells. Each Agent is happy if its neighborhood has at least a given number of Agents sharing its type. Otherwise, it will try to move to another place where it is satisfied. Using this model, Thomas Schelling showed that a small preference for one's neighbors to be of the same color could lead to total segregation.  
  
For more information, see Schelling, T. (1971) Dynamic models of seggregation, Journal of Mathematical Sociology 1:143-186.  
  

### Arguments (global variables)

- **NDIM**: Space dimensions in x and y axis.
- **PREFERENCE**: Agent contentedness, indicating the minimum number of neighbors of the same color to make the agent satisfied. It should be an integer number between 3 and 5.
- **NAGTS**: The proportion of agents in space.
- **MAX_TURNS**: Maximum number of simulation steps.


---

## [single-agent](http://localhost:5500/examples/single-agent.lua)

![](http://localhost:5500/images/single-agent.png)

  
  
A simple example with one Agent that moves randomly in space.  
  

---

## [single-agents-society](http://localhost:5500/examples/single-agents-society.lua)

![](http://localhost:5500/images/single-agents-society.png)

  
  
Simulation of a Society with 30 moving Agents.  
  

---

## [sir-abm](http://localhost:5500/examples/sir-abm.lua)

![](http://localhost:5500/images/sir-abm.png)

  
  
SIR model implemented with agents. This model needs to have more implementation decisions if compared to one implemented using system dynamics. The social network of an agent is fixed? In a system dynamics model it supposes that the network is not fixed as disease is propagated to the whole population using probabilities. Another question: an agent that has got sick in a given time step can infect other agents? This implementation supposes it can only infect in the next time step.  
  

---

## [sir-basic](http://localhost:5500/examples/sir-basic.lua)

![](http://localhost:5500/images/sir-basic.png)

  
  
A simple Susceptible-Infected-Recovered (SIR) model. This model represents a given disease that propagates over a population. It starts with a small number of infected that passes the disease to the susceptible ones. After some time, infected become recovered, which cannot be infected again.  
  
For mode details visit [http://en.wikipedia.org/wiki/Epidemic_model.](http://en.wikipedia.org/wiki/Epidemic_model.)  
  

---

## [sir-campaign](http://localhost:5500/examples/sir-campaign.lua)

![](http://localhost:5500/images/sir-campaign.png)

  
  
A Susceptible-Infected-Recovered (SIR) model with a public campaign. The campaign asks the population to stop leaving home, which reduces the number of contacts by half. It is activated whenever there are more than 1000 infected individuous in the population.  
  

---

## [sir-improved](http://localhost:5500/examples/sir-improved.lua)

![](http://localhost:5500/images/sir-improved.png)

  
  
A Susceptible-Infected-Recovered (SIR) model. In this model the disease has a duration of 8 weeks. We can see that the maximum number of infected is proportional to the duration of the disease.  
  

---

## [spatial-game](http://localhost:5500/examples/spatial-game.lua)

![](http://localhost:5500/images/spatial-game.png)

  
  
Implementation of the model proposed by Nowak and Sigmund. In this model, each Cell has a strategy and plays a non-cooperative game with its neighbors. Then it updates its strategy with the most successful one among its neighbors. This simple spatial game produces a very complex spatial dynamics such as kaleidoscopes and dynamic fractals.  
  
Reference: Nowak and Sigmund (2004) Evolutionary Dynamics of Biological Games, Science 303(5659):793-799.  
  

### Arguments (global variables)

- **N**: Space dimensions in x and y axis.
- **TURNS**: Number of simulation steps.

---

## [tube-discrete](http://localhost:5500/examples/tube-discrete.lua)

![](http://localhost:5500/images/tube-discrete.png)

  
  
A model that describes water flowing out of a tube. It uses an observation step more frequent than the execution. Because of that, we can see that the water flows out of the tube in discrete steps.  
  

---

## [tube-inflow-outflow](http://localhost:5500/examples/tube-inflow-outflow.lua)

![](http://localhost:5500/images/tube-inflow-outflow.png)

  
  
A model that describes water flowing in and out of a tube. This implementation also verifies does not allow to have negative amounts of water in the tube.  


---

## [tube](http://localhost:5500/examples/tube.lua)

![](http://localhost:5500/images/tube.png)

  
  
A simple model that describes water flowing out of a tube.