# 07 — Real Estate

**Step 11 of the year loop, plus a classification step that runs before the loss gates** · Rail: **nominal**

> **Filename note.** This module was originally "Real Estate Equity" and covered only appreciation, amortisation and equity. It now covers the full real estate picture. The filename is unchanged so existing links keep working.

---

## What this module covers

| Part | Question it answers |
|---|---|
| **A. Classification** | Is this even a rental? Is it passive? |
| **B. Equity mechanics** | What is the property worth, what is owed, what is the equity? |
| **C. Depreciation** | How much can be written off, and how fast? |
| **D. Participation** | Does the owner materially participate? Are they a real estate professional? |
| **E. Short-term rentals** | The ≤7-day rule and what it really does |
| **F. QBI** | Does the rental qualify for the 20% deduction? |
| **G. Disposition** | Sale, §1031 exchange, or hold until death |
| **H. Ordering** | Where all of this sits relative to the four loss gates |

> **Why classification comes first.** Two identical properties with identical losses can produce a **$203,409 deduction** or **$0**, depending only on how they are classified. Get Part A wrong and every number after it is wrong.

---

# PART A — Classification

Run these three questions **in order**, before anything else.

```
Q1  Is personal use excessive?          → §280A          → if yes, STOP: no loss allowed
Q2  Is the average stay ≤ 7 days?       → §1.469-1T      → if yes, NOT a rental activity
Q3  Does the owner materially participate? → §1.469-5T   → decides passive vs non-passive
```

## Q1 — §280A personal use test

```
threshold = MAX(14 days, 0.10 × daysRentedAtFairValue)

IF personalUseDays > threshold:
    property is a PERSONAL RESIDENCE
    deductions are CAPPED at rental income — no loss is allowed
    excess carries forward under §280A (not as a passive loss)
```

**Worked contrast** — a property rented 100 days at fair value:

| | Personal use 10 days | Personal use 20 days |
|---|---|---|
| Threshold | 14 days | 14 days |
| Test | 10 ≤ 14 → **passes** | 20 > 14 → **fails** |
| Rental income | $45,000 | $45,000 |
| Expenses + depreciation | $293,409 | $293,409 |
| **Deductible** | full loss flows to the gates | **capped at $45,000** |
| Disallowed | — | **$248,409** carried forward under §280A |

> **§280A runs before the four loss gates.** If it bites, the loss never reaches basis, at-risk or passive at all. This is a **pre-gate**, and module 11's sequence includes it as such.

### The Augusta rule — §280A(g)

```
IF daysRented <= 14 for the year:
    rental income is EXCLUDED from gross income entirely
    no rental deductions are allowed
```

A separate, deliberate provision. Rent the home 14 days or fewer and the income simply does not go on the return.

## Q2 — is it a "rental activity" at all?

```
averageStay = totalRentalDays / numberOfCustomerStays

IF averageStay <= 7 days:
    NOT a rental activity under Reg. §1.469-1T(e)(3)(ii)(A)
    → the automatic "passive" label does NOT apply
    → test material participation instead (Q3)
ELSE:
    IS a rental activity
    → PASSIVE BY DEFAULT regardless of hours worked
    → unless the owner qualifies as a real estate professional (Part D)
```

> There is a second exception at **≤30 days average stay with significant personal services**. The ≤7-day test is the one that matters in practice.

## Q3 — material participation

Only reached if Q2 said "not a rental activity", or if the owner is a real estate professional. See **Part D**.

### The classification outcome table

| Average stay | Material participation | Result |
|---|---|---|
| ≤ 7 days | **Yes** | **Non-passive** — losses offset W-2 income |
| ≤ 7 days | No | Passive — losses suspended |
| > 7 days | Yes, but not a REP | **Still passive** — hours do not help |
| > 7 days | REP + materially participates | Non-passive |
| > 7 days | Active participation only | Passive, but up to $25,000 allowance |

---

# PART B — Equity mechanics

**What it does.** Tracks property value up and mortgage balance down. Equity is the gap.

```
equity = propertyValue − mortgageBalance
```

## Property value

```
propertyValue(n) = propertyValue(0) × (1 + appreciationRate)^n
```

