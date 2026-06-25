# Node specification template

One row per node in the tree. Copy and fill. Drop columns that don't apply, but keep Definition, Relationship, Controllability, and Thresholds for any KRI.

| Node | Definition | Relationship to parent | Driver type | Controllability | Data source | Owner | Frequency | Green | Amber | Red | Direction | Current | Target |
|------|------------|------------------------|-------------|-----------------|-------------|-------|-----------|-------|-------|-----|-----------|---------|--------|
| Expected Loss | Modeled $ loss over 12m | root | $ outcome | — | Risk engine | CRO | Monthly | <$10m | $10–15m | >$15m | ↑ worse | $12.4m | <$11m |
| PD | 12-month default probability | × | rate | External/Macro | Rating model | Credit Risk | Monthly | <2% | 2–3% | >3% | ↑ worse | 2.6% | <2.4% |
| LGD | Loss given default | × | rate | Partial | Recovery model | Workout | Quarterly | <35% | 35–45% | >45% | ↑ worse | 41% | <40% |
| EAD | Exposure at default | × | exposure ($) | Partial | Core banking | Portfolio Mgmt | Monthly | — | — | — | ↑ worse | $116m | — |

**Column notes**
- **Driver type**: volume · rate · price · mix · exposure · outcome.
- **Controllability**: `Lever` (business can move it directly) · `Partial` · `External/Macro` (hedge or buffer, don't "manage").
- **Direction**: `↑ worse` or `↓ worse` — which way breaches the threshold. Essential so RAG status is unambiguous.
- **Green/Amber/Red**: KRI bands. For levers, set them around the target; for externals, around the appetite/limit.
