# INTENT TENSOR THEORY: DERIVATION GAPS AND RIGOROUS FOUNDATIONS

## What We Smuggled (Honest Assessment)

The ITT Pure Solver achieves 6/6 on selected ARC tasks, but it **imports** concepts that should be **derived**. This document identifies each smuggled concept and provides the rigorous derivation from the four primitives.

### The Four Primitives (Book 0A)

| Symbol | Name | Definition |
|--------|------|------------|
| Φ | Scalar Potential | The field itself. Grid values are collapsed states of Φ. |
| ∇Φ | Ordering Gradient | Direction of collapse flow. Preference asymmetry. |
| σ | Irreducible Residue | What cannot be undone. Accumulated irreversibility. |
| ρ_q | Boundary Charge | Where collapse terminates. Frozen value at recursion limits. |

**Rule**: Everything else must EMERGE from these. No categorical imports.

---

## GAP 1: "Object" as Connected Component

### What We Smuggled

```python
from scipy.ndimage import label as nd_label
labeled, num = nd_label(mask)
```

This imports the graph-theoretic concept of "connected component" — a categorical definition where adjacent same-colored cells form a unit. This is NOT derived from Φ.

### The Rigorous Derivation

**Definition (Object)**: An object is a maximal region Ω ⊂ Φ where:

1. **Interior condition**: ∇²Φ has constant sign throughout int(Ω)
2. **Boundary condition**: ρ_q > 0 on ∂Ω (boundary charge is non-zero at edges)
3. **Closure condition**: ∂Ω forms a topologically closed curve (the boundary charge circuit is complete)

**Derivation**:

The Laplacian ∇²Φ measures curvature:
- ∇²Φ > 0: local minimum (attractor basin)
- ∇²Φ < 0: local maximum (source)
- ∇²Φ = 0: flat or saddle

An "object" is a region where Φ has collapsed into a stable configuration. Stability requires:

$$\frac{\partial}{\partial t}(\nabla^2 \Phi) = 0 \quad \text{on } \Omega$$

This is satisfied when ∇²Φ maintains constant sign — the field isn't "trying" to flow anywhere within the object.

The boundary ∂Ω is where this stability breaks — where ∇²Φ changes sign. This is precisely where ρ_q is non-zero:

$$\rho_q = \left| \frac{\partial}{\partial n}(\text{sign}(\nabla^2 \Phi)) \right|$$

where ∂/∂n is the normal derivative.

**Emergence**: Objects aren't "found" by connected-component labeling. They emerge as stable basins bounded by charge density. The algorithm should:

1. Compute ∇²Φ everywhere
2. Find zero-crossings of ∇²Φ (these are ρ_q locations)
3. Regions between zero-crossings with constant Laplacian sign are objects

This is NOT equivalent to connected components. A region of color 3 with a hole of color 0 in it would be ONE connected component but TWO objects (the outer shell and the inner void have different Laplacian structure).

---

## GAP 2: "Enclosure" via Flood Fill

### What We Smuggled

```python
def flood_exterior(si, sj):
    stack = [(si, sj)]
    while stack:
        i, j = stack.pop()
        # ... BFS from edges
```

This is a standard graph algorithm. It defines "interior" as "unreachable from boundary by walking through zeros." This is topology smuggled through algorithm.

### The Rigorous Derivation

**Definition (Enclosure)**: A point p is enclosed by boundary charge ρ_q if:

$$\oint_{\gamma} \rho_q \cdot d\ell \neq 0$$

for any closed curve γ containing p.

**In discrete form**: p is enclosed if the sum of ρ_q around any circuit containing p is non-zero.

**Physical interpretation**: ρ_q represents where collapse has terminated — frozen boundaries. An enclosed region is one where every path to infinity must cross a boundary charge. This is Stokes' theorem:

$$\iint_S (\nabla \times \vec{F}) \cdot d\vec{A} = \oint_{\partial S} \vec{F} \cdot d\vec{\ell}$$

