# 11 — Loss Limitations, K-1 Attributes, and Year-to-Year Carryforwards

**Inserted between Step 5 and Step 6 of the year loop** · Rail: **nominal**

---

## Why this document exists

Modules 01–08 model a *simple* return: salary, retirement accounts, Social Security, RMDs, one rental. The moment a client has a **K-1** — from an S-corp practice or a partnership — that model produces **wrong numbers**.

A K-1 loss cannot simply be added to AGI. It must survive **four sequential gates** first, and whatever is blocked at each gate is **suspended in a different bucket with a different release rule**. Those buckets, plus NOLs, capital losses, negative QBI and the AMT credit, must then be **carried forward every year from age 42 to age 90**.

Get the sequence wrong and you either deduct a loss that isn't deductible, or count the same loss twice.

---

## 1. The four gates

```
Loss for the year
        │
        ▼
PRE-GATE A  §280A PERSONAL USE        (real estate only)
        │   personal use > MAX(14 days, 10% of rental days)?
        │   if YES → deductions capped at rental income, STOP. Nothing
        │            reaches the gates below.
        ▼
PRE-GATE B  CLASSIFICATION            (real estate only)
        │   average stay ≤ 7 days?  → not a rental activity
        │   material participation? → decides passive vs non-passive
        │   REPS?                    → removes "automatically passive"
        ▼
GATE 1  BASIS            §704(d) partnerships · §1366(d) S-corps
        │  blocked → suspendedBasis
        ▼
GATE 2  AT-RISK          §465
        │  blocked → suspendedAtRisk
        ▼
GATE 3  PASSIVE          §469
        │  blocked → suspendedPassive
        │  NON-PASSIVE losses SKIP this gate entirely
        ▼
GATE 4  EXCESS BUSINESS LOSS   §461(l)
        │  blocked → becomes an NOL carryforward
        │  non-passive real estate losses DO meet this gate
        ▼
   Deductible against AGI
```

> **The two pre-gates apply to real estate only**, and they run *before* basis. A property failing §280A never reaches the gates at all. Full mechanics in [07-REAL-ESTATE-EQUITY.md](07-REAL-ESTATE-EQUITY.md).

> **A non-passive short-term rental loss skips gate 3 but still meets gate 4.** Clearing the 7-day test does **not** exempt the loss from the $512,000 excess business loss cap.

**The rule that prevents double-counting:**

> A loss blocked at gate *n* **never reaches** gate *n+1* that year. Each gate sees only what the gate above it let through.

**The conservation identity — check this every activity, every year:**

```
allowedThisYear
  + Δ suspendedBasis
  + Δ suspendedAtRisk
  + Δ suspendedPassive
  = lossEnteringTheGates
```

If that identity fails, the model is either losing a loss or counting one twice.

---

## 2. GATE 1 — Basis

**In plain English.** You cannot deduct more than you have invested. Basis is your investment account balance in the entity — it goes up with income and contributions, down with losses and distributions. It can never go below zero.

```
allowedGate1  = MIN(loss, basisBeforeLoss)
suspendedBasis = loss − allowedGate1
basisAfter     = basisBeforeLoss − allowedGate1
```

### Partnership vs S-corp — the difference that matters

| | Partnership §704(d) | S-corp §1366(d) |
|---|---|---|
| Basis includes | Capital **+ your share of partnership liabilities** (§752) | Stock basis **+ direct loans you personally made to the company** |
| Entity-level debt | **Increases** your basis | Does **not** increase your basis |
| Guaranteeing company debt | n/a | Does **not** create basis until you actually pay |

> This is the single most common K-1 modelling error. A partner in a leveraged real estate partnership gets basis from the mortgage; an S-corp shareholder gets **nothing** from company debt no matter how much they guarantee.

### Order of basis reductions

Apply in this order — it changes how much loss survives:

```
1. Distributions
2. Nondeductible expenses
3. Losses and deductions
```

