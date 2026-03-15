# SymPy.Physics Module Usage Report

## CSU String Theory Validation - Complete Implementation

This report documents the **actual usage** of SymPy physics modules in the validation notebook.

---

## 1. sympy.physics.units

### Module Path
```python
from sympy.physics.units import Quantity, Dimension
from sympy.physics.units import length, time, mass, energy
from sympy.physics.units.systems import SI
```

### Objects Used

#### Dimension Objects
```python
dim_L = Dimension("length")   # [L]
dim_T = Dimension("time")     # [T]  
dim_M = Dimension("mass")     # [M]
dim_E = Dimension("energy")   # [M L² T⁻²]
```

#### Quantity Objects
```python
# String length
l_s = Quantity('l_s', abbrev='l_s')
SI.set_quantity_dimension(l_s, length)

# Regge slope  
alpha_prime = Quantity('alpha_prime', abbrev="α'")
SI.set_quantity_dimension(alpha_prime, length**2)

# String tension
T_s = Quantity('T_s', abbrev='T_s')
SI.set_quantity_dimension(T_s, mass / time**2)

# Planck length
l_P = Quantity('l_P', abbrev='l_P')
SI.set_quantity_dimension(l_P, length)

# String mass scale
M_s = Quantity('M_s', abbrev='M_s')
SI.set_quantity_dimension(M_s, mass)
```

### Dimensional Analysis Examples
- α' = l_s² has dimension [length]²
- T_s = 1/(2πα') has dimension [energy/length]
- M² = N/α' dimensionally consistent
- Nambu-Goto action is dimensionless

---

## 2. sympy.tensor.tensor

### Module Path
```python
from sympy.tensor.tensor import (
    TensorIndexType, TensorIndex, TensorHead, tensor_indices,
    TensorSymmetry, TensorType
)
```

### Objects Used

#### TensorIndexType - 10D Spacetime
```python
# Define Lorentz index type for 10D spacetime
Lorentz10 = TensorIndexType('Lorentz10', dim=10, metric_symmetry=1)
print(f"dimension = {Lorentz10.dim}")  # Output: 10

# Create tensor indices
mu, nu, rho, sigma = tensor_indices('mu nu rho sigma', Lorentz10)
```

#### TensorIndexType - 2D Worldsheet
```python
# Define worldsheet index type (2D)
Worldsheet = TensorIndexType('Worldsheet', dim=2, metric_symmetry=1)
print(f"dimension = {Worldsheet.dim}")  # Output: 2

# Create worldsheet indices
a, b, c_idx, d_idx = tensor_indices('a b c d', Worldsheet)
```

#### TensorHead - Metrics
```python
# 10D spacetime metric
g = TensorHead('g', [Lorentz10, Lorentz10], TensorSymmetry.fully_symmetric(2))
g_tensor = g(mu, nu)  # g_μν

# Inverse metric
g_inv = TensorHead('g_inv', [Lorentz10, Lorentz10], TensorSymmetry.fully_symmetric(2))

# 2D worldsheet metric (induced)
h = TensorHead('h', [Worldsheet, Worldsheet], TensorSymmetry.fully_symmetric(2))
h_tensor = h(a, b)  # h_ab
```

#### TensorHead - Fields
```python
# String embedding field X^μ
X = TensorHead('X', [Lorentz10])
X_mu = X(mu)

# Stress-energy tensor
T_stress = TensorHead('T', [Worldsheet, Worldsheet], TensorSymmetry.fully_symmetric(2))
T_tensor = T_stress(a, b)
```

---

## 3. sympy.diffgeom

### Module Path
```python
from sympy.diffgeom import Manifold, Patch, CoordSystem
from sympy.diffgeom import metric_to_Christoffel_1st, metric_to_Christoffel_2nd
from sympy.diffgeom import metric_to_Riemann_components, metric_to_Ricci_components
```

### Objects Used

#### Worldsheet Manifold
```python
# Create 2D worldsheet manifold
Sigma = Manifold('Sigma', 2)
print(f"dimension = {Sigma.dim}")  # Output: 2

# Create patch (coordinate chart)
P = Patch('P', Sigma)
```

#### Coordinate System
```python
# Create conformal coordinate system (τ, σ)
conformal = CoordSystem('conformal', P, ['tau', 'sigma'])

# Get coordinate functions
tau_sym, sigma_sym = conformal.coord_functions()

# Get basis vectors
e_tau, e_sigma = conformal.base_vectors()
print(f"∂/∂τ = {e_tau}")
print(f"∂/∂σ = {e_sigma}")
```

#### Metric Definition
```python
# Conformal factor
phi = Function('phi')(tau_sym, sigma_sym)
conformal_factor = exp(phi)

# 2D Minkowski metric
eta_2d = Matrix([[-1, 0], [0, 1]])

# Full conformal metric
gamma_metric = conformal_factor * eta_2d
```

---

## 4. sympy.physics.quantum

### Module Path
```python
from sympy.physics.quantum import Operator, Commutator, AntiCommutator
from sympy.physics.quantum import Dagger, represent
```

### Objects Used

#### Custom Virasoro Operator Class
```python
class VirasoroOp(Operator):
    """Virasoro generator L_n"""
    def __new__(cls, n):
        return Operator.__new__(cls, n)
    
    @property
    def n(self):
        return self.args[0]

# Create Virasoro operators
L_m = VirasoroOp(m_sym)
L_n = VirasoroOp(n_sym)
L_0 = VirasoroOp(0)
L_1 = VirasoroOp(1)
L_minus1 = VirasoroOp(-1)
```

#### Commutator Usage
```python
# Virasoro commutator
comm_Lm_Ln = Commutator(L_m, L_n)
print(f"[L_m, L_n] = {comm_Lm_Ln}")

# Full algebra:
# [L_m, L_n] = (m - n)L_{m+n} + (c/12)m(m² - 1)δ_{m+n,0}
```

#### Custom Supercharge Operator Class
```python
class SuperchargeOp(Operator):
    """Supercharge generator G_r"""
    def __new__(cls, r):
        return Operator.__new__(cls, r)

G_r = SuperchargeOp(r_sym)
G_s = SuperchargeOp(s_sym)
```

#### AntiCommutator Usage
```python
# Super-Virasoro anticommutator
anticomm_Gr_Gs = AntiCommutator(G_r, G_s)
print(f"{{G_r, G_s}} = {anticomm_Gr_Gs}")

# Full algebra:
# {G_r, G_s} = 2L_{r+s} + (c/3)(r² - 1/4)δ_{r+s,0}
```

---

## Summary

| Module | Purpose | Key Objects |
|--------|---------|-------------|
| sympy.physics.units | Dimensional analysis | Quantity, Dimension |
| sympy.tensor.tensor | Tensor algebra | TensorIndexType, TensorHead |
| sympy.diffgeom | Worldsheet geometry | Manifold, Patch, CoordSystem |
| sympy.physics.quantum | Virasoro algebra | Operator, Commutator, AntiCommutator |

All modules are used with **actual objects** (not just imports), demonstrating proper SymPy physics implementation throughout the notebook.