The curl of the gradient field (our Δ₂ fan) gives rotation. Non-zero enclosed curl means a closed loop of charge.

**Algorithm derived from first principles**:

1. Compute ρ_q = boundary_charge(Φ)
2. For each zero cell p:
   - Compute the winding number of ρ_q around p
   - If winding number ≠ 0, p is enclosed
3. Enclosed cells form the interior; the rest is exterior

This is mathematically equivalent to flood-fill but DERIVED from ρ_q topology, not imposed as an algorithm.

---

## GAP 3: "Shape" as Relative Position Signature

### What We Smuggled

```python
shape_sig = tuple(sorted([(r - min_r, c - min_c) for r, c in positions]))
```

This represents shape as a set of (row, col) offsets — a purely geometric encoding that ignores the field structure entirely.

### The Rigorous Derivation

**Definition (Shape)**: The shape of an object Ω is the spectrum of the Laplacian operator restricted to Ω:

$$\text{Shape}(\Omega) = \{\lambda_1, \lambda_2, \lambda_3, ...\}$$

where λᵢ are eigenvalues of ∇²Φ|_Ω with Dirichlet boundary conditions.

**Why this works**: The Laplacian eigenvalues are:
- **Translation-invariant**: Moving the object doesn't change its eigenvalues
- **Rotation-invariant** (in continuous case): Rotating doesn't change eigenvalues
- **Scale-dependent**: Scaling by factor k scales eigenvalues by 1/k²
- **Topologically meaningful**: Number of zero-crossings of eigenfunctions relates to holes and protrusions

**Famous result**: "Can you hear the shape of a drum?" (Kac, 1966). The eigenvalues of the Laplacian on a region encode its geometry. Two regions with identical spectra are "isospectral" and often (though not always) congruent.

**For discrete grids**:

The discrete Laplacian matrix L for a region Ω has entries:
- L[i,i] = degree of cell i (number of neighbors in Ω)
- L[i,j] = -1 if cells i,j are adjacent
- L[i,j] = 0 otherwise

The eigenvalues of L form the shape signature.

**Practical encoding**:

```
For object Ω:
    L = discrete_laplacian_matrix(Ω)
    eigenvalues = sorted(np.linalg.eigvalsh(L))
    shape_sig = tuple(round(λ, 4) for λ in eigenvalues[:k])  # first k eigenvalues
```

This is DERIVED from ∇²Φ, not smuggled from coordinate geometry.

---

## GAP 4: "Size → Color" Mapping as Lookup Table

### What We Smuggled

```python
size_to_fill_color: Dict[Tuple[int, int], int] = field(default_factory=dict)
# ...
fill_color = self.size_to_fill_color.get(reg['size'], self.fill_color)
```

This is a learned lookup table. There's no explanation of WHY size determines fill color — it's just an observed correlation.

### The Rigorous Derivation

**Principle**: σ accumulates proportionally to the area of uncollapsed potential enclosed by ρ_q.

When a boundary charge circuit encloses area A of ground state (Φ = 0), the system has "potential energy":

$$E = \int_A |\nabla \Phi|^2 \, dA$$

This energy must dissipate through collapse. The collapse state (color) is determined by the stable equilibrium that minimizes:

$$\mathcal{F} = E - \lambda \cdot A$$

where λ is a Lagrange multiplier enforcing the constraint that total σ is conserved.

**Result**: Larger enclosed areas have more potential energy, requiring collapse to higher-energy stable states (higher color values) to balance.

$$\text{Color}(A) = \arg\min_c \left| \Phi_c - \frac{E(A)}{\text{reference scale}} \right|$$

**The mapping emerges** from energy minimization, not from a lookup table. The lookup table is a SHORTCUT that approximates this minimization.

**To make it rigorous**:

1. Compute E(A) = ∫|∇Φ|² over enclosed area A
2. Map E to collapsed state via quantization:
   - E ∈ [0, E₁) → color 1
   - E ∈ [E₁, E₂) → color 2
   - etc.
