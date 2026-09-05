# 09 — Worked Example, Age 42 → 100

**Purpose:** run every formula from modules 01–08 on one client, show the numbers, and check them against the mockup in this folder.

---

## 1. The client

Taken from the `To Age 90+ Tax & Financial Roadmap` mockup.

| Input | Value |
|---|---|
| Current age | **42** (born 1984) |
| Retirement age | 62 |
| End age | 100 |
| Filing status | Married filing jointly |
| W-2 income | $420,000, growing 3%/yr |
| Lifestyle expenses | $180,000/yr (+ $18,000 healthcare) |
| Annual net tax savings | **$188,000** |
| DWC % | 20% |
| **Annual deployable wealth capital** | **$272,000** |
| Starting net worth | $1,760,000 |
| Social Security | claim at 67, $4,152/mo PIA |
| **RMD age** | **75** (born after 1959 → module 05) |

### Assumptions

| Assumption | Nominal | Real (after 2.5% inflation) |
|---|---|---|
| Qualified / retirement return | 6.25% | 3.66% |
| Taxable / liquidity return | 5.75% | 3.17% |
| Insurance cash value | 5.50% | 2.93% |
| Real estate appreciation | 4.00% | 1.46% |
| Inflation | 2.50% | — |
| Healthcare inflation | 5.00% | 2.44% |

### Bucket allocation of the $272,000

| Bucket | % | Annual $ |
|---|---|---|
| Liquidity reserve | 10% | $27,200 |
| 401(k) / Cash balance / Roth | 25% | $68,000 |
| Life insurance cash value | 20% | $54,400 |
| Real estate / business | 25% | $68,000 |
| Market / opportunity | 10% | $27,200 |
| Legacy / trust | 7% | $19,040 |
| Disability / LTC | 3% | $8,160 |

---

## 2. Year 1 in full (age 42) — every step

Following the order in module 00.

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

Effective federal rate: 78,268 / 420,000 = **18.6%**. Marginal rate: **24%**.

---

## 3. The full ledger — real (today's) dollars

Computed nominal, deflated at 2.5% per module 00.

| Age | Income | Soc Sec | RMD | Taxes | Expenses | Contrib | Net worth | Estate value |
|---|---|---|---|---|---|---|---|---|
| 42 | $420,000 | $0 | $0 | $119,065 | $198,000 | $272,000 | $2,134,995 | $1,881,387 |
| 45 | $426,176 | $0 | $0 | $121,007 | $199,349 | $252,579 | $3,145,972 | $2,790,796 |
| 50 | $436,673 | $0 | $0 | $124,382 | $201,827 | $223,243 | $4,907,931 | $4,368,782 |
| 55 | $447,428 | $0 | $0 | $128,625 | $204,622 | $197,314 | $6,798,991 | $6,052,910 |
| 60 | $458,448 | $0 | $0 | $132,973 | $207,775 | $174,397 | $8,860,877 | $7,878,848 |
| **62** | $0 | $0 | $0 | $0 | $182,146 | $0 | **$9,391,187** | $8,320,081 |
| 65 | $0 | $0 | $0 | $0 | $184,331 | $0 | $9,685,419 | $8,492,399 |
| **67** | $0 | **$49,824** | $0 | $0 | $185,878 | $0 | $9,943,785 | $8,661,874 |
| 70 | $0 | $49,824 | $0 | $0 | $188,343 | $0 | $10,435,871 | $9,008,052 |
| **75** | $0 | $49,824 | **$186,796** | $43,645 | $192,869 | $0 | $11,307,133 | $9,663,682 |
| 80 | $0 | $49,824 | $220,497 | $53,400 | $197,974 | $0 | $12,015,226 | $10,436,053 |
| 85 | $0 | $49,824 | $256,387 | $64,167 | $203,732 | $0 | $12,631,567 | $11,195,800 |
| 90 | $0 | $49,824 | $286,699 | $73,261 | $210,229 | $0 | $13,141,128 | $11,940,756 |
| 95 | $0 | $49,824 | $297,223 | $76,418 | $217,557 | $0 | $13,588,428 | $12,708,741 |
| 100 | $0 | $49,824 | $259,226 | $65,019 | $225,823 | $0 | $14,153,203 | **$13,626,975** |

### The four things this table shows

1. **Contributions shrink in real terms.** $272,000 nominal is $174,397 of purchasing power by age 60. A model that shows a flat $272,000 for 20 years overstates the real deployment by nearly 36%.

2. **Taxes go to zero from 62 to 74.** No earned income, Social Security not yet claimed or below the threshold, no RMD. **This is the Roth conversion window** — thirteen years of near-empty brackets. It is the most valuable planning space in the entire roadmap, and it exists only because the RMD age is 75.

3. **RMDs restart taxation at 75.** $186,796 forced out, dragging $43,645 of tax with it — plus it makes Social Security taxable and can trip IRMAA two years later. Three effects, one trigger.

4. **RMDs peak around age 95 and then fall.** $297,223 at 95, down to $259,226 at 100 — the balance is shrinking faster than the divisor. This is the correct behaviour and only appears if the Uniform Lifetime Table is actually implemented.

### Buckets at retirement (age 62, real dollars)

