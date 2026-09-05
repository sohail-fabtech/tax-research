# 05 — Required Minimum Distributions (RMDs)

**Step 5 of the year loop** · Rail: **nominal**

---

## What this computes

The amount the IRS **forces** out of pre-tax retirement accounts each year once the client reaches RMD age. This is not optional and not a planning choice — it is a compelled taxable event, and it is often what pushes a retiree into a higher bracket, makes 85% of their Social Security taxable, and trips IRMAA, all in the same year.

---

## 1. When RMDs start — SECURE 2.0

| Birth year | RMD begins at age | First RMD year |
|---|---|---|
| 1950 or earlier | 72 (or 70½ pre-2020) | — |
| **1951 – 1959** | **73** | year they turn 73 |
| **1960 or later** | **75** | year they turn 75 |

```
rmdAge = IF birthYear >= 1960 THEN 75
         ELSE IF birthYear >= 1951 THEN 73
         ELSE 72
```

> **`birthYear` is a required input.** You cannot derive the RMD age from current age alone — a 66-year-old in 2026 was born in 1960 and starts at 75; a 67-year-old was born in 1959 and starts at 73. Two years of age difference, two years' difference in RMD age, and a very different tax path.

**Note on the 1959 cohort:** SECURE 2.0 as drafted created an ambiguity for people born in 1959 (arguably both 73 and 75). IRS proposed regulations resolved this to **age 73**. Use 73 for 1959.

### Required Beginning Date

```
requiredBeginningDate = April 1 of the year AFTER the first RMD year
```

So a client turning 73 in 2026 has a 2026 RMD, payable by **1 April 2027**.

> **The deferral trap:** if the first RMD is delayed into the following April, **two RMDs land in the same tax year** — the deferred one and that year's own. For a high-balance client this can be a bracket disaster. The model should default to taking the first RMD in its own year, and flag the deferral option rather than assuming it.

---

## 2. The formula

```
RMD(age) = priorYearEndBalance / applicableDenominator(age)
```

That is the whole calculation. Two inputs:

- **`priorYearEndBalance`** — the balance on **31 December of the previous year**. Not the current balance. Not an average.
- **`applicableDenominator`** — from the IRS Uniform Lifetime Table, using the age the client **attains during** the distribution year.

**Worked number** — $1,000,000 balance at end of 2025, client turns 75 in 2026:

```
RMD = 1,000,000 / 24.6 = $40,650
```

This matches the worked example printed in IRS Publication 590-B itself.

---

## 3. The Uniform Lifetime Table (Table III)

Reproduced exactly from **IRS Publication 590-B, Appendix B, Table III**.

Use this table when: the owner is unmarried, **or** the spouse is not more than 10 years younger, **or** the spouse is not the sole beneficiary.

| Age | Denominator | Age | Denominator | Age | Denominator |
|---|---|---|---|---|---|
| 72 | 27.4 | 89 | 12.9 | 106 | 4.3 |
| 73 | 26.5 | 90 | 12.2 | 107 | 4.1 |
| 74 | 25.5 | 91 | 11.5 | 108 | 3.9 |
| 75 | 24.6 | 92 | 10.8 | 109 | 3.7 |
| 76 | 23.7 | 93 | 10.1 | 110 | 3.5 |
| 77 | 22.9 | 94 | 9.5 | 111 | 3.4 |
| 78 | 22.0 | 95 | 8.9 | 112 | 3.3 |
| 79 | 21.1 | 96 | 8.4 | 113 | 3.1 |
| 80 | 20.2 | 97 | 7.8 | 114 | 3.0 |
| 81 | 19.4 | 98 | 7.3 | 115 | 2.9 |
| 82 | 18.5 | 99 | 6.8 | 116 | 2.8 |
| 83 | 17.7 | 100 | 6.4 | 117 | 2.7 |
| 84 | 16.8 | 101 | 6.0 | 118 | 2.5 |
| 85 | 16.0 | 102 | 5.6 | 119 | 2.3 |
| 86 | 15.2 | 103 | 5.2 | 120+ | 2.0 |
| 87 | 14.4 | 104 | 4.9 | | |
| 88 | 13.7 | 105 | 4.6 | | |

### The exception — much younger spouse

If the sole beneficiary is a spouse **more than 10 years younger**, use **Table II (Joint and Last Survivor)** instead. The denominator is larger, so the RMD is smaller.

Example from Pub 590-B: owner turns 75, spouse turns 64 (11 years younger) → denominator **25.3**, not 24.6. RMD on $1,000,000 is $39,526 instead of $40,650.

### What the denominator means

The RMD is a rising percentage of the balance:

| Age | Denominator | ≈ % of balance forced out |
|---|---|---|
| 73 | 26.5 | 3.77% |
| 75 | 24.6 | 4.07% |
| 80 | 20.2 | 4.95% |
| 85 | 16.0 | 6.25% |
| 90 | 12.2 | 8.20% |
| 95 | 8.9 | 11.24% |
| 100 | 6.4 | 15.63% |

> By the late 80s the forced withdrawal rate exceeds any reasonable portfolio return. **Balances peak and then decline.** A roadmap that shows pre-tax balances rising forever to age 90 has not modelled RMDs.

---

## 4. Which accounts are subject

| Account | RMD required? |
|---|---|
| Traditional IRA, SEP, SIMPLE | **Yes** |
| 401(k), 403(b), 457(b) | **Yes** |
| **Roth IRA** | **No — never during the owner's lifetime** |
| **Roth 401(k)** | **No — eliminated by SECURE 2.0 from 2024** |
| Taxable brokerage | No |
| Life insurance cash value | No |

