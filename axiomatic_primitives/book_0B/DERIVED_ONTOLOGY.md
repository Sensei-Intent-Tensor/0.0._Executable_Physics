# BOOK 0B: DERIVED ONTOLOGY

## Geometric Crystallization from Book 0A

**Status**: LOCKED  
**Prerequisite**: Book 0A (all four axioms accepted)

---

## Preamble

Book 0B contains **no new axioms**. Everything here is logically unavoidable given Book 0A.

**Rule of Book 0B (Non-Negotiable):**
> If anything in Book 0B feels optional, aesthetic, or merely "useful" — it is wrong.
> Everything must be **inevitable**.

---

## What We Start With (From Book 0A)

| Symbol | Name | Status |
|--------|------|--------|
| Φ | Scalar Potential | Axiom |
| δΦ | Internal Variation | Axiom |
| σ | Irreducible Residue | Axiom |
| ρ_q | Boundary Charge | Axiom |

These are the only primitives. Everything below is derived.

---

## DERIVED QUANTITY 0B.1 — Configuration Set (𝒞)

### Statement

> **There exists a set 𝒞 of distinguishable configurations produced by recursive collapse.**

### Derivation

From Axiom 0A.1:
```
Φ ≠ 0 ⟹ recursive distinction is possible
Recursive distinction ⟹ multiple distinct outcomes
Multiple distinct outcomes ⟹ set of configurations
```

### Properties

- 𝒞 is a set (no topology yet)
- Elements of 𝒞 are distinguishable
- 𝒞 has no geometry, no metric, no coordinates
- 𝒞 is the **shadow** of state space

### What 𝒞 Is NOT (Yet)

- Not a manifold
- Not a vector space
- Not continuous
- Not measurable (no measure defined)

### Plain Language

> "Different collapses produce different configurations. The collection of all such configurations is 𝒞."

---

## DERIVED QUANTITY 0B.2 — Ordering Relation (≺)

### Statement

> **Configurations in 𝒞 admit a partial ordering induced by δΦ.**

### Derivation

From Axiom 0A.2:
```
δΦ ≠ 0 ⟹ Φ varies across configurations
Variation ⟹ comparability
Comparability ⟹ ordering

Define: c_a ≺ c_b ⟺ δΦ(c_a) < δΦ(c_b)
```

### Properties

- ≺ is reflexive: c ≺ c
- ≺ is transitive: c_a ≺ c_b and c_b ≺ c_c ⟹ c_a ≺ c_c
- ≺ is antisymmetric: c_a ≺ c_b and c_b ≺ c_a ⟹ c_a = c_b
- ≺ is **partial** (not all configurations comparable)

### Interpretation

- ≺ is **eligibility ranking**
- Higher in ordering = more eligible for collapse
- This is NOT motion, NOT force, NOT direction
- Just preference

### Plain Language

> "Some configurations are more eligible than others. This ranking is the first hint of direction."

---

## DERIVED QUANTITY 0B.3 — Persistence

### Statement

> **There exist structures that persist across recursive collapse, carrying σ.**

### Derivation (Necessity)

From Axiom 0A.3:
```
σ(n) = σ(n-1) + Δσ(n)
⟹ σ at depth n depends on σ at depth n-1
⟹ Something must carry σ from n-1 to n
⟹ That "something" persists across recursion
```

### Properties

- Persistence is not immortality
- Persistence is carrying structure across recursion levels
- Persistence is compatible with change (identity can change while persisting)

### Plain Language

> "For σ to accumulate, something must stick around to carry it."

---

## DERIVED QUANTITY 0B.4 — Identity (I)

### Statement

> **An identity I is a persistent configuration that carries σ across recursive distinction.**

### Derivation

```
Persistence exists (0B.3)
Persistent structures are distinguishable (from 𝒞)
Distinguishable persistent structure = identity
```

### Properties

- I is individuated (distinguishable from other identities)
- I carries σ (accumulated residue)
- I persists (survives across recursion)
- I is **not yet an agent** (no intention, no control)

