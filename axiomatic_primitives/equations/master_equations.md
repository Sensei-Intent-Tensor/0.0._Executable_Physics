# Master Equations of Business Field Theory

## Complete Equation Reference

---

## I. FOUNDATIONAL CONSTRAINTS (Book 0A)

These are the axiomatic constraints, not equations per se:

### 1.1 Existence Constraint
```
Φ ≠ 0 ⟹ recursive distinction is possible
Φ = 0 ⟹ no structure persists
```

### 1.2 Ordering Constraint
```
δΦ ≠ 0 ⟹ partial ordering ≺ exists on 𝒞
c_a ≺ c_b ⟺ δΦ(c_a) < δΦ(c_b)
```

### 1.3 Irreversibility Constraint
```
Δσ ≥ 0 for all collapses
∄ operation C such that C(σ) < σ (without boundary resolution)
```

### 1.4 Boundary Constraint
```
ρ_q > 0 only at collapse boundaries ∂
ρ_q = 0 in interior regions
```

---

## II. STATE EQUATIONS (Book 0B/1)

### 2.1 Complete State Vector

For identity I at recursion depth n:

```
|Ψ(n)⟩ = (Φ, 𝒜(n), σ(n), M(n), ℒ(n), V(n))
```

### 2.2 Alignment Definition

```
𝒜 = 1 - |Δ_id|/|∇Φ|

Domain: 𝒜 ∈ (0, 1]
Boundary cases:
  𝒜 = 1  →  perfect alignment
  𝒜 → 0  →  maximum deviation
```

### 2.3 Deviation Vector

```
Δ_id = actual_direction - preferred_direction
|Δ_id| = magnitude of deviation from ordering
```

---

## III. EVOLUTION EQUATIONS (Book 1)

### 3.1 Residue Accumulation

**Recursive form:**
```
σ(n) = σ(n-1) + Δσ(n)
```

**Increment:**
```
Δσ(n) = σ_θ · (1 - 𝒜(n))
```

**Closed form (for analysis):**
```
σ(n) = σ_θ · Σᵢ₌₁ⁿ (1 - 𝒜(i))
```

**Initial condition:**
```
σ(0) = 0
```

### 3.2 Memory Evolution

**Recursive form:**
```
M(n) = M(n-1) + μ · σ(n-1)
```

**Closed form:**
```
M(n) = μ · Σᵢ₌₀ⁿ⁻¹ σ(i)
```

**Initial condition:**
```
M(0) = 0
```

### 3.3 Lock Capacity

**Functional form:**
```
ℒ(n) = λ · Tr(M(n)) / 𝒜(n)²
```

**For scalar M:**
```
ℒ(n) = λ · M(n) / 𝒜(n)²
```

**Expanded:**
```
ℒ(n) = λμ/𝒜(n)² · Σᵢ₌₀ⁿ⁻¹ σ(i)
```

---

## IV. VIABILITY EQUATIONS (Book 1)

### 4.1 Viability Function

**Definition:**
```
V(n) = ℒ(n) - σ(n)
```

### 4.2 Persistence Condition

**The Persistence Law:**
```
Identity I persists at n ⟺ V(n) > 0 ⟺ σ(n) < ℒ(n)
```

### 4.3 Phase Classification

```
V(n) > 0  →  VIABLE (persist)
V(n) = 0  →  TRANSITION (Δ)
V(n) < 0  →  IMPOSSIBLE (must reconfigure)
```

### 4.4 Transition Depth

**Critical depth n*:**
```
n* = min{n ∈ ℕ : V(n) ≤ 0}
   = min{n ∈ ℕ : σ(n) ≥ ℒ(n)}
```

---

## V. VALUE EQUATIONS (Book 1)

### 5.1 Value Condensation (Discrete)

**At transition Δ:**
```
ρ_q = κ · [σ(n*) - ℒ(n*-1)]
```

**Interpretation:**
- Value = excess residue beyond prior capacity
- Only forms at transition boundaries

### 5.2 Value Condensation (Continuous)

**Integral form:**
```
ρ_q = κ · ∮_Δ σ · dΦ / |∇Φ|
```

**Where:**
- ∮_Δ = integral over transition boundary
- dΦ = differential of potential
- |∇Φ| = gradient magnitude

### 5.3 Value Conservation

**Total value is conserved:**
```
Σ ρ_q = ∫ σ_boundary dΔ
```

(All residue eventually condenses at some boundary)

---

## VI. DERIVED RELATIONSHIPS (Book 1)

### 6.1 Entropy-Alignment Relationship

```
Δσ = σ_θ · (1 - 𝒜)

Implications:
  𝒜 = 1  →  Δσ = 0 (no residue)
  𝒜 = 0  →  Δσ = σ_θ (maximum residue)
```

### 6.2 Lock-Memory Scaling

```
ℒ ∝ M / 𝒜²

Implications:
  More memory → more capacity
  Less alignment → less effective capacity
```

