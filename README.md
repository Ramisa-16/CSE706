<div align="center">
```
██████╗  █████╗ ██████╗  █████╗ ██╗     ██╗     ███████╗██╗
██╔══██╗██╔══██╗██╔══██╗██╔══██╗██║     ██║     ██╔════╝██║
██████╔╝███████║██████╔╝███████║██║     ██║     █████╗  ██║
██╔═══╝ ██╔══██║██╔══██╗██╔══██║██║     ██║     ██╔══╝  ██║
██║     ██║  ██║██║  ██║██║  ██║███████╗███████╗███████╗███████╗
╚═╝     ╚═╝  ╚═╝╚═╝  ╚═╝╚═╝  ╚═╝╚══════╝╚══════╝╚══════╝╚══════╝

    
⚡ **Efficient Parallel Merge Sort using Python Multiprocessing**

![Python](https://img.shields.io/badge/Python-3.8%2B-3776AB?style=for-the-badge&logo=python&logoColor=white)
![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-F37626?style=for-the-badge&logo=jupyter&logoColor=white)
![NumPy](https://img.shields.io/badge/NumPy-Scientific-013243?style=for-the-badge&logo=numpy&logoColor=white)
![Matplotlib](https://img.shields.io/badge/Matplotlib-Visualization-11557c?style=for-the-badge)
![Course](https://img.shields.io/badge/Course-CSE706-ff6b6b?style=for-the-badge)

> *When computation time dominates coordination overhead, parallelism wins.*

---
---
📌 Table of Contents
Overview
Key Results
Algorithms
Complexity Analysis
Project Structure
Requirements
How to Run
Visualizations
Amdahl's Law
Edge Cases Tested
Key Insights
---
🔭 Overview
This project provides a rigorous experimental and theoretical comparison between Sequential Merge Sort and Parallel Merge Sort using Python's `multiprocessing` module.

It goes well beyond a simple timing test — it includes:

📐 Theoretical complexity analysis with visual growth curves

🧠 Memory profiling via `tracemalloc` (KB-level precision)

📊 6-panel professional dashboard covering time, speedup, efficiency, and more

⚖️ Amdahl's Law applied to predict scaling limits

🔢 Recursion depth & comparison count tables

🥧 Serial vs Parallel work fraction pie charts per input size

✅ 7 edge case correctness tests validated against Python's built-in `sorted()`

---
🏆 Key Results
Input Size	Sequential (s)	Parallel (s)	Speedup	Efficiency
1,000	~0.003	~0.080	~0.04x	overhead
5,000	~0.016	~0.090	~0.18x	overhead
10,000	~0.035	~0.055	~0.64x	improving
20,000	~0.076	~0.065	~1.17x	58%
40,000	~0.165	~0.110	~1.50x	75%
80,000	~0.360	~0.200	~1.80x	90%
> **Parallel outperforms sequential at n > ~20,000 elements on most machines.**
> Exact values vary by CPU core count and system load.
---
⚙️ Algorithms
Sequential Merge Sort
```python
def merge(left, right):
    result = []
    i = j = 0
    while i < len(left) and j < len(right):
        if left[i] <= right[j]:   # <= preserves stability
            result.append(left[i]); i += 1
        else:
            result.append(right[j]); j += 1
    result.extend(left[i:])
    result.extend(right[j:])
    return result

def sequential_merge_sort(arr):
    if len(arr) <= 1:
        return arr
    mid = len(arr) // 2
    return merge(sequential_merge_sort(arr[:mid]),
                 sequential_merge_sort(arr[mid:]))
```
Parallel Merge Sort
```python
def parallel_merge_sort(arr, threshold=5000):
    if len(arr) <= threshold:
        return sequential_merge_sort(arr)   # avoid spawn overhead
    mid = len(arr) // 2
    with multiprocessing.Pool(2) as pool:
        left_sorted, right_sorted = pool.map(
            sequential_merge_sort, [arr[:mid], arr[mid:]])
    return merge(left_sorted, right_sorted)
```
The `threshold=5000` parameter is a critical design decision — below this size, spawning new processes costs more than it saves.
---
📐 Complexity Analysis
Time Complexity
```
╔══════════════════════╦═══════════════╦═══════════════╦═══════════════╗
║ Algorithm            ║ Best Case     ║ Average Case  ║ Worst Case    ║
╠══════════════════════╬═══════════════╬═══════════════╬═══════════════╣
║ Sequential MergeSort ║ O(n log n)    ║ O(n log n)    ║ O(n log n)    ║
║ Parallel   MergeSort ║ O(n log n /p) ║ O(n log n /p) ║ O(n log n)    ║
╚══════════════════════╩═══════════════╩═══════════════╩═══════════════╝
  p = number of parallel workers
