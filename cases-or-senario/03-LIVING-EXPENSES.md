# 03 — Money going out

---

### How does spending change through the projection?

```
while working    monthly spend x 12 x (1 + inflation)^years
after retiring   the same, x 85%
after a spouse   the same, x 75%
   dies
```

Output: two step-downs, both adjustable. The 75% survivor factor is the more
important of the two — the house and its running costs do not halve when one
person dies, but the income often does.

Rule: `ASSUMPTION` — both factors.
Source: [index.html:1108](../index.html#L1108), [index.html:1007](../index.html#L1007)

Links to: → `13` (this is half of the widow's problem; tax is the other half)

---

### Why is medical inflated separately?

```
general spending   2.5% a year
medical spending   5.0% a year
```

Output: healthcare runs at roughly double general inflation, so over a 48-year
projection it becomes a far larger share of spending than it starts as.

Real evidence for the gap: the 2026 Part B premium rose **9.7%** while the
Social Security increase was **2.8%**. The premium is taken out of the benefit,
so the client's net cheque fell in a year their benefit rose.

Rule: `ASSUMPTION` for the rates. The 2026 figures are `RULE`.
Source: [index.html:999](../index.html#L999) · Module 15 §1

Links to: → `11` → `06`

---

### Long-term care starts. What happens to the plan?

Inputs: annual care cost · start age · duration · care inflation

Output: a cost of roughly $110,000–$135,000 a year is added on top of ordinary
spending, and it inflates at the medical rate, not the general one.

**No government body publishes an authoritative cost for this.** Module 33
says so directly. Every figure here is the adviser's choice.

Rule: `ASSUMPTION`.
Source: Module 33 §5.5, §10 · [index.html:1113](../index.html#L1113)

Links to: → `08` → `11` → `13`

---

### Which bucket pays for the care?

Output: **none of them.** The care cost is charged to general expenses, and the
plan then funds it in the normal withdrawal order — taxable, then pre-tax,
then Roth.

The "Disability / LTC Protection" bucket on the picture, funded at 3% a year,
is never touched. It sits there compounding at an investment rate
([index.html:1058](../index.html#L1058)) while the care it exists for is paid
from somewhere else.

Rule: `PROJECTION` — defect.

Links to: → `14` → `12`

---

### The care year makes my tax bill collapse. Is that right?

Output: yes, and it is worth planning around. Medical costs above the income
floor are deductible, and a large care year can wipe out most taxable income.

Worked example: $151,000 of expenses against $190,000 of AGI left $136,750
deductible, and federal tax of $4,891 instead of about $17,222.

That empty space is the cheapest Roth conversion room the client will ever
have — see `12`.

Rule: `RULE` — IRC §213(a).
Source: Module 32 §5.2, §6 Example 2 · [index.html:385](../index.html#L385)

Links to: → `12` → `08`

---

### What happens when the money runs out?

Output: the engine drains taxable, then pre-tax, then Roth. If all three are
empty and there is still a shortfall, it writes a note naming the year and the
amount:

> "Age 87: accounts run out. The plan is short by $42,000 this year."

It does not silently continue with a negative balance. That note is the single
most important line in any projection and should never be scrolled past.

Rule: `PROJECTION`.
Source: [index.html:1566](../index.html#L1566)

Links to: → `12` → `05`
