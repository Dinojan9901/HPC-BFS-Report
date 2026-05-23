# HPC BFS Project Report

This repository contains the project report and documentation for the project **"Parallel Implementation of Breadth-First Search (BFS) Using Shared and Distributed Memory Models"** as part of the **EC7207 / EE7218 High Performance Computing** course at the Department of Electrical and Information Engineering, University of Ruhuna.

## Repository Contents

*   **[progress_report.pdf](progress_report.pdf)** - The compiled 15-page final evaluation report (PDF).
*   **[progress_report.tex](progress_report.tex)** - The LaTeX source code of the report.
*   **[G16_HPC_Project_Proposal (2).pdf](G16_HPC_Project_Proposal%20%282%29.pdf)** - The initial project proposal.
*   **[Project Guideline.pdf](Project%20Guideline.pdf)** - The course guidelines and requirements.

---

## Project Overview

Breadth-First Search (BFS) is a fundamental but memory-bound graph traversal algorithm with a time complexity of $O(V + E)$. This project implements and evaluates parallel versions of BFS using three modern high-performance computing paradigms:
1.  **OpenMP (Shared Memory):** Uses a level-synchronous approach parallelized with atomic Compare-and-Swap (CAS) instructions and thread-local buffering to avoid queue lock contention.
2.  **MPI (Distributed Memory):** Implements a 1D vertex block partitioning scheme with active frontier updates synchronized globally using collective `MPI_Allgather` and `MPI_Allgatherv` operations.
3.  **CUDA (GPU Acceleration):** Flat adjacency lists mapped to Compressed Sparse Row (CSR) format with level-synchronous thread grids executing on the GPU.

---

## Key Results & Findings

*   **Correctness:** All parallel implementations achieve perfect agreement with the sequential BFS baseline.
*   **Crossover Point:** Due to thread synchronization, thread creation, and message-passing latencies, parallel CPU implementations experience overhead on small graphs ($V \le 10,000$). Scaling and speedups are observed only on larger graph sizes ($V \ge 100,000$).
*   **Amdahl's Law Analysis:** Evaluating the OpenMP scaling behavior on massive workloads shows that BFS has a parallel fraction of $p \approx 89.4\%$. The remaining sequential portion (master queue management, level boundaries) caps the maximum theoretical speedup limit on CPUs to $9.43\text{x}$.

---

## Group 16 Members
*   **Member 1:** Serial Baseline & Visualizer
*   **Member 2:** OpenMP Parallel BFS & MPI
*   **Member 3:** OpenMP Parallel BFS & CUDA
