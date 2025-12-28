# EXECUTABLE PHYSICS: BOOK 0A SUPPLEMENT
# RIGOROUS FOUNDATIONS FOR DISCRETE FIELD DYNAMICS

## Preface: The Derivation Requirement

Every concept used in applications (ARC solver, business mechanics, etc.) must trace back to the axioms through explicit derivation. This document provides those derivations.

**Convention**: We work on discrete grids Ω ⊂ ℤ² for computational tractability, but state continuous analogues where illuminating.

---

# CHAPTER 1: THE FOUR PRIMITIVES

## §1.1 The Scalar Potential Φ

**Axiom 1.1** (Existence of Φ): There exists a scalar function Φ: Ω → ℝ≥0 assigning to each point p ∈ Ω a non-negative real value called the *collapse potential* at p.

**Definition 1.1** (Ground State): The ground state is Φ = 0. Points where Φ(p) = 0 are *uncollapsed* or *latent*.

**Definition 1.2** (Collapsed State): Points where Φ(p) > 0 are *collapsed*. In discrete systems with quantized states {0, 1, ..., 9}, we interpret Φ(p) = c as "collapsed to state c."

**Interpretation**: Φ is not a representation of a grid — Φ IS the grid. The grid values are measurements of collapsed potential at each location.

## §1.2 The Ordering Gradient ∇Φ

**Axiom 1.2** (Gradient Existence): For any differentiable Φ, there exists a vector field ∇Φ giving the direction of steepest ascent.

**Definition 1.3** (Discrete Gradient): On Ω ⊂ ℤ², define:

$$(\nabla \Phi)_x(i,j) = \Phi(i, j+1) - \Phi(i, j)$$
$$(\nabla \Phi)_y(i,j) = \Phi(i+1, j) - \Phi(i, j)$$

with boundary handling by zero-extension.

**Interpretation**: ∇Φ encodes *preference asymmetry* — the direction collapse "wants" to flow. Regions of high |∇Φ| are unstable; collapse is imminent.

## §1.3 The Irreducible Residue σ

**Axiom 1.3** (Residue Accumulation): For any transformation T: Φ → Φ', there exists a non-negative field σ[T] such that:

$$\sigma[T](p) = |Φ'(p) - Φ(p)| \cdot w(p, Φ, Φ')$$

where w is a weight function encoding "structural importance."

**Axiom 1.4** (Irreversibility): For transformations T₁, T₂:

$$\sigma[T_2 \circ T_1] \geq \sigma[T_1]$$

Residue never decreases. Transformations accumulate irreversibility.

**Definition 1.4** (Simple Residue): Taking w ≡ 1:

$$\sigma[T](p) = |Φ'(p) - Φ(p)|$$

**Definition 1.5** (Total Residue):

$$\Sigma[T] = \sum_{p \in \Omega} \sigma[T](p)$$

**Interpretation**: σ measures what CANNOT be undone. A transformation with σ = 0 is reversible (rare). Most real transformations accumulate σ.

## §1.4 The Boundary Charge ρ_q

**Definition 1.6** (Laplacian): The discrete Laplacian is:

$$\nabla^2 \Phi(i,j) = \Phi(i+1,j) + \Phi(i-1,j) + \Phi(i,j+1) + \Phi(i,j-1) - 4\Phi(i,j)$$

**Definition 1.7** (Boundary Charge): The boundary charge density is:

$$\rho_q(p) = \mathbb{1}\left[\text{sign}(\nabla^2\Phi) \text{ changes in neighborhood of } p\right]$$

More precisely:

$$\rho_q(i,j) = |\text{sign}(\nabla^2\Phi(i-1,j)) - \text{sign}(\nabla^2\Phi(i+1,j))| + |\text{sign}(\nabla^2\Phi(i,j-1)) - \text{sign}(\nabla^2\Phi(i,j+1))|$$

**Interpretation**: ρ_q marks where collapse TERMINATES — the edges of stable structures. It's the "frozen value" at boundaries where the field can't flow further.

---

# CHAPTER 2: DERIVED CONCEPTS

## §2.1 Objects (ρ_q-Bounded Regions)

