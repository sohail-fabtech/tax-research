# 16 — Events that change or stop the plan

Everything else in these files assumes the plan runs as drawn. It rarely does.
Each event below redirects the projection from the year it happens.

---

### The client retires earlier than planned.

Output: earned income stops sooner, so contributions stop sooner and the
deployable capital stops with them. The conversion window opens earlier and
lasts longer, which partly compensates.

Under 59½ the 10% extra tax is the binding constraint. Three ways round it:
leaving the job in or after the year of turning **55** and leaving the money in
that employer's plan; disability; or a fixed schedule of equal payments.

Rule: `RULE` — IRC §72(t)(2)(A)(v),(iii),(iv).
Source: Module 37 §5.4, §5.5

Links to: → `12` → `04` → `14`

---

### The client becomes disabled.

Output: two separate problems. The tax one is easy — disability is a
recognised exception, so retirement money is reachable without the 10%.

The cash-flow one is harder and is the part clients do not expect:

```
Disability benefits      5-month waiting period with nothing
Medicare eligibility     24 months after that
```

That is roughly two and a half years to bridge from savings or a private
policy. Whether a private benefit is taxable depends on who paid the premium.

Rule: `RULE` — IRC §72(t)(2)(A)(iii), §72(m)(7); Social Security Act §223, §226(b).
Source: Module 37 §5.2, §5.6, §6 Examples 1, 4–5

Links to: → `08` → `03` → `06`

---

### A spouse dies.

Output: the largest single event in the whole projection, and it moves five
things at once.

| | Effect |
|---|---|
| Filing status | joint for the year of death, single after |
| Brackets | roughly **halve** |
| Social Security | keeps the larger benefit, not both |
| Social Security taxed above | $32,000 → **$25,000** |
| Medicare surcharge starts at | $218,000 → **$109,000** |
| Spending | falls, but by far less than income |

Worked example: gross income **down 12%**, federal tax **up 29.5%**, cash
after tax **down 16.9%**.

The Medicare side **can** be appealed — death is a qualifying life event.

Rule: `RULE` — IRC §6013(a)(3), §1(j)(2), §86(c); 20 CFR §418.1205(a).
Source: Module 35 §5.2, §5.3, Examples 1 and 4

Links to: → `13` → `06` → `11` → `12`

---

### Divorce.

Output: accounts split without tax if done correctly — a court order for an
employer plan, a direct transfer for an IRA. Done as a withdrawal, it is taxed
and can carry the 10%.

Filing status is decided by the position on **31 December**, not by when the
process started. A decree in December means single for the whole year.

Divorce is a qualifying life event for the Medicare surcharge. A ten-year
marriage preserves a claim on the ex-spouse's Social Security record.

Rule: `RULE` — IRC §1041, §414(p), §408(d)(6), §7703(a); 20 CFR §418.1205.
Source: Module 36 §5.2–§5.6

Links to: → `13` → `06` → `11`

---

### The business is sold, or another windfall lands.

Output: one enormous year. The gain stacks on ordinary income, the 3.8% tax
reaches other income, the deduction limits bite, and the Medicare surcharge
arrives two years later and **cannot be appealed**.

Three levers, all of which must be pulled **before** the sale:
- qualifying C-corporation stock can be excluded, more the longer it is held
- taking the price in instalments spreads it across brackets and tiers
- charitable giving in the same year is at its most valuable

Rule: `RULE` — IRC §1(h), §1411, §1202, §453.
Source: Module 38 §5.2, §5.3 · Module 24 §5.5

Links to: → `13` → `11` → `10`

---

### A property is sold.

Output: depreciation recapture is the surprise, and cost-segregated components
come back at ordinary rates. The sale also releases suspended losses on that
activity, which can offset a large part of the gain — but only if the whole
interest goes, to an unrelated party, in a fully taxable sale.

Rule: `RULE` — IRC §1245, §1250, §1(h)(1)(E), §469(g).
Source: Module 22 §5.5 · Module 25 §5.5

Links to: → `09` → `10` → `11`

---

### The market falls.

Output: **the model cannot show this.** One flat rate is applied every year.
There is no crash, no recovery, and no modelling of the order returns arrive
in.

A poor return in the first years of drawing down does far more damage than the
same return later, because the client is selling assets to live on while they
are cheap. That risk is real and is simply not in the projection.

Say this plainly to any client who asks "what if the market drops?"

Rule: `ASSUMPTION` — and a stated limitation.

Links to: → `05` → `12`

---

### The insurance policy lapses.

Output: the tax-free income stream stops, the death benefit disappears, and a
large ordinary income bill arrives with no cash attached. Worked example:
$220,000 of gain, $52,800 of tax, $0 received.

The engine does test for this every year and writes a note. That note is the
warning.

Rule: `RULE` — IRC §72(e).
Source: Module 30 §6 Example 5

Links to: → `08` → `13`

---

### A forced withdrawal is missed.

Output: 25% of the amount that should have come out, cut to 10% if fixed
within two years, and waivable for reasonable error.

Each 401(k) carries its own shortfall, so taking everything from one plan
leaves a penalty waiting in each of the others.

Rule: `RULE` — IRC §4974.
Source: Module 09 §5.10

Links to: → `07`

---

### A 401(k) loan is outstanding when the client leaves the job.

Output: unrepaid, it becomes a taxable distribution, plus 10% if under 59½.
There is a rollover window — to the tax return due date including extensions —
to undo it. Most people never hear about the window.

Rule: `RULE` — IRC §72(p), §402(c)(3)(C).
Source: gap — not covered in Modules 07–10.

Links to: → `12`

---

### Money is inherited.

Output: what arrives matters more than how much.

| Inherited | Cost to the heir |
|---|---|
| Taxable account or property | basis steps up, prior gain erased |
| Pre-tax IRA or 401(k) | ordinary income, ten years to empty, no step-up |
| Roth | tax-free, still ten years to empty |
| Life insurance | free of income tax |

Rule: `RULE` — IRC §1014, §691, §401(a)(9)(H), §101(a).
Source: Module 31 §5.2, §5.3 · Module 09 §5.9

Links to: → `13` → `07`

---

### The law changes mid-projection.

Three are already on the statute book and **must** be built in, not discovered
later:

| When | What |
|---|---|
| **2026** | the excess business loss threshold **fell** to $256,000 / $512,000, down 18.2% |
| **After 2028** | the senior deduction ends — taxable income rises $12,000 for a couple with no change in income |
| **2030** | the state and local deduction reverts to $10,000 |

Output: a projection to age 90 crosses all three. Anything that treats today's
rules as permanent is wrong from the start.

Rule: `RULE` — P.L. 119-21; IRC §461(l), §151(d)(5)(C), §164(b)(7).
Source: Module 18 §5.3 · Module 02 §5, §8

Links to: → `02` → `10` → `15`

---

### The client moves state.

Output: changes income tax, and separately changes estate tax — the two are
not linked. A client leaving New York escapes both the income tax and the
cliff in `13`. A client moving to Oregon picks up an estate tax starting near
$1,000,000.

Rule: `RULE` — state statute.

Missing: the engine takes one state for the whole projection. A mid-life move
is not modelled.

Links to: → `02` → `13`