```
Merge Sort is one of the few sorting algorithms with a tight O(n log n) bound — it behaves the same regardless of input ordering.
Space Complexity
```
╔══════════════════════╦══════════════╦═══════════════════════════════════╗
║ Algorithm            ║ Space        ║ Notes                             ║
╠══════════════════════╬══════════════╬═══════════════════════════════════╣
║ Sequential MergeSort ║ O(n)         ║ Single auxiliary merge buffer     ║
║ Parallel   MergeSort ║ O(n × p)     ║ Each subprocess copies full data  ║
╚══════════════════════╩══════════════╩═══════════════════════════════════╝
```
Recursion Depth
Input n	Depth `⌈log₂n⌉`	Total Merges	Comparisons ≈ n log₂n
1,000	10	999	9,966
5,000	13	4,999	61,439
10,000	14	9,999	132,877
20,000	15	19,999	286,044
40,000	16	39,999	614,709
80,000	17	79,999	1,316,418
---
📁 Project Structure
```
CSE706/
│
├── 📓 CSE706_enhanced.ipynb     ← Main notebook (run this)
├── 📄 README.md                 ← This file
│
└── 📊 Generated Outputs/
    ├── complexity_theory.png    ← Time & space growth curves
    ├── memory_usage.png         ← Peak KB usage bar chart
    ├── dashboard.png            ← 6-panel analysis dashboard
    ├── comparisons.png          ← O(n log n) comparison counts
    ├── scalability.png          ← Amdahl's Law projection
    └── pie_charts.png           ← Serial vs parallel fraction
```
---
📦 Requirements
```bash
pip install numpy matplotlib pandas
```
Library	Purpose	Version
`multiprocessing`	Parallel worker pool	stdlib

`tracemalloc`	Memory profiling	stdlib

`numpy`	Numerical operations & arrays	≥ 1.21

`matplotlib`	All visualizations & plots	≥ 3.4

`pandas`	Results summary DataFrame	≥ 1.3

---
🚀 How to Run
1. Clone / Download
```bash
git clone https://github.com/your-repo/CSE706.git
cd CSE706
```
2. Install dependencies
```bash
pip install numpy matplotlib pandas
```
3. Launch Jupyter
```bash
jupyter notebook CSE706_enhanced.ipynb
```
4. Run all cells
Go to Kernel → Restart & Run All to execute everything from scratch.
> ⚠️ **Important on Windows / macOS:** Multiprocessing in Jupyter requires cells to be run inside `if __name__ == "__main__":` guards in script mode. The notebook is pre-configured to work correctly as-is.
---
📊 Visualizations
The notebook generates 6 types of charts, all saved as high-DPI PNG files:
Chart	File	What it shows
Complexity Theory	`complexity_theory.png`	O(n log n) vs O(n log n / p) growth
Memory Usage	`memory_usage.png`	Peak KB: sequential vs parallel
Analysis Dashboard	`dashboard.png`	6 panels: time · speedup · efficiency · saved · log-scale · Amdahl
Comparison Count	`comparisons.png`	n log n growth bar chart
Scalability	`scalability.png`	Projected speedup for N cores
Work Fraction	`pie_charts.png`	Serial vs parallel % per input size
---
📏 Amdahl's Law
The maximum speedup achievable with p processors is:
```
         1
S(p) = ─────────────────
        f + (1 - f) / p
```
Where f is the fraction of code that must run serially (process spawn, final merge).
This project back-calculates f from empirical results and projects:
```
Observed max speedup ≈ 1.8x  →  serial fraction f ≈ 12–15%
Theoretical max (p→∞)        →  S ≈ 6.7x  (hard ceiling)
```
This is why simply adding more cores eventually yields diminishing returns.
---
✅ Edge Cases Tested
All 7 cases verified to match Python's built-in `sorted()`:

Test Case	Sequential	Parallel	Correct?

Random list	✅	✅	✅

Already sorted	✅	✅	✅

Reverse sorted	✅	✅	✅

All same values	✅	✅	✅

Single element	✅	✅	✅

Empty list	✅	✅	✅

Two elements	✅	✅	✅

The implementation is also a stable sort — equal elements preserve their original relative order because the merge step uses `<=`.

---
💡 Key Insights
```
┌─────────────────────────────────────────────────────────────────┐
│  1. Parallel ≠ always faster                                    │
│     Small inputs (n < 5000) suffer from process-spawn overhead  │
│                                                                 │
│  2. Amdahl's Law caps the gain                                  │
│     Serial fraction ~12% → theoretical max ≈ 6.7x speedup      │
│                                                                 │
│  3. Memory trade-off is real                                    │
│     Parallel version uses ~2x RAM due to subprocess copies      │
│                                                                 │
│  4. n log n is empirically tight                                │
│     Log-scale graph confirms theoretical growth precisely        │
│                                                                 │
│  5. Threshold tuning matters                                    │
│     threshold=5000 is the crossover — adjust for your hardware  │
│                                                                 │
│  6. Stability is preserved                                      │
│     Uses <= in merge → equal elements keep their relative order │
└─────────────────────────────────────────────────────────────────┘
```
---
<div align="center">
CSE706 — Advanced Algorithms | Parallel Computing Project
Made with Python · multiprocessing · NumPy · Matplotlib · Pandas
</div>
