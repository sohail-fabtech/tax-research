# Roadmap to Age 90™ — Master Guide

**The whole calculation, start to finish, in one place.**

Tax year **2026** · Market **United States** · Verified **September 2026**

> **Looking to explain this to a client, or see worked examples and risks?** Read [HANDBOOK.md](HANDBOOK.md) instead — same 21 steps, with two contrasting examples and a risk table for each. This file is the lean build reference.

> **How to read this file.** Each step has three parts: a plain-English explanation anyone can follow, the exact formula for whoever builds it, and a link to the detailed module for constants and edge cases. The formulas here are copied word-for-word from modules 00–08 — nothing is simplified or reworded. (The one exception is the Step 8 cash-flow identity, which the modules name but never write out; it is flagged as new in the sources table.)

---

## What we are building

For every year from the client's age today to age 90 (or 100), we produce one row of a table:

| Column | In plain words |
|---|---|
| Age / Year | Who they are and when |
| Income | Money coming in |
| Contributions | Money going into savings |
| Social Security | Government retirement benefit |
| RMD | Money the IRS *forces* out of retirement accounts |
| Taxes | Money going to the government |
| Expenses | Money spent living |
| Investment growth | What the money earns |
| Retirement balance | 401(k)/IRA total |
| Insurance cash value | Money inside the life policy |
| Real estate equity | Property value minus mortgage |
| Net worth | Everything added up |
| Estate value | What actually reaches the heirs |

Do this 48 times and you have the roadmap.

---

## The 3 golden rules

**Rule 1 — Calculate in future dollars, show today's dollars.**

Do every calculation in *nominal* (future) dollars. Convert to today's dollars only at the very end, when displaying.

This is not a preference. Tax brackets rise with inflation every year, but the Social Security taxation thresholds ($25,000 / $32,000 / $34,000 / $44,000) have been **frozen in law since 1983 and 1993 and never change**. If you shrink the dollars before the tax step, you compare shrunken income against frozen thresholds and **under-tax every later year**.

**Rule 2 — The order of the steps is part of the maths.**

The steps below look independent. They are not. The RMD must be added to income *before* tax is calculated. Contributions must be subtracted *before* tax is calculated. Do them out of order and every number after is wrong.

**Rule 3 — The age 60–63 catch-up *replaces* the age-50 catch-up.**

It does not stack on top. Maximum 401(k) at age 62 is **$35,750**, not $43,750 — and it drops back to $32,500 at age 64.

---

## The flow at a glance

```
FOR each year n, age a:

  STEP 1   Grow income                     → 01
  STEP 2   Grow expenses                   → 01
  STEP 3   Compute retirement contributions → 03
  STEP 4   Compute Social Security benefit → 04
  STEP 5   Compute RMD (if age ≥ RMD age)  → 05
  STEP 5b  Classify each property           → 07   (property owners only)
  STEP 5a  Apply loss limitation gates      → 11   (K-1s and property)
  STEP 6   Assemble taxable income         → 02
  STEP 7   Compute tax on that income      → 02
  STEP 8   Compute cash flow surplus/deficit
  STEP 9   Apply investment growth         → 03
  STEP 10  Roll forward insurance          → 06
  STEP 11  Roll forward real estate        → 07
  STEP 12  Compute estate value            → 08
  STEP 13  Deflate the row to real dollars → this file, §2
```

### How the pieces feed each other

```
                    INCOME (01)
                       │
        ┌──────────────┼──────────────┐
        ▼              ▼              ▼
  CONTRIBUTIONS   EXPENSES (01)   TAXABLE INCOME (02)
      (03)             │                │
        │              │                │
        ▼              │                ▼
  RETIREMENT           │            TAXES (02)
  BALANCE (03)         │                │
        │              │                │
        │  at age 73/75│                │
        ▼              │                │
     RMD (05) ─────────┼────────────────┘
        │              │            (RMD is taxable)
        │              ▼
        │        CASH FLOW SURPLUS
        │              │
        │      ┌───────┼────────┐
        │      ▼       ▼        ▼
        │  INSURANCE  REAL   INVESTMENT
        │  CASH VAL  ESTATE   GROWTH
        │    (06)     (07)      (03)
        │      │       │        │
        └──────┴───────┴────────┘
                       │
                       ▼
             SOCIAL SECURITY (04)
             adds income from age 62–70
                       │
                       ▼
              NET WORTH → ESTATE VALUE (08)
```

---

# STEP 1 — Income

**In plain English.** While the client is working, their salary grows a few percent a year. The day they retire, that salary stops completely and the money has to come from somewhere else — Social Security, forced retirement withdrawals, rent, and their own savings.

**While working:**

```
income(n) = income(0) × (1 + growthRate)^n
```

```
earnedIncome(n) = w2(n) + k1(n) + scheduleC(n)
totalIncome(n)  = earnedIncome(n) + rental(n) + portfolio(n)
```

**After retiring** — the salary line becomes zero and four other sources take over:

```
totalIncome(n) = socialSecurity(n)        ← module 04
               + rmd(n)                    ← module 05
               + portfolioWithdrawal(n)     ← below
               + rental(n)                  ← module 07
```

**How much do they need?** Either a percentage of their final salary (75% is the standard assumption), or a figure they state themselves:

```
targetRetirementIncome = finalWorkingIncome × replacementRatio
```

```
targetRetirementIncome = clientStatedAmount, inflated to year n
                       = statedAmount × (1 + inflation)^n
```

**The savings only cover what the other sources don't:**

```
portfolioWithdrawal(n) = MAX(0,
      targetRetirementIncome(n)
    − socialSecurity(n)
    − rmd(n)
    − rental(n)
)
```

> The `MAX(0, …)` matters. If Social Security plus the RMD already cover the target, the withdrawal is zero — but the RMD still comes out. The extra goes into savings, it does not vanish.

**Full detail →** [01-INCOME-AND-EXPENSES.md](01-INCOME-AND-EXPENSES.md)

---

# STEP 2 — Expenses

**In plain English.** Living costs rise with inflation. But medical costs rise *faster* than everything else, so they must be tracked on their own line. When the client retires, general spending drops about 15% because work-related costs disappear — medical does not drop.

```
baseExpenses(0)  = (monthlyLifestyleExpenses × 12)
generalExpense(n) = baseExpenses(0) × (1 + inflation)^n
```

