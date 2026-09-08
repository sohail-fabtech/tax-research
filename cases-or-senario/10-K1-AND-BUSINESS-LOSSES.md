# 10 — K-1, partnerships and business losses

The client puts money into a deal. The K-1 arrives with a loss on it. They
expect a tax refund. Often they get nothing.

A business loss passes through **four gates, in this fixed order**. It must
clear each one to reach the next. Whichever gate stops it decides what
frees it later — and each gate is freed by a different event.

```
Gate 1   §704(d) / §1366(d)   basis
Gate 2   §465                 at risk
Gate 3   §469                 passive
Gate 4   §461(l)              excess business loss
```

Run them out of order and you get a different answer. The engine runs gates
1 and 2 per property, then pools everything for gate 3
([index.html:1299](../index.html#L1299)).

---

## The four gates

### $250,000 loss on the K-1. How much comes off the tax bill this year?

Inputs: loss $250,000 · outside basis $180,000 · at risk $150,000 · client
does not work in the business · no other passive income · wages $600,000

```
Gate 1  §704(d) basis     allowed 180,000   suspended  70,000
Gate 2  §465 at risk      allowed 150,000   suspended  30,000
Gate 3  §469 passive      allowed       0   suspended 150,000
        the $25,000 allowance is fully gone at $600,000 of income
Gate 4  §461(l)           nothing reaches it

Deducted this year    $0
Suspended             70,000 + 30,000 + 150,000  =  250,000
```

Output: **$0 off this year's tax.** All $250,000 waits, split three ways.
Every dollar is suspended at exactly one gate, and the three piles are not
interchangeable.

Rule: `RULE` — IRC §704(d) → §465 → §469 → §461(l), in that order.
Source: Module 23 §6 Example 4 · Module 26 §5.3

Missing: whether anyone guaranteed the partnership debt — that changes gate 2
and nothing else.

Links to: → `02` (no AGI change, so no knock-on)
          → `09` (a rental loss dies at the same gates)
          → `13` (each pile dies differently when the client dies)

---

### The loss is bigger than what I actually put in.

Inputs: cash contributed · income allocated over the years · distributions
taken · losses already deducted · share of partnership debt under §752

Output: the excess stops at gate 1 and waits until basis is rebuilt — by
future income or more money in. It never expires, but it also never moves on
its own.

Rule: `RULE` — §704(d) with §705 and §752 for a partner; §1366(d)(1) with
§1367(a) for an S-corp shareholder.
Source: Module 26 §5.3, §6 Example 1

Links to: → `13` (basis-suspended losses are lost at death — they do not
            pass to heirs)

---

### The partnership has a mortgage, so I have basis — but I am told I am not "at risk".

Output: basis and at-risk are two different numbers and they move
differently. Nonrecourse debt raises basis under §752 whether or not it
qualifies. Only *qualified nonrecourse financing* raises the at-risk amount.

A normal bank mortgage on real property usually qualifies, so most clients
never notice gate 2 exists. Seller financing usually does not qualify — the
seller has an interest in the property.

Rule: `RULE` — §465(b)(6) four conditions; §465(b)(3) borrowing from a person
with an interest.
Source: Module 23 §5.4, §8

Links to: → `09` (seller-financed property purchases)

---

### My partner personally guaranteed the loan, and now MY losses are blocked.

Output: a personal guarantee by any person disqualifies the debt as qualified
nonrecourse financing **for everybody else in the deal**. The guarantor gets
at-risk amount for it; the other partners lose theirs.

Module 23 calls this "the single most common way a co-owner's at-risk amount
collapses."

Rule: `RULE` — §465(b)(6)(B)(iii); §465(b)(1)(B) for the guarantor.
Source: Module 23 §5.5, §6 Example 3, §8

Links to: → `09` → `08` (guarantees and indemnities)

---

### I heard I can deduct $25,000 of rental loss. Why did I get nothing?

Inputs: modified AGI · active participation · at least 10% ownership · loss

```
AGI  $95,000   →   full $25,000 allowance
AGI $120,000   →   25,000 − 0.50 × (120,000 − 100,000)  =  $15,000
AGI $150,000   →   $0
```

Output: the allowance drops 50 cents for every dollar of AGI over $100,000
and is gone at $150,000. **Neither figure has been indexed since 1986**, so
it catches more people every year.

Rule: `RULE` — §469(i).
Source: Module 25 §5.3, §6 Example 1 · [index.html:388](../index.html#L388)

Links to: → `07` (a required distribution raises the AGI that kills this)
          → `11` (same AGI drives the Medicare surcharge)

---

### The loss is not passive at all, but I still cannot use all of it.

Inputs: total business deductions · total business income · filing status

```
2026 threshold   $256,000 single   ·   $512,000 joint
```

Output: anything above the threshold is disallowed this year and becomes a
net operating loss next year.

**Watch this one in 2026.** The threshold **fell** from $313,000 / $626,000
— an 18.2% drop. Thresholds normally rise. This one did not.

Rule: `RULE` — §461(l)(1) and (3)(A); §461(l)(2) converts the excess to an NOL.
Source: Module 18 §5.2, §5.3 · [index.html:386](../index.html#L386)

Links to: → `09` (cost segregation is what usually creates a loss this big)
          → `16` (a tax-law change mid-projection)

---

## Income with no cash

### The K-1 says $150,000 of income. The partnership sent me nothing. I still owe tax.

Inputs: distributive share $150,000 · cash actually received $0 · marginal rate

Output: the client is taxed on the full $150,000. It also raises basis under
§705, which helps a future loss — but that is no comfort in April.

The cash to pay the tax has to come from somewhere, and every source has its
own cost.

Rule: `RULE` — §702 and §704 tax the distributive share regardless of
distribution.
Source: Module 26 §5.2, §5.5

Missing: whether the operating agreement has a tax-distribution clause.

Links to: → `12` (which account funds the tax bill)
          → `11` (the phantom income still drives the Medicare surcharge)

---

### I took a distribution after several loss years and got a capital gain.

Output: losses reduce stock basis first, then debt basis. Once basis is at
zero, a distribution above it is capital gain — even though the client
"only took out their own money".

Rule: `RULE` — §1367(b)(2); §1368 / §731.
Source: Module 26 §5.4, §6 Example 3

Links to: → `02`

---

### The bank made me guarantee my S corporation's loan. Doesn't that give me basis?

Output: **No.** An S-corp shareholder gets debt basis only from indebtedness
of the corporation *to the shareholder*. A guarantee creates nothing until
the shareholder actually pays.

The fix is to borrow personally and lend on to the company — back-to-back.
This is the single most expensive difference between an LLC and an S corp
for a loss-making business, because a partner *does* get basis for
partnership debt under §752.

Rule: `RULE` — §1366(d)(1)(B).
Source: Module 26 §5.2, §6 Example 2, §9

Links to: → `01` (the same choice cuts the other way on employment tax)

---

## Getting the losses back

### I sold the partnership interest. Do all those suspended losses come back?

Output: yes for the passive pile — but only if **all three** are true:
the entire interest was sold, the sale was fully taxable, and the buyer is
not a related party. Miss any one and the release does not happen.

| What was suspended | Released on sale? |
|---|---|
| §469 passive | Yes, in full |
| §465 at risk | Yes, on disposition |
| §704(d) / §1366(d) basis | **No — generally lost** |

A gift is not a sale: the suspended loss is added to the donee's basis and
the donor loses it. A sale to a related party defers the release instead of
granting it.

Rule: `RULE` — §469(g)(1); §469(g)(1)(B) related-party deferral.
Source: Module 25 §5.5, §6 Examples 3 and 4

Links to: → `09` (aggregating rentals blocks release on selling just one)
          → `13`

---

### I own the building my own practice rents. Can that rent soak up my other suspended losses?

Output: **No, and it works against the client.** Net self-rental *income* is
recharacterised as non-passive, so it cannot absorb passive losses. A net
self-rental *loss* stays passive. The rule only ever runs one way.

Rule: `RULE` — Treas. Reg. §1.469-2(f)(6).
Source: Module 25 §5.6, §6 Example 5

Links to: → `09`

---

### I have a big carryforward. How long until I actually use it?

Output: an NOL can only wipe out 80% of taxable income in any later year, so
20% always stays taxable. It carries forward indefinitely with no carryback.

Rule: `RULE` — §172(a)(2) 80% limit; §172(b)(1)(A).
Source: Module 27 §5.2, §5.3 · [index.html:387](../index.html#L387)

Links to: → `12` (a Roth conversion is a good way to feed income to a
            carryforward)

---

### I am carrying large suspended losses and I am getting old. What happens when I die?

Output: mostly bad. This is the case clients never ask until it is too late.

| Pile | At death |
|---|---|
| NOL carryforward | **Extinguished.** Nothing survives. |
| §469 passive suspended | Released **only** above the §1014 step-up — so the bigger the step-up, the less comes back |
| §704(d) / §1366(d) basis suspended | **Lost** |

Rule: `RULE` — §172 (no survival provision); §469(g)(2); §1014.
Source: Module 27 §5.5, §8 · Module 25 §5.5, §6 Example 4

Output in plain terms: losses are worth far more used during life than left
to heirs. That is an argument for accelerating income — a Roth conversion or
a deliberate gain — while the losses are still alive.

Links to: → `12` (accelerate income to use them) → `13` → `15`

---

## What the software does not tell the client

The engine runs all four gates correctly. It computes exactly how much
stopped at each one, in `runGates` at [index.html:873](../index.html#L873):

```js
return { allowed, sBasis, sAtRisk, sPassive, basisAfter, atRiskAfter, ok };
```

Then it throws the breakdown away. `passiveSusp`, `nol` and `ebl` are stored
on every row at [index.html:1643](../index.html#L1643) but appear in **no
column of the year table and in no note**.

So a client whose $250,000 loss was fully suspended sees a screen identical
to a client who had no loss at all. They are never told which gate stopped
it, how much is waiting, or what would free it.

That is why this question had no answer.

Links to: → `00`
