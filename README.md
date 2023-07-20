# Introduction

This repository contains the genetic algorithms and analysis notebooks to support the paper "Best Practices for Using Genetic Algorithms in Molecular Discovery."

This project aimed to optimize genetic algorithm hyperparameters such as population size, mutation rate, elitism percentage, selection method, and introduce systematic convergence criteria for molecular discovery . 

# GA to tune hyperparameters

The genetic algorithm for tuning the hyperparameters (with a pre-computed search space) can be found `GA_code/GA_main.py`, with the fitness function code in `GA_code/scoring.py`.

To run this code on the command line, go into the `GA_code` directory and enter `python GA_main.py <param_type> <param_value> <chem_property> <run_label>`

The options for these arguments are:
- `<param_type>`: 'pop_size', 'selection_method', 'mutation_rate', or 'elitism_perc'
  - pop_size can be any integer, but is recommended to be larger than 10
  - selection_method can be from the following options: 'random', 'random_top50', 'tournament_2', 'tournament_3', 'tournament_4','roulette', 'SUS', or 'rank'
  - mutation_rate is any float between 0 and 1
  - elitism_perc is any float between 0 and 1
- `<param_value>`: the value to change the parameter type to. Ex: ifparam_type is pop_size, then param_value can be 32
- `<chem_property>`: This is the chemical property we are scoring on in the fitness function. Options are 'polar', 'opt_bg', or 'solv_eng'
- `<run_label>`: This label is for reproducibility and each letter corresponds to an initial random state. Options are 'A', 'B', 'C', 'D', or 'E'

# GA in a realistic test scenario
Due to the potential for relatively costly calculations with GFN2-xTB, this GA was run with cron to automatically check if the previous generation's calculations were completed before starting the next generation. While the general workflow of the GA is the same, the code was manipulated to submit one generation at a time. The code to be used with cron can be found in `optimized_ga/GA_cron/GA_main.py`. NOTE: Installing xTB for GFN2 is necessary to run the calculations.

# Package dependencies
- numpy 1.21.6
- pandas 1.1.5
- scipy 1.7.3
- rdkit 2022.3.3
- pybel (openbabel 2.4.1)
- matplotlib 3.5.2 (data analysis)