```
healthcare(0)  = monthlyMedicalInsurance × 12
healthcare(n)  = healthcare(0) × (1 + healthcareInflation)^n
```

```
totalExpenses(n) = generalExpense(n) + healthcare(n) + medicare(n)
```

**The retirement step-down:**

```
IF age ≥ retirementAge:
    generalExpense(n) = generalExpense(n) × retirementExpenseFactor
```

Default factor is `0.85`. Apply it to general spending only — never to healthcare.

> **Why healthcare gets its own rate.** At 2.5% general and 5% medical, healthcare goes from 13% of the budget at age 42 to 24% by age 72. Inflate everything at one rate and you miss that entirely.

**Full detail →** [01-INCOME-AND-EXPENSES.md](01-INCOME-AND-EXPENSES.md)

---

# STEP 3 — Retirement contributions

**In plain English.** The IRS caps how much can go into a 401(k) each year, and the cap changes with age. There is a bonus for age 50+, and a bigger bonus for ages 60–63 only — which *replaces* the age-50 bonus rather than adding to it.

```
catchUp =
    IF age >= 60 AND age <= 63:  11250
    ELSE IF age >= 50:            8000
    ELSE:                            0

limit401k = 24500 + catchUp
contribution401k = MIN(desiredContribution, limit401k, earnedIncome)
```

| Age | Maximum 401(k) |
|---|---|
| Under 50 | $24,500 |
| 50–59 | $32,500 |
| **60–63** | **$35,750** |
| 64+ | $32,500 ← drops back |

**New for 2026 — high earners must use Roth for the catch-up:**

```
IF priorYearWages > 150000:
    catchUpIsRoth = TRUE     → does NOT reduce taxable income
ELSE:
    catchUpIsRoth = FALSE    → reduces taxable income
```

> This is a real tax increase for high earners aged 50+. $8,000–$11,250 stops being deductible. Miss it and you overstate the tax saving every year from age 50 on.

**Roth IRA eligibility fades out at higher incomes:**

```
IF MAGI >= phaseOutEnd:      rothIRALimit = 0
ELSE IF MAGI > phaseOutStart:
    reduction = (MAGI − phaseOutStart) / (phaseOutEnd − phaseOutStart)
    rothIRALimit = baseLimit × (1 − reduction)
ELSE:                        rothIRALimit = baseLimit
```

**The limits themselves grow over time:**

```
limit(n) = ROUND_DOWN_TO_500( limit(2026) × (1 + inflation)^n )
```

> Holding the limits flat for 48 years understates contributions badly.

**Full detail →** [03-RETIREMENT-CONTRIBUTIONS-AND-GROWTH.md](03-RETIREMENT-CONTRIBUTIONS-AND-GROWTH.md)

---

# STEP 4 — Social Security

**In plain English.** The government averages the client's best 35 years of earnings, runs that average through a three-tier formula, then adjusts up or down depending on what age they start claiming. Claim early and the benefit is permanently smaller; wait until 70 and it is permanently bigger.

There are **two separate numbers** and they must not be confused: the benefit *received*, and the portion of it that is *taxable*. There is no circular dependency — compute the benefit first, then the taxable part in Step 6.

### The five links in the chain

```
Earnings history
   → (1) index each year
   → (2) take highest 35 → AIME
   → (3) apply bend points → PIA
   → (4) adjust for claiming age
   → (5) apply COLA forward
   = benefit received in year n
```

**(1) Restate old earnings into today's wage levels:**

```
indexingFactor(y) = AWI(yearWorkerTurns60) / AWI(y)
indexedEarnings(y) = MIN(actualEarnings(y), wageBase(y)) × indexingFactor(y)
```

**(2) Average the best 35 years, per month:**

```
AIME = FLOOR( sum of highest 35 indexed years / 420 )
```

> Fewer than 35 years of work? The missing years count as **zero** and you still divide by 420. This is why a short career depresses the benefit so heavily.

**(3) Run it through the three tiers:**

```
PIA = 0.90 × MIN(AIME, 1286)
    + 0.32 × MAX(0, MIN(AIME, 7749) − 1286)
    + 0.15 × MAX(0, AIME − 7749)

PIA = FLOOR_TO_DIME(PIA)
```

The $1,286 and $7,749 figures are not arbitrary — you can derive them yourself:

```
bendPoint1 = ROUND( 180   × AWI(eligibilityYear − 2) / 9779.44 )
bendPoint2 = ROUND( 1085  × AWI(eligibilityYear − 2) / 9779.44 )
```

```
ratio = 69,846.57 / 9,779.44 = 7.142184
180   × 7.142184 = 1,285.59  → $1,286   ✓ matches published
1,085 × 7.142184 = 7,749.27  → $7,749   ✓ matches published
```

**(4) Adjust for when they claim.** Full retirement age is 67 for anyone born 1960 or later.

Claiming early:

```
monthsEarly = (FRA − claimAge) × 12

reduction = (5/9 of 1%) × MIN(monthsEarly, 36)
          + (5/12 of 1%) × MAX(0, monthsEarly − 36)

benefit = PIA × (1 − reduction)
```

Claiming late:

```
monthsDelayed = (claimAge − FRA) × 12        [capped at age 70]
credit  = (2/3 of 1%) × monthsDelayed
benefit = PIA × (1 + credit)
```

| Claim age | % of full benefit |
|---|---|
| 62 | 70% |
| 67 (full) | 100% |
| 70 | 124% ← stops growing here |

**(5) Add the annual cost-of-living increase:**

```
benefit(n) = adjustedBenefit × (1 + colaAssumption)^(n − claimYear)
```

### If the client has their SSA statement, skip steps 1–3

```
IF ssaStatementBenefit IS PROVIDED:
    PIA = ssaStatementBenefitAtFRA
    → go straight to Step 4
ELSE:
    compute AIME → PIA from earnings history
```

**Full detail →** [04-SOCIAL-SECURITY.md](04-SOCIAL-SECURITY.md)

---

# STEP 5 — RMD (forced withdrawals)

**In plain English.** The government let the client defer tax on their 401(k) for decades. Eventually it wants that tax. From age 73 or 75 it forces a minimum amount out every year whether they need it or not — and that money is fully taxable.

**When it starts** depends on birth year, so `birthYear` is a required input:

```
rmdAge = IF birthYear >= 1960 THEN 75
         ELSE IF birthYear >= 1951 THEN 73
         ELSE 72
```