Use a **nominal** rate. Long-run US home price growth runs at or slightly above CPI; 3–4% nominal is defensible. Do not baseline on 2020–2022.

## Mortgage amortisation

```
i = annualRate / 12
N = termInMonths

payment = P × [ i × (1 + i)^N ] / [ (1 + i)^N − 1 ]
```

```
balance(m) = P × [ (1 + i)^N − (1 + i)^m ] / [ (1 + i)^N − 1 ]
```

```
FOR each month:
    interestPortion  = balance × i
    principalPortion = payment − interestPortion
    balance          = balance − principalPortion
```

**Worked number** — $500,000 at 6.5% over 30 years, `payment = $3,160.34/month`:

| After | Balance | Principal to date | Interest to date |
|---|---|---|---|
| 1 year | $494,411 | $5,589 | $32,335 |
| 5 years | $468,055 | $31,945 | $157,675 |
| 10 years | $423,881 | $76,119 | $303,121 |
| 20 years | $278,326 | $221,674 | $536,808 |
| 30 years | $0 | $500,000 | $637,722 |

> Year 1: of $37,924 paid, only **$5,589** reduces the balance. **Early equity comes from appreciation, not amortisation.** Straight-line principal assumptions overstate early equity badly.

## Equity over time

```
equity(n) = propertyValue(n) − balance(n)
```

$650,000 property, $500,000 mortgage at 6.5%, 3.5% appreciation:

| Year | Value | Balance | Equity |
|---|---|---|---|
| 0 | $650,000 | $500,000 | $150,000 |
| 5 | $771,996 | $468,055 | $303,941 |
| 10 | $916,889 | $423,881 | $493,009 |
| 20 | $1,293,363 | $278,326 | $1,015,036 |
| 30 | $1,824,416 | $0 | $1,824,416 |

Equity multiplies about **12×** while value multiplies under **3×**. That gap is the leverage effect.

## Cash flow

```
netOperatingIncome = rentalIncome
                   − propertyTax
                   − insurance
                   − maintenance
                   − managementFees
                   − vacancyAllowance

netCashFlow = netOperatingIncome − annualMortgagePayment
```

Defaults when the client supplies nothing:

| Item | Typical |
|---|---|
| Property tax | 1.0–1.25% of value/yr |
| Insurance | 0.3–0.5% of value/yr |
| Maintenance | 1% of value/yr |
| Management | 8–10% of rent |
| Vacancy | 5–8% of rent |

**A primary residence produces negative cash flow.** It is a consumption asset that builds equity. Do not model it as income-producing.

## Multiple properties

```
totalRealEstateEquity(n) = SUM over properties of ( value(n) − balance(n) )
```

Each property has its own rate, term, classification and tax treatment. **Never blend them into one average.**

---

# PART C — Depreciation and cost segregation

**What it does.** Writes off the building over time. Cost segregation splits it into faster-depreciating components.

**Why it matters.** Cost segregation plus 100% bonus depreciation can turn a $34,545 first-year deduction into **$263,409** — a 7.6× difference on the same property.

## Recovery periods

```
annualDepreciation = (purchasePrice − landValue) / recoveryPeriod
```

| Asset | Recovery period |
|---|---|
| **Residential rental** | **27.5 years** |
| **Nonresidential (commercial)** | **39 years** |
| Land improvements (fences, paving, landscaping) | **15 years** |
| Personal property (appliances, carpet, fixtures) | **5 or 7 years** |
| **Land** | **Never depreciable** |

## Bonus depreciation — 100%, permanent

```
IF assetClass has recoveryPeriod <= 20 years
   AND placedInService > 19 January 2025:
       bonusDepreciation = 100% of basis, in year 1
```

OBBBA made 100% bonus **permanent** for property placed in service after **19 January 2025**. Assets acquired on or before that date follow the old phase-down percentages for their placed-in-service year.

> **The building itself never qualifies** — 27.5 and 39 years are both well over the 20-year limit. Only the components a cost segregation study carves out are eligible.

## Cost segregation

An engineering study reclassifies parts of the purchase price into shorter-lived classes.

