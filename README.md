# 4P-HTS: ML-guided Suzuki–Miyaura couplings

Training material for the 2026–27 4th-year project (4P), School of Chemistry, University of Edinburgh.

The project combines high-throughput Suzuki–Miyaura couplings of para-substituted aryl bromides and arylboronic acids with computational chemistry and machine learning. You compute electronic descriptors for the substrates, learn how yield-prediction models are built and evaluated, and use Bayesian optimisation to decide which reactions to run next in the lab.

## The notebooks

Work through them in order:

| Notebook | What you learn |
|---|---|
| `01_electronic_descriptors.ipynb` | Turn SMILES into 3D structures, run GFN2-xTB and DFT (B3LYP/def2-SVP) calculations, and extract electronic descriptors (HOMO/LUMO, charges, dipoles, conceptual-DFT/Fukui indices). Check them against Hammett σ<sub>p</sub> and export a descriptor table for your substrates. |
| `02_suzuki_yield_prediction.ipynb` | Train and *honestly evaluate* yield-prediction models on the Perera *et al.* (*Science* 2018) high-throughput Suzuki dataset: random forests with one-hot and fingerprint features, random vs out-of-sample splits, and the Chemprop neural network. |
| `03_bayesian_optimisation.ipynb` | Bayesian optimisation (BO): first from scratch on a "virtual lab", then with [BayBE](https://emdgroup.github.io/baybe/), including descriptor encodings and transfer learning. Ends with a template for your own experimental campaign. |

Cells marked **Your turn** are exercises. They are where most of the learning happens, so don't skip them.

## Setup

All three notebooks use a single conda environment, `reactml`. Create it once, from this folder:

```bash
conda env create -f environment.yml
conda activate reactml
jupyter lab            # or: jupyter notebook
```

Always start Jupyter from the activated `reactml` environment. If in doubt, check with `import sys; sys.executable` in a notebook.

> **Install everything from conda-forge**, as `environment.yml` does. Mixing pip-installed PyTorch with conda-forge PySCF/xTB loads two OpenMP libraries, which crashes on macOS.

## Data and outputs

- The Perera Suzuki dataset is downloaded automatically into `data/` the first time you run notebook 02 or 03 (from the [rxn_yields](https://github.com/rxn4chemistry/rxn_yields) repository).
- Calculated descriptors, cached DFT results and BO suggestions are written to `results/`.
- Your own experimental results go into `data/my_experiments.csv` (see notebook 03, Part 5). Record one row per reaction, including failures, and never delete rows.


## Further reading

- Bannwarth, Ehlert, Grimme, *J. Chem. Theory Comput.* **2019**, 15, 1652: GFN2-xTB.
- Perera *et al.*, *Science* **2018**, 359, 429: the high-throughput Suzuki dataset.
- Hansch, Leo, Taft, *Chem. Rev.* **1991**, 91, 165: Hammett substituent constants.
- *J. Chem. Educ.* **2015**, 92, 571–574: the Suzuki reaction matrix used in the lab.

## Contact

Antonia Mey, School of Chemistry, University of Edinburgh.