```
requiredBeginningDate = April 1 of the year AFTER the first RMD year
```

**The calculation is one line:**

```
RMD(age) = priorYearEndBalance / applicableDenominator(age)
```

Two things to get right: the balance is the one from **31 December last year**, and the divisor comes from the IRS Uniform Lifetime Table using the age reached **during** the year.

```
RMD = 1,000,000 / 24.6 = $40,650
```

That is a client turning 75 with $1,000,000 — and it is the worked example printed in IRS Publication 590-B itself.

**It is fully taxable:**

```
rmdTaxableAmount = rmd    (100% ordinary income, if no after-tax basis)
```

**Unless it goes to charity:**

```
taxableRMD = MAX(0, rmd − qualifiedCharitableDistribution)
```

> A few divisors to show the shape: age 73 → 26.5, age 80 → 20.2, age 90 → 12.2, age 100 → 6.4. By the late 80s the forced withdrawal exceeds any realistic return, so **balances peak and then fall**. A roadmap showing retirement balances rising forever has not modelled RMDs.

> **Roth accounts are exempt.** Roth IRAs always were; Roth 401(k)s became exempt in 2024.

**Full detail →** [05-RMD.md](05-RMD.md)

---

# STEP 5b — Real estate classification (property owners only)

**In plain English.** Before any loss gate runs, each property has to be classified. Whether a loss is usable at all — and whether it is passive — is decided here, not later.

```
Q1  Is personal use excessive?          → §280A          → if yes, STOP: no loss allowed
Q2  Is the average stay ≤ 7 days?       → §1.469-1T      → if yes, NOT a rental activity
Q3  Does the owner materially participate? → §1.469-5T   → decides passive vs non-passive
```

```
threshold = MAX(14 days, 0.10 × daysRentedAtFairValue)

IF personalUseDays > threshold:
    property is a PERSONAL RESIDENCE
    deductions are CAPPED at rental income — no loss is allowed
    excess carries forward under §280A (not as a passive loss)
```

| Average stay | Material participation | Result |
|---|---|---|
| ≤ 7 days | **Yes** | **Non-passive** — losses offset W-2 income |
| ≤ 7 days | No | Passive — losses suspended |
| > 7 days | Yes, but not a REP | **Still passive** — hours do not help |
| > 7 days | REP + materially participates | Non-passive |
| > 7 days | Active participation only | Passive, but up to $25,000 allowance |

> Same property, same loss: **$203,409 deductible or $0**, decided only by average stay and hours.

> **A non-passive short-term rental loss skips Gate 3 but still meets Gate 4.** Clearing the 7-day test does not exempt the loss from the $512,000 excess business loss cap. REPS and the $25,000 allowance are both irrelevant to short-term rentals — they are rules about *rental activities*, and an STR under the 7-day rule is not one.

**Full detail →** [07-REAL-ESTATE-EQUITY.md](07-REAL-ESTATE-EQUITY.md)

---

# STEP 5a — Loss limitation gates (K-1 clients only)

**In plain English.** If the client has a K-1 from a partnership or S-corp, a loss on it cannot just be subtracted from income. It has to pass four gates in order, and whatever each gate blocks gets parked in its own bucket until a specific event releases it. Skip this and the model deducts losses that aren't deductible.

```
K-1 loss for the year
        │
        ▼
GATE 1  BASIS            §704(d) partnerships · §1366(d) S-corps
        │  blocked → suspendedBasis
        ▼
GATE 2  AT-RISK          §465
        │  blocked → suspendedAtRisk
        ▼
GATE 3  PASSIVE          §469
        │  blocked → suspendedPassive
        ▼
GATE 4  EXCESS BUSINESS LOSS   §461(l)
        │  blocked → becomes an NOL carryforward
        ▼
   Deductible against AGI
```

**The check that catches double-counting:**

```
allowedThisYear
  + Δ suspendedBasis
  + Δ suspendedAtRisk
  + Δ suspendedPassive
  = lossEnteringTheGates
```

> **The three suspended buckets have three different fates on a sale.** Passive losses release in full; at-risk losses offset the gain; basis losses **expire permanently**. They can never be merged into one number.

> **2026 change:** the §461(l) threshold **drops** to $256,000 single / $512,000 MFJ, and the rule is now permanent.

This step also brings NOL, capital-loss, negative-QBI and AMT-credit carryforwards into the year, and hands the closing state to next year.

**Full detail →** [11-LOSS-LIMITATIONS-AND-CARRYFORWARDS.md](11-LOSS-LIMITATIONS-AND-CARRYFORWARDS.md)

---

# STEP 6 — Taxable income

**In plain English.** Add up everything taxable, subtract what the law lets you subtract. Note that only *part* of Social Security counts, and pre-tax contributions come off before tax is calculated.

```
AGI = w2Income
    + k1Income
    + scheduleCProfit
    + rentalIncome
    + portfolioIncome
    + taxableSocialSecurity      ← module 04, NOT the gross benefit
    + rmd                        ← module 05
    + taxablePortfolioWithdrawal
    − pretaxContributions        ← module 03 (401k, HSA, SEP)
    − deductibleSelfEmploymentTax (half of SE tax)
```

```
taxableIncome = MAX(0, AGI − deduction − qbiDeduction)
```

### How much Social Security is taxable

First work out "provisional income":

```
provisionalIncome = AGI excluding Social Security
                  + tax-exempt interest (municipal bonds)
                  + 0.50 × grossSocialSecurityBenefit
```

Then compare it to the thresholds ($32,000 and $44,000 for a married couple):

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

> **85% is the maximum.** At least 15% of the benefit is always tax-free. And remember Rule 1 — these thresholds never rise with inflation, so nearly every retiree eventually hits the 85% tier.

**Full detail →** [02-TAXES.md](02-TAXES.md) · [04-SOCIAL-SECURITY.md](04-SOCIAL-SECURITY.md)

---

# STEP 7 — Tax

**In plain English.** Income is taxed in slices, not all at one rate. A couple with $300,000 does not pay 24% on all of it — they pay 10% on the first slice, 12% on the next, and so on. On top of the income tax sit payroll tax, an investment surtax, state tax, and Medicare surcharges.

### The order