**Worked contrast** — $1,200,000 purchase, $250,000 land, $950,000 building:

### Without cost segregation

```
$950,000 / 27.5 = $34,545 per year
```

### With cost segregation

```
15% → 5-year personal property     $142,500
10% → 15-year land improvements     $95,000
remaining 27.5-year structure      $712,500

100% bonus on the 5- and 15-year components  = $237,500
structure depreciation $712,500 / 27.5       =  $25,909
                                               ─────────
YEAR 1 TOTAL                                   $263,409
```

**The difference:** **$228,864** more deduction in year 1 — **7.6×**. At a 35% marginal rate that is **$80,102** of tax deferred into later years.

> **Deferred, not eliminated.** Cost segregation accelerates deductions; it does not create them. The later years get correspondingly less, and the lower basis means **more depreciation recapture on sale** (Part G). It is a timing strategy, and the model must show both halves.

## §179 — and why it usually does not apply

| Item | 2026 |
|---|---|
| Limit | **$2,560,000** |
| Phaseout threshold | **$4,090,000** |
| Cannot create a loss | Limited to business taxable income |

> **§179 is not available for residential rental property.** It applies to nonresidential real property improvements only — roofs, HVAC, fire protection, alarm and security systems. For a residential landlord, **bonus depreciation is the tool, not §179**.

---

# PART D — Participation and passive status

**What it does.** Decides whether losses can offset ordinary income or must wait.

## The seven material participation tests

Reproduced from **Reg. §1.469-5T(a)**. Meeting **any one** is enough.

| # | Test |
|---|---|
| 1 | More than **500 hours** in the activity during the year |
| 2 | Participation constitutes **substantially all** participation by all individuals |
| 3 | More than **100 hours**, and **no other individual participates more** |
| 4 | It is a **significant participation activity** (>100 hrs) and total SPA hours across all such activities **exceed 500** |
| 5 | Materially participated in **any 5 of the last 10** years |
| 6 | A **personal service activity** in which they materially participated for **any 3 prior years** |
| 7 | **Facts and circumstances** — regular, continuous and substantial |

> **Test 7 has a floor:** under Reg. §1.469-5T(b)(2)(iii), fewer than **100 hours** can never qualify under facts and circumstances.

**Test 3 is the one that matters for short-term rentals.** A self-managed STR owner working 120 hours, with no property manager working more, materially participates — without ever approaching 500 hours.

## Active participation — a much lower bar

Applies to **rental activities only** and unlocks the $25,000 allowance.

| | Material participation | Active participation |
|---|---|---|
| Bar | High — one of seven tests | Low — approve tenants, set terms, approve repairs |
| Effect | Losses become non-passive | Losses stay passive, but up to $25,000 may be deducted |
| Ownership required | None | **At least 10%** |

```
specialAllowance = MAX(0, 25000 − 0.50 × MAX(0, MAGI − 100000))
```

| MAGI | Allowance |
|---|---|
| ≤ $100,000 | $25,000 |
| $125,000 | $12,500 |
| ≥ $150,000 | **$0** |

> **Not indexed since 1986.** For most clients in this system it is permanently zero — but keep it in the model for lean or early years.

## Real estate professional status (REPS)

```
REPS qualifies IF BOTH:
    hours in real property trades or businesses > 750
    AND those hours > 50% of ALL personal services performed that year
```

**What REPS actually does:** it removes the "automatically passive" label from **rental activities**. It does **not** by itself make losses deductible — the owner must **then** materially participate in each rental activity.

### The aggregation election — §1.469-9(g)

```
WITHOUT the election: material participation tested PER PROPERTY
WITH the election:    all rental real estate treated as ONE activity
```

**Worked contrast** — an owner with five rentals, 200 hours each (1,000 hours total):

| | Without election | With §1.469-9(g) election |
|---|---|---|
| Test applied | Per property: 200 hrs each | Combined: 1,000 hrs |
| 500-hour test | **Fails on all five** | **Passes** |
| Result | All losses passive | All losses non-passive |

**The difference:** the same 1,000 hours produce either nothing or full deductibility, depending on a one-paragraph statement attached to the return.

