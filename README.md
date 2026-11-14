# Computational biophysics coursework

Simulation assignments from the course **Molecular Biophysics**, MSc in Quantitative Biology, University of Milan (March–May 2026).

**Author:** Pouria Johari

These are course assignments, not research projects. The questions and the helper modules (`diffusion_box.py`, `libplot_diff.py`, `PolymerFun.py`, `PolymerFun2.py`, and the `drawseq` function) were written by the course instructors, [John Nava]. The analysis in the notebooks and the written answers are mine.

## Contents

| Folder | Notebook | Topic |
|---|---|---|
| `01_lattice_diffusion` | `lattice_diffusion.ipynb` | Random walks on 2D and 3D lattices, mean square displacement |
| `02_dna_thermodynamics` | `dna_thermodynamics.ipynb` | Folding and hybridisation free energies of DNA strands with NUPACK |
| `03_diffusion_in_a_box` | `diffusion_in_a_box.ipynb` | Many particles in a closed box and in an open "infinite pool": equilibrium and steady state |
| `03_diffusion_in_a_box` | `diffusion_with_receptors.ipynb` | The same box with binding sites: receptor occupancy and affinity |
| `04_polymers` | `polymer_conformations.ipynb` | Ideal, self-avoiding and worm-like chains: radius of gyration, density, persistence length |
| `04_polymers` | `polymer_dynamics.ipynb` | Diffusion of a chain, confinement, relaxation from a stretched state |

## Main results and limits

**1. Lattice diffusion.** The mean square displacement grows linearly with the number of steps, with a slope close to 1 in both 2D and 3D, which gives D ≈ 1/4 and D ≈ 1/6 in lattice units.

**2. DNA thermodynamics.** The folding free energy becomes more negative with strand length, and a 20-nt strand binds its perfect complement far more strongly (about -35 kcal/mol) than any of 200 random sequences (best about -17 kcal/mol). *Limit:* the duplex is so stable that the binding fraction is 1 at every concentration tested, so the concentration dependence is not visible.

**3a. Diffusion in a box.** In a closed box the density profile becomes flat (equilibrium); in an open box the system goes towards a steady state with a constant flow of particles. *Limit:* the threshold I used to measure equilibration times was too coarse, so the dependence on particle number and box size is read from the curves and not from the measured times. The open box had not yet reached its steady state at the end of the run.

**3b. Receptors.** Receptor occupancy increases with the number of particles like a simple binding curve. With equal binding and unbinding probabilities the occupancy is 17% for 2000 particles, which agrees with a simple estimate based on how often a lattice site holds a particle. *Limit:* the occupancy reached only 43% in the range simulated, so the number of particles for 50% occupancy (about 10,000) is an extrapolation.

**4a. Polymer conformations.** Ideal chains follow Rg ~ L^0.5. Self-avoiding chains are larger and have a higher exponent, but below the theoretical value (0.67 against 0.75 in 2D, 0.53 against 0.588 in 3D), probably because the chains are short. The persistence length of the worm-like chain grows with the stiffness parameter, from below 1 bond to about 18 bonds.

**4b. Polymer dynamics.** At short lag times a longer chain diffuses more slowly, roughly like 1/L. A tube narrower than the chain restricts its motion to the tube axis and makes it more compact. A stretched chain relaxes back to a coil, and more slowly when it is stiffer. *Limit:* each condition is a single run of 1000 steps, so the MSD at long times and the fitted diffusion exponents are too noisy to compare.

## How to run

```
pip install numpy scipy matplotlib tqdm jupyterlab
jupyter lab
```

- Notebooks 3 and 4 import the course helper modules, which must be in the same folder as the notebook. They belong to the course and are not included in this repository.
- The DNA notebook needs [NUPACK](https://www.nupack.org) (installed separately, see its documentation) and `pip install draw_rna`.
- `lattice_diffusion.ipynb` and `polymer_dynamics.ipynb` use a fixed random seed, so running them again gives the numbers quoted in the text. The other simulation notebooks do not, so a new run gives slightly different numbers.
