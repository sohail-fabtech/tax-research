# 07 — Forced withdrawals (RMD)

At a certain age the government stops letting money sit in a pre-tax account.
The client must take a set amount out every year and pay ordinary income tax
on it, whether they need the money or not.

---

### When do mine start — 73 or 75?

Inputs: year of birth. Nothing else.

| Born | First forced withdrawal at |
|---|---|
| Before 1951 | 72 |
| 1951 – 1959 | **73** |
| 1960 or later | **75** |

Output: one age, fixed by birth year. There is no overlap and no election.

Rule: `RULE` — IRC §401(a)(9)(C)(v); SECURE 2.0 §107.
Source: Module 09 §4 · [index.html:825](../index.html#L825)

Links to: → `12` (the years before this age are the cheapest to convert)
          → `15`

---

### How is the amount worked out?

Inputs: balance on 31 December last year · age reached this year

```
1,000,000 ÷ 24.6  =  $40,650     (age 75)
```

The divisor comes from the Uniform Lifetime Table. The age used is the age
**reached during the year**, not the age on the withdrawal date — a birthday
on 30 December gives the same divisor as 2 January.

Rule: `RULE` — IRC §401(a)(9); Treas. Reg. §1.401(a)(9)-9(c); Pub 590-B Table III.
Source: Module 09 §6 Example 1 · [index.html:826](../index.html#L826)

Links to: → `02`

---

### My balance is barely moving but the forced amount keeps climbing.

Inputs: $1,200,000 at 73 · 6% growth · every withdrawal taken

| Age | Divisor | Forced out | Balance after | Share of balance |
|---|---|---|---|---|
| 73 | 26.5 | $45,283 | $1,224,000 | 3.77% |
| 75 | 24.6 | $50,673 | $1,267,640 | 4.07% |
| 80 | 20.2 | $65,988 | $1,342,986 | 4.95% |
| 85 | 16.0 | $84,362 | $1,341,361 | 6.25% |
| 90 | 12.2 | $103,190 | $1,225,069 | 8.20% |

Output: forced income **more than doubles** between 73 and 90 while the
balance ends up almost where it started. Nothing about the client changed —
the divisor shrank.

This is what clients mean by the "tax torpedo". The balance looks safe, so
nobody sees it coming.

Rule: `RULE` for the divisors. `ASSUMPTION` for the 6% growth.
Source: Module 09 §6 Example 4

Links to: → `06` (it drags more Social Security into tax)
          → `11` (it pushes the Medicare surcharge up)
          → `12` (converting early is the only real defence)

---

### Can I put the first one off until 1 April next year?

Inputs: $850,000 at 73 · divisor 26.5 · account grows 6% meanwhile

```
Age-73 amount, pushed into next year      $32,075
Age-74 amount, on the grown balance       $35,333
Taxable next year                         $67,409
Had the first been taken on time          $35,333
Extra income crammed into one year        $32,075
```

Output: yes, it is allowed. It is usually a mistake. Two years of forced
income land in one bracket, and that year also sets the Medicare surcharge
two years later.

It is right only when this year's rate is genuinely higher than next year's.

Rule: `RULE` — IRC §401(a)(9)(C).
Source: Module 09 §5.4, §6 Example 3

Missing: the engine does not model the April deadline or the two-in-one-year
outcome (Module 09 §5.1 cases 6–7).

Links to: → `11` → `02`

---

### I have three old 401(k)s and two IRAs. Can I take it all from one?

| Account type | Can be combined? |
|---|---|
| Traditional / SEP / SIMPLE IRA | Yes — total them, take from any one |
| 403(b) contracts | Only with each other |
| **Each 401(k)** | **No — each one separately** |
| **Each 457(b)** | **No — each one separately** |

Output: taking the whole amount from one 401(k) leaves a shortfall in every
other plan, and **each shortfall carries its own penalty**.

Rule: `RULE` — Treas. Reg. §1.401(a)(9)-8.
Source: Module 09 §5.6, §8

Links to: → `12`

---

### I took nothing out. What now?

Inputs: required amount $42,000

```
Penalty at 25%                        $10,500
If corrected within two years, 10%     $4,200
```

Output: an excise tax on the amount that should have come out. It can be
waived for reasonable error with Form 5329.

Rule: `RULE` — IRC §4974.
Source: Module 09 §5.10, §6 Example 6

Missing: the engine assumes the client always complies, so it never shows
this (Module 09 §5.1 case 17).

Links to: → `02`

---

### I am 74 and still working. Do I have to start?

Output: only for the plan of the employer the client **still works for**, and
only if the plan document allows the delay.

Two traps that catch exactly the people most confident about this:
- A client owning **more than 5%** of that business cannot use it at all.
- It **never** applies to any IRA — traditional, SEP or SIMPLE — no matter
  who the client works for.

Old employers' plans keep their own schedule regardless.

Rule: `RULE` — IRC §401(a)(9)(C)(i)(II).
Source: Module 09 §5.7, §8

Links to: → `10` (business owners are usually the ones asking)

---

### My wife is 14 years younger and she is my only beneficiary.

Output: the forced amount **drops**. A different table applies where the sole
beneficiary spouse is more than ten years younger.

The spouse must be the sole beneficiary for the **entire year**. A contingent
beneficiary is fine; a second primary beneficiary destroys it.

Rule: `RULE` — Treas. Reg. §1.401(a)(9)-9(d), Joint and Last Survivor Table.
Source: Module 09 §5.5, §8

**The engine gets this wrong.** The Joint and Last Survivor Table is not
implemented ([index.html:826](../index.html#L826) always uses the Uniform
table), so this household is shown a forced withdrawal that is **too large**,
and therefore too much tax, for the rest of the projection
(Module 09 §5.1 case 8, §12).

Links to: → `13` → `12`

---

### I give to charity anyway. Can I send it straight from the IRA?

Inputs: age 76 · balance $900,000 · $30,000 to charity

```
Required amount   900,000 ÷ 23.7  =  $37,975
Sent to charity                      $30,000   (never enters income)
Taxable remainder                     $7,975
```

Output: AGI rises by $7,975 instead of $37,975. The $30,000 never appears in
income at all, so it does not feed Social Security taxation and does not feed
the Medicare surcharge. A deduction cannot do that.

2026 limit: **$111,000** per person.

Three ways it gets spoiled:
- **It cannot go to a donor advised fund** or a supporting organisation. This
  is the most common failure, because the client already has the fund.
- It must come from an IRA, not a 401(k).
- Age 70½, which is earlier than the forced-withdrawal age.

Rule: `RULE` — IRC §408(d)(8); §408(d)(8)(B)(i) excludes donor advised funds.
Source: Module 09 §5.8, §6 Example 5 · [index.html:353](../index.html#L353)

Links to: → `11` → `06` → `13`

---

### I inherited my father's IRA. How fast must I empty it?

Output: depends on when he died relative to his own start date.

| He died | Years 1–9 | Year 10 |
|---|---|---|
| **Before** his start date | nothing required | must be empty |
| **On or after** his start date | annual amounts **are** required | must be empty |

The second row catches people. They take nothing for nine years, then face
both a penalty and a single enormous taxable year.

A surviving spouse has extra options a child does not.

Rule: `RULE` — IRC §401(a)(9)(B),(H); SECURE Act; SECURE 2.0 §327.
Source: Module 09 §5.9, §8

Missing: Module 09 flags that the second row rests on the regulations rather
than an explicit Publication 590-B statement — confirm for a specific account.

Links to: → `13` (the heir also gets no basis step-up on this money)