```
STEP 6a  Gross income          (module 01)
STEP 6b  − Above-the-line deductions  → ADJUSTED GROSS INCOME (AGI)
STEP 6c  − Standard or itemized deduction
STEP 6d  − QBI deduction (§199A)
                                → TAXABLE INCOME
STEP 7a  Apply ordinary brackets to ordinary income
STEP 7b  Apply capital-gains brackets to LTCG, stacked on top
STEP 7c  + Payroll tax (FICA or self-employment)
STEP 7d  + NIIT 3.8% if applicable
STEP 7e  + State income tax
STEP 7f  + Medicare IRMAA (age 65+)
                                → TOTAL TAX
```

### The bracket walk — the most important formula in the file

```
tax = 0
previousCap = 0
FOR each bracket (cap, rate):
    slice = MIN(taxableIncome, cap) − previousCap
    IF slice <= 0: BREAK
    tax = tax + slice × rate
    previousCap = cap
```

> **Never multiply total income by the top rate.** It is the single most common error in projection engines.

### Capital gains stack on top of ordinary income

```
ordinaryTaxable = taxableIncome − longTermGains
gainsStartAt    = ordinaryTaxable

FOR each LTCG bracket (cap, rate):
    slice = MIN(gainsStartAt + longTermGains, cap) − MAX(gainsStartAt, previousCap)
    IF slice > 0: tax = tax + slice × rate
```

> Ordinary income fills the 0% gains bracket first. A client with $90,000 of salary and $50,000 of gains does **not** get the full 0% band.

### Senior bonus deduction — expires after 2028

```
reduction   = MAX(0, MAGI − threshold) × 0.06
seniorBonus = MAX(0, baseAmount − reduction)
```

> Switch this off in 2029. Leaving it on overstates the after-tax result for decades.

### Business income deduction

```
tentativeQBI = qualifiedBusinessIncome × 0.20
qbiDeduction = MIN(tentativeQBI, taxableIncomeBeforeQBI × 0.20)
```

> **Specified service businesses** — health, law, accounting, consulting, financial services, performing arts, athletics — **lose this deduction entirely** above the phase-out. **Engineering and architecture are excluded from that list by statute** and keep the full 20% at any income. Real estate, manufacturing, construction and most technology businesses are not SSTBs either. Flag the business type as an input; never infer it.

### Payroll tax

Employee:

```
ssTax       = MIN(wages, 184500) × 0.062
medicareTax = wages × 0.0145
addlMedicare = MAX(0, wages − threshold) × 0.009
```

Self-employed — double the rate, on 92.35% of profit:

```
seBase       = scheduleCProfit × 0.9235
seSocialSec  = MIN(seBase, 184500) × 0.124
seMedicare   = seBase × 0.029
deductibleHalf = (seSocialSec + seMedicare) × 0.5    ← subtract from AGI
```

### Investment surtax

```
niit = 0.038 × MIN(netInvestmentIncome, MAX(0, MAGI − threshold))
```

> **RMDs are not subject to this** — but they *raise* MAGI, which can push other investment income over the line. That indirect effect is real.

### Medicare surcharge, age 65+

```
irmaaAnnual = (partB(magi_from_2_years_ago) + partD(...)) × 12 × numberOfPeopleOnMedicare
```

> Note `magi_from_2_years_ago`. Medicare looks back two years. And it is a **cliff** — one dollar over a threshold costs the whole tier.

### AMT — the parallel rail

Run the whole return a second time under AMT rules and pay whichever is higher.

```
exemption = MAX(0, baseExemption − 0.50 × MAX(0, AMTI − phaseoutStart))
amtBase = MAX(0, AMTI − exemption)
TMT     = 0.26 × MIN(amtBase, 244500) + 0.28 × MAX(0, amtBase − 244500)
amtDue  = MAX(0, TMT − regularTax)
```

> 2026 exemption $90,100 / $140,200; phaseout starts $500,000 / $1,000,000 at a **50% rate** — doubled by OBBBA. Any model on 2025 parameters understates AMT.

**Full detail →** [02-TAXES.md](02-TAXES.md) · [11-LOSS-LIMITATIONS-AND-CARRYFORWARDS.md](11-LOSS-LIMITATIONS-AND-CARRYFORWARDS.md)

---

# STEP 8 — Cash flow

**In plain English.** What is left after living costs and taxes? If positive, it goes into savings. If negative, savings must cover the gap.

```
surplus = totalIncome − totalExpenses − totalTaxes
```

While working, the surplus funds the contributions from Step 3. In retirement the number is usually negative, and the shortfall is drawn from accounts in this order — cheapest tax first:

```
1. RMD (forced, no choice)
2. Taxable brokerage (lowest tax cost — only the gain is taxed)
3. Pre-tax (ordinary income)
4. Roth (last — preserve tax-free growth longest)
```

**Full detail →** [01-INCOME-AND-EXPENSES.md](01-INCOME-AND-EXPENSES.md) · [03-RETIREMENT-CONTRIBUTIONS-AND-GROWTH.md](03-RETIREMENT-CONTRIBUTIONS-AND-GROWTH.md)

---

# STEP 9 — Investment growth

**In plain English.** Balances earn a return each year. Contributions arrive throughout the year, not all on 1 January, so they are credited with roughly half a year of growth.

```
endBalance = (startBalance × (1 + r))
           + (contribution × (1 + r)^0.5)
           − (withdrawal × (1 + r)^0.5)
```

If you prefer month-by-month:

```
monthlyRate = (1 + r)^(1/12) − 1
FOR each month:
    balance = balance × (1 + monthlyRate) + monthlyContribution
```

> Use `(1 + r)^(1/12) − 1`, **not** `r / 12`. The shortcut runs about 0.2% a year high at 7%, which compounds visibly over 48 years.

**Costs come off the return:**

```
netReturn = grossReturn − advisoryFee − fundExpenseRatio
```

> **Do not subtract inflation here.** Inflation is handled once, in Step 13. Subtracting it twice can understate a 40-year result by half.

**Three account types, tracked separately** — because they are taxed differently and only one has RMDs:

```
pretaxBalance(n)  = pretaxBalance(n−1)  × (1+r) + pretaxContrib(n)  − rmd(n) − withdrawals
rothBalance(n)    = rothBalance(n−1)    × (1+r) + rothContrib(n)    − withdrawals
taxableBalance(n) = taxableBalance(n−1) × (1+r) + surplus(n)        − withdrawals
```

**Full detail →** [03-RETIREMENT-CONTRIBUTIONS-AND-GROWTH.md](03-RETIREMENT-CONTRIBUTIONS-AND-GROWTH.md)

