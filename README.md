# Incremental Graph Neural Networks for Dynamic Channel Assignment in HAN and NAN Deployments

**Published at IEEE SPERT 2025** — 2025 IEEE International Conference on Smart Power, Energy, Renewables, and Transportation (Surat, India, Dec 22–24, 2025)

📄 **Paper:** [IEEE Xplore](https://ieeexplore.ieee.org/document/11469727) | DOI: `10.1109/SPERT67079.2025.11469727` | Added to Xplore: April 14, 2026

> Conflict-free frequency allocation with minimal disruption during topology changes. On synthetic graphs (100–1000 nodes), the incremental GNN (GraphSAGE + GAT with conflict-aware training) achieves **zero interference conflicts** while reducing channel changes by **99.4% vs DSATUR (1.1 vs 185.1 avg changes per update)**.

**Author:** Pavan Parola (UNC Chapel Hill)

## What this repo is

Reproducible implementation of the SPERT paper: dynamic graph coloring for Home / Neighborhood Area Networks (HANs/NANs) in smart-grid communications.

- `DynamicGraphProcessor` for structural feature extraction
- `ConflictAwareDynamicGNN`: 2× GraphSAGE + 2-head GAT + skip-connected color head
- Conflict-aware training with adaptive penalty + greedy repair that *asserts* validity (no hard-coded zeros)
- Baselines with their own sequential state: DSATUR, Welsh-Powell, Greedy Repair, Simulated Annealing (cooling + Metropolis)
- Held-out evaluation (disjoint from training) with 70% edge-addition / 30% edge-removal updates, label-alignment so pure color permutations don't count as changes

Random-geometric graphs here are synthetic spatial proxies, not real HAN/NAN field deployments.

## Reproduce in 2 minutes

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/YaolaP4/Incremental_GNN_For_Combinatorial_Problems/blob/main/Incremental_GNN_Combinatorial_Optimization.ipynb)

```bash
pip install -r requirements.txt
# then open Incremental_GNN_Combinatorial_Optimization.ipynb and Run All
# Training: 20 epochs static pre-training + 30 epochs incremental
# Benchmark reports time_ms / conflicts / changes / colors for all 5 methods
```

Or pure Python:

```python
from dynamic_gnn import *
set_seed(42)
# see notebook for full train + benchmark_suite() flow
```

CI: GitHub Actions `smoke-test.yml` checks PyG forward/backward, conflict repair, and an end-to-end 2-round benchmark on every push to `main`.

## Files

- `dynamic_gnn.py` — model, training, repair, baselines, graph generation, evaluation
- `Incremental_GNN_Combinatorial_Optimization.ipynb` — reproducible training + held-out benchmark
- `requirements.txt` — pinned deps

## Citation

```bibtex
@inproceedings{parola2025incrementalgnn,
  title={Incremental Graph Neural Networks for Dynamic Channel Assignment in HAN and NAN Deployments},
  author={Parola, Pavan},
  booktitle={2025 IEEE International Conference on Smart Power, Energy, Renewables, and Transportation (SPERT)},
  address={Surat, India},
  year={2025},
  publisher={IEEE},
  doi={10.1109/SPERT67079.2025.11469727},
  url={https://ieeexplore.ieee.org/document/11469727}
}
```

Also see `CITATION.cff` for GitHub's Cite button.
