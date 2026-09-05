# 04 — Social Security

**Step 4 of the year loop** · Rail: **nominal**

---

## What this computes

Two separate numbers that must not be confused:

1. **The gross benefit received** — depends only on earnings history, claiming age, and COLA.
2. **The taxable portion of that benefit** — depends on all other income.

They are computed at different steps. There is **no circular dependency** between them.

---

## PART A — THE BENEFIT

The chain has five links. Do them in order.

```
Earnings history
   → (1) index each year
   → (2) take highest 35 → AIME
   → (3) apply bend points → PIA
   → (4) adjust for claiming age
   → (5) apply COLA forward
   = benefit received in year n
```

---

### Step 1 — Index the earnings history

Each year of covered earnings is restated into wage levels as of the year the worker **turns 60**.

```
indexingFactor(y) = AWI(yearWorkerTurns60) / AWI(y)
indexedEarnings(y) = MIN(actualEarnings(y), wageBase(y)) × indexingFactor(y)
```

Two rules that are easy to miss:

- Earnings are first **capped at that year's Social Security wage base** before indexing. (2026 base: **$184,500**.)
- Earnings in the year the worker turns 60 **and every year after** are used at **face value** — indexing factor of exactly 1.0.

### Step 2 — AIME (Average Indexed Monthly Earnings)

```
AIME = FLOOR( sum of highest 35 indexed years / 420 )
```

- 420 = 35 years × 12 months.
- If the worker has fewer than 35 years of earnings, **the missing years count as zero.** They still divide by 420. This is why a short career depresses the benefit so heavily.
- Round **down** to the next lower whole dollar.

### Step 3 — PIA (Primary Insurance Amount) via bend points

**2026 bend points: $1,286 and $7,749** — source: Federal Register 2025-19763.

```
PIA = 0.90 × MIN(AIME, 1286)
    + 0.32 × MAX(0, MIN(AIME, 7749) − 1286)
    + 0.15 × MAX(0, AIME − 7749)

PIA = FLOOR_TO_DIME(PIA)
```

**Worked number** — AIME of $10,000:

| Slice | Amount | Rate | Result |
|---|---|---|---|
| First $1,286 | $1,286 | 90% | $1,157.40 |
| $1,286 → $7,749 | $6,463 | 32% | $2,068.16 |
| Above $7,749 | $2,251 | 15% | $337.65 |
| **PIA** | | | **$3,563.20**/month |

(Rounded down to the dime from $3,563.21.)

### Where the bend points come from — verify this yourself

The bend points are not arbitrary. They are the 1979 base amounts indexed by wage growth:

```
bendPoint1 = ROUND( 180   × AWI(eligibilityYear − 2) / 9779.44 )
bendPoint2 = ROUND( 1085  × AWI(eligibilityYear − 2) / 9779.44 )
```

Check for 2026, using AWI(2024) = $69,846.57:

```
ratio = 69,846.57 / 9,779.44 = 7.142184
180   × 7.142184 = 1,285.59  → $1,286   ✓ matches published
1,085 × 7.142184 = 7,749.27  → $7,749   ✓ matches published
```

Both reproduce the official figures exactly. **You can compute future years' bend points the same way** once the AWI is published — you do not have to wait for a table.

> **The bend points are locked at the year the worker turns 62** (the eligibility year), not the year they claim. A worker turning 62 in 2026 uses $1,286/$7,749 forever, even if they claim at 70.

### Step 4 — Claiming age adjustment

Full Retirement Age is **67** for anyone born in 1960 or later.

**Claiming early (before FRA) — permanent reduction:**

```
monthsEarly = (FRA − claimAge) × 12

reduction = (5/9 of 1%) × MIN(monthsEarly, 36)
          + (5/12 of 1%) × MAX(0, monthsEarly − 36)

benefit = PIA × (1 − reduction)
```

**Claiming late (after FRA) — delayed retirement credits:**

```
monthsDelayed = (claimAge − FRA) × 12        [capped at age 70]
credit  = (2/3 of 1%) × monthsDelayed
benefit = PIA × (1 + credit)
```

**The full table for FRA 67:**

