# 08 — Ending Estate Value

**Step 12 of the year loop** · Rail: **nominal**

---

## What this computes

If the client died in year *n*, what actually reaches the heirs after estate tax and after the income tax the heirs will owe.

This is the mockup's **"Projected Legacy at Age 100 — $15.4M"** figure. It is **not** the same as net worth. Two assets of identical market value can deliver very different amounts to heirs, because they are taxed differently on death.

---

## 1. The calculation, top to bottom

```
STEP 1   Gross estate            (everything the decedent owned or controlled)
STEP 2   − Debts, funeral, administration expenses
STEP 3   − Marital deduction     (unlimited, to a US-citizen spouse)
STEP 4   − Charitable deduction
                                 = TAXABLE ESTATE
STEP 5   + Adjusted taxable gifts (lifetime gifts above the annual exclusion)
STEP 6   − Applicable exclusion  ($15,000,000 in 2026, + any DSUE ported from a spouse)
                                 = AMOUNT SUBJECT TO TAX
STEP 7   × 40%                   = ESTATE TAX
STEP 8   − Income tax the heirs will owe on IRD assets
                                 = NET TO HEIRS
```

**Step 8 is the step most models omit**, and it is the difference between a headline number and a true one.

---

## 2. The 2026 numbers

Source: **IRS Rev. Proc. 2025-32**, reflecting the One Big Beautiful Bill Act.

| Item | 2026 value |
|---|---|
| Basic exclusion amount (per person) | **$15,000,000** |
| Married couple, with portability | **$30,000,000** |
| Top estate tax rate | **40%** |
| Annual gift exclusion (per recipient) | **$19,000** |
| Gift to non-citizen spouse | $194,000 |
| GST exemption | $15,000,000 |

> **OBBBA made the $15M exclusion permanent** and indexed to inflation. The scheduled 2026 drop to roughly $7M **did not happen**. Any model or article written before July 2025 that assumes a sunset is now wrong.

### Portability (DSUE)

The surviving spouse may add the deceased spouse's unused exclusion — but **only if a Form 706 is filed** for the first death, even when no tax is due.

```
survivorExclusion = ownExclusion + DSUE
```

> The election is easy to miss and the consequence is a permanently lost $15M exclusion. Flag it in the output.

---

## 3. Building the gross estate

| Asset | Included at | Code |
|---|---|---|
| Retirement accounts (pre-tax) | Full balance | §2033 |
| Roth accounts | Full balance | §2033 |
| Taxable brokerage | Fair market value | §2033 |
| Real estate | Fair market value | §2033 |
| Business interests | FMV, discounts may apply | §2031 |
| **Life insurance — personally owned** | **Full death benefit** | **§2042** |
| **Life insurance — in an ILIT** | **$0** | **§2042 (excluded)** |
| Gifts within 3 years (insurance only) | Pulled back in | §2035 |

---

## 4. Life insurance — the ownership question

This is the single largest lever in the whole estate calculation.

```
IF decedent held ANY "incident of ownership":
    grossEstate = grossEstate + fullDeathBenefit     ← taxed at 40%
ELSE (properly structured ILIT):
    grossEstate unchanged                            ← passes entirely outside the estate
```

**Incidents of ownership** include the right to: change the beneficiary, surrender or cancel the policy, assign it, revoke an assignment, or pledge it for a loan. Any one of them is enough.

**Worked number** — $5,000,000 policy, estate already above the exclusion:

| Ownership | Added to estate | Estate tax at 40% | Net to heirs |
|---|---|---|---|
| Personally owned | $5,000,000 | $2,000,000 | **$3,000,000** |
| Held in an ILIT | $0 | $0 | **$5,000,000** |

A $2,000,000 difference from a titling decision alone.

### The three-year rule (§2035)

Transferring an existing policy into an ILIT and dying within **three years** pulls the full death benefit back into the estate. The ILIT should therefore **purchase the policy directly** rather than receive a transfer.

---

## 5. Basis at death — the split that decides everything

### §1014 — assets that DO step up

Basis resets to fair market value at death. **All unrealised capital gain disappears.**

| Asset | Result |
|---|---|
| Taxable brokerage | Gain wiped out |
| Real estate | Gain **and depreciation recapture** wiped out |
| Business interests | Gain wiped out |

```
heirBasis = fairMarketValueAtDeath
```

