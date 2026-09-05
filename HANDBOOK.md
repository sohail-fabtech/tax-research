# Roadmap to Age 90™ — Handbook

**How every number is calculated, what it means, and where it goes wrong.**

Tax year **2026** · Market **United States** · Verified **September 2026**

---

## How to use this document

| If you are… | Read | Skip |
|---|---|---|
| **The client** | *What it does* · *Why it matters* · both examples · the risk table | The formula boxes |
| **The advisor** | Everything, especially the risk tables | — |
| **The developer** | The order diagram · the formula boxes · the risk tables | The plain-English openers |

Every step below follows the same shape:

> **What it does** — one sentence, no jargon
> **Why it matters** — the money consequence
> **The formula** — exactly as it will be built
> **Example 1** — the rule does *not* bite
> **Example 2** — the rule *does* bite
> **Risks and common mistakes** — what goes wrong, who it hurts, how to prevent it

The two examples always **contrast**. That is deliberate: the boundary between them is where the money is, and where nearly every modelling error lives.

**Related documents:** [MASTER-GUIDE.md](MASTER-GUIDE.md) is the developer build reference. Modules [00](00-OVERVIEW-AND-YEAR-LOOP.md)–[11](11-LOSS-LIMITATIONS-AND-CARRYFORWARDS.md) hold the full detail and every source citation.

---

## The calculation order

Twenty steps, run in this exact sequence, once per year, for 48 years.
**The order is part of the maths.** Swap any two and the answer changes.

```
                    ┌─────────────────────────────┐
                    │   OPENING STATE FROM LAST   │
                    │  YEAR — balances, suspended │
                    │  losses, NOL, credits       │
                    └──────────────┬──────────────┘
                                   │
   ── EARN AND SPEND ──────────────▼──────────────────────────────
    1  INCOME  ──────────────►  2  EXPENSES
       │
    3  CONTRIBUTIONS
       │
   ── FORCED INCOME ───────────────────────────────────────────────
    4  SOCIAL SECURITY  ────►  5  RMD
       │                          │
   ── THE FOUR GATES (K-1 clients only) ───────────────────────────
       │                          │
    6  GATE 1  BASIS        §704(d) / §1366(d)
       │  blocked ──► suspendedBasis
    7  GATE 2  AT-RISK      §465
       │  blocked ──► suspendedAtRisk
    8  GATE 3  PASSIVE      §469
       │  blocked ──► suspendedPassive
    9  GATE 4  EXCESS BUSINESS LOSS   §461(l)
       │  blocked ──► NOL carryforward
       │
   ── ASSEMBLE AND TAX ────────────▼──────────────────────────────
   10  AGI
       │
   11  REGULAR TAX ────┬──── 12  QBI DEDUCTION
       │               │
       │        ┌──────┴───────┬──────────────┐
       │        ▼              ▼              ▼
       │   REGULAR RAIL   13 NIIT RAIL   14 AMT RAIL
       │        │              │              │
       │        └──────┬───────┴──────────────┘
       │               ▼
       │         PAY THE HIGHER OF REGULAR vs AMT, PLUS NIIT
       │
   ── SETTLE AND GROW ─────────────▼──────────────────────────────
   15  CASH FLOW  ────►  16  GROWTH
                              │
                    ┌─────────┼─────────┐
                    ▼         ▼         ▼
              17 INSURANCE  18 REAL ESTATE
                    │         │
                    └────┬────┘
                         ▼
                   19  ESTATE VALUE
                         │
                   20  DEFLATE TO TODAY'S DOLLARS
                         │
                    ┌────▼────────────────────────┐
                    │  CLOSING STATE → NEXT YEAR  │
                    └─────────────────────────────┘
```

### Three parallel rails

Steps 11, 13 and 14 are **three separate calculations on the same year**, each with its own income definition. They do not feed each other.

| Rail | Income base | Result |
|---|---|---|
| **Regular** | Taxable income | Regular tax |
| **NIIT** | Net investment income vs MAGI | 3.8% surtax |
| **AMT** | AMTI (its own add-backs) | Pay the higher of AMT or regular |

---

## The whole system on one page

| # | Step | What it answers | Biggest risk |
|---|---|---|---|
| 1 | Income | What comes in? | Earned income doesn't stop at retirement |
| 2 | Expenses | What goes out? | Healthcare inflated at the general rate |
| 3 | Contributions | What can we save? | Age 60–63 catch-up stacked instead of replacing |
| 4 | Social Security | What does the government pay? | Claiming age adjustment missed |
| 5 | RMD | What are we forced to withdraw? | Wrong start age (73 vs 75) |
| 6 | Gate 1 — Basis | Do we have investment to absorb the loss? | Partnership vs S-corp debt rules confused |
| 7 | Gate 2 — At-risk | Could we actually lose it? | Nonrecourse debt wrongly treated as at-risk |
| 8 | Gate 3 — Passive | Can it offset this income? | Losses deducted against salary |
| 9 | Gate 4 — EBL | Is the loss over the cap? | Using the 2025 threshold |
| 10 | AGI | What is our income for tax? | Gross Social Security added instead of taxable part |
| 11 | Regular tax | What do we owe? | Flat marginal rate instead of the bracket walk |
| 12 | QBI | Do we get the 20% break? | SSTB phase-out ignored |
| 13 | NIIT | Do we owe the 3.8% surtax? | Reusing regular-tax income figures |
| 14 | AMT | Is the shadow tax higher? | 2025 AMT parameters |
| 15 | Cash flow | Surplus or shortfall? | Taxes not deducted before the surplus |
| 16 | Growth | What did it earn? | `r/12` instead of the true monthly rate |
| 17 | Insurance | What is in the policy? | No lapse test |
| 18 | Real estate | How much equity, and is the loss usable? | Classification skipped — passive vs non-passive |
| 19 | Estate | What reaches the heirs? | Net worth reported as legacy |
| 20 | Deflate | What is it really worth? | Inflation counted twice, or not at all |

---

# STEP 1 — Income

**What it does.** Works out how much money comes in each year, from every source.

**Why it matters.** On the day the client retires, their salary goes to **zero**. Everything after that has to come from Social Security, forced retirement withdrawals, rent, and their own savings. This step is where that cliff appears.

### The formula

```
income(n) = income(0) × (1 + growthRate)^n
```

```
totalIncome(n) = socialSecurity(n)        ← module 04
               + rmd(n)                    ← module 05
               + portfolioWithdrawal(n)     ← below
               + rental(n)                  ← module 07
```

```
portfolioWithdrawal(n) = MAX(0,
      targetRetirementIncome(n)
    − socialSecurity(n)
    − rmd(n)
    − rental(n)
)
```

### Example 1 — still working (age 45)

Salary $420,000, growing 3% a year, three years in:

```
$420,000 × 1.03³ = $458,945
```

One source, one formula. Nothing else is needed.

### Example 2 — first year of retirement (age 62)

The same client, twenty years later. Final salary was **$758,567**. Target retirement income is 75% of it — **$568,925**.

```
Social Security       $0        ← not claiming until 67
RMD                   $0        ← not until age 75
Rental                $24,000
                     ─────────
Portfolio must supply $544,925
```

**The difference:** earned income fell from **$758,567 to $0 in a single year**, and the portfolio has to replace almost all of it — five years before Social Security starts and thirteen before the first RMD.

### Risks and common mistakes

| What goes wrong | Who it hurts | How to prevent it |
|---|---|---|
| Salary keeps growing past retirement age | Client — projection is fantasy | Hard-zero earned income at `retirementAge` |
| `portfolioWithdrawal` goes negative and is treated as income | Developer — silent corruption | Floor at zero with `MAX(0, …)` |
| The gap years (62 → 67 → 75) not modelled separately | Client — misses the biggest planning window in the plan | Treat retirement→RMD as its own phase |
| All income sources grown at one rate | Both — rent and salary do not move together | Grow each source independently |

