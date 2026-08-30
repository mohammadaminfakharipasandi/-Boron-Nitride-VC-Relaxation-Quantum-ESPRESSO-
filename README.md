# Ionic + Variable-Cell Relaxation of a Boron Nitride Structure (Quantum ESPRESSO)

A DFT structural relaxation (`vc-relax`) of a tetragonal, 6-atom boron nitride (B₃N₃) cell, performed with [Quantum ESPRESSO](https://www.quantum-espresso.org) (PWSCF). Both atomic positions and the cell shape are optimized simultaneously via BFGS.

## Calculation details

| Parameter | Value |
|---|---|
| Code | Quantum ESPRESSO (PWSCF) v7.5 |
| Calculation | `vc-relax` (ionic + variable-cell relaxation) |
| Bravais lattice | `ibrav = 6`, tetragonal (P4/mmm), A = 2.63 Å, C = 6.10 Å |
| Atoms | 6 (3 × B, 3 × N) |
| Exchange–correlation | LDA (Perdew–Zunger) |
| Pseudopotentials | `B.pz-n-kjpaw_psl.0.1.UPF` (PAW), `N.pz-n-rrkjus_psl.0.1.UPF` (ultrasoft) |
| Plane-wave cutoffs | `ecutwfc` = 65 Ry, `ecutrho` = 260 Ry |
| k-point mesh | 8 × 8 × 8 Monkhorst–Pack (shifted) |
| Smearing | Gaussian, `degauss` = 0.02 Ry |
| SCF threshold | `conv_thr` = 1×10⁻⁹ Ry |
| Cell relaxation | `cell_dynamics = 'bfgs'`, `cell_dofree = 'y'` (only the *b* lattice vector is free) |

> The full list of settings is in [`Sample-1_pw.in`](Sample-1_pw.in).

## Results

Geometry optimization converged in **3 BFGS steps (4 SCF cycles)**.

| BFGS step | Total energy (Ry) | Total force (Ry/bohr) | Pressure (kbar) |
|---|---|---|---|
| 0 (initial) | −93.91503004 | 0.024931 | −79.41 |
| 1 | −93.91620919 | 0.014533 | −51.32 |
| 2 | −93.91625156 | 0.010146 | −45.59 |
| 3 (converged) | −93.91628039 | 0.001382 | −49.34 |
| Final fixed-cell SCF | −93.91623187 | 0.001386 | −49.48 |

**Final relaxed cell** (orthogonal axes): a = 2.6300 Å, b = 2.5966 Å (≈1.3% contraction from the initial 2.6300 Å), c = 6.0999 Å (unchanged) — final density 2.967 g/cm³.

![Energy and force convergence](results/convergence_plot.png)

Full relaxation log: [`Sample-1_pw.out`](Sample-1_pw.out). Final atomic coordinates as a standalone structure file: [`results/Sample-1_relaxed.xyz`](results/Sample-1_relaxed.xyz).

## Repository contents

```
├── Sample-1_pw.in                 QE input file
├── Sample-1_pw.out                Full QE output log
├── results/
│   ├── convergence_plot.png       Energy / force vs. BFGS step
│   └── Sample-1_relaxed.xyz       Final relaxed structure (XYZ)
├── LICENSE
└── README.md
```

## Reproducing this calculation

Requires a working Quantum ESPRESSO installation (tested with v7.5) and the two pseudopotential files referenced above (e.g. from [pseudopotentials.quantum-espresso.org](https://pseudopotentials.quantum-espresso.org)).

```bash
pw.x -in Sample-1_pw.in > Sample-1_pw.out
```

## Citing Quantum ESPRESSO

If you reuse this workflow, please also cite Quantum ESPRESSO itself, per its [citation policy](https://www.quantum-espresso.org/quote):

> P. Giannozzi et al., J. Phys.: Condens. Matter 21, 395502 (2009); J. Phys.: Condens. Matter 29, 465901 (2017); J. Chem. Phys. 152, 154105 (2020).

## How to cite this 
Mohammadamin Fakharipasandi, "Ionic + Variable-Cell Relaxation of a Boron Nitride Structure (Quantum ESPRESSO)", GitHub repository, 2026.


## License

This repository is licensed under a **Creative Commons Attribution 4.0 International License (CC BY 4.0)** — see [LICENSE](LICENSE) for the full text and attribution terms. Quantum ESPRESSO itself is separate, GPL-licensed software and is not redistributed here.

## Notes

* This is a personal project, written without any AI assistance, so it might contain some mistakes or issues. 
Feel free to reach out if you run into any problems. [aminfakharipasandi@gmail.com](mailto:aminfakharipasandi@gmail.com)
