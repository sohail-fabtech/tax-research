# 12 — Taking money out, and converting

---

### Which account does the money come out of first?

The engine drains in a fixed order, [index.html:1547](../index.html#L1547):

```
1.  Taxable brokerage
2.  Pre-tax (401k / IRA)
3.  Roth        — last, on purpose
```

Output: Roth is preserved to the end because it is the only pot that costs
nothing to use and passes to heirs without an income tax bill.

Rule: `PROJECTION` — no law sets an order. This is a modelling choice.

Missing: the order is **not selectable**. Competing tools let the client
change it, and for some households a different order wins.

Links to: → `13` → `07`

---

### The window between retiring and forced withdrawals.

Inputs: retires at 62 · born 1960, so forced withdrawals start at 75

```
13 years with almost no forced income
```

Output: this is the single biggest planning opportunity in the whole
projection. Earned income has stopped, forced withdrawals have not started,
and taxable income is largely under the client's control.

Income taken here — by conversion or by realising gain — is taxed at rates
that will never be available again.

Rule: `PROJECTION`. The ages come from `RULE`.
Source: Module 09 §9

Links to: → `07` → `11` → `15`

---

### I want to convert $200,000 to Roth.

Inputs: conversion $200,000 · all traditional/SEP/SIMPLE IRA balances · any
Form 8606 basis · where the tax money comes from

Output: the converted amount is ordinary income this year. There is **no
income limit** on converting, in any year.

Three things that go wrong:
- The pro-rata rule applies, exactly as in `04` — old pre-tax money makes the
  conversion mostly taxable.
- Paying the tax out of the converted money shrinks the conversion and, under
  59½, can attract the 10% additional tax on the part withheld.
- A converted amount withdrawn within **five tax years** attracts the 10% tax
  if the client is under 59½ — even though the conversion itself never does.

Rule: `RULE` — IRC §408A(d)(3), §408(d)(2), §408A(d)(3)(F).
Source: Module 10 §5.6, §8

Links to: → `04` → `11` → `06`

---

### How much should I convert?

The engine offers three targets, [index.html:1038](../index.html#L1038):

| Mode | What it does |
|---|---|
| Fixed amount | Converts the same figure every year, ignoring how much room exists |
| **Fill to a bracket** | Converts as much as fits below a rate ceiling, and nothing in a year with no room |
| **Fill to a Medicare tier** | Stops just under a surcharge cliff |

Output: filling to a ceiling converts the most that can be done at a known
rate. A fixed amount is the weakest of the three because it ignores the year.

The calculation has to **iterate**. The senior deduction phases out against
AGI, and the conversion is itself part of AGI, so a single pass overshoots —
by $10,643 in testing.

Rule: `PROJECTION`. The ceilings are `RULE`.

Links to: → `11` → `02`

---

### I am in the 12% bracket. I took an extra $10,000 and the tax was nearly double.

Output: the extra $10,000 did not just get taxed. It also dragged more Social
Security benefit into tax alongside it — up to **$1.85 of taxable income per
$1 withdrawn**.

So a client who believes they are paying 12% can be paying an effective rate
far above it. This is the real "tax torpedo", and it hits exactly the
middle-income retirees who think they are safe.

Rule: `RULE` — IRC §86(a)(2), the 85% tier.
Source: Module 14 §5.5, §6 Example 4

Links to: → `06` → `07`

---

### I want to take my whole $1,000,000 out in one year at 65.

Output: allowed, and no 10% penalty at 65. But:

- most of it lands in the top brackets
- 85% of the Social Security benefit becomes taxable
- the net investment income tax can reach other income
- the Medicare surcharge jumps two years later, and a one-off sale like this
  **cannot be appealed**
- state tax may apply on top

Spreading the same money across several years is almost always cheaper. The
engine will show both if asked.

Rule: `PROJECTION` for the decision. Consequences are `RULE`.
Source: Module 09 §7, §8

Links to: → `11` → `06` → `02`

---

### I am 60 and retired. I want to take only what stays in a low bracket.

Output: this is the same move as a bracket-filling conversion, and it is the
correct default. Take enough to use up the cheap brackets, leave the rest to
keep growing.

Rule: `PROJECTION`. Bracket ceilings are `RULE`.
Source: Module 10 §6 Example 4

Links to: → `02`

---

### Under 59½ — what actually costs 10%?

The engine does **not** model any of this. `§72(t)` appears nowhere in it
(Module 10 §5.1 case 16, recorded as not applied). So every case below is a
documentation answer, not something the projection will show.

| Situation | 10% extra tax? |
|---|---|
| Left the job in or after the year turning **55**, money still in **that employer's plan** | No |
| Same, but rolled to an IRA first | **Yes** — the exception is lost |
| Permanently disabled | No |
| Unreimbursed medical above the AGI floor | No |
| **Hardship withdrawal** | **Yes** — hardship is permission to withdraw, not a penalty exception |
| Emergency withdrawal at 45, no exception | Yes |
| Inherited account | No |

Rule: `RULE` — IRC §72(t)(1) and the §72(t)(2) exceptions.
Source: Module 10 §5.1 case 16 · Module 37 §5.4

Missing: the Rule of 55, hardship treatment, plan-loan offsets and net
unrealised appreciation are **not covered anywhere in Modules 07–10**. They
are a documentation gap, not only an engine gap.

Links to: → `16` → `04`

---

### I have a 401(k) loan and I am leaving my job.

Inputs: loan balance $30,000 · date of separation · age

Output: if it is not repaid, the outstanding balance becomes a taxable
distribution. Under 59½ with no exception, the 10% applies on top.

There is a rollover window — until the tax return due date including
extensions — to put the offset amount into an IRA and undo it. Most people
do not know it exists.

Rule: `RULE` — IRC §72(p), §402(c)(3)(C).
Source: not covered in Modules 07–10. Gap.

Links to: → `16`

---

### My 401(k) is full of my own employer's stock.

Inputs: stock market value $100,000 · plan cost basis $30,000

Output: there is a route where only the $30,000 basis is ordinary income now
and the $70,000 growth is taxed later at capital gain rates instead. It needs
a lump-sum distribution of the whole plan balance in one tax year after a
triggering event.

Executed wrongly it is simply lost, and the whole $100,000 becomes ordinary
income. The difference is large enough to be worth specialist advice.

Rule: `RULE` — IRC §402(e)(4).
Source: not covered in Modules 07–10. Gap.

Links to: → `13` (this stock gets no basis step-up)

---

### I left my job and want to move the old 401(k) without paying tax.

Inputs: old plan balance $400,000 · where it goes

Output: a **direct** trustee-to-trustee transfer to an IRA or a new employer
plan costs nothing now — no income tax, no 10%.

But the destination matters later, and most people are not told:

| Moved to | Consequence |
|---|---|
| A new employer's **plan** | stays out of the pro-rata pot; a backdoor Roth still works |
| A **traditional IRA** | creates pre-tax IRA money that poisons every future backdoor Roth |

It also destroys the Rule of 55 on that money, permanently.

Rule: `RULE` — IRC §402(c), §401(a)(31).
Source: Module 08 §5.6, §8

Links to: → `04` → `16`

---

### The 401(k) sent the cheque to me instead, and kept 20%.

Inputs: distribution $100,000 · withheld $20,000 · received $80,000

```
To roll the full $100,000 over, the client must deposit $100,000
  — the $80,000 received
  — PLUS $20,000 found from their own pocket
Within 60 days.

The $20,000 comes back as a refund the following year, not now.
Miss the 60 days, and the shortfall is a taxable distribution
  plus 10% if under 59.5.
```

Output: a paperwork mistake turns into a tax bill. Always ask for a direct
transfer — never a cheque made out to the client.

Rule: `RULE` — IRC §3405(c) 20% mandatory withholding; §402(c)(3) 60-day limit.
Source: gap — not covered in Modules 07–10.

Links to: → `16`

---

### Should I be using the Roth 401(k) instead of the traditional one?

Inputs: current rate · expected retirement rate · years to retirement ·
expected pre-tax balance at the forced-withdrawal age · heirs' rate

Output: it is not only a rate comparison. Three things push toward Roth that
clients rarely weigh:

- Roth balances are **not** subject to lifetime forced withdrawals, so they do
  not feed the snowball in `07`
- Roth money does not raise provisional income, so it does not drag Social
  Security into tax or lift the Medicare surcharge
- A Roth inherited by a child costs them nothing; a pre-tax account costs them
  ordinary income at their own peak-earning rate

The single strongest argument is the surviving spouse. A widow on single
brackets with a large pre-tax balance is the worst combination in the system.

Rule: `RULE` — IRC §402A; SECURE 2.0 §325.
Source: Module 07 §7, §9 · Module 10 §5.5, §7

Links to: → `07` → `11` → `13` → `06`