**Detail →** [01-INCOME-AND-EXPENSES.md](01-INCOME-AND-EXPENSES.md)

---

# STEP 2 — Expenses

**What it does.** Grows the cost of living forward, with medical costs tracked on their own line.

**Why it matters.** Medical inflation runs roughly double general inflation. Over 30 years that gap turns healthcare from a minor line item into a quarter of the entire budget.

### The formula

```
baseExpenses(0)  = (monthlyLifestyleExpenses × 12)
generalExpense(n) = baseExpenses(0) × (1 + inflation)^n
```

```
healthcare(0)  = monthlyMedicalInsurance × 12
healthcare(n)  = healthcare(0) × (1 + healthcareInflation)^n
```

```
IF age ≥ retirementAge:
    generalExpense(n) = generalExpense(n) × retirementExpenseFactor
```

### Example 1 — today (age 42)

```
General     $96,000
Healthcare  $14,400
            ────────
Total      $110,400      healthcare is 13% of the budget
```

### Example 2 — thirty years on (age 72)

General at 2.5%, healthcare at 5%:

```
General    $201,366      multiplied 2.10×
Healthcare  $62,236      multiplied 4.32×
            ────────
Total      $263,602      healthcare is now 24% of the budget
```

**The difference:** healthcare grew **more than twice as fast** as everything else. A model using one inflation rate for both would show healthcare at roughly $30,000 instead of $62,236 — understating lifetime spending by hundreds of thousands.

### Risks and common mistakes

| What goes wrong | Who it hurts | How to prevent it |
|---|---|---|
| Healthcare inflated at general CPI | Client — under-funds the years they are least able to earn | Separate rate, ~5% |
| Retirement step-down applied to healthcare too | Client — double optimism | Apply the 0.85 factor to general spending only |
| Medicare premiums omitted before 65 / after 65 | Both | Zero before 65, IRMAA-driven after |
| Expenses deflated here as well as at Step 20 | Developer — inflation counted twice | Deflate once, at Step 20 |

**Detail →** [01-INCOME-AND-EXPENSES.md](01-INCOME-AND-EXPENSES.md)

---

# STEP 3 — Retirement contributions

**What it does.** Caps how much can go into a 401(k), based on age.

**Why it matters.** There is a four-year window — ages 60 to 63 — when the limit jumps. Then it **drops back down** at 64. Most people, and most software, get this wrong in the same way.

### The formula

```
catchUp =
    IF age >= 60 AND age <= 63:  11250
    ELSE IF age >= 50:            8000
    ELSE:                            0

limit401k = 24500 + catchUp
contribution401k = MIN(desiredContribution, limit401k, earnedIncome)
```

### Example 1 — age 62, the peak

```
$24,500 base + $11,250 super catch-up = $35,750
```

### Example 2 — age 64, two years later

```
$24,500 base +  $8,000 standard catch-up = $32,500
```

**The difference:** the limit **falls by $3,250** at age 64. The super catch-up exists only for ages 60, 61, 62 and 63.

> **The error almost everyone makes.** Adding the super catch-up *on top of* the standard one gives `24,500 + 8,000 + 11,250 = $43,750` — overstating the limit by **$8,000 a year**. The age 60–63 catch-up **replaces** the age-50 catch-up. It does not stack.

### Risks and common mistakes

| What goes wrong | Who it hurts | How to prevent it |
|---|---|---|
| Super catch-up stacked on the standard one | Client — plans around $8,000/yr that cannot be contributed | `ELSE IF`, never `+` |
| Limit held flat for 48 years | Client — understates lifetime savings badly | Index limits forward |
| Roth catch-up requirement ignored | Client — expects a deduction they no longer get | From 2026, if prior-year wages > $150,000 the catch-up **must** be Roth |
| Contribution exceeds earned income | Developer | `MIN(…, earnedIncome)` |

**Detail →** [03-RETIREMENT-CONTRIBUTIONS-AND-GROWTH.md](03-RETIREMENT-CONTRIBUTIONS-AND-GROWTH.md)

---

# STEP 4 — Social Security

**What it does.** Averages the client's best 35 years of earnings, runs them through a three-tier formula, then adjusts for the age they start claiming.

**Why it matters.** The claiming decision is **permanent**. Choose at 62 instead of 67 and every cheque for the rest of their life is 30% smaller.

### The formula

```
AIME = FLOOR( sum of highest 35 indexed years / 420 )
```

```
PIA = 0.90 × MIN(AIME, 1286)
    + 0.32 × MAX(0, MIN(AIME, 7749) − 1286)
    + 0.15 × MAX(0, AIME − 7749)

PIA = FLOOR_TO_DIME(PIA)
```

```
monthsEarly = (FRA − claimAge) × 12

reduction = (5/9 of 1%) × MIN(monthsEarly, 36)
          + (5/12 of 1%) × MAX(0, monthsEarly − 36)

benefit = PIA × (1 − reduction)
```

### Example 1 — claiming at 67 (full retirement age)

AIME of $10,000:

```
90% × $1,286           = $1,157.40
32% × $6,463           = $2,068.16
15% × $2,251           =   $337.65
                        ──────────
PIA                     $3,563.20/month  =  $42,758/year
```

### Example 2 — claiming at 62, same earnings record

```
$3,563.20 × (1 − 0.30) = $2,494/month  =  $29,931/year
```

**The difference:** **$12,828 every year, for life.** Over the 28 years to age 90 that is **$359,171** — before COLA, which compounds the gap wider still.

### Risks and common mistakes

| What goes wrong | Who it hurts | How to prevent it |
|---|---|---|
| Bend points taken from the claim year | Client — wrong benefit entirely | Bend points lock at the year they turn **62** |
| Fewer than 35 working years not zero-filled | Client — benefit overstated | Missing years count as $0, still divided by 420 |
| Delayed credits run past age 70 | Client — plans on money that never comes | Cap at 70 |
| Gross benefit added to taxable income | Client — over-taxed | Only the taxable portion (Step 10) enters AGI |
| COLA applied before the claiming adjustment | Developer | Adjust for claiming first, then COLA |

**Detail →** [04-SOCIAL-SECURITY.md](04-SOCIAL-SECURITY.md)

---

# STEP 5 — RMD (forced withdrawals)

**What it does.** From age 73 or 75, forces a minimum amount out of pre-tax retirement accounts every year — whether the client wants it or not.

**Why it matters.** The RMD is fully taxable, it makes Social Security more taxable, and it can trigger Medicare surcharges two years later. Three effects, one trigger.

### The formula

```
rmdAge = IF birthYear >= 1960 THEN 75
         ELSE IF birthYear >= 1951 THEN 73
         ELSE 72
```

```
RMD(age) = priorYearEndBalance / applicableDenominator(age)
```

### Example 1 — born 1955, starts at 73

Balance of $2,000,000 on 31 December of the prior year:

```
$2,000,000 / 26.5 = $75,472 forced out at age 73
```

### Example 2 — born 1984, starts at 75

Nothing is forced at 73 or 74. The balance keeps compounding at 6%:

```
$2,000,000 × 1.06² = $2,247,200
$2,247,200 / 24.6  =   $91,350 forced out at age 75
```

**The difference:** two extra years of **completely empty tax brackets**. No forced income at 73 or 74 means two more years of low-cost Roth conversions — the single most valuable planning window in the whole roadmap.

### Risks and common mistakes

