<h1 align="center">⚡ Parallel Algorithms — CSE706 (MSc @ BRAC University)</h1>

<p align="center">
  <img src="https://img.shields.io/badge/Python-3.10+-3776AB?style=for-the-badge&logo=python&logoColor=white"/>
  <img src="https://img.shields.io/badge/Multiprocessing-Parallel%20Computing-00b39e?style=for-the-badge"/>
  <img src="https://img.shields.io/badge/BRAC%20University-MSc%20CSE-012d35?style=for-the-badge"/>
  <img src="https://img.shields.io/badge/Grade-A%2B-success?style=for-the-badge"/>
</p>

<p align="center">
  MSc coursework on parallel algorithms — implementing <strong>Parallel Merge Sort</strong>
  using Python multiprocessing with full complexity analysis, Amdahl's Law visualization,
  and benchmarking across core counts.
</p>

---

## 📚 Course Info

- **Course:** CSE706 — Parallel Algorithms
- **Program:** MSc in Computer Science & Engineering
- **University:** BRAC University
- **Grade:** A+ (97–100) → CGPA 4.00

---

## 🔬 Project: Parallel Merge Sort

### Key Concepts Implemented

| Concept | Description |
|---|---|
| **Parallel Merge Sort** | Divide array across CPU cores, merge results |
| **Python multiprocessing** | True parallelism using multiple processes |
| **Amdahl's Law** | Theoretical speedup limit visualization |
| **Memory Profiling** | RAM usage analysis across configurations |
| **Benchmarking** | Execution time vs core count comparison |

---

## 🏗️ Algorithm Flow

```
Input Array (n elements)
      │
      ▼
Split into p chunks (p = number of cores)
      │
      ▼
Each process sorts its chunk independently
(multiprocessing.Pool)
      │
      ▼
Merge sorted chunks back together
      │
      ▼
Benchmarking: time vs cores, memory usage
      │
      ▼
Amdahl's Law plot: theoretical vs actual speedup
```

---

## 📊 Analysis Performed

- **Time complexity** — O(n log n / p) parallel, O(n log n) sequential
- **Speedup analysis** — actual vs theoretical (Amdahl's Law)
- **Core scaling** — 1, 2, 4, 8 cores benchmarked
- **Memory profiling** — overhead per process measured
- **Efficiency** — speedup / number of cores

---

## 🚀 Getting Started

```bash
git clone https://github.com/Ramisa-16/CSE706.git
cd CSE706
pip install -r requirements.txt
jupyter notebook
```

---

## 🛠️ Tech Stack

**Python** · **multiprocessing** · **time** · **memory_profiler** · **Matplotlib** · **NumPy**

---

## 👩‍💻 Author

**Ramisa Sharar Nidhi** — MSc CSE @ BRAC University (CGPA 4.00/4.00)
[![LinkedIn](https://img.shields.io/badge/LinkedIn-ramisashararnidhi-0077B5?style=flat&logo=linkedin)](https://linkedin.com/in/ramisashararnidhi)
[![GitHub](https://img.shields.io/badge/GitHub-Ramisa--16-181717?style=flat&logo=github)](https://github.com/Ramisa-16)
