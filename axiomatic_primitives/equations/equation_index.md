# Equation Index

## Quick Reference for All Business Field Theory Equations

---

## CORE EQUATIONS

### The Persistence Law (Master Equation)
```
Identity I persists at depth n ⟺ σ(n) < ℒ(n)
```

### Viability Function
```
V(n) = ℒ(n) - σ(n)
```

### Value Condensation
```
ρ_q = κ · [σ(n*) - ℒ(n*-1)]
```

---

## STATE EQUATIONS

### E.1 — Alignment
```
𝒜 = 1 - |Δ_id|/|∇Φ|

Domain: 𝒜 ∈ (0, 1]
```

### E.2 — Residue Increment
```
Δσ(n) = σ_θ · (1 - 𝒜(n))
```

### E.3 — Residue Accumulation
```
σ(n) = σ(n-1) + Δσ(n)
σ(n) = σ_θ · Σᵢ₌₁ⁿ (1 - 𝒜(i))
σ(0) = 0
```

### E.4 — Memory Evolution
```
M(n) = M(n-1) + μ · σ(n-1)
M(n) = μ · Σᵢ₌₀ⁿ⁻¹ σ(i)
M(0) = 0
```

### E.5 — Lock Capacity
```
ℒ(n) = λ · Tr(M(n)) / 𝒜(n)²
```

---

## DERIVED EQUATIONS

### E.6 — Critical Depth (Constant 𝒜)
```
n* ≈ 2𝒜²(1-𝒜) / (λμ)
```

### E.7 — Entropy Rate
```
σ_θ(n) = σ_θ · (1 - 𝒜(n))
```

### E.8 — Value Integral Form
```
ρ_q = κ · ∮_Δ σ · dΦ / |∇Φ|
```

---

## CONSTRAINT EQUATIONS

### C.1 — Existence
```
Φ ≠ 0 ⟹ recursive distinction possible
```

### C.2 — Ordering
```
δΦ ≠ 0 ⟹ c_a ≺ c_b exists
```

### C.3 — Irreversibility
```
∄ C such that C(σ) < σ
```

### C.4 — Boundary Localization
```
ρ_q > 0 only at ∂ (boundaries)
```

---

## DIMENSIONAL TABLE

| Quantity | Dimension |
|----------|-----------|
| Φ | [Φ] |
| σ, ℒ, V | [σ] |
| 𝒜 | [1] (dimensionless) |
| M | [σ]·[n] |
| n | [n] |
| ρ_q | [ρ] |
| σ_θ | [σ] |
| μ | [1] |
| λ | [1]/[n] |
| κ | [ρ]/[σ] |

---

## SPECIAL CASES

### Perfect Alignment (𝒜 = 1)
```
Δσ = 0, σ(n) = 0, V = ℒ, n* = ∞, ρ_q = 0
```

### Constant Alignment
```
σ(n) = σ_θn(1-𝒜)
ℒ(n) ≈ λμσ_θn²(1-𝒜)/(2𝒜²)
n* = 2𝒜²(1-𝒜)/(λμ)
```

---

## PHASE CLASSIFICATION

```
V > 0   →  VIABLE
V = 0   →  TRANSITION (Δ)
V < 0   →  IMPOSSIBLE
```

---

*Quick reference — see master_equations.md for full derivations*
