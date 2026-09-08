# 06 — Social Security

---

### Should I take it at 62, at 67, or at 70?

Inputs: date of birth (sets full retirement age) · benefit at full age · claiming month

For someone whose full age is 67:

| Claim at | Monthly benefit |
|---|---|
| 62 | about **70%** |
| 67 | 100% |
| 70 | about **124%** |

Output: the difference between the two ends is roughly **77% more per month**
for waiting eight years. It is permanent, and it carries into the survivor
benefit.

Rule: `RULE` — Social Security Act §202(q), §202(w); 20 CFR §404.313.
Source: Module 11 §5.4, §6 Example 1 · [index.html:807](../index.html#L807)

Links to: → `12` (waiting frees up the cheapest conversion years)
          → `13` (the widow keeps the larger of the two benefits)

---

### My adviser's number for waiting to 70 is smaller than I expected.

Output: cost-of-living increases accrue from the year the client turns **62**,
not from the year they claim. Someone who waits to 70 has already banked eight
years of increases before the first cheque.

Modelling it from the claiming age instead understates a client who waits by
roughly **24% for life** — and biases the whole system against waiting.

Rule: `RULE` — Social Security Act §215(i).
Source: Module 11 §5.5, §6 Example 2 (recorded defect D1, now fixed)
· [index.html:341](../index.html#L341)

Links to: → `15`

---

### I claimed at 63 and I am working part-time. They stopped my cheques.

Inputs: earned wages · claiming age · months below full age this year

```
2026 exempt amount            $24,480 a year
Withheld                      $1 for every $2 above it
In the year full age is reached   $65,160, and $1 for every $3
From full age onward              nothing is withheld, at any income
```

Output: benefits are held back, not taken. Ask the second question below.

Rule: `RULE` — Social Security Act §203(f).
Source: Module 11 §5.6, §6 Example 3 · [index.html:342](../index.html#L342)

Links to: → `01`

---

### Is that withheld money gone forever?

Output: **No.** At full retirement age the benefit is recalculated upward to
give credit for the months that were withheld. Most clients are told only the
first half of this and claim later than they needed to.

Rule: `RULE` — Social Security Act §203; 20 CFR §404.430.
Source: Module 11 §5.6, §8 (recorded defect D2)

Links to: → `15`

---

### I have $400,000 of IRA and portfolio income. Will that cut my early benefit?

Output: **No.** The earnings test counts **earned** income only — wages and
self-employment. Pensions, IRA withdrawals, interest, dividends, rent, capital
gains and K-1 income are all ignored by it.

They still affect how much of the benefit is **taxed**. Two different tests,
constantly confused.

Rule: `RULE` — Social Security Act §203(f).
Source: Module 11 §5.6, §8

Links to: → `07` → `09` → `10`

---

### My wife never worked. What can she draw on my record?

Output: up to **50%** of the husband's benefit at her full retirement age,
reduced if she claims earlier. Waiting past her full age adds **nothing** to a
spousal benefit — the delayed credits that grow a worker's own benefit do not
apply here.

Rule: `RULE` — Social Security Act §202(b), (c), (q).
Source: Module 12 §5.2, §6 Examples 1–2 · [index.html:791](../index.html#L791)

Links to: → `13`

---

### I have my own small benefit and a bigger spousal one. Do I get both?

Output: **No. Benefits never add.** The client receives the larger of the two,
not the sum. This is the single most common misunderstanding in the whole
topic.

Rule: `RULE` — Social Security Act §202(k); POMS RS 00615.020.
Source: Module 12 §5.1 case 6, §6 Example 2, §8

Links to: → `13` (the widow keeps one benefit, not two)

---

### Can I take just the spousal benefit now and let my own grow to 70?

Output: **No, that door is closed.** It survives only for people born on or
before 1 January 1954. Everyone else is deemed to have filed for both and
receives the larger.

Rule: `RULE` — Social Security Act §202(r); Bipartisan Budget Act 2015.
Source: Module 12 §5.3, §8

Links to: → `12` (the workaround people used for the conversion window is gone)

---

### My husband died. What do I get now?

Inputs: his benefit · the age he claimed · her age · her **survivor** full age

Output: the widow steps up to the larger of the two benefits, adjusted for
when she claims. Three things make this harder than it looks:

- The survivor full retirement age is **not** the same as the retirement full
  age. Different table.
- If he claimed early at 62, that reduction follows her.
- A separate ceiling caps what she can receive based on what he was actually
  drawing.
- At 60 the survivor benefit is about **71.5%**.

Rule: `RULE` — Social Security Act §202(e), (f); POMS RS 00615.320, RS 00615.301.
Source: Module 12 §5.4, §5.5, §6 Examples 3–4 (recorded defect D3)
· [index.html:953](../index.html#L953)

Links to: → `13`

---

### I am a widow at 60. Must I choose one benefit permanently?

Output: **No** — and this is valuable. A survivor benefit and the client's own
retirement benefit are not subject to deemed filing against each other. She
can take one now and switch to the other later when it has grown.

Rule: `RULE` — Social Security Act §202(e), (f).
Source: Module 12 §5.6, §6 Example 5

Links to: → `12`

---

### My income barely changed after he died, but my tax bill jumped.

Output: this is the widow's penalty, and it is three separate things landing
at once:

| | Married | Alone |
|---|---|---|
| Brackets | wide | roughly **half** the width |
| Social Security taxed above | $32,000 / $44,000 | **$25,000 / $34,000** |
| Net investment income tax above | $250,000 | **$200,000** |
| Medicare surcharge starts at | $218,000 | **$109,000** |

Worked example: gross income **down 12.0%**, federal tax **up 29.5%**, cash
after tax **down 16.9%**.

Rule: `RULE` — IRC §1(j)(2), §86(c), §1411; Social Security Act §1839(i).
Source: Module 35 §5.3, Example 1 · Module 12 §6 Example 3

Links to: → `13` (this is the strongest argument for converting early)
          → `11` → `12`

---

### I divorced after 12 years. Can I claim on my ex-husband's record?

Output: **Yes** — married ten years or more, currently unmarried, both at
least 62. After two years divorced she can claim even if he has not filed.

It costs him nothing and does not reduce his benefit or his new wife's. He is
not notified.

Rule: `RULE` — Social Security Act §202(b)(2), (c)(2).
Source: Module 12 §4, §5.1 cases 9–10, §8

Missing: **not implemented in the engine.**

Links to: → `16`

---

### I am 63 and widowed. Will remarrying cost me the survivor benefit?

Output: **No.** Remarriage at or after 60 does not end a survivor benefit.
Before 60 it does.

Rule: `RULE` — Social Security Act §202(e), (f).
Source: Module 12 §8

Links to: → `13` → `16`

---

### I am a retired teacher and was told my benefit would be cut.

Output: **not any more.** The provisions that reduced benefits for people with
non-covered government pensions were repealed for months after December 2023.

Rule: `RULE` — P.L. 118-273, Social Security Fairness Act.
Source: Module 11 §4, §8 · Module 12 §4, §9

Links to: → `01` (a government pension no longer reduces the benefit)

---

### How much of my benefit is actually taxed, and why does it get worse every year?

```
Provisional income = AGI + tax-exempt interest + half the benefit

Married      up to $32,000    none taxed
             $32,000-$44,000  up to 50% taxed
             above $44,000    up to 85% taxed
```

Output: **these thresholds have never been indexed.** They were set in 1983
and 1993 and have not moved since. Every year of inflation pulls more
households over them, so the same real income is taxed more heavily over a
long projection.

Rule: `RULE` — IRC §86; P.L. 98-21; P.L. 103-66.
Source: Module 14 §5.2–§5.4, §8 · [index.html:344](../index.html#L344)

Links to: → `07` → `12`

---

### I moved everything into municipal bonds to keep my benefit untaxed.

Output: **it does not work.** Tax-exempt interest is added back into
provisional income by name. It is exempt from income tax and not exempt here —
and it counts for the Medicare surcharge too.

Rule: `RULE` — IRC §86(b)(2)(B); 20 CFR §418.1010.
Source: Module 14 §7, §8

Links to: → `11` → `05`
