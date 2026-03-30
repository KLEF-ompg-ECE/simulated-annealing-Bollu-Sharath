# Assignment 1 — Simulated Annealing: Exam Timetable Scheduling
## Observation Report

**Student Name  :** B.sharath  
**Student ID    :** 2310040022  
**Date Submitted:** 30/03/2026  

---

## How to Submit

1. Run each experiment following the instructions below
2. Fill in every answer box — do not leave placeholders
3. Make sure the `plots/` folder contains all required images
4. Commit this README and the `plots/` folder to your GitHub repo

---

## Before You Begin — Read the Code

Open `sa_timetable.py` and read through it. Then answer these questions.

**Q1. What does `count_clashes()` measure? What value means a perfect timetable?**

```
[ The count_clashes() function measures the total number of scheduling conflicts where a student has two exams in the same time slot. It checks each student’s exam list and counts how many overlaps occur.

A value of 0 means a perfect timetable, as there are no clashes and every student’s exams are scheduled in different slots. ]
```

**Q2. What does `generate_neighbor()` do? How is the new timetable different from the current one?**

```
[ The generate_neighbor() function creates a new timetable by randomly selecting one exam and assigning it to a different time slot. This introduces a small change to the current solution.

The new timetable differs from the current one by only one exam’s slot, allowing the algorithm to explore nearby solutions step by step. ]
```

**Q3. In `run_sa()`, there is this line:**
```python
if delta < 0 or random.random() < math.exp(-delta / T):
```
**What does this line decide? Why does SA sometimes accept a worse solution?**

```
[ This line decides whether the new timetable should be accepted. If the new solution has fewer clashes (delta < 0), it is always accepted; otherwise, it may still be accepted with a probability based on temperature.

Simulated Annealing accepts worse solutions to escape local optima and explore more of the search space, especially when the temperature is high. ]
```

---

## Experiment 1 — Baseline Run

**Instructions:** Run the program without changing anything.
```bash
python sa_timetable.py
```

**Fill in this table:**

| Metric | Your result |
|--------|-------------|
| Number of iterations completed |1379|
| Clashes at iteration 1 |12|
| Final best clashes |3|
| Did SA reach 0 clashes? (Yes / No) |No|

**Copy the printed timetable output here:**
```
[ Slot 1:  Geography
  Slot 2:  Chemistry, English
  Slot 3:  History, Computer Science, Economics
  Slot 4:  Biology, Statistics
  Slot 5:  Mathematics, Physics ]
```

**Look at `plots/experiment_1.png` and describe what you see (2–3 sentences).**  
*Where does the biggest drop in clashes happen? Does the curve flatten out?*
```
[ The plot shows a sharp drop in the number of clashes during the early iterations, especially from around 12 down to 6 within the first 100 iterations. After this, the improvement becomes slower and more gradual.

The curve eventually flattens out around 3–4 clashes, indicating that the algorithm is converging and struggling to find a perfect (zero-clash) solution. ]
```

---

## Experiment 2 — Effect of Cooling Rate

**Instructions:** In `sa_timetable.py`, find the `# EXPERIMENT 2` block in `__main__`.  
Copy it three times and run with `cooling_rate` = **0.80**, **0.95**, and **0.995**.  
Save plots as `experiment_2a.png`, `experiment_2b.png`, `experiment_2c.png`.

**Results table:**

| cooling_rate | Final clashes | Iterations completed | Reached 0 clashes? |
|-------------|---------------|----------------------|--------------------|
| 0.80        | 8             | ~30                  | No                 |
| 0.95        | 3             | ~300                 | No                 |
| 0.995       | 3             | ~1400                | No                 |

**Compare the three plots. What do you notice about how fast vs slow cooling affects the result? (3–4 sentences)**  
*Hint: Fast cooling = temperature drops quickly. Does it have time to explore well?*
```
[ Fast cooling (cooling_rate = 0.80) causes the temperature to drop very quickly, which freezes the algorithm early and prevents it from exploring enough solutions, resulting in a poor final outcome. With a moderate cooling rate (0.95), the algorithm has more time to explore and finds a significantly better solution.

Slow cooling (0.995) allows even more thorough exploration, giving the algorithm enough time to escape local minima and gradually improve. This shows that slower cooling generally leads to better solution quality, while fast cooling leads to worse results. ]
```

**Which cooling_rate gave the best result? Why do you think that is?**
```
[ The cooling_rate = 0.95 and 0.995 both gave the best result (final clashes = 3). However, 0.995 is generally better because it allows slower cooling and more thorough exploration of the solution space.

Although 0.95 reaches a good solution faster, 0.995 is more reliable for finding optimal or near-optimal solutions. ]
```

---

## Summary

**Complete this table with your best result from each experiment:**

| Experiment | Key setting | Final clashes | Main finding in one sentence |
|------------|-------------|---------------|------------------------------|
| 1 — Baseline | cooling_rate = 0.995 | 3 | Slow cooling allows steady improvement but takes more time |
| 2 — Cooling rate | cooling_rate = 0.995 | 3 | Slower cooling improves solution quality through better exploration |

**In your own words — what is the most important thing you learned about Simulated Annealing from these experiments? (3–5 sentences)**
```
[ The most important thing I learned is that the cooling schedule in Simulated Annealing has a major impact on performance. If the temperature decreases too quickly, the algorithm stops exploring early and gets stuck in poor solutions.

Slower cooling allows the algorithm to explore more of the solution space and escape local minima, leading to better results. However, it also requires more iterations and computational time. Overall, balancing exploration and convergence is key to making Simulated Annealing effective. ]
```

---

## Submission Checklist

- [done] Student name and ID filled in
- [done] Q1, Q2, Q3 answered
- [done] Experiment 1: table filled, timetable pasted, plot observation written
- [done] Experiment 2: results table filled (3 rows), observation and answer written
- [done] Summary table completed and reflection written
- [done] `plots/` contains: `experiment_1.png`, `experiment_2a.png`, `experiment_2b.png`, `experiment_2c.png`