**Full detail →** [26 U.S.C. §704(d)](https://www.law.cornell.edu/uscode/text/26/704) · [26 U.S.C. §1366(d)](https://www.law.cornell.edu/uscode/text/26/1366)

---

## 3. GATE 2 — At-risk (§465)

**In plain English.** Basis says "how much is in the account". At-risk says "how much could you actually lose". Money you borrowed but aren't personally on the hook for doesn't count — you have nothing at risk.

```
allowedGate2   = MIN(allowedGate1, atRiskAmount)
suspendedAtRisk = allowedGate1 − allowedGate2
atRiskAfter     = atRiskAmount − allowedGate2
```

**At-risk generally includes:** cash contributed, basis of property contributed, and borrowed amounts where you are **personally liable** or have pledged property as security.

**It excludes:** nonrecourse debt, amounts protected by stop-loss agreements or guarantees.

### The real estate carve-out

```
IF debt is qualified nonrecourse financing (§465(b)(6)):
    it COUNTS toward at-risk even though nobody is personally liable
```

Requires: borrowed for holding **real property**, from a **qualified person** (an unrelated commercial lender), nobody personally liable, and not convertible debt.

> Without this carve-out, almost no leveraged real estate loss would ever be deductible. With it, most are — which is why misclassifying ordinary nonrecourse debt as *qualified* is a common and expensive error.

### Negative at-risk recapture

```
IF atRiskAmount < 0 at year end:
    include the shortfall in GROSS INCOME this year
    treat the same amount as a deduction allocable to the activity NEXT year
```

This happens when distributions exceed investment. It is income, not a loss.

**Full detail →** [26 U.S.C. §465](https://www.law.cornell.edu/uscode/text/26/465) · [Form 6198](https://www.irs.gov/forms-pubs/about-form-6198)

---

## 4. GATE 3 — Passive activity (§469)

**In plain English.** If you don't materially participate in a business, it is "passive". Passive losses can only offset passive income — not your salary, not your dividends. Anything left over waits until the activity produces income or you sell it.

```
passiveLossPool   = SUM of allowedGate2 across all PASSIVE activities
passiveIncomePool = SUM of income from all PASSIVE activities

allowedGate3    = MIN(passiveLossPool, passiveIncomePool + specialAllowance)
suspendedPassive = passiveLossPool − allowedGate3
```

Allocate `allowedGate3` back to activities **pro rata** by each activity's share of the loss pool.

### Passive or not?

| Status | Test | Result |
|---|---|---|
| **Material participation** | 7 tests; commonly >500 hrs/yr, or substantially all participation | **Non-passive** |
| **Active participation** (rental only) | Lower bar — approve tenants, set terms, arrange repairs | Passive, but unlocks the $25,000 allowance |
| **Real estate professional** (§469(c)(7)) | >750 hrs **and** >half of personal services in real property trades | Rentals leave "per se passive"; then tested for material participation |
| Everything else | — | **Passive** |

### The $25,000 rental allowance

```
specialAllowance = MAX(0, 25000 − 0.50 × MAX(0, MAGI − 100000))
```

| MAGI | Allowance |
|---|---|
| ≤ $100,000 | $25,000 |
| $125,000 | $12,500 |
| ≥ $150,000 | **$0** |

> **Not indexed for inflation.** Fixed since 1986. For the high-income clients this roadmap targets it is **always zero** — but it must still be in the model, because early or late years can dip below the threshold.

### Release triggers

| Event | What happens |
|---|---|
| Activity produces passive income | Suspended passive losses offset it |
| Other passive activities produce income | Same pool — offsets across activities |
| **Complete taxable disposition to an unrelated party** | **ALL** suspended passive losses for that activity release, against **any** income |
| Partial sale (even 99%) | **No release** |
| Sale to a related party | **No release** |
| Becoming a real estate professional | **No release** of prior-year suspended losses — not retroactive |

**Full detail →** [26 U.S.C. §469](https://www.law.cornell.edu/uscode/text/26/469) · [Form 8582](https://www.irs.gov/forms-pubs/about-form-8582)

---

## 5. GATE 4 — Excess business loss (§461(l))

**In plain English.** Even after a loss survives all three gates, there is a cap on how much business loss can offset non-business income like salary and investments. Anything above the cap becomes an NOL for next year.

```
aggregateBusinessLoss = SUM of allowed business losses − SUM of business income
excessBusinessLoss    = MAX(0, aggregateBusinessLoss − threshold)

allowedThisYear = aggregateBusinessLoss − excessBusinessLoss
nolCarryforward = nolCarryforward + excessBusinessLoss
```

### 2026 thresholds — note the direction

| Year | Single | MFJ |
|---|---|---|
| 2025 | $313,000 | $626,000 |
| **2026** | **$256,000** | **$512,000** |

> **The threshold goes DOWN in 2026.** OBBBA reset the inflation-indexing base and erased several years of creep — while also making the rule **permanent** (the scheduled 2028 sunset is gone). This is counterintuitive and materially worsens loss-year outcomes. A model carrying 2025 figures forward will overstate deductible losses by $114,000 for a couple.

> Only losses that survived gates 1–3 reach here. Passive losses already suspended never enter the §461(l) aggregation.

**Full detail →** [26 U.S.C. §461(l)](https://www.law.cornell.edu/uscode/text/26/461) · [Form 461 instructions](https://www.irs.gov/instructions/i461)

---

## 6. After the gates — AGI

```
AGI = w2Income
    + nonpassiveBusinessIncome        ← after gates 1, 2, 4
    − allowedNonpassiveBusinessLoss   ← after gates 1, 2, 4
    + passiveIncome
    − allowedPassiveLoss              ← after gate 3
    + portfolioIncome
    + taxableSocialSecurity           ← §7 below
    + rmd                             ← module 05
    − pretaxContributions             ← module 03
    − deductibleSelfEmploymentTax
```

---

## 7. Social Security when RMD and SSA-1099 land in the same year

**In plain English.** From the RMD age onward the client has two forced income streams at once. The RMD does not just get taxed itself — it pushes the Social Security benefit into a higher taxable band, and can trip IRMAA two years later. Three effects, one trigger.

```
provisionalIncome = AGI excluding Social Security
                  + tax-exempt interest
                  + 0.50 × grossSocialSecurityBenefit
```

**The RMD is in "AGI excluding Social Security".** So the sequence is strictly:

```
1. Compute the gross benefit           (module 04)
2. Compute the RMD                     (module 05)
3. Compute provisional income          ← includes the RMD
4. Compute the taxable portion         (module 04 §Part B)
5. Only THEN add it to AGI
```

> **There is no circularity.** The benefit amount depends only on earnings history, claiming age and COLA — never on tax. Do not iterate.

**Allowed passive losses reduce AGI, so they reduce provisional income too** — which is one of the few levers that can pull a benefit back below the 85% band.

**Full detail →** [04-SOCIAL-SECURITY.md](04-SOCIAL-SECURITY.md) · [05-RMD.md](05-RMD.md)

---

## 8. NOL carryforward

```
nolDeduction = MIN(nolCarryforward, 0.80 × taxableIncomeBeforeNOL)
nolCarryforward = nolCarryforward − nolDeduction
```

| Rule | Post-TCJA |
|---|---|
| Limit | **80%** of taxable income |
| Carryforward | **Indefinite** |
| Carryback | **None** |

> The 80% cap means **20% of taxable income is always taxed**, no matter how large the NOL balance. A model that lets an NOL wipe out income entirely is wrong.

**Full detail →** [26 U.S.C. §172](https://www.law.cornell.edu/uscode/text/26/172) · [Form 172](https://www.irs.gov/instructions/i172)

---

## 9. Capital loss carryforward

```
netShortTerm = shortTermGains − shortTermLosses
netLongTerm  = longTermGains  − longTermLosses
netCapital   = netShortTerm + netLongTerm

IF netCapital < 0:
    deductedAgainstOrdinary = MIN(3000, −netCapital)
    capitalLossCarryforward = −netCapital − deductedAgainstOrdinary
```

| Rule | Value |
|---|---|
| Annual ordinary-income offset | **$3,000** ($1,500 MFS) |
| Indexed? | **No — unchanged since 1978** |
| Carryforward | **Indefinite** |
| Character | **Preserved** — short-term stays short-term |
| At death | **Dies with the taxpayer.** Cannot pass to heirs or the estate |

> Character preservation matters: a short-term carryforward nets first against short-term gains, which are taxed at ordinary rates. Merging the two buckets understates tax.

> **The death rule interacts with module 08.** An unused capital loss carryforward is worth nothing to the estate. If a client is carrying a large balance late in life, realising gains to absorb it is a real strategy — and the roadmap should surface it.

**Full detail →** [26 U.S.C. §1211](https://www.law.cornell.edu/uscode/text/26/1211) · [§1212](https://www.law.cornell.edu/uscode/text/26/1212)

---

## 10. QBI (§199A) after the gates

**In plain English.** The 20% pass-through deduction is computed on income that actually made it through the gates — and if the total is negative, it becomes a penalty against next year's deduction.

```
qbiDeduction = MIN(
    0.20 × combinedQBI,
    0.20 × (taxableIncomeBeforeQBI − netCapitalGain)
)
```

### Negative QBI carries forward

```
IF combinedQBI < 0:
    qbiDeduction = 0
    negativeQBICarryforward = combinedQBI      ← treated next year as a
                                                 separate trade or business
```

It reduces future positive QBI **before** any deduction is computed, and carries **indefinitely**.

### Released suspended losses reduce QBI

```
IF a suspended loss is released this year:
    it reduces QBI this year (if it arose in 2018 or later)
    it does NOT affect QBI     (if it arose before 2018)
```

> A client who sells a rental and releases ten years of suspended passive losses gets a large deduction — **and** a large QBI reduction in the same year. Model both.

**Full detail →** [02-TAXES.md](02-TAXES.md) · [26 U.S.C. §199A](https://www.law.cornell.edu/uscode/text/26/199A)

---

## 11. NIIT — a separate calculation, not a reuse

**In plain English.** The 3.8% investment surtax uses its own income definition. You cannot reuse the regular-tax numbers.

```
netInvestmentIncome = interest + dividends + capitalGains
                    + PASSIVE business income
                    + annuities + royalties
                    − properly allocable deductions

niit = 0.038 × MIN(netInvestmentIncome, MAX(0, MAGI − threshold))
```

| In NII | Not in NII |
|---|---|
| Passive business income | Wages |
| Portfolio income | Self-employment income |
| Rental (if passive) | Social Security |
| | **Distributions from IRAs and qualified plans** |

> **The RMD is excluded from NII but included in MAGI.** So it cannot be taxed by NIIT directly, yet it can push *other* investment income over the threshold. Both effects are real and both must be modelled.

### Two traps

**Self-rental recharacterisation** — renting property to your own business in which you materially participate makes that income **non-passive** under Reg. §1.469-2(f)(6), which takes it **out of NII** entirely.

**Suspended losses in NII** — a released suspended loss from a former passive activity is deductible against NII, but **only to the extent** that activity's income or gain is itself in NII.

**Full detail →** [Form 8960 instructions](https://www.irs.gov/instructions/i8960) · [Reg. §1.1411-4](https://www.law.cornell.edu/cfr/text/26/1.1411-4)

---

## 12. AMT — the parallel rail

**In plain English.** Run the entire return a second time under different rules. Pay whichever is higher. If AMT wins, the difference becomes a credit you may recover in later years.

```
AMTI = regularTaxableIncome
     + standardDeduction (disallowed for AMT)
     + SALT deduction (disallowed)
     + ISO bargain element on shares still held at year end
     + private activity bond interest
     ± depreciation differences
     ± passive activity adjustments

exemption = MAX(0, baseExemption − 0.50 × MAX(0, AMTI − phaseoutStart))

amtBase = MAX(0, AMTI − exemption)
TMT     = 0.26 × MIN(amtBase, 244500) + 0.28 × MAX(0, amtBase − 244500)

amtDue  = MAX(0, TMT − regularTax)
minimumTaxCredit = minimumTaxCredit + amtDue(from deferral items)
```

### 2026 figures

| Item | Single | MFJ |
|---|---|---|
| Exemption | $90,100 | $140,200 |
| Phaseout starts | $500,000 | $1,000,000 |
| **Phaseout rate** | **50%** | **50%** |
| 28% bracket starts | $244,500 | $244,500 ($122,250 MFS) |

> **Two OBBBA changes bite in 2026.** The phaseout thresholds reverted to 2018 levels ($500k/$1M, down from roughly $640k/$1.28M), and the phaseout rate **doubled from 25% to 50%**. Together they mean the exemption vanishes far faster. Any model using 2025 AMT parameters will understate AMT for high earners.

### The minimum tax credit

AMT paid on **deferral** items (ISO exercise, depreciation timing) generates a credit carried forward indefinitely, usable in years when regular tax exceeds tentative minimum tax. AMT paid on **exclusion** items (SALT, standard deduction) generates **no** credit.

**Full detail →** [26 U.S.C. §55](https://www.law.cornell.edu/uscode/text/26/55)–[§59](https://www.law.cornell.edu/uscode/text/26/59) · [Form 6251](https://www.irs.gov/forms-pubs/about-form-6251)

---

## 13. The carryforward state — what moves from year to year

This is the object that must persist from age 42 to age 90. **Year n's closing state is year n+1's opening state, field for field.**

### Per activity (one record per K-1, per rental, per business)

```
activityId
entityType            partnership | s-corp | rental | soleProp
isPassive             true | false          ← re-test every year
materialParticipation true | false

basis                 running balance
atRiskAmount          running balance

suspendedBasis        §704(d) / §1366(d) bucket
suspendedAtRisk       §465 bucket
suspendedPassive      §469 bucket
```

### Global

```
nolCarryforward             §172
capitalLossShortTerm        §1212 — tracked separately
capitalLossLongTerm         §1212 — tracked separately
negativeQBICarryforward     §199A
minimumTaxCredit            §53

pretaxRetirementBalance     module 03  → drives next year's RMD
rothBalance                 module 03
taxableBalance              module 03
priorYearEndPretaxBalance   module 05  → the RMD divisor base
insuranceCashValue          module 06
insuranceLoanBalance        module 06
mortgageBalance             module 07
accumulatedDepreciation     module 07  → drives recapture at sale
```

### The three buckets have three different fates

This is why they cannot be merged into one "suspended losses" number:

| Bucket | On continued operation | On complete taxable disposition |
|---|---|---|
| **suspendedPassive** §469 | Released as passive income arises | **Fully released** against any income |
| **suspendedAtRisk** §465 | Carries forward indefinitely | **Offsets the gain** — disposition gain is income from the activity |
| **suspendedBasis** §704(d) | Released when basis is restored | **EXPIRES — permanently lost.** Gain does not restore basis |

> A model that lumps them together will either resurrect a dead loss or destroy a live one.

---

## 14. Anti-double-count and circularity rules

**Rule 1 — Conservation.** Every activity, every year:

```
allowed + Δ suspendedBasis + Δ suspendedAtRisk + Δ suspendedPassive = lossEnteringGates
```

**Rule 2 — One gate only.** A loss blocked at gate *n* does not appear in gate *n+1*'s input that year.

**Rule 3 — Release once.** A released suspended loss is removed from its bucket in the same step it enters income. Never leave it in both.

**Rule 4 — Income is consumed, not reused.** When activity income restores basis and at-risk and frees a suspended loss, that income is **spent**. It is not *also* available as passive income to free older suspended passive losses. (See year 2 of the worked example — this is the subtlest trap in the whole module.)

**Rule 5 — No circular dependencies.** Four places where one is tempting:

| Looks circular | Resolution |
|---|---|
| SS benefit ↔ provisional income | One-directional. Benefit depends only on earnings/claiming/COLA |
| QBI ↔ taxable income | QBI limit uses taxable income computed **before** the QBI deduction |
| AMT ↔ regular tax | Parallel rail. AMT never feeds back into the regular calculation |
| RMD ↔ balance | RMD uses the **prior** 31 December balance, never the current one |

---

## 15. Worked example — the age-42 client, with K-1s

Extending the [module 09](09-WORKED-EXAMPLE.md) client: age 42, MFJ, $420,000 W-2 — now with four business activities layered on.

> **Why the tax differs from module 09.** Module 09's baseline client has W-2 income only: AGI $420,000, federal tax $78,268. Here the same person also has $180,000 of S-corp income and $20,000 of portfolio income, so AGI is $620,000 and federal tax is $143,268. Same client, more income — not a contradiction.

| Activity | Type | Participation | Year 1 K-1 | Basis | At-risk |
|---|---|---|---|---|---|
| **A** Consulting firm (SSTB) | 1120-S K-1 | Material → **non-passive** | **+$180,000** | ample | ample |
| **B** Real estate LP | 1065 K-1 | None → **passive** | **−$120,000** | $80,000 | $50,000 |
| **C** Rental property | Schedule E | Active only → **passive** | **−$30,000** | ample | ample |
| **D** Passive LP | 1065 K-1 | None → **passive** | **+$60,000** | ample | ample |

Plus $20,000 of portfolio income.

### Year 1 (age 42) — all four gates

```
GATE 1  basis
  B: loss 120,000 vs basis 80,000  → passes 80,000, suspendedBasis 40,000
  C: loss  30,000 vs basis ample   → passes 30,000, suspendedBasis 0

GATE 2  at-risk
  B: 80,000 vs at-risk 50,000      → passes 50,000, suspendedAtRisk 30,000
  C: 30,000 vs at-risk ample       → passes 30,000, suspendedAtRisk 0

GATE 3  passive
  passive loss pool   = 50,000 (B) + 30,000 (C) = 80,000
  passive income pool = 60,000 (D)
  special allowance   = 0        ← MAGI far above $150,000
  allowed 60,000, suspendedPassive 20,000
  pro rata:  B 37,500 allowed / 12,500 suspended
             C 22,500 allowed /  7,500 suspended

GATE 4  excess business loss
  net non-passive business income = +180,000 → no EBL (threshold 512,000)
```

**Conservation check:**

| Activity | Allowed | susp. Basis | susp. At-risk | susp. Passive | Total | Original |
|---|---|---|---|---|---|---|
| B | $37,500 | $40,000 | $30,000 | $12,500 | **$120,000** | $120,000 ✓ |
| C | $22,500 | $0 | $0 | $7,500 | **$30,000** | $30,000 ✓ |

**Downstream:**

```
AGI = 420,000 W-2 + 180,000 S-corp + 20,000 portfolio + 0 net passive = 620,000
Taxable income = 620,000 − 32,200 = 587,800

QBI      consulting is an SSTB; TI 587,800 > 553,500 phase-out end → deduction $0
Regular federal tax                                            = $143,268
NIIT     3.8% × MIN(20,000 NII, 620,000 − 250,000)             = $760

AMT      AMTI 620,000, exemption 140,200 (no phaseout below 1,000,000)
         base 479,800 → TMT 129,454  <  regular 143,268        → no AMT
```

> Note the net passive line is **zero**, not +$60,000. D's income was fully consumed absorbing B and C's losses.

### Year 1 variant — AMT actually firing

Same year, but the client exercises ISOs with a **$300,000** bargain element and holds the shares past year end:

```
AMTI = 587,800 + 32,200 std + 300,000 ISO = 920,000
exemption 140,200 (still below the 1,000,000 phaseout)
base 779,800 → TMT = 0.26 × 244,500 + 0.28 × 535,300 = 213,454
AMT due = 213,454 − 143,268 = $70,186
minimumTaxCredit carried forward = $70,186   ← ISO spread is a deferral item
```

### Year 2 (age 43) — B allocates income; capacity restores

```
opening B:  basis 0, at-risk 0
            suspended: basis 40,000, at-risk 30,000, passive 12,500

K-1 income +40,000  → basis 40,000, at-risk 40,000

GATE 1  releases 40,000 from suspendedBasis  → basis 0, suspendedBasis 0
GATE 2  40,000 freed + 30,000 already waiting = 70,000 seeking at-risk 40,000
        → passes 40,000, suspendedAtRisk stays 30,000
GATE 3  activity income 40,000 − released loss 40,000 = NET 0 passive

closing B:  basis 0, at-risk 0
            suspended: basis 0, at-risk 30,000, passive 12,500
```

> **This is Rule 4 in action.** The $40,000 of income was consumed restoring basis and at-risk. It is **not** also available as passive income to free the $12,500 of older suspended passive losses. Counting it twice is the most common error in this entire module.

### Year 3 (age 44) — complete taxable disposition of B, $90,000 gain

```
opening suspended:  basis 0, at-risk 30,000, passive 12,500

§465 at-risk  30,000  → disposition gain is income from the activity
                        → deducts against the gain in full
§469 passive  12,500  → complete taxable disposition releases ALL of it,
                        against ANY income
§704(d) basis      0  → would EXPIRE if any remained

net effect on income = 90,000 − 30,000 − 12,500 = +$47,500
```

**Had B been sold at the end of year 1 instead** — while $40,000 still sat in the basis bucket — the at-risk and passive buckets would behave identically, but that **$40,000 would be permanently lost**. Gain on sale does not restore basis.

> Same activity, same gain, same suspended total — **$40,000 difference in outcome** purely from timing. This is why the buckets are tracked separately.

---

## 16. Where this fits in the year loop

Insert between Step 5 and Step 6 of [00-OVERVIEW-AND-YEAR-LOOP.md](00-OVERVIEW-AND-YEAR-LOOP.md):

```
STEP 5    Compute RMD                          → 05
STEP 5a   Load opening carryforward state      → this file, §13
STEP 5b   Gate 1 — basis, per activity         → §2
STEP 5c   Gate 2 — at-risk, per activity       → §3
STEP 5d   Gate 3 — passive, pooled             → §4
STEP 5e   Gate 4 — excess business loss        → §5
STEP 5f   Conservation check                   → §14 Rule 1
STEP 6    Assemble AGI                         → §6, then 02
STEP 6a   Social Security taxable portion      → §7
STEP 6b   NOL deduction (80% cap)              → §8
STEP 6c   Capital loss ($3,000)                → §9
STEP 7    Regular tax                          → 02
STEP 7a   QBI deduction                        → §10
STEP 7b   NIIT — separate NII/MAGI             → §11
STEP 7c   AMT — parallel rail                  → §12
STEP 7d   Save closing carryforward state      → §13
```

---

## 17. Known gaps

| Gap | Note |
|---|---|
| State conformity | California and others decouple from federal §461(l), §172 and bonus depreciation. Model per state. |
| Grouping elections | §469 activity grouping (Reg. §1.469-4) changes which losses pool. Assumed no grouping. |
| Basis-reduction ordering election | §1.704-1(d)(2) allows an election to reorder. Assumed default order. |
| Form 461 aggregation detail | Wages are excluded from the §461(l) computation but included in the threshold test. Verify against current-year instructions. |
| Real estate pre-gates | §280A and the §469 classification tests run before these four gates — see [07-REAL-ESTATE-EQUITY.md](07-REAL-ESTATE-EQUITY.md) Part H. |

---

## Sources

| Formula / rule | Type | Source | Google this |
|---|---|---|---|
| **Four-gate ordering** | **Law** | [The Tax Adviser — Partnership interests, Sec. 465 at-risk limit](https://www.thetaxadviser.com/issues/2021/apr/partnership-interests-sec-465-at-risk-limit-form-6198/) · [S shareholders' loss limitations](https://www.thetaxadviser.com/issues/2023/apr/interaction-of-s-shareholders-loss-limitations/) | `order of loss limitations basis at-risk passive excess business loss` |
| Basis limitation, partnership | **Law** | [IRC §704(d)](https://www.law.cornell.edu/uscode/text/26/704) | `IRC 704(d) partner basis loss limitation` |
| Basis limitation, S-corp | **Law** | [IRC §1366(d)](https://www.law.cornell.edu/uscode/text/26/1366) | `IRC 1366(d) S corporation shareholder basis debt basis` |
| Liabilities in partnership basis | **Law** | [IRC §752](https://www.law.cornell.edu/uscode/text/26/752) | `IRC 752 partnership liabilities basis` |
| At-risk limitation | **Law** | [IRC §465](https://www.law.cornell.edu/uscode/text/26/465) | `IRC 465 at risk rules Form 6198` |
| Qualified nonrecourse financing | **Law** | [Reg. §1.465-27](https://www.law.cornell.edu/cfr/text/26/1.465-27) | `qualified nonrecourse financing 465(b)(6) real property` |
| Negative at-risk recapture | **Law** | IRC §465(e) | `section 465(e) recapture negative at risk amount` |
| Passive activity loss | **Law** | [IRC §469](https://www.law.cornell.edu/uscode/text/26/469) | `IRC 469 passive activity loss suspended` |
| $25,000 allowance, $100k–$150k phaseout | **Law** | IRC §469(i) — **not indexed** | `section 469(i) $25,000 rental allowance phaseout` |
| Release on complete disposition | **Law** | IRC §469(g) | `passive activity suspended losses complete disposition release` |
| Real estate professional | **Law** | IRC §469(c)(7) | `real estate professional 750 hours material participation` |
| **EBL $256,000 / $512,000 (2026)** | **Law** | **IRS Rev. Proc. 2025-32** · [IRC §461(l)](https://www.law.cornell.edu/uscode/text/26/461) | `Rev Proc 2025-32 excess business loss threshold 2026` |
| EBL made permanent | **Law** | OBBBA (P.L. 119-21) | `OBBBA excess business loss permanent 461(l)` |
| NOL 80%, indefinite, no carryback | **Law** | [IRC §172](https://www.law.cornell.edu/uscode/text/26/172) | `section 172 NOL 80 percent limitation TCJA` |
| Capital loss $3,000, indefinite, character | **Law** | [IRC §1211](https://www.law.cornell.edu/uscode/text/26/1211) · [§1212](https://www.law.cornell.edu/uscode/text/26/1212) | `capital loss carryover $3,000 limit character` |
| Capital loss dies with taxpayer | **Law** | Reg. §1.212-1; final return rule | `capital loss carryover death final return` |
| QBI limit = 20% × (TI − net cap gain) | **Law** | [IRC §199A](https://www.law.cornell.edu/uscode/text/26/199A) | `199A deduction 20 percent taxable income net capital gain` |
| Negative QBI carryforward | **Law** | IRC §199A(c)(2) | `negative QBI carryforward separate trade or business` |
| Pre-2018 losses excluded from QBI | **Law** | Reg. §1.199A-3(b)(1)(iv) | `suspended losses pre-2018 QBI treatment` |
| NII definition and exclusions | **Law** | [Reg. §1.1411-4](https://www.law.cornell.edu/cfr/text/26/1.1411-4) · [Form 8960](https://www.irs.gov/instructions/i8960) | `Form 8960 net investment income definition` |
| Self-rental recharacterisation | **Law** | Reg. §1.469-2(f)(6) | `self-rental recharacterization 1.469-2(f)(6) NIIT` |
| **AMT 2026 exemption / phaseout** | **Law** | [IRS Rev. Proc. 2025-32](https://www.irs.gov/newsroom/irs-releases-tax-inflation-adjustments-for-tax-year-2026-including-amendments-from-the-one-big-beautiful-bill) | `2026 AMT exemption 90,100 140,200 phaseout 500,000` |
| AMT 50% phaseout rate | **Law** | OBBBA §70107 | `OBBBA section 70107 AMT phaseout rate 50 percent` |
| AMT 26%/28%, $244,500 | **Law** | IRC §55(b) · Rev. Proc. 2025-32 | `2026 AMT 28 percent rate threshold 244,500` |
| Minimum tax credit | **Law** | [IRC §53](https://www.law.cornell.edu/uscode/text/26/53) | `IRC 53 minimum tax credit deferral exclusion items` |
| **§704(d) losses expire on sale** | **Law** | [The Tax Adviser — Application of tax basis and at-risk limitations](https://www.thetaxadviser.com/issues/2012/mar/clinic-story-04-mar-2012/) | `suspended 704(d) losses expire sale partnership interest` |
| §465 losses offset disposition gain | **Law** | Same source; IRC §465(a)(2) | `at-risk suspended losses offset gain sale partnership` |
| Pro-rata allocation at gate 3 | **Law** | Form 8582 instructions | `Form 8582 allocation of allowed passive losses pro rata` |
| Conservation identity (Rule 1) | Math | Stated here — an accounting check, not a statute | — |