---

# STEP 10 — Insurance cash value

**In plain English.** A permanent life policy builds a savings balance inside it. Handled correctly that balance grows tax-deferred and can be borrowed against tax-free. Handled incorrectly — overfund it, or let it lapse with a loan outstanding — and the tax benefits collapse.

**The yearly roll-forward:**

```
cashValue(n) = cashValue(n−1)
             + premium(n)
             − premiumLoad(n)          ← typically 5–8% of premium
             − costOfInsurance(n)      ← rises steeply with age
             − policyFees(n)           ← administrative, per-thousand charges
             + creditedInterest(n)
             − loanInterest(n)         ← if loans outstanding
```

**Insurance cost rises every year:**

```
costOfInsurance(n) = netAmountAtRisk(n) × mortalityRate(age) / 1000
netAmountAtRisk(n) = deathBenefit(n) − cashValue(n)
```

**For indexed policies, the return is capped and floored:**

```
rawIndexReturn = (indexEnd − indexStart) / indexStart
credited = MIN( MAX(rawIndexReturn × participationRate, floor), cap )
```

> Typical cap 9–10%, floor 0%. Because the cap truncates good years while the floor protects bad ones, modelling this as a flat "index average" **overstates results badly**.

**Test 1 — don't overfund it (the MEC test):**

```
IF cumulativePremiumsPaid(first 7 years) > 7 × netLevelPremium:
    policy is a MODIFIED ENDOWMENT CONTRACT
```

> If this trips, loans become taxable and the whole "tax-free income" premise disappears. It **cannot be undone**.

**The death benefit is forced up as cash value grows:**

```
requiredDeathBenefit(n) = MAX(faceAmount, cashValue(n) × corridor(age))
```

**Taking money out:**

```
availableLoan(n) = cashValue(n) × maxLoanPercentage   ← typically 0.90
loanBalance(n)   = loanBalance(n−1) × (1 + loanRate) + newLoan(n)
netCashValue(n)  = cashValue(n) − loanBalance(n)
```

```
basis = cumulativePremiumsPaid − priorWithdrawals

IF withdrawal <= basis:  tax = 0                    ← return of basis
ELSE:                    switch to loans for the remainder
```

**Test 2 — check every single year that the policy survives:**

```
IF netCashValue(n) < costOfInsurance(n) + fees(n):
    POLICY LAPSES
    taxableGain = loanBalance − basis
    FLAG this loudly — do not silently continue the projection
```

> This is the worst outcome in the product: the client owes tax on money they already borrowed and spent. A model that borrows to hit an income target without lapse-testing is producing a fictional number.

**What reaches the estate:**

```
netDeathBenefit = deathBenefit(n) − loanBalance(n)
```

**Full detail →** [06-INSURANCE-CASH-VALUE.md](06-INSURANCE-CASH-VALUE.md)

---

# STEP 11 — Real estate equity

**In plain English.** Equity grows from two directions at once — the property appreciates while the mortgage shrinks. That is why property compounds faster than the appreciation rate alone suggests.

```
equity = propertyValue − mortgageBalance
```

**The property rises:**

```
propertyValue(n) = propertyValue(0) × (1 + appreciationRate)^n
```

**The mortgage falls:**

```
i = annualRate / 12
N = termInMonths

payment = P × [ i × (1 + i)^N ] / [ (1 + i)^N − 1 ]
```

```
balance(m) = P × [ (1 + i)^N − (1 + i)^m ] / [ (1 + i)^N − 1 ]
```

Splitting a year into interest and principal (interest is deductible):

```
FOR each month:
    interestPortion  = balance × i
    principalPortion = payment − interestPortion
    balance          = balance − principalPortion
```

```
equity(n) = propertyValue(n) − balance(n)
```

> **Early payments are almost all interest.** On $500,000 at 6.5%, year one pays $37,924 but only $5,589 comes off the balance. Assuming straight-line paydown badly overstates early equity.

**Rental cash flow:**

```
netOperatingIncome = rentalIncome
                   − propertyTax
                   − insurance
                   − maintenance
                   − managementFees
                   − vacancyAllowance

netCashFlow = netOperatingIncome − annualMortgagePayment
```

**Depreciation on rentals — land is not depreciable:**

```
annualDepreciation = (purchasePrice − landValue) / 27.5
```

**And it comes back on sale:**

```
adjustedBasis   = costBasis + improvements − accumulatedDepreciation
gainOnSale      = salePrice − sellingCosts − adjustedBasis
recaptureAmount = MIN(accumulatedDepreciation, gainOnSale)   → taxed at 25%
remainingGain   = gainOnSale − recaptureAmount               → taxed at LTCG rates
```

> Unless it is held until death — then Step 12's step-up wipes both the gain **and** the recapture out entirely.

**Multiple properties are summed, not averaged:**

```
totalRealEstateEquity(n) = SUM over properties of ( value(n) − balance(n) )
```

**Full detail →** [07-REAL-ESTATE-EQUITY.md](07-REAL-ESTATE-EQUITY.md)

---

# STEP 12 — Estate value

**In plain English.** Net worth is not what the heirs get. Two accounts of identical size can deliver very different amounts, because a 401(k) still owes income tax and a brokerage account does not.

```
STEP 1   Gross estate            (everything the decedent owned or controlled)
STEP 2   − Debts, funeral, administration expenses
STEP 3   − Marital deduction     (unlimited, to a US-citizen spouse)
STEP 4   − Charitable deduction
                                 = TAXABLE ESTATE
STEP 5   + Adjusted taxable gifts (lifetime gifts above the annual exclusion)
STEP 6   − Applicable exclusion  ($15,000,000 in 2026, + any DSUE ported from a spouse)
                                 = AMOUNT SUBJECT TO TAX
STEP 7   × 40%                   = ESTATE TAX
STEP 8   − Income tax the heirs will owe on IRD assets
                                 = NET TO HEIRS
```

> **Step 8 is the one most models skip**, and it is the difference between a headline number and a true one.

**A widow(er) can inherit the unused exclusion — but only if a return was filed:**

```
survivorExclusion = ownExclusion + DSUE
```

### Life insurance — who owns it decides everything

```
IF decedent held ANY "incident of ownership":
    grossEstate = grossEstate + fullDeathBenefit     ← taxed at 40%
ELSE (properly structured ILIT):
    grossEstate unchanged                            ← passes entirely outside the estate
```

