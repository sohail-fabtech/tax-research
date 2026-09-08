# 02 — Tax

2026 figures. Every one taken from the frozen constants in
[index.html:294](../index.html#L294), which were checked against the primary
source.

---

### How is the tax actually worked out?

Output: by walking the brackets, slice by slice. **Never** by multiplying
income by the marginal rate. The comment in the engine says so, because it is
the classic mistake:

```js
/* --- the bracket walk. Never multiply by the marginal rate --- */
```

2026 married filing jointly:

| Up to | Rate |
|---|---|
| $24,800 | 10% |
| $100,800 | 12% |
| $211,400 | 22% |
| $403,550 | 24% |
| $512,450 | 32% |
| $768,700 | 35% |
| above | 37% |

Single brackets are roughly **half** the width at every step. That single fact
is what makes the widow's penalty in `13` so expensive.

Rule: `RULE` — IRC §1; Rev. Proc. 2025-32.
Source: Module 01 §5 · [index.html:759](../index.html#L759)

Links to: → `13` → `12`

---

### What comes off before the brackets?

```
Standard deduction   $32,200 joint  /  $16,100 single  /  $24,150 head of household
Age 65 addition      $1,650 per person joint  /  $2,050 single
Senior deduction     $6,000 per person aged 65+
```

Output: a married couple both over 65 start with $32,200 + $3,300 + $12,000
before a dollar is taxed.

**The senior deduction expires after 2028.** In 2029 a couple relying on it
sees taxable income rise $12,000 with no change in their income at all. Any
projection running to age 90 must switch it off.

Rule: `RULE` — IRC §63(c),(f), §151(d)(5)(C); P.L. 119-21.
Source: Module 02 §5 · [index.html:317](../index.html#L317)

Links to: → `16` → `15`

---

### Capital gains are taxed on top of ordinary income, not beside it.

```
Married, 2026
  0%   up to $98,900
  15%  to $613,700
  20%  above
```

Output: ordinary income fills the space first, and gains stack on top. So a
client with low ordinary income can realise a substantial gain at **0%** — and
the same gain in a high-income year costs 20% plus the 3.8% investment income
tax.

Two ceilings the plain table does not show:
- Unrecaptured depreciation on property is capped at **25%** — the lower of 25%
  and the client's own rate, not a flat 25%.
- Collectibles are capped at 28%.

Rule: `RULE` — IRC §1(h).
Source: Module 24 §5.2 · [index.html:768](../index.html#L768)

Links to: → `09` → `12`

---

### What sits on top of the ordinary tax?

| | Rate | Starts at (joint) | Indexed? |
|---|---|---|---|
| Net investment income tax | 3.8% | $250,000 | **No — frozen since 2013** |
| Additional Medicare tax | 0.9% | $250,000 | **No** |
| Social Security tax on wages | 6.2% | up to $184,500 of wages | yes |
| Medicare tax on wages | 1.45% | no ceiling | — |

Output: the two frozen thresholds catch more households every year. Over a
long projection they behave like a slow tax rise that nobody voted for.

Rule: `RULE` — IRC §1411, §3101(b)(2), §3121.
Source: Modules 04–06 · [index.html:333](../index.html#L333)

Links to: → `05` → `11`

---

### The 20% business deduction.

```
2026 threshold   $403,500 joint  /  $201,750 other
Fully phased at  $553,500 joint  /  $276,750 other
```

Output: below the threshold it is a clean 20% of business income. Above it,
two things happen at once — a wage and property limit applies, and **service
businesses lose it entirely**.

Service means health, law, accounting, consulting, financial services,
performing arts, athletics. Engineering and architecture are specifically
**not** service businesses, which surprises people every time.

Rule: `RULE` — IRC §199A(b),(d)(2); §199A(i) minimum.
Source: Module 17 §5.2–§5.5 · [index.html:325](../index.html#L325)

Links to: → `10` → `01`

---

### State tax.

Output: nine states take nothing. California, New York, Oregon and Hawaii take
up to roughly 13% on top of everything federal.

For a client near the top bracket, moving state is worth more than most tax
strategies in this document combined — and it also changes the estate tax
position in `13`.

Rule: `RULE` — state statute.
Source: [index.html:399](../index.html#L399)

Links to: → `13` → `16`

---

### The alternative minimum tax got worse in 2026.

```
Exemption          $140,200 joint
Phases out from    $1,000,000
Phase-out rate     50%   — DOUBLED from 25%
```

Output: the exemption now disappears twice as fast. A client with large
deductions or incentive stock options who was previously clear of it may not
be any more.

Rule: `RULE` — IRC §55–§59; P.L. 119-21 §70107.
Source: Module 01 · [index.html:376](../index.html#L376)

Links to: → `16`

---

### The state and local deduction is on a timetable.

```
2026    $40,400, phasing down 30% above $505,000, never below $10,000
2030    reverts to $10,000 flat
```

Output: this is a **schedule written into law**, not an inflation-indexed
figure. A projection must step it forward year by year and then drop it in
2030.

Rule: `RULE` — IRC §164(b)(7); P.L. 119-21.
Source: Module 02 · [index.html:370](../index.html#L370)

Links to: → `16`

---

### Capital losses.

```
Offset gains in full
Then $3,000 a year against ordinary income
The rest carries forward, indefinitely
```

Output: a large loss can take decades to use at $3,000 a year. It does not
expire — but it dies with the client, so it is worth far more used during
life.

Rule: `RULE` — IRC §1211(b), §1212(b).
Source: Module 24 §5.3 · [index.html:387](../index.html#L387)

Links to: → `10` → `13`