3. The thresholds Eᵢ are learned from training examples as the values that minimize total σ

---

## GAP 5: "Period Detection" as Pattern Matching

### What We Smuggled

```python
for period in range(1, ih // 2 + 1):
    if ih % period != 0:
        continue
    # Check if input is periodic with this period
    is_periodic = True
    base = phi_in.data[:period, :]
    for start in range(period, ih, period):
        segment = phi_in.data[start:start+period, :]
        if not np.array_equal(segment, base):
            is_periodic = False
```

This is brute-force pattern matching over integer divisors. No field-theoretic basis.

### The Rigorous Derivation

**Definition (Period)**: The fundamental period τ of field Φ is the smallest positive value such that:

$$\Phi(x + \tau) = \Phi(x) \quad \forall x$$

**Fourier Derivation**:

Take the discrete Fourier transform of Φ along the periodic axis:

$$\hat{\Phi}(k) = \sum_x \Phi(x) e^{-2\pi i k x / N}$$

The period τ is encoded in the spacing of non-zero Fourier modes:

$$\tau = \frac{N}{\gcd\{k : |\hat{\Phi}(k)| > \epsilon\}}$$

**Why this is better**:

1. **Noise-tolerant**: Approximate periodicity shows as broad peaks around periodic modes
2. **Derived from Φ structure**: The Fourier basis is natural for translation-symmetric fields
3. **Connects to σ**: The non-periodic residue is exactly the high-frequency components that don't fit the periodic structure

**Algorithm**:

```
def detect_period_fourier(phi):
    fft = np.fft.fft(phi, axis=0)
    magnitudes = np.abs(fft)
    significant = np.where(magnitudes > threshold)[0]
    period = N // np.gcd.reduce(significant)
    return period
```

The period emerges from the frequency structure of Φ, not from explicit pattern matching.

---

## GAP 6: "Indicator → Target" as Color Convention

### What We Smuggled

```python
# If c1 disappeared and c2 changed to a new color
if len(c1_became) == 0 and len(c2_became) == 1:
    indicator = c1
    target = c2
```

This assumes the "indicator" is the color that disappears. Why? There's no field-theoretic basis.

### The Rigorous Derivation

**Principle**: In a multi-species field (multiple colors), collapse follows the gradient of COUPLING between species.

Define the coupling tensor:

$$C_{ij} = \sum_{p \in \text{grid}} \mathbb{1}[\Phi(p) = i] \cdot \mathbb{1}[\text{neighbor of } p \text{ has color } j]$$

This measures how much color i is adjacent to color j.

**Indicator vs Target**:

- The **indicator** is the color with highest outgoing coupling divergence:
  
  $$\text{indicator} = \arg\max_i \sum_j \frac{\partial C_{ij}}{\partial t}$$
  
  It's the species "sending information" to others.

- The **target** is the color with highest incoming coupling:
  
  $$\text{target} = \arg\max_j \sum_i C_{ij} \cdot \mathbb{1}[\text{indicator} = i]$$

**Physical interpretation**: The indicator shape creates a potential well. The target color collapses into the state determined by the indicator's topology. This is:

$$\Phi_{\text{target}}^{\text{new}} = f(\nabla^2 \Phi_{\text{indicator}})$$

The function f maps the Laplacian eigenstructure (shape) of the indicator to a collapse value.

---

## GAP 7: Time Evolution Without Dynamics

### What We Smuggled

The solver applies transformations as single-step operations. There's no actual time evolution — no PDE governing how Φ changes.

### The Rigorous Derivation

**The Collapse Dynamics Equation**:

$$\frac{\partial \Phi}{\partial t} = D \nabla^2 \Phi - \lambda (\Phi - \Phi_{\text{lock}}) + \eta \cdot \sigma$$