| Claim age | Adjustment | % of PIA |
|---|---|---|
| 62 | −30.0% | 70.0% |
| 63 | −25.0% | 75.0% |
| 64 | −20.0% | 80.0% |
| 65 | −13.33% | 86.67% |
| 66 | −6.67% | 93.33% |
| **67 (FRA)** | **0%** | **100%** |
| 68 | +8% | 108% |
| 69 | +16% | 116% |
| 70 | **+24%** | **124%** |

> Delayed credits **stop at 70**. There is no benefit to claiming later. Cap the calculation.

### Step 5 — COLA

**2026 COLA: 2.8%.**

```
benefit(n) = adjustedBenefit × PRODUCT of (1 + COLA(y)) for each year y from eligibility to n
```

For projection, assume a constant long-run COLA (use the same inflation assumption, ~2.5%):

```
benefit(n) = adjustedBenefit × (1 + colaAssumption)^(n − claimYear)
```

> **Apply COLA AFTER the claiming adjustment, not before.** COLAs actually accrue from age 62 regardless of when you claim, but applying them to the already-adjusted benefit gives the identical result and is simpler. Applying COLA first and then reducing produces the same number only if you are careful — do it in the stated order and avoid the risk.

### The override

When the client provides their SSA statement, skip Steps 1–3 entirely:

```
IF ssaStatementBenefit IS PROVIDED:
    PIA = ssaStatementBenefitAtFRA
    → go straight to Step 4
ELSE:
    compute AIME → PIA from earnings history
```

The SSA statement figure is already a PIA at FRA, so it enters at exactly the same point. **Flag which path was used** in the output so an advisor can see whether the number is computed or client-supplied.

---

## PART B — TAXATION OF THE BENEFIT

### Provisional income

```
provisionalIncome = AGI excluding Social Security
                  + tax-exempt interest (municipal bonds)
                  + 0.50 × grossSocialSecurityBenefit
```

### The thresholds — FROZEN, NEVER INDEXED

| Filing status | Tier 1 | Tier 2 |
|---|---|---|
| Single / HoH | $25,000 | $34,000 |
| Married filing jointly | $32,000 | $44,000 |
| Married filing separately (lived together) | $0 | $0 |

> These have not moved since **1983 and 1993**. They are not inflation-adjusted and there is no mechanism to adjust them. In a 48-year projection this is the single most consequential frozen number in the entire tax code — nearly every retiree eventually hits the 85% tier.

### Formula

```
IF provisional <= tier1:
    taxable = 0

ELSE IF provisional <= tier2:
    taxable = MIN( 0.50 × (provisional − tier1),
                   0.50 × benefit )

ELSE:
    taxable = MIN( 0.85 × (provisional − tier2)
                   + MIN( 0.50 × (tier2 − tier1), 0.50 × benefit ),
                   0.85 × benefit )
```

**The cap is 85%.** At least 15% of the benefit is always tax-free.

**Worked number** — MFJ, $40,000 benefit, $60,000 other income:

```
provisional = 60,000 + 0.50 × 40,000 = 80,000
80,000 > 44,000  → tier 3

taxable = MIN( 0.85 × (80,000 − 44,000) + MIN(0.50 × 12,000, 0.50 × 40,000),
               0.85 × 40,000 )
        = MIN( 30,600 + 6,000, 34,000 )
        = MIN( 36,600, 34,000 )
        = 34,000
```

$34,000 of the $40,000 benefit is taxable — the 85% cap binds.

### State treatment

**The large majority of states do not tax Social Security**, including California, New York, Texas, and Florida. A small and shrinking number do. Apply the state rule separately from the federal calculation — do not reuse the federal taxable amount.

---

## PART C — WHEN THE HOUSEHOLD CHANGES

### Death of a spouse — the survivor gets the higher benefit, not both

```
survivorBenefit = MAX(ownBenefit, deceasedSpouseBenefit)
householdBenefit = survivorBenefit          ← the smaller benefit is LOST
```

> This is the single most misunderstood rule in retirement planning. A couple receiving $42,758 and $28,000 does **not** leave the survivor with $70,758. It leaves them with **$42,758**. The household loses $28,000 a year, permanently.

**Survivor FRA is not the same as retirement FRA:**

| Born | Survivor FRA |
|---|---|
| 1957 | 66 and 2 months |
| 1958 | 66 and 4 months |
| 1959 | 66 and 6 months |
| 1962 and later | 67 |

```
claim at 60         → 71.5% of the deceased's benefit
claim at survivor FRA → 100%
```

