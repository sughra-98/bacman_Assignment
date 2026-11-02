# ITML601 — Advanced AI & NLP
## Assignment 1: Search & Adversarial Search in the Pacman Environment


**Classic and adversarial search algorithms implemented, experimentally evaluated, and reported in the Berkeley Pacman framework.**

---

## 👥 Team Members

| Name | Student ID | Main Contribution |
|---|---|---|
| Sughra Hassan  | 20165579| DFS, BFS, UCS, A* (`search.py`); Table T1 experiments ,  MST `foodHeuristic`,  , Minimax ,Table T3 experiments ;| 
| Mariam Wael | 20174867 | `CornersProblem`, `cornersHeuristic` (`searchAgents.py`); Table T2 ,  α-β |
| Qabas Elayan | 20174119 | `ClosestDotSearchAgent` (`searchAgents.py`), Expectimax, evaluation function (`multiAgents.py`); Table T5 |



---

## 📁 Repository Contents

```
bacman_Assignment/
├── search/                  # Part A — Search (Berkeley Project 1)
│   ├── search.py            # Q1–Q4: DFS, BFS, UCS, A*
│   ├── searchAgents.py      # Q5–Q8: Corners, heuristics, greedy agent
│   └── ...
├── multiagent/              # Part B — Multi-Agent Search (Berkeley Project 2)
│   ├── multiAgents.py       # Q2–Q5: Minimax, α-β, Expectimax, evaluation
│   └── ...
├── report.pdf               # Scientific report: Tables T1–T5 + analysis (≤2000 words)
└── README.md
```

---

## ✅ Autograder Results

All scores obtained with `python autograder.py --no-graphics` (Berkeley CS188 autograder, sp24).

### Part A — Search

| Question | Topic | Score | Notes |
|---|---|---|---|
| Q1 | Depth-First Search | **3/3** | |
| Q2 | Breadth-First Search | **3/3** | |
| Q3 | Uniform-Cost Search | **3/3** | |
| Q4 | A* Search | **3/3** | Handles inconsistent heuristics via best-g re-expansion |
| Q5 | CornersProblem formulation | **3/3** | State = (position, visited-corner bitmask) |
| Q6 | cornersHeuristic | **3/3** | **801** expansions (A* with heuristic corners) vs **1966** (BFS) on mediumCorners |
| Q7 | foodHeuristic ⭐ | **5/4** *(extra credit)* | **410** expansions on trickySearch (top threshold: 7000; UCS ≈ 170,000) |
| Q8 | ClosestDotSearchAgent ⭐ | **3/3** | Greedy BFS-to-nearest; fast, near-optimal (cost 68 vs optimal 60) |

⭐ *Bonus questions (+5 points each max)*

### Part B — Multi-Agent Search

| Question | Topic | Score | Notes |
|---|---|---|---|
| Q1 | ReflexAgent | — | Warmup (ungraded), left as provided |
| Q2 | MinimaxAgent | **5/5** | Multi-layer, arbitrary depth |
| Q3 | AlphaBetaAgent | **5/5** | Identical values to minimax: 9, 8, 7, −492 at depths 1–4 |
| Q4 | ExpectimaxAgent | **5/5** | Chance nodes — uniform random ghosts |
| Q5 | betterEvaluationFunction | **6/6** | **10/10 wins, average score 1123.5** on smallClassic |

**Code total: 40/40 + 5 bonus (extra credit on Q7)**

---

## 🔬 Key Experimental Findings (see `report.pdf`)

| Experiment | Headline result |
|---|---|
| T1 — Uninformed vs informed | A* expands 549 nodes vs UCS's 620 on bigMaze (identical optimal cost 210) |
| T2 — Heuristic value | cornersHeuristic: 393 vs 1966 BFS expansions (−80%) at equal cost |
| T3 — α-β vs minimax | Identical root values at all depths; ~1.8× faster (0.034 s vs 0.062 s) |
| T4 — Opponent modeling | α-β (perfect adversary): 0/10 wins; Expectimax (random): 2/10 wins on trappedClassic |
| T5 — Evaluation design | 10/10 wins, avg 1123.5 with feature-weighted evaluation function |
| Bonus — Cost vs optimality | MST heuristic: optimal path 60, 410 expansions; greedy: 13% longer path, near-instant |

---

## 🚀 How to Run

### Setup
```bash
# Requires Python 3.x. Unzip each Berkeley project into its OWN folder (do not mix files).
python pacman.py            # play manually (arrow keys)
```

### Reproduce autograder scores
```bash
# Part A
cd search
python autograder.py --no-graphics

# Part B
cd multiagent
python autograder.py --no-graphics
```

### Visual demonstrations
```bash
# T1: A* vs UCS on bigMaze — watch the search contours
python pacman.py -l bigMaze -p SearchAgent -a fn=astar,heuristic=manhattanHeuristic -z .5
python pacman.py -l bigMaze -p SearchAgent -a fn=ucs -z .5

# T2: corners heuristic
python pacman.py -l mediumCorners -p AStarCornersAgent -z .5

# Bonus: MST food heuristic & greedy comparison
python pacman.py -l trickySearch -p AStarFoodSearchAgent -q
python pacman.py -l trickySearch -p ClosestDotSearchAgent -q

# T3: minimax / alpha-beta thinking on minimaxClassic
python pacman.py -p MinimaxAgent   -l minimaxClassic -a depth=3 --frameTime 1
python pacman.py -p AlphaBetaAgent -l minimaxClassic -a depth=3 --frameTime 1

# T4: opponent-modeling showdown on trappedClassic (10 games each)
python pacman.py -p AlphaBetaAgent -l trappedClassic -a depth=3 -q -n 10
python pacman.py -p ExpectimaxAgent -l trappedClassic -a depth=3 -q -n 10

# T5: graded evaluation agent
python autograder.py -q q5 --no-graphics
```

---



## 📚 References

1. S. Russell & P. Norvig, *Artificial Intelligence: A Modern Approach*, 4th ed., Pearson, 2021 (ch. 3–5).
2. UC Berkeley CS188, *Pacman Projects 1 & 2* — http://ai.berkeley.edu

---