### §691 — IRD assets that do NOT step up

**Income in Respect of a Decedent** is income the decedent earned but never paid tax on. There is **no step-up**. Heirs pay ordinary income tax on the full amount.

| Asset | Result |
|---|---|
| Traditional IRA / 401(k) | **100% taxable** to heirs as ordinary income |
| Annuities (gain portion) | Taxable |
| Accrued but unpaid comp | Taxable |
| **Roth IRA / Roth 401(k)** | **Tax-free** — no income tax at all |

> **This is the core insight of the whole estate module.** A $3M traditional IRA and a $3M brokerage account look identical on a net-worth statement. After death they are not remotely equal:

| | $3M traditional IRA | $3M brokerage (with $1M gain) |
|---|---|---|
| Estate tax exposure | $3M | $3M |
| Heirs' income tax | ~$1.11M (37%) | **$0** — stepped up |
| Net to heirs | **$1.89M** | **$3.00M** |

### The 10-year rule

Under SECURE 1.0, most non-spouse beneficiaries must empty an inherited IRA **within 10 years**. Combined with the heirs' own peak earning years, this often means distribution at the **highest** marginal rates.

### §691(c) — the deduction that prevents double taxation

If estate tax was actually paid on the IRD asset, heirs get an income tax deduction for that portion.

```
IF estateTaxPaid > 0:
    ird691cDeduction = estateTax attributable to the IRD asset
    heirTaxableAmount = irdAmount − ird691cDeduction
```

> **Estate tax must actually have been paid** to claim this. Below the $15M exclusion there is no estate tax, so no §691(c) deduction — but also no double tax to relieve.

---

## 6. Net to heirs — the honest number

```
netToHeirs = grossEstate
           − debts
           − estateTax
           − heirIncomeTaxOnIRD
           + lifeInsuranceOutsideEstate
```

Where:

```
heirIncomeTaxOnIRD = (pretaxRetirementBalance − ird691cDeduction) × heirMarginalRate
```

Use the **heirs'** marginal rate, not the decedent's. Absent better information, 32–37% is a reasonable assumption for adult children of a high-net-worth client.

**Worked number** — $12M estate, below the exclusion:

| Component | Value |
|---|---|
| Pre-tax retirement | $4,000,000 |
| Roth | $1,000,000 |
| Taxable brokerage | $2,000,000 |
| Real estate equity | $2,000,000 |
| Life insurance (ILIT) | $3,000,000 |
| **Gross estate (excl. ILIT)** | **$9,000,000** |
| Estate tax (below $15M exclusion) | **$0** |
| Heirs' income tax on the $4M IRA at 35% | **−$1,400,000** |
| **Net to heirs** | **$10,600,000** |

Headline net worth is $12,000,000. The real legacy is **$10,600,000**. The $1.4M gap is invisible unless IRD is modelled.

---

## 6b. The first death — what must happen, and when

Most planning attention goes to the second death. The **first** death is where the irreversible decisions are made.

### Portability has a deadline

```
DSUE requires Form 706 to be FILED — it is never automatic
Standard deadline:  9 months after death (+6 month extension)
Late relief:        up to 5 YEARS after death, under Rev. Proc. 2022-32
                    print at the top of the return:
                    "FILED PURSUANT TO REV. PROC. 2022-32 TO ELECT
                     PORTABILITY UNDER § 2010(c)(5)(A)"
```

> A $15,000,000 exclusion is lost permanently if nobody files. Estates well below the filing threshold still **should** file, precisely because no tax is due and the exclusion is worth carrying forward.

### The step-up at the first death depends on the state

```
COMMUNITY PROPERTY state:  BOTH halves step up          → 100%
COMMON LAW state:          only the decedent's half     → 50%
```

**Community property states:** Arizona, California, Idaho, Louisiana, Nevada, New Mexico, Texas, Washington, Wisconsin (plus elective regimes in Alaska, Tennessee, South Dakota, Florida and Kentucky).

**Worked contrast** — a $2,000,000 jointly held asset with a $1,000,000 basis, first spouse dies:

| | Community property | Common law |
|---|---|---|
| Step-up | **100%** — full $2,000,000 | **50%** — $1,500,000 |
| Built-in gain remaining | **$0** | **$500,000** |
| Tax if sold at 23.8% | **$0** | **$119,000** |