> The election is **binding for all future years** unless facts materially change. It is also a trap on disposition: with all properties grouped as one activity, selling **one** property is not a complete disposition and does **not** release suspended losses.

## Grouping — §1.469-4

Activities may be grouped as an **"appropriate economic unit"**, based on similarities in type, common control, common ownership, geography and interdependence. Disclosure is required under **Rev. Proc. 2010-13**.

## The self-rental rule

```
IF the owner rents property to a business in which they materially participate:
    NET RENTAL INCOME  is recharacterised as NON-PASSIVE
    NET RENTAL LOSS    remains PASSIVE
```

> **Deliberately one-way, and it works against the taxpayer.** Income gets pulled out of the passive bucket (so it cannot absorb other passive losses) while losses stay in it. The one silver lining: recharacterised non-passive rental income is **outside NII**, so it escapes the 3.8% surtax.

---

# PART E — Short-term rentals

**What it does.** The ≤7-day rule removes the automatic "passive" label. Combined with material participation, it lets rental losses offset W-2 income directly — the single largest real estate planning lever in the code.

**Why it matters.** Same property, same loss: **$203,409 deductible now** versus **$0**.

## The two conditions — both required

```
CONDITION 1   averageStay <= 7 days
              → not a rental activity under Reg. §1.469-1T(e)(3)(ii)(A)

CONDITION 2   material participation met (any of the seven tests, Part D)
              → the loss is non-passive
```

> **Condition 1 alone does nothing.** Clearing the 7-day test only removes the automatic passive label. Without material participation the activity is still passive — just for a different reason. Most promotional material blurs this.

## Worked contrast — identical property, identical loss

$1,200,000 property with a cost segregation study, $60,000 net operating income, $263,409 depreciation → **$203,409 tax loss**.

| | Long-term rental (30-day leases) | Short-term rental (5-day average) |
|---|---|---|
| Rental activity? | **Yes** | **No** — ≤7 days |
| Default status | Passive | Tested on material participation |
| Material participation | Irrelevant — still passive | **Met** (120 hrs, Test 3) |
| $25,000 allowance | $0 — MAGI over $150,000 | Does not apply |
| **Deductible this year** | **$0** | **$203,409** |
| Suspended | $203,409 | $0 |
| **Tax value at 35%** | **$0** | **$71,193** |

## Four things that are widely misstated

**1. The EBL cap still applies.**

Being non-passive does **not** exempt the loss from §461(l).

| Scenario | Non-passive loss | EBL cap | Deducted now | To NOL |
|---|---|---|---|---|
| One STR | $203,409 | $512,000 | $203,409 | $0 |
| Four STRs | $813,636 | $512,000 | **$512,000** | **$301,636** |

> A client scaling up STRs to shelter a large salary hits the **$512,000 ceiling**, and the excess becomes an NOL that can only offset **80%** of future income. Promotional material almost never mentions this.

**2. REPS is irrelevant to short-term rentals.**

REPS is a rule about *rental activities*. An STR under the 7-day rule is **not a rental activity**, so REPS neither helps nor is required. Pursuing 750 hours to make an STR work is wasted effort.

**3. The $25,000 allowance does not apply either** — for the same reason.

**4. Self-employment tax is a separate question.**

```
Average stay length  → governs the PASSIVE rules (§469)
Substantial services → governs SELF-EMPLOYMENT tax
```

| Reported on | When | SE tax |
|---|---|---|
| **Schedule E** | Space plus ordinary rental services | **No** |
| **Schedule C** | **Substantial hotel-like services** — daily housekeeping during the stay, meals, concierge | **Yes, 15.3%** |

> Furnishing the property, cleaning **between** guests, wifi and utilities do **not** count as substantial services. A client can be non-passive under §469 and still owe no SE tax — the two tests are independent.

## What the model must track per STR

```
averageStayDays          → recompute every year; classification can flip
participationHours       → and hours of anyone else, for Test 3
materialParticipation    → boolean, re-tested annually
substantialServices      → boolean, drives Schedule C vs E
personalUseDays          → §280A pre-gate
```

> **Classification is not permanent.** A property let on 5-day stays in 2026 and 30-day stays in 2027 changes category, and losses suspended while passive stay suspended — they are not retroactively freed.