**The switching strategy — two separate entitlements:**

```
Survivor benefit and the survivor's OWN retirement benefit are separate.
They may claim one early and switch to the other later.

Typical: claim the SURVIVOR benefit at 60, let their OWN benefit grow
         with delayed credits, then switch at 70.
Or the reverse, if their own benefit is the smaller one.
```

> The model must test **both orders** and take the higher lifetime total. Assuming a single claim date understates the benefit for most widows and widowers.

### Divorce — the ex-spouse benefit

```
QUALIFIES IF ALL OF:
    the marriage lasted at least 10 years
    the claimant is currently unmarried
    the claimant is age 62 or older
```

```
exSpouseBenefit does NOT reduce the worker's own benefit
   nor the benefit of the worker's current spouse
```

> A worker can have an ex-spouse **and** a current spouse both drawing on their record with no reduction to anyone. Remarriage by the **claimant** ends their ex-spouse benefit — but remarriage after age 60 does **not** end a **survivor** benefit.

## The planning window this creates

Between retirement and the RMD age (73 or 75), a client may have very low provisional income. This is the window where Roth conversions cost the least. Once RMDs begin, they inflate provisional income, push the benefit to 85% taxable, and can trip IRMAA at the same time. **The model must show these three effects landing together** — that compound is the entire argument for pre-RMD planning.

---

## Ordering traps

| Don't | Do |
|---|---|
| Index the $25,000/$32,000/$34,000/$44,000 thresholds | Leave them frozen forever |
| Add the gross benefit to taxable income | Add only the taxable portion |
| Use the wage base of the current year to cap old earnings | Use each year's own wage base |
| Index earnings from the year of age 62 | Index to the year of age **60** |
| Give delayed credits past age 70 | Cap at 70 |
| Use the claim year's bend points | Use the year the worker turns **62** |
| Assume 35 years of earnings exist | Fill missing years with zero |
| Apply COLA before the claiming adjustment | Adjust for claiming first, then COLA |
| Add both benefits together after a death | The survivor keeps only the **higher** of the two |
| Use retirement FRA for a survivor claim | Survivor FRA differs — see the table above |
| Assume one claim date for a widow(er) | Test survivor-first and own-first; take the higher lifetime total |
| End a survivor benefit on remarriage after 60 | Remarriage at 60+ does **not** end a survivor benefit |

---

## Sources

| What | Source | Google this |
|---|---|---|
| 2026 bend points, COLA, wage base, AWI | [Federal Register 2025-19763](https://www.federalregister.gov/documents/2025/11/03/2025-19763/cost-of-living-increase-and-other-determinations-for-2026) | `Cost-of-Living Increase and Other Determinations for 2026` |
| PIA formula | [SSA — Primary Insurance Amount](https://www.ssa.gov/oact/cola/piaformula.html) | `SSA primary insurance amount bend points formula` |
| Bend point history and derivation | [SSA — Benefit Formula Bend Points](https://www.ssa.gov/oact/cola/bendpoints.html) | `SSA benefit formula bend points` |
| Early / delayed adjustment rates | [SSA — Early or Late Retirement](https://www.ssa.gov/oact/quickcalc/early_late.html) · [20 CFR 404.313](https://www.ssa.gov/OP_Home/cfr20/404/404-0313.htm) | `SSA early or late retirement reduction factors` |
| Taxation of benefits | [IRS Publication 915](https://www.irs.gov/forms-pubs/about-publication-915) · [CRS RL32552](https://www.congress.gov/crs-product/RL32552) | `IRS Publication 915 Social Security benefits taxable` |
| Thresholds never indexed | [CRS IF11397](https://www.congress.gov/crs-product/IF11397) | `CRS Social Security Benefit Taxation Highlights` |
| Survivor benefits, survivor FRA | [SSA — Survivor benefit amounts](https://www.ssa.gov/survivor/amount) · [Survivor FRA](https://www.ssa.gov/survivor/full-retirement-age-survivor) | `SSA survivor benefit full retirement age` |
| Divorced-spouse benefit, 10-year rule | [SSA — prior marriage](https://www.ssa.gov/help/iClaim_marriagePrior.html) · [20 CFR 404.331](https://www.ssa.gov/OP_Home/cfr20/404/404-0331.htm) | `SSA divorced spouse benefit 10 year marriage` |
