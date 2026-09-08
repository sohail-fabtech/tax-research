# Cases and scenarios — start here

Real client situations, short, in plain English. One question per case.

The full legal reference is
[docs/ROADMAP-TO-AGE-90-DOCUMENTATION.md](../docs/ROADMAP-TO-AGE-90-DOCUMENTATION.md)
— 41 modules, 12,033 lines. Every case here points back to the module that
proves it. You should not need to open it.

---

## The chain

Every file is one link. The whole picture is this sentence:

```
Tax savings → Deploy capital → Grow wealth → Retirement
    → Distribute wealth → Protect assets → Leave a legacy
```

Tax savings are not money to spend. They are capital to deploy. That is the
idea the picture exists to sell.

```
01 Income  ──► 02 Taxes ──► 14 Deploy the savings into 7 buckets
   │              │                    │
   │              ▼                    ▼
   │         03 Expenses          04 Contributions ──► 05 Growth
   │                                                        │
   └────────────────────────────────────────────────────────┤
                                                            ▼
                                   RETIREMENT ──► 06 Social Security
                                                  07 Forced withdrawals
                                                  11 Medicare surcharge
                                                  12 Distributions
                                                        │
                                                        ▼
                                                  13 Estate → heirs

  Running alongside, all the way through:
      08 Insurance      09 Property      10 K-1 and business losses
      16 Events that redirect any of it
```

---

## Which file answers the question

| The client asks | File |
|---|---|
| "What do I earn, and when does it stop?" | [01](01-INCOME.md) |
| "What is my tax?" | [02](02-TAXES.md) |
| "What do I spend? What does care cost?" | [03](03-LIVING-EXPENSES.md) |
| "How much can I put in?" | [04](04-RETIREMENT-CONTRIBUTIONS.md) |
| "What does it grow at? What if the market drops?" | [05](05-INVESTMENT-GROWTH.md) |
| "62 or 70? What does my widow get?" | [06](06-SOCIAL-SECURITY.md) |
| "When am I forced to take money out?" | [07](07-RMD.md) |
| "Is the policy income really tax-free?" | [08](08-INSURANCE-CASH-VALUE.md) |
| "My rental made a loss. Can I use it?" | [09](09-REAL-ESTATE.md) |
| **"My K-1 came back with a loss. Now what?"** | **[10](10-K1-AND-BUSINESS-LOSSES.md)** |
| "Why did my Medicare premium jump?" | [11](11-MEDICARE-AND-IRMAA.md) |
| "Which account do I spend first? Should I convert?" | [12](12-DISTRIBUTIONS-AND-ROTH-CONVERSION.md) |
| "What do my children actually keep?" | [13](13-ESTATE-AND-HEIRS.md) |
| "Where does the $272K go?" | [14](14-DWC-AND-SEVEN-BUCKETS.md) |
| "What happens at each age?" | [15](15-AGE-JOURNEY.md) |
| "What if I get divorced / sell / die / get sick?" | [16](16-EVENTS-THAT-CHANGE-THE-PLAN.md) |
| "Do the numbers on the picture add up?" | [17](17-IMAGE-NUMBER-CHECK.md) |

Every case ends with **`Links to:`**. Follow those rather than reading a file
end to end — that is how one situation connects to the next.

---

## Reading a case

```
### The client's actual question

Inputs:      what you need to answer it
What happens: the working, in numbers
Output:      the answer
Rule:        the law, if there is one
Source:      where to check it
Missing:     what we would need and do not have
Links to:    what this touches next
```

---

## Government rule, or our assumption?

Never blur these. The picture itself says the software must not decide
eligibility or calculate savings — the adviser owns those numbers.

| Label | Meaning |
|---|---|
| `RULE` | Real law. Always carries a citation. |
| `PROJECTION` | Our own arithmetic. Not law. |
| `ADVISOR` | The adviser supplies it — the $188,000, the 20%, the bucket splits. |
| `ASSUMPTION` | A growth or product guess — 7% returns, 5.5% credited rate, care costs. |

