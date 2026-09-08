# Client Cases

## MONEY COMING IN

### What counts as income while the client is still working?

```
w2 = (client W-2 + spouse W-2 + bonus) x (1 + income growth)^years
business profit x (1 + income growth)^years
other income    x (1 + income growth)^years
```

Output: everything grows at one rate. Default 3% on the Expected scenario, 2%
Conservative, 4% Accelerated.

Rule: an assumption — one growth rate for every income source.

Missing: a client whose bonus swings, or whose business is lumpy, is not
modelled. One rate is applied to all of it.

**Also touches:** Tax · Putting money in · Growth

---

### What happens the year the client retires?

Output: W-2 and business income stop **completely** at the retirement age.
There is no wind-down and no final part-year.

If part-time work was selected, that income starts instead and runs until the
age the client set.

Rule: our own calculation. Not law.

**Also touches:** Social Security (part-time earnings can trigger the earnings test) · Taking money out (this is where the conversion window opens)

---

### My spouse died. What happens to their salary in the projection?

Output: the spouse's W-2 drops to zero from that year. Their Social Security
does not simply disappear — the survivor keeps the larger of the two benefits,
which is a different calculation entirely.

Rule: our own calculation for the wage. a real rule for the benefit.

**Also touches:** Social Security · Estate and family

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

Rule: Social Security Act §203(f); IRC §86; Social Security Act §1839(i).

**Also touches:** Social Security · Medicare · Forced withdrawals

---

### Business structure changes the answer.

Output: the same profit taxed through an S corporation, a partnership or a
sole trade produces different employment tax, different retirement
contribution room, and — critically — a different basis result if the business
ever makes a loss.

The engine asks for the business type explicitly. It is never inferred, and
service businesses are treated differently from product businesses for the
20% business deduction.

Rule: IRC §1402; §199A(d)(2).

**Also touches:** K-1 and business losses · Putting money in · Tax

---

## TAX

### How is the tax actually worked out?

Output: by walking the brackets, slice by slice. **Never** by multiplying
income by the marginal rate. The comment in the engine says so, because it is
the classic mistake.

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
is what makes the widow's penalty in the Estate and family cases so expensive.

Rule: IRC §1; Rev. Proc. 2025-32.

**Also touches:** Estate and family · Taking money out

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

Rule: IRC §63(c),(f), §151(d)(5)(C); P.L. 119-21.

**Also touches:** Events · Age by age

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

Rule: IRC §1(h).

**Also touches:** Property · Taking money out

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

Rule: IRC §1411, §3101(b)(2), §3121.

**Also touches:** Growth · Medicare

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

Rule: IRC §199A(b),(d)(2); §199A(i) minimum.

**Also touches:** K-1 and business losses · Money coming in

---

### State tax.

Output: nine states take nothing. California, New York, Oregon and Hawaii take
up to roughly 13% on top of everything federal.

For a client near the top bracket, moving state is worth more than most tax
strategies in this document combined — and it also changes the estate tax
position in the Estate and family cases.

Rule: state statute.

**Also touches:** Estate and family · Events

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

Rule: IRC §55–§59; P.L. 119-21 §70107.

**Also touches:** Events

---

### The state and local deduction is on a timetable.

```
2026    $40,400, phasing down 30% above $505,000, never below $10,000
2030    reverts to $10,000 flat
```

Output: this is a **schedule written into law**, not an inflation-indexed
figure. A projection must step it forward year by year and then drop it in
2030.

Rule: IRC §164(b)(7); P.L. 119-21.

**Also touches:** Events

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

Rule: IRC §1211(b), §1212(b).

**Also touches:** K-1 and business losses · Estate and family

---

## SPENDING AND CARE

---

### How does spending change through the projection?

```
while working    monthly spend x 12 x (1 + inflation)^years
after retiring   the same, x 85%
after a spouse   the same, x 75%
   dies
```

Output: two step-downs, both adjustable. The 75% survivor factor is the more
important of the two — the house and its running costs do not halve when one
person dies, but the income often does.

Rule: an assumption — both factors.