| What goes wrong | Who it hurts | How to prevent it |
|---|---|---|
| Everyone assumed to start at 73 | Client born 1960+ — loses two years of planning | Requires `birthYear`, not current age |
| Current balance used instead of prior 31 December | Developer — wrong every year | Use the prior year-end balance |
| RMD applied to Roth accounts | Client — needless taxable withdrawal | Roth IRA never; Roth 401(k) exempt since 2024 |
| Tax computed before adding the RMD | Client — understates tax from 73/75 onward | RMD enters income **before** the tax step |
| Pre-tax balance shown rising forever | Client — implausible projection | After ~85 the RMD % exceeds returns; balances must fall |
| First RMD deferred to 1 April without warning | Client — two RMDs in one tax year | Default to taking it in its own year |

**Detail →** [05-RMD.md](05-RMD.md)

---

# THE FOUR GATES — steps 6 to 9

**Only for clients with a K-1** (a partnership or S-corp interest) or a rental.

**What they do.** A business loss cannot simply be subtracted from income. It has to pass four tests, in order. Whatever each test blocks is **parked** — not lost — in its own bucket, waiting for a specific event to release it.

**Why it matters.** A client can have a real, economic $120,000 loss and deduct **none of it** this year. Telling them otherwise is the fastest way to lose their trust when the return is filed.

> **The rule that keeps the maths honest:** a loss blocked at one gate **never reaches the next gate** that year. Each gate only sees what the gate above it let through.

**The check that catches double-counting:**

```
allowedThisYear
  + Δ suspendedBasis
  + Δ suspendedAtRisk
  + Δ suspendedPassive
  = lossEnteringTheGates
```

---

# STEP 6 — Gate 1: Basis

**What it does.** Checks whether the client has enough investment in the business to absorb the loss.

**Why it matters.** You cannot deduct more than you put in. Basis is the client's running investment balance — and it can never go below zero.

### The formula

```
allowedGate1  = MIN(loss, basisBeforeLoss)
suspendedBasis = loss − allowedGate1
basisAfter     = basisBeforeLoss − allowedGate1
```

### Example 1 — basis is ample

```
Loss                $60,000
Basis              $200,000
                   ─────────
Deducted            $60,000      the full loss passes
Suspended                 $0
Basis after        $140,000
```

### Example 2 — basis is exhausted

```
Loss               $120,000
Basis               $80,000
                   ─────────
Deducted            $80,000      only what the basis covers
Suspended           $40,000      parked until basis is restored
Basis after              $0
```

**The difference:** **$40,000** of a genuine economic loss is not deductible this year. It is not gone — it waits for the client to put more in, or for the business to make money.

> **Partnership vs S-corp — the trap.** A partner's basis **includes their share of the partnership's debt** (§752). An S-corp shareholder gets **nothing** from company debt — only from money they personally loaned to the company. Guaranteeing a company loan creates **no** basis until they actually pay it.

### Risks and common mistakes

| What goes wrong | Who it hurts | How to prevent it |
|---|---|---|
| S-corp shareholder given basis for company debt | Client — deducts a loss the IRS will disallow | Only direct shareholder loans count |
| Basis allowed to go negative | Developer — corrupts every later year | Floor at zero; the excess is suspended |
| Reduction order wrong | Client — wrong loss allowed | Distributions → nondeductible expenses → losses |
| Suspended-basis losses assumed to survive a sale | Client — expects a deduction that never comes | They **expire** on sale of a partnership interest |

**Detail →** [11-LOSS-LIMITATIONS-AND-CARRYFORWARDS.md](11-LOSS-LIMITATIONS-AND-CARRYFORWARDS.md)

---

# STEP 7 — Gate 2: At-risk

**What it does.** Asks a harder question than basis: could the client **actually lose** this money?

**Why it matters.** Money borrowed without personal liability is not at risk. But there is a large carve-out for real estate — and whether a loan qualifies for it decides whether the loss is deductible.

### The formula

```
allowedGate2   = MIN(allowedGate1, atRiskAmount)
suspendedAtRisk = allowedGate1 − allowedGate2
atRiskAfter     = atRiskAmount − allowedGate2
```

### Example 1 — qualified nonrecourse financing

A real estate partnership with a **commercial bank mortgage** on the property:

```
Cash contributed              $50,000
Qualified nonrecourse debt   $250,000     counts, under §465(b)(6)
                             ─────────
At-risk amount               $300,000

Loss $120,000  vs  at-risk $300,000  →  fully deductible
```

### Example 2 — the same deal, seller-financed

Identical property, identical loss, but the financing came from the **seller** — a related party, so it is not *qualified* nonrecourse:

```
Cash contributed              $50,000
Seller financing              counts for $0
                             ─────────
At-risk amount                $50,000

Loss $120,000  vs  at-risk $50,000  →  deduct $50,000, suspend $70,000
```

**The difference:** **$70,000.** Same property, same money, same loss — different lender.

> **Negative at-risk is income, not a loss.** If distributions push the at-risk amount below zero, the shortfall is **added to gross income** that year under §465(e).

### Risks and common mistakes

| What goes wrong | Who it hurts | How to prevent it |
|---|---|---|
| All nonrecourse debt treated as at-risk | Client — large disallowed deduction on audit | Test the four §465(b)(6) conditions |
| At-risk assumed equal to basis | Developer — the two diverge constantly | Track them as separate running balances |
| Negative at-risk not recaptured | Client — understates income | Add the shortfall to income, deduct it next year |
| Guarantees counted as at-risk | Client | A guarantee is not at-risk until paid |

**Detail →** [11-LOSS-LIMITATIONS-AND-CARRYFORWARDS.md](11-LOSS-LIMITATIONS-AND-CARRYFORWARDS.md)

---

# STEP 8 — Gate 3: Passive activity

**What it does.** Stops losses from businesses the client doesn't actively run from offsetting their salary.

**Why it matters.** This is the gate that catches most high-income clients. A surgeon, a software executive or a law-firm partner with rental losses cannot use them against their earned income — the losses simply wait.

### The formula

```
passiveLossPool   = SUM of allowedGate2 across all PASSIVE activities
passiveIncomePool = SUM of income from all PASSIVE activities

allowedGate3    = MIN(passiveLossPool, passiveIncomePool + specialAllowance)
suspendedPassive = passiveLossPool − allowedGate3
```

```
specialAllowance = MAX(0, 25000 − 0.50 × MAX(0, MAGI − 100000))
```

### Example 1 — there is passive income to absorb it

The client also owns a profitable passive partnership:

```
Passive losses      $80,000
Passive income      $90,000
                    ────────
Deducted            $80,000      fully absorbed
Suspended                 $0
```

### Example 2 — no passive income at all

Same losses, but every passive activity lost money this year:

```
Passive losses      $80,000
Passive income            $0
$25,000 allowance         $0      MAGI is $620,000 — gone above $150,000
                    ────────
Deducted                  $0
Suspended           $80,000
```

**The difference:** **$80,000** deductible versus **nothing**. The losses are suspended, not destroyed — but they do nothing for this year's tax bill.

> **The $25,000 rental allowance is useless to this client.** It phases out completely at $150,000 of MAGI and has **never been indexed for inflation** since 1986. For the income levels this roadmap targets it is always zero — but it must still be in the model for the early or lean years.

### Risks and common mistakes

| What goes wrong | Who it hurts | How to prevent it |
|---|---|---|
| Passive losses deducted against salary | Client — the most common error in the whole system | Pool separately; only passive income absorbs them |
| $25,000 allowance given at high income | Client — overstates the deduction | Phase out 50¢ per $1 over $100,000 |
| Partial sale treated as a full disposition | Client — expects a release that doesn't happen | Only a **complete** taxable sale to an **unrelated** party releases |
| Real estate professional status applied retroactively | Client | It is not retroactive; prior suspended losses stay passive |
| Suspended losses merged into one bucket | Developer — the three have different fates | Keep basis / at-risk / passive separate |

