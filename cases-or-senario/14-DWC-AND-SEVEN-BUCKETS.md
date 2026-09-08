# 14 — Deployable Wealth Capital and the seven buckets

This is the picture's own logic, not tax law. Almost nothing here has an IRC
section behind it. Every number is `ADVISOR` or `ASSUMPTION`, and the picture
says so itself:

> The front end should render approved values from the roadmap engine. It
> should not determine eligibility, calculate tax savings, or override
> advisor-approved assumptions.

Read that as: **the adviser owns these numbers, the software just displays them.**

---

## Before anything else: there are three different formulas, and they disagree

This has to be settled before any of the numbers below mean anything.

**1. The picture**

```
Net Tax Savings + DWC % x Qualified Deduction Base
188,000 + 0.20 x 420,000  =  $272,000
```

**2. The front end** — [index.html:1050](../index.html#L1050)

```js
const annualDWC = (netTaxSavings + dwcPct * N(s.qualifiedDeductionBase)) * effectiveness;
```

Same as the picture, with an effectiveness multiplier added.

**3. The documented methodology** — Module 39, which is also what the
`tax-be` backend actually runs

```
totalTaxSaved = baseTotalTaxSaved x (strategyEffectiveness / 100)
```

**There is no DWC percentage in it. There is no qualified deduction base in
it.** Both terms are absent. The whole $84,000 that the picture adds on top
of the tax savings has no counterpart in the documented method.

Checked directly against the 12,033-line reference document:

| Searched for | Times it appears |
|---|---|
| "Deployable Wealth Capital" or "DWC" | **0** |
| "Qualified deduction base" | **0** |

Module 39 is titled "Tax Savings Deployment Framework" and labels itself
*"Proprietary methodology — not law."* It says nothing in it may be cited to
the Internal Revenue Code.

**And the bucket counts do not agree either:**

| Source | Buckets |
|---|---|
| The picture | **7** |
| Module 39 (the documented method, and the backend) | **6** |
| `index.html` | **6** |

Module 39 says "the six buckets" in four separate places. Market /
Opportunity Capital exists only on the picture.

**Module 39 also splits the money differently.** It does not apply flat
percentages to the whole balance. It computes an *allocatable plan* first:

```
allocatablePlan = max(0, plan - compoundedQualifiedSavings)
retirement      = compoundedQualifiedSavings + 0.35 x allocatablePlan
the other five  = straight percentage x allocatablePlan
```

The front end does none of this. It seeds buckets from raw inputs and grows
each at its own rate.

So the picture, the front end and the documented method are three different
calculations producing three different numbers from the same client. **Pick
one before this goes in front of a client.** Everything below describes what
the front end does today.

Links to: → `17` (which picture numbers survive this)

---

## How much gets deployed

### The adviser approves $188,000 of savings. How much actually goes to work?

Inputs: net tax savings $188,000 · DWC 20% · qualified deduction base $420,000 · effectiveness 100%

```
(188,000 + 0.20 × 420,000) × 100%  =  $272,000 per year
```

Output: $272,000 deployed every working year.

Rule: none. `ADVISOR` — all four inputs come from the adviser's tax plan.
Source: picture formula card · [index.html:1050](../index.html#L1050)

Links to: → `02` (the savings are only real if the strategies survive audit)
          → `17` (the $420,000 base is not printed on the picture)

---

### The client's strategy costs more to run than it saves this year.

Inputs: strategy federal + state savings $60,000 · investment required $90,000

```
Net for the year  =  60,000 + 0 − 90,000  =  −$30,000
```

Output: nothing deploys this year. The buckets get their growth but no new money.

**Careful — the engine gets this partly wrong.** [index.html:1595](../index.html#L1595)
gates the *whole* deployment on the savings being positive:

```js
if (working && savingsThisYear > 0) { ... }
```

So the `DWC% × Qualified Deduction Base` half is dropped too. That half is
$84,000 a year and it does not depend on the savings at all. In a year where
a strategy costs more than it returns, the client silently loses $84,000 of
deployment they were entitled to.

Rule: none. `PROJECTION` — and this one is a defect.
Source: [index.html:1595](../index.html#L1595)

Links to: → `05` (a missed year compounds for the rest of the projection)

---

### The client pushes the DWC dial to 40%.

Inputs: same $188,000 · DWC 40% · base $420,000

```
188,000 + 0.40 × 420,000  =  $356,000 per year   (+31%)
```

Output: $356,000 a year. The picture's slider allows it — 0% to 40% — but
marks 15–25% as recommended.

Nothing in the engine stops a client at 40%. The recommendation is hint text
at [index.html:705](../index.html#L705), not a guardrail, and the picture's
visible slider does not exist in the UI at all.

Rule: none. `ADVISOR`.

Links to: → `17`

---

### The adviser is only 80% confident the strategies will land.

Inputs: $272,000 · effectiveness 80%

```
272,000 × 0.80  =  $217,600 per year
```

Output: $217,600. Over 20 working years that is **$1.09M less** deployed
before any growth is counted.

Effectiveness is also set by the scenario picker — conservative 80%,
expected 100%, accelerated 125%.

Rule: none. `ADVISOR`.
Source: [index.html:1050](../index.html#L1050), [index.html:988](../index.html#L988)

Links to: → `05`

---

## Where the money goes

### The $272,000 splits seven ways.

| Bucket | Share | Per year | Grows at |
|---|---|---|---|
| Liquidity reserve | 10% | $27,200 | 5.75% |
| 401(k) / cash balance / Roth | 25% | $68,000 | 7.00% |
| Life insurance cash value | 20% | $54,400 | 5.50% |
| Real estate / business | 25% | $68,000 | 5.00% |
| Market / opportunity capital | 10% | $27,200 | 5.75% |
| Legacy / trust / philanthropy | 7% | $19,040 | 5.75% |
| Disability / LTC protection | 3% | $8,160 | 5.75% |

Every rate is an `ASSUMPTION`, and admin fee plus cost of investment are
subtracted from all of them as drag.

Because the rates differ, the ending dollars stop matching the percentages.
That is correct, not a bug — see `17`.

Source: [index.html:1057](../index.html#L1057)

Links to: → `04` (the 401(k) bucket collides with real contribution limits)
          → `08` (the insurance bucket) → `09` (the real estate bucket)

---

### The client asks: is the $15.4M on the picture the same as my net worth?

Output: **No, and this is the biggest problem in the current build.**

The seven buckets are a separate ledger. The engine computes their total at
[index.html:1601](../index.html#L1601):

```js
const dwcTotal = Object.values(bucket).reduce((a,b)=>a+b,0);
```

and then computes net worth at [index.html:1609](../index.html#L1609)
**without it**:

```js
const gross = pretax + roth + taxable + cv - polLoan + reEquity
            + N(s.otherAssets) + insInEstate;
```

`dwcTotal` is not in that line. So the bucket table and the net-worth chart
sit on the same screen showing two unrelated worlds. Deploying $272,000 a
year for twenty years moves the bucket table and does **nothing** to the
projected estate.

Rule: none. `PROJECTION` — defect.

Links to: → `13` (the estate number the client actually cares about)

---

### There are only six buckets in the software, not seven.

**Market / Opportunity Capital (10%) does not exist.** The engine's bucket
list at [index.html:1051](../index.html#L1051) has six keys: retirement,
insurance, realestate, liquidity, legacy, disabilityLtc. The UI even prints
the words "split across six buckets" at [index.html:1979](../index.html#L1979).

The research already assumes seven — [09-WORKED-EXAMPLE.md](../09-WORKED-EXAMPLE.md)
line 45 lists Market / opportunity at 10%, $27,200 a year.

Output: 10% of every deployment has nowhere to go. The remaining six are
re-normalised to 100%, so each one is silently overweighted.

Links to: → `05`

---

### The default splits in the software are not the picture's splits.

| Bucket | Picture | Software default |
|---|---|---|
| Liquidity | 10% | 10% |
| 401(k) / Roth | 25% | **35%** |
| Life insurance | 20% | **25%** |
| Real estate | 25% | 25% |
| Market / opportunity | 10% | **absent** |
| Legacy / trust | 7% | **3%** |
| Disability / LTC | 3% | **2%** |

Output: a client who never touches the bucket fields gets a plan that does
not match the picture they were shown.

Source: [index.html:474](../index.html#L474)

---

### The client's house gets counted twice.

Inputs: house worth $1,300,000, entered once in the property list and once as "current real estate value"

The real estate bucket is seeded from `currentRealEstateValue` at
[index.html:1060](../index.html#L1060). Separately, `reEquity` is built from
the property list at [index.html:1605](../index.html#L1605).

Output: the same house appears in both. The insurance bucket has the same
problem — it compounds at the credited rate while the actual policy cash
value is rolled forward independently at STEP 17.

Rule: none. `PROJECTION` — defect.

Links to: → `09` → `08`

---

### The disability / LTC bucket grows like an investment and never pays a claim.

Inputs: 3% of $272,000 = $8,160 a year

The engine grows this bucket at the taxable investment rate,
[index.html:1058](../index.html#L1058):

```js
disabilityLtc: rTax - costDrag
```

Output: it compounds at 5.75% forever. But protection is a premium paid out,
not an asset that grows — and when long-term care actually starts, the cost
is charged to general expenses and **never drawn from this bucket**.

So the bucket that exists to fund care does not fund care.

Rule: none. `PROJECTION` — defect.

Links to: → `03` (where the LTC cost is actually charged)
          → `08` (the policy that would really pay)
