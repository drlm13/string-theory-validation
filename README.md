# string-theory-validation

**String theory underpinning for the zero-parameter derivation of the cosmological constant**

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Python 3.8+](https://img.shields.io/badge/python-3.8+-blue.svg)](https://www.python.org/downloads/)
[![SymPy](https://img.shields.io/badge/SymPy-1.12+-green.svg)](https://www.sympy.org/)

## Overview

This repository contains the complete symbolic verification of the **CSU (Chrono Singularity Unification)** string theory framework — the microscopic foundation for the zero-parameter derivation of the cosmological constant presented in the companion repository:

👉 [cosmological-constant-derivation](https://github.com/drlm13/cosmological-constant-derivation)

The notebook constructs the full derivation chain from first principles using **machine-verified symbolic computation** via `sympy.physics`, `sympy.tensor`, `sympy.diffgeom`, and `sympy.physics.quantum`.

## Key Results

| Result | Value | Status |
|--------|-------|--------|
| Superstring critical dimension | D = 10 | ✅ Derived |
| Bosonic string critical dimension | D = 26 | ✅ Derived |
| Ghost central charge (superstring) | c_ghost = −15 | ✅ Derived |
| Vacuum spectral weight | w_vac = 25/12 | ✅ Derived |
| Minimal state space | Z = 2 (unique) | ✅ Proved |
| Worldsheet SUSY | N = 1 (unique) | ✅ Proved |
| Fundamental extended object | p = 1 strings (unique) | ✅ Proved |
| Spectral dimension | d_S = 2 | ✅ Derived |
| Dimensional split | 4 + 6 (from topology) | ✅ Derived |
| Dark energy density parameter | Ω_Λ = 25/36 ≈ 0.6944 | ✅ Connected |

## Validation Summary

- **46/46 physics tests passed**
- **32/32 code cells execute without error**
- **4 sympy.physics modules used:**
  - `sympy.physics.units` — Quantity & Dimension objects for dimensional analysis
  - `sympy.tensor.tensor` — TensorIndexType & TensorHead for 10D Lorentz and 2D worldsheet tensor algebra
  - `sympy.diffgeom` — Manifold, Patch, CoordSystem for differential geometry on worldsheet and target space
  - `sympy.physics.quantum` — Operator, Commutator, AntiCommutator for Virasoro algebra

## Derivation Chain

The notebook verifies the following chain from string theory axioms to cosmological prediction:

```
Anomaly cancellation (c_total = 0)
    → D = 10 critical dimensions
        → N = 1 worldsheet SUSY (unique)
            → p = 1 strings (unique fundamental object)
                → Z = 2 minimal state space (unique)
                    → χ(S²) = 2 (Gauss-Bonnet topological action)
                    → c/12 = 1/12 (CFT trace anomaly)
                        → w_vac = 2 + 1/12 = 25/12
                            → Ω_Λ = w_vac²/D² = (25/12)²/10² ... = 25/36
```

Every step is symbolically verified with proper dimensional analysis.

## Quick Start

### Requirements

```bash
pip install sympy numpy
```

### Run the notebook

```bash
jupyter notebook CSU_String_Theory_Verification_FINAL.ipynb
```

Or run the standalone Python script:

```bash
python validate_string_theory_symbolic.py
```

## Repository Structure

```
string-theory-validation/
├── CSU_String_Theory_Verification_FINAL.ipynb    # Main verification notebook
├── validate_string_theory_symbolic.py            # Standalone verification script
├── sympy_physics_usage_report.md                 # Detailed report on sympy.physics usage
├── EXECUTION_REPORT.md                           # Full execution log
├── requirements.txt                              # Python dependencies
├── LICENSE                                       # MIT License
└── README.md                                     # This file
```

## Connection to Cosmological Constant Derivation

This string theory validation provides the **microscopic justification** for the three CSU postulates used in the [cosmological constant derivation](https://github.com/drlm13/cosmological-constant-derivation):

1. **Postulate A (Z = 2):** Proved as the unique minimal non-trivial state space (Section 25)
2. **Postulate B (S ≤ A/4ℓ²_P):** Derived from the Bekenstein-Hawking entropy via string microstates (Section 18)
3. **Postulate C (c = 1/12):** Derived from ζ-function regularization ζ(−1) = −1/12 and the CFT trace anomaly (Section 24)

## Sensitivity Analysis

The notebook includes a rigorous sensitivity analysis (Section 29) demonstrating that **all CSU parameters are rigidly fixed** — any perturbation to Z, c, D, or N breaks the derivation chain. This is not a tunable framework.

## Citation

If you use this work, please cite both repositories:

```bibtex
@software{csu_string_validation,
  author = {drlm13},
  title = {String Theory Validation for CSU Framework},
  url = {https://github.com/drlm13/string-theory-validation},
  year = {2025}
}

@software{csu_cosmological_constant,
  author = {drlm13},
  title = {Zero-Parameter Derivation of the Cosmological Constant},
  url = {https://github.com/drlm13/cosmological-constant-derivation},
  year = {2025}
}
```

## License

This project is licensed under the MIT License — see the [LICENSE](LICENSE) file for details.
