# 03 — Retirement Contributions and Investment Growth

**Steps 3 and 9 of the year loop** · Rail: **nominal**

---

## PART A — CONTRIBUTIONS

### What this computes

How much goes into retirement accounts each year, capped by IRS limits that change with age.

### 2026 contribution limits

Source: **IRS Notice 2025-67 (IR-2025-111)**.

| Plan | Base limit | Age 50+ catch-up | Age 60–63 catch-up |
|---|---|---|---|
| 401(k) / 403(b) / 457 / TSP | **$24,500** | +$8,000 | +$11,250 |
| IRA (traditional or Roth) | **$7,500** | +$1,100 | +$1,100 |
| SIMPLE | $17,000 ($18,100 applicable) | +$4,000 ($3,850) | +$5,250 |

### The rule everyone gets wrong

> **The age 60–63 "super catch-up" REPLACES the age-50 catch-up. It does not add to it.**

| Age | Maximum 401(k) deferral | Working |
|---|---|---|
| 49 and under | **$24,500** | base only |
| 50–59 | **$32,500** | 24,500 + 8,000 |
| **60, 61, 62, 63** | **$35,750** | 24,500 + 11,250 ← *not* 24,500 + 8,000 + 11,250 |
| 64+ | **$32,500** | back to 24,500 + 8,000 |

Note the **drop at age 64**. The super catch-up applies only in those four years. A model that keeps it running to retirement overstates contributions.

### Formula

```
catchUp =
    IF age >= 60 AND age <= 63:  11250
    ELSE IF age >= 50:            8000
    ELSE:                            0

limit401k = 24500 + catchUp
contribution401k = MIN(desiredContribution, limit401k, earnedIncome)
```

The `earnedIncome` cap matters: you cannot defer more than you earned.

### Mandatory Roth catch-up — new for 2026

SECURE 2.0 §603, effective 2026:

> If the participant's **prior-year wages from that plan sponsor exceeded $150,000**, the catch-up contribution **must** be made as Roth (after-tax).

```
IF priorYearWages > 150000:
    catchUpIsRoth = TRUE     → does NOT reduce taxable income
ELSE:
    catchUpIsRoth = FALSE    → reduces taxable income
```

**Tax impact:** for a high earner aged 50+, $8,000–$11,250 of the contribution stops being deductible. The model must move that amount out of the pre-tax deduction and into the Roth bucket, or it will overstate the tax saving every year from age 50 on.

### Employer contributions and the §415(c) cap

```
totalAnnualAdditions = employeeDeferral + employerMatch + profitSharing
```

This total is capped by IRC §415(c) at the lesser of 100% of compensation or the annual dollar limit (approximately $72,000 for 2026, plus catch-up). Catch-up contributions sit **outside** the §415(c) cap.

### Roth IRA eligibility phase-out — 2026

| Filing status | Phase-out range |
|---|---|
| Single / HoH | $153,000 – $168,000 |
| Married filing jointly | $242,000 – $252,000 |

```
IF MAGI >= phaseOutEnd:      rothIRALimit = 0
ELSE IF MAGI > phaseOutStart:
    reduction = (MAGI − phaseOutStart) / (phaseOutEnd − phaseOutStart)
    rothIRALimit = baseLimit × (1 − reduction)
ELSE:                        rothIRALimit = baseLimit
```

> Any client above the phase-out — which at $242,000–$252,000 MFJ includes most two-earner professional households — cannot contribute directly to a Roth IRA. Model the backdoor Roth (non-deductible traditional IRA then conversion) only if the client actually does it — and remember the **pro-rata rule** applies across all traditional IRA balances.

### Do the limits grow over time?

Yes. They are indexed to inflation and rounded to the nearest $500 (401k) or $500 (IRA). For a projection:

```
limit(n) = ROUND_DOWN_TO_500( limit(2026) × (1 + inflation)^n )
```

This is an approximation — actual indexing uses a specific CPI measure with a lag — but it is the correct modelling behaviour. Holding limits flat for 48 years understates contributions badly.

---

## PART B — INVESTMENT GROWTH

### What this computes

How balances grow each year.

### Formula — annual compounding with mid-year contributions

```
endBalance = (startBalance × (1 + r))
           + (contribution × (1 + r)^0.5)
           − (withdrawal × (1 + r)^0.5)
```

