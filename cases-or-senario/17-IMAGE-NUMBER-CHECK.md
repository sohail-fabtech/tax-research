# 17 — Checking the picture's own numbers

Every number printed on the roadmap picture, checked against the engine.
Three answers only: **derives**, **needs an input the picture does not show**, or **cannot be derived at all**.

Full working: [09-WORKED-EXAMPLE.md](../09-WORKED-EXAMPLE.md) §4.

---

## The formula card

### $188,000 savings and 20% become $272K. Where did $272K come from?

Inputs: net tax savings $188,000 · DWC 20% · qualified deduction base — not shown

```
188,000 + 0.20 × QDB = 272,000
        0.20 × QDB   =  84,000
              QDB    = 420,000
```

Output: **derives.** The picture is internally correct.

Missing: the $420,000 qualified deduction base is never printed. Anyone
re-checking the card cannot see where the extra $84,000 came from.

Rule: none. `ADVISOR` — the adviser supplies all three numbers.
Source: picture formula card · [index.html:1050](../index.html#L1050)

Links to: → `14` (this is the number every bucket is a slice of)

---

## The nine milestone cards

### Age 42 shows $1.76M in year one, but only $272K was deployed.

Output: **needs an input the picture does not show.** $1.76M at the first
milestone means the client already had roughly $1.5M before the plan
started. The picture shows no starting capital.

The engine seeds two buckets from existing money — cash on hand into
liquidity, current real estate value into real estate
([index.html:1060](../index.html#L1060)). Those two inputs are what the
picture is hiding.

Missing: opening cash, opening real estate value, opening retirement balances.

Links to: → `14` (seeding) → `05` (what it grows at)

---

### Ages 45, 50 and 55 do not sit on any single growth curve.

Fitting one rate to 45 / 50 / 55 / 62 at the same time leaves **$1.37M** of
total error, and it misses in a consistent direction — the picture runs high
early:

| Age | Picture | Best single curve at 3.48% real | Gap |
|---|---|---|---|
| 45 | $3.05M | $2.81M | −$0.24M |
| 50 | $5.25M | $4.82M | −$0.43M |
| 55 | $7.90M | $7.20M | −$0.70M |
| 62 | $11.30M | $11.30M | $0.00M |

Output: **cannot be derived.** Ages 45, 50 and 55 were placed for visual
progression. Only 42 and 62 are anchored.

Rule: none. `PROJECTION`.
Source: [09-WORKED-EXAMPLE.md](../09-WORKED-EXAMPLE.md) §4 Finding 3

Links to: → `15` (the age journey uses these same ages)

---

### The two ends of the picture imply two different returns, and they are the wrong way round.

```
Age 42 → 62   $1.76M + $272K/yr → $11.3M over 20 years   =  3.57% real
Age 62 → 100  $11.3M − $18.7M paid out → $15.4M          ≈  4.70% real
```

Output: **derives, but it is inconsistent.** A portfolio normally gets *more*
conservative at retirement, not less. Either the accumulation number is too
low or the distribution number is too high. Both cannot be right under one
asset allocation.

Missing: one glide path that both phases are derived from.

Links to: → `05` (return assumptions) → `12` (distributions)

---

## The bottom four

### $18.7M of distributions over 38 years is $492,000 a year.

The client's stated lifestyle in the worked example is $180,000 a year. The
engine, drawing only what the client needs, produces **$8.7M** of total
distributions — less than half.

Output: **derives arithmetically, but the label does not say what it counts.**
$492K/yr is only reachable if the figure is gross withdrawals — including
required distributions that get taxed and immediately reinvested — rather
than money actually spent.

Missing: gross or net. The two differ by more than 2× here.

Links to: → `07` (required distributions inflate gross withdrawals)
          → `12` (withdrawal order)

---

### Bucket percentages do not match bucket dollars.

Picture labels: 10 / 25 / 20 / 25 / 10 / 7 / 3
Picture dollars work out to: 10.4 / 29.2 / 19.0 / 27.4 / 8.1 / 3.8 / 2.0

Output: **derives, and it is correct behaviour.** The percentages are shares
*of the annual contribution*. The dollars are *ending balances*. They drift
apart because each bucket compounds at a different rate — retirement at 7%,
insurance at 5.5%, real estate at 5%, the rest at 5.75%.

The card does not say this, so it reads as an error to anyone checking it.
Relabel as "% of annual contribution".

Source: [index.html:1057](../index.html#L1057)

Links to: → `14`

---

### Tax-free income target 82%.

Output: **cannot be derived from anything on the picture.**

Two inputs are missing and neither is guessable:
- what counts as tax-free income — Roth withdrawals, policy loans, return of
  basis, municipal interest, the untaxed part of Social Security? Each
  choice moves the answer by a lot.
- over what period — one retirement year, or all years 62 to 100?

There is no such output anywhere in the engine. Do not reverse-engineer a
number to fit 82%.

Links to: → `12` (which income sources are actually tax-free)
          → `08` (policy loans are only tax-free while the policy stays alive)

---

## Age 90 or age 100?

The picture is titled "To Age 90+" and then prints three numbers at age 100.
The engine offers 90 or 100 as a choice ([index.html:510](../index.html#L510)).

Every figure quoted from this picture must name its age. "$15.4M legacy" is
an **age-100** figure. The age-90 figure is $14.8M.

Links to: → `00` → `15`