**Also touches:** Estate and family (this is half of the widow's problem; tax is the other half)

---

### Why is medical inflated separately?

```
general spending   2.5% a year
medical spending   5.0% a year
```

Output: healthcare runs at roughly double general inflation, so over a 48-year
projection it becomes a far larger share of spending than it starts as.

Real evidence for the gap: the 2026 Part B premium rose **9.7%** while the
Social Security increase was **2.8%**. The premium is taken out of the benefit,
so the client's net cheque fell in a year their benefit rose.

Rule: an assumption for the rates. The 2026 figures are a real rule.

**Also touches:** Medicare · Social Security

---

### Long-term care starts. What happens to the plan?

Inputs: annual care cost · start age · duration · care inflation

Output: a cost of roughly $110,000–$135,000 a year is added on top of ordinary
spending, and it inflates at the medical rate, not the general one.

**No government body publishes an authoritative cost for this.** Every figure here is the adviser's choice.

Rule: an assumption. Not law.

**Also touches:** Life insurance · Medicare · Estate and family

---

### Which bucket pays for the care?

Output: **none of them.** The care cost is charged to general expenses, and the
plan then funds it in the normal withdrawal order — taxable, then pre-tax,
then Roth.

The "Disability / LTC Protection" bucket on the picture, funded at 3% a year,
is never touched. It sits there compounding at an investment rate while the care it exists for is paid from somewhere else.

Rule: our own calculation — defect.

**Also touches:** The seven buckets · Taking money out

---

### The care year makes my tax bill collapse. Is that right?

Output: yes, and it is worth planning around. Medical costs above the income
floor are deductible, and a large care year can wipe out most taxable income.

Worked example: $151,000 of expenses against $190,000 of AGI left $136,750
deductible, and federal tax of $4,891 instead of about $17,222.

That empty space is the cheapest Roth conversion room the client will ever
have — see the Taking money out cases.

Rule: IRC §213(a).

**Also touches:** Taking money out · Life insurance

---

### What happens when the money runs out?

Output: the engine drains taxable, then pre-tax, then Roth. If all three are
empty and there is still a shortfall, it writes a note naming the year and the
amount:

> "Age 87: accounts run out. The plan is short by $42,000 this year."

It does not silently continue with a negative balance. That note is the single
most important line in any projection and should never be scrolled past.

Rule: our own calculation. Not law.

**Also touches:** Taking money out · Growth

---

## PUTTING MONEY IN

### I turn 61 this year. Can I add the $11,250 catch-up on top of the $8,000 one?

Inputs: age reached during the calendar year · base deferral $24,500

```
Age 50-59    24,500 +  8,000  =  $32,500
Age 60-63    24,500 + 11,250  =  $35,750     NOT 24,500 + 8,000 + 11,250
Age 64+      24,500 +  8,000  =  $32,500
```

Output: **the bigger catch-up replaces the smaller one. It does not stack.**
$35,750, not $43,750.

Rule: IRC §414(v)(2)(E)(i); SECURE 2.0 §109.

**Also touches:** Money coming in

---

### I turn 64 this year and my payroll election is still set to last year's number.

```
Age 63    $35,750
Age 64    $32,500      capacity falls $3,250
```

Output: the window is ages 60, 61, 62 and 63 only. At 64 it closes and the
client over-defers unless payroll is changed.

Rule: IRC §414(v)(2)(E)(i).

**Also touches:** Tax

---

### I earn over $150,000 and my catch-up is suddenly not deductible.

Inputs: **prior calendar-year FICA wages from that same employer** · catch-up amount

Output: above the wage line, the catch-up must go into the Roth side. No
deduction now; tax-free later instead.

Three things people get wrong about the test:
- It looks at the **prior** year, not this year.
- It looks at **wages from that one employer**, not total income.
- Self-employment income is not FICA wages, so it does not trigger it.

Rule: IRC §414(v)(7); SECURE 2.0 §603; Notice 2023-62. Live for tax
years beginning after 31 December 2025.

**The engine gets this wrong.** It tests current-year income instead of
prior-year wages from the sponsor.

**Also touches:** Taking money out (Roth balances escape forced withdrawals entirely)

---

### I have a salaried job and an unrelated side business. How much in total?

```
One   §402(g) limit  $24,500  shared across every plan   — follows the PERSON
One   §415(c) limit  $72,000  per unrelated employer     — follows the PLAN
```

Output: the client cannot defer $24,500 twice. But the $72,000 total-additions
cap applies separately to each unrelated employer, so a side business plan can
take a lot more through profit sharing.

Rule: IRC §402(g)(1), §415(c)(1)(A); §414(b),(c),(m),(o) decide what
"unrelated" means.

**Also touches:** K-1 and business losses (how the side business is structured changes this)

---

### I over-deferred across two employers and noticed in February.

Output: fix it by **15 April**. If it is not corrected, the excess is taxed
twice — once in the year it went in, again when it comes out.

Neither employer can see the other's plan, so this is the client's problem to
catch.

Rule: IRC §402(g)(2).

**Also touches:** Tax

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

Rule: IRC §408(o), §408A(d)(3), §408(d)(2).

**Also touches:** Taking money out

---

### I made non-deductible contributions for years and cannot find the paperwork.

Inputs: non-deductible contributions $75,000 · total balance $600,000

```
Basis fraction  75,000 ÷ 600,000  =  12.5% of every future withdrawal tax-free
```

Output: that 12.5% is worth real money for the rest of the client's life — but
only if Form 8606 was filed to establish it. Without the filing history the
client can end up paying tax twice on the same money.

Rule: IRC §408(o), §408(d)(2); Form 8606.

**Also touches:** Forced withdrawals (basis reduces the taxable part of every forced withdrawal) · Estate and family

---

### My spouse has no workplace plan and I do. Can we still deduct?

```
Spouse covered by a plan        $129,000 - $149,000
Spouse NOT covered              $242,000 - $252,000
```

Output: two completely different ranges in the same household. The uncovered
spouse can often still deduct when the covered one cannot.

Rule: IRC §219(g), §219(g)(7).

**Also touches:** Tax

---

### What does the plan actually let me contribute?

The **lowest** of three things: what you asked for, the legal limit, and your salary.

So a client with a large business profit but small W-2 wages is capped by the
wages, and contributions stop entirely at retirement.

**Also touches:** Money coming in · The seven buckets (the 401k bucket ignores all of these limits)

---

## GROWTH

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

Output: every one of these is an assumption. None has a government source
and none should be presented as a fact.

**Two of the three scenarios use 0% inflation.** A 48-year projection at 0%
inflation is not conservative — it silently overstates purchasing power at the
end by a wide margin. The written method flags the same problem in the backend.

**Also touches:** The seven buckets · Checking the picture

---

### Effectiveness above 100% — what is that?

Output: the Accelerated scenario multiplies the tax savings by **125%**. That
is an assertion that the strategies deliver a quarter more than the adviser's
own estimate.

The written method says so in plain terms: it is an assumption of outperformance,
not a computation. It should never be the default shown to a client.

Rule: an assumption. Not law.

**Also touches:** The seven buckets

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
nominal throughout and deflates once at the end.

Rule: a real rule for which thresholds are frozen. our own calculation for the method.

**Also touches:** Social Security · Tax

---

### Do contributions get a full year of growth?

Contributions are given half a year of growth, not a full year.

Output: no — contributions get **half a year**, because they arrive spread
across the year rather than on 1 January. Giving them a full year would
overstate the balance a little every year, and compound that error for
fifty.

Rule: our own calculation. Not law.

**Also touches:** Putting money in

---

### What does the advisory fee do?

```
retirement return = stated return - advisory fee
bucket returns    = stated return - admin fee - cost of investment
```

Output: fees come straight off the return before anything compounds. Over
forty-eight years a 1% fee is not 1% of the outcome — it is a large multiple
of that.

Rule: an assumption. Not law.

**Also touches:** The seven buckets

---

### A bad market year right at retirement.

Output: the projection applies **one flat rate every year**. It does not model
a crash, a recovery, or the order returns arrive in.

That matters, because a poor return in the first years of drawing down does
far more damage than the same return later — the client is selling assets to
live on while they are cheap.

Rule: an assumption — and a limitation worth stating to any client who asks
"what if the market drops?"

Missing: no sequence-of-returns modelling, no volatility, no Monte Carlo. The
answer to that question is currently "the model cannot show you".

**Also touches:** Taking money out · Events

---

## SOCIAL SECURITY

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

Rule: Social Security Act §202(q), §202(w); 20 CFR §404.313.

**Also touches:** Taking money out (waiting frees up the cheapest conversion years) · Estate and family (the widow keeps the larger of the two benefits)

---

### My adviser's number for waiting to 70 is smaller than I expected.

Output: cost-of-living increases accrue from the year the client turns **62**,
not from the year they claim. Someone who waits to 70 has already banked eight
years of increases before the first cheque.

Modelling it from the claiming age instead understates a client who waits by
roughly **24% for life** — and biases the whole system against waiting.

Rule: Social Security Act §215(i).

**Also touches:** Age by age

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

Rule: Social Security Act §203(f).

**Also touches:** Money coming in

---

### Is that withheld money gone forever?

Output: **No.** At full retirement age the benefit is recalculated upward to
give credit for the months that were withheld. Most clients are told only the
first half of this and claim later than they needed to.

Rule: Social Security Act §203; 20 CFR §404.430.

**Also touches:** Age by age

---

### I have $400,000 of IRA and portfolio income. Will that cut my early benefit?

Output: **No.** The earnings test counts **earned** income only — wages and
self-employment. Pensions, IRA withdrawals, interest, dividends, rent, capital
gains and K-1 income are all ignored by it.

They still affect how much of the benefit is **taxed**. Two different tests,
constantly confused.

Rule: Social Security Act §203(f).

**Also touches:** Forced withdrawals · Property · K-1 and business losses

---

### My wife never worked. What can she draw on my record?

Output: up to **50%** of the husband's benefit at her full retirement age,
reduced if she claims earlier. Waiting past her full age adds **nothing** to a
spousal benefit — the delayed credits that grow a worker's own benefit do not
apply here.

Rule: Social Security Act §202(b), (c), (q).

**Also touches:** Estate and family

---

### I have my own small benefit and a bigger spousal one. Do I get both?

Output: **No. Benefits never add.** The client receives the larger of the two,
not the sum. This is the single most common misunderstanding in the whole
topic.

Rule: Social Security Act §202(k); POMS RS 00615.020.

**Also touches:** Estate and family (the widow keeps one benefit, not two)

---

### Can I take just the spousal benefit now and let my own grow to 70?

Output: **No, that door is closed.** It survives only for people born on or
before 1 January 1954. Everyone else is deemed to have filed for both and
receives the larger.

Rule: Social Security Act §202(r); Bipartisan Budget Act 2015.

**Also touches:** Taking money out (the workaround people used for the conversion window is gone)

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

Rule: Social Security Act §202(e), (f); POMS RS 00615.320, RS 00615.301.

**Also touches:** Estate and family

---

### I am a widow at 60. Must I choose one benefit permanently?

Output: **No** — and this is valuable. A survivor benefit and the client's own
retirement benefit are not subject to deemed filing against each other. She
can take one now and switch to the other later when it has grown.

Rule: Social Security Act §202(e), (f).

**Also touches:** Taking money out

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

Rule: IRC §1(j)(2), §86(c), §1411; Social Security Act §1839(i).

**Also touches:** Estate and family (this is the strongest argument for converting early) · Medicare · Taking money out

---

### I divorced after 12 years. Can I claim on my ex-husband's record?

Output: **Yes** — married ten years or more, currently unmarried, both at
least 62. After two years divorced she can claim even if he has not filed.

It costs him nothing and does not reduce his benefit or his new wife's. He is
not notified.

Rule: Social Security Act §202(b)(2), (c)(2).

Missing: **not implemented in the engine.**

**Also touches:** Events

---

### I am 63 and widowed. Will remarrying cost me the survivor benefit?

Output: **No.** Remarriage at or after 60 does not end a survivor benefit.
Before 60 it does.

Rule: Social Security Act §202(e), (f).

**Also touches:** Estate and family · Events

---

### I am a retired teacher and was told my benefit would be cut.

Output: **not any more.** The provisions that reduced benefits for people with
non-covered government pensions were repealed for months after December 2023.

Rule: P.L. 118-273, Social Security Fairness Act.

**Also touches:** Money coming in (a government pension no longer reduces the benefit)

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

Rule: IRC §86; P.L. 98-21; P.L. 103-66.

**Also touches:** Forced withdrawals · Taking money out

---

### I moved everything into municipal bonds to keep my benefit untaxed.

Output: **it does not work.** Tax-exempt interest is added back into
provisional income by name. It is exempt from income tax and not exempt here —
and it counts for the Medicare surcharge too.

Rule: IRC §86(b)(2)(B); 20 CFR §418.1010.

**Also touches:** Medicare · Growth

---

## FORCED WITHDRAWALS

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

Rule: IRC §401(a)(9)(C)(v); SECURE 2.0 §107.

**Also touches:** Taking money out (the years before this age are the cheapest to convert) · Age by age

---

### How is the amount worked out?

Inputs: balance on 31 December last year · age reached this year

```
1,000,000 ÷ 24.6  =  $40,650     (age 75)
```

The divisor comes from the Uniform Lifetime Table. The age used is the age
**reached during the year**, not the age on the withdrawal date — a birthday
on 30 December gives the same divisor as 2 January.

Rule: IRC §401(a)(9); Treas. Reg. §1.401(a)(9)-9(c); Pub 590-B Table III.

**Also touches:** Tax

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

Rule: a real rule for the divisors. an assumption for the 6% growth.

**Also touches:** Social Security (it drags more Social Security into tax) · Medicare (it pushes the Medicare surcharge up) · Taking money out (converting early is the only real defence)

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

Rule: IRC §401(a)(9)(C).

Missing: the engine does not model the April deadline or the two-in-one-year
outcome.

**Also touches:** Medicare · Tax

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

Rule: Treas. Reg. §1.401(a)(9)-8.

**Also touches:** Taking money out

---

### I took nothing out. What now?

Inputs: required amount $42,000

```
Penalty at 25%                        $10,500
If corrected within two years, 10%     $4,200
```

Output: an excise tax on the amount that should have come out. It can be
waived for reasonable error with Form 5329.

Rule: IRC §4974.

Missing: the engine assumes the client always complies, so it never shows
this.

**Also touches:** Tax

---

### I am 74 and still working. Do I have to start?

Output: only for the plan of the employer the client **still works for**, and
only if the plan document allows the delay.

Two traps that catch exactly the people most confident about this:
- A client owning **more than 5%** of that business cannot use it at all.
- It **never** applies to any IRA — traditional, SEP or SIMPLE — no matter
  who the client works for.

Old employers' plans keep their own schedule regardless.

Rule: IRC §401(a)(9)(C)(i)(II).

**Also touches:** K-1 and business losses (business owners are usually the ones asking)

---

### My wife is 14 years younger and she is my only beneficiary.

Output: the forced amount **drops**. A different table applies where the sole
beneficiary spouse is more than ten years younger.

The spouse must be the sole beneficiary for the **entire year**. A contingent
beneficiary is fine; a second primary beneficiary destroys it.

Rule: Treas. Reg. §1.401(a)(9)-9(d), Joint and Last Survivor Table.

**The engine gets this wrong.** The Joint and Last Survivor Table is not
implemented — the plan always uses the ordinary table — so this household is shown a forced withdrawal that is **too large**,
and therefore too much tax, for the rest of the projection.

**Also touches:** Estate and family · Taking money out

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

Rule: IRC §408(d)(8); §408(d)(8)(B)(i) excludes donor advised funds.

**Also touches:** Medicare · Social Security · Estate and family

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

Rule: IRC §401(a)(9)(B),(H); SECURE Act; SECURE 2.0 §327.

Missing: the written rules flag that the second row rests on the regulations rather
than an explicit Publication 590-B statement — confirm for a specific account.

**Also touches:** Estate and family (the heir also gets no basis step-up on this money)

---

## LIFE INSURANCE

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

Rule: IRC §72(e), §7702, §101(a). The income amount itself is
our own calculation.

**Also touches:** Taking money out · Social Security · Medicare · Spending and care

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

Rule: IRC §72(e).

The engine does model this. It tests every year and writes a note when it happens. Do not switch that warning off.

**Also touches:** Tax · Medicare (a spike like this sets the surcharge two years later) · Estate and family · Taking money out

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

Rule: IRC §7702A(b) seven-pay test; §72(e)(10); §72(v).

**Also touches:** The seven buckets (over-funding is exactly what a large insurance bucket encourages)

---

### The illustration showed 7%. What if it credits 4%?

Output: everything downstream moves. Lower crediting means less cash value,
which means the loan reaches the cash value sooner, which brings the lapse
case above forward by years.

The engine defaults to a credited rate of 5.5%, and it is an input the client can set to whatever the illustration said. That
is a decision to check, not a default to accept.

Rule: an assumption. The illustration ceiling (AG 49-B) is an insurance
regulator's limit on what may be shown, not tax law.

**Also touches:** Growth · The seven buckets

---

### I am 84 and the internal charges keep climbing. Will this survive to 90?

Output: the cost of insurance is charged on the gap between the death benefit
and the cash value, and it rises steeply with age. A policy with no premium
going in and a loan going out is being drained from both ends.

This has to be tested year by year to age 90, not assumed.

Rule: an assumption for the test. a real rule — IRC §72(e) — only for the
consequence.

**Also touches:** Age by age

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

Rule: IRC §2042; §101(a)(1) for the income side.

**Also touches:** Estate and family · The seven buckets

---

### I moved the policy into a trust two years ago. Does that fix it?

Output: **No — not yet.** A policy transferred within three years of death is
pulled back into the estate in full. In the worked example a transfer 26 months
before death put the whole $4,000,000 back and cost $800,000.

The trust should **buy** the policy at the outset rather than receive it later.

Rule: IRC §2035(a).

**Also touches:** Estate and family

---

### Can I at least deduct the policy loan interest?

Output: **No.** Policy loan interest is generally not deductible. The engine does not apply this rule at all, so this is a documentation answer only.

Rule: IRC §264.

**Also touches:** Tax

---

### I want out. How much of the surrender is taxable?

Output: everything above the premiums paid, and it is **ordinary income**, not
capital gain. Any outstanding loan counts as money received, which is how
people end up with a taxable amount larger than the cheque.

Rule: IRC §72(e).

**Also touches:** Tax · Medicare

---

## Long-term care

### What does care actually cost, and for how long?

Output: there is **no government figure for this.** No federal agency publishes
an authoritative cost schedule. The roadmap uses $110,000–$135,000 a year
against a national median private room near $129,575, and inflates it at a
healthcare rate above general inflation.

Every part of that is an adviser's choice and should be shown as one.

Rule: an assumption — the written rules say so explicitly.

**Also touches:** Spending and care · Medicare · Estate and family

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

Rule: IRC §213(d)(10), §7702B(b); Rev. Proc. 2025-32.

**Also touches:** Tax · Spending and care

---

### My policy pays $500 a day but the care costs less. Is the extra taxable?

```
Received       $500 x 365    =  $182,500
2026 limit     $430 a day    =  $156,950
Taxable                          $25,550
```

Output: only on an indemnity or per-diem contract. A reimbursement contract
that pays actual cost has no excess to tax.

Rule: IRC §7702B(d); Rev. Proc. 2025-32.

**Also touches:** Tax · Medicare

---

### The care year wrecks my income. Should I convert that year?

Output: often **yes**, and it is counter-intuitive. A huge medical deduction
can drop taxable income far enough that converting into the space costs very
little.

Worked example: $151,000 of expenses against $190,000 of AGI left $136,750
deductible and federal tax of $4,891 instead of about $17,222. Converting
$57,550 into that room cost $10,140 — an effective **17.6%**.

Rule: IRC §213 creates the room; §408A governs the conversion. The
decision is our own calculation.

**Also touches:** Taking money out · Estate and family (it also protects the surviving spouse)

---

## PROPERTY

A rental loss has to pass the same four gates as a K-1 loss (see the K-1 and business losses cases). But
property has two gates **before** those, and the order is not optional.

```
Gate 0   §280A    personal use — tested first
Gate 0b  §469     is it passive at all? (the 7-day rule)
then     §704(d) → §465 → §469 → §461(l)
```

---

### I bought a rental and a cost segregation study turned it into a big paper loss.

Inputs: purchase price · land allocation · % in 5-year and 15-year components ·
placed in service after 19 January 2025

Output: cost segregation splits the building into shorter-lived parts, and
100% bonus depreciation writes those parts off immediately. A property that
makes money in cash can show a large loss on paper.

Whether that loss is worth anything is a completely separate question — see
the next case.

Rule: IRC §167, §168(c),(e), §168(k); §1016(a)(2) reduces basis.

**Also touches:** K-1 and business losses (the loss now has to survive four gates) · Tax

---

### I earn $600,000 and I was told the loss is worthless this year.

Output: a long-term rental is passive **by definition**, whatever the client
does. The $25,000 allowance is gone above $150,000 of income. So the loss is
suspended and does nothing this year.

The paper loss is real. The tax benefit is not — yet.

Rule: IRC §469(c)(2); §469(i) phase-out.

**Also touches:** K-1 and business losses · Money coming in

---

### The same property as a short-term rental offsets my salary. Why?

Inputs: total rental days · number of separate stays · owner hours · personal
use days

```
Average stay  =  total rental days / number of stays

7 days or less  +  material participation   →  NOT passive
                                            →  offsets W-2 income
```

Output: this is the single biggest swing in the whole property section. The
same building, the same loss, and the answer changes entirely on the average
booking length.

Rule: Treas. Reg. §1.469-1T(e)(3)(ii)(A); §1.469-5T(a) for
participation.

**Also touches:** K-1 and business losses (it still has to clear the at-risk and overall-cap gates) · Medicare (a large W-2 offset moves AGI, which moves the surcharge)

---

### One long winter booking pushed my average over seven days.

Output: the whole year fails. Not the one booking — the year. The property
reverts to passive for every day of it, and the entire loss is suspended.

The written rules tabulate a 7.4-day average as a failure.

Rule: Treas. Reg. §1.469-1T(e)(3)(ii)(A).

**Also touches:** K-1 and business losses

---

### I use a management company, and the loss got suspended anyway.

Output: the seven-day test was met, but material participation failed. The
manager's hours are another individual's participation, and they count against
the client under several of the tests.

Time spent as an investor — reading statements, reviewing finances — does not
count as participation at all.

Rule: Treas. Reg. §1.469-5T(a)(1)–(7); §1.469-5T(f)(4).

**Also touches:** K-1 and business losses

---

### Can I qualify as a real estate professional and free up all my rentals?

```
750 hours   in real property trades or businesses
   AND
more than half of ALL personal services for the year
```

Output: the second test is what stops most people. A full-time job elsewhere
makes "more than half" arithmetically impossible, regardless of hours spent on
property.

An aggregation election groups the rentals so participation is tested across
all of them together — but it then blocks the loss release on selling just one.

Rule: IRC §469(c)(7)(B); Treas. Reg. §1.469-9(g).

**Also touches:** Money coming in · K-1 and business losses

---

### We use the beach house a few weeks a year.

```
Personal use over the greater of 14 days or 10% of rental days
  →  expenses are allocated
  →  deductions are capped at rental income
  →  no loss survives at all
```

Output: this is tested **first**, before the four gates. If it bites, nothing
reaches them. A client planning a loss on a property they also holiday in is
usually planning nothing.

Family use counts, and family is defined broadly.

Rule: IRC §280A(d)(1), (d)(2), (e), (c)(5).

**Also touches:** K-1 and business losses

---

### My son lives in the rental. Does that ruin it?

Output: family use counts as personal use — **unless** the family member pays
a fair market rent and uses it as their principal residence. Both conditions,
not one.

Rule: IRC §280A(d)(2)(A), (d)(3); §267(c)(4) defines family.

**Also touches:** Estate and family

---

### Can I rent my own home to my company for 14 days tax free?

Output: **yes**, and it is one of the few genuinely free things in the code.
Up to 14 days a year, the rent is excluded from the client's income entirely
and the company still deducts it.

It needs a defensible daily rate backed by comparables and a real business
purpose. At 15 days the whole thing collapses and all of it becomes income.

Rule: IRC §280A(g).

**Also touches:** K-1 and business losses · Tax

---

### I sold the rental and got hit with recapture I did not expect.

Output: every dollar of depreciation taken over the years comes back. Worse,
the cost segregation that produced the fast early deductions comes back at
**ordinary** rates, not the 25% that applies to the building.

| Component | Rate on sale |
|---|---|
| Cost-segregated personal property (§1245) | **ordinary** |
| The building's depreciation (§1250) | 25% ceiling |
| The rest of the gain (§1231) | capital gain |
| On top, if applicable | 3.8% investment income tax |

The 25% is a **ceiling**, not a flat rate — it is the lower of 25% and the
client's own marginal rate.

Rule: IRC §1245, §1250, §1(h)(1)(E), §1231, §1411.

**Also touches:** Medicare (a sale year sets the surcharge and cannot be appealed) · K-1 and business losses (the sale releases suspended losses)

---

### I never claimed depreciation, so there is nothing to recapture.

Output: **wrong.** Recapture is computed on depreciation *allowed or
allowable*. The client is taxed on deductions they never took.

It can be recovered — a change of accounting method pulls the missed
depreciation into one year — but it has to be done deliberately.

Rule: IRC §1016(a)(2); §446/§481(a) with Form 3115.

**Also touches:** Tax

---

### Can I roll the sale into another property instead of paying tax?

Output: yes, but it defers rather than forgives. The old basis and the whole
depreciation history carry into the new property, so the recapture is still
waiting.

Hard deadlines: 45 days to identify, 180 days to close, and a qualified
intermediary must hold the money — the client must never touch it. Cash taken
out is taxed immediately.

Held until death, the chain is wiped clean by the basis step-up.

Rule: IRC §1031(a),(b),(d),(a)(3).

**Also touches:** Estate and family

---

### We are selling the family home.

```
Owned and lived in 2 of the last 5 years
Excluded:  $250,000 single  /  $500,000 married
```

Output: gain above that is taxable. And the exclusion does **not** cover
depreciation claimed since May 1997 for a home office or a rental period —
that part is taxed regardless.

Usable once every two years.

Rule: IRC §121(a),(b),(b)(3),(d)(6).

**Also touches:** Medicare · Tax

---

### My equity is growing. Is that the mortgage paying down?

Inputs: $500,000 loan at 6.5%

```
Principal repaid in year one   $5,589
```

Output: almost all early equity is appreciation, not repayment. Barely 1% of
the loan comes off in the first year. Clients consistently overestimate this.

Rule: an assumption — standard amortisation and an assumed growth rate.

**Also touches:** Growth · Estate and family

---

### The property is worth less than the mortgage and I want to walk away.

Output: this depends entirely on whether the debt is recourse or nonrecourse,
and the answers are very different. Forgiven recourse debt is income unless an
exclusion applies; nonrecourse debt is simply added to the sale price. At-risk
recapture can also fire.

Rule: IRC §1001; §61(a)(11); §108(a)(1)(B),(D); §465(e).

Missing: **the modules carry no dedicated §108 case.** This sits outside every
Case Register and needs specialist advice.

**Also touches:** K-1 and business losses · Tax

---

### One note on the software

The property list and the "current real estate value" field feed two different
parts of the engine — the projection, and the real estate bucket. A client who enters the same house in both is counted twice.

**Also touches:** The seven buckets

---

## K-1 AND BUSINESS LOSSES

The client puts money into a deal. The K-1 arrives with a loss on it. They
expect a tax refund. Often they get nothing.

A business loss passes through **four gates, in this fixed order**. It must
clear each one to reach the next. Whichever gate stops it decides what
frees it later — and each gate is freed by a different event.

```
Gate 1   §704(d) / §1366(d)   basis
Gate 2   §465                 at risk
Gate 3   §469                 passive
Gate 4   §461(l)              excess business loss
```

Run them out of order and you get a different answer. The engine runs gates
1 and 2 per property, then pools everything for gate 3.

---

## The four gates

### $250,000 loss on the K-1. How much comes off the tax bill this year?

Inputs: loss $250,000 · outside basis $180,000 · at risk $150,000 · client
does not work in the business · no other passive income · wages $600,000

```
Gate 1  §704(d) basis     allowed 180,000   suspended  70,000
Gate 2  §465 at risk      allowed 150,000   suspended  30,000
Gate 3  §469 passive      allowed       0   suspended 150,000
        the $25,000 allowance is fully gone at $600,000 of income
Gate 4  §461(l)           nothing reaches it

Deducted this year    $0
Suspended             70,000 + 30,000 + 150,000  =  250,000
```

Output: **$0 off this year's tax.** All $250,000 waits, split three ways.
Every dollar is suspended at exactly one gate, and the three piles are not
interchangeable.

Rule: IRC §704(d) → §465 → §469 → §461(l), in that order.

Missing: whether anyone guaranteed the partnership debt — that changes gate 2
and nothing else.

**Also touches:** Tax (no AGI change, so no knock-on) · Property (a rental loss dies at the same gates) · Estate and family (each pile dies differently when the client dies)

---

### The loss is bigger than what I actually put in.

Inputs: cash contributed · income allocated over the years · distributions
taken · losses already deducted · share of partnership debt under §752

Output: the excess stops at gate 1 and waits until basis is rebuilt — by
future income or more money in. It never expires, but it also never moves on
its own.

Rule: §704(d) with §705 and §752 for a partner; §1366(d)(1) with
§1367(a) for an S-corp shareholder.

**Also touches:** Estate and family (basis-suspended losses are lost at death — they do not pass to heirs)

---

### The partnership has a mortgage, so I have basis — but I am told I am not "at risk".

Output: basis and at-risk are two different numbers and they move
differently. Nonrecourse debt raises basis under §752 whether or not it
qualifies. Only *qualified nonrecourse financing* raises the at-risk amount.

A normal bank mortgage on real property usually qualifies, so most clients
never notice gate 2 exists. Seller financing usually does not qualify — the
seller has an interest in the property.

Rule: §465(b)(6) four conditions; §465(b)(3) borrowing from a person
with an interest.

**Also touches:** Property (seller-financed property purchases)

---

### My partner personally guaranteed the loan, and now MY losses are blocked.

Output: a personal guarantee by any person disqualifies the debt as qualified
nonrecourse financing **for everybody else in the deal**. The guarantor gets
at-risk amount for it; the other partners lose theirs.

The written rules call this "the single most common way a co-owner's at-risk amount collapses."

Rule: §465(b)(6)(B)(iii); §465(b)(1)(B) for the guarantor.

**Also touches:** Property · Life insurance (guarantees and indemnities)

---

### I heard I can deduct $25,000 of rental loss. Why did I get nothing?

Inputs: modified AGI · active participation · at least 10% ownership · loss

```
AGI  $95,000   →   full $25,000 allowance
AGI $120,000   →   25,000 − 0.50 × (120,000 − 100,000)  =  $15,000
AGI $150,000   →   $0
```

Output: the allowance drops 50 cents for every dollar of AGI over $100,000
and is gone at $150,000. **Neither figure has been indexed since 1986**, so
it catches more people every year.

Rule: §469(i).

**Also touches:** Forced withdrawals (a required distribution raises the AGI that kills this) · Medicare (same AGI drives the Medicare surcharge)

---

### The loss is not passive at all, but I still cannot use all of it.

Inputs: total business deductions · total business income · filing status

```
2026 threshold   $256,000 single   ·   $512,000 joint
```

Output: anything above the threshold is disallowed this year and becomes a
net operating loss next year.

**Watch this one in 2026.** The threshold **fell** from $313,000 / $626,000
— an 18.2% drop. Thresholds normally rise. This one did not.

Rule: §461(l)(1) and (3)(A); §461(l)(2) converts the excess to an NOL.

**Also touches:** Property (cost segregation is what usually creates a loss this big) · Events (a tax-law change mid-projection)

---

## Income with no cash

### The K-1 says $150,000 of income. The partnership sent me nothing. I still owe tax.

Inputs: distributive share $150,000 · cash actually received $0 · marginal rate

Output: the client is taxed on the full $150,000. It also raises basis under
§705, which helps a future loss — but that is no comfort in April.

The cash to pay the tax has to come from somewhere, and every source has its
own cost.

Rule: §702 and §704 tax the distributive share regardless of
distribution.

Missing: whether the operating agreement has a tax-distribution clause.

**Also touches:** Taking money out (which account funds the tax bill) · Medicare (the phantom income still drives the Medicare surcharge)

---

### I took a distribution after several loss years and got a capital gain.

Output: losses reduce stock basis first, then debt basis. Once basis is at
zero, a distribution above it is capital gain — even though the client
"only took out their own money".

Rule: §1367(b)(2); §1368 / §731.

**Also touches:** Tax

---

### The bank made me guarantee my S corporation's loan. Doesn't that give me basis?

Output: **No.** An S-corp shareholder gets debt basis only from indebtedness
of the corporation *to the shareholder*. A guarantee creates nothing until
the shareholder actually pays.

The fix is to borrow personally and lend on to the company — back-to-back.
This is the single most expensive difference between an LLC and an S corp
for a loss-making business, because a partner *does* get basis for
partnership debt under §752.

Rule: §1366(d)(1)(B).

**Also touches:** Money coming in (the same choice cuts the other way on employment tax)

---

## Getting the losses back

### I sold the partnership interest. Do all those suspended losses come back?

Output: yes for the passive pile — but only if **all three** are true:
the entire interest was sold, the sale was fully taxable, and the buyer is
not a related party. Miss any one and the release does not happen.

| What was suspended | Released on sale? |
|---|---|
| §469 passive | Yes, in full |
| §465 at risk | Yes, on disposition |
| §704(d) / §1366(d) basis | **No — generally lost** |

A gift is not a sale: the suspended loss is added to the donee's basis and
the donor loses it. A sale to a related party defers the release instead of
granting it.

Rule: §469(g)(1); §469(g)(1)(B) related-party deferral.

**Also touches:** Property (aggregating rentals blocks release on selling just one) · Estate and family

---

### I own the building my own practice rents. Can that rent soak up my other suspended losses?

Output: **No, and it works against the client.** Net self-rental *income* is
recharacterised as non-passive, so it cannot absorb passive losses. A net
self-rental *loss* stays passive. The rule only ever runs one way.

Rule: Treas. Reg. §1.469-2(f)(6).

**Also touches:** Property

---

### I have a big carryforward. How long until I actually use it?

Output: an NOL can only wipe out 80% of taxable income in any later year, so
20% always stays taxable. It carries forward indefinitely with no carryback.

Rule: §172(a)(2) 80% limit; §172(b)(1)(A).

**Also touches:** Taking money out (a Roth conversion is a good way to feed income to a carryforward)

---

### I am carrying large suspended losses and I am getting old. What happens when I die?

Output: mostly bad. This is the case clients never ask until it is too late.

| Pile | At death |
|---|---|
| NOL carryforward | **Extinguished.** Nothing survives. |
| §469 passive suspended | Released **only** above the §1014 step-up — so the bigger the step-up, the less comes back |
| §704(d) / §1366(d) basis suspended | **Lost** |

Rule: §172 (no survival provision); §469(g)(2); §1014.

Output in plain terms: losses are worth far more used during life than left
to heirs. That is an argument for accelerating income — a Roth conversion or
a deliberate gain — while the losses are still alive.

**Also touches:** Taking money out (accelerate income to use them) · Estate and family · Age by age

---

## What the software does not tell the client

The engine runs all four gates correctly. It works out exactly how much stopped at each one — basis, at risk, passive — and then throws that breakdown away. The parked amounts are stored on every row but appear in **no column of the year table and in no note**.

So a client whose $250,000 loss was fully suspended sees a screen identical
to a client who had no loss at all. They are never told which gate stopped
it, how much is waiting, or what would free it.

That is why this question had no answer.

**Also touches:** Checking the picture

---

## MEDICARE

The surcharge is set by the client's income from **two years earlier**, and it
is a cliff, not a slope. That combination is what makes it dangerous.

---

### Which year's income sets my premium?

```
Income in 2026   →   sets the premium for 2028
```

Output: a client retiring at 65 pays their first premium based on their last
big working year. Nothing about their current income matters.

Rule: Social Security Act §1839(i); 20 CFR §418.1010.

**Also touches:** Taking money out (conversions done at 63 land at 65)

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

Rule: Social Security Act §1839(i).

**Also touches:** Taking money out (this is why the engine offers a "fill to a tier" mode)

---

### We converted $120,000 to Roth at 64 and got a Medicare bill at 66.

Output: the conversion is added to income in the conversion year, and the
surcharge follows two years later. For a couple, both spouses pay it.

The conversion may still be right. But the surcharge is a real cost of it and
belongs in the comparison.

Rule: Social Security Act §1839(i), §1860D-13(a)(7).

**Also touches:** Taking money out · Forced withdrawals

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

Rule: 20 CFR §418.1205; Form SSA-44.

**Also touches:** Property · Events · K-1 and business losses

---

### I retired and my income collapsed, but the premium is based on my old salary.

Output: this one **can** be fixed. Work stoppage or reduction of hours is on
the qualifying list. File Form SSA-44 with evidence of the retirement date and
ask for a new determination rather than waiting two years.

Rule: 20 CFR §418.1205(d), §418.1201.

Missing: **not implemented in the engine**. A client who
retires is shown the surcharge anyway.

**Also touches:** Events

---

### I am delaying Social Security to 70 but I am on Medicare. Why am I billed directly?

Output: the protection that caps a premium increase against the annual
cost-of-living rise only applies to people who have a benefit in payment and
are not paying a surcharge. A client deferring to 70 has no benefit to deduct
it from, so they pay the full increase in cash.

Rule: Social Security Act §1839(f).

**Also touches:** Social Security

---

### I am taxed on more Social Security than actually reached my bank account.

Output: the premium and any surcharge are withheld from the benefit, but the
tax is worked out on the **gross** benefit before that deduction. The client
is taxed on money they never saw.

The premiums are at least a qualifying medical expense, which matters in a
high-care year.

Rule: IRC §86 on the gross benefit; Social Security Act §1839.

Note: the engine shows premiums as an expense rather than netting them from
the benefit. Presentation only — the tax result is right, because §86 uses the
gross figure either way.

**Also touches:** Spending and care · Social Security

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

Rule: Social Security Act §1813.

**Also touches:** Spending and care · Life insurance · The seven buckets (the bucket that was meant to fund this)

---

### We are separated but not divorced and want to file separately.

Output: this is the worst filing position in the system. The Social Security
taxation thresholds drop to **zero** unless the couple lived apart for the
whole year, and the surcharge schedule is compressed savagely.

Rule: IRC §86(c); Social Security Act §1839(i).

**Also touches:** Events · Tax

---

## TAKING MONEY OUT

---

### Which account does the money come out of first?

The engine drains in a fixed order:

```
1.  Taxable brokerage
2.  Pre-tax (401k / IRA)
3.  Roth        — last, on purpose
```

Output: Roth is preserved to the end because it is the only pot that costs
nothing to use and passes to heirs without an income tax bill.

Rule: our own calculation — no law sets an order. This is a modelling choice.

Missing: the order is **not selectable**. Competing tools let the client
change it, and for some households a different order wins.

**Also touches:** Estate and family · Forced withdrawals

---

### The window between retiring and forced withdrawals.

Inputs: retires at 62 · born 1960, so forced withdrawals start at 75

```
13 years with almost no forced income
```

Output: this is the single biggest planning opportunity in the whole
projection. Earned income has stopped, forced withdrawals have not started,
and taxable income is largely under the client's control.

Income taken here — by conversion or by realising gain — is taxed at rates
that will never be available again.

Rule: our own calculation. The ages come from a real rule.

**Also touches:** Forced withdrawals · Medicare · Age by age

---

### I want to convert $200,000 to Roth.

Inputs: conversion $200,000 · all traditional/SEP/SIMPLE IRA balances · any
Form 8606 basis · where the tax money comes from

Output: the converted amount is ordinary income this year. There is **no
income limit** on converting, in any year.

Three things that go wrong:
- The pro-rata rule applies, exactly as in the Putting money in cases — old pre-tax money makes the
  conversion mostly taxable.
- Paying the tax out of the converted money shrinks the conversion and, under
  59½, can attract the 10% additional tax on the part withheld.
- A converted amount withdrawn within **five tax years** attracts the 10% tax
  if the client is under 59½ — even though the conversion itself never does.

Rule: IRC §408A(d)(3), §408(d)(2), §408A(d)(3)(F).

**Also touches:** Putting money in · Medicare · Social Security

---

### How much should I convert?

The engine offers three targets:

| Mode | What it does |
|---|---|
| Fixed amount | Converts the same figure every year, ignoring how much room exists |
| **Fill to a bracket** | Converts as much as fits below a rate ceiling, and nothing in a year with no room |
| **Fill to a Medicare tier** | Stops just under a surcharge cliff |

Output: filling to a ceiling converts the most that can be done at a known
rate. A fixed amount is the weakest of the three because it ignores the year.

The calculation has to **iterate**. The senior deduction phases out against
AGI, and the conversion is itself part of AGI, so a single pass overshoots —
by $10,643 in testing.

Rule: our own calculation. The ceilings are a real rule.

**Also touches:** Medicare · Tax

---

### I am in the 12% bracket. I took an extra $10,000 and the tax was nearly double.

Output: the extra $10,000 did not just get taxed. It also dragged more Social
Security benefit into tax alongside it — up to **$1.85 of taxable income per
$1 withdrawn**.

So a client who believes they are paying 12% can be paying an effective rate
far above it. This is the real "tax torpedo", and it hits exactly the
middle-income retirees who think they are safe.

Rule: IRC §86(a)(2), the 85% tier.

**Also touches:** Social Security · Forced withdrawals

---

### I want to take my whole $1,000,000 out in one year at 65.

Output: allowed, and no 10% penalty at 65. But:

- most of it lands in the top brackets
- 85% of the Social Security benefit becomes taxable
- the net investment income tax can reach other income
- the Medicare surcharge jumps two years later, and a one-off sale like this
  **cannot be appealed**
- state tax may apply on top

Spreading the same money across several years is almost always cheaper. The
engine will show both if asked.

Rule: our own calculation for the decision. Consequences are a real rule.

**Also touches:** Medicare · Social Security · Tax

---

### I am 60 and retired. I want to take only what stays in a low bracket.

Output: this is the same move as a bracket-filling conversion, and it is the
correct default. Take enough to use up the cheap brackets, leave the rest to
keep growing.

Rule: our own calculation. Bracket ceilings are a real rule.

**Also touches:** Tax

---

### Under 59½ — what actually costs 10%?

The engine does **not** model any of this — the early-withdrawal penalty appears nowhere in it. So every case below is a
documentation answer, not something the projection will show.

| Situation | 10% extra tax? |
|---|---|
| Left the job in or after the year turning **55**, money still in **that employer's plan** | No |
| Same, but rolled to an IRA first | **Yes** — the exception is lost |
| Permanently disabled | No |
| Unreimbursed medical above the AGI floor | No |
| **Hardship withdrawal** | **Yes** — hardship is permission to withdraw, not a penalty exception |
| Emergency withdrawal at 45, no exception | Yes |
| Inherited account | No |

Rule: IRC §72(t)(1) and the §72(t)(2) exceptions.

Missing: the Rule of 55, hardship treatment, plan-loan offsets and net
unrealised appreciation are **not covered anywhere in the written rules**. They
are a documentation gap, not only an engine gap.

**Also touches:** Events · Putting money in

---

### I have a 401(k) loan and I am leaving my job.

Inputs: loan balance $30,000 · date of separation · age

Output: if it is not repaid, the outstanding balance becomes a taxable
distribution. Under 59½ with no exception, the 10% applies on top.

There is a rollover window — until the tax return due date including
extensions — to put the offset amount into an IRA and undo it. Most people
do not know it exists.

Rule: IRC §72(p), §402(c)(3)(C).

**Also touches:** Events

---

### My 401(k) is full of my own employer's stock.

Inputs: stock market value $100,000 · plan cost basis $30,000

Output: there is a route where only the $30,000 basis is ordinary income now
and the $70,000 growth is taxed later at capital gain rates instead. It needs
a lump-sum distribution of the whole plan balance in one tax year after a
triggering event.

Executed wrongly it is simply lost, and the whole $100,000 becomes ordinary
income. The difference is large enough to be worth specialist advice.

Rule: IRC §402(e)(4).

**Also touches:** Estate and family (this stock gets no basis step-up)

---

### I left my job and want to move the old 401(k) without paying tax.

Inputs: old plan balance $400,000 · where it goes

Output: a **direct** trustee-to-trustee transfer to an IRA or a new employer
plan costs nothing now — no income tax, no 10%.

But the destination matters later, and most people are not told:

| Moved to | Consequence |
|---|---|
| A new employer's **plan** | stays out of the pro-rata pot; a backdoor Roth still works |
| A **traditional IRA** | creates pre-tax IRA money that poisons every future backdoor Roth |

It also destroys the Rule of 55 on that money, permanently.

Rule: IRC §402(c), §401(a)(31).

**Also touches:** Putting money in · Events

---

### The 401(k) sent the cheque to me instead, and kept 20%.

Inputs: distribution $100,000 · withheld $20,000 · received $80,000

```
To roll the full $100,000 over, the client must deposit $100,000
  — the $80,000 received
  — PLUS $20,000 found from their own pocket
Within 60 days.

The $20,000 comes back as a refund the following year, not now.
Miss the 60 days, and the shortfall is a taxable distribution
  plus 10% if under 59.5.
```

Output: a paperwork mistake turns into a tax bill. Always ask for a direct
transfer — never a cheque made out to the client.

Rule: IRC §3405(c) 20% mandatory withholding; §402(c)(3) 60-day limit.

**Also touches:** Events

---

### Should I be using the Roth 401(k) instead of the traditional one?

Inputs: current rate · expected retirement rate · years to retirement ·
expected pre-tax balance at the forced-withdrawal age · heirs' rate

Output: it is not only a rate comparison. Three things push toward Roth that
clients rarely weigh:

- Roth balances are **not** subject to lifetime forced withdrawals, so they do
  not feed the snowball in the Forced withdrawals cases
- Roth money does not raise provisional income, so it does not drag Social
  Security into tax or lift the Medicare surcharge
- A Roth inherited by a child costs them nothing; a pre-tax account costs them
  ordinary income at their own peak-earning rate

The single strongest argument is the surviving spouse. A widow on single
brackets with a large pre-tax balance is the worst combination in the system.

Rule: IRC §402A; SECURE 2.0 §325.

**Also touches:** Forced withdrawals · Medicare · Estate and family · Social Security

---

## ESTATE AND FAMILY

The number that matters is not the estate value. It is what the family keeps after tax.

---

### Two accounts, same size on the statement. Which do I leave to which child?

Inputs: $1,000,000 pre-tax IRA · $1,000,000 brokerage with $200,000 of basis

```
IRA to the heir       taxed as ordinary income as it comes out
                      NO basis step-up
                      at 35%, roughly $650,000 survives

Brokerage to the heir basis steps up to value at death
                      $800,000 of gain is erased
                      sold the next day, tax is $0
                      $1,000,000 survives
```

Output: **they are not the same asset.** The statement says they are. A
pre-tax retirement balance is the worst thing to leave to a taxable heir and
the best thing to leave to charity.

Rule: IRC §1014(a) step-up; §1014(c) and §691 deny it to retirement
money; §1223(9) makes inherited gain automatically long-term.

**Also touches:** Forced withdrawals · Taking money out (converting during life moves money to the good side)

---

### My daughter inherits the IRA and has to empty it in ten years.

Output: and those ten years are usually her highest-earning ones. The whole
balance is taxed on top of her salary, at her rate, not the client's.

Whether she must take something each year depends on when the client died
relative to their own start date — see the Forced withdrawals cases.

Rule: IRC §401(a)(9)(H); SECURE Act; §691.

**Also touches:** Forced withdrawals · Taking money out

---

### My estate is over the federal line. What is the bill?

```
2026 exclusion    $15,000,000 per person
Rate above it     flat 40%
```

Output: the tax is a flat 40% of the excess. There is nothing progressive
about it at this level, which makes the arithmetic simple and the planning
binary — either the estate is under the line or every extra dollar costs 40
cents.

This exclusion is now **permanent**, so the old rush to use it before it
halved is over.

Rule: IRC §2001, §2010(c), §2031, §2053; P.L. 119-21 §70106.

**Also touches:** Life insurance · Property

---

### I am well under the federal line but well over my state's.

Output: many states run their own estate tax at a far lower threshold, and
there is **no portability between the two systems**. A client comfortably
under $15,000,000 federally can still owe state estate tax.

Oregon starts near $1,000,000. That is fifteen times lower than the federal
line.

Rule: state statute. No IRC section.

**Also touches:** Events (moving state changes this)

---

### I live in New York and I am just over the threshold.

Inputs: estate $7,800,000 · NY exclusion $7,350,000 · cliff at 105% = $7,717,500

Output: **the whole estate is taxed, not just the excess.** Going $82,500 past
the cliff exposes all $7,800,000 at up to 16%.

This is the one place in the whole system where a modest charitable gift — just
enough to drop back under $7,717,500 — pays for itself many times over.

Rule: NY Tax Law cliff. No IRC section.

**Also touches:** Events

---

### I already gave a lot away. How much exclusion is left?

Output: lifetime taxable gifts already reported come off the exclusion at
death. They are added back into the computation, so giving early does not by
itself save estate tax — it moves the **growth** out, which is where the real
saving is.

Rule: IRC §2001(b), §2505, §2010(c).

**Also touches:** Growth

---

### I want to give to my children every year without using up anything.

```
2026 annual exclusion   $19,000 per recipient per year
Married couple          $38,000 per recipient
```

Output: these gifts never touch the lifetime exclusion and need no return.
Direct payments of tuition or medical bills to the institution are unlimited
and on top.

Rule: IRC §2503(b), §2513, §2503(e).

**Also touches:** Growth

---

### Should I give my children appreciated stock now, or leave it to them?

```
Given now      they take MY basis      —  the gain survives and they pay it
Left at death  basis steps up          —  the gain is erased
```

Output: for an estate **under** the exclusion, giving appreciated assets away
during life is usually the wrong move. It converts a free step-up into a
carried-over gain for no estate tax saving.

Give cash, or give the assets with the *least* built-in gain.

Rule: IRC §1015 carryover vs §1014 step-up.

**Also touches:** Tax

---

### My husband died this year. How do I file?

```
Year of death         joint, for the whole year
Next two years        surviving-spouse rates ONLY if a dependent child lives at home
Otherwise             single
```

Output: most clients have no dependent child, so they go straight from joint
to single in the year after the death. See the widow's penalty in the Social Security cases for
what that costs.

Rule: IRC §6013(a)(3); §2(a); §1(j)(2)(C).

**Also touches:** Social Security · Medicare · Taking money out

---

### I am 54, my husband left me his IRA, and I need the money now.

Output: this decision is **irreversible** and it goes the opposite way to
intuition.

| Choice | Under 59½ |
|---|---|
| Keep it as an **inherited** IRA | withdrawals escape the 10% extra tax |
| Roll it into **her own** IRA | the 10% applies until she is 59½ |

A widow who needs income before 59½ should usually **not** roll it over yet.
Most advisers default to the rollover.

Rule: IRC §401(a)(9)(B)(iv); §72(t)(2)(A)(ii); SECURE 2.0 §327.

**Also touches:** Taking money out · Forced withdrawals

---

### We are splitting the 401(k) and the IRA down the middle in the divorce.

Output: **half of a pre-tax account is not half of a taxable account.** An
even split by balance is an uneven split by value, because one side owes
income tax on every dollar and the other does not.

The transfer itself is tax-free if done correctly — a court order for an
employer plan, a direct transfer for an IRA. Done as a withdrawal instead, it
is taxed and can carry the 10%.

Rule: IRC §1041; §414(p); §408(d)(6); §72(t)(2)(C).

**Also touches:** Events · Social Security (a 10-year marriage keeps her claim on his record)

---

### I am selling my business for $3,000,000 of gain.

```
Federal tax                        $700,745    (22.85% effective)
Medicare surcharge two years later  $13,872
```

Output: the surcharge cannot be appealed — a sale is not on the qualifying
list. Everything else that year moves too: the deduction limits, the business
deduction, the senior deduction.

Rule: IRC §1(h), §1411, §199A, §68; 20 CFR §418.1205.

**Also touches:** Medicare · K-1 and business losses · Property

---

### Some of that gain might be tax-free.

Output: stock in a qualifying C corporation can be excluded, and the rules
were widened. The exclusion now steps in:

```
Held 3 years    50% excluded
Held 4 years    75%
Held 5 years    100%
Per-issuer cap  $15,000,000
```

Output: waiting one more year before selling can be worth millions. Excluded
gain never enters income at all, so it does not touch the Medicare surcharge
either.

Rule: IRC §1202 as amended by P.L. 119-21.

**Also touches:** Medicare · Tax

---

### Can I take the price over six years instead?

Output: spreading it keeps the client out of the top brackets and out of the
top surcharge tiers. Worked example saving: **$142,975**.

Two catches: depreciation recapture is **all** accelerated into year one
regardless, and the election out is irreversible. Above $5,000,000 outstanding
there is an interest charge.

Rule: IRC §453, §453A.

**Also touches:** Medicare · Property

---

### What is the estate number the engine shows?

What the family gets = everything − debts − federal estate tax − state estate tax − the children’s income tax on the pre-tax money.

That last term is the heirs' income tax on the pre-tax balance — the thing
almost every projection leaves out. Net worth and estate value are **not** the
same number, and the gap is real money.

Note the seven buckets are not in net worth at all. See the seven buckets cases.

**Also touches:** The seven buckets · Checking the picture

---

## THE SEVEN BUCKETS

This is the picture's own logic, not tax law. Almost none of it has a legal rule behind it — every number is the adviser's, and the picture says so itself:

> The front end should render approved values from the roadmap engine. It
> should not determine eligibility, calculate tax savings, or override
> advisor-approved assumptions.

Read that as: **the adviser owns these numbers, the software just displays them.**

---

## Three different formulas, and they disagree

This has to be settled before any of these numbers mean anything.

**1. The picture**

```
Net Tax Savings + DWC % x Qualified Deduction Base
188,000 + 0.20 x 420,000  =  $272,000
```

**2. The front end**

Deployable capital = (net tax savings + DWC% × the base) × how well the strategy works.

Same as the picture, with an effectiveness multiplier added.

**3. The documented methodology** — the written method, which is also what the
`tax-be` backend actually runs

```
totalTaxSaved = baseTotalTaxSaved x (strategyEffectiveness / 100)
```

**There is no DWC percentage in it. There is no qualified deduction base in
it.** Both terms are absent. The whole $84,000 that the picture adds on top
of the tax savings has no counterpart in the documented method.

Checked directly against the 12,033-line reference document:

| Searched for | Times it appears |
|---|---|
| "Deployable Wealth Capital" or "DWC" | **0** |
| "Qualified deduction base" | **0** |

the written method is titled "Tax Savings Deployment Framework" and labels itself
*"Proprietary methodology — not law."* It says nothing in it may be cited to
the Internal Revenue Code.

**And the bucket counts do not agree either:**

| Source | Buckets |
|---|---|
| The picture | **7** |
| the written method (the documented method, and the backend) | **6** |
| the software | **6** |

the written method says "the six buckets" in four separate places. Market /
Opportunity Capital exists only on the picture.

**the written method also splits the money differently.** It does not apply flat
percentages to the whole balance. It computes an *allocatable plan* first:

```
allocatablePlan = max(0, plan - compoundedQualifiedSavings)
retirement      = compoundedQualifiedSavings + 0.35 x allocatablePlan
the other five  = straight percentage x allocatablePlan
```

The front end does none of this. It seeds buckets from raw inputs and grows
each at its own rate.

So the picture, the front end and the documented method are three different
calculations producing three different numbers from the same client. **Pick
one before this goes in front of a client.** Everything below describes what
the front end does today.

**Also touches:** Checking the picture (which picture numbers survive this)

---

## How much gets deployed

### The adviser approves $188,000 of savings. How much actually goes to work?

Inputs: net tax savings $188,000 · DWC 20% · qualified deduction base $420,000 · effectiveness 100%

```
(188,000 + 0.20 × 420,000) × 100%  =  $272,000 per year
```

Output: $272,000 deployed every working year.

Rule: the adviser supplies it — all four inputs come from the adviser's tax plan.

**Also touches:** Tax (the savings are only real if the strategies survive audit) · Checking the picture (the $420,000 base is not printed on the picture)

---

### The client's strategy costs more to run than it saves this year.

Inputs: strategy federal + state savings $60,000 · investment required $90,000

```
Net for the year  =  60,000 + 0 − 90,000  =  −$30,000
```

Output: nothing deploys this year. The buckets get their growth but no new money.

**Careful — the engine gets this partly wrong.** It only deploys anything in a year where the savings come out positive.

So the `DWC% × Qualified Deduction Base` half is dropped too. That half is
$84,000 a year and it does not depend on the savings at all. In a year where
a strategy costs more than it returns, the client silently loses $84,000 of
deployment they were entitled to.

Rule: our own calculation — and this one is a defect.

**Also touches:** Growth (a missed year compounds for the rest of the projection)

---

### The client pushes the DWC dial to 40%.

Inputs: same $188,000 · DWC 40% · base $420,000

```
188,000 + 0.40 × 420,000  =  $356,000 per year   (+31%)
```

Output: $356,000 a year. The picture's slider allows it — 0% to 40% — but
marks 15–25% as recommended.

Nothing in the engine stops a client at 40%. The recommendation is hint text, not a guardrail, and the picture's
visible slider does not exist in the UI at all.

Rule: the adviser supplies it.

**Also touches:** Checking the picture

---

### The adviser is only 80% confident the strategies will land.

Inputs: $272,000 · effectiveness 80%

```
272,000 × 0.80  =  $217,600 per year
```

Output: $217,600. Over 20 working years that is **$1.09M less** deployed
before any growth is counted.

Effectiveness is also set by the scenario picker — conservative 80%,
expected 100%, accelerated 125%.

Rule: the adviser supplies it.

**Also touches:** Growth

---

## Where the money goes

### The $272,000 splits seven ways.

| Bucket | Share | Per year | Grows at |
|---|---|---|---|
| Liquidity reserve | 10% | $27,200 | 5.75% |
| 401(k) / cash balance / Roth | 25% | $68,000 | 7.00% |
| Life insurance cash value | 20% | $54,400 | 5.50% |
| Real estate / business | 25% | $68,000 | 5.00% |
| Market / opportunity capital | 10% | $27,200 | 5.75% |
| Legacy / trust / philanthropy | 7% | $19,040 | 5.75% |
| Disability / LTC protection | 3% | $8,160 | 5.75% |

Every rate is an assumption, and admin fee plus cost of investment are
subtracted from all of them as drag.

Because the rates differ, the ending dollars stop matching the percentages.
That is correct, not a bug — see the Checking the picture cases.

**Also touches:** Putting money in (the 401k bucket collides with the real contribution limits) · Life insurance (the insurance bucket) · Property (the real estate bucket)

---

### The client asks: is the $15.4M on the picture the same as my net worth?

Output: **No, and this is the biggest problem in the current build.**

The seven buckets are a separate ledger. The engine adds them into one total — and then works out net worth **without it**:

Net worth is: pre-tax + Roth + brokerage + policy cash value − policy loans + property equity + other assets + insurance in the estate.

The bucket total is not in that line. So the bucket table and the net-worth chart
sit on the same screen showing two unrelated worlds. Deploying $272,000 a
year for twenty years moves the bucket table and does **nothing** to the
projected estate.

Rule: our own calculation — defect.

**Also touches:** Estate and family (the estate number the client actually cares about)

---

### There are only six buckets in the software, not seven.

**Market / Opportunity Capital (10%) does not exist.** The engine's bucket
list has only six: retirement, insurance, real estate, liquidity, legacy, disability/LTC. The screen even prints the words "split across six buckets". The research already assumes seven, listing Market / opportunity at 10%, $27,200 a year.

Output: 10% of every deployment has nowhere to go. The remaining six are
re-normalised to 100%, so each one is silently overweighted.

**Also touches:** Growth

---

### The default splits in the software are not the picture's splits.

| Bucket | Picture | Software default |
|---|---|---|
| Liquidity | 10% | 10% |
| 401(k) / Roth | 25% | **35%** |
| Life insurance | 20% | **25%** |
| Real estate | 25% | 25% |
| Market / opportunity | 10% | **absent** |
| Legacy / trust | 7% | **3%** |
| Disability / LTC | 3% | **2%** |

Output: a client who never touches the bucket fields gets a plan that does
not match the picture they were shown.

---

### The client's house gets counted twice.

Inputs: house worth $1,300,000, entered once in the property list and once as "current real estate value"

The real estate bucket is seeded from "current real estate value". Separately, property equity is built from the property list.

Output: the same house appears in both. The insurance bucket has the same
problem — it compounds at the credited rate while the actual policy cash
value is rolled forward independently at STEP 17.

Rule: our own calculation — defect.

**Also touches:** Property · Life insurance

---

### The disability / LTC bucket grows like an investment and never pays a claim.

Inputs: 3% of $272,000 = $8,160 a year

The engine grows this bucket at the taxable investment rate, like an investment.

Output: it compounds at 5.75% forever. But protection is a premium paid out,
not an asset that grows — and when long-term care actually starts, the cost
is charged to general expenses and **never drawn from this bucket**.

So the bucket that exists to fund care does not fund care.

Rule: our own calculation — defect.

**Also touches:** Spending and care (where the LTC cost is actually charged) · Life insurance (the policy that would really pay)

---

## AGE BY AGE

The picture's nine cards are marketing milestones. The ones in **bold** are legal dates where something changes whether you plan for it or not.

---

## Contribution Phase

### Age 42 — Foundation · $1.76M
*Implement Perfect Tax Plan layers*

The plan starts. Tax savings begin being deployed rather than spent.

The $1.76M is not built from the $272,000 — it is mostly money the client
already had. The picture does not say so. → see Checking the picture

**Also touches:** The seven buckets · Money coming in

---

### Age 45 — Protection · $3.05M
*Lock annual planning rhythm*

Nothing changes in law at 45. This is a review cadence, not a tax date.

If there is a K-1 or a rental in the plan, this is where suspended losses
start accumulating quietly. Nobody sees them, because the software does not
show them. → see K-1 and business losses

---

### **Age 50** — Acceleration · $5.25M
*Scale wealth buckets*

```
401(k) catch-up opens:  $24,500 + $8,000 = $32,500
```

Rule: IRC §414(v). → see Putting money in

---

### **Age 55** — Multiplication · $7.90M
*Retirement stress test*

The **Rule of 55** becomes available: leave the job in or after the year of
turning 55, and money in **that employer's plan** is reachable with no 10%
extra tax.

Roll it to an IRA first and the exception is gone forever. This is the most
commonly destroyed exception in the whole system. → see Taking money out

Rule: IRC §72(t)(2)(A)(v).

---

### **Age 59½**
*Not on the picture, and it should be*

The 10% additional tax ends. Every retirement account becomes reachable
without an exception.

This is a more significant date for most clients than 55 or 62, and the
picture skips it entirely.

Rule: IRC §72(t). → see Taking money out

---

### **Ages 60 – 63**

```
Catch-up rises:  $24,500 + $11,250 = $35,750
```

It **replaces** the $8,000, it does not stack. Four years only. → see Putting money in

Rule: IRC §414(v)(2)(E)(i); SECURE 2.0 §109.

---

## Distribution + Legacy Phase

### Age 62 — Retirement · $11.3M
*Shift to distributions*

Three separate things happen here:

- Social Security can be claimed, at roughly **70%** of the full amount → see Social Security
- Cost-of-living increases begin accruing **from this age**, whether or not
  the client claims → see Social Security
- Earned income stops, so **the conversion window opens** → see Taking money out

**Age 64:** catch-up drops back to $32,500. Payroll elections must be changed
or the client over-defers. → see Putting money in

---

### **Age 65**
*Not on the picture*

- Medicare starts — and the premium is set by income from **age 63** → see Medicare
- The extra standard deduction for age 65 begins → see Tax
- The senior deduction applies, **but only through 2028** → see Events

---

### **Age 67** — full retirement age
*Not on the picture*

The earnings test stops entirely. A client can work and claim with no
withholding at all. → see Social Security

---

### Age 70 — Distribution · $12.4M
*Coordinate tax-aware income*

Social Security reaches its maximum — about **124%**. Waiting beyond 70 adds
nothing.

**Age 70½:** charitable distributions straight from an IRA become available,
$111,000 a year. The only route that keeps money out of AGI entirely. → see Forced withdrawals

---

### **Age 73 or 75** — forced withdrawals begin
*Not on the picture, and it is the biggest tax event in the plan*

```
Born 1951-1959   start at 73
Born 1960+       start at 75
```

The conversion window **closes here**. Everything not converted before this
age is now forced out on the government's schedule, at the government's pace,
for the rest of the client's life. → see Forced withdrawals → see Taking money out

---

### Age 80 — Preservation · $13.9M
*Protect income + spouse*

The forced withdrawal is now taking about **5%** of the balance a year and
climbing. → see Forced withdrawals

"Protect spouse" is the right instruction. This is where the widow's penalty
becomes the main risk: brackets halve, thresholds drop, and the survivor keeps
one benefit instead of two. Conversions done **now** are the defence. → see Estate and family

Insurance needs its annual check from here — a policy with loans running
against it and rising internal costs can fail in the eighties. → see Life insurance

---

### Age 90 — Legacy · $14.8M
*Age 90+ continuity*

The forced withdrawal is now **8.2%** of the balance a year. Required income
has more than doubled since 73 while the balance has barely moved. → see Forced withdrawals

The default projection ends here. The $15.4M on the picture does not — it is
an age-100 figure. → see Checking the picture

---

### Age 100 — Legacy continuation · $15.4M
*Legacy remains visible*

---

### Death, and what the family actually receives

The estate value is not the net worth. Three things come off first:

```
federal estate tax  +  state estate tax  +  the heirs' income tax on pre-tax money
```

And several things the client was carrying simply vanish:

| | At death |
|---|---|
| Taxable accounts and property | basis steps up — prior gain erased |
| Pre-tax IRA / 401(k) | ordinary income to the heir, ten years to empty |
| Loss carryforwards | **extinguished** |
| Suspended passive losses | released only above the step-up |
| Life insurance | free of income tax; in the estate unless properly owned |

→ see Estate and family

---

## What the software shows for this

The milestone strip is hardcoded:

The age strip is a fixed list: 42, 45, 50, 55, your retirement age, 70, 80, 90, 100.

Two consequences:

- A client aged 50 loses the 42 and 45 cards and the strip looks broken.
- **59½, 65, 67 and the forced-withdrawal age are not on it** — the four ages
  that matter most in law are the four the client is never shown.

The picture's phase names — Foundation, Protection, Acceleration,
Multiplication — and the action text under each card exist nowhere in the UI.

**Also touches:** Checking the picture

---

## EVENTS

Each of these redirects the plan from the year it happens.

---

### The client retires earlier than planned.

Output: earned income stops sooner, so contributions stop sooner and the
deployable capital stops with them. The conversion window opens earlier and
lasts longer, which partly compensates.

Under 59½ the 10% extra tax is the binding constraint. Three ways round it:
leaving the job in or after the year of turning **55** and leaving the money in
that employer's plan; disability; or a fixed schedule of equal payments.

Rule: IRC §72(t)(2)(A)(v),(iii),(iv).

**Also touches:** Taking money out · Putting money in · The seven buckets

---

### The client becomes disabled.

Output: two separate problems. The tax one is easy — disability is a
recognised exception, so retirement money is reachable without the 10%.

The cash-flow one is harder and is the part clients do not expect:

```
Disability benefits      5-month waiting period with nothing
Medicare eligibility     24 months after that
```

That is roughly two and a half years to bridge from savings or a private
policy. Whether a private benefit is taxable depends on who paid the premium.

Rule: IRC §72(t)(2)(A)(iii), §72(m)(7); Social Security Act §223, §226(b).

**Also touches:** Life insurance · Spending and care · Social Security

---

### A spouse dies.

Output: the largest single event in the whole projection, and it moves five
things at once.

| | Effect |
|---|---|
| Filing status | joint for the year of death, single after |
| Brackets | roughly **halve** |
| Social Security | keeps the larger benefit, not both |
| Social Security taxed above | $32,000 → **$25,000** |
| Medicare surcharge starts at | $218,000 → **$109,000** |
| Spending | falls, but by far less than income |

Worked example: gross income **down 12%**, federal tax **up 29.5%**, cash
after tax **down 16.9%**.

The Medicare side **can** be appealed — death is a qualifying life event.

Rule: IRC §6013(a)(3), §1(j)(2), §86(c); 20 CFR §418.1205(a).

**Also touches:** Estate and family · Social Security · Medicare · Taking money out

---

### Divorce.

Output: accounts split without tax if done correctly — a court order for an
employer plan, a direct transfer for an IRA. Done as a withdrawal, it is taxed
and can carry the 10%.

Filing status is decided by the position on **31 December**, not by when the
process started. A decree in December means single for the whole year.

Divorce is a qualifying life event for the Medicare surcharge. A ten-year
marriage preserves a claim on the ex-spouse's Social Security record.

Rule: IRC §1041, §414(p), §408(d)(6), §7703(a); 20 CFR §418.1205.

**Also touches:** Estate and family · Social Security · Medicare

---

### The business is sold, or another windfall lands.

Output: one enormous year. The gain stacks on ordinary income, the 3.8% tax
reaches other income, the deduction limits bite, and the Medicare surcharge
arrives two years later and **cannot be appealed**.

Three levers, all of which must be pulled **before** the sale:
- qualifying C-corporation stock can be excluded, more the longer it is held
- taking the price in instalments spreads it across brackets and tiers
- charitable giving in the same year is at its most valuable

Rule: IRC §1(h), §1411, §1202, §453.

**Also touches:** Estate and family · Medicare · K-1 and business losses

---

### A property is sold.

Output: depreciation recapture is the surprise, and cost-segregated components
come back at ordinary rates. The sale also releases suspended losses on that
activity, which can offset a large part of the gain — but only if the whole
interest goes, to an unrelated party, in a fully taxable sale.

Rule: IRC §1245, §1250, §1(h)(1)(E), §469(g).

**Also touches:** Property · K-1 and business losses · Medicare

---

### The market falls.

Output: **the model cannot show this.** One flat rate is applied every year.
There is no crash, no recovery, and no modelling of the order returns arrive
in.

A poor return in the first years of drawing down does far more damage than the
same return later, because the client is selling assets to live on while they
are cheap. That risk is real and is simply not in the projection.

Say this plainly to any client who asks "what if the market drops?"

Rule: an assumption — and a stated limitation.

**Also touches:** Growth · Taking money out

---

### The insurance policy lapses.

Output: the tax-free income stream stops, the death benefit disappears, and a
large ordinary income bill arrives with no cash attached. Worked example:
$220,000 of gain, $52,800 of tax, $0 received.

The engine does test for this every year and writes a note. That note is the
warning.

Rule: IRC §72(e).

**Also touches:** Life insurance · Estate and family

---

### A forced withdrawal is missed.

Output: 25% of the amount that should have come out, cut to 10% if fixed
within two years, and waivable for reasonable error.

Each 401(k) carries its own shortfall, so taking everything from one plan
leaves a penalty waiting in each of the others.

Rule: IRC §4974.

**Also touches:** Forced withdrawals

---

### A 401(k) loan is outstanding when the client leaves the job.

Output: unrepaid, it becomes a taxable distribution, plus 10% if under 59½.
There is a rollover window — to the tax return due date including extensions —
to undo it. Most people never hear about the window.

Rule: IRC §72(p), §402(c)(3)(C).

**Also touches:** Taking money out

---

### Money is inherited.

Output: what arrives matters more than how much.

| Inherited | Cost to the heir |
|---|---|
| Taxable account or property | basis steps up, prior gain erased |
| Pre-tax IRA or 401(k) | ordinary income, ten years to empty, no step-up |
| Roth | tax-free, still ten years to empty |
| Life insurance | free of income tax |

Rule: IRC §1014, §691, §401(a)(9)(H), §101(a).

**Also touches:** Estate and family · Forced withdrawals

---

### The law changes mid-projection.

Three are already on the statute book and **must** be built in, not discovered
later:

| When | What |
|---|---|
| **2026** | the excess business loss threshold **fell** to $256,000 / $512,000, down 18.2% |
| **After 2028** | the senior deduction ends — taxable income rises $12,000 for a couple with no change in income |
| **2030** | the state and local deduction reverts to $10,000 |

Output: a projection to age 90 crosses all three. Anything that treats today's
rules as permanent is wrong from the start.

Rule: P.L. 119-21; IRC §461(l), §151(d)(5)(C), §164(b)(7).

**Also touches:** Tax · K-1 and business losses · Age by age

---

### The client moves state.

Output: changes income tax, and separately changes estate tax — the two are
not linked. A client leaving New York escapes both the income tax and the
cliff in the Estate and family cases. A client moving to Oregon picks up an estate tax starting near
$1,000,000.

Rule: state statute.

Missing: the engine takes one state for the whole projection. A mid-life move
is not modelled.

**Also touches:** Tax · Estate and family

---

## CHECKING THE PICTURE

Three answers only: **it works**, **needs a number the picture does not show**, or **cannot be worked out at all**.

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

Rule: the adviser supplies it — the adviser supplies all three numbers.

**Also touches:** The seven buckets (this is the number every bucket is a slice of)

---

## The nine milestone cards

### Age 42 shows $1.76M in year one, but only $272K was deployed.

Output: **needs an input the picture does not show.** $1.76M at the first
milestone means the client already had roughly $1.5M before the plan
started. The picture shows no starting capital.

The engine seeds two buckets from existing money — cash on hand into
liquidity, current real estate value into real estate. Those two inputs are what the
picture is hiding.

Missing: opening cash, opening real estate value, opening retirement balances.

**Also touches:** The seven buckets (seeding) · Growth (what it grows at)

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

Rule: our own calculation.

**Also touches:** Age by age (the age journey uses these same ages)

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

**Also touches:** Growth (return assumptions) · Taking money out (distributions)

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

**Also touches:** Forced withdrawals (required distributions inflate gross withdrawals) · Taking money out (withdrawal order)

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

**Also touches:** The seven buckets

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

**Also touches:** Taking money out (which income sources are actually tax-free) · Life insurance (policy loans are only tax-free while the policy stays alive)

---

## Age 90 or age 100?

The picture is titled "To Age 90+" and then prints three numbers at age 100.
The engine offers 90 or 100 as a choice.

Every figure quoted from this picture must name its age. "$15.4M legacy" is
an **age-100** figure. The age-90 figure is $14.8M.

**Also touches:** Age by age