The `^0.5` exponent treats contributions and withdrawals as occurring **mid-year on average**, which is what actually happens with monthly payroll deferrals. It is more accurate than assuming everything lands on January 1 (overstates) or December 31 (understates).

**Simpler alternative** if monthly precision is wanted:

```
monthlyRate = (1 + r)^(1/12) − 1
FOR each month:
    balance = balance × (1 + monthlyRate) + monthlyContribution
```

> Use `(1 + r)^(1/12) − 1`, **not** `r / 12`. The second is the nominal-rate shortcut and produces a slightly higher result — about 0.2% per year at 7%, which compounds to a visible gap over 48 years.

### Net return after costs

```
netReturn = grossReturn − advisoryFee − fundExpenseRatio
```

Typical: 7.0% gross − 1.0% advisory − 0.15% fund = **5.85% net**.

> **Do not also subtract inflation here.** Inflation is handled once, by the deflator in module 00. Subtracting it twice is the most common double-count in projection engines and can understate a 40-year result by 50% or more.

### Three account types, tracked separately

They must be separate because they are taxed differently at withdrawal and only one is subject to RMDs.

| Bucket | Growth | Taxed on withdrawal | RMD? |
|---|---|---|---|
| **Pre-tax** (401k, traditional IRA, SEP) | Tax-deferred | Ordinary income, 100% | **Yes** |
| **Roth** (Roth 401k, Roth IRA) | Tax-free | Not taxed if qualified | **No** (Roth IRA never; Roth 401k not since 2024) |
| **Taxable** (brokerage) | Taxed annually on dividends | Capital gains on basis only | No |

```
pretaxBalance(n)  = pretaxBalance(n−1)  × (1+r) + pretaxContrib(n)  − rmd(n) − withdrawals
rothBalance(n)    = rothBalance(n−1)    × (1+r) + rothContrib(n)    − withdrawals
taxableBalance(n) = taxableBalance(n−1) × (1+r) + surplus(n)        − withdrawals
```

**Withdrawal order in retirement** (standard tax-efficient sequence):
1. RMD (forced, no choice)
2. Taxable brokerage (lowest tax cost — only the gain is taxed)
3. Pre-tax (ordinary income)
4. Roth (last — preserve tax-free growth longest)

### Worked number

$500,000 pre-tax balance, $24,500/yr contribution, 6% net return:

| Year | Age | Start balance | Contribution | Growth | End balance |
|---|---|---|---|---|---|
| 1 | 43 | $500,000 | $24,500 | $30,724 | $555,224 |
| 5 | 47 | — | $24,500 | — | $811,304 |
| 10 | 52 | — | $24,500 | — | $1,227,900 |
| 20 | 62 | — | $24,500 | — | $2,531,458 |

(Contributions applied mid-year at `(1 + r)^0.5`, per the formula above.)

---

## Ordering traps

| Don't | Do |
|---|---|
| Add the 60–63 catch-up **on top of** the 50+ catch-up | Replace it — $35,750, not $43,750 |
| Keep the super catch-up past age 63 | Drop back to $32,500 at 64 |
| Deduct the Roth-mandated catch-up from taxable income | Treat it as after-tax from 2026 when wages > $150,000 |
| Use `r / 12` for monthly compounding | Use `(1 + r)^(1/12) − 1` |
| Subtract inflation from the return AND deflate the output | Subtract it once, in the deflator |
| Hold contribution limits flat for 48 years | Index them forward |
| Pool all accounts into one balance | Track pre-tax / Roth / taxable separately |

---

## Sources

| What | Source | Google this |
|---|---|---|
| 2026 limits, super catch-up, Roth catch-up rule | [IRS Notice 2025-67 / IR-2025-111](https://www.irs.gov/newsroom/401k-limit-increases-to-24500-for-2026-ira-limit-increases-to-7500) | `IRS 401k limit increases to 24500 for 2026` |
| Catch-up mechanics | [IRS — Retirement topics: catch-up contributions](https://www.irs.gov/retirement-plans/plan-participant-employee/retirement-topics-catch-up-contributions) | `IRS retirement topics catch-up contributions` |
| SECURE 2.0 §603 mandatory Roth catch-up | [Quarles — Roth Catch-Up Contributions in 2026](https://www.quarles.com/newsroom/publications/secure-2-0-act-retirement-plan-update-roth-catch-up-contributions-in-2026) | `SECURE 2.0 Roth catch-up contributions 2026 $145,000 $150,000` |
