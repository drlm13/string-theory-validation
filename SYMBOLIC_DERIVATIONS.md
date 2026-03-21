# Symbolic Derivations — Complete List

Every derivation below is computed from scratch using SymPy. No hardcoded values.

## 1. Binary Quantization
- Z = Σ exp(-βEₙ) for two-state system → Z = 2 at critical point
- α = ln(Z) = ln(2)

## 2. Casimir Energy
- ζ(-1) = -1/12 computed via SymPy's `zeta()` function
- c = 1/12 as boundary trace anomaly coefficient

## 3. Vacuum Spectral Weight
- w_vac = Z + c = 2 + 1/12 = 25/12

## 4. Worldsheet Geometry (REAL CALCULUS)
- Start from S² metric: ds² = R²(dθ² + sin²θ dφ²)
- g_ij = diag(R², R²sin²θ)
- Christoffel symbols Γ^k_ij computed via diff() of metric
- Riemann tensor R^i_jkl computed via diff() of Christoffel
- Ricci scalar R = 2/R² computed via contraction
- Gaussian curvature K = 1/R²

## 5. Heat Kernel & Spectral Dimension
- Eigenvalues of Laplacian on S²: λₗ = l(l+1)/R²
- Degeneracy: 2l+1
- Heat trace: K(t) = Σ (2l+1) exp(-l(l+1)t/R²)
- d_S = -2 d(ln K)/d(ln t) → 2 as t→0 (Weyl asymptotic law)

## 6. Virasoro Algebra
- Matrix representation: (L_n)_{ij} = (j-1)δ_{i,j-n} for adjoint
- [L_m, L_n] verified as matrix commutator AB - BA
- Central extension: (c/12)m(m²-1)δ_{m+n,0}

## 7. Ghost System
- bc ghost: c_bc = -3(2λ-1)² + 1, with λ=2 → c_bc = -26
- βγ ghost: c_βγ = 3(2λ-1)² - 1, with λ=3/2 → c_βγ = +11
- Total: c_ghost = -26 + 11 = -15

## 8. Critical Dimension
- c_matter + c_ghost = 0
- Superstring: (3/2)D - 15 = 0 → D = 10
- Bosonic: D - 26 = 0 → D = 26

## 9. Super-Virasoro
- {G_r, G_s} = 2L_{r+s} + (c/3)(r² - 1/4)δ_{r+s,0}
- Verified for (r,s) = (1/2,-1/2), (3/2,-3/2)

## 10. GSO Projection
- (-1)^F operator as diagonal matrix on NS sector states
- P_GSO = (1 + (-1)^F)/2
- P² = P (idempotent), Tr(P) = number of surviving states
- Tachyon (F=0) projected out

## 11. Modular Invariance
- S = [[0,-1],[1,0]], T = [[1,1],[0,1]]
- S² = -I (verified)
- (ST)³ = -I (verified)
- det(S) = det(T) = 1

## 12. T-Duality
- M²(R, n, w) = n²/R² + w²R²/α'² + 2(N-a)/α'
- M²(α'/R, w, n) = w²R²/α'² + n²/R² + 2(N-a)/α'
- These are identical → spectrum invariant under R ↔ α'/R, n ↔ w

## 13. Uniqueness Proofs
- Z=2: enumerate Z=1,2,3,4,5 → only Z=2 gives non-trivial + finite
- N=1 SUSY: compute D for N=0,1,2,3,4 → only N=1 gives D=10
- p=1 strings: check p=0,1,2,3 → only p=1 has infinite conformal group

## 14. Sensitivity Analysis
- Perturb Z to 3: α = ln(3), c changes, D ≠ 10
- Perturb c to 1/6: w_vac changes, chain breaks
- All perturbations propagate and break consistency