---

# PART F — QBI for rentals

**What it does.** Decides whether rental income qualifies for the 20% §199A deduction.

A rental qualifies only if it rises to a **trade or business under §162**. Rev. Proc. 2019-38 offers a safe harbor.

```
SAFE HARBOR requires ALL of:
    separate books and records per rental enterprise
    250+ hours of rental services per year
      (for enterprises 4+ years old: 250 hrs in 3 of the last 5 years)
    contemporaneous records — hours, description, dates, who performed them
    a signed statement attached to the return
```

| Excluded from the safe harbor | Why |
|---|---|
| **Triple-net leases** | Tenant pays taxes, insurance and maintenance — too passive |
| Property used as a residence by the taxpayer | §280A territory |

> Failing the safe harbor is **not fatal** — the rental may still be a §162 trade or business on facts and circumstances. The safe harbor just removes the argument.

**Rental income is not an SSTB**, so a landlord above the income thresholds keeps the full 20% — unlike a service business owner. The exception is **self-rental to a commonly-controlled SSTB**, which is itself treated as an SSTB.

---

# PART G — Disposition

Three exits, three completely different outcomes.

## Exit 1 — outright sale

```
adjustedBasis   = costBasis + improvements − accumulatedDepreciation
gainOnSale      = salePrice − sellingCosts − adjustedBasis
recaptureAmount = MIN(accumulatedDepreciation, gainOnSale)   → taxed at 25%
remainingGain   = gainOnSale − recaptureAmount               → taxed at LTCG rates
```

**Worked number** — $1,200,000 property sold for $1,800,000 with $250,000 of accumulated depreciation:

```
Adjusted basis    $1,200,000 − $250,000 =   $950,000
Gain              $1,800,000 − $950,000 =   $850,000

§1250 recapture      $250,000 @ 25%     =    $62,500
Remaining gain       $600,000 @ 20%     =   $120,000
                                            ─────────
TOTAL TAX                                   $182,500
```

Plus NIIT at 3.8% if passive, plus state tax.

> **This is the other half of cost segregation.** Accelerating depreciation lowers basis, which raises the gain **and** the 25% recapture. The model must carry `accumulatedDepreciation` forward for exactly this reason.

## Exit 2 — §1031 like-kind exchange

```
45 days   to identify replacement property
180 days  to close
```

| Rule | Detail |
|---|---|
| Qualifying property | **Real property only** since TCJA — permanent |
| Excluded | Primary residence, fix-and-flip inventory, partnership interests, all personal property |
| Basis | **Carries over** — the deferred gain lives in the lower basis |
| Boot | Cash or debt relief received triggers gain **up to the boot** |
| Qualified intermediary | Required — the seller must never touch the proceeds |

**On the same facts:** $182,500 of tax **deferred**, carryover basis of $950,000 into the replacement property.

> **Deferred, not forgiven.** Unless the property is held until death.

## Exit 3 — hold until death

```
heirBasis = fairMarketValueAtDeath
```

**On the same facts:** capital gain **and** depreciation recapture both become **$0**. Heirs take a $1,800,000 basis.

### The three exits compared

| Exit | Tax now | Deferred gain | Recapture |
|---|---|---|---|
| Sell | **$182,500** | — | Paid |
| §1031 | **$0** | Carried in the new basis | Deferred |
| Hold to death | **$0** | **Erased** | **Erased** |

> This is the mechanical basis of "buy, borrow, die". It also means a §1031 chain held to death converts a lifetime of deferral into permanent forgiveness — which is why disposition timing belongs in the roadmap, not just the tax return.

---

# PART H — Where real estate sits in the loss gates

Real estate does not simply enter the four gates of module 11. Two steps run **before** them.

```
PRE-GATE A   §280A PERSONAL USE            → if it bites, loss capped at rental income, STOP
PRE-GATE B   CLASSIFICATION                → rental activity? passive or non-passive?
             (§1.469-1T 7-day rule, then §1.469-5T material participation, then REPS)

GATE 1       Basis            §704(d) / §1366(d)
GATE 2       At-risk          §465  ← qualified nonrecourse financing carve-out applies here
GATE 3       Passive          §469  ← pre-gate B decided whether the loss even arrives here
GATE 4       EBL              §461(l) ← non-passive STR losses DO pass through this
```

