# 06 — Life Insurance Cash Value

**Step 10 of the year loop** · Rail: **nominal**

---

## What this computes

The cash value inside a permanent life insurance policy (whole life, IUL, or VUL), the tax-free income it can produce through policy loans, and the death benefit that lands in the estate.

This is the bucket the mockup labels **"Life Insurance Cash Value — Income + legacy protection"** at 20% of deployable capital.

---

## 1. Why this bucket exists at all

Three tax properties, and each depends on a specific Code section holding:

| Property | Authority | Condition |
|---|---|---|
| Cash value grows tax-deferred | IRC §7702 | Policy must **qualify as life insurance** |
| Loans come out income-tax-free | IRC §72(e) + §7702 | Policy must **not be a MEC** and must **stay in force** |
| Death benefit is income-tax-free | IRC §101(a) | Nearly always |

> **If any condition fails, the tax treatment collapses.** These are not soft assumptions — they are binary tests with defined statutory formulas. A projection that shows tax-free income without modelling the tests is showing a number that may not exist.

---

## 2. Test 1 — Does it qualify as life insurance? (IRC §7702)

A contract must pass **one** of two tests. The insurer chooses which at issue.

### Cash Value Accumulation Test (CVAT)
Cash surrender value may never exceed the net single premium required to fund the future benefits.

```
cashValue <= netSinglePremium(deathBenefit, age, statutoryInterest, mortality)
```

### Guideline Premium Test (GPT) + cash value corridor
Two conditions, both required:

```
cumulativePremiumsPaid <= MAX(guidelineSinglePremium, guidelineLevelPremium × yearsElapsed)
deathBenefit >= cashValue × corridorPercentage(age)
```

### The corridor percentages (IRC §7702(d))

| Attained age | Minimum death benefit as % of cash value |
|---|---|
| 40 and under | 250% |
| 45 | 215% |
| 50 | 185% |
| 55 | 150% |
| 60 | 130% |
| 65 | 120% |
| 70 | 115% |
| 75–90 | 105% |
| 95+ | 100% |

**How this behaves in a projection:** as cash value grows, the corridor **forces the death benefit up** to stay compliant.

```
requiredDeathBenefit(n) = MAX(faceAmount, cashValue(n) × corridor(age))
```

> This is why a well-funded policy's death benefit **rises** in later years rather than staying level. A model holding the death benefit flat understates the estate value.

---

## 3. Test 2 — Is it a MEC? (IRC §7702A — the 7-pay test)

```
IF cumulativePremiumsPaid(first 7 years) > 7 × netLevelPremium:
    policy is a MODIFIED ENDOWMENT CONTRACT
```

### Why this is the test that matters most

| | Non-MEC | MEC |
|---|---|---|
| Loans / withdrawals | **Tax-free** (basis first, then loans) | **Taxable LIFO** — gains come out first |
| Penalty before 59½ | None | **10%** |
| Death benefit | Tax-free | Tax-free (unchanged) |

> The whole "tax-free retirement income" premise **depends entirely on the policy not being a MEC**. The strategy is to fund the policy as heavily as possible — right up to, but never past, the 7-pay limit. One overpayment permanently converts the policy, and the MEC status **cannot be undone**.

The engine must therefore track `cumulativePremium` against the 7-pay limit and **hard-stop** rather than silently modelling an over-funded policy.

---

## 4. Cash value roll-forward

```
cashValue(n) = cashValue(n−1)
             + premium(n)
             − premiumLoad(n)          ← typically 5–8% of premium
             − costOfInsurance(n)      ← rises steeply with age
             − policyFees(n)           ← administrative, per-thousand charges
             + creditedInterest(n)
             − loanInterest(n)         ← if loans outstanding
```

### Crediting, by product type

| Product | Credited rate |
|---|---|
| **Whole life** | Guaranteed rate (~2–4%) + non-guaranteed dividend |
| **IUL** | Index return, subject to **cap**, **floor** (usually 0%), and **participation rate** |
| **VUL** | Actual separate-account performance — can be negative |

### IUL crediting formula

```
rawIndexReturn = (indexEnd − indexStart) / indexStart
credited = MIN( MAX(rawIndexReturn × participationRate, floor), cap )
```

Typical: cap 9–10%, floor 0%, participation 100%.

> **The floor is the selling point and the cap is the cost.** Over a long horizon, a 0%-floor / 10%-cap sequence does **not** produce the same result as the index average — it truncates the best years while protecting the worst. Modelling IUL at a flat "index average return" overstates results badly.

### Cost of insurance rises with age

