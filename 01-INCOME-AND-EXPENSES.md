# 01 — Annual Income and Expenses

**Steps 1–2 of the year loop** · Rail: **nominal**

---

## PART A — INCOME

### What this computes

Gross income for each year, by source, from the current age through age 90.

### Inputs

| Input | Type | Source |
|---|---|---|
| `w2Income` | $ | Client W-2 / payroll |
| `k1Income` | $ | K-1 from S-corp or partnership |
| `scheduleCProfit` | $ | Sole proprietor net profit |
| `rentalIncome` | $ | Schedule E |
| `portfolioIncome` | $ | Interest, dividends, realized gains |
| `incomeGrowth` | rate | Assumption, typically 0.03 |
| `retirementAge` | int | Client target |

### Formula — accumulation phase (age < retirement age)

Each income source grows independently:

```
income(n) = income(0) × (1 + growthRate)^n
```

Total earned income for year n:

```
earnedIncome(n) = w2(n) + k1(n) + scheduleC(n)
totalIncome(n)  = earnedIncome(n) + rental(n) + portfolio(n)
```

**Worked number** — W-2 of $250,000 growing at 3%:

| Year | Age | Calculation | Income |
|---|---|---|---|
| 0 | 42 | 250,000 × 1.03⁰ | $250,000 |
| 1 | 43 | 250,000 × 1.03¹ | $257,500 |
| 5 | 47 | 250,000 × 1.03⁵ | $289,819 |
| 20 | 62 | 250,000 × 1.03²⁰ | $451,528 |

### Formula — retirement phase (age ≥ retirement age)

Earned income stops. Income now comes from four places:

```
totalIncome(n) = socialSecurity(n)        ← module 04
               + rmd(n)                    ← module 05
               + portfolioWithdrawal(n)     ← below
               + rental(n)                  ← module 07
```

### Portfolio withdrawal — the replacement-ratio method

The client needs a target income in retirement. Two ways to set it:

**Option 1 — replacement ratio (use when the client gives no number):**

```
targetRetirementIncome = finalWorkingIncome × replacementRatio
```

Standard replacement ratio is **70–80%**. Use **0.75** as the default. The reasoning: payroll tax stops, retirement contributions stop, and commuting/work costs stop, so the client needs less gross income to fund the same lifestyle.

**Option 2 — explicit (use when the client states a figure):**

```
targetRetirementIncome = clientStatedAmount, inflated to year n
                       = statedAmount × (1 + inflation)^n
```

Then the portfolio must supply whatever the guaranteed sources don't:

```
portfolioWithdrawal(n) = MAX(0,
      targetRetirementIncome(n)
    − socialSecurity(n)
    − rmd(n)
    − rental(n)
)
```

> **Note the `MAX(0, …)`.** If Social Security plus the RMD already exceed the target, the withdrawal is zero — but the RMD is still forced out (see module 05). The excess goes to taxable savings, it does not vanish.

---

## PART B — EXPENSES

### What this computes

Annual lifestyle spending, inflated forward.

### Inputs

| Input | Type | Source |
|---|---|---|
| `monthlyLifestyleExpenses` | $ | Client questionnaire |
| `monthlyMedicalInsurance` | $ | Client questionnaire |
| `inflation` | rate | Assumption, typically 0.025 |
| `healthcareInflation` | rate | Assumption, typically 0.05 |

### Formula

```
baseExpenses(0)  = (monthlyLifestyleExpenses × 12)
generalExpense(n) = baseExpenses(0) × (1 + inflation)^n
```

**Healthcare inflates faster than everything else** and must be tracked separately:

```
healthcare(0)  = monthlyMedicalInsurance × 12
healthcare(n)  = healthcare(0) × (1 + healthcareInflation)^n
```

```
totalExpenses(n) = generalExpense(n) + healthcare(n) + medicare(n)
```

Where `medicare(n)` is zero before age 65 and comes from module 02 (IRMAA) from age 65 on.

**Worked number** — $8,000/month lifestyle + $1,200/month medical, 2.5% and 5%:

| Year | Age | General | Healthcare | Total |
|---|---|---|---|---|
| 0 | 42 | $96,000 | $14,400 | $110,400 |
| 10 | 52 | $122,888 | $23,456 | $146,344 |
| 20 | 62 | $157,307 | $38,207 | $195,515 |
| 30 | 72 | $201,366 | $62,236 | $263,602 |

Notice healthcare goes from 13% of the budget to 24%. A model that inflates everything at one rate misses this entirely.

### The retirement expense adjustment

Expenses do **not** simply continue at the working-life level. Apply a step-down at retirement:

```
IF age ≥ retirementAge:
    generalExpense(n) = generalExpense(n) × retirementExpenseFactor
```

Default `retirementExpenseFactor = 0.85`. Work-related costs disappear; healthcare is already tracked separately and does not get this haircut.

### The "retirement smile" (optional refinement)

Real retiree spending is not flat. It follows a U-shape:

| Ages | Pattern | Factor |
|---|---|---|
| Retirement → +10 yrs | "Go-go" — travel, active | 1.00 |
| +10 → +20 yrs | "Slow-go" — activity declines | 0.85 |
| +20 yrs → death | "No-go" — but medical rises | 0.75 general, healthcare unchanged |

Implement this only if the client wants that fidelity. The flat 0.85 factor is defensible on its own.

---

## Ordering traps

| ❌ Don't | ✅ Do |
|---|---|
| Inflate healthcare at the general CPI rate | Track healthcare separately at ~5% |
| Continue earned income past retirement age | Zero it out and switch to the withdrawal formula |
| Let `portfolioWithdrawal` go negative | Floor it at zero with `MAX(0, …)` |
| Apply the retirement expense factor to healthcare | Apply it to general expenses only |
| Deflate expenses here | Deflate once, at Step 13 |

---

## Sources

| What | Source | Google this |
|---|---|---|
| Replacement ratio 70–80% | [Social Security Administration — replacement rates](https://www.ssa.gov/policy/docs/ssb/v70n1/v70n1p1.html) | `SSA replacement rate retirement income policy` |
| Healthcare cost inflation exceeds CPI | [CMS National Health Expenditure Projections](https://www.cms.gov/data-research/statistics-trends-and-reports/national-health-expenditure-data/projected) | `CMS National Health Expenditure Projections` |
| Retirement spending smile | [BLS Consumer Expenditure Survey, by age](https://www.bls.gov/cex/tables.htm) | `BLS Consumer Expenditure Survey age of reference person` |
