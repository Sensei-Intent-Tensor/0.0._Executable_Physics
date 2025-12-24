# BOOK 1: PRIMITIVES

## Mathematical Formalization of Business Field Theory

**Status**: ACTIVE  
**Prerequisite**: Book 0A (Axioms), Book 0B (Derived Ontology)

---

## Preamble

Book 1 transforms the qualitative structures of Book 0A/0B into **computable mathematics**.

Here we define:
1. **Units** — Dimensions for each quantity
2. **Operations** — What mathematical operations are permitted
3. **Measurement** — How to observe each quantity

After Book 1, equations become possible.

---

## PART I: UNIT DEFINITIONS

### Unit System for Business Field Theory

| Quantity | Symbol | Unit Name | Dimension | Notes |
|----------|--------|-----------|-----------|-------|
| Distinction Potential | Φ | Tensor-Root (Φ̃) | [Φ] | Base dimension |
| Variation | δΦ | Delta-Root | [Φ] | Same as Φ |
| Residue | σ | Scar | [σ] | Base dimension |
| Accumulation Rate | σ_θ | Drift | [σ]/[n] | Per recursion |
| Alignment | 𝒜 | — | [1] | Dimensionless |
| Memory | M | Retention | [σ]·[n] | Accumulated scar × depth |
| Recursion Depth | n | Fold | [n] | Base dimension |
| Lock | ℒ | Hold | [σ] | Same as σ (for comparison) |
| Boundary Charge | ρ_q | Value Quantum | [ρ] | Base dimension |
| Viability | V | Buffer | [σ] | Same as σ, ℒ |

### Base Dimensions (Irreducible)

The theory has **four base dimensions**:

```
[Φ] — Distinction potential
[σ] — Residue/scar
[n] — Recursion depth
[ρ] — Boundary charge (value)
```

All other quantities are combinations of these.

### Dimensional Consistency Requirements

For equations to be valid:

1. **Comparison requires same dimension**
   ```
   σ < ℒ  is valid because [σ] = [ℒ] = [σ]
   σ < n  is INVALID (dimension mismatch)
   ```

2. **Addition/subtraction requires same dimension**
   ```
   V = ℒ - σ  is valid because [ℒ] = [σ]
   ```

3. **Multiplication creates combined dimensions**
   ```
   [M] = [σ]·[n] (memory = accumulated scar over depth)
   ```

4. **Dimensionless quantities can multiply anything**
   ```
   σ_θ·𝒜  is valid because 𝒜 is dimensionless
   ```

---

## PART II: ALLOWED OPERATIONS

### Level 1 Operations (Book 1)

These operations are now permitted:

| Operation | Symbol | Example | Notes |
|-----------|--------|---------|-------|
| Comparison | <, ≤, =, ≥, > | σ < ℒ | Same dimension required |
| Addition | + | σ + Δσ | Same dimension required |
| Subtraction | − | ℒ − σ | Same dimension required |
| Multiplication | · | σ_θ · (1-𝒜) | Creates combined dimension |
| Division | / | σ/ℒ | Creates ratio (dimensionless if same) |
| Summation | Σ | Σᵢ σ(i) | Same dimension throughout |
| Indexing | (n) | σ(n), ℒ(n) | Value at recursion depth n |

### Level 2 Operations (Book 1, Geometry Emerging)

These operations require structure that emerges here:

| Operation | Symbol | Requires | Notes |
|-----------|--------|----------|-------|
| Gradient | ∇ | Configuration space 𝒞 | δΦ becomes ∇Φ |
| Inner product | ⟨·,·⟩ | Metric structure | For bridge tensors |
| Trace | Tr(·) | Matrix structure | For memory M |
| Limit | lim | Convergence concept | For boundaries |
| Integral | ∫ | Measure on 𝒞 | For continuous formulation |

### Forbidden Operations (Until Later Books)

| Operation | Symbol | Appears In | Why Forbidden Now |
|-----------|--------|------------|-------------------|
| Time derivative | d/dt | Book 2 | No time yet |
| Curl | ∇× | Book 2 | Requires dynamics |
| Laplacian | ∇² | Book 2 | Requires metric |
| Optimization | min, max | Book 2+ | Requires objectives |