**Two interactions the sequence makes explicit:**

- A **non-passive** STR loss **skips gate 3** entirely but still meets **gate 4**.
- A **passive** long-term rental loss stops at **gate 3** and never reaches gate 4.

**Full gate mechanics →** [11-LOSS-LIMITATIONS-AND-CARRYFORWARDS.md](11-LOSS-LIMITATIONS-AND-CARRYFORWARDS.md)

---

# Edge-case matrix

| Situation | Treatment | Where |
|---|---|---|
| Rented ≤14 days/year | Income excluded entirely; no deductions | §280A(g) |
| Personal use > 14 days or 10% | Deductions capped at rental income | §280A |
| Average stay ≤7 days + material participation | **Non-passive** — offsets W-2 | §1.469-1T |
| Average stay ≤7 days, no material participation | Passive | §469 |
| Average stay >7 days, 600 hrs worked, not a REP | **Still passive** — hours don't help | §469(c)(2) |
| REP + §1.469-9(g) aggregation | All rentals one activity; hours combine | §1.469-9(g) |
| REP, no aggregation election | Tested per property — usually fails | §1.469-9 |
| Renting to your own business (income) | Recharacterised **non-passive**, and out of NII | §1.469-2(f)(6) |
| Renting to your own business (loss) | Stays **passive** | same |
| Triple-net lease | No §199A safe harbor | Rev. Proc. 2019-38 |
| STR with daily housekeeping and meals | Schedule C, **SE tax applies** | §1402 |
| Sell one property from an aggregated group | **Not** a complete disposition — no release | §469(g) |
| Sell to a related party | No release of suspended losses | §469(g)(1)(B) |
| Cost seg then sell | Higher recapture at 25% — the deferral reverses | §1250 |
| Cost seg then hold to death | Recapture **erased** by step-up | §1014 |
| §1031 into a new property | Basis carries over; depreciation continues on the old schedule | §1031 |
| Property converted from personal to rental | Basis = **lesser of** cost or FMV at conversion | §1.168(i)-4 |
| Land | Never depreciable | §168 |

## Out of scope for v1

Opportunity Zones (§1400Z), Delaware Statutory Trusts, §721 UPREIT contributions, installment sales (§453), and state-level conformity differences. Each is noted here so their absence is deliberate rather than accidental.

---

# Risks and common mistakes

| What goes wrong | Who it hurts | How to prevent it |
|---|---|---|
| **Classification skipped entirely** | Client — the single biggest error; $203,409 vs $0 | Run Part A before any other real estate step |
| Straight-line principal paydown | Client — overstates early equity | Use the amortisation formula |
| Land depreciated | Client — disallowed deduction | Building value only |
| Cost seg modelled without the recapture consequence | Client — overstates lifetime benefit | Carry `accumulatedDepreciation`; apply 25% on sale |
| §179 claimed on residential rental | Client — disallowed | Bonus depreciation instead; §179 is nonresidential only |
| Bonus claimed on the building itself | Client | Only ≤20-year components qualify |
| REPS pursued to fix a short-term rental | Client — wasted hours, no benefit | STRs are not rental activities; REPS is irrelevant |
| STR loss assumed exempt from §461(l) | Client — plans on a deduction that is capped | Non-passive still meets gate 4 |
| $25,000 allowance applied at high income or to STRs | Client | Zero above $150,000 MAGI; never for STRs |
| Aggregation election made without considering exit | Client — cannot release losses on a single sale | Model the disposition consequence before electing |
| Classification assumed permanent | Both — it can flip year to year | Re-test average stay and hours every year |
| Self-rental loss recharacterised as non-passive | Client — the rule is one-way | Income only; losses stay passive |
| Substantial services conflated with the 7-day test | Client — unexpected SE tax | Two independent tests |
| Primary residence modelled as income-producing | Client | Negative cash flow; §121 on sale |
| Properties blended into one average | Developer | Model each separately |

---

# Sources