> On a $5,000,000 policy in a taxable estate, that titling decision is worth **$2,000,000**.

### The split that decides the real legacy

Most assets reset their cost basis at death — all the built-up gain disappears:

```
heirBasis = fairMarketValueAtDeath
```

But retirement accounts do **not**. They are "income in respect of a decedent" and the heirs pay full ordinary income tax:

| | $3M traditional IRA | $3M brokerage (with $1M gain) |
|---|---|---|
| Heirs' income tax | ~$1.11M | **$0** — stepped up |
| Net to heirs | **$1.89M** | **$3.00M** |

If estate tax was actually paid, heirs get partial relief:

```
IF estateTaxPaid > 0:
    ird691cDeduction = estateTax attributable to the IRD asset
    heirTaxableAmount = irdAmount − ird691cDeduction
```

### The honest number

```
netToHeirs = grossEstate
           − debts
           − estateTax
           − heirIncomeTaxOnIRD
           + lifeInsuranceOutsideEstate
```

**Full detail →** [08-ESTATE-VALUE.md](08-ESTATE-VALUE.md)

---

# STEP 13 — Convert to today's dollars

**In plain English.** Everything so far is in future dollars. $15 million in 2074 does not buy what $15 million buys now. This is the *only* place inflation is applied to the output.

```
realValue(year n) = nominalValue(year n) / (1 + inflation)^n
```

Apply it once, to the finished row, immediately before display.

> If you already subtracted inflation from the investment return in Step 9, **stop** — you would be counting it twice.

**Full detail →** [00-OVERVIEW-AND-YEAR-LOOP.md](00-OVERVIEW-AND-YEAR-LOOP.md)

---

# One full year, worked

A 42-year-old couple, $420,000 salary, $198,000 of expenses, $272,000 of deployable capital.

```
STEP 1  Income          W-2                            = $420,000
STEP 2  Expenses        180,000 + 18,000               = $198,000
STEP 3  Contributions   DWC                            = $272,000
STEP 4  Social Security age 42 < 67                    = $0
STEP 5  RMD             age 42 < 75                    = $0

STEP 6  Taxable income
        AGI                                            = $420,000
        − standard deduction (MFJ)                     = −$32,200
        = taxable income                               = $387,800

STEP 7  Tax
        Federal (bracket walk):
             0 →  24,800  @10%                         =   $2,480
        24,800 → 100,800  @12%                         =   $9,120
       100,800 → 211,400  @22%                         =  $24,332
       211,400 → 387,800  @24%                         =  $42,336
        federal                                        =  $78,268
        payroll  (184,500 × 6.2% + 420,000 × 1.45%)    =  $17,529
        state    (387,800 × 6%)                        =  $23,268
        TOTAL TAX                                      = $119,065

STEP 9  Growth — each bucket grows at its own rate, contribution applied mid-year
STEP 13 Deflate by (1.025)^0                           = ×1.0

        END-OF-YEAR NET WORTH                          = $2,134,995
```

Effective federal rate **18.6%**. Marginal rate **24%**. Both matter — the marginal rate drives planning decisions, the effective rate drives the cash-flow line.

**The full 48-year table →** [09-WORKED-EXAMPLE.md](09-WORKED-EXAMPLE.md)

---

# Quick constants card — 2026

The dozen figures used most. Full tables are in the modules.

| What | Value |
|---|---|
| Standard deduction (MFJ / single) | $32,200 / $16,100 |
| Top bracket starts (MFJ) | $768,700 |
| 401(k) limit / 50+ / 60–63 | $24,500 / $32,500 / $35,750 |
| IRA limit / catch-up | $7,500 / $1,100 |
| Social Security wage base | $184,500 |
| Social Security COLA | 2.8% |
| PIA bend points | $1,286 / $7,749 |
| Full retirement age | 67 (born 1960+) |
| SS taxation thresholds (MFJ) — **frozen** | $32,000 / $44,000 |
| RMD age | 73 (born 1951–59) / **75 (born 1960+)** |
| Estate exclusion / rate | $15,000,000 / 40% |
| Medicare Part B standard | $202.90/mo |

**Full tables →** [10-SOURCES-AND-COMPETITORS.md](10-SOURCES-AND-COMPETITORS.md)

---

# Sources — which formula came from where

Every formula in this guide, and its origin. **Law** means the number or method is fixed by statute or regulation. **Math** means it is a standard identity, not a legal rule. **Convention** means it is a modelling choice we made — defensible, but changeable.

### Step 1–2 · Income and expenses

| Formula | Type | Source | Google this |
|---|---|---|---|
| `income(n) = income(0) × (1 + growthRate)^n` | Math | Compound growth identity | `compound annual growth rate formula` |
| Replacement ratio 70–80% | Convention | SSA replacement-rate research | `SSA replacement rate retirement income policy` |
| Healthcare inflation > CPI | Convention | CMS National Health Expenditure Projections | `CMS National Health Expenditure Projections` |
| Retirement expense factor 0.85 | Convention | BLS Consumer Expenditure Survey by age | `BLS Consumer Expenditure Survey age of reference person` |

### Step 3 · Contributions

| Formula | Type | Source | Google this |
|---|---|---|---|
| `catchUp` bands (8,000 / 11,250) | **Law** | IRS Notice 2025-67 (IR-2025-111) | `IRS 401k limit increases to 24500 for 2026` |
| `limit401k = 24500 + catchUp` | **Law** | IRC §402(g), same notice | same |
| Mandatory Roth catch-up over $150,000 | **Law** | SECURE 2.0 Act §603 | `SECURE 2.0 Roth catch-up contributions 2026` |
| Roth IRA phase-out proration | **Law** | IRC §408A | `Roth IRA income limits 2026 phase out` |
| `ROUND_DOWN_TO_500` indexing | Convention | Approximates the statutory indexing method | `IRS retirement plan limits cost of living adjustments` |

### Step 4 · Social Security

