# Hydrogent

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Python 3.11+](https://img.shields.io/badge/python-3.11+-blue.svg)](https://www.python.org/downloads/)

Code and data accompanying the paper:

> **Descriptor-guided thermodynamic screening of H₂ adsorption on single-atom-doped anatase TiO₂ nanoparticles using interpretable machine learning**
>
> Mustafa Kurban¹², Can Polat³, Erchin Serpedin³, Hasan Kurban⁴
>
> ¹ Department of Prosthetics and Orthotics, Ankara University, Ankara, Turkey
> ² Department of Electrical and Computer Engineering, Texas A&M University at Qatar, Doha, Qatar
> ³ Department of Electrical and Computer Engineering, Texas A&M University, College Station, TX, USA
> ⁴ College of Science and Engineering, Hamad Bin Khalifa University, Doha, Qatar
>
> Correspondence: kurbanm@ankara.edu.tr (M. Kurban), hkurban@hbku.edu.qa (H. Kurban)

## Abstract

Understanding how surface dopants tune H₂ adsorption on oxide nanoparticles is important for the rational design of reversible hydrogen-storage materials and catalytic interfaces. Here, we present a descriptor-guided screening study of molecular H₂ adsorption on pristine and single-atom-doped anatase TiO₂ nanoparticles using density-functional tight-binding (DFTB) calculations, conceptual DFT descriptors, thermodynamic modelling, and interpretable machine learning with active learning. In the doped models, one surface Ti atom is substitutionally replaced by a dopant species (X = Al, Fe, Hf, La, Mo, Nb, Sn, V, W, and Zr), enabling systematic comparison across chemically distinct surface environments. Most dopants preserve molecular adsorption, whereas Fe shows incipient dissociative activation marked by pronounced H–H bond elongation. The computed adsorption energies span more than 0.25 eV, from weakly bound Fe to strongly bound Mo, demonstrating that single-atom doping provides an effective handle for tuning adsorption strength across a regime relevant to reversible H₂ storage. Descriptor analysis reveals a clear electronic partitioning between wide-gap dopants that largely preserve the insulating character of pristine TiO₂ and narrow-gap dopants that introduce dopant-derived frontier states while enhancing electrophilicity and softness. Symbolic regression identifies the electrophilicity index ω as the primary descriptor associated with adsorption strength, with the HOMO–LUMO gap, electron affinity, and LUMO energy contributing through nonlinear coupling. Greedy maximum-uncertainty active learning rapidly improves surrogate performance and supports screening-level classification after only a few additional DFTB evaluations. Thermodynamic analysis and decision-oriented storage classification show that Nb and Zr provide the most balanced combination of room-temperature uptake and release within the DOE-relevant operating window, Sn remains a borderline but thermodynamically viable case, and Hf and Mo define a stronger-binding regime with higher retention but less balanced release. Forward screening of previously untested dopants (Rh, Sc, and Ta), together with follow-up DFTB calculations, further supports the screening-level utility of the surrogate under limited-data conditions. Overall, this work provides a data-efficient and physically interpretable route for screening dopant chemistry in oxide nanomaterials for hydrogen-storage applications.

**Keywords:** H₂ adsorption · Anatase TiO₂ nanoparticles · Single-atom doping · Thermodynamic screening · Interpretable machine learning

## Architecture

```
Python Library (3.11+)
  ├── thermo_tools  — Langmuir isotherm, van't Hoff, T50
  └── ml_tools      — GP, symbolic regression, active learning
```

## Features

- **Interpretable ML** — Symbolic regression (PySR) discovers human-readable formulas; Gaussian Process provides uncertainty-quantified predictions
- **Active learning** — Suggests most informative next experiment via maximum GP uncertainty
- **Thermodynamic screening** — Langmuir isotherm, van't Hoff analysis, T50 desorption midpoint, DOE window compliance

## Quick Start

```bash
pip install -r requirements.txt
```

## Data

The `data/` directory contains DFT-computed descriptors and XYZ geometries for 10 doped TiO₂ nanoparticles (Al, Fe, Hf, La, Mo, Nb, Sn, V, W, Zr) plus pristine TiO₂, each with and without adsorbed H₂. The `labels.csv` includes 102 descriptors per system covering electronic structure, CDFT reactivity indices, structural metrics, and thermodynamic properties.

## ML Capabilities

| Method | Purpose | Best For |
|--------|---------|----------|
| Symbolic Regression | Discover E_ads = f(descriptors) | Interpretable relationships |
| Gaussian Process | Predict E_ads with uncertainty | Small datasets (n < 20) |
| Active Learning | Rank untested dopants | Experiment planning |
| Feature Importance | Identify key descriptors | Understanding what drives adsorption |

## Tech Stack

- **Core**: Python, pandas, NumPy, SciPy
- **ML**: scikit-learn, PySR
- **Data**: DFT-computed descriptors, XYZ geometries

## Testing

```bash
pytest src/tests/ -v
```

## License

MIT