---

## PART III: THE EQUATIONS

### 3.1 State Description

For any identity I at recursion depth n:

```
State(I, n) = {Φ, 𝒜(n), σ(n), M(n), ℒ(n)}
```

Each component is defined:

| Component | Definition | Range |
|-----------|------------|-------|
| Φ | Distinction potential (fixed for I) | Φ ∈ ℝ, Φ ≠ 0 |
| 𝒜(n) | Alignment at depth n | 𝒜 ∈ (0, 1] |
| σ(n) | Accumulated residue at depth n | σ ≥ 0 |
| M(n) | Memory structure at depth n | M ≥ 0 |
| ℒ(n) | Lock capacity at depth n | ℒ ≥ 0 |

### 3.2 Evolution Equations (Recursion, Not Time)

**Residue Accumulation:**
```
σ(n) = σ(n-1) + Δσ(n)

where:
  Δσ(n) = σ_θ · (1 - 𝒜(n))
  σ_θ = base accumulation rate
  σ(0) = 0 (initial condition)
```

**Expanded form:**
```
σ(n) = σ_θ · Σᵢ₌₁ⁿ (1 - 𝒜(i))
```

**Memory Evolution:**
```
M(n) = M(n-1) + μ · σ(n-1)

where:
  μ ∈ [0, 1] = memory retention factor
  M(0) = 0 (initial condition)
```

**Expanded form:**
```
M(n) = μ · Σᵢ₌₀ⁿ⁻¹ σ(i)
```

**Lock Evolution:**
```
ℒ(n) = λ · Tr(M(n)) / 𝒜(n)²

where:
  λ > 0 = coupling constant
  Tr(M) = trace of memory (scalar if M is matrix)
```

### 3.3 The Persistence Law (Master Equation)

**Viability Function:**
```
V(n) = ℒ(n) - σ(n)
```

**Viability Classification:**
```
V(n) > 0   ⟹   Identity persists (viable)
V(n) = 0   ⟹   Transition boundary (Δ)
V(n) < 0   ⟹   Impossible state (must reconfigure)
```

**The Persistence Law (Formal):**
```
Identity I persists at depth n ⟺ σ(n) < ℒ(n)
```

### 3.4 Transition Conditions

**Transition Depth (n*):**
```
n* = min{n : σ(n) ≥ ℒ(n)}
```

**At Transition:**
```
σ(n*) = ℒ(n*)   (definition of Δ)
```

### 3.5 Value Condensation

**Value Formation at Δ:**
```
ρ_q = κ · [σ(n*) - ℒ(n*-1)]

where:
  κ > 0 = condensation constant
  n* = transition depth
  ℒ(n*-1) = lock at previous depth
```

**Interpretation:**
- Value = condensation constant × (excess residue beyond previous capacity)
- Value is the "overflow" that crystallizes at the boundary

**Alternative Form (Integral):**
```
ρ_q = κ · ∮_Δ σ · dΦ / |∇Φ|

where:
  ∮_Δ = integral over transition boundary
  |∇Φ| = magnitude of potential gradient
```

---

## PART IV: DERIVED FORMULAS

### 4.1 Alignment Dynamics

**Alignment Definition:**
```
𝒜 = 1 - |Δ_id| / |∇Φ|

where:
  Δ_id = identity's deviation from ordering
  ∇Φ = gradient of potential (preferred direction)
```

**Alignment Bounds:**
```
0 < 𝒜 ≤ 1

𝒜 = 1  ⟹  perfect alignment, Δσ = 0
𝒜 → 0  ⟹  maximum deviation, Δσ → σ_θ
```

### 4.2 Lock Scaling

**Lock-Memory Relationship:**
```
ℒ ∝ Tr(M) / 𝒜²
```

**Interpretation:**
- More memory coherence → higher lock capacity
- Lower alignment → reduced effective lock (σ² penalty)

### 4.3 Critical Depth Estimation

