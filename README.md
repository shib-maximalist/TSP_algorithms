# TSP Algorithms — Traveling Salesman on a German Map

Three different approaches to solving the Traveling Salesman Problem, visualized on a map of Germany with 44 cities. Because nothing teaches you about optimization like watching a greedy algorithm confidently pick the worst possible route.

## What it does

Loads 44 coordinate points on a German map and finds the shortest route that visits all of them exactly once, then returns to the start. You pick the algorithm, watch it work, and compare the results.

## Demo
https://github.com/user-attachments/assets/f6c186d9-8115-4f35-afaf-f8f32e775f92

## The three algorithms

### 1. Greedy (Nearest Neighbor)
Starts at a random city, always goes to the closest unvisited one. Fast, simple, and reliably mediocre. It's the "good enough" baseline.

### 2. 2-opt Swap (Local Search)
Starts with a random route, then iteratively removes two edges and reconnects them differently. If the swap shortens the route, it keeps it. Repeats until no more improvements are found. Better than greedy, but can get stuck in local optima.

### 3. Genetic Algorithm (Evolutionary)
Maintains a population of 1,000 random routes and evolves them over generations using selection, crossover, and mutation:

- **Selection:** Routes performing below average are removed
- **Crossover:** Order-preserving crossover combines segments from two parent routes
- **Mutation:** Random city swaps at a 10% rate, applied to offspring only
- **Termination:** Stops when improvement drops below 0.1% over 500 generations

Generates a fitness graph showing convergence of both population average and best individual.

## Running it

```bash
pip install matplotlib
python main.py
```

A map window opens with the 44 cities plotted. Select an algorithm from the console menu (1, 2, or 3) and watch the route optimization in real time.

**Note:** Uses `ctypes.windll` for dialog boxes — Windows only as written. Replace the message box calls with `print()` to run on other platforms.

## Project structure

```
main.py              — Entry point, user interaction, algorithm selection
Logic.py             — All three algorithm implementations
GraphicsUnit.py      — Matplotlib visualization and map rendering
Ressources/
  coords.csv         — 44 city coordinates (x, y pixel positions)
  germany_without_cities.png — Background map image
```

## Dependencies

- Python 3.x
- matplotlib
- Windows OS (for dialog boxes)

## Context

Graduate coursework project exploring heuristic optimization. The genetic algorithm is the most interesting part — watching a population of random routes evolve into near-optimal solutions is a good demonstration of why evolutionary approaches work for NP-hard problems.