### Key Distinction

| Concept | Has | Does Not Have |
|---------|-----|---------------|
| Identity | Persistence, σ-carrying, individuation | Intent, choice, action |
| Agent | All of identity + intent | (Appears in Book 2) |

### Plain Language

> "An identity is something that sticks around and accumulates scars. It doesn't choose — it just persists."

---

## DERIVED QUANTITY 0B.5 — Alignment (𝒜)

### Statement

> **Alignment 𝒜 is the degree to which a collapse follows the ordering ≺.**

### Derivation

```
Ordering ≺ exists (0B.2)
σ is produced by deviation from ordering (0A.3)
⟹ Deviation is quantifiable
⟹ Define alignment as complement of deviation

𝒜 = 1 - (deviation from ordering)
𝒜 ∈ (0, 1]
```

### Properties

| 𝒜 Value | Meaning | σ Production |
|---------|---------|--------------|
| 𝒜 = 1 | Perfect alignment | Δσ = 0 |
| 𝒜 → 0 | Maximum deviation | Δσ → maximum |
| 𝒜 ∈ (0,1) | Partial alignment | Δσ > 0 |

### Formal Definition

```
𝒜 = 1 - d(c, ≺) / d_max

Where:
  d(c, ≺) = deviation of collapse c from ordering ≺
  d_max = maximum possible deviation
```

### Plain Language

> "Alignment measures how well a collapse follows the preferred direction. High alignment = low scar production."

---

## DERIVED QUANTITY 0B.6 — Accumulation Rate (σ_θ)

### Statement

> **The accumulation rate σ_θ is the residue produced per recursion level.**

### Derivation

From Axiom 0A.3:
```
σ(n) = σ(n-1) + Δσ(n)
Define: σ_θ = Δσ/Δn
```

### Relationship to Alignment

```
σ_θ = σ̂ · (1 - 𝒜)

Where σ̂ is the base rate (maximum possible per step)
```

### Properties

- σ_θ ≥ 0 (always non-negative)
- σ_θ = 0 only when 𝒜 = 1
- Higher deviation → higher σ_θ

### Plain Language

> "σ_θ tells you how fast the scars are accumulating."

---

## DERIVED QUANTITY 0B.7 — Memory (M)

### Statement

> **Memory M is the structured retention of past misalignment that conditions future eligibility.**

### Derivation

```
σ is irreducible (0A.3)
σ accumulates across recursion
⟹ Past σ influences present state
⟹ Past is "remembered" as structure
⟹ Memory exists
```

### Formal Definition

```
M(n) = g(σ(0), σ(1), ..., σ(n-1))

Where g is a retention function (specified in Book 1)
```

### Properties

- M is not just "stored data"
- M is structured (has internal organization)
- M influences future eligibility
- M grows with recursion depth

### Preliminary Form (Pre-Tensor)

At this layer, M is scalar or simple functional. In Book 1, M becomes tensor M_ij when geometry crystallizes.

### Plain Language

> "Memory is how past scars shape future possibilities."

---

## DERIVED QUANTITY 0B.8 — Recursion Depth (n)

### Statement

> **Recursion depth n counts how many recursive distinctions an identity has survived.**

### Derivation

```
Recursion is implicit in Axiom 0A.1
σ accumulates across recursion (0A.3)
⟹ Recursion can be counted
⟹ n ∈ ℕ is the depth counter
```

### Properties

- n ∈ ℕ (natural numbers)
- n is NOT time
- n is nesting depth / fold count
- n increases monotonically for persistent identity

### Key Distinction

| Concept | Definition | Requires |
|---------|------------|----------|
| n (depth) | Recursion count | Only counting |
| t (time) | Duration | Dynamics (Book 2) |

### Plain Language

> "n counts how many levels deep the recursion has gone. It's not time — just depth."

---

## DERIVED QUANTITY 0B.9 — Lock (ℒ)

