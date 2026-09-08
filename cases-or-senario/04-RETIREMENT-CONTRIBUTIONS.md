# 04 — Putting money in

2026 limits, and the places clients lose money by getting them wrong.

---

### I turn 61 this year. Can I add the $11,250 catch-up on top of the $8,000 one?

Inputs: age reached during the calendar year · base deferral $24,500

```
Age 50-59    24,500 +  8,000  =  $32,500
Age 60-63    24,500 + 11,250  =  $35,750     NOT 24,500 + 8,000 + 11,250
Age 64+      24,500 +  8,000  =  $32,500
```

Output: **the bigger catch-up replaces the smaller one. It does not stack.**
$35,750, not $43,750.

Rule: `RULE` — IRC §414(v)(2)(E)(i); SECURE 2.0 §109.
Source: Module 07 §5.3, §8 · [index.html:828](../index.html#L828)

Links to: → `01`

---

### I turn 64 this year and my payroll election is still set to last year's number.

```
Age 63    $35,750
Age 64    $32,500      capacity falls $3,250
```

Output: the window is ages 60, 61, 62 and 63 only. At 64 it closes and the
client over-defers unless payroll is changed.

Rule: `RULE` — IRC §414(v)(2)(E)(i).
Source: Module 07 §5.3, §8

Links to: → `02`

---

### I earn over $150,000 and my catch-up is suddenly not deductible.

Inputs: **prior calendar-year FICA wages from that same employer** · catch-up amount

Output: above the wage line, the catch-up must go into the Roth side. No
deduction now; tax-free later instead.

Three things people get wrong about the test:
- It looks at the **prior** year, not this year.
- It looks at **wages from that one employer**, not total income.
- Self-employment income is not FICA wages, so it does not trigger it.

Rule: `RULE` — IRC §414(v)(7); SECURE 2.0 §603; Notice 2023-62. Live for tax
years beginning after 31 December 2025.
Source: Module 07 §5.4, §6 Example 2 · [index.html:365](../index.html#L365)

**The engine gets this wrong.** It tests current-year income instead of
prior-year wages from the sponsor (Module 07 §5.1 case 8, §12).

Links to: → `12` (Roth balances escape forced withdrawals entirely)

---

### I have a salaried job and an unrelated side business. How much in total?

```
One   §402(g) limit  $24,500  shared across every plan   — follows the PERSON
One   §415(c) limit  $72,000  per unrelated employer     — follows the PLAN
```

Output: the client cannot defer $24,500 twice. But the $72,000 total-additions
cap applies separately to each unrelated employer, so a side business plan can
take a lot more through profit sharing.

Rule: `RULE` — IRC §402(g)(1), §415(c)(1)(A); §414(b),(c),(m),(o) decide what
"unrelated" means.
Source: Module 07 §5.5, §6 Examples 4–5, §8

Links to: → `10` (how the side business is structured changes this)

---

### I over-deferred across two employers and noticed in February.

Output: fix it by **15 April**. If it is not corrected, the excess is taxed
twice — once in the year it went in, again when it comes out.

Neither employer can see the other's plan, so this is the client's problem to
catch.

Rule: `RULE` — IRC §402(g)(2).
Source: Module 07 §8

Links to: → `02`

---

### My income is too high for a Roth IRA, so I will contribute non-deductibly and convert.

Inputs: contribution $7,500 · existing traditional/SEP/SIMPLE IRA balances $200,000

```
Basis fraction   7,500 ÷ 207,500  =  3.6%
Tax-free part                        $271
Taxable part                       $7,229     — 96.4% of the conversion
```

Output: the conversion is **not** tax-free. Every traditional, SEP and SIMPLE
IRA the client owns is treated as one pot on 31 December, so old pre-tax money
poisons the new contribution.

The fix, where the employer plan accepts it: roll the pre-tax IRA money **into
the 401(k)** first. Plan balances are counted out of the pot; IRA balances
are counted in.

Rule: `RULE` — IRC §408(o), §408A(d)(3), §408(d)(2).
Source: Module 08 §5.6, §6 Example 4, §8

Links to: → `12`

---

### I made non-deductible contributions for years and cannot find the paperwork.

Inputs: non-deductible contributions $75,000 · total balance $600,000

```
Basis fraction  75,000 ÷ 600,000  =  12.5% of every future withdrawal tax-free
```

Output: that 12.5% is worth real money for the rest of the client's life — but
only if Form 8606 was filed to establish it. Without the filing history the
client can end up paying tax twice on the same money.

Rule: `RULE` — IRC §408(o), §408(d)(2); Form 8606.
Source: Module 08 §6 Example 5, §8

Links to: → `07` (basis reduces the taxable part of every forced withdrawal)
          → `13`

---

### My spouse has no workplace plan and I do. Can we still deduct?

```
Spouse covered by a plan        $129,000 - $149,000
Spouse NOT covered              $242,000 - $252,000
```

Output: two completely different ranges in the same household. The uncovered
spouse can often still deduct when the covered one cannot.

Rule: `RULE` — IRC §219(g), §219(g)(7).
Source: Module 08 §5.3, §6 Example 3

Links to: → `02`

---

### What the engine actually contributes

[index.html:1115](../index.html#L1115) caps the contribution at the **lowest**
of three things:

```js
const total = Math.min(want, lim, Math.max(0, w2));
```

what the client asked for · the legal limit · their wages.

So a client with a large business profit but small W-2 wages is capped by the
wages, and contributions stop entirely at retirement.

Links to: → `01` → `14` (the "401(k) bucket" ignores all of these limits)