| Formula | Type | Source | Google this |
|---|---|---|---|
| `indexingFactor = AWI(age60) / AWI(y)` | **Law** | SSA wage-indexing rules | `SSA indexing factors average wage index` |
| `AIME = FLOOR(highest 35 / 420)` | **Law** | IRC §215(b) | `SSA average indexed monthly earnings AIME` |
| `PIA = 0.90/0.32/0.15 × slices` | **Law** | IRC §215(a) | `SSA primary insurance amount bend points formula` |
| Bend points $1,286 / $7,749 | **Law** | **Federal Register 2025-19763** | `Cost-of-Living Increase and Other Determinations for 2026` |
| `bendPoint = ROUND(180 × AWI/9779.44)` | **Law** | Same notice — derivation stated in the text | same |
| Early reduction 5/9 then 5/12 of 1% | **Law** | 20 CFR §404.313 | `SSA early or late retirement reduction factors` |
| Delayed credit 2/3 of 1%, cap age 70 | **Law** | IRC §202(w) | `SSA delayed retirement credits` |
| COLA 2.8% | **Law** | Federal Register 2025-19763 | same as bend points |
| Provisional income + 50/85% tiers | **Law** | IRC §86 · IRS Pub 915 | `IRS Publication 915 Social Security benefits taxable` |
| Thresholds never indexed | **Law** | CRS RL32552 / IF11397 | `CRS Social Security Taxation of Benefits` |

### Step 5 · RMD

| Formula | Type | Source | Google this |
|---|---|---|---|
| `rmdAge` 73 / 75 by birth year | **Law** | SECURE 2.0 Act §107 | `IRS required minimum distribution FAQs SECURE 2.0` |
| `requiredBeginningDate` = 1 April | **Law** | IRC §401(a)(9) · IRS Pub 590-B | `IRS Publication 590-B required beginning date` |
| `RMD = priorYearEndBalance / denominator` | **Law** | **IRS Pub 590-B, Appendix B, Table III** | `IRS Publication 590-B Appendix B Table III Uniform Lifetime` |
| Divisor table (72→27.4 … 120→2.0) | **Law** | Same — extracted from the IRS PDF | same |
| QCD offset, $111,000 | **Law** | IRC §408(d)(8) · Notice 2025-67 | `2026 qualified charitable distribution limit` |

### Step 6–7 · Taxes

| Formula | Type | Source | Google this |
|---|---|---|---|
| Bracket walk (slice by slice) | **Law** | IRC §1 · Rev. Proc. 2025-32 | `IRS 2026 inflation adjustments One Big Beautiful Bill` |
| 2026 brackets and standard deduction | **Law** | IRS Rev. Proc. 2025-32 | same |
| LTCG stacking on ordinary income | **Law** | IRC §1(h) | `2026 capital gains tax brackets Rev Proc 2025-32` |
| Senior bonus deduction, 6% phase-out | **Law** | OBBBA (P.L. 119-21), 2025–2028 only | `OBBBA senior bonus deduction 65 phase out` |
| `qbiDeduction` 20% with taxable-income cap | **Law** | IRC §199A · OBBBA §70105 | `OBBBA section 70105 QBI deduction permanent` |
| FICA 6.2% / 1.45% / 0.9%, base $184,500 | **Law** | IRC §3101 · Federal Register 2025-19763 | `OASDI contribution and benefit base 2026` |
| SE tax on 92.35%, half deductible | **Law** | IRC §1401, §164(f) | `IRS self-employment tax 92.35 percent` |
| `niit = 0.038 × MIN(NII, MAGI − threshold)` | **Law** | IRC §1411 | `CRS 3.8% Net Investment Income Tax IF11820` |
| NIIT thresholds frozen since 2013 | **Law** | IRC §1411 — no indexing provision | same |
| IRMAA, two-year lookback | **Law** | CMS 2026 fact sheet | `CMS 2026 Medicare Parts A B premiums deductibles` |

### Step 5b · Real estate classification

| Formula | Type | Source | Google this |
|---|---|---|---|
| ≤7-day rule — not a rental activity | **Law** | Reg. §1.469-1T(e)(3)(ii)(A) | `1.469-1T(e)(3)(ii)(A) seven day average rental` |
| Seven material participation tests | **Law** | Reg. §1.469-5T(a) | `1.469-5T material participation seven tests` |
| §280A personal use, 14 days / 10% | **Law** | IRC §280A | `section 280A vacation home 14 days 10 percent` |
| REPS 750 hrs + 50% | **Law** | IRC §469(c)(7) | `real estate professional 750 hours` |

### Step 5a · Loss limitation gates

| Formula | Type | Source | Google this |
|---|---|---|---|
| Four-gate ordering (basis → at-risk → passive → EBL) | **Law** | IRC §704(d)/§1366(d), §465, §469, §461(l) | `order of loss limitations basis at-risk passive excess business loss` |
| EBL threshold $256,000 / $512,000 (2026) | **Law** | IRS Rev. Proc. 2025-32 | `Rev Proc 2025-32 excess business loss threshold 2026` |
| Conservation identity | Math | Accounting check — stated in module 11 | — |

### Step 7c · AMT

| Formula | Type | Source | Google this |
|---|---|---|---|
| AMT exemption, 50% phaseout | **Law** | IRS Rev. Proc. 2025-32 · OBBBA §70107 | `2026 AMT exemption 90,100 140,200 phaseout 500,000` |
| 26% / 28% rates, $244,500 break | **Law** | IRC §55(b) · Rev. Proc. 2025-32 | `2026 AMT 28 percent rate threshold 244,500` |
| Minimum tax credit | **Law** | IRC §53 | `IRC 53 minimum tax credit deferral items` |

### Step 8 · Cash flow

| Formula | Type | Source | Google this |
|---|---|---|---|
| `surplus = totalIncome − totalExpenses − totalTaxes` | Math | Accounting identity — stated here for the first time; module 00 names the step but gives no formula | — |
| Withdrawal order (RMD → taxable → pre-tax → Roth) | Convention | Industry-standard tax-efficient sequencing | `tax efficient withdrawal sequencing retirement` |

### Step 9 · Growth

| Formula | Type | Source | Google this |
|---|---|---|---|
| `endBalance` with `(1+r)^0.5` mid-year | Convention | Standard mid-period actuarial convention | `mid year convention future value contributions` |
| `monthlyRate = (1+r)^(1/12) − 1` | Math | Effective-rate conversion | `effective annual rate to monthly rate conversion` |
| Three-bucket separation | **Law** (drives it) | Different tax treatment per registration | `traditional vs Roth vs taxable account tax treatment` |
| Withdrawal order (taxable → pre-tax → Roth) | Convention | Industry standard tax-efficient sequencing | `tax efficient withdrawal sequencing retirement` |

### Step 10 · Insurance

