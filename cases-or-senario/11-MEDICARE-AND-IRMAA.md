# 11 — Medicare and the income surcharge

The surcharge is set by the client's income from **two years earlier**, and it
is a cliff, not a slope. That combination is what makes it dangerous.

---

### Which year's income sets my premium?

```
Income in 2026   →   sets the premium for 2028
```

Output: a client retiring at 65 pays their first premium based on their last
big working year. Nothing about their current income matters.

Rule: `RULE` — Social Security Act §1839(i); 20 CFR §418.1010.
Source: Module 16 §5.5 · [index.html:866](../index.html#L866)

Links to: → `12` (conversions done at 63 land at 65)

---

### I was one dollar over the line and my premium jumped for the whole year.

2026 tiers, per person:

| Income two years back (single / joint) | Part B | Part D extra |
|---|---|---|
| below $109,000 / $218,000 | $202.90 | — |
| $109,000 / $218,000 | $284.10 | $14.50 |
| $137,000 / $274,000 | $405.80 | $37.50 |
| $171,000 / $342,000 | $527.50 | $60.40 |
| $205,000 / $410,000 | $649.20 | $83.30 |
| $500,000 / $750,000 | $689.90 | $91.00 |

```
One dollar over the first line:
  (284.10 - 202.90 + 14.50) x 12  =  $1,148  per person, per year
  A couple both enrolled           =  $2,297
```

Output: there is no phase-in. One dollar moves the entire premium to the next
tier for twelve months. Stopping just under a line is worth the whole tier.

Rule: `RULE` — Social Security Act §1839(i).
Source: Module 16 §5.2, §5.4, §6 Example 1, §8

Links to: → `12` (this is why the engine offers a "fill to a tier" mode)

---

### We converted $120,000 to Roth at 64 and got a Medicare bill at 66.

Output: the conversion is added to income in the conversion year, and the
surcharge follows two years later. For a couple, both spouses pay it.

The conversion may still be right. But the surcharge is a real cost of it and
belongs in the comparison.

Rule: `RULE` — Social Security Act §1839(i), §1860D-13(a)(7).
Source: Module 16 §5.2, §5.5, §6 Example 2

Links to: → `12` → `07`

---

### I sold a rental for a big gain. Can I appeal the surcharge?

Output: **No.** There is a closed list of seven life-changing events, and a
one-time gain is not on it. A loss taken at the taxpayer's own direction is
expressly excluded.

| Qualifies | Does not qualify |
|---|---|
| Marriage, divorce, death of a spouse | Selling a property |
| **Work stoppage or reduction** | Selling a business |
| Loss of income-producing property (not by choice) | A Roth conversion |
| Loss or reduction of a pension | A large forced withdrawal |
| Employer settlement payment | |

Output: the client pays it. The only defences are before the fact — spreading
the sale over instalments, or timing it against the tier boundaries.

Rule: `RULE` — 20 CFR §418.1205; Form SSA-44.
Source: Module 16 §5.6, §6 Example 4, §8

Links to: → `09` → `16` → `10`

---

### I retired and my income collapsed, but the premium is based on my old salary.

Output: this one **can** be fixed. Work stoppage or reduction of hours is on
the qualifying list. File Form SSA-44 with evidence of the retirement date and
ask for a new determination rather than waiting two years.

Rule: `RULE` — 20 CFR §418.1205(d), §418.1201.
Source: Module 16 §5.6, §6 Example 3

Missing: **not implemented in the engine** (Module 16 §9). A client who
retires is shown the surcharge anyway.

Links to: → `16`

---

### I am delaying Social Security to 70 but I am on Medicare. Why am I billed directly?

Output: the protection that caps a premium increase against the annual
cost-of-living rise only applies to people who have a benefit in payment and
are not paying a surcharge. A client deferring to 70 has no benefit to deduct
it from, so they pay the full increase in cash.

Rule: `RULE` — Social Security Act §1839(f).
Source: Module 15 §5.4, §8

Links to: → `06`

---

### I am taxed on more Social Security than actually reached my bank account.

Output: the premium and any surcharge are withheld from the benefit, but the
tax is worked out on the **gross** benefit before that deduction. The client
is taxed on money they never saw.

The premiums are at least a qualifying medical expense, which matters in a
high-care year.

Rule: `RULE` — IRC §86 on the gross benefit; Social Security Act §1839.
Source: Module 15 §5.3, §7, §8

Note: the engine shows premiums as an expense rather than netting them from
the benefit. Presentation only — the tax result is right, because §86 uses the
gross figure either way.

Links to: → `03` → `06`

---

### Will Medicare pay for my mother's nursing home?

```
Days  1-20     covered
Days 21-100    $217 a day coinsurance
Day  101+      nothing
```

Output: **Medicare does not pay for long-term care.** It pays for short skilled
nursing after a qualifying hospital stay. Custodial care — the kind that lasts
years — is entirely on the household.

Worked example: $17,360 of coinsurance plus $220,000 of custodial care =
**$237,360** borne by the family.

Rule: `RULE` — Social Security Act §1813.
Source: Module 15 §5.2, §6 Examples 2–3 · Module 33 §8

Links to: → `03` → `08` → `14` (the bucket that was meant to fund this)

---

### We are separated but not divorced and want to file separately.

Output: this is the worst filing position in the system. The Social Security
taxation thresholds drop to **zero** unless the couple lived apart for the
whole year, and the surcharge schedule is compressed savagely.

Rule: `RULE` — IRC §86(c); Social Security Act §1839(i).
Source: Module 14 §5.3, §8 · Module 16 §4, §8

Links to: → `16` → `02`