> Same asset, same death, **$119,000 apart** — decided by which state the couple lived in. A client moving from California to a common law state loses this treatment unless the community property character is preserved.

## 7. State estate and inheritance taxes

Federal is not the whole story. Roughly **17 states plus DC impose some form of death tax** — around a dozen levy a state **estate** tax, five (NJ, PA, NE, KY, MD) levy an **inheritance** tax on the recipient, and Maryland has both.

Several have **far lower** exclusions than the federal $15M:

| State | Approximate exclusion |
|---|---|
| **Oregon** | **$1,000,000** |
| **Massachusetts** | **$2,000,000** |
| Connecticut | matches federal (~$13–15M) |

> A client in Oregon with a $5M estate owes **zero federal** estate tax and a meaningful **state** estate tax. Model the state layer separately, driven by the client's state of domicile.

> **Massachusetts quirk:** once the exclusion is exceeded, Massachusetts taxes the **entire** estate from the first dollar, not just the excess. A cliff, not a threshold.

State exclusions change frequently and several are **not** inflation-indexed. Verify the client's state annually rather than hard-coding.

---

## Ordering traps

| Don't | Do |
|---|---|
| Report net worth as the legacy figure | Subtract the heirs' income tax on IRD |
| Step up a traditional IRA | IRD assets never step up |
| Include ILIT-owned insurance in the estate | Excluded under §2042 — if truly no incidents of ownership |
| Assume the exclusion drops to ~$7M in 2026 | OBBBA made **$15M** permanent |
| Assume portability is automatic | Requires a filed Form 706 — up to 5 years late under Rev. Proc. 2022-32 |
| Skip Form 706 because no tax is due | That is exactly when it should be filed, to preserve the DSUE |
| Apply a 50% step-up in a community property state | Community property gets **100%** on the first death |
| Ignore the §2035 three-year rule | A transferred policy is pulled back for 3 years |
| Apply depreciation recapture to property held to death | §1014 wipes it out |
| Model only federal estate tax | ~17 states + DC have a death tax; Oregon starts at $1M |
| Claim §691(c) when no estate tax was paid | It requires estate tax actually paid |

---

## Sources

| What | Source | Google this |
|---|---|---|
| 2026 exclusion, gift exclusion, 40% rate | [IRS Rev. Proc. 2025-32](https://www.irs.gov/newsroom/irs-releases-tax-inflation-adjustments-for-tax-year-2026-including-amendments-from-the-one-big-beautiful-bill) · [IRS — What's New, Estate and Gift Tax](https://www.irs.gov/businesses/small-businesses-self-employed/whats-new-estate-and-gift-tax) | `IRS 2026 estate tax basic exclusion amount 15 million` |
| §1014 step-up | [26 U.S.C. §1014](https://www.law.cornell.edu/uscode/text/26/1014) | `IRC 1014 basis of property acquired from a decedent` |
| §691 IRD and §691(c) deduction | [26 U.S.C. §691](https://www.law.cornell.edu/uscode/text/26/691) · [Kitces on the IRD deduction](https://www.kitces.com/blog/understanding-the-irc-section-691c-income-in-respect-of-a-decedent-ird-deduction-for-the-beneficiary-of-an-inherited-ira/) | `IRC 691(c) income in respect of a decedent deduction inherited IRA` |
| §2042 insurance inclusion | [26 U.S.C. §2042](https://www.law.cornell.edu/uscode/text/26/2042) | `IRC 2042 life insurance proceeds incidents of ownership` |
| §2035 three-year rule | [26 U.S.C. §2035](https://www.law.cornell.edu/uscode/text/26/2035) | `IRC 2035 three year rule life insurance transfer` |
| Portability / DSUE | [IRS — Form 706 instructions](https://www.irs.gov/instructions/i706) | `Form 706 portability DSUE election instructions` |
| State estate / inheritance taxes | [Tax Foundation — estate and inheritance taxes by state](https://taxfoundation.org/data/all/state/estate-inheritance-taxes/) | `states with estate tax inheritance tax 2026 exemption` |
| Late portability relief, 5 years | [Rev. Proc. 2022-32](https://www.irs.gov/pub/irs-drop/rp-22-32.pdf) | `Rev Proc 2022-32 late portability election five years` |
| Community property 100% step-up | IRC §1014(b)(6) | `IRC 1014(b)(6) community property double step up basis` |