**Detail →** [11-LOSS-LIMITATIONS-AND-CARRYFORWARDS.md](11-LOSS-LIMITATIONS-AND-CARRYFORWARDS.md)

---

# STEP 9 — Gate 4: Excess business loss

**What it does.** Caps how much business loss can offset non-business income like salary and investments.

**Why it matters.** **This cap gets tighter in 2026.** The threshold went *down*, not up — a change most software will miss.

### The formula

```
aggregateBusinessLoss = SUM of allowed business losses − SUM of business income
excessBusinessLoss    = MAX(0, aggregateBusinessLoss − threshold)

allowedThisYear = aggregateBusinessLoss − excessBusinessLoss
nolCarryforward = nolCarryforward + excessBusinessLoss
```

### Example 1 — under the cap

```
Business loss      $400,000
2026 threshold     $512,000
                   ─────────
Deducted now       $400,000      fully allowed
To NOL                    $0
```

### Example 2 — over the cap

```
Business loss      $900,000
2026 threshold     $512,000
                   ─────────
Deducted now       $512,000
To NOL             $388,000      carried forward, 80%-limited
```

**The difference:** **$388,000** deferred to future years — and once it becomes an NOL it can only offset **80%** of income in any later year.

> **The 2026 shock.** The threshold was **$626,000** in 2025 and is **$512,000** in 2026. OBBBA reset the inflation base and erased several years of drift, while making the rule **permanent**. Identical facts, **$114,000 less** deductible. Any model carrying 2025 figures forward is wrong.

### Risks and common mistakes

| What goes wrong | Who it hurts | How to prevent it |
|---|---|---|
| 2025 threshold used for 2026 | Client — $114,000 overstated deduction | $256,000 single / $512,000 MFJ |
| Rule assumed to sunset in 2028 | Both — plan built on an expiry that no longer exists | OBBBA made it permanent |
| Passive losses included in the aggregation | Developer — double-counted | Only losses that survived gates 1–3 reach here |
| Disallowed amount treated as lost | Client | It becomes an NOL, carried forward indefinitely |

**Detail →** [11-LOSS-LIMITATIONS-AND-CARRYFORWARDS.md](11-LOSS-LIMITATIONS-AND-CARRYFORWARDS.md)

---

# STEP 10 — AGI

**What it does.** Adds up everything taxable, after the gates have done their work.

**Why it matters.** AGI drives almost everything downstream — how much Social Security is taxed, whether the 3.8% surtax applies, and what the Medicare premium will be two years later.

### The formula

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

### Example 1 — a client with no K-1s

```
W-2                 $420,000
Portfolio            $20,000
                    ─────────
AGI                 $440,000
```

### Example 2 — the same client, with the K-1s from steps 6–9

```
W-2                 $420,000
S-corp K-1          $180,000
Portfolio            $20,000
Net passive                $0     ← $60,000 income fully absorbed by losses
                    ─────────
AGI                 $620,000
```

**The difference:** the $120,000 partnership loss changed AGI by **exactly zero**. It never reached the return — the gates stopped it. A model that subtracts K-1 losses directly from income would report AGI of $500,000 and understate tax by tens of thousands.

### Risks and common mistakes

| What goes wrong | Who it hurts | How to prevent it |
|---|---|---|
| Gross Social Security added instead of the taxable part | Client — heavily over-taxed | Only the Step 4/10 taxable portion enters AGI |
| K-1 losses subtracted before the gates | Client — understates tax badly | Gates first, always |
| Pre-tax contributions not subtracted | Client — overstates tax | Deduct before the tax step |
| Net passive shown as gross passive income | Developer | Net the absorbed losses first |

**Detail →** [02-TAXES.md](02-TAXES.md)

---

# STEP 11 — Regular tax

**What it does.** Taxes income in slices, each slice at its own rate.

**Why it matters.** A couple earning $587,800 does **not** pay 35% on all of it. They pay 10%, then 12%, then 22%, and so on. Confusing the marginal rate with the effective rate is the most common arithmetic error in financial projections.

### The formula

```
tax = 0
previousCap = 0
FOR each bracket (cap, rate):
    slice = MIN(taxableIncome, cap) − previousCap
    IF slice <= 0: BREAK
    tax = tax + slice × rate
    previousCap = cap
```

### Example 1 — the bracket walk, done correctly

Taxable income $587,800, married filing jointly:

| Slice | Amount | Rate | Tax |
|---|---|---|---|
| 0 → 24,800 | $24,800 | 10% | $2,480 |
| 24,800 → 100,800 | $76,000 | 12% | $9,120 |
| 100,800 → 211,400 | $110,600 | 22% | $24,332 |
| 211,400 → 403,550 | $192,150 | 24% | $46,116 |
| 403,550 → 512,450 | $108,900 | 32% | $34,848 |
| 512,450 → 587,800 | $75,350 | 35% | $26,373 |
| **Total** | | | **$143,268** |

Effective rate **24.4%**. Marginal rate **35%**.

### Example 2 — the flat-rate shortcut

Applying the marginal rate to everything:

```
$587,800 × 35% = $205,730
```

**The difference:** **$62,462** — the shortcut overstates tax by **44%**. Over 48 years that error compounds into a projection that is not merely wrong but useless.

> **Both rates matter, for different jobs.** The **marginal** rate (35%) answers "what does the next dollar cost?" — it drives every planning decision. The **effective** rate (24.4%) answers "what did we actually pay?" — it drives the cash-flow line.

### Risks and common mistakes

| What goes wrong | Who it hurts | How to prevent it |
|---|---|---|
| Marginal rate applied to all income | Client — projection is unusable | Walk the brackets slice by slice |
| Brackets held flat for 48 years | Client — overstates future tax | Index brackets forward each year |
| Capital gains taxed as a separate parallel calc | Client — understates tax | Gains **stack on top** of ordinary income |
| Effective and marginal rates used interchangeably | Advisor — wrong advice | Report both, labelled |

**Detail →** [02-TAXES.md](02-TAXES.md)

---

# STEP 12 — QBI deduction

**What it does.** Gives pass-through business owners a deduction of up to 20% of their business income.

**Why it matters.** Whether the client gets it depends on **what they do for a living**. Service businesses — health, law, accounting, consulting, financial services — lose it entirely above the income threshold. An engineer, architect, manufacturer or landlord with identical income keeps all of it.

### The formula

```
qbiDeduction = MIN(
    0.20 × combinedQBI,
    0.20 × (taxableIncomeBeforeQBI − netCapitalGain)
)
```

### Example 1 — an engineering firm (not an SSTB)

$180,000 of business income, taxable income $587,800:

```
20% × $180,000 = $36,000 deduction
Tax saved at 35% marginal = $12,600
```

### Example 2 — a consulting firm (an SSTB)

**Identical income**, but consulting is a "specified service trade or business". The 2026 phase-out ends at $553,500 for a couple, and taxable income is $587,800:

```
Above the phase-out end  →  deduction = $0
Tax saved = $0
```

**The difference:** **$36,000** of deduction and **$12,600** of tax — decided entirely by profession, not by income.

> **Engineering and architecture are excluded from the SSTB list by statute** (IRC §199A(d)(2) adopts the §1202(e)(3)(A) list *minus* those two fields). Their work depends on reputation and skill just as much as a physician's — the statute simply carves them out. Real estate, manufacturing, construction and most technology businesses are not SSTBs either.

