# 01 — Money coming in

The first link in the chain. Everything downstream — tax, contributions,
deployable capital — is sized off this.

---

### What counts as income while the client is still working?

```
w2 = (client W-2 + spouse W-2 + bonus) x (1 + income growth)^years
business profit x (1 + income growth)^years
other income    x (1 + income growth)^years
```

Output: everything grows at one rate. Default 3% on the Expected scenario, 2%
Conservative, 4% Accelerated.

Rule: `ASSUMPTION` — one growth rate for every income source.
Source: [index.html:1099](../index.html#L1099)

Missing: a client whose bonus swings, or whose business is lumpy, is not
modelled. One rate is applied to all of it.

Links to: → `02` → `04` → `05`

---

### What happens the year the client retires?

Output: W-2 and business income stop **completely** at the retirement age.
There is no wind-down and no final part-year.

If part-time work was selected, that income starts instead and runs until the
age the client set.

Rule: `PROJECTION`.
Source: [index.html:1099](../index.html#L1099)

Links to: → `06` (part-time earnings can trigger the earnings test)
          → `12` (this is where the conversion window opens)

---

### My spouse died. What happens to their salary in the projection?

Output: the spouse's W-2 drops to zero from that year. Their Social Security
does not simply disappear — the survivor keeps the larger of the two benefits,
which is a different calculation entirely.

Rule: `PROJECTION` for the wage. `RULE` for the benefit.
Source: [index.html:1100](../index.html#L1100)

Links to: → `06` → `13`

---

### Which income actually affects what?

Three different tests use three different definitions. Clients mix them up
constantly.

| Test | What it counts |
|---|---|
| Social Security **earnings test** | earned income only — wages, self-employment |
| Social Security **taxation** | AGI + tax-exempt interest + half the benefit |
| **Medicare surcharge** | AGI + tax-exempt interest, from **two years ago** |

So an IRA withdrawal does not reduce an early Social Security cheque, but it
does increase how much of that cheque is taxed, and it does raise the Medicare
premium two years later.

Rule: `RULE` — Social Security Act §203(f); IRC §86; Social Security Act §1839(i).
Source: Module 11 §5.6 · Module 14 §5.2 · Module 16 §5.5

Links to: → `06` → `11` → `07`

---

### Business structure changes the answer.

Output: the same profit taxed through an S corporation, a partnership or a
sole trade produces different employment tax, different retirement
contribution room, and — critically — a different basis result if the business
ever makes a loss.

The engine asks for the business type explicitly. It is never inferred, and
service businesses are treated differently from product businesses for the
20% business deduction.

Rule: `RULE` — IRC §1402; §199A(d)(2).
Source: Module 19 §5.2 · Module 17 §5.4 · [index.html:325](../index.html#L325)

Links to: → `10` → `04` → `02`
