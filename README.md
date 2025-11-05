# CI2025_lab2: Genetic Algorithm for the TSP

## Solution Representation

A solution is an array of integers containing a permutation of [0, …, N-1].

The tour is cyclic: the last city returns to the first.

### cost(adj, sol) 
    Calculates the sum of the edge costs in the tour using a “shift”.

## Generating Initial Solutions
### starting_point(problem)
    Technique: random permutation using np.random.default_rng().
    Generates a random tour as a starting point.
    For reproducibility: pass a fixed seed or an initialized Generator.

## Genetic Operators

### swap_mutation(solution, mutation_rate)
    Technique: swap mutation.
    With probability mutation_rate, two cities in the solution are swapped at random.

    Advantages:
    1) Maintains a valid permutation
    2) Introduces variation without overly disrupting the structure

### order_crossover_ox1(parent1, parent2)

    Technique: Order Crossover (OX1), standard for permutation-based problems.
    Steps:
        Selects two random cut points (cut1, cut2)
        Copies the segment parent1[cut1:cut2] into the offspring
        Fills the remaining positions with elements from parent2 in order, skipping duplicates
        Properly handles the “wrap-around” to close the offspring

### tournament_selection(population, costs, k)

    Technique: tournament selection. Selects k random individuals and returns the one with the lowest cost.
    Properties:
        1) Small k → more diversity, less selective pressure
        2) Large k → stronger pressure, risk of premature convergence

## Evolutionary Cycle

### evolutionary_algorithm(problem, population_size, num_generations, tournament_size, mutation_rate, elitism)
    Workflow: 
        1) Initialization: random population
        2) Evaluation: compute the cost of each individual
        3) Elitism: copy the top elitism individuals into the new generation
        4) Reproduction: Selection → Crossover → Mutation
        5) Replacement: new population
        6) Update: tracking of the best-so-far solution
        7) Termination: after num_generations


work with: (https://github.com/LucaFavole)