> Treat the business type as an **explicit input**, never an inference. Two clients with identical income are $36,000 apart in deduction purely by field.

### Risks and common mistakes

| What goes wrong | Who it hurts | How to prevent it |
|---|---|---|
| SSTB phase-out ignored | Client — overstates after-tax income for decades | Flag the business type as an input; test against $403,500–$553,500 |
| 20% applied to gross business income | Client | It is limited by taxable income **minus net capital gain** |
| Negative QBI treated as zero | Client — loses a real carryforward | Negative QBI carries forward against future QBI |
| Released suspended losses not reducing QBI | Client — overstates the deduction in the release year | Losses arising 2018+ reduce QBI when released |
| Engineers or architects treated as SSTBs | Client — deduction wrongly zeroed | **Excluded by statute** — full 20% at any income |

**Detail →** [02-TAXES.md](02-TAXES.md) · [11-LOSS-LIMITATIONS-AND-CARRYFORWARDS.md](11-LOSS-LIMITATIONS-AND-CARRYFORWARDS.md)

---

# STEP 13 — NIIT (the 3.8% surtax)

**What it does.** Adds 3.8% on investment income once total income crosses a threshold.

**Why it matters.** The threshold has been **frozen since 2013** and is never adjusted for inflation. Every year, more clients cross it without earning any more in real terms.

### The formula

```
niit = 0.038 × MIN(netInvestmentIncome, MAX(0, MAGI − threshold))
```

### Example 1 — below the threshold

```
MAGI                $240,000
NII                  $20,000
Threshold (MFJ)     $250,000
                    ─────────
NIIT                      $0      MAGI is under the line
```

### Example 2 — the RMD pushes MAGI over

Same $20,000 of dividends, but the client is now taking RMDs and MAGI is $620,000:

```
NIIT = 3.8% × MIN($20,000, $620,000 − $250,000) = $760
```

**The difference:** **$760** on unchanged investment income. The RMD itself is **not** subject to NIIT — but it lifted MAGI and exposed the portfolio income that was sitting safely below the line.

> **This is the second of the RMD's three effects.** It raises income tax directly, it makes Social Security more taxable, and it drags other investment income into NIIT. All three land in the same year.

### Risks and common mistakes

| What goes wrong | Who it hurts | How to prevent it |
|---|---|---|
| Regular-tax income figures reused for NIIT | Developer — wrong base entirely | NII has its own definition; compute separately |
| RMD included in NII | Client — over-taxed | Retirement distributions are **excluded** from NII, but **included** in MAGI |
| Threshold indexed for inflation | Client — understates tax in later years | Frozen at $200,000 / $250,000 since 2013 |
| Self-rental income treated as passive | Client — over-taxed | Material participation makes it non-passive, so out of NII |

**Detail →** [02-TAXES.md](02-TAXES.md)

---

# STEP 14 — AMT (the shadow tax)

**What it does.** Runs the whole return a second time under different rules. The client pays whichever is higher.

**Why it matters.** **Two OBBBA changes bite in 2026.** The exemption starts phasing out much earlier, and it phases out twice as fast. Anyone modelling on 2025 parameters will understate AMT for high earners.

### The formula

```
exemption = MAX(0, baseExemption − 0.50 × MAX(0, AMTI − phaseoutStart))
amtBase = MAX(0, AMTI − exemption)
TMT     = 0.26 × MIN(amtBase, 244500) + 0.28 × MAX(0, amtBase − 244500)
amtDue  = MAX(0, TMT − regularTax)
```

### Example 1 — no AMT

```
AMTI              $620,000       taxable income + standard deduction back
Exemption         $140,200       full — AMTI is below the $1,000,000 phaseout
AMT base          $479,800
TMT               $129,454
Regular tax       $143,268
                  ─────────
AMT due                 $0       regular tax is higher, so AMT does nothing
```

### Example 2 — the client exercises incentive stock options

Same year, but they exercise ISOs with a **$300,000** bargain element and hold the shares past 31 December:

```
AMTI              $920,000       + the $300,000 ISO spread
Exemption         $140,200       still full — below $1,000,000
AMT base          $779,800
TMT               $213,454
Regular tax       $143,268
                  ─────────
AMT due            $70,186
```

**The difference:** **$70,186** of tax on a paper gain — no shares were sold, no cash was received. The client also gains a **$70,186 minimum tax credit** carried forward, recoverable in later years when regular tax exceeds the tentative minimum.

> **The 2026 changes.** The phaseout now begins at $500,000 / $1,000,000 (down from roughly $640,000 / $1,280,000) and the rate **doubled from 25% to 50%**. The exemption disappears far faster than it used to.

### Risks and common mistakes

| What goes wrong | Who it hurts | How to prevent it |
|---|---|---|
| 2025 AMT parameters used | Client — understates AMT badly | 2026: $90,100 / $140,200, phaseout $500k / $1M at 50% |
| ISO exercise not modelled as a preference | Client — surprise tax bill with no cash | Add the bargain element to AMTI if held past year end |
| Minimum tax credit not tracked | Client — never recovers tax already paid | Carry it forward; deferral items only |
| AMT fed back into the regular calculation | Developer — circular reference | It is a **parallel rail**; it never feeds back |

**Detail →** [02-TAXES.md](02-TAXES.md) · [11-LOSS-LIMITATIONS-AND-CARRYFORWARDS.md](11-LOSS-LIMITATIONS-AND-CARRYFORWARDS.md)

---

# STEP 15 — Cash flow

**What it does.** Works out whether the year ended with money left over or money short.

**Why it matters.** This is where the plan meets reality. A surplus funds contributions; a shortfall has to come out of accounts, and **which account** it comes from changes the tax bill.

### The formula

```
surplus = totalIncome − totalExpenses − totalTaxes
```

Withdrawal order in retirement — cheapest tax first:

```
1. RMD (forced, no choice)
2. Taxable brokerage (lowest tax cost — only the gain is taxed)
3. Pre-tax (ordinary income)
4. Roth (last — preserve tax-free growth longest)
```

### Example 1 — a working year (age 42)

```
Income             $440,000
Expenses          −$198,000
Taxes             −$119,065
                   ─────────
Surplus            $122,935      funds part of the $272,000 deployed
```

### Example 2 — a retirement year (age 70)

Social Security has started; RMDs have not:

```
Income              $49,824      Social Security only
Expenses          −$188,343
Taxes                    $0      income is below the filing threshold
                   ─────────
Shortfall         −$138,519      must come out of accounts
```

**The difference:** the client swings from putting **$122,935 in** to taking **$138,519 out** — a $261,454 turnaround in the direction of money. Every year after 62 is a drawdown year.

### Risks and common mistakes

| What goes wrong | Who it hurts | How to prevent it |
|---|---|---|
| Surplus computed before tax | Client — overstates savings every year | Tax comes out first |
| Withdrawals taken from the wrong account first | Client — pays more tax than needed | Taxable → pre-tax → Roth |
| RMD excess assumed to disappear | Developer — money vanishes from the model | Unspent RMD, after tax, moves to the taxable account |
| Shortfall allowed to exceed available balances | Both — plan fails silently | Test for depletion and flag the year |

**Detail →** [01-INCOME-AND-EXPENSES.md](01-INCOME-AND-EXPENSES.md) · [03-RETIREMENT-CONTRIBUTIONS-AND-GROWTH.md](03-RETIREMENT-CONTRIBUTIONS-AND-GROWTH.md)

---

# STEP 16 — Investment growth

**What it does.** Grows every account balance by its return, crediting contributions with roughly half a year of growth.

**Why it matters.** A tiny error in the monthly rate compounds over 48 years into hundreds of thousands of dollars of fictional wealth.

