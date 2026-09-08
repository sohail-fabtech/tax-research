# 05 — Growth

---

### What rates does the projection use?

| | Conservative | Expected | Accelerated |
|---|---|---|---|
| Income growth | 2.0% | 3.0% | 4.0% |
| Retirement accounts | 5.0% | **7.0%** | 9.0% |
| Real estate | 3.5% | **5.0%** | 6.5% |
| Inflation | 0% | **3%** | 0% |
| Strategy effectiveness | 80% | 100% | 125% |

Taxable accounts grow at 5.75% and insurance cash value at the policy's
credited rate, default 5.5%.

Output: every one of these is an `ASSUMPTION`. None has a government source
and none should be presented as a fact.

Source: [index.html:988](../index.html#L988), [index.html:1002](../index.html#L1002)

**Two of the three scenarios use 0% inflation.** A 48-year projection at 0%
inflation is not conservative — it silently overstates purchasing power at the
end by a wide margin. Module 39 flags the same problem in the backend.

Links to: → `14` → `17`

---

### Effectiveness above 100% — what is that?

Output: the Accelerated scenario multiplies the tax savings by **125%**. That
is an assertion that the strategies deliver a quarter more than the adviser's
own estimate.

Module 39 §8 says so in plain terms: it is an assumption of outperformance,
not a computation. It should never be the default shown to a client.

Rule: `ASSUMPTION`.
Source: Module 39 §5.4, §8

Links to: → `14`

---

### Why is everything computed in future dollars and shown in today's?

Output: because tax brackets rise with inflation but several thresholds are
frozen in law and never move.

```
Bracket ceilings          indexed every year
Social Security taxation  $32,000 / $44,000  — frozen since 1983 and 1993
Net investment income     $250,000           — frozen since 2013
The $25,000 rental allowance                 — frozen since 1986
```

Shrinking the dollars first would compare shrunken income against frozen
limits and understate the tax in every later year. The engine computes
nominal throughout and deflates once at the end
([index.html:1632](../index.html#L1632)).

Rule: `RULE` for which thresholds are frozen. `PROJECTION` for the method.
Source: Module 00 · Module 14 §8

Links to: → `06` → `02`

---

### Do contributions get a full year of growth?

```js
pretax = pretax * (1 + r) + contribution * Math.pow(1 + r, 0.5)
```

Output: no — contributions get **half a year**, because they arrive spread
across the year rather than on 1 January. Giving them a full year would
overstate the balance a little every year, and compound that error for
fifty.

Rule: `PROJECTION`.
Source: [index.html:1548](../index.html#L1548)

Links to: → `04`

---

### What does the advisory fee do?

```
retirement return = stated return - advisory fee
bucket returns    = stated return - admin fee - cost of investment
```

Output: fees come straight off the return before anything compounds. Over
forty-eight years a 1% fee is not 1% of the outcome — it is a large multiple
of that.

Rule: `ASSUMPTION`.
Source: [index.html:1002](../index.html#L1002), [index.html:1056](../index.html#L1056)

Links to: → `14`

---

### A bad market year right at retirement.

Output: the projection applies **one flat rate every year**. It does not model
a crash, a recovery, or the order returns arrive in.

That matters, because a poor return in the first years of drawing down does
far more damage than the same return later — the client is selling assets to
live on while they are cheap.

Rule: `ASSUMPTION` — and a limitation worth stating to any client who asks
"what if the market drops?"

Missing: no sequence-of-returns modelling, no volatility, no Monte Carlo. The
answer to that question is currently "the model cannot show you".

Links to: → `12` → `16`
