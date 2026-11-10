# Heuristic Graph Pathfinding Agent Search Engine

**Progree AI Internship - Task 3**

Pathfinding agents that navigate grid mazes, implemented **from scratch** in Python: **A\* Search** (Manhattan heuristic) and **Dijkstra's algorithm**. Both run on the same search engine; only the heuristic differs. The agents are tested on grids with different obstacle layouts, and the experiments log step count, runtime and expanded-node density, with visualizations exported.

## Features
- A\* and Dijkstra written from scratch (only `heapq` is used for the priority queue)
- 4-connected movement (up, down, left, right), uniform step cost
- Six test grids (41x41): open, random 10%, random 20%, random 30%, perfect maze, serpentine corridor
- Metrics tracked: **path steps, runtime (ms), expanded nodes, expanded-node density (%)**
- Scalability test from 20x20 up to 160x160
- Automatic optimality check (A\* and Dijkstra must return equally short paths)
- Exported visualization logs: PNG paths, comparison charts, CSV, JSON and an animated GIF

## How it works
| Algorithm | Priority | Heuristic |
|-----------|----------|-----------|
| Dijkstra | g(n) | h(n) = 0 (explores in all directions) |
| A\* | g(n) + h(n) | Manhattan distance to the goal (admissible on a 4-connected grid, so the path is still optimal) |

Ties in the priority queue are broken in favour of the node closest to the goal, then by insertion order.

## Run it
**Google Colab (recommended)**
1. Upload `Progree_Task3_Pathfinding_Agent.ipynb` at colab.research.google.com
2. Runtime -> Run all
3. The last cell downloads `task3_results.zip`

**Locally**
```
pip install numpy pandas matplotlib pillow
jupyter notebook Progree_Task3_Pathfinding_Agent.ipynb
```

## Results
Expanded nodes on each 41x41 grid (start top-left, goal bottom-right):

| Grid | Path steps | Dijkstra expanded | A\* expanded | A\* saves |
|------|-----------:|------------------:|-------------:|----------:|
| Open (no obstacles) | 80 | 1681 | 81 | 95.2% |
| Random 10% | 80 | 1526 | 128 | 91.6% |
| Random 20% | 80 | 1316 | 172 | 86.9% |
| Random 30% | 80 | 1153 | 121 | 89.5% |
| Maze | 200 | 289 | 281 | 2.8% |
| Serpentine corridor | 440 | 1301 | 1249 | 4.0% |

Scalability (random grids, 20% obstacles):

| Grid size | Path steps | Dijkstra expanded | A\* expanded |
|-----------|-----------:|------------------:|-------------:|
| 20x20 | 38 | 311 | 65 |
| 40x40 | 78 | 1254 | 242 |
| 80x80 | 158 | 5059 | 476 |
| 120x120 | 238 | 11472 | 789 |
| 160x160 | 318 | 20400 | 1390 |

Runtime values are in `results/search_log.csv`. They vary slightly between machines, so rerun the notebook to get your own numbers.

## Key findings
- Both algorithms always found paths of identical length, confirming the Manhattan heuristic is admissible.
- On open and random grids, A\* expanded roughly 87-95% fewer nodes than Dijkstra because the heuristic steers the search toward the goal.
- On the maze and serpentine corridor there is essentially one route, so both algorithms explore almost the same cells and A\* gains little.
- As the grid grows, Dijkstra's expanded nodes grow much faster than A\*'s.

## Output files (`results/`)
| File | Description |
|------|-------------|
| `search_log.csv` | Steps, runtime, expanded nodes and density per grid and algorithm |
| `scalability_log.csv` | Results for the grid-size test |
| `path_*.png` | Side-by-side path images (explored area in blue, path in red) |
| `metrics_comparison.png` | Bar charts of expanded nodes, runtime and density |
| `scalability.png` | Expanded nodes and runtime versus grid size |
| `search_animation.gif` | Animated search expansion, Dijkstra vs A\* |
| `paths_log.json` | Full coordinate list of every path found |
| `summary.txt` | Text summary of all results |

## Tech stack
Python, NumPy, Pandas, Matplotlib, Pillow, Google Colab

## Author
Saheli, Final-year BCA, Meghnad Saha Institute of Technology (MSIT), Kolkata