### The formula

```
endBalance = (startBalance × (1 + r))
           + (contribution × (1 + r)^0.5)
           − (withdrawal × (1 + r)^0.5)
```

```
monthlyRate = (1 + r)^(1/12) − 1
```

### Example 1 — the correct monthly rate

$1,000,000 starting, $24,500/year contributed, 7% annual return, 30 years:

```
monthlyRate = (1.07)^(1/12) − 1 = 0.5654% per month
30-year balance = $9,999,887
```

### Example 2 — the `r / 12` shortcut

```
monthlyRate = 0.07 / 12 = 0.5833% per month
30-year balance = $10,607,272
```

**The difference:** **$607,384** — a **6.1% overstatement** produced by one wrong divisor. The shortcut ignores compounding within the year, and the error grows with every year added.

> **Do not subtract inflation here.** Inflation is handled once, at Step 20. Subtracting it from the return *and* deflating the output counts it twice and can halve a 40-year result.

### Risks and common mistakes

| What goes wrong | Who it hurts | How to prevent it |
|---|---|---|
| `r / 12` used as the monthly rate | Client — 6%+ of phantom wealth | Use `(1 + r)^(1/12) − 1` |
| Inflation subtracted here *and* at Step 20 | Client — understates result severely | Deflate once, at the end |
| Contributions credited a full year of growth | Client — overstates | Mid-year convention, `(1 + r)^0.5` |
| Pre-tax, Roth and taxable pooled into one balance | Client — wrong tax on every withdrawal | Track the three separately |
| Fees not deducted from the return | Client | `netReturn = gross − advisory − fund expenses` |

**Detail →** [03-RETIREMENT-CONTRIBUTIONS-AND-GROWTH.md](03-RETIREMENT-CONTRIBUTIONS-AND-GROWTH.md)

---

# STEP 17 — Insurance cash value

**What it does.** Rolls the life policy forward — premiums in, costs out, interest credited — and tests every year that the policy is still alive.

**Why it matters.** Handled well, this is tax-free retirement income. Handled badly, it is the single worst outcome in the entire plan: a tax bill on money already spent, with nothing left to pay it.

### The formula

```
cashValue(n) = cashValue(n−1)
             + premium(n)
             − premiumLoad(n)          ← typically 5–8% of premium
             − costOfInsurance(n)      ← rises steeply with age
             − policyFees(n)           ← administrative, per-thousand charges
             + creditedInterest(n)
             − loanInterest(n)         ← if loans outstanding
```

```
IF netCashValue(n) < costOfInsurance(n) + fees(n):
    POLICY LAPSES
    taxableGain = loanBalance − basis
    FLAG this loudly — do not silently continue the projection
```

### Example 1 — the policy performs

$54,400 a year for 20 years, 7% premium load, 5.5% credited:

```
Cash value after 20 years   $1,861,081
Basis (premiums paid)       $1,088,000

Withdraw to basis tax-free, then borrow against the rest
→ tax-free retirement income, policy stays in force
```

### Example 2 — the policy is over-borrowed

The same policy, but the client borrows $120,000 a year for 12 years at 5% loan interest:

```
Loan balance                $1,910,055
Cash value                  $1,861,081     ← the loan now exceeds it

POLICY LAPSES

Taxable gain = $1,910,055 − $1,088,000 =   $822,055
Tax at 35%                             =   $287,719
```

**The difference:** a **$287,719 tax bill on money that was borrowed and spent years ago**, with no cash value left to pay it. The client receives nothing — only the bill.

> **This is why the lapse test is not optional.** A projection that borrows to hit an income target without testing solvency every year is showing a number that cannot happen.

### Risks and common mistakes

| What goes wrong | Who it hurts | How to prevent it |
|---|---|---|
| No annual lapse test | Client — catastrophic, unpayable tax bill | Test solvency every single year and flag failures |
| Over-funding past the 7-pay limit | Client — loans become taxable, permanently | Track cumulative premium against the MEC limit |
| Indexed policy modelled at a flat average return | Client — overstates badly | Apply cap, floor and participation rate each year |
| Illustrated above the AG 49-B ceiling | Client + advisor — regulatory exposure | Cap at 145% of the portfolio earning rate |
| Cost of insurance held flat | Client — hides late-year collapse risk | It rises steeply with age |
| Death benefit shown gross of the loan | Client — overstates the legacy | Net the loan off |

**Detail →** [06-INSURANCE-CASH-VALUE.md](06-INSURANCE-CASH-VALUE.md)

---

# STEP 18 — Real estate equity

**What it does.** Tracks property value up and mortgage balance down. Equity is the gap between them.

**Why it matters.** In the early years almost every mortgage payment is interest. Assuming the loan pays down evenly overstates early equity — and early equity is what the plan is counting on.

### The formula

```
payment = P × [ i × (1 + i)^N ] / [ (1 + i)^N − 1 ]
```

```
balance(m) = P × [ (1 + i)^N − (1 + i)^m ] / [ (1 + i)^N − 1 ]
```

```
equity(n) = propertyValue(n) − balance(n)
```

### Example 1 — year 1 of a $500,000 mortgage at 6.5%

```
Paid in the year    $37,924
  → principal        $5,589      15%
  → interest        $32,335      85%
```

### Example 2 — year 25 of the same mortgage

```
Paid in the year    $37,924      identical payment
  → principal       $26,484      70%
  → interest        $11,441      30%
```

**The difference:** the same $37,924 builds **4.7× more equity** in year 25 than in year 1. Assuming straight-line paydown ($500,000 ÷ 30 = $16,667/yr) would overstate year-1 equity by **$11,078** — and every early year after it.

> **Equity grows from two directions at once**: the property appreciates while the loan amortises. That is the leverage effect, and it is why real estate earns its own bucket rather than being folded into a generic growth rate.

### Risks and common mistakes

| What goes wrong | Who it hurts | How to prevent it |
|---|---|---|
| Straight-line principal paydown | Client — overstates early equity badly | Use the amortisation formula |
| Land depreciated | Client — disallowed deduction | Building value only, over 27.5 years |
| Depreciation recapture forgotten on sale | Client — surprise 25% tax | Recapture before capital gain |
| Recapture applied to property held until death | Client — overstates tax | §1014 step-up wipes it out |
| Primary residence modelled as income-producing | Client | It has negative cash flow |
| Multiple properties blended into one average | Developer | Model each separately |

### Before any of this — classify the property

Equity mechanics are the easy half. The half that decides the tax bill is **classification**, and it runs before the loss gates.

```
Q1  Is personal use excessive?          → §280A          → if yes, STOP: no loss allowed
Q2  Is the average stay ≤ 7 days?       → §1.469-1T      → if yes, NOT a rental activity
Q3  Does the owner materially participate? → §1.469-5T   → decides passive vs non-passive
```

### Example 3 — a long-term rental

$1,200,000 property, cost segregation study done, $60,000 net operating income, $263,409 depreciation → **$203,409 tax loss**. Let on 12-month leases:

```
Average stay 365 days → IS a rental activity → PASSIVE by default
Hours worked are irrelevant — a rental activity is passive no matter how hard you work it
$25,000 allowance = $0 (MAGI above $150,000)

Deductible this year        $0
Suspended                   $203,409
```

### Example 4 — the identical property, let short-term

Same building, same loss, but let on an average 5-day stay with 120 hours of self-management and no property manager working more:

```
Average stay 5 days  → NOT a rental activity (Reg. §1.469-1T(e)(3)(ii)(A))
Material participation met → Test 3: >100 hrs and nobody participates more
→ NON-PASSIVE

Deductible against W-2 now  $203,409
Tax value at 35%            $71,193
```