| Formula | Type | Source | Google this |
|---|---|---|---|
| CVAT / GPT qualification | **Law** | IRC §7702 | `IRC 7702 life insurance contract defined` |
| `requiredDeathBenefit` corridor | **Law** | IRC §7702(d) | `IRC 7702 cash value corridor applicable percentage` |
| 7-pay / MEC test | **Law** | IRC §7702A | `IRC 7702A modified endowment contract seven pay test` |
| Basis-first withdrawal ordering | **Law** | IRC §72(e) | `IRC 72(e) life insurance distributions basis first` |
| Death benefit income-tax-free | **Law** | IRC §101(a) | `IRC 101(a) life insurance proceeds excluded` |
| Illustrated rate ≤ 145% of portfolio | **Law** (regulatory) | NAIC Actuarial Guideline 49-B | `NAIC Actuarial Guideline 49-B maximum illustrated rate` |
| `cashValue(n)` roll-forward, COI, cap/floor | Convention | Standard policy mechanics | `indexed universal life cost of insurance cap floor` |

### Step 11 · Real estate

| Formula | Type | Source | Google this |
|---|---|---|---|
| `payment = P × [i(1+i)^N] / [(1+i)^N − 1]` | Math | Standard amortisation identity | `mortgage amortization formula derivation` |
| `balance(m)` closed form | Math | Same identity, rearranged | `remaining loan balance formula` |
| `annualDepreciation` over 27.5 years | **Law** | IRC §168 · IRS Pub 527 | `IRS Publication 527 residential rental depreciation` |
| Depreciation recapture at 25% | **Law** | IRC §1250 | `IRS unrecaptured section 1250 gain 25 percent` |
| Mortgage interest cap $750,000 | **Law** | IRC §163(h) · IRS Pub 936 | `IRS Publication 936 mortgage interest deduction limit` |
| §121 home sale exclusion | **Law** | IRC §121 · IRS Pub 523 | `IRS Publication 523 selling your home exclusion` |

### Step 12 · Estate

| Formula | Type | Source | Google this |
|---|---|---|---|
| Gross estate → taxable estate → tax | **Law** | IRC §2001, §2031–2056 | `IRS Form 706 instructions estate tax computation` |
| Exclusion $15,000,000, rate 40% | **Law** | Rev. Proc. 2025-32 · OBBBA | `IRS 2026 estate tax basic exclusion 15 million` |
| `survivorExclusion = own + DSUE` | **Law** | IRC §2010(c) | `Form 706 portability DSUE election` |
| Insurance inclusion / incidents of ownership | **Law** | IRC §2042 | `IRC 2042 incidents of ownership life insurance` |
| Three-year pullback on transfers | **Law** | IRC §2035 | `IRC 2035 three year rule life insurance` |
| `heirBasis = FMV at death` | **Law** | IRC §1014 | `IRC 1014 basis property acquired from decedent` |
| IRD — no step-up on retirement accounts | **Law** | IRC §691(a) | `IRC 691 income in respect of a decedent` |
| `ird691cDeduction` | **Law** | IRC §691(c) | `IRC 691(c) IRD deduction inherited IRA` |
| Heirs' marginal rate assumption | Convention | Modelling choice — 32–37% typical | `10 year rule inherited IRA tax` |

### Step 13 · Deflation

| Formula | Type | Source | Google this |
|---|---|---|---|
| `realValue = nominal / (1 + inflation)^n` | Math | Standard present-value deflator | `real versus nominal dollars formula` |

---

## Primary sources of record

| Topic | Document |
|---|---|
| 2026 brackets, deductions, estate exclusion | [IRS Rev. Proc. 2025-32](https://www.irs.gov/newsroom/irs-releases-tax-inflation-adjustments-for-tax-year-2026-including-amendments-from-the-one-big-beautiful-bill) |
| 2026 retirement plan limits | [IRS Notice 2025-67](https://www.irs.gov/newsroom/401k-limit-increases-to-24500-for-2026-ira-limit-increases-to-7500) |
| 2026 Social Security parameters | [Federal Register 2025-19763](https://www.federalregister.gov/documents/2025/11/03/2025-19763/cost-of-living-increase-and-other-determinations-for-2026) |
| Uniform Lifetime Table | [IRS Publication 590-B](https://www.irs.gov/pub/irs-pdf/p590b.pdf) |
| 2026 Medicare premiums and IRMAA | [CMS fact sheet](https://www.cms.gov/newsroom/fact-sheets/2026-medicare-parts-b-premiums-deductibles) |

> `ssa.gov` blocks automated access. The Federal Register notice is the **legally authoritative** publication of the same figures and is freely readable — cite it.

---

## Where to go next

| If you want | Read |
|---|---|
| The order of operations in depth | [00-OVERVIEW-AND-YEAR-LOOP.md](00-OVERVIEW-AND-YEAR-LOOP.md) |
| Income and expense detail | [01-INCOME-AND-EXPENSES.md](01-INCOME-AND-EXPENSES.md) |
| Full tax tables | [02-TAXES.md](02-TAXES.md) |
| Contribution limits and growth | [03-RETIREMENT-CONTRIBUTIONS-AND-GROWTH.md](03-RETIREMENT-CONTRIBUTIONS-AND-GROWTH.md) |
| Social Security in depth | [04-SOCIAL-SECURITY.md](04-SOCIAL-SECURITY.md) |
| The complete RMD divisor table | [05-RMD.md](05-RMD.md) |
| Insurance policy mechanics | [06-INSURANCE-CASH-VALUE.md](06-INSURANCE-CASH-VALUE.md) |
| Property and mortgage detail | [07-REAL-ESTATE-EQUITY.md](07-REAL-ESTATE-EQUITY.md) |
| Estate planning detail | [08-ESTATE-VALUE.md](08-ESTATE-VALUE.md) |
| The full 48-year worked table | [09-WORKED-EXAMPLE.md](09-WORKED-EXAMPLE.md) |
| Test vectors and competitor benchmark | [10-SOURCES-AND-COMPETITORS.md](10-SOURCES-AND-COMPETITORS.md) |
| K-1 losses, at-risk, passive, NOL, AMT, carryforwards | [11-LOSS-LIMITATIONS-AND-CARRYFORWARDS.md](11-LOSS-LIMITATIONS-AND-CARRYFORWARDS.md) |
| Examples, risks, client explanations | [HANDBOOK.md](HANDBOOK.md) |