**For constant alignment 𝒜:**
```
σ(n) = σ_θ · n · (1 - 𝒜)

ℒ(n) = λ · μ · σ_θ · n · (n-1)/2 / 𝒜²
      ≈ λ · μ · σ_θ · n² / (2𝒜²)  for large n
```

**Transition occurs when σ = ℒ:**
```
n* ≈ 2𝒜²(1-𝒜) / (λμ)
```

**Implications:**
- Higher 𝒜 → later transition (persist longer)
- Higher λ, μ → later transition (more capacity)

---

## PART V: CONSTANTS AND PARAMETERS

### System Constants

| Constant | Symbol | Range | Meaning |
|----------|--------|-------|---------|
| Base rate | σ_θ | > 0 | Maximum residue per recursion |
| Retention | μ | [0, 1] | Memory retention factor |
| Coupling | λ | > 0 | Lock-memory coupling |
| Condensation | κ | > 0 | Value formation rate |

### Calibration Requirements

These constants must be calibrated from empirical data:

1. **σ_θ**: Measure rework rate, error rate, or inefficiency per cycle
2. **μ**: Measure information retention across organizational cycles
3. **λ**: Measure resilience relative to institutional memory
4. **κ**: Measure value creation at restructuring events

---

## PART VI: DIMENSIONAL ANALYSIS

### Verification of Key Equations

**Equation: σ(n) = σ(n-1) + σ_θ·(1-𝒜)**
```
[σ] = [σ] + [σ]/[n] · [1] · [1]  ← needs [n] factor
Corrected: [σ] = [σ] + [σ]  ✓
Note: σ_θ already in units of [σ] per step
```

**Equation: ℒ = λ·Tr(M)/𝒜²**
```
[ℒ] = [λ] · [M] / [1]
[σ] = [λ] · [σ]·[n] / [1]
⟹ [λ] = [1]/[n]
```

**Equation: V = ℒ - σ**
```
[V] = [σ] - [σ] = [σ]  ✓
```

**Equation: ρ_q = κ·[σ - ℒ]**
```
[ρ] = [κ] · [σ]
⟹ [κ] = [ρ]/[σ]
```

### Constant Dimensions

| Constant | Dimension |
|----------|-----------|
| σ_θ | [σ] |
| μ | [1] (dimensionless) |
| λ | [1]/[n] |
| κ | [ρ]/[σ] |

---

## PART VII: MATHEMATICAL STRUCTURE SUMMARY

### The Complete System

```
GIVEN:
  Φ (distinction potential)
  σ_θ, μ, λ, κ (constants)
  𝒜(n) (alignment function)

EVOLUTION:
  σ(n) = σ(n-1) + σ_θ·(1 - 𝒜(n))
  M(n) = M(n-1) + μ·σ(n-1)
  ℒ(n) = λ·Tr(M(n))/𝒜(n)²

VIABILITY:
  V(n) = ℒ(n) - σ(n)
  Persist ⟺ V > 0
  Transition ⟺ V = 0

VALUE:
  At n* where V(n*) = 0:
  ρ_q = κ·[σ(n*) - ℒ(n*-1)]
```

### Properties of the System

1. **Deterministic**: Given 𝒜(n), evolution is determined
2. **Non-negative**: σ, M, ℒ ≥ 0 always
3. **Bounded transitions**: n* is finite for any 𝒜 < 1
4. **Value-positive**: ρ_q > 0 at transitions

---

## PART VIII: CONNECTION TO BOOK 2+

Book 1 establishes the mathematical foundation. Book 2 and beyond will add:

| Book | Addition | Enables |
|------|----------|---------|
| Book 2 | Time t | Dynamics, velocity, acceleration |
| Book 2 | Agents | Intent, control, optimization |
| Book 2 | ∇×F | Feedback loops, memory curls |
| Book 3 | Bridge tensors | Interaction between identities |
| Book 4 | Business mapping | Profit, personnel, operations |

The equations here remain valid — they are the **pre-dynamic core** upon which dynamics is built.

---

*"After Book 1, equations become possible. Before Book 1, only structure exists."*