**The difference:** **$203,409 deductible versus nothing** — same property, same loss, decided purely by average stay length and hours.

> **Three things almost everyone gets wrong here.**
> **1.** Being non-passive does **not** exempt the loss from the §461(l) cap. Four such properties would produce $813,636 of loss, of which only **$512,000** is deductible; $301,636 becomes an NOL.
> **2.** Real estate professional status is **irrelevant** to short-term rentals — REPS is a rule about *rental activities*, and an STR under the 7-day rule is not one.
> **3.** The $25,000 allowance does not apply to STRs either, for the same reason.

> **Cost segregation is a timing strategy, not a free deduction.** It turns a $34,545 first-year write-off into $263,409 — but it lowers basis, so the 25% depreciation recapture on sale is correspondingly larger. Unless the property is held until death, when §1014 erases both.

### Risks and common mistakes — classification

| What goes wrong | Who it hurts | How to prevent it |
|---|---|---|
| Classification skipped entirely | Client — $203,409 vs $0 on the same property | Run the three questions before any other real estate step |
| Hours assumed to make a long-term rental non-passive | Client — deducts a suspended loss | A rental activity is passive regardless of hours, unless REPS |
| REPS pursued to fix a short-term rental | Client — wasted effort, no benefit | STRs are not rental activities |
| STR loss assumed exempt from the EBL cap | Client — plans on a capped deduction | Non-passive still meets gate 4 |
| §280A personal use test skipped | Client — claims a loss that is capped at rental income | Test before the gates |
| Classification treated as permanent | Both — it can flip year to year | Re-test average stay and hours annually |
| Cost seg modelled without the recapture consequence | Client — overstates lifetime benefit | Carry accumulated depreciation; 25% on sale |
| Substantial services confused with the 7-day test | Client — unexpected 15.3% SE tax | Two independent tests |

**Detail →** [07-REAL-ESTATE-EQUITY.md](07-REAL-ESTATE-EQUITY.md)

---

# STEP 19 — Estate value

**What it does.** Works out what actually reaches the heirs — after estate tax **and** after the income tax the heirs will owe.

**Why it matters.** Net worth is not legacy. Two accounts of identical size can deliver amounts that differ by more than a third.

### The formula

```
netToHeirs = grossEstate
           − debts
           − estateTax
           − heirIncomeTaxOnIRD
           + lifeInsuranceOutsideEstate
```

```
heirBasis = fairMarketValueAtDeath
```

### Example 1 — a $3,000,000 brokerage account

Cost basis $2,000,000, so $1,000,000 of unrealised gain:

```
Step-up under §1014 resets basis to market value at death
Heirs' income tax                    $0
Net to heirs                 $3,000,000
```

### Example 2 — a $3,000,000 traditional IRA

Identical value on the statement:

```
"Income in respect of a decedent" under §691 — NO step-up
Heirs' income tax at 37%     $1,110,000
Net to heirs                 $1,890,000
```

**The difference:** **$1,110,000.** The two accounts look identical on a net-worth statement and are **37% apart** in what the family actually receives.

> **And the ownership of life insurance is worth as much again.** A $5,000,000 policy owned personally adds $5,000,000 to a taxable estate — $2,000,000 of tax at 40%. The same policy in an irrevocable trust adds nothing. One titling decision.

### Risks and common mistakes

| What goes wrong | Who it hurts | How to prevent it |
|---|---|---|
| Net worth reported as the legacy figure | Client — overstates by the heirs' entire tax bill | Subtract income tax on IRD assets |
| Retirement accounts assumed to step up | Client — overstates legacy by 30–37% | IRD never steps up |
| Life insurance in the estate when it needn't be | Client — 40% of the death benefit | ILIT, with no incidents of ownership |
| 2026 exemption assumed to drop to ~$7M | Both — plan built on a repealed sunset | OBBBA made **$15,000,000** permanent |
| Portability assumed automatic | Client — loses a $15M exclusion | Requires a timely Form 706 |
| Only federal estate tax modelled | Client — surprise state bill | ~17 states have a death tax; Oregon starts at $1M |

**Detail →** [08-ESTATE-VALUE.md](08-ESTATE-VALUE.md)

---

# STEP 20 — Convert to today's dollars

**What it does.** Translates future dollars into what they will actually buy.

**Why it matters.** This is the difference between a number that impresses and a number that is true.

### The formula

```
realValue(year n) = nominalValue(year n) / (1 + inflation)^n
```

### Example 1 — the nominal headline

```
Projected legacy at age 100:   $15,400,000
```

### Example 2 — the same money, in today's purchasing power

58 years out, at 2.5% inflation:

```
$15,400,000 / 1.025^58 = $3,677,363
```

**The difference:** **$11,722,637** — **76%** of the headline figure is inflation, not wealth. Both numbers are correct. Only one of them means anything to a client deciding how to live.

> **Why the whole ledger is computed in nominal dollars first.** Tax brackets rise with inflation each year, but the Social Security taxation thresholds ($25,000 / $32,000 / $34,000 / $44,000) have been **frozen since 1983 and 1993**. Deflate before the tax step and you compare shrunken income against frozen thresholds, under-taxing every later year. Compute nominal, deflate once, at the end.

### Risks and common mistakes

| What goes wrong | Who it hurts | How to prevent it |
|---|---|---|
| Deflating before the tax step | Client — under-taxes every later year | Nominal all the way through; deflate last |
| Inflation subtracted at Step 16 *and* here | Client — halves a 40-year result | Once, and only here |
| Only nominal figures shown to the client | Client — believes they are 4× wealthier than they are | Show real dollars, offer nominal as a toggle |
| Different inflation rates in different modules | Developer — internally inconsistent | One global assumption |

**Detail →** [00-OVERVIEW-AND-YEAR-LOOP.md](00-OVERVIEW-AND-YEAR-LOOP.md)

---

# The top 10 mistakes, ranked by money at stake

Every one of these is drawn from a step above. Ranked by what they cost on the example client.

| # | Mistake | Step | What it costs | The fix |
|---|---|---|---|---|
| 1 | Net worth reported as the legacy figure | 19 | **$1,110,000** on a $3M IRA | Subtract the heirs' income tax on IRD |
| 2 | Life insurance owned personally, not in a trust | 19 | **$2,000,000** on a $5M policy | ILIT with no incidents of ownership |
| 3 | No annual lapse test on the policy | 17 | **$287,719** unpayable tax bill | Test solvency every year |
| 4 | `r / 12` used as the monthly growth rate | 16 | **$607,384** of phantom wealth over 30 yrs | `(1 + r)^(1/12) − 1` |
| 5 | Marginal rate applied to all income | 11 | **$62,462** overstated in one year | Walk the brackets |
| 6 | SSTB phase-out ignored for QBI | 12 | **$36,000** of deduction that doesn't exist | Test profession against the threshold |
| 7 | 2025 EBL threshold used in 2026 | 9 | **$114,000** of overstated deduction | $256,000 / $512,000 |
| 8 | Passive losses deducted against salary | 8 | **$80,000** disallowed on audit | Only passive income absorbs them |
| 9 | Age 60–63 catch-up stacked, not substituted | 3 | **$8,000/yr** the client cannot contribute | `ELSE IF`, never `+` |
| 10 | Claiming Social Security at 62 without modelling it | 4 | **$359,171** over 28 years | Apply the claiming adjustment |

> **Runner-up, and rising fast:** skipping real estate classification (Step 18). The same property with the same loss is worth **$203,409** of current deduction or **$0**, decided only by average stay length and hours worked. For a client with several properties this outranks most of the list above.

---

