# PMPD
#Problem Statement
Cloud data centers (CDCs) waste significant energy because most virtual machine (VM)
scheduling algorithms optimize central processing unit (CPU) utilization while ignoring
memory, leaving physical machines (PMs) with unbalanced CPU/memory usage. This forces
more PMs to stay active than necessary, increasing energy consumption. The paper asks: how
can a scheduling algorithm jointly balance CPU and memory utilization to reduce the
number of active PMs and lower CDC energy use?

# Research Paper
Memory Priority Scheduling Algorithm for Cloud Data Center Based on Machine Learning
Dynamic Clustering Algorithm [1]

# Dataset
https://github.com/alibaba/clusterdata/blob/master/cluster-trace-v2018/fetchData.sh [2]
(real-world cloud/data-center workload and resource-usage trace data )

# Justification for Selection
It gives explicit pseudocode (Algorithm 1), worked numerical examples (Tables II–IX), and
simple formulaic metrics (Equations 1–4), making it unusually reproducible. The machine
learning (ML) component is just K-means — lightweight, fast, no graphics processing unit
(GPU) or large datasets needed. Baselines (like First-Fit) are trivial to implement, so
meaningful comparison is feasible in a course timeline.

# Core Contribution
PMPD balances CPU and memory jointly instead of separately, via two rules:
* 1. PM clustering — group PMs by CPU-to-memory utilization ratio using K-means,
updated dynamically.
* 2. VM deployment — assign each VM to the cluster whose imbalance it corrects, then
place it on the PM with closest remaining runtime to minimize wasted active time.
This reduces active PM count and light-load time, improving CPU/memory utilization and
cutting CDC energy consumption by ~14–20% versus FF, WS, task placement optimization
(TPO), and differential evolution-enhanced regional particle swarm optimization
(DE-ERPSO) in the paper's experiments.

# Project Scope
* 1. Implement the PMPD algorithm (K-means PM clustering + CPU-to-memory ratio-based
VM deployment rule) as a shared, reusable simulation core.
* 2. Synthetic experiment: Generate PMs and VMs matching the paper's parameter ranges
(Table VI, Table X), and reproduce the VM-count sweep and
minimum-utilization-threshold sweep experiments, computing the same four metrics
(light-load time, CPU utilization, memory utilization, energy consumption).
* 3. Real-data experiment: Use the Alibaba Cluster Trace v2018 (batch_instance
data), extract and clean a sample, derive PM/VM parameters from it, and run the same
PMPD core and metrics.
* 4. Implement First-Fit as a baseline and run it through both experiments for direct
comparison.
* 5. Compare synthetic results directionally and (where feasible) numerically against the
paper's reported figures; compare real-data results directionally against the same baseline.
* 6. Discuss any differences between synthetic and real-data outcomes, and what that implies
about the algorithm's robustness.