**A number with no citation is never `RULE`.**

---

## The picture, as a contract

| | |
|---|---|
| Formula | `Net Tax Savings + DWC % × Qualified Deduction Base` |
| Dials | 20% · $188,000 net savings · $272K deployable |
| Phases | Contribution (now → retirement) · Distribution + Legacy (retirement → 90+) |
| Buckets | Liquidity 10 · 401(k)/Roth 25 · Insurance 20 · Real estate 25 · Market/opportunity 10 · Legacy 7 · Disability/LTC 3 |
| Bottom four | $11.3M at retirement · $18.7M distributed to 100 · $15.4M legacy at 100 · 82% tax-free target |

Milestones: 42 Foundation · 45 Protection · 50 Acceleration ·
55 Multiplication · 62 Retirement · 70 Distribution · 80 Preservation ·
90 Legacy · 100 Legacy continuation.

**Three things to know before quoting any of it.** Full working in
[17](17-IMAGE-NUMBER-CHECK.md) and [14](14-DWC-AND-SEVEN-BUCKETS.md):

1. The picture, the front end and the documented method use **three different
   formulas**. The terms "Deployable Wealth Capital", "DWC" and "qualified
   deduction base" appear **zero times** in the 12,033-line reference document.
2. The picture shows **seven** buckets. The documentation and the software both
   have **six** — Market / Opportunity Capital does not exist in either.
3. **82% tax-free income cannot be derived from anything on the picture.** Do
   not reverse-engineer a number to match it.

The picture also says the phases run to "Age 90+" and then prints three
age-100 figures. Always name the age when quoting one.

---

## Where these cases came from

1. **The 41 modules' own Case Registers and Edge Cases.** Already enumerated,
   already cited. The main source.
2. **`old-chat.txt`** — 20 real 401(k) cases, translated from Roman Urdu and
   re-checked against the modules. Where the two disagreed, the module won.
3. **Advisor videos**, used only to confirm which situations clients actually
   raise — the Medicare cliff after a conversion, the widow's penalty, the
   forced-withdrawal snowball, 62 versus 70. **No figure comes from a video and
   no video appears in a `Source:` line.**

---

## What is written down but not built

Found while writing these files. Each is recorded in the case file that covers
it, so nobody rediscovers them from a client's question:

- The seven buckets never reach net worth — `dwcTotal` is computed and left out
  of the estate calculation entirely → [14](14-DWC-AND-SEVEN-BUCKETS.md)
- Suspended losses are computed and never displayed. A fully blocked $250,000
  K-1 loss looks identical on screen to no loss at all →
  [10](10-K1-AND-BUSINESS-LOSSES.md)
- The Joint and Last Survivor table is missing, so a client with a much younger
  spouse is shown too large a forced withdrawal → [07](07-RMD.md)
- The Roth catch-up test reads current-year income instead of prior-year wages
  → [04](04-RETIREMENT-CONTRIBUTIONS.md)
- `§72(t)` is not modelled at all, so no early-withdrawal penalty ever appears
  → [12](12-DISTRIBUTIONS-AND-ROTH-CONVERSION.md)
- The Disability/LTC bucket compounds like an investment and never pays for
  care → [03](03-LIVING-EXPENSES.md)
- The `DWC% × base` term is dropped in any year a strategy costs more than it
  saves → [14](14-DWC-AND-SEVEN-BUCKETS.md)
- 59½, 65, 67 and the forced-withdrawal age are missing from the milestone
  strip → [15](15-AGE-JOURNEY.md)

Documentation gaps, not just software gaps — **not covered anywhere in the 41
modules**: the Rule of 55, hardship withdrawals, 401(k) loan offsets, net
unrealised appreciation on employer stock, and cancellation of debt on an
underwater property.