# Risk register

| Risk | Likelihood | Impact | How it shows up | Mitigation |
|---|---|---|---|---|
| **Ordering error in the year loop** | Medium | **Severe** | Tax understated from age 73 onward | Enforce the Step 1→20 sequence; assert no step reads a value produced later |
| **Loss double-counted across gates** | Medium | **Severe** | Suspended losses exceed the original loss | Conservation identity checked every activity, every year |
| **Stale tax constants** | **High** | **Severe** | Silently wrong from 1 January each year | Annual refresh (Oct–Nov); see the maintenance calendar in module 10 |
| **Insurance policy lapse not modelled** | Medium | **Severe** | Plan shows tax-free income that ends in a tax bill | Mandatory annual lapse test with a hard flag |
| **Inflation counted twice** | Medium | High | 40-year results roughly halved | Deflate once, at Step 20, and nowhere else |
| **Client has K-1s but gates not implemented** | **High** | High | Losses deducted that the IRS will disallow | Detect K-1 presence and route through steps 6–9 |
| **Frozen thresholds indexed by mistake** | Medium | High | Tax understated in later years | NIIT, SS taxation and the $25,000 allowance never move |
| **Single deterministic path presented as certainty** | **High** | Medium | Client treats one line as a promise | Present scenario ranges; the model has no Monte Carlo yet |
| **State tax layer oversimplified** | **High** | Medium | Wrong for CA, NY, OR clients | Flat-rate placeholder is a known gap |
| **Senior bonus deduction left on after 2028** | Medium | Medium | After-tax income overstated for decades | Switch it off in 2029 |
| **Mockup figures shown as engine output** | Medium | Medium | Numbers cannot be reproduced on request | Generate every milestone from the engine — see module 09 |

## The three things that would most improve confidence

1. **Monte Carlo.** Every serious competitor has it. A single deterministic line invites the client to read a projection as a promise.
2. **Real state tax brackets.** A flat percentage is wrong for the graduated states where most of these clients live.
3. **Real policy mechanics.** Insurance is currently modelled at a flat credited rate; module 06 specifies the cost-of-insurance, cap/floor and lapse behaviour that should replace it.

---

# Glossary — for the client

| Term | What it actually means |
|---|---|
| **AGI** | Your total income for tax purposes, after a few specific deductions |
| **Taxable income** | AGI minus your standard or itemised deduction — the number the brackets apply to |
| **Marginal rate** | What the *next* dollar you earn costs you in tax |
| **Effective rate** | What you actually paid, as a percentage of income — always lower than the marginal rate |
| **Basis** | How much of your own money is invested in something. You cannot deduct more than this |
| **At-risk** | How much you could genuinely lose. Borrowed money you aren't personally liable for doesn't count |
| **Passive** | A business you don't actively run. Its losses can't offset your salary |
| **Suspended loss** | A real loss you couldn't deduct this year. It waits — it isn't lost |
| **RMD** | The minimum the government forces out of your retirement account each year from 73 or 75 |
| **Provisional income** | A special income measure that decides how much of your Social Security is taxed |
| **QBI** | A deduction of up to 20% of business income — but service businesses (health, law, accounting, consulting, finance) lose it above the income threshold. Engineers, architects, landlords and product businesses keep it |
| **NIIT** | An extra 3.8% tax on investment income above $250,000 (married) |
| **AMT** | A second tax calculation with different rules. You pay whichever is higher |
| **AMTI** | Your income as the AMT rules measure it — usually higher than normal taxable income |
| **MEC** | A life policy funded too fast. Loans from it become taxable, permanently |
| **IRD** | Income you earned but never paid tax on. Your heirs pay it — retirement accounts are the main example |
| **Step-up** | Most assets reset to market value at death, erasing the capital gains tax. Retirement accounts do **not** |
| **ILIT** | A trust that owns your life insurance so the death benefit escapes estate tax |
| **Nominal / Real** | Nominal = future dollars. Real = what they will actually buy in today's money |

---

# Cross-reference — where the full detail lives

| Steps | Detail module |
|---|---|
| The year loop and ordering | [00-OVERVIEW-AND-YEAR-LOOP.md](00-OVERVIEW-AND-YEAR-LOOP.md) |
| 1, 2, 15 | [01-INCOME-AND-EXPENSES.md](01-INCOME-AND-EXPENSES.md) |
| 10, 11, 12, 13, 14 | [02-TAXES.md](02-TAXES.md) |
| 3, 16 | [03-RETIREMENT-CONTRIBUTIONS-AND-GROWTH.md](03-RETIREMENT-CONTRIBUTIONS-AND-GROWTH.md) |
| 4 | [04-SOCIAL-SECURITY.md](04-SOCIAL-SECURITY.md) |
| 5 | [05-RMD.md](05-RMD.md) |
| 17 | [06-INSURANCE-CASH-VALUE.md](06-INSURANCE-CASH-VALUE.md) |
| 18 | [07-REAL-ESTATE-EQUITY.md](07-REAL-ESTATE-EQUITY.md) |
| 19 | [08-ESTATE-VALUE.md](08-ESTATE-VALUE.md) |
| Full 48-year worked table | [09-WORKED-EXAMPLE.md](09-WORKED-EXAMPLE.md) |
| Every source + test vectors | [10-SOURCES-AND-COMPETITORS.md](10-SOURCES-AND-COMPETITORS.md) |
| 6, 7, 8, 9 and all carryforwards | [11-LOSS-LIMITATIONS-AND-CARRYFORWARDS.md](11-LOSS-LIMITATIONS-AND-CARRYFORWARDS.md) |
| The build reference, formula by formula | [MASTER-GUIDE.md](MASTER-GUIDE.md) |

---

# Where every number in this document comes from

All figures are **tax year 2026**, taken from the primary US government source.

| Constant | Value | Source |
|---|---|---|
| Tax brackets, standard deduction | see Step 11 | [IRS Rev. Proc. 2025-32](https://www.irs.gov/newsroom/irs-releases-tax-inflation-adjustments-for-tax-year-2026-including-amendments-from-the-one-big-beautiful-bill) |
| 401(k) limits and catch-ups | $24,500 / $32,500 / $35,750 | [IRS Notice 2025-67](https://www.irs.gov/newsroom/401k-limit-increases-to-24500-for-2026-ira-limit-increases-to-7500) |
| Social Security bend points, COLA | $1,286 / $7,749 · 2.8% | [Federal Register 2025-19763](https://www.federalregister.gov/documents/2025/11/03/2025-19763/cost-of-living-increase-and-other-determinations-for-2026) |
| RMD divisors | 26.5 at 73 · 24.6 at 75 | [IRS Publication 590-B](https://www.irs.gov/pub/irs-pdf/p590b.pdf) |
| Medicare premiums, IRMAA | $202.90/mo standard | [CMS 2026 fact sheet](https://www.cms.gov/newsroom/fact-sheets/2026-medicare-parts-b-premiums-deductibles) |
| Excess business loss threshold | $256,000 / $512,000 | IRS Rev. Proc. 2025-32 · IRC §461(l) |
| AMT exemption and phaseout | $90,100 / $140,200 · 50% | IRS Rev. Proc. 2025-32 · OBBBA §70107 |
| Estate exclusion | $15,000,000 · 40% | IRS Rev. Proc. 2025-32 · OBBBA |

Full citations, the exact Google phrase for each, and hand-checkable test vectors are in [10-SOURCES-AND-COMPETITORS.md](10-SOURCES-AND-COMPETITORS.md).

> **Every example figure in this handbook was computed, not written by hand.** The 2026 constants change each autumn — see the maintenance calendar in module 10 before relying on this document in a later year.
