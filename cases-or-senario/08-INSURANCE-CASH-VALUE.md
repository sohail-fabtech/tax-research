# 08 — Life insurance cash value

The roadmap puts 20% of every deployed dollar here, and the plan is that the
client borrows from the policy in retirement and pays no tax on it. That works
— right up until it does not, and the failure is expensive.

---

### I want to draw tax-free income from the policy every year in retirement.

Inputs: cash value · premiums paid (basis) · annual loan · loan interest rate ·
not a MEC · policy stays in force

Output: loans from a policy that stays in force are not income. The money does
not enter AGI, so it does not drag Social Security into tax and does not feed
the Medicare surcharge. That is the whole attraction.

**It only holds while the policy is alive.** Read the next case before relying
on it.

Rule: `RULE` — IRC §72(e), §7702, §101(a). The income amount itself is
`PROJECTION`.
Source: Module 30 §5.5, §7 · [06-INSURANCE-CASH-VALUE.md](../06-INSURANCE-CASH-VALUE.md) §6

Links to: → `12` → `06` → `11` → `03`

---

### The loan kept compounding and one year the policy lapsed. Now I owe tax on money I spent years ago.

Inputs: cash value $520,000 · loans outstanding $480,000 · basis $300,000

```
Deemed distribution of the full cash value    $520,000
Less basis                                    $300,000
Taxable gain                                  $220,000
Tax at 24%                                     $52,800
Cash actually received                              $0
```

Output: **a $52,800 bill and nothing to pay it with.** The income stream also
stops, and the death benefit the family was counting on is gone.

The interest is what does it. Unpaid loan interest capitalises into the balance
and compounds, so the loan grows faster than the cash value in the later years
when the cost of insurance is also climbing.

Rule: `RULE` — IRC §72(e).
Source: Module 30 §5.5, §6 Example 5, §8