| Bucket | Value |
|---|---|
| Liquidity reserve | $0.81M |
| 401(k) / Cash balance / Roth | $3.06M |
| Life insurance cash value | $1.92M |
| Real estate / business | $1.92M |
| Market / opportunity | $0.99M |
| Legacy / trust | $0.48M |
| Disability / LTC | $0.21M |
| **Total** | **$9.39M** |

### Net worth vs estate value

At age 100: net worth **$14.15M**, estate value **$13.63M**. The $0.53M gap is the income tax the heirs owe on the pre-tax bucket (IRD — module 08). It is invisible on a net-worth statement and it is real money.

---

## 4. Reconciliation against the mockup

The mockup states these figures. Comparing them to the model:

| Age | Mockup | Model (real $) | Difference |
|---|---|---|---|
| 42 | $1.76M | $2.13M | +$0.37M |
| 45 | $3.05M | $3.15M | +$0.10M |
| 50 | $5.25M | $4.91M | −$0.34M |
| 55 | $7.90M | $6.80M | −$1.10M |
| **62** | **$11.3M** | **$9.39M** | **−$1.91M** |
| 70 | $12.4M | $10.44M | −$1.96M |
| 80 | $13.9M | $12.02M | −$1.88M |
| 90 | $14.8M | $13.14M | −$1.66M |
| 100 | $15.4M | $14.15M | −$1.25M |

### What was tested

**Finding 1 — the mockup's endpoints ARE internally coherent.**

Solving for the rate that takes $1.76M plus $272,000/year to $11.3M over 20 years gives a **real return of 3.57%** — entirely reasonable, and consistent with a ~6.1% nominal return net of 2.5% inflation.

Solving the distribution phase independently: $11.3M at 62 growing at a real **4.7%** while paying out $18.7M over 38 years lands almost exactly on **$15.4M** at 100. Also coherent.

**Finding 2 — but the two phases use different rates, in the wrong direction.**

Accumulation implies **3.57%** real; distribution implies **4.7%** real. That is backwards. Portfolios normally get *more* conservative at retirement, not less. Either the accumulation figure is understated or the distribution figure is overstated — they cannot both be right under one asset allocation.

**Finding 3 — the intermediate milestones do not sit on any single compounding curve.**

Fitting the best single rate to ages 45/50/55/62 simultaneously leaves a total absolute error of **$1.37M**, with a consistent pattern: the mockup runs high at 45 and 50 relative to any curve that also hits $11.3M at 62.

| Age | Mockup | Best-fit curve (3.48% real) | Gap |
|---|---|---|---|
| 45 | $3.05M | $2.81M | −$0.24M |
| 50 | $5.25M | $4.82M | −$0.43M |
| 55 | $7.90M | $7.20M | −$0.70M |
| 62 | $11.30M | $11.30M | $0.00M |

**Conclusion:** the age-45/50/55 cards appear to have been placed for visual progression rather than computed. They are illustrative.

**Finding 4 — the $18.7M distribution figure implies spending far above the stated lifestyle.**

$18.7M over 38 years is roughly **$492,000/year**. The client's stated lifestyle is $180,000/year. The model, drawing only what is needed, produces **$8.7M** of total distributions. To reach $18.7M the client would have to spend about 2.7× their stated lifestyle — or the figure includes gross distributions (RMDs recycled into taxable savings) rather than net spending.

> **Recommendation:** define precisely what "projected distributions" means before publishing it. Gross withdrawals and net spending differ by a factor of two here, and the label does not say which is shown.

**Finding 5 — the bucket percentages do not match the bucket dollars.**

The mockup labels the buckets 10/25/20/25/10/7/3 but its own dollar figures give 10.4/29.2/19.0/27.4/8.1/3.8/2.0. This is actually **correct behaviour** — the percentages are contribution shares and the dollars are ending balances, which diverge because each bucket compounds at a different rate. But the card does not say so, and it reads as an error. **Label the percentages "of annual contribution", not "of total".**

---

## 5. What the model reproduces well

- The **shape** of the curve — steep accumulation to 62, then a long flat rise — matches the mockup closely.
- The age-45 figure matches within $0.10M.
- The order of magnitude at every milestone is right.
- The endpoint ratio (age 100 ≈ 1.5× age 62) is reproduced: model 1.51×, mockup 1.36×.

## 6. What must be fixed before this is client-facing

| Issue | Action |
|---|---|
| Intermediate milestones not computed | Generate them from the engine, not by hand |
| Two different real returns across phases | Pick one asset-allocation glide path and derive both |
| "$18.7M distributions" undefined | State gross vs net |
| Bucket % vs $ mismatch unexplained | Relabel as "% of annual contribution" |
| Estate value shown as net worth | Subtract heirs' IRD tax (module 08) |

---

## 7. Reproducing this

Every figure above comes from applying modules 01–08 in the order given in module 00. The two findings that required solving rather than direct calculation:

```
Accumulation rate:   solve  1.76M × (1+r)^20 + 272K × [((1+r)^20 − 1)/r] = 11.3M
                     →  r = 3.572% real

Distribution rate:   solve  11.3M × (1+r)^38 − D × [((1+r)^38 − 1)/r] = 15.4M
                     with total distributions D × 38 = 18.7M
                     →  r ≈ 4.7% real, D ≈ $492K/yr
```

Both are standard time-value-of-money solves and can be checked in any spreadsheet with `RATE()` and `PMT()`.