| Rule | Type | Source | Google this |
|---|---|---|---|
| ≤7-day rule — not a rental activity | **Law** | [Reg. §1.469-1T(e)(3)(ii)(A)](https://www.law.cornell.edu/cfr/text/26/1.469-1T) | `1.469-1T(e)(3)(ii)(A) seven day average rental activity` |
| Seven material participation tests | **Law** | [Reg. §1.469-5T(a)](https://www.law.cornell.edu/cfr/text/26/1.469-5T) | `1.469-5T material participation seven tests` |
| REPS 750 hours + 50% | **Law** | [IRC §469(c)(7)](https://www.law.cornell.edu/uscode/text/26/469) | `real estate professional 750 hours 469(c)(7)` |
| §1.469-9(g) aggregation election | **Law** | [Reg. §1.469-9(g)](https://www.law.cornell.edu/cfr/text/26/1.469-9) | `1.469-9(g) election group rental real estate` |
| Grouping — appropriate economic unit | **Law** | [Reg. §1.469-4](https://www.law.cornell.edu/cfr/text/26/1.469-4) · Rev. Proc. 2010-13 | `1.469-4 grouping appropriate economic unit disclosure` |
| Self-rental recharacterisation | **Law** | [Reg. §1.469-2(f)(6)](https://www.law.cornell.edu/cfr/text/26/1.469-2) | `self-rental rule 1.469-2(f)(6)` |
| $25,000 allowance, $100k–$150k phaseout | **Law** | IRC §469(i) — **not indexed** | `section 469(i) 25000 rental allowance phaseout` |
| §280A personal use, 14 days / 10% | **Law** | [IRC §280A](https://www.law.cornell.edu/uscode/text/26/280A) | `section 280A vacation home 14 days 10 percent` |
| Augusta rule | **Law** | IRC §280A(g) | `Augusta rule 280A(g) 14 days tax free` |
| Recovery periods 27.5 / 39 / 15 / 5–7 | **Law** | [IRS Pub 946](https://www.irs.gov/publications/p946) · [Pub 527](https://www.irs.gov/publications/p527) | `IRS Publication 946 MACRS recovery periods` |
| 100% bonus, permanent, after 19 Jan 2025 | **Law** | OBBBA (P.L. 119-21) · IRC §168(k) | `OBBBA 100% bonus depreciation permanent January 19 2025` |
| §179 $2,560,000 / $4,090,000 (2026) | **Law** | Rev. Proc. 2025-32 · IRC §179 | `2026 section 179 limit 2,560,000 phaseout` |
| §179 unavailable on residential rental | **Law** | IRC §179(d)(1) · §168(e)(2)(A) | `section 179 residential rental property not eligible` |
| §1250 recapture at 25% | **Law** | [IRC §1250](https://www.law.cornell.edu/uscode/text/26/1250) · IRS Topic 409 | `unrecaptured section 1250 gain 25 percent` |
| §199A rental safe harbor, 250 hours | **Law** | [Rev. Proc. 2019-38](https://www.irs.gov/pub/irs-drop/rp-19-38.pdf) | `Revenue Procedure 2019-38 rental real estate safe harbor` |
| Triple-net excluded from safe harbor | **Law** | same | `199A safe harbor triple net lease excluded` |
| §1031 real property only, 45/180 | **Law** | [IRC §1031](https://www.law.cornell.edu/uscode/text/26/1031) | `1031 exchange 45 day 180 day real property only TCJA` |
| §121 home sale exclusion | **Law** | IRC §121 · IRS Pub 523 | `IRS Publication 523 home sale exclusion` |
| Mortgage interest $750,000 cap | **Law** | IRC §163(h) · IRS Pub 936 | `IRS Publication 936 mortgage interest limit` |
| §1014 step-up | **Law** | [IRC §1014](https://www.law.cornell.edu/uscode/text/26/1014) | `IRC 1014 basis property acquired from decedent` |
| STR Schedule C vs E / SE tax | **Law** | IRC §1402 · Reg. §1.1402(a)-4(c) | `short term rental substantial services Schedule C self-employment tax` |
| Amortisation formula | Math | Standard identity | `mortgage amortization formula derivation` |