### Statement

> **Lock ℒ is the capacity of a persistent identity to absorb accumulated σ without reconfiguration.**

### Derivation (Necessity Proof)

```
σ accumulates irreversibly (0A.3)
Identity persists by carrying σ (0B.4)
Persistence cannot be unconditional (infinite σ → structure breaks)
⟹ There must be a capacity limit
⟹ This capacity is Lock (ℒ)
```

### Formal Definition

```
ℒ ≥ 0 (non-negative)

Identity I persists ⟺ σ < ℒ
Identity I transitions ⟺ σ = ℒ
```

### Source of Lock

```
ℒ = f(M, 𝒜, n)

Where:
  - Higher memory coherence → higher ℒ
  - Lower alignment → lower ℒ (strain)
  - Deeper recursion → potentially higher ℒ
```

### Properties

- ℒ is capacity, NOT control
- ℒ is NOT binary (not just locked/unlocked)
- ℒ is NOT rigidity (flexible systems can have high ℒ)
- ℒ has same dimension as σ (for comparison to work)

### Plain Language

> "Lock is how much scar an identity can carry before it has to change form."

---

## DERIVED QUANTITY 0B.10 — Transition Boundary (Δ)

### Statement

> **Delta Δ is the threshold condition at which σ = ℒ and reconfiguration becomes mandatory.**

### Derivation

```
σ < ℒ → identity persists
σ > ℒ → persistence impossible (violates capacity)
⟹ σ > ℒ cannot exist for persistent identity
⟹ At σ = ℒ, something must happen
⟹ That "something" is transition (Δ)
```

### Formal Definition

```
Δ ≡ {(I, n) : σ(n) = ℒ(n)}

At Δ:
  - Current configuration ineligible to continue
  - Reconfiguration mandatory
  - σ resolves to ρ_q (per 0A.4)
```

### Properties

- Δ is a **surface**, not a point
- Δ is where collapse terminates
- Δ is where value condenses
- Δ is NOT chosen (it's forced)

### Key Insight

Δ is **logical**, not temporal:
- It's the boundary of viability
- Crossing requires reconfiguration
- No "duration" involved

### Plain Language

> "Δ is the point of no return — where accumulated scar hits capacity and change becomes mandatory."

---

## Complete Derived Stack

| Symbol | Name | Derived From | Status |
|--------|------|--------------|--------|
| 𝒞 | Configuration Set | 0A.1 | ✅ |
| ≺ | Ordering Relation | 0A.2 | ✅ |
| Persistence | — | 0A.1, 0A.3 | ✅ |
| I | Identity | 0A.1, 0A.3 | ✅ |
| 𝒜 | Alignment | 0A.2, 0A.3 | ✅ |
| σ_θ | Accumulation Rate | 0A.3 | ✅ |
| M | Memory | 0A.3 | ✅ |
| n | Recursion Depth | 0A.1 | ✅ |
| ℒ | Lock | 0A.3 | ✅ |
| Δ | Transition | 0A.3, 0A.4 | ✅ |

---

## What Book 0B Does NOT Contain

| Forbidden | Reason | Appears In |
|-----------|--------|------------|
| ∇Φ as vector | No manifold yet | Book 1 |
| Time t | No dynamics yet | Book 2 |
| Agents | No intent yet | Book 2 |
| Equations | No operations yet | Book 1 |
| Conservation laws | No quantification yet | Book 1 |

---

## The Viability Condition (Summary)

The fundamental relationship emerging from Book 0B:

```
PERSIST:      σ(n) < ℒ(n)
TRANSITION:   σ(n) = ℒ(n)  →  Δ  →  ρ_q
IMPOSSIBLE:   σ(n) > ℒ(n)  (for persistent identity)
```

This is the **pre-dynamic constraint** from which all business physics will flow.

---

*"Everything in Book 0B must be logically unavoidable given Book 0A. No poetry, no business language yet. Only inevitability."*