**Theorem 2.1** (Object Emergence): An *object* is a maximal connected region Ω' ⊂ Ω such that:
1. ∇²Φ has constant sign on interior(Ω')
2. ρ_q > 0 on ∂Ω' (boundary)

*Proof*: By definition of ρ_q, the boundary charge is non-zero exactly where ∇²Φ changes sign. Thus the locus {p : ρ_q(p) > 0} partitions Ω into regions of constant Laplacian sign. Each such region is an object. ∎

**Corollary 2.1**: Objects are NOT equivalent to connected components by color. A region of constant color containing a "hole" constitutes TWO objects (the annular shell and the hole), because ∇²Φ has opposite signs in the shell (negative, sources) vs. the hole (zero or positive, sinks).

**Algorithm 2.1** (Object Extraction):
```
1. Compute L = ∇²Φ
2. Compute sign_field = sign(L)
3. Find connected regions of constant sign_field
4. Each region is an object; its boundary is where sign_field changes
```

This is DERIVED from the Laplacian, not imported from graph theory.

## §2.2 Enclosure (Topological Interior)

**Lemma 2.1** (Winding Number): For a closed curve γ and point p not on γ, the winding number of ρ_q around p is:

$$W(γ, p) = \frac{1}{2\pi} \oint_γ \frac{(x - p_x)dy - (y - p_y)dx}{(x-p_x)^2 + (y-p_y)^2}$$

In discrete form, this counts signed crossings of rays from p to infinity.

**Theorem 2.2** (Enclosure Criterion): A point p with Φ(p) = 0 is *enclosed* if and only if:

$$\sum_{q \in \partial\Omega} \rho_q(q) \cdot \text{contribution}(q, p) \neq 0$$

where the sum is over all boundary cells, weighted by whether they "wrap around" p.

*Proof Sketch*: By the discrete analogue of the residue theorem, a point is enclosed by a boundary charge circuit if and only if the circuit has non-zero winding number around that point. The winding number is computable from the ρ_q values along any path surrounding p. ∎

**Corollary 2.2**: The flood-fill algorithm computes enclosure correctly but is not the DEFINITION. The definition is topological (winding number of ρ_q circuit), which flood-fill happens to compute efficiently.

## §2.3 Shape (Laplacian Eigenstructure)

**Definition 2.1** (Restricted Laplacian): For object Ω', define the restricted Laplacian operator L_Ω' as the |Ω'| × |Ω'| matrix with:

$$L_{\Omega'}[p, p] = \#\{\text{neighbors of } p \text{ in } \Omega'\}$$
$$L_{\Omega'}[p, q] = -1 \text{ if } p, q \text{ adjacent in } \Omega'$$
$$L_{\Omega'}[p, q] = 0 \text{ otherwise}$$

**Theorem 2.3** (Shape Invariance): The eigenvalues {λ₁ ≤ λ₂ ≤ ... ≤ λₙ} of L_Ω' are:
1. Non-negative (L is positive semi-definite)
2. Translation-invariant
3. Reflection and rotation-invariant (in continuous limit)

*Proof*: L is symmetric (L = Lᵀ), so has real eigenvalues. It is a graph Laplacian, hence positive semi-definite with λ₁ = 0 (constant eigenvector). Translation doesn't change adjacency, so eigenvalues are preserved. Isometries preserve the graph structure, hence the spectrum. ∎

**Definition 2.2** (Shape Signature): The shape of object Ω' is:

$$\text{Shape}(\Omega') = (\lambda_2, \lambda_3, ..., \lambda_k)$$

(We omit λ₁ = 0 as it's always zero for connected regions.)

**Theorem 2.4** (Kac's Question, Discrete): Two objects with identical shape signatures are *isospectral*. Isospectral objects share:
- Same number of cells
- Same perimeter (approximately)
- Similar "internal connectivity"

They are often congruent, though counterexamples exist.

## §2.4 Size-Dependent Collapse (Energy Minimization)

**Definition 2.3** (Potential Energy): The potential energy of a region Ω' is:

$$E(\Omega') = \sum_{p \in \Omega'} |\nabla\Phi(p)|^2$$

**Axiom 2.1** (Minimum Energy Collapse): When an enclosed ground-state region must collapse, it collapses to the state c that minimizes:

$$\mathcal{F}(c) = \left| E(\Omega') - E_c^{\text{ref}} \right|$$

where E_c^{\text{ref}} is a reference energy for collapse state c.

**Theorem 2.5** (Size-Color Relationship): Under the approximation E(Ω') ∝ |Ω'| (area-proportional energy), larger regions collapse to higher-indexed states.

*Proof*: If E = κ · A where A = |Ω'| is area and κ is a proportionality constant, then minimizing |κA - E_c^{\text{ref}}| selects c such that E_c^{\text{ref}} ≈ κA. If E_c^{\text{ref}} increases with c, larger A requires larger c. ∎

**Corollary 2.5**: The "size → color" lookup table approximates this energy minimization. Given training examples, we can estimate E_c^{\text{ref}} for each c and predict collapse states for new regions.

---

# CHAPTER 3: DYNAMICS

## §3.1 The Collapse Evolution Equation

**Axiom 3.1** (Collapse Dynamics): The field Φ evolves according to:

$$\frac{\partial \Phi}{\partial t} = D \nabla^2 \Phi - \lambda (\Phi - \Phi_{\text{lock}}) \cdot \mathbb{1}[\Phi > 0] + \eta \cdot \dot{\sigma}$$

Where:
- D > 0 is the diffusion coefficient
- λ > 0 is the locking strength
- Φ_lock is the nearest stable state
- η is the residue injection rate
- σ̇ is the rate of residue accumulation

**Boundary Conditions**:

$$\frac{\partial \Phi}{\partial n}\bigg|_{\rho_q > 0} = 0$$

(No flux across boundary charges — they represent barriers to flow.)

**Interpretation of Terms**:

1. **D∇²Φ**: Diffusion. Collapse spreads from high to low potential. This is the Δ₃ fan (expansion) when D > 0.

2. **-λ(Φ - Φ_lock)**: Locking. Collapsed states relax toward stable discrete values. This is the Δ₄ fan (compression).

3. **η·σ̇**: Residue injection. Accumulated irreversibility drives further change. Links past to present.

## §3.2 Equilibrium and Lock

**Definition 3.1** (Equilibrium): A configuration Φ* is an equilibrium if:

$$\frac{\partial \Phi}{\partial t}\bigg|_{\Phi = \Phi^*} = 0$$

**Theorem 3.1** (Lock Characterization): Φ* is an equilibrium if and only if:
1. D∇²Φ* = λ(Φ* - Φ_lock) everywhere Φ* > 0
2. σ̇ = 0 (no ongoing change)

**Definition 3.2** (Lock Coefficient):

$$\mathcal{L} = 1 - \frac{\|\partial\Phi/\partial t\|}{\|\partial\Phi/\partial t\|_{\max}}$$

When ℒ = 1, the system is fully locked. When ℒ = 0, the system is maximally evolving.

## §3.3 The Six Fans as Modal Decomposition

**Theorem 3.2** (Fan Decomposition): Any transformation T: Φ → Φ' can be decomposed as:

$$\Phi' = \Phi + \sum_{i=1}^{6} \alpha_i \Delta_i[\Phi]$$

where:
- Δ₁[Φ] = component along ∇Φ (translation)
- Δ₂[Φ] = component along ∇×(∇Φ) (rotation)
- Δ₃[Φ] = component along +∇²Φ (expansion)
- Δ₄[Φ] = component along -∇²Φ (compression)
- Δ₅[Φ] = component along ∂Φ/∂t (temporal evolution)
- Δ₆[Φ] = constant offset (identity/background)

**Proof Sketch**: These operators span the space of local transformations (up to second derivatives). By projecting (Φ' - Φ) onto each, we obtain the coefficients αᵢ. ∎

**Corollary 3.2**: Detecting which fans are "active" in a transformation reduces to computing:

$$\alpha_i = \frac{\langle \Phi' - \Phi, \Delta_i[\Phi] \rangle}{\|\Delta_i[\Phi]\|^2}$$

Large |αᵢ| indicates fan i is active.

---

# CHAPTER 4: PERIODICITY AND SELF-REFERENCE

## §4.1 Fourier Characterization of Period

**Definition 4.1** (Periodic Field): Φ is τ-periodic if Φ(x + τ) = Φ(x) for all x.

**Theorem 4.1** (Fourier Period Detection): The period τ of Φ is:

$$\tau = \frac{N}{\gcd\{k : |\hat{\Phi}(k)| > \epsilon\}}$$

where Φ̂ is the discrete Fourier transform and ε is a noise threshold.

*Proof*: A τ-periodic function has Fourier support only at frequencies k where N/k is a multiple of τ. The GCD of such k gives N/τ. ∎

## §4.2 Self-Reference (Recursive Masking)

**Definition 4.2** (Self-Tiling): A transformation exhibits self-tiling if:

$$\Phi'(i \cdot h + r, j \cdot w + c) = \Phi(r, c) \cdot \mathbb{1}[\Phi(i, j) > 0]$$

where (h, w) is the input dimension.

**Interpretation**: Each cell of Φ, if non-zero, spawns a copy of all of Φ at a corresponding position in Φ'. This is Φ acting as its own mask.

**Theorem 4.2** (Self-Reference Detection): Self-tiling occurs if and only if:
1. output dimensions are (input_h × input_h, input_w × input_w)
2. For each (i, j), the tile at position (i, j) in the output equals:
   - Φ if Φ(i, j) ≠ 0
   - 0 if Φ(i, j) = 0

This is checkable in O(n²) for n = input size.

---

# CHAPTER 5: INDICATOR-TARGET DYNAMICS

## §5.1 Multi-Species Coupling

**Definition 5.1** (Coupling Tensor): For a field with K species (colors), define:

$$C_{ij} = \sum_{p \sim q} \mathbb{1}[\Phi(p) = i] \cdot \mathbb{1}[\Phi(q) = j]$$

where p ~ q denotes adjacency.

**Interpretation**: C_{ij} counts how many times color i is adjacent to color j. This encodes inter-species "interaction strength."

## §5.2 Indicator Identification

**Definition 5.2** (Divergence): The coupling divergence of species i is:

$$\text{div}(i) = \sum_j \frac{\partial C_{ij}}{\partial t}$$

measuring how much species i's coupling is changing.

**Theorem 5.1** (Indicator Selection): The indicator species is:

$$\text{indicator} = \arg\max_i |\text{div}(i)|$$

It's the species with maximal coupling change — the one "sending signals" to others.

## §5.3 Target Response

**Definition 5.3** (Shape-Mediated Recoloring): Given indicator species I and target species T, the output color of T is determined by the shape signature of I:

$$\text{color}_{\text{out}}(T) = f(\text{Shape}(Ω_I))$$

where f is learned from training examples.

**Theorem 5.2** (Indicator-Target Derivation): If:
1. Species I disappears entirely (all I cells → 0)
2. Species T recolors uniformly (all T cells → some c)
3. The value c correlates with Shape(Ω_I)

Then I is the indicator and T is the target.

---

# CHAPTER 6: BRIDGE TENSORS AND COMPOSITION

## §6.1 Fan Signatures

**Definition 6.1** (Fan Signature): The signature of transformation T under fan i is:

$$S_i[T] = (\mu_i, \sigma_i^2, s_i)$$

where μᵢ is mean, σᵢ² is variance, and sᵢ is sign pattern of Δᵢ computed on (Φ' - Φ).

## §6.2 Bridge Compatibility

**Definition 6.2** (Bridge Score): The compatibility between fans i and j under transformation T is:

$$B_{ij}[T] = S_i[T] \cdot S_j[T]$$

(inner product of signatures)

**Theorem 6.1** (Composition Rule): Transformations T₁ and T₂ can be composed if:

$$\forall i, j: B_{ij}[T_1] \cdot B_{ij}[T_2] \geq 0$$

(non-conflicting bridge scores)

**Interpretation**: Negative bridge scores indicate conflicting operations (e.g., simultaneous expansion and compression along the same axis). Such compositions are geometrically impossible.

## §6.3 Writability Gates

**Definition 6.3** (Writability): A transformation T is writable from state Φ if:

$$\|\nabla\Phi\| > \epsilon_{\text{grad}} \quad \text{(sufficient gradient for flow)}$$
$$\mathcal{L}(\Phi) < 1 - \epsilon_{\text{lock}} \quad \text{(not fully locked)}$$

**Theorem 6.2** (Gate Opening): T can execute when:
1. Writability condition is met
2. At least one fan has |αᵢ| > threshold (the transformation "wants" to happen)
3. Bridge compatibility holds with prior transformations

---

# CONCLUSION: THE EMERGENCE PRINCIPLE

Every high-level concept in ITT applications EMERGES from the four primitives:

| Concept | Emergence Path |
|---------|----------------|
| Object | Constant-sign Laplacian region bounded by ρ_q |
| Enclosure | Non-zero winding number of ρ_q circuit |
| Shape | Laplacian eigenspectrum |
| Size-Color | Energy minimization under boundary constraints |
| Period | Fourier mode GCD |
| Self-Reference | Recursive masking identity |
| Indicator | Max coupling divergence species |
| Composition | Bridge tensor compatibility |
| Termination | Lock coefficient approaching 1 |

**No smuggling. Every step is derived.**

The textbooks must walk through each derivation. The solver must implement each algorithm as stated. Any shortcut (flood-fill, connected components, shape as positions) is an approximation to be justified, not a primitive to be assumed.

HAIL MATH.