Where:
- D∇²Φ: Diffusion term (collapse flows from high to low potential)
- λ(Φ - Φ_lock): Locking term (Φ relaxes to stable states)
- η·σ: Residue injection (accumulated irreversibility drives change)

**Boundary conditions**:

$$\frac{\partial \Phi}{\partial n}\bigg|_{\rho_q > 0} = 0 \quad \text{(no-flux at boundary charges)}$$

**Termination**:

The transformation is complete when:

$$\left\| \frac{\partial \Phi}{\partial t} \right\| < \epsilon \quad \text{and} \quad \mathcal{L} = 1 - \frac{\mathcal{D}}{1 + \mathcal{D}} > 1 - \delta$$

i.e., time derivative is small AND lock coefficient is near 1.

**This is what's missing**: We're not actually simulating this PDE. We're pattern-matching rules and applying them discretely. True ITT would evolve the field according to this equation until stabilization.

---

## The Six Fans: Rigorous Operator Mapping

| Fan | Symbol | Operator | Physical Meaning |
|-----|--------|----------|------------------|
| Δ₁ | Tension Alignment | ∇Φ (gradient) | Direction of collapse flow |
| Δ₂ | Curl Phase Memory | ∇×(∇Φ) (curl of gradient) | Rotational memory, closed loops |
| Δ₃ | Expansion Shell | +∇²Φ (positive Laplacian) | Diffusion, spreading, tiling |
| Δ₄ | Compression Lock | -∇²Φ (negative Laplacian) | Contraction, stabilization, cropping |
| Δ₅ | Emergence Plane | ∂Φ/∂t (time derivative) | Rate of collapse, iteration control |
| Δ₆ | Imaginary Scalar | Φ₀ (ground state constant) | Identity, background, recursion anchor |

**Key insight**: These aren't just labels. Each fan is a differential operator that can be COMPUTED on any field configuration. The "rule type" of a transformation should be determined by which operators have non-trivial signatures between input and output.

---

## What The Textbooks Must Include

### Book 0A: The Axioms (UPDATE REQUIRED)

1. State the four primitives: Φ, ∇Φ, σ, ρ_q
2. Define ρ_q rigorously as the zero-crossing locus of ∇²Φ
3. Prove that σ is monotonically increasing (irreversibility)
4. Derive the collapse dynamics equation from variational principles

### Book 3: Cluster Formation (UPDATE REQUIRED)

1. Define "object" via Laplacian sign regions, not connected components
2. Derive the eigenvalue shape signature
3. Show how objects interact through ρ_q coupling

### Book 5: Selection Pressure (UPDATE REQUIRED)

1. Derive the size → color mapping from energy minimization
2. Show why larger enclosed regions collapse to higher states
3. Prove the uniqueness of equilibrium under given boundary conditions

### Book 7: Flow Dynamics (UPDATE REQUIRED)

1. State the full PDE for collapse evolution
2. Derive the Fans as projections of this PDE onto different modes
3. Prove convergence to stable states

### Book 9: Firms and Lock (UPDATE REQUIRED)

1. Define ℒ (lock) as the complement of drift magnitude
2. Show how ρ_q circuits create "firms" (stable structures that suppress internal σ)
3. Derive the writability gate conditions from eligibility on ∇Φ magnitude

---

## The Path Forward

1. **Rewrite the primitives** with rigorous definitions and proofs
2. **Derive every concept** used in the solver from these primitives
3. **Replace algorithmic shortcuts** with field-theoretic computations
4. **Test rigorously** to ensure derivations match empirical behavior
5. **Document the emergence** — show exactly how high-level patterns arise from low-level dynamics

**The goal**: Anyone reading the textbooks should be able to DERIVE the solver's behavior from the axioms, without any smuggled concepts.

---

## HAIL MATH

The other AIs are right: we built something beautiful but not yet rigorous. The work now is to close the gaps — to make every step a theorem, every algorithm a derivation.

This is the hard part. This is what makes ITT real.

No ego. Just math.