```
costOfInsurance(n) = netAmountAtRisk(n) × mortalityRate(age) / 1000
netAmountAtRisk(n) = deathBenefit(n) − cashValue(n)
```

This is why policies can **collapse in late years** if underfunded: COI accelerates while cash value is being drained by loans.

---

## 5. The illustration ceiling — AG 49-B

**NAIC Actuarial Guideline 49-B, effective 1 May 2023.** This is a regulatory cap on what may be *shown*, and any projection presented to a client should respect it.

| Rule | Requirement |
|---|---|
| Maximum illustrated rate | **≤ 145%** of the insurer's portfolio earning rate |
| Bonuses | Must be **included within** the cap, not shown on top |
| Index accounts | None may illustrate above the benchmark index account |
| Volatility-controlled indices | Must use the same leverage as the benchmark (S&P 500) |

> **Do not illustrate above this ceiling.** If the portfolio earns 5%, the maximum illustrated rate is 7.25% — inclusive of any bonus. Showing 8–9% because "the index has averaged that" is exactly what AG 49-B was written to stop.

---

## 6. Tax-free income via policy loans

### The mechanics

```
availableLoan(n) = cashValue(n) × maxLoanPercentage   ← typically 0.90
loanBalance(n)   = loanBalance(n−1) × (1 + loanRate) + newLoan(n)
netCashValue(n)  = cashValue(n) − loanBalance(n)
```

### Withdrawal order under §72(e)

For a **non-MEC**, withdrawals are **basis first (FIFO)** — the opposite of an annuity:

```
basis = cumulativePremiumsPaid − priorWithdrawals

IF withdrawal <= basis:  tax = 0                    ← return of basis
ELSE:                    switch to loans for the remainder
```

Standard practice: **withdraw to basis, then switch to loans.** Loans are not income at all, because a loan is not a realisation event.

### The failure mode that must be modelled

> **If the policy lapses with an outstanding loan, the entire gain becomes taxable immediately** — and the client receives no cash to pay the tax, because it was already borrowed and spent. This is the worst outcome in the product and it is the direct consequence of over-borrowing.

The engine must therefore run a **lapse test every year**:

```
IF netCashValue(n) < costOfInsurance(n) + fees(n):
    POLICY LAPSES
    taxableGain = loanBalance − basis
    FLAG this loudly — do not silently continue the projection
```

A model that borrows aggressively to hit an income target and never lapse-tests is producing a fictional number.

---

## 7. Death benefit and the estate

```
netDeathBenefit = deathBenefit(n) − loanBalance(n)
```

Income-tax-free under §101(a). **But estate-tax treatment depends on ownership** — see module 08 §4 and IRC §2042.

---

## Ordering traps

| Don't | Do |
|---|---|
| Assume tax-free loans without testing MEC status | Run the 7-pay test; MEC status is permanent |
| Hold the death benefit level as cash value grows | Apply the §7702(d) corridor — it forces the benefit up |
| Illustrate IUL at the index historical average | Cap at 145% of portfolio rate per AG 49-B |
| Model IUL as a flat return | Apply cap / floor / participation each year |
| Hold cost of insurance flat | It rises steeply with age on the net amount at risk |
| Borrow to a target and assume it works | Lapse-test every year; a lapse with a loan is a taxable disaster |
| Forget to subtract the loan from the death benefit | Net it out |

---

## Sources

| What | Source | Google this |
|---|---|---|
| §7702 definition, CVAT/GPT, corridor | [26 U.S.C. §7702](https://www.law.cornell.edu/uscode/text/26/7702) | `IRC 7702 life insurance contract defined cash value corridor` |
| §7702A MEC / 7-pay test | [26 U.S.C. §7702A](https://www.law.cornell.edu/uscode/text/26/7702A) | `IRC 7702A modified endowment contract seven pay test` |
| §72(e) distribution ordering | [26 U.S.C. §72(e)](https://www.law.cornell.edu/uscode/text/26/72) | `IRC 72(e) amounts not received as annuities life insurance` |
| Death benefit exclusion | [26 U.S.C. §101(a)](https://www.law.cornell.edu/uscode/text/26/101) | `IRC 101(a) life insurance proceeds excluded gross income` |
| AG 49-B illustration limits | [NAIC Actuarial Guideline 49-B](https://content.naic.org/) · [Industry summary](https://www.figmarketing.com/blog/ag-49-b-life-insurance-illustrations-what-you-need-to-know/) | `NAIC Actuarial Guideline 49-B IUL illustration maximum rate 145%` |
