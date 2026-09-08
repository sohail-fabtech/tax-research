# 15 — The journey, age by age

The picture's nine cards, plus the ages the law actually cares about. The
picture's ages are marketing milestones; the ones in **bold** below are legal
dates where something changes whether the client plans for it or not.

---

## Contribution Phase

### Age 42 — Foundation · $1.76M
*Implement Perfect Tax Plan layers*

The plan starts. Tax savings begin being deployed rather than spent.

The $1.76M is not built from the $272,000 — it is mostly money the client
already had. The picture does not say so. → `17`

Links to: → `14` → `01`

---

### Age 45 — Protection · $3.05M
*Lock annual planning rhythm*

Nothing changes in law at 45. This is a review cadence, not a tax date.

If there is a K-1 or a rental in the plan, this is where suspended losses
start accumulating quietly. Nobody sees them, because the software does not
show them. → `10`

---

### **Age 50** — Acceleration · $5.25M
*Scale wealth buckets*

```
401(k) catch-up opens:  $24,500 + $8,000 = $32,500
```

Rule: `RULE` — IRC §414(v). → `04`

---

### **Age 55** — Multiplication · $7.90M
*Retirement stress test*

The **Rule of 55** becomes available: leave the job in or after the year of
turning 55, and money in **that employer's plan** is reachable with no 10%
extra tax.

Roll it to an IRA first and the exception is gone forever. This is the most
commonly destroyed exception in the whole system. → `12`

Rule: `RULE` — IRC §72(t)(2)(A)(v).

---

### **Age 59½**
*Not on the picture, and it should be*

The 10% additional tax ends. Every retirement account becomes reachable
without an exception.

This is a more significant date for most clients than 55 or 62, and the
picture skips it entirely.

Rule: `RULE` — IRC §72(t). → `12`

---

### **Ages 60 – 63**

```
Catch-up rises:  $24,500 + $11,250 = $35,750
```

It **replaces** the $8,000, it does not stack. Four years only. → `04`

Rule: `RULE` — IRC §414(v)(2)(E)(i); SECURE 2.0 §109.

---

## Distribution + Legacy Phase

### Age 62 — Retirement · $11.3M
*Shift to distributions*

Three separate things happen here:

- Social Security can be claimed, at roughly **70%** of the full amount → `06`
- Cost-of-living increases begin accruing **from this age**, whether or not
  the client claims → `06`
- Earned income stops, so **the conversion window opens** → `12`

**Age 64:** catch-up drops back to $32,500. Payroll elections must be changed
or the client over-defers. → `04`

---

### **Age 65**
*Not on the picture*

- Medicare starts — and the premium is set by income from **age 63** → `11`
- The extra standard deduction for age 65 begins → `02`
- The senior deduction applies, **but only through 2028** → `16`

---

### **Age 67** — full retirement age
*Not on the picture*

The earnings test stops entirely. A client can work and claim with no
withholding at all. → `06`

---

### Age 70 — Distribution · $12.4M
*Coordinate tax-aware income*

Social Security reaches its maximum — about **124%**. Waiting beyond 70 adds
nothing.

**Age 70½:** charitable distributions straight from an IRA become available,
$111,000 a year. The only route that keeps money out of AGI entirely. → `07`

---

### **Age 73 or 75** — forced withdrawals begin
*Not on the picture, and it is the biggest tax event in the plan*

```
Born 1951-1959   start at 73
Born 1960+       start at 75
```

The conversion window **closes here**. Everything not converted before this
age is now forced out on the government's schedule, at the government's pace,
for the rest of the client's life. → `07` → `12`

---

### Age 80 — Preservation · $13.9M
*Protect income + spouse*

The forced withdrawal is now taking about **5%** of the balance a year and
climbing. → `07`

"Protect spouse" is the right instruction. This is where the widow's penalty
becomes the main risk: brackets halve, thresholds drop, and the survivor keeps
one benefit instead of two. Conversions done **now** are the defence. → `13`

Insurance needs its annual check from here — a policy with loans running
against it and rising internal costs can fail in the eighties. → `08`

---

### Age 90 — Legacy · $14.8M
*Age 90+ continuity*

The forced withdrawal is now **8.2%** of the balance a year. Required income
has more than doubled since 73 while the balance has barely moved. → `07`

The default projection ends here. The $15.4M on the picture does not — it is
an age-100 figure. → `17`

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

→ `13`

---

## What the software shows for this

The milestone strip is hardcoded at [index.html:1947](../index.html#L1947):

```js
const miles = [42,45,50,55,meta.retAge,70,80,90,100].filter(a => a >= meta.startAge ...)
```

Two consequences:

- A client aged 50 loses the 42 and 45 cards and the strip looks broken.
- **59½, 65, 67 and the forced-withdrawal age are not on it** — the four ages
  that matter most in law are the four the client is never shown.

The picture's phase names — Foundation, Protection, Acceleration,
Multiplication — and the action text under each card exist nowhere in the UI.

Links to: → `00` → `17`