The engine does model this — [index.html:1584](../index.html#L1584) tests every
year and writes a note when it happens. Do not switch that warning off.

Links to: → `02` → `11` (a spike like this sets the surcharge two years later)
          → `13` → `12`

---

### I funded it fast to build cash value quickly.

Inputs: cash value $400,000 · basis $250,000 · $100,000 taken

```
Ordinary policy   loan of $100,000                   $0 taxable
A MEC             $100,000 comes out gain-first     $100,000 taxable
                  plus 10% if under 59.5             $10,000
                  total                              $42,000
```

Output: paying premiums too fast in the first seven years turns the contract
into a MEC. Every distribution then comes out gain-first and is taxable from
the first dollar. The status is permanent and cannot be undone.

Rule: `RULE` — IRC §7702A(b) seven-pay test; §72(e)(10); §72(v).
Source: Module 30 §5.4, §6 Example 4

Links to: → `14` (over-funding is exactly what a large insurance bucket
            encourages)

---

### The illustration showed 7%. What if it credits 4%?

Output: everything downstream moves. Lower crediting means less cash value,
which means the loan reaches the cash value sooner, which brings the lapse
case above forward by years.

The engine defaults to a credited rate of 5.5% ([index.html:1057](../index.html#L1057)),
and it is an input the client can set to whatever the illustration said. That
is a decision to check, not a default to accept.

Rule: `ASSUMPTION`. The illustration ceiling (AG 49-B) is an insurance
regulator's limit on what may be shown, not tax law.
Source: [06-INSURANCE-CASH-VALUE.md](../06-INSURANCE-CASH-VALUE.md) §4, §5

Links to: → `05` → `14`

---

### I am 84 and the internal charges keep climbing. Will this survive to 90?

Output: the cost of insurance is charged on the gap between the death benefit
and the cash value, and it rises steeply with age. A policy with no premium
going in and a loan going out is being drained from both ends.

This has to be tested year by year to age 90, not assumed.

Rule: `ASSUMPTION` for the test. `RULE` — IRC §72(e) — only for the
consequence.
Source: [06-INSURANCE-CASH-VALUE.md](../06-INSURANCE-CASH-VALUE.md) §4, §6

Links to: → `15`

---

### I own a $4,000,000 policy on my own life. Is the death benefit in my estate?

Inputs: death benefit $4,000,000 · other estate $13,000,000 · who owns it

```
Owned personally     $17,000,000 estate  →  about $800,000 of estate tax
Owned by a trust from the start          →  $0
```

Output: the death benefit is free of **income** tax either way. Whether it is
free of **estate** tax depends entirely on who holds the rights to it — to
change the beneficiary, surrender it, borrow against it or assign it.

Rule: `RULE` — IRC §2042; §101(a)(1) for the income side.
Source: Module 30 §5.3, §6 Example 1

Links to: → `13` → `14`

---

### I moved the policy into a trust two years ago. Does that fix it?

Output: **No — not yet.** A policy transferred within three years of death is
pulled back into the estate in full. In the worked example a transfer 26 months
before death put the whole $4,000,000 back and cost $800,000.

The trust should **buy** the policy at the outset rather than receive it later.

Rule: `RULE` — IRC §2035(a).
Source: Module 30 §5.3, §6 Example 2, §8

Links to: → `13`

---

### Can I at least deduct the policy loan interest?

Output: **No.** Policy loan interest is generally not deductible. The engine
does not apply this rule at all (Module 30 §12), so it is a documentation
answer only.

Rule: `RULE` — IRC §264.
Source: Module 30 §5.5, §8

Links to: → `02`

---

### I want out. How much of the surrender is taxable?

Output: everything above the premiums paid, and it is **ordinary income**, not
capital gain. Any outstanding loan counts as money received, which is how
people end up with a taxable amount larger than the cheque.

Rule: `RULE` — IRC §72(e).
Source: Module 30 §5.5

Links to: → `02` → `11`

---

## Long-term care

### What does care actually cost, and for how long?

Output: there is **no government figure for this.** No federal agency publishes
an authoritative cost schedule. The roadmap uses $110,000–$135,000 a year
against a national median private room near $129,575, and inflates it at a
healthcare rate above general inflation.

Every part of that is an adviser's choice and should be shown as one.

Rule: `ASSUMPTION` — Module 33 says so explicitly.
Source: Module 33 §5.5, §10 · [index.html:999](../index.html#L999)

Links to: → `03` → `11` → `13`

---

### How much of my $7,500 long-term care premium can I deduct?

2026 caps, per person, by age at year end:

| Age | Deductible |
|---|---|
| 40 or under | $500 |
| 41 – 50 | $930 |
| 51 – 60 | $1,860 |
| 61 – 70 | $4,960 |
| 71 and over | $6,200 |

Worked example, ages 58 and 72: $1,860 + $6,200 counted, **$3,640 not
deductible at any level** — and even that only counts toward the medical
deduction, which has its own income floor.

Rule: `RULE` — IRC §213(d)(10), §7702B(b); Rev. Proc. 2025-32.
Source: Module 32 §5.4, §6 Example 4 · [index.html:987](../index.html#L987)

Links to: → `02` → `03`

---

### My policy pays $500 a day but the care costs less. Is the extra taxable?

```
Received       $500 x 365    =  $182,500
2026 limit     $430 a day    =  $156,950
Taxable                          $25,550
```

Output: only on an indemnity or per-diem contract. A reimbursement contract
that pays actual cost has no excess to tax.

Rule: `RULE` — IRC §7702B(d); Rev. Proc. 2025-32.
Source: Module 33 §5.3, §5.4, §6 Example 1

Links to: → `02` → `11`

---

### The care year wrecks my income. Should I convert that year?

Output: often **yes**, and it is counter-intuitive. A huge medical deduction
can drop taxable income far enough that converting into the space costs very
little.

Worked example: $151,000 of expenses against $190,000 of AGI left $136,750
deductible and federal tax of $4,891 instead of about $17,222. Converting
$57,550 into that room cost $10,140 — an effective **17.6%**.

Rule: `RULE` — IRC §213 creates the room; §408A governs the conversion. The
decision is `PROJECTION`.
Source: Module 32 §6 Example 3, §9

Links to: → `12` → `13` (it also protects the surviving spouse)
