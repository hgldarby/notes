# Genetic Algorithm (GA)

### Definition

- A procedure inspires by the process of natural selection that belongs to the class of evolutionary algorithms. They are commonly used to generate high-quality solutions by relying on bio-inspired operators such as mutation, crossover and selection.

### Methodology

- In GA, a population of candidate solutions (eg creatures) to an optimisation problem is evolved toward better solutions.
- Each candidate solution has a set of properties (i.e. strength, chromosomes, genotypes) which can be mutated and altered.
- Each iteration in the process is called a "generation"
- In each generation, the fitness of every individual in the population is evaluated

- The fitter individuals are randomly selected from the current population, and each individuals genome is modified to form a new generation.
- The new generation of candidate solutions is then used in the next iteration
- Commonly it terminates when either a max number of generations has been produced, or satisfactory fitness level has been reached for the population.
- A typical GA requires:
  - A genetic representation of the solution domain,
  - A fitness function to evaluate the solution domain
- A standard representation of each candidate solution is an array of bits.
- These are convenient due to their fixed size, facilitating simple crossover operations.

#### Initialisation

- Population size depends o the nature of the problem, but typically contains several hundreds of thousands of possible solutions.
- Initial population is generated randomly
- Occasionally solutions may be seeded in areas where optimal solutions are likely to be found.

#### Selection

- During each successive Generation, a portion of the existing population is selected to breed a new generation.
- Individual solutions are selected through a fitness-based process where the fitter solutions (chosen using the fitness function) are more likely to be selected
- Certain selection methods rate the fitness of each solution and preferentially select the best solutions.
- Other methods rate only a random sample of the population, as the former process may be very time-consuming

- In some problems, it is hard or even impossible to define a fitness expression. In these cases a simulation may be used to determine the fitness function value, or even interactive genetic algorithms are used.