> The Roth 401(k) exemption is new. Before 2024 Roth 401(k)s **did** require RMDs. Any logic written against the old rule is wrong now.

### Aggregation rules

- **IRAs:** compute the RMD for each IRA separately, but the **total** may be taken from any one or combination of them.
- **401(k)s:** each plan's RMD must be taken **from that plan**. No aggregation across employers.

This matters because it changes which balance is drawn down.

---

## 5. Tax treatment

```
rmdTaxableAmount = rmd    (100% ordinary income, if no after-tax basis)
```

- Taxed as **ordinary income** at the client's marginal rate.
- **Not** eligible for capital gains rates.
- **Not** subject to NIIT (module 02) — but **it does raise MAGI**, which can push other investment income over the NIIT threshold and can trip IRMAA two years later.

### The QCD offset

From age **70½** (note: not the RMD age — 70½), the client may direct up to **$111,000** (2026; indexed annually under SECURE 2.0) per year directly from an IRA to charity. That amount:
- satisfies the RMD,
- is **excluded from AGI entirely** — better than a charitable deduction, because it never enters provisional income or MAGI.

```
taxableRMD = MAX(0, rmd − qualifiedCharitableDistribution)
```

For a charitably inclined client this is the single most efficient RMD strategy available, and the model should expose it.

---

## 5b. When the account owner dies — the surviving spouse's choices

A surviving spouse has options no other beneficiary has. The choice changes the RMD for the rest of their life.

| Option | RMD basis | Early-withdrawal penalty under 59½ |
|---|---|---|
| **Spousal rollover** — treat it as their own | Their **own** age, Uniform Lifetime Table | **10% applies** |
| **Remain a beneficiary** (inherited IRA) | Deceased's schedule, single life table | **No penalty** |
| **SECURE 2.0 §327 election** (from 2024) | Treated as the **deceased employee** — RMDs start when the deceased *would have* reached RMD age, using the Uniform Lifetime Table | **No penalty** |

```
IF survivingSpouse is sole beneficiary:
    IF survivor is under 59½ and needs the money:
        → stay a beneficiary, or make the §327 election  (no 10% penalty)
    ELSE IF deceased was YOUNGER than the survivor:
        → §327 election delays RMDs until the deceased would have hit 73/75
    ELSE:
        → spousal rollover is usually simplest
```

> **The §327 election is new and widely missed.** Where the deceased spouse was the younger of the two, it can postpone RMDs by years — and the resulting empty brackets are exactly the Roth conversion window described above.

> **Non-spouse beneficiaries** get none of this. Most must empty the account within **10 years**, often during their own peak earning years.

## 6. Penalty

| Situation | Excise tax |
|---|---|
| RMD not taken | **25%** of the shortfall |
| Corrected within 2 years | Reduced to **10%** |

SECURE 2.0 cut this from the previous 50%.

---

## 7. Where the RMD lands in the year loop

```
STEP 5   rmd = priorYearEndPretaxBalance / denominator(age)
STEP 6   AGI includes rmd          ← taxable income
STEP 7   tax computed on that AGI
STEP 9   pretaxBalance reduced by rmd
```

> **The RMD must be added to income BEFORE the tax step.** Computing tax first and then subtracting the RMD understates tax for every year from 73/75 to death.

If the RMD exceeds what the client needs to spend, the excess does **not** disappear — after tax, it moves to the taxable brokerage bucket:

```
surplus = rmd − amountNeededForExpenses − taxOnRmd
taxableBalance = taxableBalance + surplus
```

---

## Ordering traps

| Don't | Do |
|---|---|
| Use the current balance | Use the **31 December prior-year** balance |
| Use age at the start of the year | Use the age **attained during** the year |
| Apply RMDs to Roth accounts | Roth IRA and (since 2024) Roth 401(k) are exempt |
| Assume everyone starts at 73 | Born 1960+ starts at **75** — needs `birthYear` |
| Compute tax before adding the RMD | RMD goes into income first |
| Let the pre-tax balance grow forever | RMD % exceeds returns after ~age 85 |
| Subject the RMD to NIIT | Excluded from NII, but included in MAGI |
| Aggregate 401(k) RMDs across plans | Each 401(k) pays its own |
| Roll over automatically on a spouse's death | Test all three options — rollover, beneficiary, §327 election |
| Apply the 10% penalty to an inherited IRA | It does not apply while the survivor remains a beneficiary |

---

## Sources

| What | Source | Google this |
|---|---|---|
| Uniform Lifetime Table, RBD, worked examples | [IRS Publication 590-B](https://www.irs.gov/publications/p590b) ([PDF](https://www.irs.gov/pub/irs-pdf/p590b.pdf)) | `IRS Publication 590-B Appendix B Table III Uniform Lifetime` |
| RMD ages, penalty | [IRS — Retirement topics: RMDs](https://www.irs.gov/retirement-plans/plan-participant-employee/retirement-topics-required-minimum-distributions-rmds) | `IRS retirement topics required minimum distributions` |
| SECURE 2.0 age changes | [IRS — RMD FAQs](https://www.irs.gov/retirement-plans/retirement-plan-and-ira-required-minimum-distributions-faqs) | `IRS required minimum distribution FAQs SECURE 2.0 age 73 75` |
| Surviving spouse §327 election | SECURE 2.0 Act §327 · IRS 2024 final regulations | `SECURE 2.0 section 327 surviving spouse election` |