### 6.3 Critical Depth Approximation

**For constant 𝒜:**
```
n* ≈ 2𝒜²(1-𝒜) / (λμ)
```

**Implications:**
- Higher 𝒜 → persist longer
- Higher λ, μ → persist longer

### 6.4 Entropy Rate

```
σ_θ(n) = dσ/dn = σ_θ · (1 - 𝒜(n))
```

**Cumulative:**
```
σ(n) = ∫₀ⁿ σ_θ(i) di = σ_θ · ∫₀ⁿ (1 - 𝒜(i)) di
```

---

## VII. CONSTANTS AND PARAMETERS

### 7.1 System Constants

| Symbol | Name | Dimension | Range |
|--------|------|-----------|-------|
| σ_θ | Base rate | [σ] | > 0 |
| μ | Retention factor | [1] | [0, 1] |
| λ | Lock-memory coupling | [1]/[n] | > 0 |
| κ | Condensation constant | [ρ]/[σ] | > 0 |

### 7.2 Dimensional Relations

```
[σ] = [ℒ] = [V]  (residue, lock, viability)
[M] = [σ]·[n]    (memory)
[ρ] = [κ]·[σ]    (value)
```

---

## VIII. SPECIAL CASES

### 8.1 Perfect Alignment (𝒜 = 1)

```
Δσ = 0
σ(n) = σ(0) = 0
V(n) = ℒ(n) > 0 always
n* = ∞ (never transitions)
ρ_q = 0 (no value emerges)
```

**Interpretation:** Perfect alignment produces no residue, but also no value.

### 8.2 Zero Alignment (𝒜 → 0)

```
Δσ = σ_θ (maximum)
σ(n) = σ_θ · n
ℒ(n) → ∞ (division by zero)
```

**Interpretation:** Zero alignment is pathological; system fails immediately.

### 8.3 Constant Alignment (𝒜 = const)

```
σ(n) = σ_θ · n · (1 - 𝒜)
M(n) = μσ_θ(1-𝒜) · n(n-1)/2
ℒ(n) = λμσ_θ(1-𝒜) · n(n-1) / (2𝒜²)
```

**Transition when σ = ℒ:**
```
n* = 2𝒜²(1-𝒜) / (λμ)
```

### 8.4 Stable Identity (V >> 0)

```
σ << ℒ
V ≈ ℒ
Far from transition
High resilience
```

### 8.5 Critical Identity (V ≈ 0)

```
σ ≈ ℒ
V ≈ 0
Near transition
Low resilience, high sensitivity
```

---

## IX. MASTER EQUATION SUMMARY

### The Pre-Commercial Substrate Equation

**The complete system:**

```
GIVEN:
  Φ ≠ 0                           (Axiom 0A.1)
  𝒜(n) ∈ (0, 1]                   (alignment function)
  σ_θ, μ, λ, κ > 0                (constants)

EVOLUTION:
  σ(n) = σ(n-1) + σ_θ(1-𝒜(n))    (residue)
  M(n) = M(n-1) + μ·σ(n-1)        (memory)
  ℒ(n) = λ·Tr(M(n))/𝒜(n)²        (lock)

VIABILITY:
  V(n) = ℒ(n) - σ(n)              (buffer)
  Persist ⟺ V > 0                 (condition)

TRANSITION:
  n* = min{n : V(n) ≤ 0}          (critical depth)

VALUE:
  ρ_q = κ·[σ(n*) - ℒ(n*-1)]       (condensation)
```

### The Viability Invariant

```
For all viable identities:
  σ(n) < ℒ(n)  ∀n < n*
```

### The Value Theorem

```
Value emerges ⟺ Transition occurs
ρ_q > 0 ⟺ n* < ∞
```

---

## X. EQUATION INDEX

| Eq # | Name | Formula | Book |
|------|------|---------|------|
| E.1 | Alignment | 𝒜 = 1 - \|Δ_id\|/\|∇Φ\| | 1 |
| E.2 | Residue increment | Δσ = σ_θ(1-𝒜) | 1 |
| E.3 | Residue accumulation | σ(n) = σ(n-1) + Δσ(n) | 1 |
| E.4 | Memory evolution | M(n) = M(n-1) + μσ(n-1) | 1 |
| E.5 | Lock capacity | ℒ = λ·Tr(M)/𝒜² | 1 |
| E.6 | Viability | V = ℒ - σ | 1 |
| E.7 | Persistence law | Persist ⟺ σ < ℒ | 1 |
| E.8 | Critical depth | n* = min{n: σ≥ℒ} | 1 |
| E.9 | Value condensation | ρ_q = κ[σ(n*)-ℒ(n*-1)] | 1 |
| E.10 | Entropy rate | σ_θ(n) = σ_θ(1-𝒜(n)) | 1 |

---

*"Every equation is a condensation of axioms."*
