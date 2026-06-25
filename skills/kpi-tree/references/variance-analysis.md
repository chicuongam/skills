# Variance analysis — attributing a movement to drivers

Read this when the user asks **"why did the metric move?"** or wants a **bridge / waterfall** from one period to the next. A KPI tree tells you the *structure*; variance analysis quantifies *how much each driver contributed* to the change.

The method depends on how the children combine.

## Additive trees: `P = A + B + C`
Trivial: `ΔP = ΔA + ΔB + ΔC`. Each driver's contribution is its own change. Present as a waterfall from P₀ to P₁.

## Multiplicative trees: `P = A × B × C`
A change in P comes from changes in all factors simultaneously; you must allocate the **interaction (cross) terms** fairly. Two standard methods:

### (a) Log / LMDI attribution (recommended — exact, no residual)
Contribution of factor A to the change in P:
```
Contrib_A = (P₁ − P₀) / (ln P₁ − ln P₀) × (ln A₁ − ln A₀)
```
and likewise for B, C. These contributions **sum exactly** to `P₁ − P₀`, with no leftover interaction term. This is the Logarithmic Mean Divisia Index — clean and order-independent. (Falls back gracefully; if P₁≈P₀ use the average value.)

### (b) Sequential (waterfall) attribution
Change one factor at a time, holding the not-yet-changed factors at their old value and the already-changed ones at their new value:
```
Contrib_A = (A₁ − A₀) × B₀ × C₀
Contrib_B = A₁ × (B₁ − B₀) × C₀
Contrib_C = A₁ × B₁ × (C₁ − C₀)
```
Sums exactly to ΔP, but is **order-dependent** (the factor you move first gets less interaction). State the order. Useful when there's a natural sequence (volume first, then rate).

**Example — Expected Loss bridge** (`EL = PD × LGD × EAD`): tells the committee "of the +$4.2m rise, +$3.1m was higher PD (macro), +$0.6m EAD growth, +$0.5m worse LGD." That sentence is the whole point of the tree.

## Ratio trees: `P = A / B`
`ΔP ≈ (ΔA / B₀) − (A₀/B₀²)·ΔB`, or just compute `A₁/B₁ − A₀/B₀` and attribute numerator vs denominator effects via the multiplicative method on `A × (1/B)`.

## Mix vs rate (the most important and most missed)
When a blended rate moved, decompose into **mix effect** (segment weights changed) and **rate effect** (within-segment rates changed). For blended rate `R = Σ wᵢ rᵢ` with weights wᵢ summing to 1:
```
Rate effect  = Σ w0ᵢ × (r1ᵢ − r0ᵢ)      # rates changed, old mix
Mix effect   = Σ (w1ᵢ − w0ᵢ) × r0ᵢ       # mix changed, old rates
Interaction  = Σ (w1ᵢ − w0ᵢ)(r1ᵢ − r0ᵢ)  # usually small; fold into rate or report
```
This separates **"each segment got riskier"** from **"we wrote more of the risky segment."** Failing to split these is how teams misdiagnose movements (Simpson's paradox). Always offer mix/rate split when the root is a blended ratio across segments.

## Output for variance analysis
1. A **waterfall/bridge**: start bar (P₀), one bar per driver contribution (signed), end bar (P₁). Render via the visualizer or, on request, the **xlsx**/**pptx** skills.
2. A short **attribution table**: driver · contribution ($ or bps) · % of total move · direction.
3. A one-line **narrative**: "The +X move was driven mainly by [largest driver]; [partial offset]." Lead with the dominant driver.

Always confirm the contributions **sum to the actual total change** before presenting — that reconciliation is the credibility check.
