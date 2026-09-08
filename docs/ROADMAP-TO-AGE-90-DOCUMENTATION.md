# Roadmap to Age 90 — Reference Documentation

**Tax year:** 2026 · **As of:** September 2026 · **Jurisdiction:** United States, federal

A reference work covering every rule that affects the Roadmap to Age 90 projection. One section per rule, each built to the same structure, with the governing statute, the calculation, the tables, worked examples, and a plain statement of what this system does and does not apply.

All 41 sections are complete. Each was written and verified against primary sources between the dates recorded in Appendix A, and each is final unless a source changes. Appendix B records 25 defects found in the software while writing them.

---

## How this document is built

### Sourcing

Primary government sources only. Verified reachable and used: `irs.gov` (newsroom, `/pub/irs-drop/`, `/pub/irs-pdf/`, `/irb/`), `federalregister.gov`, `ecfr.gov`, `cms.gov`, `govinfo.gov`, and `secure.ssa.gov/poms.nsf`.

`www.ssa.gov` returns 403 and `uscode.house.gov` refuses connections from this environment. Substitutions: the Federal Register for annual Social Security figures, eCFR title 20 for the rules themselves, POMS for operating detail, and govinfo for United States Code text.

Search is used only with results restricted to a government domain, and only to locate a URL. The page is then retrieved and quoted. A search result is never itself a citation — during the drafting of the RMD section a search returned the 2025 qualified charitable distribution limit of $108,000 as though it were current; the primary source shows $111,000 for 2026.

Never cited: Investopedia, NerdWallet, SmartAsset, Kiplinger, Forbes, Motley Fool, Yahoo Finance, Google Finance, Wikipedia, CPA-firm marketing pages, AI-generated summary sites. Tax Foundation is a formatting reference, not a source.

### Verification

Every figure passes a three-way check — primary source, the constants register in `../10-SOURCES-AND-COMPETITORS.md`, and the frozen `C` object in `../index.html`. A disagreement is resolved at source and recorded, never reconciled silently.

Whether this system applies a given rule is established by reading the implementing function, never by searching for keywords. Statute numbers do not appear in code comments and code identifiers do not match legal vocabulary. When this documentation was scoped, a keyword sweep reported roughly 40 percent false positives in both directions — it flagged the §199A wage limit, the Uniform Lifetime Table, the §402(g) limit and the $25,000 allowance phase-out as missing when all four are implemented, and it reported matches for §1245, GST and WEP that were substring collisions.

All arithmetic is machine-computed. Where a source publishes its own worked example, it is reproduced and the agreement noted.

### Structure of each section

Twelve parts, in fixed order: 1 Overview and Purpose · 2 Governing Law and Authorities · 3 Key Definitions · 4 Who Is Affected · 5 Core Rules and Calculations · 6 Examples and Case Calculations · 7 Interactions with Other Rules · 8 Common Scenarios and Edge Cases · 9 Planning Implications · 10 Data Tables for the Engine · 11 References · 12 Status in This System.

Part 5 opens with a **Case Register** — every case the rule contains and whether this system applies it. Completeness there is what prevents an omission from becoming a wrong number. Part 12 records what the projection engine and the `tax-be` backend actually do.

---

## Contents

| # | Section | Tier | Status |
|---|---|---|---|
| **A** | **Income Tax and Filing** | | |
| 01 | Federal Income Tax Rate Schedules | Table | **Complete** |
| 02 | Standard Deduction, Itemised Deductions and the Age-65 Addition | Standard | **Complete** |
| 03 | Filing Status | Standard | **Complete** |
| **B** | **Payroll and Medicare Taxes** | | |
| 04 | Social Security and Medicare Taxes | Standard | **Complete** |
| 05 | Additional Medicare Tax | Table | **Complete** |
| 06 | Net Investment Income Tax | Standard | **Complete** |
| **C** | **Retirement Accounts and Distributions** | | |
| 07 | 401(k), 403(b) and 457 Contribution Limits | Standard | **Complete** |
| 08 | IRA Contribution Limits and Rules | Standard | **Complete** |
| 09 | Required Minimum Distributions | Deep | **Complete** |
| 10 | Roth IRA and Roth 401(k) | Standard | **Complete** |
| **D** | **Social Security** | | |
| 11 | Retirement Benefits | Standard | **Complete** |
| 12 | Spousal and Survivor Benefits | Deep | **Complete** |
| 13 | Children's Benefits and the Family Maximum | Standard | **Complete** |
| 14 | Taxation of Benefits | Standard | **Complete** |
| **E** | **Medicare** | | |
| 15 | Medicare Part A, Part B and Part D Premiums | Standard | **Complete** |
| 16 | Income-Related Monthly Adjustment Amount | Standard | **Complete** |
| **F** | **Business Income and Deductions** | | |
| 17 | Qualified Business Income | Deep | **Complete** |
| 18 | Excess Business Loss | Standard | **Complete** |
| 19 | Self-Employment Income and Business Deductions | Standard | **Complete** |
| **G** | **Real Estate and Rentals** | | |
| 20 | Personal Use and Vacation Homes | Standard | **Complete** |
| 21 | Short-Term Rentals and the Seven-Day Rule | Deep | **Complete** |
| 22 | Depreciation, Cost Segregation and Recapture | Deep | **Complete** |
| 23 | At-Risk Rules for Real Estate | Standard | **Complete** |
| **H** | **Investments, Losses and Carryforwards** | | |
| 24 | Capital Gains and Losses | Standard | **Complete** |
| 25 | Passive Activity Losses | Deep | **Complete** |
| 26 | Basis in Partnerships and S Corporations | Deep | **Complete** |
| 27 | Net Operating Losses | Standard | **Complete** |
| **I** | **Estate, Gifts and Insurance** | | |
| 28 | Federal Estate Tax | Deep | **Complete** |
| 29 | Gift Tax | Standard | **Complete** |
| 30 | Life Insurance and Estate Inclusion | Standard | **Complete** |
| 31 | Step-Up in Basis at Death | Standard | **Complete** |
| **J** | **Medical, Long-Term Care and Living Costs** | | |
| 32 | Medical Expense Deduction | Standard | **Complete** |
| 33 | Long-Term Care | Standard | **Complete** |
| 34 | Health Savings Accounts | Standard | **Complete** |
| **K** | **Life Events** | | |
| 35 | Death of a Spouse | Deep | **Complete** |
| 36 | Divorce | Standard | **Complete** |
| 37 | Disability and Early Retirement | Standard | **Complete** |
| 38 | Windfalls and One-Time Gains | Standard | **Complete** |
| **L** | **Methodology** | | |
| 39 | Tax Savings Deployment Framework | Standard | **Complete** |
| **M** | **Reference** | | |
| 40 | Glossary | Table | **Complete** |
| 41 | Index of Code Sections | Table | **Complete** |
| — | Appendix A — Verification Log | | **Current** |
| — | Appendix B — Defects on Record | | **Current** |

---

## Module 01 — Federal Income Tax Rate Schedules

**Tax year:** 2026 · **As of:** September 2026 · **Primary authority:** IRC § 1

---

### 1. Overview and Purpose

Section 1 of the Internal Revenue Code imposes the federal income tax and sets the rate schedules that convert taxable income into tax. Seven rates apply — 10, 12, 22, 24, 32, 35 and 37 percent — and the income at which each begins depends on filing status.[1]

The schedules are progressive and marginal. A rate applies only to the income falling within its own band, not to the whole of taxable income. A married couple with $217,800 of taxable income reaches the 24 percent bracket, but pays 24 percent on $6,400 of it and less on everything below. Their tax is $37,468, an effective rate on taxable income of 17.20 percent. The distinction between the marginal rate and the effective rate is the single most common source of misunderstanding in retirement planning, and the two figures answer different questions: the effective rate describes the year that has happened, the marginal rate governs every decision about the next dollar.

For a projection running to age 90, the rate schedules matter in a way that a single-year return does not reveal. The brackets are indexed annually, so their position moves with inflation; several thresholds that interact with them are not indexed and do not move at all. Over a forty-eight year horizon that divergence compounds, and it is the reason this system computes tax in nominal dollars and deflates only at the point of display.

### 2. Governing Law and Authorities

| Type | Citation | What it establishes |
|---|---|---|
| Statute | IRC § 1(a)–(d) | Imposition of tax; the four individual rate schedules |
| Statute | IRC § 1(j) | The rate structure and bracket thresholds in effect for 2026 |
| Statute | IRC § 1(f) | Annual inflation adjustment, measured by C-CPI-U |
| Statute | IRC § 1(h) | Maximum rate on net capital gain |
| Statute | IRC § 1(g) | Tax on the unearned income of certain children |
| Legislation | P.L. 119-21 (One Big Beautiful Bill Act) | Made the § 1(j) structure permanent and revised related provisions |
| Guidance | Rev. Proc. 2025-32, § 3.01 | The 2026 rate tables reproduced below |

The rate schedules for 2026 were published by the Internal Revenue Service in Revenue Procedure 2025-32.[2] Every figure in this module is taken from that document.

### 3. Key Definitions

| Term | Definition |
|---|---|
| **Taxable income** | Gross income less deductions allowed by chapter 1, including the standard or itemized deduction. It is the figure the rate schedules operate on — not gross income, and not adjusted gross income. |
| **Marginal rate** | The rate applied to the next dollar of ordinary income. |
| **Effective rate** | Total tax divided by a stated base. The base must always be identified, because the effective rate on taxable income and the effective rate on gross income are different numbers. |
| **Bracket** | A band of taxable income to which a single rate applies. |
| **Indexing** | Annual adjustment of a threshold under § 1(f), measured by the Chained Consumer Price Index for All Urban Consumers (C-CPI-U). |
| **Surviving spouse** | A taxpayer entitled under § 2(a) to use the joint-return rate schedule for the two years following the year of a spouse's death. |

### 4. Who Is Affected

Every individual with taxable income. The applicable schedule is determined by filing status:

| Status | Schedule | Note |
|---|---|---|
| Married filing jointly | § 1(j)(2)(A) | Widest brackets |
| Surviving spouse | § 1(j)(2)(A) | Same schedule as joint; available for two years after the year of death |
| Head of household | § 1(j)(2)(B) | Requires a qualifying person and more than half the cost of maintaining a household |
| Unmarried (single) | § 1(j)(2)(C) | |
| Married filing separately | § 1(j)(2)(D) | Matches the single schedule until the top bracket, which begins far lower |
| Estates and trusts | § 1(j)(2)(E) | Reaches 37 percent at $16,000 |

Marital status is determined as of the last day of the taxable year, subject to the rules of § 7703 for taxpayers living apart.

### 5. Core Rules and Calculations

#### 5.1 Case Register

Every case within this rule, and whether this system applies it.

| # | Case | Applied |
|---|---|---|
| 1 | Seven-rate progressive schedule | Yes |
| 2 | Married filing jointly schedule | Yes |
| 3 | Surviving spouse uses the joint schedule | Yes |
| 4 | Head of household schedule | Yes |
| 5 | Single schedule | Yes |
| 6 | Married filing separately schedule, with its lower top bracket | Yes |
| 7 | Estate and trust schedule | Not applicable — the projection models individuals |
| 8 | Annual indexing under § 1(f) | Yes — thresholds inflate forward |
| 9 | Adjusted net capital gain at 0 / 15 / 20 percent | Yes |
| 10 | Ordinary income stacked below capital gain | Yes |
| 10a | Unrecaptured § 1250 gain at 25 percent | **No** — see § 12 |
| 10b | 28-percent rate gain on collectibles and § 1202 gain | **No** — see § 12 |
| 10c | § 163(d)(4)(B)(iii) election to treat gain as investment income | **No** |
| 11 | Filing status change on death of a spouse | Yes |
| 12 | § 7703 determination for taxpayers living apart | No — status is taken as given |
| 13 | Kiddie tax under § 1(g) | No — see § 12 |

#### 5.2 The computation

Tax is computed by applying each rate to the portion of taxable income falling in its band, and summing:

```
tax = Σ over brackets b of  rate(b) × [ min(taxableIncome, ceiling(b)) − floor(b) ]
      for every b where taxableIncome > floor(b)
```

Net capital gain and qualified dividends are removed from this computation and taxed separately under § 1(h). Ordinary income is stacked first, and the capital gain rate is determined by where the gain sits on top of it.

#### 5.3 2026 rate schedules

**Married individuals filing joint returns and surviving spouses — § 1(j)(2)(A)**

| Taxable income | Tax |
|---|---|
| Not over $24,800 | 10% of taxable income |
| Over $24,800, not over $100,800 | $2,480 + 12% of the excess over $24,800 |
| Over $100,800, not over $211,400 | $11,600 + 22% of the excess over $100,800 |
| Over $211,400, not over $403,550 | $35,932 + 24% of the excess over $211,400 |
| Over $403,550, not over $512,450 | $82,048 + 32% of the excess over $403,550 |
| Over $512,450, not over $768,700 | $116,896 + 35% of the excess over $512,450 |
| Over $768,700 | $206,583.50 + 37% of the excess over $768,700 |

**Heads of households — § 1(j)(2)(B)**

| Taxable income | Tax |
|---|---|
| Not over $17,700 | 10% of taxable income |
| Over $17,700, not over $67,450 | $1,770 + 12% of the excess over $17,700 |
| Over $67,450, not over $105,700 | $7,740 + 22% of the excess over $67,450 |
| Over $105,700, not over $201,750 | $16,155 + 24% of the excess over $105,700 |
| Over $201,750, not over $256,200 | $39,207 + 32% of the excess over $201,750 |
| Over $256,200, not over $640,600 | $56,631 + 35% of the excess over $256,200 |
| Over $640,600 | $191,171 + 37% of the excess over $640,600 |

**Unmarried individuals other than surviving spouses and heads of households — § 1(j)(2)(C)**

| Taxable income | Tax |
|---|---|
| Not over $12,400 | 10% of taxable income |
| Over $12,400, not over $50,400 | $1,240 + 12% of the excess over $12,400 |
| Over $50,400, not over $105,700 | $5,800 + 22% of the excess over $50,400 |
| Over $105,700, not over $201,775 | $17,966 + 24% of the excess over $105,700 |
| Over $201,775, not over $256,225 | $41,024 + 32% of the excess over $201,775 |
| Over $256,225, not over $640,600 | $58,448 + 35% of the excess over $256,225 |
| Over $640,600 | $192,979.25 + 37% of the excess over $640,600 |

**Married individuals filing separate returns — § 1(j)(2)(D)**

| Taxable income | Tax |
|---|---|
| Not over $12,400 | 10% of taxable income |
| Over $12,400, not over $50,400 | $1,240 + 12% of the excess over $12,400 |
| Over $50,400, not over $105,700 | $5,800 + 22% of the excess over $50,400 |
| Over $105,700, not over $201,775 | $17,966 + 24% of the excess over $105,700 |
| Over $201,775, not over $256,225 | $41,024 + 32% of the excess over $201,775 |
| Over $256,225, not over $384,350 | $58,448 + 35% of the excess over $256,225 |
| Over $384,350 | $103,291.75 + 37% of the excess over $384,350 |

**Estates and trusts — § 1(j)(2)(E)**

| Taxable income | Tax |
|---|---|
| Not over $3,300 | 10% of taxable income |
| Over $3,300, not over $11,700 | $330 + 24% of the excess over $3,300 |
| Over $11,700, not over $16,000 | $2,346 + 35% of the excess over $11,700 |
| Over $16,000 | $3,851 + 37% of the excess over $16,000 |

The separate-return schedule is not simply half the joint schedule. It tracks the single schedule through the 32 percent bracket and then reaches 37 percent at $384,350, while a single filer does not reach that rate until $640,600.

#### 5.4 Net capital gain — § 1(h)

Section 1(h) does not impose a single preferential rate. It imposes four, and the 0, 15 and 20 percent rates apply only to **adjusted net capital gain** — net capital gain reduced by unrecaptured section 1250 gain and by 28-percent rate gain, then increased by qualified dividend income.[8]

| Component | Rate | What it is |
|---|---|---|
| Adjusted net capital gain | 0 / 15 / 20% | Ordinary long-term gain and qualified dividends |
| Unrecaptured § 1250 gain | **25%** | Depreciation previously taken on real property, recaptured on sale |
| 28-percent rate gain | **28%** | Collectibles gain plus § 1202 gain, net of collectibles loss, net short-term capital loss, and long-term capital loss carried forward |

The breakpoints for the 0, 15 and 20 percent rates for 2026 are:[2]

| Filing status | 0% up to | 15% up to | 20% above |
|---|---|---|---|
| Married filing jointly and surviving spouse | $98,900 | $613,700 | $613,700 |
| Head of household | $66,200 | $579,600 | $579,600 |
| Single | $49,450 | $545,500 | $545,500 |
| Married filing separately | $49,450 | $306,850 | $306,850 |
| Estates and trusts | $3,300 | $16,250 | $16,250 |

These thresholds are measured against total taxable income, with ordinary income counted first. A taxpayer with $40,000 of ordinary taxable income and $30,000 of long-term gain filing jointly pays nothing on the gain, because the total remains below $98,900.

The 25 and 28 percent rates are **ceilings, not flat rates**. Where a taxpayer's ordinary rate is below the stated figure, the lower rate applies. A retiree in the 12 percent bracket selling a rental property does not pay 25 percent on the depreciation component; the 25 percent operates only as a cap.

Two further points affect the calculation. Net capital gain is reduced by any amount the taxpayer elects to treat as investment income under § 163(d)(4)(B)(iii), which trades preferential rate treatment for a current investment interest deduction. And gain on the sale of a partnership or S corporation interest attributable to unrealised appreciation in collectibles is itself treated as collectibles gain, so the 28 percent component can arise without the taxpayer having sold a collectible directly.

### 6. Examples and Case Calculations

All figures below are computed, not estimated.

#### Example 1 — Married couple, $250,000 of gross income

Standard deduction of $32,200 gives taxable income of $217,800.

| Rate | Applied to | Tax |
|---|---|---|
| 10% | $24,800 | $2,480.00 |
| 12% | $76,000 | $9,120.00 |
| 22% | $110,600 | $24,332.00 |
| 24% | $6,400 | $1,536.00 |
| | **Total** | **$37,468.00** |

Marginal rate 24 percent. Effective rate 17.20 percent of taxable income, 14.99 percent of gross income. The couple has crossed into the 24 percent bracket by $6,400, so a deduction of that size would remove $1,536 of tax; a deduction of $10,000 would remove $1,536 at 24 percent and the remaining $3,600 at 22 percent.

#### Example 2 — Single filer, $95,000 of gross income

Standard deduction of $16,100 gives taxable income of $78,900.

| Rate | Applied to | Tax |
|---|---|---|
| 10% | $12,400 | $1,240.00 |
| 12% | $38,000 | $4,560.00 |
| 22% | $28,500 | $6,270.00 |
| | **Total** | **$12,070.00** |

Marginal rate 22 percent, effective rate 15.30 percent of taxable income.

#### Example 3 — The change of schedule on the death of a spouse

Taxable income of $180,000, held constant, taxed first under the joint schedule and then under the single schedule.

| Schedule | Tax | Marginal rate |
|---|---|---|
| Married filing jointly | $29,024.00 | 22% |
| Single | $35,798.00 | 24% |
| **Difference** | **+$6,774.00** | **+23.3%** |

Identical income, $6,774 more tax. In practice a survivor's income also falls, because the smaller of the two Social Security benefits ends. The combination — less income, taxed on a narrower schedule — is the effect commonly called the widow's penalty, and it is treated in full in Module 35.

#### Verification against the source

Applying the computation in § 5.2 to the top of each schedule reproduces the cumulative amounts printed in Revenue Procedure 2025-32 exactly: $206,583.50 at $768,700 for joint filers, and $192,979.25 at $640,600 for single filers.[2] Agreement at these points confirms both the thresholds and the arithmetic.

### 7. Interactions with Other Rules

**Standard deduction (Module 02).** The rate schedules operate on taxable income, so the deduction determines where on the schedule a taxpayer lands. The two must be read together.

**Qualified business income (Module 17).** The § 199A deduction is claimed after adjusted gross income and reduces taxable income, but the § 199A threshold is itself measured on taxable income computed before the deduction. Order matters, and reversing it produces a circular result.

**Capital gain stacking (Module 24).** Ordinary income fills the schedule first. Long-term gain sits on top and is taxed under § 1(h). A change in ordinary income can therefore change the rate on a gain that has not itself changed.

**Alternative minimum tax (Module 02).** The § 1 computation is only one of two. The tentative minimum tax is computed in parallel and the taxpayer pays the greater.

**Taxation of Social Security benefits (Module 14).** The § 86 thresholds that determine how much of a benefit enters taxable income are fixed in statute and are not indexed. As the § 1 brackets rise with inflation and the § 86 thresholds do not, an increasing share of benefits becomes taxable over a long projection without any real increase in income.

**Filing status (Module 03).** Status selects the schedule, and status can change mid-projection through death, divorce or the end of the surviving-spouse period.

### 8. Common Scenarios and Edge Cases

**The head of household and single schedules diverge by small amounts.** The 24 percent bracket ends at $201,750 for a head of household and $201,775 for a single filer; the 32 percent bracket ends at $256,200 and $256,225 respectively. The amounts are trivial but they are not typographical, and a table that silently equates the two schedules is wrong.

**Married filing separately reaches 37 percent at $384,350.** This is less than half the joint threshold of $768,700 and well below the single threshold of $640,600. Separate filing is sometimes chosen for reasons unrelated to rate — to isolate liability, or to reduce income-driven student loan payments — and the rate consequence at higher incomes is severe.

**Estates and trusts compress seven brackets into four.** A trust reaches the top rate at $16,000. Undistributed income accumulating in a trust is taxed far more heavily than the same income in the hands of most individuals.

**The surviving-spouse schedule is time-limited.** Section 2(a) permits the joint schedule for the two taxable years following the year of death, and only where the taxpayer maintains a household for a dependent child. Where there is no qualifying dependent, the single schedule applies from the year after death.

**Indexing is measured by C-CPI-U.** Chained CPI rises more slowly than the traditional CPI-U. Brackets therefore drift upward more slowly than headline inflation, and real bracket creep is a permanent feature of the structure rather than an anomaly.

### 9. Planning Implications

The marginal rate, not the effective rate, governs every decision at the margin. Deferring income, accelerating a deduction, converting to a Roth account or realising a gain are all evaluated against the rate on the next dollar.

The gap between the top of one bracket and the bottom of the next defines the room available for deliberate income recognition. In Example 1 the couple has $185,750 of space remaining in the 24 percent bracket before reaching 32 percent, and that space is the capacity available for a Roth conversion at a known rate.

The years between retirement and the required beginning date for distributions are usually the lowest-rate years of a taxpayer's life, because earned income has stopped and required distributions have not started. Module 09 treats that window in detail. The rate schedules are what make it valuable: income recognised there is taxed at 10, 12 or 22 percent rather than at the rate that will apply once required distributions begin.

The change of schedule on the death of a spouse is the largest single rate event in most projections, and it is foreseeable. Recognising income under the joint schedule while both spouses are living is generally preferable to leaving it to be recognised by a survivor filing singly.

### 10. Data Tables for the Engine

| Constant | Value | Indexed |
|---|---|---|
| Rate sequence | 10, 12, 22, 24, 32, 35, 37 percent | Rates fixed by statute |
| MFJ / surviving spouse thresholds | 24,800 · 100,800 · 211,400 · 403,550 · 512,450 · 768,700 | Yes, § 1(f) |
| Head of household thresholds | 17,700 · 67,450 · 105,700 · 201,750 · 256,200 · 640,600 | Yes |
| Single thresholds | 12,400 · 50,400 · 105,700 · 201,775 · 256,225 · 640,600 | Yes |
| MFS thresholds | 12,400 · 50,400 · 105,700 · 201,775 · 256,225 · 384,350 | Yes |
| Estate and trust thresholds | 3,300 · 11,700 · 16,000 | Yes |
| LTCG 0% ceiling | 98,900 MFJ · 66,200 HoH · 49,450 single and MFS | Yes |
| LTCG 15% ceiling | 613,700 MFJ · 579,600 HoH · 545,500 single · 306,850 MFS | Yes |
| Unrecaptured § 1250 gain rate ceiling | 25 percent | Fixed |
| 28-percent rate gain ceiling | 28 percent | Fixed |
| Kiddie tax base amount, § 1(g)(4)(A)(ii)(I) | $1,350 | Yes |
| Indexing measure | C-CPI-U, § 1(f)(3) | — |

### 11. References

[1] 26 U.S.C. § 1, *Tax imposed*. United States Code, Office of the Law Revision Counsel. https://www.govinfo.gov/app/collection/uscode

[2] Internal Revenue Service, *Revenue Procedure 2025-32*, § 3.01 (tax rate tables), § 3.02 (kiddie tax), § 3.03 (maximum capital gains rate). Internal Revenue Bulletin 2025-45, 3 November 2025. https://www.irs.gov/pub/irs-drop/rp-25-32.pdf

[3] Internal Revenue Service, *IRS releases tax inflation adjustments for tax year 2026, including amendments from the One, Big, Beautiful Bill*. https://www.irs.gov/newsroom/irs-releases-tax-inflation-adjustments-for-tax-year-2026-including-amendments-from-the-one-big-beautiful-bill

[4] One Big Beautiful Bill Act, P.L. 119-21. https://www.govinfo.gov/

[8] 26 U.S.C. § 1(h), including paragraphs (3) to (6) defining adjusted net capital gain, 28-percent rate gain, collectibles gain and unrecaptured section 1250 gain. https://www.govinfo.gov/app/collection/uscode

### 12. Status in This System

| Layer | Status |
|---|---|
| Projection engine | **Applied.** All five individual schedules are implemented and were verified against Revenue Procedure 2025-32 in September 2026. Every threshold matches, including the head-of-household and single divergences at $201,750/$201,775 and $256,200/$256,225, and the separate-return top bracket at $384,350. The capital gain breakpoints match at all five statuses. |
| Backend (`tax-be`) | **Not applied.** The backend holds standard deduction figures for tax year 2025 and does not implement the § 1 rate schedules. Where it estimates tax, it applies capital gain rates to ordinary income. Both points are recorded in the defect register as D6 and D7. |
| Known limitations | Only the 0, 15 and 20 percent components of § 1(h) are implemented. The 25 percent ceiling on unrecaptured § 1250 gain is not applied to the capital gain computation, which matters on the sale of depreciated rental property — the depreciation component is taxed at the ordinary long-term rate instead of its own. The 28 percent ceiling on collectibles and § 1202 gain is likewise absent. The kiddie tax under § 1(g) is not modelled; the projection assumes the taxpayer and spouse hold the income, so a household shifting investment income to children is not separately taxed. |

---

## Module 02 — Standard Deduction, Itemised Deductions and the Age-65 Addition

**Tax year:** 2026 · **As of:** September 2026 · **Primary authority:** IRC §§ 63, 68, 164, 170

---

### 1. Overview and Purpose

Section 63 defines taxable income as gross income less deductions, and gives every individual a choice: subtract a fixed statutory amount, or subtract actual itemised deductions. The standard deduction is the fixed amount, and for most taxpayers it is the larger of the two.

Three separate provisions stack for older taxpayers, and they are frequently confused. The basic standard deduction under § 63(c)(2) is available to everyone. The additional amount under § 63(f) is available to a taxpayer who is 65 or older or blind, counted once per condition per person. A third and temporary deduction of $6,000 per qualifying individual was added as § 151(d)(5)(C), applies only to taxable years beginning before 1 January 2029, and is allowed whether or not the taxpayer itemises.

Tax year 2026 is the first year in which four further changes enacted by the One Big Beautiful Bill Act take effect. The state and local tax limitation rises to $40,400 and acquires a phasedown. Section 68 is rewritten to reduce itemised deductions by two thirty-sevenths for taxpayers in the top bracket. A permanent deduction for charitable contributions by non-itemisers returns at $1,000 and $2,000. And a 0.5 percent floor is imposed on charitable contributions by itemisers. Each applies to taxable years beginning after 31 December 2025, so all four are live in the year this document describes.

For a projection to age 90 the deduction matters twice over. It determines where a taxpayer sits on the rate schedule in every year, and it changes shape at 65, again at the end of 2028 when the senior deduction expires, and again in 2030 when the state and local limitation reverts to $10,000.

### 2. Governing Law and Authorities

| Type | Citation | What it establishes |
|---|---|---|
| Statute | IRC § 63(c)(2) | Basic standard deduction by filing status |
| Statute | IRC § 63(c)(5) | Limited deduction for an individual claimed as a dependent |
| Statute | IRC § 63(f) | Additional amount for the aged and the blind |
| Statute | IRC § 68 | Overall limitation on itemised deductions, as rewritten |
| Statute | IRC § 151(d)(5)(C) | Temporary senior deduction, 2025 through 2028 |
| Statute | IRC § 163(h) | Qualified residence interest |
| Statute | IRC § 164(b)(6), (7) | Limitation on the state and local tax deduction |
| Statute | IRC § 170(b)(1)(I) | 0.5 percent floor on charitable contributions |
| Statute | IRC § 170(p) | Deduction for non-itemisers |
| Statute | IRC § 213 | Medical expenses above 7.5 percent of adjusted gross income |
| Legislation | P.L. 119-21, §§ 70103, 70111, 70120, 70424, 70425 | Enacted or amended each of the above |
| Guidance | Rev. Proc. 2025-32, § 3.14 | 2026 standard deduction and § 63(f) amounts |

### 3. Key Definitions

| Term | Definition |
|---|---|
| **Basic standard deduction** | The § 63(c)(2) amount determined by filing status. |
| **Additional standard deduction** | The § 63(f) amount for age 65 or over, and separately for blindness. Each condition counts once per qualifying person. |
| **Senior deduction** | The temporary § 151(d)(5)(C) deduction of $6,000 per qualified individual. Distinct from the § 63(f) addition and allowed in addition to it. |
| **Itemised deductions** | Deductions other than those allowable in computing adjusted gross income and other than the standard deduction. Principally state and local taxes, qualified residence interest, charitable contributions, and medical expenses above the floor. |
| **Contribution base** | For § 170 purposes, adjusted gross income computed without regard to any net operating loss carryback. It is the base against which the 0.5 percent charitable floor and the percentage ceilings are measured. |
| **Modified adjusted gross income** | For the senior deduction and the state and local phasedown, adjusted gross income increased by amounts excluded under §§ 911, 931 or 933. |
| **Applicable limitation amount** | The § 164(b)(7) ceiling on the state and local tax deduction. |

### 4. Who Is Affected

Every individual who does not itemise takes the basic standard deduction. The § 63(f) addition reaches taxpayers aged 65 or over and taxpayers who are blind, in both cases regardless of income. The senior deduction reaches taxpayers aged 65 or over below the point at which it fully phases out — $175,000 for a single filer, $350,000 for a couple where both spouses qualify.

Three exclusions are worth stating. A married individual filing separately is denied the senior deduction entirely; § 151(d)(5)(C)(v) permits it only where a married taxpayer and their spouse file a joint return. Where one spouse filing separately itemises, the other must itemise as well and may not take the standard deduction. And a nonresident alien is not entitled to the standard deduction at all.

### 5. Core Rules and Calculations

#### 5.1 Case Register

| # | Case | Applied |
|---|---|---|
| 1 | Basic standard deduction by filing status | Yes |
| 2 | § 63(f) addition for age 65 or over | Yes |
| 3 | § 63(f) addition for blindness | **No** — blindness is not an input |
| 4 | § 63(f) higher amount for an unmarried taxpayer | Yes |
| 5 | § 63(c)(5) limited deduction for a dependent | **No** — dependants are not modelled as filers |
| 6 | Senior deduction of $6,000 per qualified individual | Yes |
| 7 | Senior deduction requires **each** spouse to be 65 for the doubled amount | **No** — D11 |
| 8 | Senior deduction denied to married filing separately | **No** — D12 |
| 9 | Senior deduction thresholds are not indexed | **No** — D12 |
| 10 | Senior deduction expires after 2028 | Yes |
| 11 | Choice of the greater of standard or itemised | Yes |
| 12 | Itemised: state and local taxes | Yes |
| 13 | Itemised: medical above the 7.5 percent floor | Yes |
| 14 | Itemised: qualified residence interest under § 163(h) | **No** — D14 |
| 15 | Itemised: charitable contributions under § 170 | **No** — D14 |
| 16 | State and local limitation amount for 2026 | **No** — D8 |
| 17 | State and local phasedown above the threshold | **No** — D9 |
| 18 | Reversion of the limitation to $10,000 in 2030 | **No** — D10 |
| 19 | § 68 overall limitation, two thirty-sevenths | **No** — D15 |
| 20 | § 68 disregarded for § 199A purposes | Not applicable — § 68 is not implemented |
| 21 | § 170(p) deduction for non-itemisers | **No** — D16 |
| 22 | § 170(b)(1)(I) 0.5 percent charitable floor | **No** — D16 |
| 23 | Married filing separately: both spouses must itemise if either does | **No** |
| 24 | Nonresident alien ineligible for the standard deduction | Not applicable |

#### 5.2 The basic standard deduction — 2026

| Filing status | Amount |
|---|---|
| Married filing jointly and surviving spouse | $32,200 |
| Head of household | $24,150 |
| Single | $16,100 |
| Married filing separately | $16,100 |

An individual who may be claimed as a dependent by another taxpayer is limited to the greater of $1,350, or the sum of $450 and that individual's earned income.[1]

#### 5.3 The § 63(f) addition — 2026

The additional amount is **$1,650**, increased to **$2,050** where the individual is unmarried and not a surviving spouse.[1] It is allowed once for age and once for blindness, for each qualifying person.

| Situation | Computation | Deduction |
|---|---|---|
| Single, aged 66 | 16,100 + 2,050 | $18,150 |
| Married filing jointly, both 67 | 32,200 + 2 × 1,650 | $35,500 |
| Married filing jointly, one 67 and one 60 | 32,200 + 1,650 | $33,850 |
| Married filing jointly, both 67 and both blind | 32,200 + 4 × 1,650 | $38,800 |

#### 5.4 The senior deduction — § 151(d)(5)(C)

```
seniorDeduction = max(0, 6,000 × qualifiedIndividuals
                         − 0.06 × max(0, MAGI − threshold))

threshold = 150,000 on a joint return, otherwise 75,000
```

The statute allows $6,000 for each qualified individual, reduces the amount by 6 percent of modified adjusted gross income above the threshold, and requires the qualifying individual's social security number on the return.[2] It applies to taxable years beginning before 1 January 2029.

| Situation | Computation | Deduction |
|---|---|---|
| Single aged 66, MAGI $90,000 | 6,000 − 6% × 15,000 | $5,100 |
| Joint, both 66, MAGI $200,000 | 12,000 − 6% × 50,000 | $9,000 |
| Joint, both 66, MAGI $300,000 | 12,000 − 6% × 150,000 | $3,000 |
| Joint, one 66, MAGI $200,000 | 6,000 − 6% × 50,000 | $3,000 |

The deduction reaches zero at $175,000 for a single qualifying individual and at $350,000 for a couple where both qualify. Neither the $6,000 amount nor the thresholds are indexed; the provision expires by its own terms, so no adjustment mechanism was enacted.

#### 5.5 What itemised deductions consist of

For an individual the significant categories are:

| Category | Authority | Principal limitation |
|---|---|---|
| State and local taxes | § 164 | Applicable limitation amount, § 5.6 below |
| Qualified residence interest | § 163(h) | Acquisition indebtedness ceiling; home equity interest not deductible |
| Charitable contributions | § 170 | 0.5 percent floor and percentage ceilings, § 5.7 |
| Medical and dental expenses | § 213 | Only the excess over 7.5 percent of adjusted gross income |
| Casualty and theft losses | § 165(h) | Federally declared disaster areas only |

Miscellaneous itemised deductions subject to the former two percent floor remain disallowed.

#### 5.6 The state and local tax limitation — § 164(b)(6) and (7)

The One Big Beautiful Bill Act replaced the flat $10,000 ceiling with a scheduled amount:[3]

| Taxable year beginning in | Applicable limitation amount |
|---|---|
| 2025 | $40,000 |
| **2026** | **$40,400** |
| 2027 through 2029 | 101 percent of the preceding year's amount |
| 2030 and after | $10,000 |

A married individual filing separately takes half of each figure.

The limitation is then reduced by **30 percent** of modified adjusted gross income above a threshold amount — $500,000 for 2025, **$505,000** for 2026, and 101 percent of the preceding year thereafter. The reduction may not bring the limitation below **$10,000**.[3]

| Modified adjusted gross income | Reduction | Deduction allowed |
|---|---|---|
| $400,000 | $0 | $40,400 |
| $505,000 | $0 | $40,400 |
| $600,000 | $28,500 | $11,900 |
| $700,000 | $58,500 | $10,000 |

The floor is reached at modified adjusted gross income of $606,333. Above that the deduction is $10,000 regardless of income or of tax actually paid.

#### 5.7 Charitable contributions — the two new rules

**The 0.5 percent floor.** Section 170(b)(1)(I), added for taxable years beginning after 31 December 2025, allows a charitable contribution deduction only to the extent the aggregate of contributions exceeds **0.5 percent of the taxpayer's contribution base**.[4] The floor is applied against the categories of contribution in a specified order, absorbing those subject to the least favourable percentage ceilings first.

```
deductibleContributions = max(0, totalContributions − 0.005 × contributionBase)
```

| Contribution base | Floor | Contributions | Deductible |
|---|---|---|---|
| $200,000 | $1,000 | $5,000 | $4,000 |
| $400,000 | $2,000 | $25,000 | $23,000 |
| $1,000,000 | $5,000 | $100,000 | $95,000 |
| $150,000 | $750 | $600 | **$0** |

The last row is the case that surprises people. A modest gift below the floor produces no deduction at all.

**The deduction for non-itemisers.** Section 170(p), made permanent and expanded, allows a taxpayer who does not itemise to deduct up to **$1,000, or $2,000 on a joint return**, from 2026 onward.[5] The deduction is confined to contributions made **in cash**, to an organisation described in § 170(b)(1)(A), and **not**:

- to an organisation described in § 509(a)(3), that is a supporting organisation; or
- for the establishment of a new, or the maintenance of an existing, donor advised fund as defined in § 4966(d)(2).[6]

Non-cash gifts do not qualify.

#### 5.8 The overall limitation on itemised deductions — § 68 as rewritten

Section 68 was rewritten entirely and applies to taxable years beginning after 31 December 2025.[7] Itemised deductions otherwise allowable are reduced by **two thirty-sevenths** of the lesser of:

1. the amount of the itemised deductions, or
2. so much of taxable income, computed without regard to § 68 and increased by the itemised deductions, as exceeds the dollar amount at which the 37 percent bracket begins.

```
reduction = (2 ÷ 37) × min( itemisedDeductions,
                             max(0, taxableIncomeBefore68 + itemisedDeductions
                                    − top37BracketThreshold) )
```

Section 68 is applied **after** every other limitation on any itemised deduction, so the state and local limitation and the charitable floor come first. It is disregarded in computing the § 199A deduction.

The arithmetic has a clean interpretation. Two thirty-sevenths of 37 percent is 2 percent, so for a taxpayer fully within the top bracket the provision reduces the value of each deduction dollar from 37 cents to **35 cents**. It is a rate cap on itemised deductions, expressed as a haircut on the deduction itself.

| Situation | Lesser of | Reduction | Allowed |
|---|---|---|---|
| MFJ, taxable income $900,000, itemised $60,000 | $60,000 and $191,300 | $3,243.24 | $56,756.76 |
| MFJ, taxable income $750,000, itemised $60,000 | $60,000 and $41,300 | $2,232.43 | $57,767.57 |
| MFJ, taxable income $700,000, itemised $40,000 | $40,000 and $0 | $0 | $40,000 |
| Single, taxable income $800,000, itemised $50,000 | $50,000 and $209,400 | $2,702.70 | $47,297.30 |

The third row shows the phase-in: a taxpayer below the top bracket threshold even after adding back itemised deductions is unaffected.

### 6. Examples and Case Calculations

#### Example 1 — A couple entering retirement

Both spouses turn 66 during the year. Modified adjusted gross income is $200,000.

```
Basic standard deduction                     32,200
§ 63(f) addition, two qualifying persons      3,300
Senior deduction, 12,000 − 6% × 50,000        9,000
                                             ------
Total deduction                             $44,500
```

Taxable income is $155,500 and the couple remains in the 22 percent bracket, whose ceiling is $211,400.

#### Example 2 — The same couple five years later

The senior deduction has expired. With the other figures unchanged in nominal terms:

```
Basic standard deduction                     32,200
§ 63(f) addition                              3,300
Senior deduction                                  0
                                             ------
Total deduction                             $35,500
```

Taxable income rises by $9,000 with no change in income. The expiry of a temporary provision is a scheduled tax increase, and a projection that carries the senior deduction past 2028 understates tax in every later year.

#### Example 3 — A high earner, in the order the statute requires

Married filing jointly. Modified adjusted gross income $600,000. State and local taxes paid $45,000. Charitable contributions $25,000. Qualified residence interest $18,000.

```
Step 1 — state and local limitation
   Applicable limitation amount, 2026            40,400
   Phasedown 30% × (600,000 − 505,000)           28,500
   Allowed                                       11,900

Step 2 — charitable floor
   Contribution base                            600,000
   Floor 0.5%                                     3,000
   Allowed 25,000 − 3,000                        22,000

Step 3 — assemble itemised deductions
   State and local                               11,900
   Charitable                                    22,000
   Residence interest                            18,000
                                                 ------
   Itemised before § 68                          51,900

Step 4 — § 68
   Taxable income before § 68
      600,000 − 51,900                          548,100
   Increased by itemised deductions             600,000
   Excess over 768,700                                0
   Reduction                                          0

Total itemised deductions allowed              $51,900
```

Section 68 does not bite here because income is below the top bracket even before the deductions are added back. The taxpayer nonetheless lost $28,500 of state and local deduction and $3,000 of charitable deduction to the two other limitations. Against the $85,000 actually paid or given, $51,900 is deductible.

#### Example 4 — The same taxpayer at $1,000,000 of income

Modified adjusted gross income $1,000,000, same payments.

```
State and local: 40,400 − 30% × 495,000 = floor of  10,000
Charitable:      25,000 − 0.5% × 1,000,000 =        20,000
Residence interest                                  18,000
                                                    ------
Itemised before § 68                                48,000

§ 68: taxable income before § 68 = 952,000
      increased by itemised = 1,000,000
      excess over 768,700 = 231,300
      lesser of (48,000, 231,300) = 48,000
      reduction 2/37 × 48,000 =                   2,594.59

Allowed                                          $45,405.41
```

Every one of the three limitations applies, in the statutory order, and the last reduces the value of what survives from 37 to 35 cents in the dollar.

### 7. Interactions with Other Rules

**Rate schedules (Module 01).** The deduction determines taxable income, which is what the schedules operate on. Section 68 in turn depends on where the 37 percent bracket begins, so the two provisions are mutually referential and must be computed in the order the statute gives.

**Qualified business income (Module 17).** The § 199A threshold is measured on taxable income computed before the § 199A deduction but after the standard or itemised deduction. Section 199A(e)(1) expressly directs that taxable income for this purpose be computed **without regard to § 68**, so the new limitation does not feed back into the § 199A calculation.

**Alternative minimum tax.** The standard deduction is not allowed for alternative minimum tax purposes, and neither is the state and local deduction. A taxpayer whose itemised deductions consist mostly of state and local taxes can find the deduction disallowed in the parallel computation.

**Medical expense deduction (Module 32).** Medical expenses are deductible only above 7.5 percent of adjusted gross income. In a year of substantial long-term care cost, itemising may exceed the standard deduction for the first time in a taxpayer's life.

**Qualified charitable distributions (Module 09).** A distribution direct from an individual retirement account to charity is excluded from gross income rather than deducted. It therefore escapes the 0.5 percent floor, the percentage ceilings, and § 68 entirely, and it reduces adjusted gross income rather than merely offsetting it.

**Death of a spouse (Module 35).** The basic deduction falls from $32,200 to $16,100 and one § 63(f) addition is lost, while the survivor's own addition rises from $1,650 to $2,050 once they are no longer a surviving spouse.

### 8. Common Scenarios and Edge Cases

**The § 63(f) addition and the senior deduction are different provisions.** Both are available to the same taxpayer in the same year, and both are allowed to a non-itemiser. Treating them as alternatives understates the deduction by up to $6,000 per person.

**One spouse turns 65 and the other has not.** Only one § 63(f) addition and only one $6,000 senior deduction are available. The doubled amounts require both spouses to have attained 65 before the close of the year.

**Married filing separately.** The senior deduction is unavailable entirely, not merely halved. Separately, if one spouse itemises the other must itemise too, and cannot fall back on the standard deduction.

**A small charitable gift may produce nothing.** With the 0.5 percent floor, a taxpayer with a $150,000 contribution base who gives $600 deducts nothing. Below the floor the gift is not partially deductible; it is wholly non-deductible.

**Non-itemisers now have a charitable deduction again, but only for cash.** Appreciated stock, household goods and vehicles do not qualify under § 170(p), and gifts to a donor advised fund or a supporting organisation are excluded even if made in cash.

**Section 68 is applied last.** Computing it before the state and local limitation or the charitable floor produces a different and wrong answer, because those limitations reduce the base to which the two thirty-sevenths applies.

**The senior deduction expires after 2028** and the state and local limitation reverts to $10,000 in 2030. Both are enacted, not assumed, and a long projection should show them.

### 9. Planning Implications

Bunching itemised deductions into alternate years is worth considering wherever the itemised total sits close to the standard deduction. The 0.5 percent charitable floor strengthens the case, because bunching two years of giving into one year incurs the floor once rather than twice.

The senior deduction creates a 6 percent implicit surcharge on income between $150,000 and $350,000 for a qualifying couple, on top of the statutory rate. Income recognised in that band during 2026, 2027 and 2028 costs more than the bracket alone suggests.

The state and local phasedown produces a comparable effect at 30 cents in the dollar between $505,000 and $606,333 for taxpayers who itemise.

For a taxpayer in the top bracket, § 68 caps the value of itemised deductions at 35 cents. A qualified charitable distribution, which is an exclusion rather than a deduction, is worth the full 37 cents and is not subject to the floor. For a charitably inclined taxpayer over 70½ the distinction is now worth two percentage points more than it was.

The scheduled reversion of the state and local limitation to $10,000 in 2030 is a known future increase for taxpayers in high-tax states, resting on enacted law rather than assumption.

### 10. Data Tables for the Engine

| Constant | Value | Indexed |
|---|---|---|
| Standard deduction | 32,200 MFJ and QSS · 24,150 HoH · 16,100 single and MFS | Yes, § 63(c)(4) |
| § 63(f) addition | 1,650; 2,050 if unmarried and not a surviving spouse | Yes |
| Dependent standard deduction | greater of 1,350 or earned income + 450 | Yes |
| Senior deduction | 6,000 per qualified individual | **No** |
| Senior deduction threshold | 150,000 joint · 75,000 otherwise | **No** |
| Senior deduction phase-out rate | 6 percent | Fixed |
| Senior deduction final year | 2028 | Fixed |
| SALT limitation 2026 | 40,400 (half for MFS) | Scheduled, not CPI-indexed |
| SALT limitation 2027–2029 | 101 percent of prior year | Scheduled |
| SALT limitation 2030 onward | 10,000 | Fixed |
| SALT phasedown threshold 2026 | 505,000 (half for MFS) | Scheduled |
| SALT phasedown rate | 30 percent | Fixed |
| SALT phasedown floor | 10,000 | Fixed |
| Charitable floor, itemisers | 0.5 percent of contribution base | Fixed |
| Charitable deduction, non-itemisers | 1,000 single · 2,000 joint, cash only | **No** |
| § 68 reduction fraction | 2 ÷ 37 | Fixed |
| § 68 reference threshold | the 37 percent bracket floor: 768,700 MFJ · 640,600 single and HoH · 384,350 MFS | Yes |
| Medical floor | 7.5 percent of adjusted gross income | Fixed |

### 11. References

[1] Internal Revenue Service, *Revenue Procedure 2025-32*, § 3.14. https://www.irs.gov/pub/irs-drop/rp-25-32.pdf

[2] One Big Beautiful Bill Act, P.L. 119-21, § 70103, adding IRC § 151(d)(5)(C). https://www.govinfo.gov/content/pkg/PLAW-119publ21/html/PLAW-119publ21.htm

[3] P.L. 119-21, amending IRC § 164(b)(6) and adding § 164(b)(7). https://www.govinfo.gov/content/pkg/PLAW-119publ21/html/PLAW-119publ21.htm

[4] P.L. 119-21, § 70425, adding IRC § 170(b)(1)(I). https://www.govinfo.gov/content/pkg/PLAW-119publ21/html/PLAW-119publ21.htm

[5] P.L. 119-21, § 70424, amending IRC § 170(p). https://www.govinfo.gov/content/pkg/PLAW-119publ21/html/PLAW-119publ21.htm

[6] 26 U.S.C. § 170(p). United States Code, Office of the Law Revision Counsel. https://www.govinfo.gov/app/collection/uscode

[7] P.L. 119-21, rewriting IRC § 68. https://www.govinfo.gov/content/pkg/PLAW-119publ21/html/PLAW-119publ21.htm

[8] Internal Revenue Service, *One Big Beautiful Bill Act: tax deductions for working Americans and seniors*. https://www.irs.gov/newsroom/one-big-beautiful-bill-act-tax-deductions-for-working-americans-and-seniors

### 12. Status in This System

| Layer | Status |
|---|---|
| Projection engine | **Applied in part.** The basic standard deduction and the § 63(f) addition match Revenue Procedure 2025-32 exactly for every filing status, including the $2,050 amount for unmarried taxpayers. The senior deduction is implemented at $6,000 with a 6 percent phase-out and correctly expires after 2028. The medical deduction above the 7.5 percent floor is implemented, and the AMT treatment is correct in not adding medical expenses back. A state and local deduction is computed and capped, and the greater of standard and itemised is taken. |
| Backend (`tax-be`) | **Not applied.** Standard deduction figures in `taxRoadmapController.js` are for tax year 2025 — $15,000 and $30,000 against the 2026 amounts of $16,100 and $32,200. Recorded as D6. |
| Known limitations | Itemised deductions comprise only medical expenses and state and local taxes. **Qualified residence interest and charitable contributions are not modelled at all**, so any taxpayer whose itemised deductions rest on a mortgage or on giving is understated, and may be shown taking the standard deduction when they would itemise. The state and local limitation is computed as $40,000 inflated by a general factor rather than the statutory $40,400 growing at 101 percent, the 30 percent phasedown above $505,000 is absent, and the amount never reverts to $10,000 in 2030. The rewritten § 68 is not implemented, so top-bracket taxpayers are shown deductions worth 37 cents rather than 35. Neither the § 170(p) deduction for non-itemisers nor the 0.5 percent charitable floor is implemented. The senior deduction is doubled whenever the taxpayer is married without testing the spouse's age, is allowed to married taxpayers filing separately whom the statute excludes, and has its thresholds inflated although the statute does not index them. The § 63(f) addition for blindness is not modelled. These are recorded as D8 through D16. |

---

## Module 03 — Filing Status

**Tax year:** 2026 · **As of:** September 2026 · **Primary authority:** IRC §§ 1, 2, 6013, 7703

---

### 1. Overview and Purpose

Filing status selects the rate schedule, the standard deduction, and the threshold for nearly every income-sensitive provision in the Code. It is determined by facts — marriage, death, dependants, household maintenance — rather than by election, except where two married people choose between a joint and a separate return.

The tests are narrower than most summaries suggest. Surviving spouse status requires not merely a dependant but specifically a son, stepson, daughter or stepdaughter living in the home. Head of household status requires the taxpayer to furnish more than half the cost of maintaining the household, and treats a parent differently from every other qualifying person. A married person living apart from their spouse may be treated as unmarried, but only on three conditions that must all hold.

In a projection running several decades, status is not a constant. It changes on marriage, on divorce, and on the death of a spouse, and in the last case it may change twice: once at death and again two years later. Each change moves the taxpayer to a different schedule and a different deduction, and the effect on tax is larger than any single year's investment return.

### 2. Governing Law and Authorities

| Type | Citation | What it establishes |
|---|---|---|
| Statute | IRC § 1(a)–(d) | The four rate schedules and who uses each |
| Statute | IRC § 2(a) | Surviving spouse |
| Statute | IRC § 2(b) | Head of household |
| Statute | IRC § 2(b)(3) | Exclusions from head of household status |
| Statute | IRC § 6013(a) | Joint returns, including for the year of a spouse's death |
| Statute | IRC § 6015 | Relief from joint and several liability |
| Statute | IRC § 7703(a) | Marital status determined at the close of the taxable year |
| Statute | IRC § 7703(b) | Certain married individuals living apart treated as not married |
| Statute | IRC § 152 | Qualifying child and qualifying relative |

### 3. Key Definitions

| Term | Definition |
|---|---|
| **Surviving spouse** | Under § 2(a), a taxpayer whose spouse died in one of the two immediately preceding taxable years, who has not remarried before the close of the year, for whose year of death a joint return could have been made, and who maintains as their home a household that is for the taxable year the principal place of abode of a **son, stepson, daughter or stepdaughter** who is the taxpayer's dependant.[9] |
| **Head of household** | Under § 2(b), an individual who is not married at the close of the year, is not a surviving spouse, and either maintains a household that is for more than half the year the principal place of abode of a qualifying child or other dependant, or maintains a household that is the principal place of abode of the taxpayer's father or mother who is the taxpayer's dependant.[9] |
| **Maintaining a household** | Furnishing **over half** the cost of maintaining the household during the taxable year. The test applies to both § 2(a) and § 2(b). |
| **Considered not married** | Under § 7703(b), a married individual filing separately who maintains a household that is for more than half the year the principal place of abode of a dependent child, who furnishes over half the cost, and whose spouse is not a member of the household during the last six months of the year.[10] |
| **Year of death** | The taxable year in which a spouse dies. Marital status is determined as of the date of death, and a joint return may still be filed. |

### 4. Who Is Affected

Every individual. Marital status is determined as of the last day of the taxable year, except that where a spouse dies during the year it is determined as of the date of death.[10] A taxpayer legally separated under a decree of divorce or separate maintenance is not considered married.

Two categorical exclusions apply to head of household status: a nonresident alien may not use it at any time during the year, and a taxpayer whose only qualifying person is a dependant by reason of a multiple support agreement or of residence in the taxpayer's home under § 152(d)(2)(H) does not qualify.

### 5. Core Rules and Calculations

#### 5.1 Case Register

| # | Case | Applied |
|---|---|---|
| 1 | Single | Yes |
| 2 | Married filing jointly | Yes |
| 3 | Married filing separately | Yes — selectable |
| 4 | Head of household | Yes — selectable |
| 5 | Surviving spouse under § 2(a) | Yes |
| 6 | Joint return permitted for the year of death | Yes |
| 7 | Surviving spouse limited to two years after the year of death | Yes |
| 8 | Surviving spouse requires a son, stepson, daughter or stepdaughter | **No** — status is applied on the two-year clock alone |
| 9 | Surviving spouse lost on remarriage | **No** |
| 10 | Surviving spouse requires that a joint return could have been made for the year of death | **No** |
| 11 | Reversion to single where no qualifying child exists | **No** |
| 12 | § 2(b) qualifying child or dependant test | **No** — head of household is accepted as an input |
| 13 | § 2(b)(1)(B) parent need not live with the taxpayer | **No** |
| 14 | Over-half-the-cost-of-maintaining test | **No** |
| 15 | § 2(b)(3) nonresident alien exclusion | Not applicable |
| 16 | § 7703(a) status determined at year end, or at death | Yes |
| 17 | § 7703(b) married living apart treated as not married | **No** |
| 18 | Change of status on divorce | Yes |
| 19 | Change of status on remarriage | **No** |
| 20 | Married filing separately: both must itemise if either does | **No** |
| 21 | Community property allocation between separate returns | **No** |

#### 5.2 The five statuses and what selects them

| Status | Test | Rate schedule |
|---|---|---|
| Married filing jointly | Married at year end, or spouse died during the year, and a joint return is elected | § 1(j)(2)(A) |
| Surviving spouse | § 2(a), for the two years after the year of death | § 1(j)(2)(A) |
| Head of household | § 2(b) | § 1(j)(2)(B) |
| Single | None of the above | § 1(j)(2)(C) |
| Married filing separately | Married at year end, separate return elected | § 1(j)(2)(D) |

#### 5.3 Head of household — the two routes

Section 2(b)(1) offers two alternative qualifying routes, and the difference between them is frequently missed.

**Route A — a qualifying person living in the home.** The household must be, for **more than one-half of the taxable year**, the principal place of abode of a qualifying child of the individual, or of any other person who is a dependant of the taxpayer.

**Route B — a parent.** The household must be, **for the taxable year**, the principal place of abode of the taxpayer's father or mother, who must be the taxpayer's dependant. The statute does **not** require that the parent live with the taxpayer. A taxpayer who maintains a separate home for a dependent parent — including a place in a care facility — can qualify on this route while living elsewhere.

Both routes require the taxpayer to furnish over half the cost of maintaining the household.

Section 2(b)(2) then supplies three status rules: a taxpayer legally separated under a decree is not married; a taxpayer whose spouse is a nonresident alien at any time during the year is treated as not married; and a taxpayer whose spouse died during the year is treated as married for that year.

#### 5.4 The married-living-apart rule — § 7703(b)

A married individual filing a separate return is treated as **not married** — and so may file as head of household — if all three of the following hold:[10]

1. the individual maintains as their home a household that is, for more than half the taxable year, the principal place of abode of a child for whom the individual is entitled to a dependency deduction;
2. the individual furnishes over half the cost of maintaining that household; and
3. during the **last six months** of the taxable year, the individual's spouse is not a member of that household.

All three are required. A separation in September does not satisfy the third condition for that year.

#### 5.5 The sequence on the death of a spouse

| Year | Status available | Rate schedule | Standard deduction |
|---|---|---|---|
| Year of death | Married filing jointly | Joint | $32,200 |
| First following year | Surviving spouse, **only if** § 2(a) is satisfied | Joint | $32,200 |
| Second following year | Surviving spouse, on the same condition | Joint | $32,200 |
| Third following year | Head of household or single | Narrower | $24,150 or $16,100 |

Where § 2(a) is not satisfied — the ordinary case for a couple in their seventies or eighties, because the provision requires a dependent son, stepson, daughter or stepdaughter in the home — surviving spouse status is unavailable and the survivor moves from the joint schedule to the single schedule in the year **after** the year of death. This is the common path, and it is the path a retirement projection should assume unless a qualifying child is present.

#### 5.6 Married filing separately — the consequences

Separate filing is available to any married couple, and it carries a consistent set of disadvantages beyond the rate schedule:

| Consequence | Detail |
|---|---|
| Top bracket | 37 percent begins at $384,350 rather than $768,700 |
| Capital loss limitation | $1,500 rather than $3,000 |
| Roth IRA contribution | Phase-out range of $0 to $10,000, so most separate filers are excluded |
| Itemising | If either spouse itemises, the other must; the standard deduction is unavailable |
| Senior deduction | Denied entirely under § 151(d)(5)(C)(v) |
| State and local limitation | Half the applicable limitation amount, and half the phasedown threshold |
| Net investment income tax | Threshold of $125,000 rather than $250,000 |
| Additional Medicare Tax | Threshold of $125,000 rather than $250,000 |
| Credits | The earned income credit, education credits and the child and dependent care credit are generally unavailable |

In a community property state, income earned by either spouse is generally allocated one half to each on separate returns, which can produce a result quite different from each spouse reporting what they earned.

Separate filing is nonetheless chosen for reasons unrelated to rate: to separate liability where one spouse doubts the other's reporting, and to reduce payments under income-driven student loan plans that look to the borrower's own return. Section 6015 offers relief from joint and several liability after the fact, but it is discretionary and slow, and filing separately is the certain route.

### 6. Examples and Case Calculations

#### Example 1 — The effect of the schedule alone

Taxable income of $180,000, held constant.

| Schedule | Tax | Marginal rate |
|---|---|---|
| Married filing jointly | $29,024 | 22% |
| Single | $35,798 | 24% |
| **Difference** | **+$6,774** | +23.3% |

#### Example 2 — Deduction and schedule together

A widow aged 78 in the year after her husband's death, with no qualifying child, so § 2(a) does not apply. Her income is $95,000; the couple's had been $130,000.

```
As a couple, the prior year:   income 130,000, deduction 35,500, taxable  94,500
As a single filer now:         income  95,000, deduction 18,150, taxable  76,850
```

Income fell 27 percent. Taxable income fell only 19 percent, because the deduction fell by $17,350 at the same time. The narrower schedule then applies to what remains. This is the arithmetic behind the widow's penalty, treated in full in Module 35.

#### Example 3 — The parent route to head of household

A single taxpayer supports a mother living in a care facility, meeting more than half her total support and more than half the cost of maintaining that home. The taxpayer lives alone elsewhere.

Under § 2(b)(1)(B) the taxpayer is a head of household, because the parent route does not require the parent to live with the taxpayer. The standard deduction is $24,150 rather than $16,100, and the 22 percent bracket begins at $67,450 rather than $50,400. On $120,000 of income the difference is worth several thousand dollars a year, and it is commonly missed.

### 7. Interactions with Other Rules

**Standard deduction (Module 02).** Status selects the amount, and a surviving spouse retains the joint amount only while § 2(a) applies. Separate filers must both itemise if either does.

**Social Security (Modules 12 and 14).** On a death the survivor keeps the higher of the two benefits and loses the lower. The § 86 thresholds fall from $32,000 and $44,000 to $25,000 and $34,000. For a married person filing separately who lived with their spouse at any time during the year, the § 86 thresholds are zero, so benefits are taxable from the first dollar.

**Medicare surcharge (Module 16).** The income-related threshold halves from $218,000 to $109,000 on a change from joint to single.

**Net investment income tax (Module 06) and the Additional Medicare Tax (Module 05).** Both thresholds fall on a change of status, and both are frozen in statute, so the change is permanent in real terms.

**Capital losses (Module 24).** The annual limitation is $3,000 for every status except married filing separately, where it is $1,500.

### 8. Common Scenarios and Edge Cases

**Surviving spouse status is much narrower than commonly assumed.** It requires a dependent son, stepson, daughter or stepdaughter in the home — not merely any dependant, and not merely the fact of widowhood. Most retirees have none, so the two-year extension of joint rates is unavailable and the change to the single schedule happens immediately in the year after death.

**A joint return is still available for the year of death.** The survivor may file jointly for the year in which the spouse died, provided they have not remarried before the close of that year.

**A dependent parent need not live with the taxpayer.** This is the one qualifying-person route in § 2(b) that dispenses with the shared-residence requirement, and it regularly goes unclaimed by taxpayers supporting a parent in a care facility.

**The last-six-months test in § 7703(b) is unforgiving.** A spouse who moves out in July fails it for that year, and the taxpayer remains married for filing purposes.

**Divorce is determined at year end.** A decree entered on 31 December makes both parties unmarried for the entire year. A decree entered on 2 January leaves them married for the whole of the preceding year.

**Remarriage ends surviving spouse status immediately**, and the taxpayer files jointly with the new spouse or separately.

**Community property complicates separate returns.** In the nine community property states, income is generally split equally between spouses on separate returns regardless of who earned it, which can defeat the purpose for which separate filing was chosen.

### 9. Planning Implications

The change of status on death is the largest foreseeable rate event in a retirement projection. Its timing is unknown but its direction is not. Income recognised while both spouses are alive is taxed on the joint schedule with the joint deduction; the same income recognised by a survivor is taxed on the single schedule with roughly half the deduction. That asymmetry is the central argument for accelerating Roth conversions and gain realisation into the years when both spouses are living.

Where a projection assumes surviving spouse status for two years after death, it should be tested against the § 2(a) qualifying-child requirement. Without one, the assumption overstates the deduction by $16,100 and understates the rate for two full years.

For a taxpayer supporting a dependent parent, the § 2(b)(1)(B) route is worth checking annually. It survives the parent living elsewhere, and it is lost in the year the parent ceases to be a dependant.

### 10. Data Tables for the Engine

| Constant | Value |
|---|---|
| Statuses | single · married filing jointly · married filing separately · head of household · surviving spouse |
| Surviving spouse duration | Two taxable years after the year of death |
| Surviving spouse condition | Household that is the principal abode of a dependent son, stepson, daughter or stepdaughter; over half the cost furnished; not remarried; joint return possible for the year of death |
| Head of household, route A | Qualifying child or other dependant, principal abode for more than half the year |
| Head of household, route B | Dependent father or mother; shared residence **not** required |
| Maintaining a household | Over half the cost |
| § 7703(b) living apart | Child in home more than half the year; over half the cost; spouse absent for the last six months |
| Determination date | Last day of the taxable year; date of death where a spouse dies |
| MFS capital loss limitation | $1,500 |
| MFS Roth IRA phase-out | $0 to $10,000 |

### 11. References

[9] 26 U.S.C. § 2, *Definitions and special rules*. United States Code, Office of the Law Revision Counsel. https://www.govinfo.gov/app/collection/uscode

[10] 26 U.S.C. § 7703, *Determination of marital status*. https://www.govinfo.gov/app/collection/uscode

[1] Internal Revenue Service, *Revenue Procedure 2025-32*, §§ 3.01 and 3.14. https://www.irs.gov/pub/irs-drop/rp-25-32.pdf

### 12. Status in This System

| Layer | Status |
|---|---|
| Projection engine | **Applied.** All five statuses are implemented, each with its own rate schedule, standard deduction, and every status-dependent threshold — including the separate-return capital loss limitation of $1,500 and the Roth IRA phase-out range of $0 to $10,000, both of which are correct. The change of status on the death of a spouse is modelled, and joint filing is correctly retained for the year of death itself. |
| Backend (`tax-be`) | **Partially present.** `TaxPlan.js` carries a `filingStatus` enumeration of single, married filing jointly, married filing separately and head of household. Surviving spouse is absent from the enumeration, and no rate consequence attaches to any value. |
| Known limitations | Status is largely taken as an input rather than derived from the statutory tests. Surviving spouse is applied on the two-year clock without testing the § 2(a) requirement of a dependent son, stepson, daughter or stepdaughter, which most retired households do not meet — so where no such child exists the projection shows two years of joint rates and the joint deduction that the taxpayer is not entitled to. Neither route of the § 2(b) head of household test is evaluated, including the parent route that dispenses with shared residence, so the status is accepted as entered. The over-half-the-cost-of-maintaining test is not applied anywhere. The § 7703(b) married-living-apart rule is not implemented. Remarriage is not modelled, so surviving spouse status is never lost early. The rule requiring both spouses to itemise if either does is not enforced, and community property allocation between separate returns is not modelled. |

---

## Module 04 — Social Security and Medicare Taxes

**Tax year:** 2026 · **As of:** September 2026 · **Primary authority:** IRC §§ 1401, 1402, 3101, 3111

---

### 1. Overview and Purpose

Employment income bears a tax separate from the income tax. An employee pays 6.2 percent for old-age, survivors and disability insurance on wages up to an annual ceiling, and 1.45 percent for hospital insurance on all wages, with the employer matching both. A self-employed person pays both halves under the Self-Employment Contributions Act, at 12.4 and 2.9 percent, on 92.35 percent of net earnings.

The ceiling matters more than the rates. For 2026 it is $184,500, and it is indexed to average wages rather than to prices.[6] Above it the marginal payroll rate on an employee's wages falls from 7.65 percent to 1.45 percent, then rises again at $200,000 where the Additional Medicare Tax of Module 05 begins. The pattern is not monotonic, which surprises people who assume payroll tax simply stops.

These taxes are also what build the benefit. Earnings subject to the old-age component are the earnings credited to the worker's record, and they buy quarters of coverage at $1,890 each in 2026. Income above the ceiling bears no old-age tax and produces no additional benefit, so the trade at the margin is between the hospital insurance component alone and no further accrual.

For a business owner deciding how to characterise a return — wages, distributions, or partnership earnings — payroll tax is usually the deciding number, and over a career the difference compounds substantially.

### 2. Governing Law and Authorities

| Type | Citation | What it establishes |
|---|---|---|
| Statute | IRC § 3101(a), (b) | Employee old-age and hospital insurance tax |
| Statute | IRC § 3111 | Employer's matching tax |
| Statute | IRC § 1401(a), (b) | Self-employment tax |
| Statute | IRC § 1402(a)(12) | The 92.35 percent factor applied to net earnings |
| Statute | IRC § 1402(b)(1) | Coordination of the ceiling with wages already paid |
| Statute | IRC § 1402(b)(2) | The $400 floor below which there is no self-employment income |
| Statute | IRC § 1402(c) | Exclusions from trade or business, including employee services |
| Statute | IRC § 1402(g), (h) | Exemption for members of certain religious faiths |
| Statute | IRC § 164(f) | Deduction for one half of the self-employment tax, excluding the § 1401(b)(2) tax |
| Statute | § 230 Social Security Act | Annual contribution and benefit base |
| Guidance | Federal Register 2025-19763 | 2026 base and quarter of coverage amount |

### 3. Key Definitions

| Term | Definition |
|---|---|
| **Contribution and benefit base** | The annual ceiling on wages and self-employment income subject to the old-age component. $184,500 for 2026. |
| **Net earnings from self-employment** | Net profit from a trade or business, reduced to 92.35 percent under § 1402(a)(12) before the rates are applied. |
| **Self-employment income** | Net earnings from self-employment, excluding the excess over the contribution base less wages already paid, and excluding the whole amount if it is less than $400. |
| **OASDI** | Old-age, survivors and disability insurance. The capped component. |
| **Hospital insurance** | The Medicare component. Uncapped. |
| **Quarter of coverage** | The unit in which insured status is earned. $1,890 of covered earnings in 2026, with a maximum of four in any year. |

### 4. Who Is Affected

Employees, on wages. Self-employed individuals and general partners, on net earnings from self-employment.

Shareholders of an S corporation are **not** subject to self-employment tax on their distributive share, though they are subject to employment tax on wages the corporation pays them. Limited partners are generally excluded on their distributive share. A nonresident alien is outside the definition of self-employment income except under a totalisation agreement. Members of certain religious faiths who conscientiously object to insurance may apply for an irrevocable exemption under § 1402(g).

### 5. Core Rules and Calculations

#### 5.1 Case Register

| # | Case | Applied |
|---|---|---|
| 1 | Employee old-age tax at 6.2 percent to the base | Yes |
| 2 | Employee hospital insurance at 1.45 percent, uncapped | Yes |
| 3 | Employer matching | Not modelled — the projection tracks the individual |
| 4 | Contribution base indexed annually | Yes |
| 5 | Self-employment tax on sole proprietor net profit | Yes |
| 6 | Self-employment tax on a general partner's distributive share | Yes |
| 7 | S corporation distributive share exempt | Yes |
| 8 | 92.35 percent factor under § 1402(a)(12) | Yes |
| 9 | Wage base coordination — wages consume the base first | Yes |
| 10 | § 164(f) deduction for half the self-employment tax | Yes |
| 11 | § 164(f) excludes the § 1401(b)(2) tax from the deduction | Yes, in effect |
| 12 | Additional Medicare Tax on wages | Yes |
| 13 | Additional Medicare Tax on self-employment income | **No** — D13 |
| 14 | $400 floor under § 1402(b)(2) | **No** |
| 15 | Reasonable compensation for an S corporation shareholder | **No** |
| 16 | Limited partner exclusion | **No** — partner treatment is by election, not by class |
| 17 | Farm and nonfarm optional methods | **No** |
| 18 | § 1402(g) religious exemption | **No** |
| 19 | Quarters of coverage and insured status | **No** — benefits are taken from a statement or an assumed earnings figure |
| 20 | Household employment tax | **No** |
| 21 | Tips and statutory employees | **No** |

#### 5.2 Rates and base — 2026

| Component | Employee | Employer | Self-employed | Ceiling |
|---|---|---|---|---|
| Old-age, survivors and disability | 6.20% | 6.20% | 12.40% | $184,500 |
| Hospital insurance | 1.45% | 1.45% | 2.90% | None |
| Additional Medicare | 0.90% | — | 0.90% | None; begins at the Module 05 threshold |

The employer's half is not income to the employee and does not appear on the employee's return. It is nonetheless part of the cost of employing them, and in the self-employed case the taxpayer bears both halves directly — which is what the 92.35 percent factor is designed to equalise.

#### 5.3 The self-employment computation

```
netEarnings   = netProfit × 0.9235
   if netEarnings < 400 → no self-employment tax at all       § 1402(b)(2)

oasdi         = min(netEarnings, base − wagesAlreadyPaid) × 0.124
hospital      = netEarnings × 0.029
additional    = max(0, netEarnings + wages − threshold) × 0.009
deduction     = 0.5 × (oasdi + hospital)        ← § 164(f) excludes the additional tax
```

Wages and self-employment income share one contribution base. Section 1402(b)(1) counts wages first, and only the remaining room is available for the old-age component of self-employment income.

The § 164(f) deduction is one half of the tax imposed by § 1401 **other than** the tax imposed by § 1401(b)(2). The Additional Medicare Tax is therefore not deductible.

#### 5.4 The $400 floor

Section 1402(b)(2) excludes net earnings from self-employment entirely where they are less than $400 for the year. The floor is a cliff, not an exemption of the first $400: at $399 of net earnings there is no tax, and at $401 the tax applies to the whole amount.

For church employee income a separate and lower threshold applies under § 1402(j)(2).

#### 5.5 What is not a trade or business

Section 1402(c) removes several categories from self-employment income, most significantly the performance of services by an individual as an employee. Public office functions are also excluded, with a narrow exception for fee-basis state and local officials. Rentals from real estate are generally excluded from net earnings from self-employment under § 1402(a)(1) unless received by a real estate dealer or accompanied by substantial services.

#### 5.6 Quarters of coverage

Insured status for retirement benefits is earned in quarters of coverage. In 2026 one quarter is credited for each **$1,890** of covered earnings, to a maximum of four in a year — so $7,560 of covered earnings in 2026 earns a full year of credits.[6] Forty quarters confer fully insured status for retirement benefits. The amount is indexed annually.

Earnings above the contribution base are not covered earnings. They bear no old-age tax and add nothing to the benefit computation, which is treated in Module 11.

### 6. Examples and Case Calculations

#### Example 1 — Employee with wages of $200,000, filing single

```
OASDI      6.2%  × 184,500  =  11,439.00
Hospital   1.45% × 200,000  =   2,900.00
Additional 0.9%  ×       0  =       0.00
                               ----------
Employee total                 14,339.00
```

The Additional Medicare Tax is nil because wages equal the $200,000 threshold exactly. One further dollar of wages produces nine tenths of a cent of tax. The employer pays a matching $14,339 of old-age and hospital insurance tax, which is not income to the employee.

#### Example 2 — Sole proprietor with Schedule C profit of $250,000, filing single

```
Net earnings          250,000 × 0.9235   = 230,875.00
OASDI      12.4% × 184,500               =  22,878.00
Hospital    2.9% × 230,875               =   6,695.38
Additional  0.9% × (230,875 − 200,000)   =     277.88
                                            ----------
Total self-employment tax                   29,851.25

§ 164(f) deduction  0.5 × (22,878 + 6,695.38) = 14,786.69
```

The deduction excludes the $277.88 of additional tax. It reduces adjusted gross income, and therefore income tax, but does not reduce the self-employment tax itself.

#### Example 3 — Wage base coordination

An individual with $150,000 of wages and $80,000 of net profit from a side business. Wages consume $150,000 of the $184,500 base, leaving $34,500.

```
On wages         OASDI 6.2% × 150,000              =  9,300.00
Net earnings     80,000 × 0.9235                   = 73,880.00
                 OASDI 12.4% × min(73,880, 34,500) =  4,278.00
                 Hospital 2.9% × 73,880            =  2,142.52
```

Without the § 1402(b)(1) coordination the old-age component would be overstated by 12.4 percent of $39,380, or $4,883.

#### Example 4 — Entity choice at the same economic return

A business producing $300,000 of profit for its owner, filing jointly.

| | Sole proprietorship | S corporation paying $120,000 of wages |
|---|---|---|
| Base for old-age tax | 92.35% of 300,000 = 277,050, capped at 184,500 | 120,000 |
| Old-age tax | 22,878.00 | 14,880.00 (both halves) |
| Hospital insurance | 2.9% × 277,050 = 8,034.45 | 2.9% × 120,000 = 3,480.00 |
| **Total** | **30,912.45** | **18,360.00** |

The difference of $12,552 is the reason the reasonable compensation requirement exists, and the reason wage levels in closely held S corporations are examined.

### 7. Interactions with Other Rules

**Additional Medicare Tax (Module 05).** Wages and self-employment income are aggregated against a single threshold that is not indexed.

**Adjusted gross income and the income tax (Module 01).** Half the self-employment tax is an above-the-line deduction, so it must be computed before adjusted gross income is known. This ordering constraint is why the payroll computation precedes the income tax computation in any correct implementation.

**Qualified business income (Module 17).** The § 164(f) deduction reduces qualified business income for § 199A purposes where the trade or business generated it.

**Social Security benefits (Module 11).** Covered earnings build the record from which the primary insurance amount is computed. The contribution base therefore caps both the tax and the benefit.

**Retirement contributions (Module 07).** A deductible retirement plan contribution reduces income tax. It does **not** reduce self-employment tax, because the tax is imposed on net earnings before that deduction.

### 8. Common Scenarios and Edge Cases

**The base is indexed to wages, not prices.** It rises with the national average wage index and can rise faster than the consumer price index. Projecting it at a general inflation rate understates it in most periods.

**The 92.35 percent factor is not a deduction.** It approximates the exclusion of the employer's half from the tax base, so that a self-employed person is treated comparably to an employee. It is applied before the rates, not after.

**An S corporation shareholder must take reasonable compensation.** Characterising the whole of the return as a distribution avoids employment tax and is the most frequently litigated position in small business tax.

**A general partner pays self-employment tax on the distributive share**, whether or not the cash is distributed. A limited partner generally does not, and the boundary is contested for partners who work in the business.

**Rental income is generally not self-employment income.** Section 1402(a)(1) excludes rentals from real estate unless the taxpayer is a dealer or provides substantial services beyond those customary for occupancy. This is a different question from whether the activity is passive under § 469, and the two classifications do not have to agree.

**Two employers can each withhold correctly and still leave the employee short.** Each employer tests its own payroll against the base, so an employee with two jobs may overpay the old-age component and claim a credit, while underpaying the Additional Medicare Tax.

**A small side business below $400 of net earnings owes no self-employment tax at all** — but it also earns no quarters of coverage.

### 9. Planning Implications

For a business owner, entity choice is primarily a payroll tax decision. Above the contribution base the choice is between 2.9 or 3.8 percent on the whole of the return and nothing beyond reasonable compensation, and Example 4 shows the annual scale.

Retirement plan contributions reduce income tax only. A projection that shows a deductible contribution reducing self-employment tax as well is wrong, and the error compounds across a career.

Because the old-age component stops at the base while benefits are computed from the same capped earnings, a taxpayer consistently earning above the base is buying no additional benefit with additional income. For someone weighing whether to keep working part-time in early retirement, the relevant question is whether the additional years replace low-earning years in the benefit computation, which Module 11 addresses.

### 10. Data Tables for the Engine

| Constant | Value | Indexed |
|---|---|---|
| Old-age rate, employee | 6.2% | Fixed |
| Hospital insurance rate, employee | 1.45% | Fixed |
| Self-employment old-age rate | 12.4% | Fixed |
| Self-employment hospital rate | 2.9% | Fixed |
| Contribution and benefit base | $184,500 | Yes — average wage index |
| § 1402(a)(12) factor | 0.9235 | Fixed |
| § 1402(b)(2) floor | $400 | Fixed |
| Quarter of coverage | $1,890, maximum four a year | Yes |
| Quarters for fully insured status | 40 | Fixed |
| § 164(f) deduction | one half of § 1401 tax, excluding § 1401(b)(2) | Fixed |

### 11. References

[6] *Cost-of-Living Increase and Other Determinations for 2026*, Federal Register document 2025-19763. https://www.federalregister.gov/documents/2025/11/03/2025-19763/cost-of-living-increase-and-other-determinations-for-2026

[11] 26 U.S.C. § 1402, *Definitions*, including subsections (a)(12), (b), (c) and (g). United States Code, Office of the Law Revision Counsel. https://www.govinfo.gov/app/collection/uscode

[5] 26 U.S.C. §§ 1401, 3101, 3111 and 164(f). https://www.govinfo.gov/app/collection/uscode

### 12. Status in This System

| Layer | Status |
|---|---|
| Projection engine | **Applied.** Rates and the $184,500 base match the Federal Register determination. The 92.35 percent factor is applied before the rates. Wage base coordination under § 1402(b)(1) is implemented — wages consume the base first and only the remainder is available to self-employment income. The § 164(f) deduction is taken at one half and computed before adjusted gross income, which is the correct order and a common source of error elsewhere. Self-employment tax is charged to sole proprietors and to general partners who materially participate, and correctly not to S corporation shareholders on their distributive share. |
| Backend (`tax-be`) | **Not applied.** No payroll or self-employment tax logic. |
| Known limitations | The Additional Medicare Tax is applied only to wages; § 1401(b)(2) imposes it on self-employment income as well, against a threshold shared with wages, so a sole proprietor with substantial profit and no wages is shown no additional tax at all. Recorded as D13. The $400 floor in § 1402(b)(2) is not applied, so a trivial side business generates self-employment tax it does not owe. Reasonable compensation for an S corporation shareholder is not tested, so the wage-versus-distribution split is accepted as entered and the engine cannot flag an unsustainable position. The farm and nonfarm optional methods, the § 1402(g) religious exemption, household employment tax, and the treatment of tips and statutory employees are not modelled. Quarters of coverage and insured status are not tracked; the projection takes the benefit from a statement figure or an assumed earnings level rather than building it from a covered-earnings history. |

---

## Module 05 — Additional Medicare Tax

**Tax year:** 2026 · **As of:** September 2026 · **Primary authority:** IRC §§ 3101(b)(2), 1401(b)(2)

---

### 1. Overview and Purpose

The Additional Medicare Tax is a 0.9 percent levy on wages, railroad retirement compensation and self-employment income above a threshold that depends on filing status. It was enacted by the Affordable Care Act and took effect in 2013.

Three features distinguish it from the hospital insurance tax it sits on top of. It is imposed on the employee or the self-employed individual alone, with no employer match. It is not deductible: § 164(f) expressly excludes it from the amount a self-employed taxpayer may deduct. And its thresholds are written into the statute as fixed dollar amounts with no indexing provision, so they have not moved since 2013 and will not move.

That third feature is what gives the tax its significance in a long projection. Wages rise with inflation and the threshold does not, so the share of taxpayers subject to it grows every year without anyone earning more in real terms. A wage that was comfortably below the threshold in 2013 may be above it today on identical purchasing power.

There is also a structural mismatch between withholding and liability. An employer must begin withholding once it has paid a single employee more than $200,000, regardless of that employee's filing status or of what a spouse earns. The liability, by contrast, is computed on the couple's combined wages against a joint threshold. The two rarely coincide, and the difference is settled on the return.

### 2. Governing Law and Authorities

| Type | Citation | What it establishes |
|---|---|---|
| Statute | IRC § 3101(b)(2) | The 0.9 percent tax on wages, and the thresholds |
| Statute | IRC § 1401(b)(2) | The corresponding tax on self-employment income |
| Statute | IRC § 3201(a) | Application to railroad retirement compensation |
| Statute | IRC § 3102(f) | Employer withholding obligation above $200,000 of wages |
| Statute | IRC § 164(f) | Excludes this tax from the deduction for half of self-employment tax |
| Form | Form 8959 | Reconciles the tax and the amounts withheld |

### 3. Key Definitions

| Term | Definition |
|---|---|
| **Threshold amount** | $250,000 for a joint return, $125,000 for married filing separately, $200,000 in every other case. Fixed by statute. |
| **Applicable wages** | Wages under chapter 21, railroad retirement compensation under chapter 22, and net earnings from self-employment, aggregated against a single threshold. |
| **Withholding threshold** | The $200,000 of wages paid by a single employer at which withholding must begin, without regard to filing status. |

### 4. Who Is Affected

Any individual whose combined wages, railroad retirement compensation and net earnings from self-employment exceed the threshold for their filing status. There is no age limit and no exemption for a retiree who continues to work. Nonresident aliens are subject on wages for services performed in the United States.

### 5. Core Rules and Calculations

#### 5.1 Case Register

| # | Case | Applied |
|---|---|---|
| 1 | 0.9 percent on wages above the threshold | Yes |
| 2 | Thresholds by filing status | Yes |
| 3 | Thresholds not indexed | Yes |
| 4 | 0.9 percent on self-employment income | **No** — D13 |
| 5 | Wages and self-employment income share one threshold | **No** — follows from case 4 |
| 6 | Railroad retirement compensation included | **No** |
| 7 | No employer match | Yes — the projection tracks the individual only |
| 8 | Not deductible under § 164(f) | Yes, in effect |
| 9 | Employer withholding above $200,000 regardless of status | Not modelled — a withholding rule, not a liability rule |
| 10 | Ordering: wages are tested before self-employment income | **No** — follows from case 4 |

#### 5.2 Thresholds

| Filing status | Threshold | Indexed |
|---|---|---|
| Married filing jointly | $250,000 | **No** |
| Married filing separately | $125,000 | **No** |
| Single, head of household, surviving spouse | $200,000 | **No** |

#### 5.3 The computation

```
additionalMedicareTax = 0.009 × max(0, wages + RRTA + netEarnings − threshold)
```

Where a taxpayer has both wages and self-employment income, the statute applies the threshold to wages first and reduces the threshold available to self-employment income by the wages taken into account. The threshold is never applied twice.

The self-employment component is computed on net earnings after the 92.35 percent factor, consistently with the rest of the self-employment tax. Unlike the old-age component, there is no ceiling.

#### 5.4 Withholding and the reconciliation on Form 8959

Section 3102(f) requires an employer to withhold the additional tax once it has paid an employee more than $200,000 in the calendar year. The employer applies that single figure to its own payroll. It does not know the employee's filing status, does not know what a spouse earns, and does not aggregate with another employer's payroll.

Three mismatches follow, and all are settled on the return:

| Situation | Withheld | Owed | Result |
|---|---|---|---|
| Married couple, each earning $150,000 | $0 | $450 | Balance due |
| Single employee, $210,000 from one employer | $90 | $90 | Correct |
| Single employee, $130,000 from each of two employers | $0 | $540 | Balance due |
| Married filing jointly, one spouse earning $260,000, other not working | $540 | $90 | Refund of the excess |

Form 8959 performs the reconciliation. Amounts withheld are treated as income tax withholding and credited against total tax, so an over-withheld taxpayer is not out of pocket permanently, but the timing difference is real and can produce an unexpected balance due.

### 6. Examples and Case Calculations

| Situation | Excess over threshold | Tax |
|---|---|---|
| Single, wages $240,000 | $40,000 | $360.00 |
| Married filing jointly, combined wages $300,000 | $50,000 | $450.00 |
| Married filing separately, wages $160,000 | $35,000 | $315.00 |

#### The marriage effect

Two single people each earning $200,000 pay nothing — each sits exactly at the threshold. The same two people married and filing jointly have $400,000 of wages against a $250,000 threshold and pay $1,350. The joint threshold is not twice the single threshold, and the difference is a marriage penalty of fixed size that grows in real terms as wages inflate past a frozen number.

#### A self-employed taxpayer

A sole proprietor filing single with $250,000 of Schedule C profit:

```
Net earnings   250,000 × 0.9235   = 230,875.00
Excess over threshold              =  30,875.00
Tax  0.9% × 30,875                 =     277.88
```

The amount is small in isolation and grows steadily with profit. At $500,000 of profit the tax is $2,432.

### 7. Interactions with Other Rules

**Social Security and Medicare taxes (Module 04).** The tax sits on top of the 1.45 percent hospital insurance rate, so the employee marginal rate on wages above the threshold is 2.35 percent, and the self-employed marginal rate on net earnings above the threshold is 3.8 percent.

**Net investment income tax (Module 06).** The two taxes share the same rate in the self-employed case, the same three threshold figures, and the same absence of indexing. They reach different income: wages and self-employment income bear this tax, investment income bears the other, and no dollar bears both. A taxpayer can nonetheless pay both in the same year.

**Self-employment tax deduction (Module 04).** Section 164(f) excludes this tax from the amount that may be deducted, so unlike the rest of the self-employment tax it carries no offsetting income tax benefit.

**Filing status (Module 03).** A change from joint to single lowers the threshold from $250,000 to $200,000. For a survivor who continues to work, the tax begins $50,000 of wages earlier.

### 8. Common Scenarios and Edge Cases

**Withholding does not match liability, in either direction.** The four rows in § 5.4 are all common. A two-earner couple below $200,000 each is the most frequent under-withholding case, and a single high earner with a non-working spouse is the most frequent over-withholding case.

**The thresholds have not changed since 2013.** A taxpayer whose real income has been flat for a decade may have crossed the threshold purely through inflation. Any projection that indexes these figures will understate the tax in every later year, and the error grows across the horizon.

**There is no employer match**, which distinguishes it from every other component of employment tax and means the full 0.9 percent is borne by the individual.

**It is not deductible.** A self-employed taxpayer deducts half of the old-age and hospital components under § 164(f) and none of this one.

**Two employers each withhold correctly and the employee still owes.** Each tests its own payroll against $200,000. An employee with $130,000 from each of two employers has $260,000 of wages, owes $540 as a single filer, and has had nothing withheld.

**A retiree who keeps working is not exempt.** There is no age-based cessation, unlike the earnings test for Social Security benefits, which stops at full retirement age.

### 9. Planning Implications

The tax is small in rate and difficult to avoid by structure. It cannot be deferred by retirement plan contributions, which reduce income tax rather than employment tax, and it cannot be shifted by entity choice except to the extent that entity choice reduces wages and self-employment income themselves. An S corporation that pays lower reasonable compensation reduces this tax along with the rest of the employment tax, and is constrained by the same requirement.

Its practical importance in a projection is twofold. It is a component of the true marginal rate on earned income for high earners, adding 0.9 percentage points that a bracket table does not show. And it is one of the two frozen thresholds — with the net investment income tax — whose reach expands every year, which is a structural reason for a long projection to compute in nominal dollars and deflate only at the end.

For a two-earner couple approaching the threshold, the only reliable response is to expect a balance due and adjust withholding or estimated payments rather than be surprised by it.

### 10. Data Tables for the Engine

| Constant | Value | Indexed |
|---|---|---|
| Rate | 0.9% | Fixed |
| Threshold, married filing jointly | $250,000 | **No — frozen since 2013** |
| Threshold, married filing separately | $125,000 | **No** |
| Threshold, all others | $200,000 | **No** |
| Employer withholding trigger | $200,000 of wages from one employer | **No** |
| Employer match | None | — |
| Deductible under § 164(f) | No | — |
| Applies to self-employment net earnings | Yes, after the 0.9235 factor | — |

### 11. References

[5] 26 U.S.C. §§ 3101(b)(2), 1401(b)(2), 3102(f) and 164(f). United States Code, Office of the Law Revision Counsel. https://www.govinfo.gov/app/collection/uscode

[12] Internal Revenue Service, *Form 8959, Additional Medicare Tax*, and instructions. https://www.irs.gov/forms-pubs/about-form-8959

### 12. Status in This System

| Layer | Status |
|---|---|
| Projection engine | **Applied to wages.** The rate and all three thresholds match the statute, and the thresholds are correctly held constant rather than inflated — which matters, because inflating them would understate the tax in every later year of a projection and understate it by more each year. |
| Backend (`tax-be`) | **Not applied.** |
| Known limitations | The tax reaches wages only. Section 1401(b)(2) imposes it equally on net earnings from self-employment, and the two are meant to be aggregated against a single threshold with wages counted first. A self-employed taxpayer with no wages is shown no liability however large the profit, and a taxpayer with both wages and self-employment income has the self-employment portion ignored. Recorded as D13. Railroad retirement compensation is not modelled. The withholding rules of § 3102(f) and the reconciliation on Form 8959 are not modelled, which is defensible because the projection computes liability rather than cash flow through payroll, but it means the projection cannot show the balance due that a two-earner couple should expect. |

---

## Module 06 — Net Investment Income Tax

**Tax year:** 2026 · **As of:** September 2026 · **Primary authority:** IRC § 1411

---

### 1. Overview and Purpose

Section 1411 imposes a tax of 3.8 percent on investment income, but only for taxpayers whose modified adjusted gross income exceeds a threshold. The amount taxed is the **lesser** of net investment income and the excess of modified adjusted gross income over the threshold, which means the tax phases in rather than applying at a cliff.

Like the Additional Medicare Tax, its thresholds were set in statute in 2013 and carry no indexing provision.[7] They are the same dollar amounts — $250,000, $125,000 and $200,000 — and they have not moved in thirteen years.

The tax matters in retirement projections because so many things raise modified adjusted gross income without themselves being investment income. A required minimum distribution is not net investment income, but it lifts modified adjusted gross income and can therefore expose dividends and capital gains that would otherwise have escaped.

### 2. Governing Law and Authorities

| Type | Citation | What it establishes |
|---|---|---|
| Statute | IRC § 1411(a), (b) | The 3.8 percent rate and the threshold amounts |
| Statute | IRC § 1411(c) | Definition of net investment income |
| Statute | IRC § 1411(d) | Modified adjusted gross income |
| Regulation | Treas. Reg. § 1.1411-2 | Application to individuals |

### 3. Key Definitions

| Term | Definition |
|---|---|
| **Net investment income** | Interest, dividends, annuities, royalties, rents, net capital gain, and income from a passive trade or business or from trading in financial instruments, less properly allocable deductions. |
| **Modified adjusted gross income** | Under § 1411(d), adjusted gross income increased by the amount excluded under § 911(a)(1), less any deductions or exclusions disallowed under § 911(d)(6) with respect to that amount. For a taxpayer with no foreign earned income it equals adjusted gross income. Note that this definition is narrower than the one used for the senior deduction and the state and local phasedown, which also add back §§ 931 and 933. |
| **Threshold amount** | $250,000 joint and surviving spouse, $125,000 married filing separately, $200,000 otherwise. Fixed by statute.[7] |

### 4. Who Is Affected

Individuals with both net investment income and modified adjusted gross income above the threshold. Estates and trusts are also subject, at a threshold tied to the top bracket, which for 2026 begins at $16,000 of taxable income.

Excluded from net investment income: wages and self-employment income, which bear the Additional Medicare Tax instead; distributions from qualified retirement plans and individual retirement accounts; Social Security benefits; tax-exempt interest; and income from a trade or business in which the taxpayer materially participates.

### 5. Core Rules and Calculations

#### 5.1 Case Register

| # | Case | Applied |
|---|---|---|
| 1 | 3.8 percent rate | Yes |
| 2 | Lesser-of computation | Yes |
| 3 | Thresholds by filing status | Yes |
| 4 | Thresholds not indexed | Yes |
| 5 | Retirement plan distributions excluded from net investment income | Yes |
| 6 | Retirement plan distributions still raise modified adjusted gross income | Yes |
| 7 | Wages and self-employment income excluded | Yes |
| 8 | Material participation income excluded | Yes |
| 9 | Passive activity income included | Yes |
| 10 | Rental income included unless from a non-passive activity | Yes |
| 11 | Properly allocable deductions under § 1411(c)(1)(B) | Partially — the engine nets rental expenses but does not allocate investment interest |
| 12 | Estates and trusts | Not applicable — the projection models individuals |
| 13 | Tax-exempt interest excluded | Yes |
| 14 | § 1411(c)(1)(A)(iii) net gain on disposition of property | Yes, for portfolio and real property |
| 15 | § 1411(c)(3) working capital treated as investment income | **No** |
| 16 | § 1411(c)(4) look-through on sale of a partnership or S corporation interest | **No** |
| 17 | § 1411(c)(5) qualified plan distributions excluded | Yes |
| 18 | § 1411(c)(6) no overlap with self-employment income | Yes, in effect |
| 19 | § 1411(e) nonresident alien and charitable trust exclusion | Not applicable |
| 20 | Trading in financial instruments or commodities treated as a covered business | **No** |

#### 5.2 The computation

```
netInvestmentIncomeTax = 0.038 × min( netInvestmentIncome,
                                       max(0, MAGI − threshold) )
```

The lesser-of structure produces a phase-in. A taxpayer $10,000 over the threshold with $80,000 of investment income is taxed on $10,000, not on $80,000. Only once the excess exceeds net investment income does the whole of that income bear the tax.

#### 5.3 Thresholds

| Filing status | Threshold | Indexed |
|---|---|---|
| Married filing jointly and surviving spouse | $250,000 | **No** |
| Married filing separately | $125,000 | **No** |
| Single and head of household | $200,000 | **No** |

#### 5.4 What is and is not net investment income

Section 1411(c)(1) builds net investment income from three categories, reduced by properly allocable deductions:[13]

| Included | Statutory hook |
|---|---|
| Interest, dividends, annuities, royalties and rents, unless derived in the ordinary course of a non-passive trade or business | § 1411(c)(1)(A)(i) |
| Other gross income from a passive activity, or from trading in financial instruments or commodities | § 1411(c)(1)(A)(ii) |
| Net gain on the disposition of property, other than property held in a non-passive trade or business | § 1411(c)(1)(A)(iii) |

Four exclusions and special rules complete the picture.

**Working capital.** Section 1411(c)(3) applies a rule similar to § 469(e)(1)(B): income from the investment of working capital is **not** treated as derived in the ordinary course of a trade or business, and so is net investment income even where the business itself is one the taxpayer materially participates in. A profitable operating company holding a large cash balance generates net investment income on that balance.

**Disposition of a partnership or S corporation interest.** Section 1411(c)(4) provides a look-through. Gain on the sale of the interest is taken into account only to the extent of the net gain the transferor would have taken into account had the entity sold all of its property at fair market value immediately before the disposition. Where the entity's assets are used in a business in which the seller materially participates, much of the gain falls outside the tax. A parallel rule applies to losses.

**Qualified plan distributions.** Section 1411(c)(5) excludes any distribution from a plan described in § 401(a), § 403(a), § 403(b), § 408, § 408A or § 457(b). This covers traditional and Roth individual retirement accounts, 401(k) and 403(b) plans, and governmental 457(b) plans.

**No overlap with self-employment income.** Section 1411(c)(6) excludes any item taken into account in determining self-employment income on which the § 1401(b) tax is imposed. This is the provision that guarantees no dollar bears both this tax and the Additional Medicare Tax.

Section 1411(e) disapplies the tax entirely to a nonresident alien and to a trust all of whose unexpired interests are devoted to charitable purposes.

For an estate or trust the tax is 3.8 percent of the lesser of undistributed net investment income, or the excess of adjusted gross income over the dollar amount at which the highest bracket begins — **$16,000** for 2026. The threshold is dramatically lower than any individual threshold, which is why investment income accumulating in a non-grantor trust attracts the tax almost immediately.

### 6. Examples and Case Calculations

| Situation | Lesser of | Taxed | Tax |
|---|---|---|---|
| Single, MAGI $250,000, net investment income $60,000 | $60,000 and $50,000 | $50,000 | $1,900.00 |
| Single, MAGI $400,000, net investment income $60,000 | $60,000 and $200,000 | $60,000 | $2,280.00 |
| Joint, MAGI $260,000, net investment income $80,000 | $80,000 and $10,000 | $10,000 | $380.00 |

The first and second rows share the same investment income. The difference in tax comes entirely from where modified adjusted gross income sits, which is why the tax is best understood as a function of total income rather than of the portfolio.

#### The compounding effect of a required distribution

A married couple with $200,000 of modified adjusted gross income and $40,000 of net investment income pays nothing, being below the $250,000 threshold. A required minimum distribution of $80,000 raises modified adjusted gross income to $280,000. The distribution is not itself net investment income, but the excess over the threshold is now $30,000, so $30,000 of the couple's investment income becomes taxable and the tax is $1,140. The distribution created a liability on income it did not produce.

### 7. Interactions with Other Rules

**Required minimum distributions (Module 09).** Distributions are excluded from net investment income but included in modified adjusted gross income. This is the most common route by which a retiree becomes subject to the tax.

**Roth conversions (Module 10).** A conversion is likewise excluded from net investment income and included in modified adjusted gross income, so a large conversion can expose investment income to the tax in the year of conversion.

**Qualified charitable distributions (Module 09).** Because the amount never enters gross income, a qualified charitable distribution reduces modified adjusted gross income and can pull a taxpayer back under the threshold. An itemised charitable deduction does not, since it is taken below the line.

**Passive activity losses (Module 25).** Income from a passive activity is net investment income; income from an activity in which the taxpayer materially participates is not. The § 469 classification therefore determines § 1411 treatment.

**Capital gains (Module 24).** A realised gain is net investment income and simultaneously raises modified adjusted gross income, so it can push a taxpayer across the threshold and be taxed by the same movement.

**Medicare surcharge (Module 16).** Both are driven by modified adjusted gross income, though the surcharge uses income from two years earlier. A single large income event triggers the net investment income tax immediately and the surcharge two years later.

### 8. Common Scenarios and Edge Cases

**Retirement distributions are excluded but not neutral.** The exclusion applies to the character of the income, not to its effect on the threshold test. This is the most misunderstood feature of the tax.

**Tax-exempt interest is excluded from both sides.** It is neither net investment income nor part of modified adjusted gross income for this purpose, which distinguishes § 1411 from the Medicare surcharge, where tax-exempt interest is added back.

**Rental income depends on classification.** Rent from a passive activity is net investment income. Rent from a trade or business in which the taxpayer materially participates, including one qualifying under the real estate professional rules, generally is not.

**The sale of a residence.** Gain excluded under § 121 is not net investment income. Gain above the exclusion is.

**The thresholds are the same as the Additional Medicare Tax thresholds, but the taxes do not overlap.** Earned income bears one; investment income bears the other. Section 1411(c)(6) makes the separation explicit. A taxpayer can pay both in the same year on different income.

**An operating business can still generate net investment income.** The working capital rule in § 1411(c)(3) reaches interest and dividends earned on a company's cash reserves even where the owner materially participates in the business. Businesses that accumulate cash rather than distribute it are the common case.

**Selling a partnership interest is not all-or-nothing.** The § 1411(c)(4) look-through treats only the portion of the gain attributable to assets that would themselves have produced net investment income as subject to the tax. A materially participating partner selling an interest in an operating business may find much of the gain outside § 1411 — but the computation requires a deemed asset sale, which is not trivial.

**A trust reaches the threshold almost at once.** At $16,000 of adjusted gross income for 2026, undistributed investment income in a non-grantor trust bears the tax at income levels far below any individual threshold. Distributing income to beneficiaries who are below their own thresholds is the ordinary response.

### 9. Planning Implications

Because the tax turns on modified adjusted gross income, the levers that work are the ones that reduce income before the line: qualified charitable distributions, deductible retirement contributions during working years, and the timing of discretionary realisation.

The window between retirement and the required beginning date is again the relevant opportunity. Modified adjusted gross income is low, so investment income may fall entirely below the threshold, and gains realised in that period can escape the tax that the same gains would attract once required distributions begin.

The frozen thresholds mean the tax reaches further every year. A projection that indexes them will understate tax increasingly across the horizon, and by age 90 the error is substantial.

### 10. Data Tables for the Engine

| Constant | Value | Indexed |
|---|---|---|
| Rate | 3.8% | Fixed |
| Threshold, joint and surviving spouse | $250,000 | **No — frozen since 2013** |
| Threshold, married filing separately | $125,000 | **No** |
| Threshold, single and head of household | $200,000 | **No** |
| Computation | 3.8% × lesser of net investment income and MAGI excess | — |
| Threshold, estates and trusts | Top bracket floor: $16,000 for 2026 | Yes |
| MAGI definition | AGI + § 911(a)(1) exclusion, less § 911(d)(6) disallowed amounts | — |
| Excluded | Qualified plan distributions; self-employment income; tax-exempt interest; nonresident aliens | — |

### 11. References

[7] Treas. Reg. § 1.1411-2, *Application to individuals*. Electronic Code of Federal Regulations. https://www.ecfr.gov/current/title-26

[13] 26 U.S.C. § 1411, including subsections (c)(3), (c)(4), (c)(5), (c)(6), (d) and (e). United States Code, Office of the Law Revision Counsel. https://www.govinfo.gov/app/collection/uscode

### 12. Status in This System

| Layer | Status |
|---|---|
| Projection engine | **Applied.** The rate and all three thresholds match the regulation, and the lesser-of computation is implemented rather than the common simplification of taxing all net investment income once the threshold is crossed. Thresholds are correctly held constant rather than inflated. Retirement distributions are excluded from net investment income while still raising modified adjusted gross income, which is the correct treatment and the one most models get wrong. |
| Backend (`tax-be`) | **Not applied.** |
| Known limitations | Properly allocable deductions under § 1411(c)(1)(B) are handled only to the extent that rental expenses are netted against rental income; investment interest expense and other allocable items are not separately deducted, which overstates the base for a taxpayer carrying margin debt. The working capital rule in § 1411(c)(3) is not implemented, so interest and dividends on a business's cash reserves are not brought into net investment income. The § 1411(c)(4) look-through on the sale of a partnership or S corporation interest is not implemented; such a gain is treated under the general rule rather than by reference to a deemed sale of the entity's assets. Trading in financial instruments or commodities is not available as a business classification. Estates and trusts are not modelled, which is consistent with the scope of the projection. |


---

## Module 07 — 401(k), 403(b) and 457 Contribution Limits

**Tax year:** 2026 · **As of:** September 2026 · **Primary authority:** IRC §§ 402(g), 414(v), 415(c)

---

### 1. Overview and Purpose

Employer retirement plans are governed by several limits that operate at once and are frequently confused with one another. Section 402(g) caps what an individual may defer from salary across all plans. Section 415(c) caps the total that may go into one employer's defined contribution plan from every source combined. Section 414(v) permits an additional catch-up amount from age 50, with a higher amount for a four-year window from 60 to 63. Section 401(a)(17) caps the compensation that may be taken into account in the first place.

The limits differ in whose behaviour they constrain. The § 402(g) limit belongs to the person and follows them across employers within a calendar year. The § 415(c) limit belongs to the plan and applies separately to unrelated employers. A participant with two unrelated jobs has one deferral limit and two annual-addition limits, which is a distinction that matters for anyone with a side business alongside employment.

Tax year 2026 brings one change of substance. The administrative transition period for the SECURE 2.0 Roth catch-up requirement ended with the 2025 taxable year, so from 2026 a participant whose prior-year wages from the plan sponsor exceeded $150,000 must make catch-up contributions on a Roth basis.[14] For a high earner accustomed to deducting the whole of a deferral, part of it is now after-tax.

### 2. Governing Law and Authorities

| Type | Citation | What it establishes |
|---|---|---|
| Statute | IRC § 402(g)(1) | Annual limit on elective deferrals |
| Statute | IRC § 402(g)(7) | Fifteen-year service catch-up for certain 403(b) employers |
| Statute | IRC § 414(v)(2)(B)(i) | Age-50 catch-up |
| Statute | IRC § 414(v)(2)(E)(i) | Higher catch-up for ages 60 to 63 |
| Statute | IRC § 414(v)(3)(A) | Catch-up contributions disregarded for § 415 |
| Statute | IRC § 414(v)(7) | Requirement that certain catch-up contributions be Roth |
| Statute | IRC § 415(c)(1)(A) | Annual additions limit for defined contribution plans |
| Statute | IRC § 415(b)(1)(A) | Annual benefit limit for defined benefit plans |
| Statute | IRC § 401(a)(17) | Compensation limit |
| Statute | IRC § 457(b)(3), (e)(15) | Deferred compensation plans of governments and tax-exempt organisations |
| Legislation | SECURE 2.0 Act §§ 109, 603 | Higher catch-up at 60 to 63; mandatory Roth catch-up |
| Guidance | Notice 2023-62 | Two-year administrative transition period for § 603 |
| Guidance | Notice 2025-67 | All 2026 dollar limits |

### 3. Key Definitions

| Term | Definition |
|---|---|
| **Elective deferral** | An amount a participant elects to have contributed to a plan rather than paid as salary. Includes pre-tax and designated Roth amounts. |
| **Annual additions** | The sum of elective deferrals, employer contributions and forfeitures allocated to a participant's account in a plan for a year. Catch-up contributions are excluded. |
| **Catch-up contribution** | An additional deferral permitted from the year the participant attains age 50. |
| **Designated Roth contribution** | An elective deferral the participant irrevocably designates as includible in income, so that qualified distributions are tax free. |
| **Roth catch-up wage threshold** | The prior-year wage level above which catch-up contributions must be designated Roth. $150,000 for 2026 purposes.[15] |
| **Highly compensated employee** | Under § 414(q)(1)(B), an employee with prior-year compensation above $160,000 for 2026, or a more-than-five-percent owner. Used for non-discrimination testing, not for the Roth catch-up rule. |

### 4. Who Is Affected

Participants in 401(k), 403(b) and governmental 457(b) plans, and in SIMPLE plans under a separate and lower set of limits. The § 402(g) limit applies to the individual across all plans in which they participate, other than a 457(b) plan, which has its own separate limit.

The Roth catch-up requirement applies only where the participant's **wages from the employer sponsoring the plan** for the **preceding calendar year** exceeded the threshold. Three consequences follow: a participant with no wages from that employer in the prior year is not caught, a self-employed individual with no FICA wages is not caught, and the test is applied employer by employer rather than to total income.

### 5. Core Rules and Calculations

#### 5.1 Case Register

| # | Case | Applied |
|---|---|---|
| 1 | § 402(g) elective deferral limit | Yes |
| 2 | Limit applies to the individual across employers | Yes — one balance is modelled |
| 3 | Age-50 catch-up | Yes |
| 4 | Higher catch-up at ages 60 to 63 | Yes |
| 5 | Catch-up replaces rather than stacks | Yes |
| 6 | Catch-up reverts to the age-50 amount at 64 | Yes |
| 7 | Roth catch-up required above the wage threshold | Yes |
| 8 | Threshold measured on **prior-year** wages from the plan sponsor | **No** — current-year income is used |
| 9 | Requirement applies from taxable years beginning after 2025 | Yes |
| 10 | § 415(c) annual additions limit | **No** |
| 11 | § 415(c) applies per unrelated employer | **No** |
| 12 | Catch-up contributions excluded from § 415(c) | Not applicable — § 415(c) is not implemented |
| 13 | § 401(a)(17) compensation limit | **No** |
| 14 | § 402(g)(7) fifteen-year service catch-up | **No** |
| 15 | § 457(b) separate limit, not aggregated with § 402(g) | **No** |
| 16 | § 457(b)(3) final-three-years catch-up | **No** |
| 17 | SIMPLE plan limits | Partially — the constants are held but no SIMPLE plan type is offered |
| 18 | Defined benefit and cash balance plans under § 415(b) | **No** |
| 19 | Employer matching contributions | Yes, as an input |
| 20 | Pension-linked emergency savings accounts | **No** |

#### 5.2 The 2026 limits

| Limit | Section | 2026 amount |
|---|---|---|
| Elective deferrals, 401(k)/403(b)/457(b) | § 402(g)(1), § 457(e)(15) | **$24,500** |
| Catch-up, age 50 and over | § 414(v)(2)(B)(i) | **$8,000** |
| Catch-up, ages 60 to 63 | § 414(v)(2)(E)(i) | **$11,250** |
| Roth catch-up wage threshold | § 414(v)(7)(A) | **$150,000** |
| Annual additions, defined contribution | § 415(c)(1)(A) | **$72,000** |
| Annual benefit, defined benefit | § 415(b)(1)(A) | **$290,000** |
| Compensation limit | § 401(a)(17) | **$360,000** |
| Highly compensated employee threshold | § 414(q)(1)(B) | **$160,000** |
| Key employee threshold | § 416(i)(1)(A)(i) | **$235,000** |
| SIMPLE deferral | § 408(p)(2)(E)(i)(III) | **$17,000** |
| SIMPLE deferral, certain plans | § 408(p)(2)(E)(i)(I), (II) | **$18,100** |
| SIMPLE catch-up, age 50 | § 414(v)(2)(B)(ii) | **$4,000** |
| SIMPLE catch-up, ages 60 to 63 | § 414(v)(2)(E)(ii) | **$5,250** |
| Pension-linked emergency savings | § 402A(e)(3)(A)(i) | **$2,600** |

All figures are from Notice 2025-67.[15] The age-50 catch-up rose from $7,500; the 60-to-63 amount is unchanged at $11,250; the highly compensated employee threshold is unchanged at $160,000.

#### 5.3 The catch-up structure by age

The higher amount is available for exactly four years and does not stack on the ordinary catch-up. It **replaces** it.

| Age in the year | Catch-up available | Total deferral |
|---|---|---|
| Under 50 | $0 | $24,500 |
| 50 to 59 | $8,000 | $32,500 |
| **60, 61, 62, 63** | **$11,250** | **$35,750** |
| 64 and over | $8,000 | $32,500 |

The drop at 64 is a feature of the statute, not an error. A participant who plans around the higher figure will find $3,250 of capacity disappears in the year they turn 64.

#### 5.4 The Roth catch-up requirement

Section 414(v)(7)(A), added by SECURE 2.0 § 603, requires that catch-up contributions be designated Roth where the participant's wages from the employer sponsoring the plan exceeded the threshold in the **preceding** calendar year.

The timing has two layers and they are often conflated:

| Layer | Date |
|---|---|
| Statutory effective date, SECURE 2.0 § 603(c) | Taxable years beginning after 31 December 2023 |
| Administrative transition period, Notice 2023-62 | The first two such years — 2024 and 2025 — during which a catch-up is treated as satisfying the requirement even if not designated Roth[14] |
| **Requirement in force** | **Taxable years beginning after 31 December 2025 — that is, from 2026** |
| Applicability date of the final regulations | Taxable years beginning after 31 December 2026, with a reasonable good-faith interpretation permitted for earlier years |

So the requirement itself binds in 2026, while the detailed regulations formally apply from 2027 and plans may rely on a good-faith reading in the interim. Notice 2025-67 confirms the point by stating that the $150,000 figure determines whether catch-up contributions **for 2026** must be designated Roth.[15]

The consequence for a high earner is a partial loss of deduction. A participant aged 62 earning $200,000 defers $35,750, of which $24,500 is deductible and $11,250 is not.

#### 5.5 Section 415(c) — the limit people forget

Section 415(c)(1)(A) caps annual additions to a defined contribution plan at the lesser of $72,000 or 100 percent of compensation. Annual additions comprise elective deferrals, employer contributions and forfeitures. Catch-up contributions are **excluded** by § 414(v)(3)(A), so a participant aged 62 can reach $72,000 of annual additions and still add $11,250 on top.

The limit applies **per employer**, aggregating only related employers under §§ 414(b), (c), (m) and (o). An employee with an unrelated side business therefore has two § 415(c) limits and one § 402(g) limit — which is the structural reason a solo 401(k) alongside employment is worth considering, and also the reason the deferral portion cannot simply be doubled.

#### 5.6 Two catch-ups that are not the age-50 catch-up

**The 403(b) fifteen-year service catch-up.** Section 402(g)(7) increases the deferral limit for an employee of a qualified organisation — an educational organisation, hospital, home health service agency, health and welfare service agency, or church — who has completed fifteen years of service with that organisation. The increase is the least of $3,000, a $15,000 lifetime cap reduced by amounts previously used, or $5,000 multiplied by years of service less prior elective deferrals. It is available in addition to the age-50 catch-up.

**The 457(b) final-three-years catch-up.** Section 457(b)(3) permits a participant in the three years before normal retirement age to defer up to twice the ordinary limit, to the extent of amounts under-deferred in earlier years. It cannot be combined with the age-50 catch-up in the same year; the participant uses whichever is greater.

A 457(b) limit is separate from the § 402(g) limit. A participant with both a 403(b) and a governmental 457(b) may defer $24,500 to each in 2026.

### 6. Examples and Case Calculations

#### Example 1 — Participant aged 55, salary $120,000

```
Elective deferral limit                24,500
Age-50 catch-up                         8,000
                                       ------
Maximum deferral                      $32,500
```

Prior-year wages of $120,000 are below $150,000, so the catch-up may be made pre-tax. The whole $32,500 is deductible.

#### Example 2 — Participant aged 62, salary $200,000

```
Elective deferral limit                24,500   deductible
Catch-up, ages 60 to 63                11,250   must be Roth
                                       ------
Maximum deferral                      $35,750
```

Prior-year wages exceeded $150,000, so § 414(v)(7)(A) requires the catch-up to be designated Roth. At a 32 percent marginal rate the lost deduction costs $3,600 of current tax, in exchange for tax-free qualified distributions later.

#### Example 3 — The same participant two years later, aged 64

```
Elective deferral limit                24,500
Age-50 catch-up                         8,000
                                       ------
Maximum deferral                      $32,500
```

Capacity falls by $3,250 because the 60-to-63 window has closed.

#### Example 4 — Section 415(c) with an employer contribution

Participant aged 62, compensation $300,000, deferring the maximum, with an employer profit-sharing contribution of $40,000.

```
Elective deferral                      24,500
Employer contribution                  40,000
                                       ------
Annual additions                       64,500   against the $72,000 limit — within
Catch-up (excluded from § 415(c))      11,250
                                       ------
Total into the plan                   $75,750
```

The total exceeds $72,000 and is nonetheless permitted, because § 414(v)(3)(A) removes the catch-up from the annual additions computation. Compensation of $300,000 is below the § 401(a)(17) limit of $360,000, so the whole of it counts for the employer contribution formula.

#### Example 5 — Two unrelated employers

An employee earning $150,000 with a 401(k), who also runs an unrelated consulting business with a solo 401(k).

```
Elective deferrals across both plans, combined       24,500   one § 402(g) limit
Annual additions, employer plan                   up to 72,000
Annual additions, solo 401(k)                     up to 72,000   a separate § 415(c) limit
```

The deferral is shared; the employer contributions are not. The practical constraint on the solo plan is the profit of the business rather than the statutory ceiling.

### 7. Interactions with Other Rules

**Rate schedules and adjusted gross income (Module 01).** A pre-tax deferral reduces taxable income. A designated Roth deferral does not, so the mandatory Roth catch-up raises taxable income for affected participants relative to prior years.

**Self-employment tax (Module 04).** A deferral reduces income tax but **not** self-employment tax, which is imposed on net earnings before the deduction. This is a persistent source of error in projections.

**Required minimum distributions (Module 09).** Pre-tax deferrals build the balance that will later be forced out. Roth deferrals do not, because designated Roth accounts have been exempt from lifetime distributions since 2024 under SECURE 2.0 § 325. The mandatory Roth catch-up therefore has a second-order benefit that partly offsets the lost deduction.

**Roth accounts (Module 10).** Designated Roth contributions in an employer plan follow different rules from Roth individual retirement accounts, particularly on the five-year clock.

**Qualified business income (Module 17).** A deduction for a retirement contribution attributable to a trade or business reduces qualified business income, so the benefit of a deferral for a § 199A-eligible owner is less than the marginal rate suggests.

### 8. Common Scenarios and Edge Cases

**The catch-up replaces, it does not stack.** A participant aged 61 gets $11,250, not $11,250 plus $8,000. Adding them is the most common arithmetic error in this area.

**Capacity falls at 64.** The four-year window is 60, 61, 62 and 63 inclusive.

**The Roth catch-up test looks backwards and looks at one employer.** It is prior-year FICA wages from the sponsoring employer, not current-year total income. A participant who changed jobs during the prior year, or who had no wages from that employer, is outside the requirement even at a high income. A partner or sole proprietor with no FICA wages from the plan sponsor is likewise outside it.

**A plan without a Roth feature cannot offer catch-ups to affected participants at all.** Section 414(v)(7)(B) conditions the availability of catch-up contributions on the plan providing for designated Roth contributions for those who need them.

**Section 402(g) follows the person; section 415(c) follows the plan.** An employee with two unrelated employers can exceed $72,000 in aggregate across two plans without breaching anything, but cannot defer more than $24,500 in total.

**Excess deferrals must be corrected by 15 April** of the following year, or the amount is taxed twice — once in the year deferred and again when distributed.

**The § 401(a)(17) compensation limit constrains employer formulas, not deferrals.** A participant earning $500,000 has employer contributions computed on $360,000, but may still defer the full $24,500.

### 9. Planning Implications

For a participant in the 60-to-63 window the higher catch-up is worth using while it lasts, and the year they turn 64 should be planned for as a reduction in capacity rather than discovered.

The mandatory Roth catch-up changes the calculus for high earners. The immediate cost is the lost deduction at the marginal rate; the offset is that the amount grows tax free, is never subject to lifetime required distributions, and passes to heirs without the income tax that burdens a pre-tax balance. For a participant who expects to be in a similar or higher bracket in retirement — which describes most people with large pre-tax balances facing required distributions — the requirement is closer to neutral than it first appears.

Where a taxpayer has both employment and self-employment income, the two § 415(c) limits are the principal opportunity. The deferral is shared and should generally be made where the match is, with the side business used for employer contributions.

For an employee of a hospital, school or church with long service, the § 402(g)(7) catch-up is available in addition to the age-50 amount and is regularly unclaimed.

### 10. Data Tables for the Engine

| Constant | 2026 value | Indexed |
|---|---|---|
| § 402(g) elective deferral | $24,500 | Yes |
| § 457(e)(15) deferral | $24,500 | Yes |
| Age-50 catch-up | $8,000 | Yes |
| Ages 60–63 catch-up | $11,250 | Yes |
| Roth catch-up wage threshold | $150,000 | Yes |
| § 415(c) annual additions | $72,000 | Yes |
| § 415(b) annual benefit | $290,000 | Yes |
| § 401(a)(17) compensation | $360,000 | Yes |
| § 414(q) highly compensated employee | $160,000 | Yes |
| § 416(i) key employee | $235,000 | Yes |
| SIMPLE deferral | $17,000 / $18,100 | Yes |
| SIMPLE catch-up | $4,000 / $5,250 | Yes |
| Emergency savings account | $2,600 | Yes |
| § 402(g)(7) service catch-up | $3,000 a year, $15,000 lifetime | **No** |
| Catch-up excluded from § 415(c) | Yes, § 414(v)(3)(A) | — |
| Roth catch-up in force from | Taxable years beginning after 31 December 2025 | — |

### 11. References

[14] Internal Revenue Service, *Notice 2023-62, Guidance on Section 603 of the SECURE 2.0 Act with Respect to Catch-Up Contributions*, part IV. https://www.irs.gov/pub/irs-drop/n-23-62.pdf

[15] Internal Revenue Service, *Notice 2025-67, 2026 Amounts Relating to Retirement Plans and IRAs*. https://www.irs.gov/pub/irs-drop/n-25-67.pdf

[16] 26 U.S.C. §§ 402(g), 414(v), 415 and 457. United States Code, Office of the Law Revision Counsel. https://www.govinfo.gov/app/collection/uscode

[17] Internal Revenue Service, *Treasury, IRS issue final regulations on new Roth catch-up rule, other SECURE 2.0 Act provisions*. https://www.irs.gov/newsroom/treasury-irs-issue-final-regulations-on-new-roth-catch-up-rule-other-secure-2point0-act-provisions

### 12. Status in This System

| Layer | Status |
|---|---|
| Projection engine | **Applied.** The § 402(g) limit, both catch-up amounts and the Roth catch-up wage threshold match Notice 2025-67 exactly. The catch-up correctly **replaces** rather than stacks, and correctly reverts to the age-50 amount at 64 — an error that would otherwise overstate contributions by $3,250 a year for the rest of a career. Employer matching is taken as an input. |
| Backend (`tax-be`) | **Not applied, and stale.** `taxRoadmapController.js` holds `traditional401k: 23500` and `catchUp401k: 31000`, which are tax year 2025 figures, against 2026 amounts of $24,500 and $32,500. Recorded as D6. |
| Known limitations | The Roth catch-up test is applied to current-year income rather than to prior-year wages from the plan sponsor, so a participant who crossed $150,000 only in the current year is treated as caught when the statute does not catch them, and one who dropped below it is treated as free when the prior year governs. The § 415(c) annual additions limit is not implemented at all, so a large employer contribution can exceed $72,000 without being flagged, and the per-employer structure that permits a second limit for an unrelated business is not modelled. The § 401(a)(17) compensation limit is not applied to employer contribution formulas. Neither the § 402(g)(7) fifteen-year service catch-up nor the § 457(b)(3) final-three-years catch-up is available, and a 457(b) plan is not offered as a separate deferral bucket alongside a 403(b). Defined benefit and cash balance plans under § 415(b) are not modelled, which matters for the professional-practice owners the backend strategy library targets with them. |


---

## Module 08 — IRA Contribution Limits and Rules

**Tax year:** 2026 · **As of:** September 2026 · **Primary authority:** IRC §§ 219, 408, 408A

---

### 1. Overview and Purpose

An individual retirement account is subject to three separate tests that are often collapsed into one. Section 219(b) sets the amount that may be contributed. Section 219(g) determines how much of a traditional contribution is **deductible**, and applies only where the taxpayer or their spouse is covered by an employer plan. Section 408A(c)(3) determines whether a **Roth** contribution may be made at all.

The distinction between the second and third tests matters. A taxpayer above the § 219(g) range may still contribute to a traditional account; the contribution is simply non-deductible, and creates basis that must be tracked on Form 8606 for the rest of the account's life. A taxpayer above the § 408A range may not contribute to a Roth account directly at all.

That asymmetry is what produces the conversion route commonly called the backdoor Roth: a non-deductible traditional contribution, which has no income limit, followed by a conversion, which has had no income limit since 2010. The route works cleanly only where the taxpayer holds no other pre-tax individual retirement money, because § 408(d)(2) requires every traditional account to be treated as one for the purpose of measuring what portion of a distribution is a return of basis.

For a projection running to age 90, the significant feature is basis. Non-deductible contributions create after-tax money inside a pre-tax account, and every later distribution is part return of basis and part taxable income. A model that treats the whole balance as pre-tax overstates tax for the rest of the projection.

### 2. Governing Law and Authorities

| Type | Citation | What it establishes |
|---|---|---|
| Statute | IRC § 219(b)(5) | Contribution limit and age-50 catch-up |
| Statute | IRC § 219(c) | Spousal individual retirement account |
| Statute | IRC § 219(g) | Deduction phase-out for active participants |
| Statute | IRC § 408(d)(2) | Aggregation of all traditional accounts for basis recovery |
| Statute | IRC § 408(o) | Non-deductible contributions permitted |
| Statute | IRC § 408A(c)(2), (3) | Roth contribution limit and phase-out |
| Statute | IRC § 408A(d)(3) | Conversions |
| Statute | IRC § 25B | Retirement savings contributions credit |
| Statute | IRC § 4973 | Excise tax on excess contributions |
| Form | Form 8606 | Reporting of non-deductible contributions, basis and conversions |
| Guidance | Notice 2025-67 | All 2026 dollar limits and ranges |

### 3. Key Definitions

| Term | Definition |
|---|---|
| **Compensation** | For § 219 purposes, wages, salaries, professional fees, and net earnings from self-employment. Investment income, pension income and Social Security are not compensation, so they cannot support a contribution. |
| **Active participant** | An individual covered by an employer retirement plan for the year. Determined by plan participation, not by whether the individual contributed. |
| **Basis** | The cumulative total of non-deductible contributions, tracked on Form 8606, that has already been taxed and is recovered tax free on distribution. |
| **Aggregation rule** | Under § 408(d)(2), all traditional, SEP and SIMPLE accounts are treated as a single account when determining the taxable portion of any distribution or conversion. |
| **Conversion** | A transfer from a traditional account to a Roth account. Taxable to the extent it is not a return of basis. No income limit applies. |

### 4. Who Is Affected

Any individual with compensation may contribute up to the § 219(b) limit. The age restriction on traditional contributions was repealed by the SECURE Act, so a working taxpayer of any age may contribute.

Deductibility is restricted only where the taxpayer or their spouse is an active participant in an employer plan. A taxpayer with no employer plan may deduct the full contribution at any income level.

A married taxpayer filing separately who lived with their spouse at any time during the year faces phase-out ranges of $0 to $10,000 for both the traditional deduction and the Roth contribution. These are not indexed and are effectively a prohibition.

### 5. Core Rules and Calculations

#### 5.1 Case Register

| # | Case | Applied |
|---|---|---|
| 1 | § 219(b)(5)(A) contribution limit | Yes |
| 2 | Age-50 catch-up | Yes |
| 3 | Contribution limited to compensation | **No** |
| 4 | No age ceiling on traditional contributions | Yes |
| 5 | § 219(g) deduction phase-out, contributor is an active participant | **No** |
| 6 | § 219(g)(7) phase-out where only the spouse is an active participant | **No** |
| 7 | No phase-out where neither spouse is an active participant | **No** |
| 8 | § 408A(c)(3) Roth contribution phase-out | Constants held; not applied to limit contributions |
| 9 | Married filing separately ranges of $0 to $10,000 | Constants held |
| 10 | § 219(c) spousal contribution on the working spouse's compensation | **No** |
| 11 | Non-deductible contributions permitted above the § 219(g) range | **No** |
| 12 | Basis tracked on Form 8606 | **No** |
| 13 | § 408(d)(2) aggregation of all traditional accounts | **No** |
| 14 | Pro-rata recovery of basis on distribution or conversion | **No** |
| 15 | Conversions have no income limit | Yes — conversions are modelled |
| 16 | § 4973 excise tax on excess contributions | **No** |
| 17 | § 25B saver's credit | **No** |
| 18 | SEP and SIMPLE contribution limits | Partially — SIMPLE constants held |

#### 5.2 Contribution limits — 2026

| Limit | Section | Amount |
|---|---|---|
| Contribution | § 219(b)(5)(A) | **$7,500** |
| Catch-up, age 50 and over | § 219(b)(5)(B)(ii) | **$1,100** |
| Combined, age 50 and over | | **$8,600** |

The limit is a single ceiling across traditional and Roth accounts combined. A taxpayer may split $7,500 between the two, but may not contribute $7,500 to each. The contribution may not exceed the individual's compensation for the year.

#### 5.3 Deductibility of a traditional contribution — § 219(g)

The phase-out applies **only** where the taxpayer or their spouse is an active participant in an employer plan. Where neither is, the contribution is fully deductible at any income.[15]

| Situation | Phase-out range, 2026 | Indexed |
|---|---|---|
| Single or head of household, active participant | **$81,000 – $91,000** | Yes |
| Married filing jointly, the contributor is an active participant | **$129,000 – $149,000** | Yes |
| Married filing jointly, the contributor is **not** but the spouse is | **$242,000 – $252,000** | Yes |
| Married filing separately, active participant | **$0 – $10,000** | **No** |
| Neither spouse is an active participant | No phase-out | — |

```
deductibleAmount = limit × (1 − (MAGI − rangeStart) ÷ (rangeEnd − rangeStart))
                   rounded up to the next $10, with a $200 floor while any deduction remains
```

The third row is the one most often missed. A couple where one spouse has no employer plan can deduct a full contribution for that spouse at incomes far above the range that applies to the covered spouse.

#### 5.4 Eligibility for a Roth contribution — § 408A(c)(3)

| Filing status | Phase-out range, 2026 | Indexed |
|---|---|---|
| Married filing jointly and surviving spouse | **$242,000 – $252,000** | Yes |
| Single and head of household | **$153,000 – $168,000** | Yes |
| Married filing separately | **$0 – $10,000** | **No** |

Above the top of the range no direct Roth contribution is permitted. Below the bottom, the full limit is available.

#### 5.5 Non-deductible contributions, basis and the aggregation rule

Section 408(o) permits a contribution that is not deductible. The taxpayer reports it on Form 8606, and the cumulative total becomes **basis** — money already taxed, which is recovered free of tax on distribution.

Section 408(d)(2) then imposes the rule that governs everything downstream. **All** traditional, SEP and SIMPLE accounts are treated as a single account, and every distribution or conversion carries out basis and pre-tax money in the same proportion:

```
nontaxablePortion = distribution × (totalBasis ÷ totalTraditionalBalance at 31 December)
```

The balance is measured at the end of the year in which the distribution occurs, plus any outstanding rollovers, not at the moment of the transaction. A conversion in January is therefore measured against a balance that is not known until December.

#### 5.6 The conversion route and why aggregation defeats it

A contribution to a traditional account has no income limit. A conversion has had no income limit since 2010. A taxpayer above the Roth range can therefore contribute non-deductibly and convert.

The route is clean only where there is no other pre-tax individual retirement money. Where there is, § 408(d)(2) makes most of the conversion taxable:

| Situation | Basis | Total balance | Taxable share of a $7,500 conversion |
|---|---|---|---|
| No other traditional money | $7,500 | $7,500 | **$0** |
| $200,000 rollover balance alongside | $7,500 | $207,500 | **$7,229** — 96.4 percent |

The second row is the ordinary case for someone who has rolled a former employer's plan into an individual retirement account. Employer plan balances are **not** included in the § 408(d)(2) aggregation, so rolling the pre-tax balance into a current employer's 401(k) — where the plan accepts it — restores the clean result.

#### 5.7 Spousal contributions and the saver's credit

Section 219(c) permits a contribution for a spouse with little or no compensation, supported by the working spouse's compensation, provided a joint return is filed. Each spouse has a full $7,500 limit.

Section 25B provides a credit of 50, 20 or 10 percent of up to $2,000 of contributions, on a stepped scale. For 2026 the credit disappears above adjusted gross income of $80,500 for a joint return, $60,375 for a head of household, and $40,250 for all other taxpayers.[15] It is rarely relevant to the population this system serves and is recorded here for completeness. SECURE 2.0 replaces it with a federal matching contribution from 2027.

### 6. Examples and Case Calculations

#### Example 1 — Deductible contribution, no employer plan

A married couple, joint income $300,000, neither covered by an employer plan. Both are 52.

```
Contribution each   7,500 + 1,100 = 8,600
Deductible                          8,600 each, $17,200 total
```

No phase-out applies at any income, because § 219(g) is engaged only by active participation.

#### Example 2 — Partial deduction

Single filer aged 45, active participant, modified adjusted gross income $86,000. The range is $81,000 to $91,000.

```
Position in range   (86,000 − 81,000) ÷ 10,000 = 50%
Deductible          7,500 × 50%                 = $3,750
Non-deductible      the remaining               = $3,750, which becomes basis
```

#### Example 3 — One spouse covered, one not

Married couple, joint income $200,000. One spouse is an active participant, the other is not. Both are 48.

```
Covered spouse      range 129,000 – 149,000; income above it   →  $0 deductible
Uncovered spouse    range 242,000 – 252,000; income below it   →  $7,500 fully deductible
```

The couple deducts $7,500. Treating both spouses as covered because one is would forfeit it.

#### Example 4 — The aggregation rule defeating a conversion

A taxpayer aged 50 with a $200,000 traditional balance from a former employer contributes $7,500 non-deductibly and converts it immediately.

```
Total basis                                     7,500
Total traditional balance at 31 December      207,500
Non-taxable share      7,500 × (7,500 ÷ 207,500) =   271
Taxable                7,500 − 271                = $7,229
```

At a 32 percent marginal rate the conversion costs $2,313 of tax. Rolling the $200,000 into a current employer's 401(k) first, where the plan permits it, would have left the conversion almost entirely tax free.

#### Example 5 — Basis surviving into retirement

The same taxpayer makes a $7,500 non-deductible contribution each year for ten years without converting, reaching $75,000 of basis against a $600,000 balance.

```
Basis fraction   75,000 ÷ 600,000 = 12.5%
```

Every distribution, including every required minimum distribution, is 12.5 percent tax free. Over the remaining life of the account that is $75,000 of income never taxed — but only if the Form 8606 record has been kept. Where it has not, the basis is generally lost and the whole balance is taxed.

### 7. Interactions with Other Rules

**Employer plans (Module 07).** Active participation in an employer plan is what engages the § 219(g) phase-out. The two limits are separate: a participant may defer $24,500 to a 401(k) and still contribute $7,500 to an individual retirement account.

**Required minimum distributions (Module 09).** Basis reduces the taxable portion of every required distribution. Roth individual retirement accounts are exempt from lifetime distributions entirely, which is the principal long-run argument for the conversion route.

**Roth accounts (Module 10).** A conversion starts its own five-year clock for penalty purposes, separate from the five-year clock for qualified distributions.

**Net investment income tax (Module 06).** A conversion is excluded from net investment income but raises modified adjusted gross income, so a large conversion can expose other investment income to the 3.8 percent tax.

**Medicare surcharge (Module 16).** A conversion raises modified adjusted gross income and therefore the Part B and Part D surcharge two years later. This is the most common unpleasant surprise following a large conversion.

**Qualified charitable distributions (Module 09).** Available from a traditional account at 70½. Basis is **not** recovered pro rata on a qualified charitable distribution — the excluded amount is treated as coming first from the pre-tax portion, which is favourable and is the opposite of the ordinary ordering.

### 8. Common Scenarios and Edge Cases

**Contributions require compensation.** A retiree living on Social Security, pensions and investment income has no compensation and cannot contribute, regardless of cash available. A working spouse's compensation can support a spousal contribution.

**Deductibility and eligibility are different questions.** Being above the § 219(g) range does not prevent a contribution; it prevents a deduction.

**The uncovered spouse has a much higher range.** $242,000 to $252,000, against $129,000 to $149,000 for the covered spouse.

**Aggregation counts employer plans out, not in.** Only traditional, SEP and SIMPLE individual retirement accounts are aggregated. A 401(k) balance is invisible to § 408(d)(2), which is why the rollover-in strategy works.

**The measuring date is 31 December.** A conversion executed in January is tested against the balance at the end of that same year. Contributing to a traditional account later in the year, after converting, changes the fraction retrospectively.

**Form 8606 must be filed to establish basis.** Where it has not been filed, reconstructing basis years later is difficult and the Service is not obliged to accept it. The practical consequence is that the same money is taxed twice.

**Married filing separately is effectively excluded from both.** The $0 to $10,000 ranges are not indexed and have not moved since they were enacted.

**Excess contributions attract a six percent excise tax each year** under § 4973 until corrected, which makes an unnoticed excess expensive over time.

### 9. Planning Implications

For a taxpayer above the Roth range, the sequence matters more than the contribution. Clearing pre-tax individual retirement balances into an employer plan before making non-deductible contributions is what makes the conversion route work, and doing it in the reverse order produces a largely taxable conversion.

Where only one spouse is covered by an employer plan, the uncovered spouse's contribution is deductible to a much higher income, and this is worth testing every year rather than assumed away.

Basis is an asset that must be documented. For a client with a long history of non-deductible contributions, locating the Form 8606 history is worth real money, and its absence should be treated as a finding rather than a formality.

The years between retirement and the required beginning date are when conversions are cheapest, and Module 09 sets out why. The constraint in those years is usually not the income limit — there is none on conversions — but the interaction with the Medicare surcharge two years later and with the net investment income tax in the year itself.

### 10. Data Tables for the Engine

| Constant | 2026 value | Indexed |
|---|---|---|
| Contribution limit | $7,500 | Yes |
| Age-50 catch-up | $1,100 | Yes |
| § 219(g) range, single and head of household | $81,000 – $91,000 | Yes |
| § 219(g) range, joint, contributor covered | $129,000 – $149,000 | Yes |
| § 219(g)(7) range, joint, only spouse covered | $242,000 – $252,000 | Yes |
| § 219(g) range, married filing separately | $0 – $10,000 | **No** |
| § 408A range, joint and surviving spouse | $242,000 – $252,000 | Yes |
| § 408A range, single and head of household | $153,000 – $168,000 | Yes |
| § 408A range, married filing separately | $0 – $10,000 | **No** |
| Conversion income limit | None | — |
| § 4973 excise on excess | 6 percent a year until corrected | Fixed |
| § 25B credit disappears above | $80,500 joint · $60,375 HoH · $40,250 other | Yes |

### 11. References

[15] Internal Revenue Service, *Notice 2025-67, 2026 Amounts Relating to Retirement Plans and IRAs*. https://www.irs.gov/pub/irs-drop/n-25-67.pdf

[18] 26 U.S.C. §§ 219, 408, 408A and 4973. United States Code, Office of the Law Revision Counsel. https://www.govinfo.gov/app/collection/uscode

[19] Internal Revenue Service, *Publication 590-A, Contributions to Individual Retirement Arrangements*. https://www.irs.gov/pub/irs-pdf/p590a.pdf

[20] Internal Revenue Service, *Form 8606, Nondeductible IRAs*, and instructions. https://www.irs.gov/forms-pubs/about-form-8606

### 12. Status in This System

| Layer | Status |
|---|---|
| Projection engine | **Applied in part.** The contribution limit of $7,500 and the catch-up of $1,100 match Notice 2025-67. The Roth phase-out ranges are held as constants and match the notice exactly for all five filing statuses, including the unindexed $0 to $10,000 range for married filing separately. Roth conversions are modelled, and correctly carry no income limit. |
| Backend (`tax-be`) | **Not applied, and stale.** `taxRoadmapController.js` holds `traditionalIRA: 7000` and `catchUpIRA: 8000`; the 2026 figures are $7,500 and $1,100, and the second backend value appears to conflate the combined limit with the catch-up itself. Recorded as D6. |
| Known limitations | The § 219(g) deduction phase-out is not implemented, so a traditional contribution is treated as fully deductible regardless of income or active-participant status — including the favourable § 219(g)(7) range for an uncovered spouse, which is therefore neither applied nor available. Non-deductible contributions and Form 8606 basis are not tracked at all, and the § 408(d)(2) aggregation rule is absent, so a modelled conversion is treated as fully taxable rather than pro rata and the backdoor route cannot be represented. Because basis is not carried, every later distribution is taxed in full even where part of it would be a tax-free return of basis. The contribution is not limited to compensation, so a retiree with no earned income can be shown contributing. Spousal contributions under § 219(c), the § 4973 excise tax on excess contributions, and the § 25B credit are not modelled. |

---

## Module 09 — Required Minimum Distributions

**Tax year:** 2026 · **As of:** September 2026 · **Primary authority:** IRC § 401(a)(9)

---

### 1. Overview and Purpose

Tax-deferred retirement accounts postpone tax; they do not forgive it. Section 401(a)(9) sets the point at which deferral ends by requiring that a minimum amount be distributed each year once the account owner reaches an applicable age.[1] The distribution is included in gross income and taxed at ordinary rates.

The mechanism is arithmetic rather than discretionary. The prior year's closing balance is divided by a life expectancy factor published by the Treasury, and the quotient is the amount that must come out. Neither the owner's need for the money nor the composition of the account affects the calculation.

Required distributions matter to a long projection out of proportion to their size, for three reasons. They are involuntary, so they set a floor under taxable income in every year after they begin. The divisor shrinks as the owner ages, so the required percentage rises even when the balance does not — from 3.77 percent at 73 to 8.20 percent at 90. And because they are ordinary income, they cascade: a required distribution can make Social Security benefits taxable, push modified adjusted gross income across a Medicare surcharge threshold, and expose investment income to the net investment income tax, all in the same year.

The years between retirement and the first required distribution are consequently the most valuable planning window in the system, and they exist only because the applicable age is later than the age at which most people stop working.

### 2. Governing Law and Authorities

| Type | Citation | What it establishes |
|---|---|---|
| Statute | IRC § 401(a)(9) | The distribution requirement and its timing |
| Statute | IRC § 401(a)(9)(C) | Required beginning date; the still-working exception |
| Statute | IRC § 4974 | Excise tax on an amount not distributed |
| Statute | IRC § 408(d)(8) | Qualified charitable distributions |
| Regulation | Treas. Reg. § 1.401(a)(9)-5 | How the required minimum is determined |
| Regulation | Treas. Reg. § 1.401(a)(9)-9 | The Uniform Lifetime and Joint and Last Survivor tables |
| Legislation | SECURE Act, P.L. 116-94 | Ten-year rule for most non-spouse beneficiaries |
| Legislation | SECURE 2.0 Act, P.L. 117-328, § 107 | Applicable age raised to 73, then 75 |
| Legislation | SECURE 2.0 Act, § 325 | Designated Roth accounts removed from lifetime requirements |
| Legislation | SECURE 2.0 Act, § 327 | Surviving spouse election to be treated as the deceased employee |
| Guidance | IRS Publication 590-B | Worked examples and the tables as published |
| Guidance | IRS Notice 2025-67 | 2026 dollar amounts, including the qualified charitable distribution limit |

### 3. Key Definitions

| Term | Definition |
|---|---|
| **Applicable age** | The age at which distributions must begin. 73 or 75, determined by year of birth. |
| **Required beginning date (RBD)** | 1 April of the year following the year the owner reaches the applicable age. |
| **Distribution calendar year** | A calendar year for which a minimum distribution is required. |
| **Applicable denominator** | The life expectancy factor from the governing table, using the age the owner attains during the distribution year. |
| **Account balance** | The balance as of the last valuation date in the preceding calendar year, adjusted for subsequent contributions and outstanding rollovers.[2] |
| **Designated Roth account** | A Roth subaccount within an employer plan, as distinct from a Roth IRA. |
| **Eligible designated beneficiary** | A beneficiary who escapes the ten-year rule: a surviving spouse, a minor child of the owner, a disabled or chronically ill individual, or a person not more than ten years younger than the owner. |
| **Qualified charitable distribution (QCD)** | A direct transfer from an IRA to a qualifying charity, excluded from gross income, available from age 70½. |

### 4. Who Is Affected

Owners of traditional IRAs, SEP IRAs and SIMPLE IRAs, and participants in employer plans including 401(k), 403(b) and governmental 457(b) plans, once they reach the applicable age.

The applicable age depends on year of birth:

| Year of birth | Applicable age | Authority |
|---|---|---|
| Before 1951 | 72 | Pre-SECURE 2.0 rule, retained for those already subject to it |
| 1951 – 1959 | 73 | SECURE 2.0 § 107 |
| 1960 or later | 75 | SECURE 2.0 § 107 |

Not affected during the owner's lifetime: Roth IRAs, and — since 2024 — designated Roth accounts in employer plans.[1] Beneficiaries of both remain subject to distribution requirements after the owner's death.

### 5. Core Rules and Calculations

#### 5.1 Case Register

Every case within this rule, and whether this system applies it.

| # | Case | Applied |
|---|---|---|
| 1 | Applicable age 73 for those born 1951–1959 | Yes |
| 2 | Applicable age 75 for those born 1960 or later | Yes |
| 3 | Applicable age 72 for those born before 1951 | Yes |
| 4 | Uniform Lifetime Table divisor by attained age | Yes |
| 5 | Prior 31 December balance as the numerator | Yes |
| 6 | Required beginning date of 1 April in the following year | **No** — the projection assumes the first distribution is taken in the year the applicable age is reached |
| 7 | Two distributions in one year where the first is deferred | **No** — follows from case 6 |
| 8 | Joint and Last Survivor Table where the sole beneficiary spouse is more than ten years younger | **No** |
| 9 | Still-working exception for employer plans | **No** |
| 10 | Five-percent-owner carve-out from the still-working exception | **No** |
| 11 | Aggregation across IRAs | Not modelled separately — pre-tax accounts are held as one balance |
| 12 | Separate distribution required from each 401(k) and 457(b) | Not modelled separately — as above |
| 13 | Designated Roth accounts exempt during life (SECURE 2.0 § 325) | Yes — Roth balances are excluded from the calculation |
| 14 | Roth IRA exempt during life | Yes |
| 15 | Qualified charitable distribution reduces the taxable amount | Yes |
| 16 | QCD annual limit of $111,000 | Yes |
| 16a | QCD recipient may not be a donor advised fund or supporting organisation | **No** |
| 16b | § 408(d)(8)(A) reduction for post-70½ deductible contributions | **No** |
| 16c | § 408(d)(8)(D) pre-tax-first ordering | **No** — basis is not tracked |
| 17 | Excise tax under § 4974 | **No** — the projection assumes compliance |
| 18 | Ten-year rule for most non-spouse beneficiaries | **No** — post-death, outside the projection horizon |
| 18a | No distributions required in years 1–9 where death was before the RBD | **No** — as above |
| 18b | Annual distributions required where death was on or after the RBD | **No** — as above |
| 19 | Eligible designated beneficiary categories | **No** — as above |
| 20 | Surviving spouse § 327 election | **No** |

Cases 6 to 10 and 20 are the ones most likely to change a projected number for a living taxpayer. They are recorded in § 12 and in the defect register.

#### 5.2 The computation

```
requiredMinimumDistribution(year) = accountBalance(prior 31 December)
                                    ÷ applicableDenominator(age attained during year)
```

Two details govern correctness. The numerator is the balance at the close of the *preceding* year, not the current balance. The denominator uses the age the owner *attains during* the distribution year, not the age at the start of it — a person turning 75 in December uses the divisor for 75, not 74.

#### 5.3 Uniform Lifetime Table — Treas. Reg. § 1.401(a)(9)-9(c)

| Age | Divisor | Age | Divisor | Age | Divisor | Age | Divisor |
|---|---|---|---|---|---|---|---|
| 72 | 27.4 | 85 | 16.0 | 98 | 7.3 | 111 | 3.4 |
| 73 | 26.5 | 86 | 15.2 | 99 | 6.8 | 112 | 3.3 |
| 74 | 25.5 | 87 | 14.4 | 100 | 6.4 | 113 | 3.1 |
| 75 | 24.6 | 88 | 13.7 | 101 | 6.0 | 114 | 3.0 |
| 76 | 23.7 | 89 | 12.9 | 102 | 5.6 | 115 | 2.9 |
| 77 | 22.9 | 90 | 12.2 | 103 | 5.2 | 116 | 2.8 |
| 78 | 22.0 | 91 | 11.5 | 104 | 4.9 | 117 | 2.7 |
| 79 | 21.1 | 92 | 10.8 | 105 | 4.6 | 118 | 2.5 |
| 80 | 20.2 | 93 | 10.1 | 106 | 4.3 | 119 | 2.3 |
| 81 | 19.4 | 94 | 9.5 | 107 | 4.1 | 120+ | 2.0 |
| 82 | 18.5 | 95 | 8.9 | 108 | 3.9 | | |
| 83 | 17.7 | 96 | 8.4 | 109 | 3.7 | | |
| 84 | 16.8 | 97 | 7.8 | 110 | 3.5 | | |

The implied percentage is the reciprocal of the divisor: 3.77 percent at 73, 4.07 percent at 75, 4.95 percent at 80, 8.20 percent at 90.

#### 5.4 Required beginning date

The first distribution may be deferred to 1 April of the year following the year the applicable age is reached. Every subsequent distribution is due by 31 December.[3]

Deferral does not reduce the number of distributions; it moves the first one into the same calendar year as the second. Both are then taxable in that year. Example 3 below quantifies the effect.

#### 5.5 Spouse more than ten years younger

Where the sole beneficiary for the entire distribution year is a spouse more than ten years younger than the owner, the Joint and Last Survivor Table in Treas. Reg. § 1.401(a)(9)-9(d) is substituted for the Uniform Lifetime Table.[2] The joint divisor is larger, so the required distribution is smaller. The spouse must remain the sole beneficiary throughout the year for the substitution to apply.

#### 5.6 Aggregation

The rules differ by account type, and the distinction is a common source of penalty exposure.[3]

| Account type | Rule |
|---|---|
| Traditional, SEP and SIMPLE IRAs | Compute separately for each, then withdraw the total from any one or more of them |
| 403(b) contracts | Same treatment — compute separately, aggregate the withdrawal |
| 401(k) plans | Compute and withdraw **separately from each plan** |
| 457(b) plans | Compute and withdraw **separately from each plan** |

IRAs and 403(b) contracts may not be aggregated with each other, and neither may be used to satisfy a 401(k) requirement.

#### 5.7 Still-working exception

A participant in an employer plan who is still employed by the plan sponsor may defer distributions from that plan until the year of retirement. The exception does not extend to a participant who owns more than five percent of the sponsoring business, and it never applies to IRAs — traditional, SEP and SIMPLE IRA owners must begin at the applicable age regardless of employment.[3]

#### 5.8 Qualified charitable distributions

From age 70½ — earlier than the applicable age — an IRA owner may direct a distribution to a qualifying charity. The amount is excluded from gross income and counts toward the required minimum distribution for the year.[4]

For 2026 the annual limit is **$111,000**, increased from $108,000. A one-time distribution to a split-interest entity under § 408(d)(8)(F) is limited to $55,000, increased from $54,000.[4] On a joint return each spouse has a separate limit.

Because the amount never enters gross income, a QCD reduces adjusted gross income rather than producing a deduction. That distinction matters: it lowers the base for the taxation of Social Security benefits, for the Medicare surcharge, and for the net investment income tax, none of which respond to an itemised charitable deduction.

**Three restrictions are easy to miss and each defeats the distribution entirely.**

*The recipient cannot be a donor advised fund or a supporting organisation.* Section 408(d)(8)(B)(i) requires the transfer to go to an organisation described in § 170(b)(1)(A) **other than** a § 509(a)(3) supporting organisation or a fund or account described in § 4966(d)(2) — that is, a donor advised fund.[95] A donor advised fund is the most common vehicle a charitably minded client already holds, and directing a qualified charitable distribution into one produces a fully taxable distribution with an itemised deduction instead. The split-interest election in § 408(d)(8)(F) is a narrow and separate exception for a charitable remainder trust or charitable gift annuity, used once in a lifetime.

*The exclusion is reduced by deductible contributions made after 70½.* Section 408(d)(8)(A) reduces the excludable amount by the aggregate deductions allowed under § 219 for all taxable years ending on or after the year the taxpayer attains 70½, less reductions already applied. A taxpayer who continues working and contributing deductibly to an individual retirement account after 70½ erodes their own qualified charitable distribution capacity dollar for dollar.

*The amount comes out of the pre-tax portion first.* Section 408(d)(8)(D) displaces the ordinary § 72 pro-rata rule: the distribution is treated as includible in gross income to the fullest extent it would have been had every individual retirement account been emptied that year. Basis is therefore **not** recovered proportionately, and it is preserved for later distributions. This is favourable, and it is the reverse of the aggregation rule that governs conversions in Module 08.

#### 5.9 Beneficiaries — the ten-year rule

The projection models a living owner, so beneficiary rules sit outside its horizon. They are stated here because Modules 28 and 31 depend on what an heir actually receives.

For deaths after 2019, the SECURE Act requires most **designated beneficiaries** to empty the account by the end of the **tenth calendar year** following the year of death. **Eligible designated beneficiaries** are exempt and may use life expectancy: a surviving spouse, a minor child of the owner, a disabled or chronically ill individual, and a person not more than ten years younger than the owner.

Whether anything must come out **during** those ten years turns on when the owner died.

| Owner died | Distributions in years 1 to 9 |
|---|---|
| **Before** the required beginning date | **None required.** Publication 590-B states: "If the IRA owner dies before the required beginning date and the 10-year rule applies, no distribution is required for any year before the 10th year."[96] |
| **On or after** the required beginning date | Annual distributions are required as well as full distribution by year 10, because the at-least-as-rapidly rule of § 401(a)(9)(B)(i) continues to apply alongside the ten-year limit under the final regulations, which govern distribution calendar years beginning on or after 1 January 2025 |

The second row is stated on the authority of § 401(a)(9)(B)(i) and the final regulations rather than on a quotation from Publication 590-B, which does not address it in the same explicit terms. For a specific inherited account the position should be confirmed against the final regulations before a distribution schedule is set.

The planning consequence is the same either way and is the point Module 31 makes: a pre-tax account inherited by a child is compressed into ten years, frequently landing in the child's peak earning years, and it receives no basis step-up.

#### 5.10 Failure to take a distribution

Section 4974 imposes an excise tax on the amount that should have been distributed and was not. The rate is 25 percent, reduced to 10 percent where the shortfall is corrected within a two-year correction window.[3] The tax is reported on Form 5329, and the Service may waive it where the shortfall was due to reasonable error and reasonable steps are being taken to remedy it.

### 6. Examples and Case Calculations

All figures below are computed, not estimated.

#### Example 1 — Verification against Publication 590-B

An owner with $1,000,000 at the close of the prior year who turns 75 during the distribution year:

```
1,000,000 ÷ 24.6 = $40,650
```

This reproduces the worked example published in Publication 590-B.[3]

#### Example 2 — First distribution at 73

Balance of $850,000 at 31 December; owner turns 73 during the year.

```
850,000 ÷ 26.5 = $32,075
```

The amount is ordinary income in full and is added to whatever other income the year produces.

#### Example 3 — The cost of deferring the first distribution

The same owner defers the first distribution to 1 April of the following year, and the account grows 6 percent in the interim.

| | Amount |
|---|---|
| Age-73 distribution, deferred into year 2 | $32,075 |
| Age-74 distribution, on the grown balance of $901,000 | $35,333 |
| **Total taxable in year 2** | **$67,409** |
| Total taxable in year 2 had the first been taken on time | $35,333 |
| **Additional income bunched into a single year** | **$32,075** |

Deferral is permitted and is occasionally the right choice — where year 1 income is unusually high and year 2 will be low. In the ordinary case it does the opposite of what the taxpayer intends, compressing two distributions into one bracket-filling year and potentially raising the Medicare surcharge determined from that year's income two years later.

#### Example 4 — The trajectory of required distributions

Balance of $1,200,000 at age 73, growing 6 percent annually, with each distribution withdrawn.

| Age | Divisor | Distribution | Closing balance | Required share |
|---|---|---|---|---|
| 73 | 26.5 | $45,283 | $1,224,000 | 3.77% |
| 74 | 25.5 | $48,000 | $1,246,560 | 3.92% |
| 75 | 24.6 | $50,673 | $1,267,640 | 4.07% |
| 80 | 20.2 | $65,988 | $1,342,986 | 4.95% |
| 85 | 16.0 | $84,362 | $1,341,361 | 6.25% |
| 90 | 12.2 | $103,190 | $1,225,069 | 8.20% |

The balance rises for roughly a decade after distributions begin, because growth at 6 percent exceeds a required share below 6 percent. The crossover occurs in the mid-eighties. Required income more than doubles between 73 and 90 while the balance is close to unchanged — the increase is driven entirely by the shrinking divisor.

#### Example 5 — Qualified charitable distribution against the requirement

Owner aged 76, balance $900,000, making a $30,000 QCD.

```
Required distribution   900,000 ÷ 23.7 = $37,975
Satisfied by the QCD                     $30,000   (excluded from income)
Taxable remainder                         $7,975
```

Adjusted gross income rises by $7,975 rather than $37,975. The $30,000 never appears in income, so it does not participate in the calculation of taxable Social Security benefits or in modified adjusted gross income for Medicare purposes.

#### Example 6 — Excise tax on a shortfall

A missed distribution of $42,000 attracts $10,500 at 25 percent, or $4,200 if corrected within the two-year window.

### 7. Interactions with Other Rules

**Taxation of Social Security benefits (Module 14).** A required distribution enters provisional income and can move a benefit from partly taxable to 85 percent taxable. The § 86 thresholds are fixed in statute and are not indexed, so the interaction intensifies over a long projection.

**Medicare surcharge (Module 16).** Modified adjusted gross income determines the Part B and Part D surcharge two years later. The surcharge is a cliff, not a slope: one dollar over a threshold moves the whole premium to the next tier. A required distribution that crosses a threshold raises premiums for a full year, and a distribution that is involuntary cannot be timed away.

**Net investment income tax (Module 06).** The distribution is not itself net investment income, but it increases modified adjusted gross income, which can expose other investment income to the 3.8 percent tax.

**Rate schedules (Module 01).** Required distributions set a floor under ordinary income. Where they exceed spending, the excess is taxed and reinvested in a taxable account, converting tax-deferred growth into currently taxed growth.

**Roth conversions (Module 10).** A conversion before the applicable age reduces the pre-tax balance and therefore every future required distribution. The window between retirement and the applicable age is where that trade is cheapest.

**Estate treatment (Modules 28 and 31).** Pre-tax retirement balances are income in respect of a decedent under § 691. They receive no basis step-up, and the heir pays ordinary income tax on withdrawal. A pre-tax balance is therefore worth materially less to an heir than a taxable account of the same size.

### 8. Common Scenarios and Edge Cases

**A qualified charitable distribution cannot go to a donor advised fund.** Section 408(d)(8)(B)(i) excludes both donor advised funds and supporting organisations. This is the single most common way the distribution is spoiled, because the client already has the fund.

**The account owner does not need the money.** The requirement is unaffected. The distribution is taxed, and what remains after tax moves to a taxable account where future growth is taxed annually rather than deferred.

**The owner turns the applicable age late in the year.** The divisor is set by the age attained during the year, not by age on the distribution date. A birthday on 30 December produces the same divisor as one on 2 January of the same year.

**A younger spouse is the sole beneficiary.** Where the age gap exceeds ten years, the Joint and Last Survivor Table applies and reduces the requirement. The spouse must be the sole beneficiary for the entire year; naming a contingent beneficiary does not defeat this, but naming a second primary beneficiary does.

**Multiple employer plans.** Each 401(k) and each 457(b) requires its own distribution. Aggregating them the way IRAs are aggregated leaves a shortfall in every plan from which nothing was taken, and each shortfall carries its own excise tax.

**The still-working participant who owns the business.** An owner of more than five percent cannot use the still-working exception. This catches a large share of the professional-practice and closely-held-business population, who are often the taxpayers most confident that the exception applies to them.

**Roth balances in an employer plan.** Before 2024 a designated Roth account was subject to lifetime distributions and a Roth IRA was not, which made rolling the former into the latter a routine step. SECURE 2.0 § 325 removed the difference. The rollover may still be advantageous for other reasons, but it is no longer required to avoid a distribution.

**The first year of a surviving spouse.** Where the deceased spouse was younger, the § 327 election permits the survivor to be treated as the deceased employee, delaying distributions until the deceased would have reached the applicable age. Where the deceased was older, a spousal rollover treating the account as the survivor's own is usually simpler. The choice is made once and is difficult to reverse.

### 9. Planning Implications

The window between the end of earned income and the applicable age is the central planning opportunity in the system. For a taxpayer born in 1960 or later retiring at 62, it is thirteen years in which taxable income can be very low and is largely within the taxpayer's control. Income recognised there — through Roth conversions or realisation of gain — is taxed at rates that will not be available again once distributions begin.

Reducing the pre-tax balance before the applicable age reduces every subsequent required distribution, and the effect compounds. It also reduces the balance that will pass to heirs as income in respect of a decedent.

Qualified charitable distributions are the only route by which a required distribution can be satisfied without the amount entering adjusted gross income. For a charitably inclined taxpayer over 70½ this dominates the alternative of taking the distribution and claiming a deduction, because the deduction does not affect the Social Security, Medicare or net investment income calculations.

Deferring the first distribution to the following 1 April should be treated as an exception requiring justification rather than a default. It is right only where the first year's marginal rate is materially higher than the second's.

Where a spouse is more than ten years younger, confirming sole beneficiary status each year is worth the administrative effort, since it directly reduces the required amount.

### 10. Data Tables for the Engine

| Constant | Value | Indexed |
|---|---|---|
| Applicable age, born before 1951 | 72 | Fixed by statute |
| Applicable age, born 1951–1959 | 73 | Fixed by statute |
| Applicable age, born 1960 or later | 75 | Fixed by statute |
| Uniform Lifetime Table | See § 5.3, ages 72–120 | Revised by regulation, not annually indexed |
| Required beginning date | 1 April following the applicable-age year | Fixed |
| Excise tax on a shortfall | 25%, or 10% if timely corrected | Fixed by statute |
| QCD annual limit | $111,000 | Yes — § 408(d)(8), Notice 2025-67 |
| QCD split-interest one-time limit | $55,000 | Yes |
| QCD minimum age | 70½ | Fixed |
| Roth IRA lifetime requirement | None | — |
| Designated Roth account lifetime requirement | None from 2024 | — |

Related 2026 amounts from the same notice, used by Modules 07 and 08: § 402(g) elective deferral $24,500; age-50 catch-up $8,000; ages 60–63 catch-up $11,250; § 415(c) annual additions $72,000; IRA contribution $7,500 with a $1,100 catch-up; mandatory Roth catch-up wage threshold $150,000.[4]

### 11. References

[1] 26 U.S.C. § 401(a)(9), *Required distributions*. United States Code, Office of the Law Revision Counsel. https://www.govinfo.gov/app/collection/uscode

[2] Treas. Reg. § 1.401(a)(9)-5, *Required minimum distributions from defined contribution plans*, and § 1.401(a)(9)-9, *Life expectancy and distribution period tables*. Electronic Code of Federal Regulations. https://www.ecfr.gov/current/title-26

[3] Internal Revenue Service, *Retirement plan and IRA required minimum distributions FAQs*. https://www.irs.gov/retirement-plans/retirement-plan-and-ira-required-minimum-distributions-faqs

[4] Internal Revenue Service, *Notice 2025-67, 2026 Amounts Relating to Retirement Plans and IRAs*. https://www.irs.gov/pub/irs-drop/n-25-67.pdf

[5] Internal Revenue Service, *Publication 590-B, Distributions from Individual Retirement Arrangements (IRAs)*. https://www.irs.gov/pub/irs-pdf/p590b.pdf

[6] SECURE 2.0 Act of 2022, Division T of P.L. 117-328, §§ 107, 325 and 327. https://www.govinfo.gov/

[95] 26 U.S.C. § 408(d)(8), *Distributions for charitable purposes*, subparagraphs (A), (B)(i), (D) and (F). United States Code, Office of the Law Revision Counsel. https://www.govinfo.gov/app/collection/uscode

[96] Internal Revenue Service, *Publication 590-B, Distributions from Individual Retirement Arrangements*, "Payment under the 10-year rule". https://www.irs.gov/publications/p590b

### 12. Status in This System

| Layer | Status |
|---|---|
| Projection engine | **Applied.** The applicable age is derived from year of birth across all three cohorts, and the Uniform Lifetime Table is implemented in full for ages 72 to 120. The prior year-end balance is used as the numerator. Roth balances are correctly excluded. The qualified charitable distribution limit of $111,000 is current and was verified against Notice 2025-67 in September 2026, as were all related contribution limits. |
| Backend (`tax-be`) | **Not applied.** The backend does not model required distributions. It projects the deployment of tax savings across six buckets and holds no § 401(a)(9) logic. |
| Known limitations | Six cases from the register are not modelled, each of which can change a projected figure for a living taxpayer. The required beginning date is not implemented, so the projection cannot show the two-distributions-in-one-year outcome of Example 3. The Joint and Last Survivor Table is not implemented, so a household with a spouse more than ten years younger is shown a distribution that is too large. The still-working exception and its five-percent-owner carve-out are not implemented, so a participant working past the applicable age is shown distributions beginning earlier than they would. Aggregation is not modelled separately, since pre-tax accounts are carried as a single balance; this is correct in aggregate but cannot surface a per-plan compliance failure. The § 4974 excise tax is not modelled, as the projection assumes compliance. The surviving spouse election under SECURE 2.0 § 327 is not implemented. |


---

## Module 10 — Roth IRA and Roth 401(k)

**Tax year:** 2026 · **As of:** September 2026 · **Primary authority:** IRC §§ 408A, 402A

---

### 1. Overview and Purpose

A Roth account reverses the ordinary bargain. Contributions are made after tax, and qualified distributions of both principal and earnings are free of income tax. Neither a Roth individual retirement account nor, since 2024, a designated Roth account in an employer plan is subject to required minimum distributions during the owner's lifetime.

Two features generate most of the confusion in practice. The first is that there are **two different five-year rules**, doing different jobs. One determines whether earnings come out tax free; it starts once, with the first Roth individual retirement account contribution the taxpayer ever makes, and never restarts. The other determines whether a converted amount escapes the ten percent early distribution tax; it starts separately for each conversion. A taxpayer can satisfy one and not the other.

The second is that a Roth individual retirement account and a designated Roth account inside a 401(k) or 403(b) are different creatures. They have separate clocks, separate ordering rules, and separate distribution treatment, and a rollover from the plan to the account does not carry the plan's holding period across.

For a projection to age 90, the Roth account matters less for its own return than for what it removes from the pre-tax balance. Every dollar converted before the required beginning date reduces every future required distribution, the taxable share of Social Security, the base for the net investment income tax, and the income that sets the Medicare surcharge two years later. Conversions are the principal lever available in the years between retirement and the first required distribution.

### 2. Governing Law and Authorities

| Type | Citation | What it establishes |
|---|---|---|
| Statute | IRC § 408A(c)(2), (3) | Contribution limit and income phase-out |
| Statute | IRC § 408A(d)(1) | Qualified distributions excluded from gross income |
| Statute | IRC § 408A(d)(2) | Definition of a qualified distribution and the five-year nonexclusion period |
| Statute | IRC § 408A(d)(3) | Conversions; no income limit |
| Statute | IRC § 408A(d)(3)(F) | Ten percent tax on a converted amount distributed within five years |
| Statute | IRC § 408A(d)(4) | Aggregation and ordering rules |
| Statute | IRC § 402A | Designated Roth contributions in an employer plan |
| Statute | IRC § 72(t) | Ten percent additional tax on early distributions |
| Legislation | SECURE 2.0 Act § 325 | Designated Roth accounts removed from lifetime required distributions |
| Legislation | P.L. 115-97 (TCJA) | Recharacterisation of a conversion repealed |

### 3. Key Definitions

| Term | Definition |
|---|---|
| **Qualified distribution** | A distribution made after the five-taxable-year nonexclusion period **and** on or after age 59½, on death, on disability within § 72(m)(7), or as a qualified special purpose distribution.[21] Both conditions must hold. |
| **Nonexclusion period** | The five-taxable-year period beginning with the first taxable year for which the individual made any contribution to any Roth individual retirement account. One period per person, for life. |
| **Conversion clock** | A separate five-taxable-year period beginning with the year of each conversion, governing only the ten percent additional tax. |
| **Designated Roth account** | A Roth subaccount within a 401(k), 403(b) or governmental 457(b) plan, governed by § 402A. |
| **Qualified special purpose distribution** | A first-time homebuyer distribution to which § 72(t)(2)(F) applies, capped at $10,000 in a lifetime. |

### 4. Who Is Affected

Any individual with compensation below the § 408A(c)(3) phase-out may contribute directly. For 2026 the ranges are $242,000 to $252,000 on a joint return, $153,000 to $168,000 for single and head of household filers, and $0 to $10,000 for a married taxpayer filing separately.[15]

Conversions are available to everyone. There has been no income limit on a conversion since 2010, and none on the amount converted.

Designated Roth accounts in an employer plan have **no income limit at all**, which makes them the accessible route for high earners whose income excludes a direct Roth individual retirement account contribution. From 2026 certain participants have no choice: catch-up contributions must be designated Roth where prior-year wages from the sponsor exceeded $150,000, as Module 07 sets out.

### 5. Core Rules and Calculations

#### 5.1 Case Register

| # | Case | Applied |
|---|---|---|
| 1 | Contributions are after tax | Yes |
| 2 | Qualified distributions excluded from income | Yes |
| 3 | § 408A(c)(3) income phase-out on direct contributions | Constants held; not applied to limit contributions |
| 4 | Conversions have no income limit | Yes |
| 5 | Conversion taxable to the extent not a return of basis | **No** — conversions are treated as fully taxable |
| 6 | Five-year nonexclusion period for earnings | **No** |
| 7 | Separate five-year clock per conversion for the ten percent tax | **No** |
| 8 | Age 59½ condition for a qualified distribution | **No** |
| 9 | § 408A(d)(4) ordering: contributions, then conversions, then earnings | **No** |
| 10 | Conversions withdrawn first-in first-out, taxable portion first | **No** |
| 11 | Roth accounts aggregated separately from traditional accounts | Yes, in effect — balances are held separately |
| 12 | No lifetime required distributions, Roth IRA | Yes |
| 13 | No lifetime required distributions, designated Roth from 2024 | Yes |
| 14 | Designated Roth clock does not carry over on rollover to a Roth IRA | **No** |
| 15 | Recharacterisation of a conversion unavailable | Yes, in effect — no recharacterisation is offered |
| 16 | § 72(t) ten percent additional tax generally | **No** |
| 17 | Qualified special purpose distribution, $10,000 lifetime | **No** |
| 18 | Beneficiary distribution rules after death | **No** |

#### 5.2 What makes a distribution qualified

Section 408A(d)(2) requires **both** limbs:

```
qualified = ( outside the 5-taxable-year nonexclusion period )
            AND
            ( age ≥ 59½  OR  death  OR  disability  OR  first-time homebuyer )
```

Failing either limb does not make the whole distribution taxable. It makes only the **earnings** taxable, because the ordering rules bring contributions out first.

#### 5.3 The two five-year rules

This is the single most misunderstood area, and the rules answer different questions.

| | Nonexclusion period, § 408A(d)(2)(B) | Conversion clock, § 408A(d)(3)(F) |
|---|---|---|
| **Question it answers** | Are **earnings** tax free? | Does the **ten percent tax** apply to a converted amount? |
| **How many clocks** | One, for life | One per conversion |
| **Starts** | First taxable year for which any Roth IRA contribution was made | The taxable year of that conversion |
| **Restarts** | Never | Not applicable |
| **Irrelevant once** | — | The taxpayer reaches 59½ |

A taxpayer aged 62 who opens a first Roth individual retirement account and converts has satisfied the age limb but not the nonexclusion period. Contributions and converted principal come out free at any time; **earnings** are taxable until the fifth taxable year has run.

Conversely a taxpayer aged 45 who has held a Roth account for twenty years and converts today may withdraw the converted amount, but the ten percent tax applies to it for five years under § 408A(d)(3)(F), which treats the amount as if it were includible in gross income for § 72(t) purposes.[21]

Both clocks run in **taxable years**, not in 365-day periods. A conversion on 31 December 2026 starts a clock whose first taxable year is 2026, so it completes at the start of 2031 — four years and one day later in practice.

#### 5.4 The ordering rules — § 408A(d)(4)

Every distribution from a Roth individual retirement account is treated as coming out in a fixed order, regardless of what the taxpayer intends:[21]

```
1. Regular contributions            — always tax free, always penalty free
2. Conversions, first-in first-out  — within each conversion, the portion that was
                                       taxable on conversion comes out first
3. Earnings                         — taxable and penalty-exposed unless qualified
```

All Roth individual retirement accounts are treated as one for this purpose. Section 408A(d)(4)(A) applies the § 408(d)(2) aggregation separately to Roth accounts, so Roth and traditional accounts are never blended together.

The practical effect is protective. A taxpayer who has contributed $60,000 over the years may withdraw up to $60,000 at any age, for any reason, with no tax and no penalty, because contributions are deemed to come out first.

#### 5.5 Designated Roth accounts — § 402A

A designated Roth account inside an employer plan differs from a Roth individual retirement account in four ways that matter:

| | Roth IRA | Designated Roth account |
|---|---|---|
| Income limit on contributions | Yes | **None** |
| Annual amount | $7,500 plus $1,100 | $24,500 plus catch-up |
| Five-year clock | One, personal, for life | Per plan; starts with the first contribution to **that** plan |
| Ordering on a non-qualified distribution | Contributions first | **Pro rata** between basis and earnings, under § 72 |
| Lifetime required distributions | Never | None from 2024, under SECURE 2.0 § 325 |

The clock does not travel. Rolling a designated Roth account into a Roth individual retirement account brings the money under the Roth IRA's own clock. Where the individual has held a Roth IRA for many years, the rollover **shortens** the wait. Where the individual has never held one, the rollover starts a fresh five-year period even though the plan account may have been open for a decade — which is an argument for opening a Roth individual retirement account with a small contribution early, purely to start the clock.

#### 5.6 Conversions

A conversion is a distribution from a traditional account contributed to a Roth account. It is includible in gross income to the extent it is not a return of basis, and § 72(t) does not apply to the conversion itself.

Three consequences follow for a projection:

- The conversion is **ordinary income** in the year of conversion, stacked on top of everything else.
- It raises modified adjusted gross income, so it can expose investment income to the net investment income tax in that year and raise the Medicare surcharge two years later.
- It is **irrevocable**. Recharacterisation of a conversion was repealed by the Tax Cuts and Jobs Act, so a conversion made when markets were higher cannot be undone.

Where the taxpayer holds basis in traditional accounts, the taxable portion is determined pro rata under § 408(d)(2), as Module 08 sets out.

### 6. Examples and Case Calculations

#### Example 1 — Contributions are always available

A taxpayer aged 45 has contributed $7,000 a year for eight years, $56,000 in total, and the account is worth $92,000.

```
Withdrawal of $50,000
   Ordering: contributions first, up to $56,000
   Taxable                                   $0
   Ten percent additional tax                $0
```

The whole amount is a return of contributions. Age and the five-year period are both irrelevant, because neither limb is reached.

#### Example 2 — Earnings withdrawn too early

The same taxpayer withdraws the full $92,000.

```
Contributions      56,000   tax free
Earnings           36,000   not a qualified distribution — taxable,
                            plus ten percent additional tax
Tax at 24 percent   8,640
Additional tax      3,600
                   ------
Total cost        $12,240
```

#### Example 3 — The nonexclusion period for a late starter

A taxpayer aged 62 opens a first Roth individual retirement account in 2026 and converts $200,000.

```
Age limb            satisfied — over 59½
Five-year limb      not satisfied until the 2031 taxable year

Converted principal   available at any time, tax and penalty free
Earnings              taxable if withdrawn before 2031
```

The age of the taxpayer does not shorten the nonexclusion period. Opening the account with a small contribution five years earlier would have removed the constraint entirely.

#### Example 4 — Conversion in the pre-distribution window

A married couple, both 66, retired, with $180,000 of taxable income before any conversion and $1,400,000 in a traditional account. The 24 percent bracket runs to $403,550.

```
Room in the 24 percent bracket   403,550 − 180,000 = 223,550
Conversion of                                        223,550
Tax at 24 percent                                     53,652
```

Converting to the top of the bracket each year for the seven years to age 73 moves roughly $1,560,000 at a known 24 percent, against a balance that would otherwise be forced out at rates set by the required distribution schedule and by whatever the survivor's single-filer schedule turns out to be. The cost is that modified adjusted gross income of $403,550 sets the Medicare surcharge two years later, at a tier the couple should expect rather than discover.

#### Example 5 — The plan clock does not travel

A participant aged 60 has held a designated Roth account in a 401(k) since 2016 and has never held a Roth individual retirement account. On retiring in 2026 they roll the plan account into a newly opened Roth individual retirement account.

```
Designated Roth account clock    began 2016 — complete
Roth IRA clock                   begins 2026 — complete in 2031
```

Ten years of holding period are lost for the purpose of the receiving account. Earnings withdrawn before 2031 are taxable. Opening a Roth individual retirement account with $1 in any earlier year would have started the personal clock and preserved the outcome.

### 7. Interactions with Other Rules

**Required minimum distributions (Module 09).** Roth accounts are outside the lifetime requirement, so a conversion permanently reduces every future required distribution. This is the largest structural benefit and it compounds.

**IRA rules and basis (Module 08).** The § 408(d)(2) aggregation determines how much of a conversion is taxable. Roth accounts are aggregated separately from traditional ones.

**Employer plan limits (Module 07).** The mandatory Roth catch-up from 2026 forces designated Roth treatment on high earners, which builds Roth balances that are then outside the lifetime distribution rules.

**Net investment income tax (Module 06).** A conversion is not net investment income but raises modified adjusted gross income, and can therefore expose other investment income to the 3.8 percent tax in the conversion year.

**Medicare surcharge (Module 16).** The surcharge is set by modified adjusted gross income from two years earlier. A conversion at 63 sets the premium at 65. This lag is the most commonly overlooked cost of a conversion programme.

**Taxation of Social Security (Module 14).** A conversion raises provisional income and can push benefits to 85 percent taxable in the conversion year. Converting before benefits begin avoids the interaction entirely.

**Estate and step-up (Module 31).** A Roth account passes to heirs free of income tax, unlike a pre-tax balance, which is income in respect of a decedent and receives no step-up. Conversion shifts the burden from the heir to the owner at the owner's own rate.

### 8. Common Scenarios and Edge Cases

**The two five-year rules are not the same rule.** One governs earnings, the other governs the penalty on converted amounts. A taxpayer over 59½ never faces the second.

**The clock counts taxable years, not calendar months.** A conversion in December buys almost a full year of the period at no cost, which is why late-December conversions are common.

**Contributions can always come out.** The ordering rules make a Roth individual retirement account the most liquid retirement vehicle available, which is worth knowing before treating it as untouchable.

**A designated Roth account uses pro-rata ordering, not contributions-first.** A non-qualified distribution from a plan Roth account carries out basis and earnings proportionately under § 72, so it is less forgiving than a Roth individual retirement account.

**Conversions cannot be undone.** Recharacterisation was repealed for conversions by the Tax Cuts and Jobs Act. A conversion made at a market peak stays converted, which argues for converting in instalments rather than at once.

**A conversion is not subject to withholding requirements in the way a plan distribution is**, but withholding from the converted amount itself is a costly error: the withheld amount is treated as a distribution, not converted, and may attract the ten percent tax. Tax on a conversion should be paid from outside funds.

**There is no age limit and no requirement to have compensation for a conversion**, unlike a contribution.

**Inherited Roth accounts are not free of distribution requirements.** The owner escapes lifetime distributions; the beneficiary does not, and most non-spouse beneficiaries must empty the account within ten years. The distributions remain tax free if the five-year period has run.

### 9. Planning Implications

The years between the end of earned income and the required beginning date are when conversions are cheapest, because taxable income is low and controllable. For a taxpayer born in 1960 or later retiring at 62, that window is thirteen years. Module 09 sets out why it exists.

Conversion capacity should be measured against a bracket ceiling rather than a fixed dollar figure, and the ceiling that matters may not be the tax bracket. The Medicare surcharge tiers and the net investment income tax threshold frequently bind first, and the surcharge does so with a two-year delay that has to be planned for rather than observed.

Opening a Roth individual retirement account early, even with a token contribution, starts the personal five-year clock and is close to free. For anyone who may later roll a designated Roth account out of a plan, it is the difference between an immediate qualified distribution and a five-year wait.

Tax on a conversion should be paid from taxable funds rather than withheld from the conversion. Withholding reduces the amount that reaches the Roth account and, before 59½, converts part of the transaction into a penalised distribution.

For a couple, the asymmetry described in Module 03 argues for converting while both are alive. The same income recognised by a survivor is taxed on the single schedule with roughly half the deduction.

### 10. Data Tables for the Engine

| Constant | 2026 value | Indexed |
|---|---|---|
| Roth IRA contribution limit | $7,500, plus $1,100 catch-up | Yes |
| Phase-out, joint and surviving spouse | $242,000 – $252,000 | Yes |
| Phase-out, single and head of household | $153,000 – $168,000 | Yes |
| Phase-out, married filing separately | $0 – $10,000 | **No** |
| Conversion income limit | None | — |
| Nonexclusion period | 5 taxable years from the first Roth IRA contribution | Fixed |
| Conversion clock | 5 taxable years per conversion, for § 72(t) only | Fixed |
| Qualified distribution age | 59½ | Fixed |
| First-time homebuyer distribution | $10,000 lifetime | **No** |
| Lifetime required distributions, Roth IRA | None | — |
| Lifetime required distributions, designated Roth | None from 2024 | — |
| Recharacterisation of a conversion | Not available | — |

### 11. References

[21] 26 U.S.C. § 408A, including subsections (c)(3), (d)(2), (d)(3)(F) and (d)(4). United States Code, Office of the Law Revision Counsel. https://www.govinfo.gov/app/collection/uscode

[15] Internal Revenue Service, *Notice 2025-67, 2026 Amounts Relating to Retirement Plans and IRAs*. https://www.irs.gov/pub/irs-drop/n-25-67.pdf

[22] 26 U.S.C. § 402A, *Optional treatment of elective deferrals as Roth contributions*. https://www.govinfo.gov/app/collection/uscode

[3] Internal Revenue Service, *Retirement plan and IRA required minimum distributions FAQs*. https://www.irs.gov/retirement-plans/retirement-plan-and-ira-required-minimum-distributions-faqs

### 12. Status in This System

| Layer | Status |
|---|---|
| Projection engine | **Applied in part.** Roth balances are held separately from pre-tax balances and are correctly excluded from the required minimum distribution computation, for both Roth individual retirement accounts and designated Roth accounts. Conversions are modelled during the window between retirement and the required beginning date, and correctly carry no income limit. The § 408A phase-out ranges are held as constants and match Notice 2025-67 for all five filing statuses. |
| Backend (`tax-be`) | **Not applied.** No Roth logic. |
| Known limitations | Neither five-year rule is implemented. The nonexclusion period under § 408A(d)(2)(B) is absent, so a modelled distribution of earnings is treated as tax free even where the period has not run, and the separate conversion clock under § 408A(d)(3)(F) is absent, so no ten percent additional tax is applied to a converted amount withdrawn early. The age 59½ condition is not tested. The § 408A(d)(4) ordering rules are not implemented, so the engine cannot represent the position that contributions are always available tax and penalty free, nor the first-in first-out treatment of successive conversions. A conversion is treated as fully taxable because basis is not tracked, which overstates tax for any taxpayer with non-deductible contributions — the same limitation recorded in Module 08. The distinction between a Roth individual retirement account and a designated Roth account is not modelled, so the pro-rata ordering that applies to plan accounts and the fact that a plan holding period does not carry across on rollover are both absent. Beneficiary treatment after death is outside the projection horizon and is not modelled. |


---

## Module 11 — Social Security Retirement Benefits

**Tax year:** 2026 · **As of:** September 2026 · **Primary authority:** Social Security Act §§ 202, 203, 215

---

### 1. Overview and Purpose

A retirement benefit is built in five steps. Covered earnings are indexed to national average wages, the highest thirty-five indexed years are averaged into a monthly figure, that figure is run through a three-band formula to produce the primary insurance amount, the result is adjusted for the age at which the worker claims, and cost-of-living increases are applied.

Each step has its own rounding rule and its own authority, and the order cannot be rearranged. The most consequential feature is that cost-of-living adjustments accrue from the year the worker attains **age 62**, whatever age they actually claim at. A worker claiming at 70 does not begin at the 2026 formula result; they begin at that result increased by eight years of adjustments and then increased by the delayed retirement credit. Treating the adjustments as starting at the claiming age understates a late claimer's benefit for the rest of their life.

The benefit is the only inflation-indexed, guaranteed income most households will have, and the claiming decision is irreversible in practice. It is also the input that drives the taxation of benefits in Module 14, the provisional income calculation, and — through the survivor rules in Module 12 — the largest single income event in a married couple's projection.

### 2. Governing Law and Authorities

| Type | Citation | What it establishes |
|---|---|---|
| Statute | Social Security Act § 215(a) | The primary insurance amount formula and bend points |
| Statute | Social Security Act § 215(b) | Average indexed monthly earnings |
| Statute | Social Security Act § 215(i) | Cost-of-living adjustments, accruing from age 62 |
| Statute | Social Security Act § 202(q) | Reduction for claiming before full retirement age |
| Statute | Social Security Act § 202(w) | Delayed retirement credits |
| Statute | Social Security Act § 203(f) | Retirement earnings test |
| Statute | Social Security Act § 203(a) | Family maximum — see Module 13 |
| Regulation | 20 CFR § 404.313 | Delayed retirement credit rates |
| Regulation | 20 CFR § 404.430 | Recomputation at full retirement age for months withheld |
| Legislation | P.L. 118-273 | Repeal of the Windfall Elimination Provision and Government Pension Offset |
| Determination | Federal Register 2025-19763 | 2026 bend points, wage index, cost-of-living increase, earnings test amounts |

### 3. Key Definitions

| Term | Definition |
|---|---|
| **Average indexed monthly earnings (AIME)** | The highest thirty-five years of covered earnings, each indexed to the national average wage index for the year the worker attains 60, summed and divided by 420. Rounded **down** to the next lower dollar. |
| **Primary insurance amount (PIA)** | The benefit payable at full retirement age, produced by applying the three-band formula to AIME. Rounded **down** to the next lower ten cents. |
| **Full retirement age (FRA)** | The age at which the primary insurance amount is payable unreduced. 67 for those born in 1960 or later. |
| **Bend points** | The two AIME levels at which the formula percentage changes. $1,286 and $7,749 for workers first eligible in 2026. |
| **Delayed retirement credit** | An increase of two thirds of one percent for each month claiming is deferred past full retirement age, to age 70. |
| **Quarter of coverage** | The unit of insured status. $1,890 of covered earnings in 2026, four a year maximum, forty needed for retirement benefits. |

### 4. Who Is Affected

Workers with forty quarters of coverage, from age 62. The benefit may be claimed at any month from 62 to 70; deferring beyond 70 produces no further increase.

Since the Social Security Fairness Act, **P.L. 118-273**, signed 5 January 2025 and applying to benefits payable for months after December 2023, the Windfall Elimination Provision and the Government Pension Offset are repealed.[23] A worker with a pension from non-covered employment is no longer subject to a reduced formula, and a spouse or survivor with such a pension is no longer offset. Advisers continue to assume both provisions apply, and they do not.

### 5. Core Rules and Calculations

#### 5.1 Case Register

| # | Case | Applied |
|---|---|---|
| 1 | AIME from the highest 35 indexed years | **No** — the benefit is taken from a statement figure or a proxy |
| 2 | Wage indexing to the year of attaining 60 | **No** |
| 3 | AIME rounded down to the next lower dollar | **No** |
| 4 | Three-band PIA formula | Yes |
| 5 | Bend points derived from the wage index ratio | Yes |
| 6 | PIA rounded down to the next lower ten cents | Yes |
| 7 | Reduction of 5/9 of 1% for the first 36 months early | Yes |
| 8 | Reduction of 5/12 of 1% for months beyond 36 | Yes |
| 9 | Delayed retirement credit of 2/3 of 1% a month to 70 | Yes |
| 10 | No credit accrues past age 70 | Yes |
| 11 | Cost-of-living adjustments accrue from age **62** | **No** — D1 |
| 12 | Earnings test, $1 withheld per $2 over the lower amount | Yes |
| 13 | Earnings test, $1 withheld per $3 in the year FRA is reached | Yes |
| 14 | Earnings test ceases at full retirement age | Yes |
| 15 | Withheld months restored by recomputation at FRA | **No** — D2 |
| 16 | Earnings test applies only to earned income | Yes |
| 17 | Recomputation for continued earnings after claiming | **No** |
| 18 | Family maximum under § 203(a) | **No** — D4, see Module 13 |
| 19 | Windfall Elimination Provision | Correctly absent — repealed |
| 20 | Government Pension Offset | Correctly absent — repealed |
| 21 | Quarters of coverage and insured status | **No** |

#### 5.2 Step one — average indexed monthly earnings

Each year of covered earnings, up to that year's contribution and benefit base, is multiplied by the ratio of the national average wage index for the year the worker attains 60 to the index for the year of the earnings. Years after age 60 are taken at face value. The highest thirty-five indexed years are summed and divided by 420, and the result is rounded **down** to the next lower dollar.

Years with no covered earnings enter as zeros. A worker with thirty years of earnings has five zeros in the computation, and additional work later in life replaces those zeros rather than adding to the total — which is why continued work at modest earnings can still raise a benefit.

#### 5.3 Step two — the primary insurance amount

For a worker first eligible in 2026:[24]

```
PIA = 0.90 × the first $1,286 of AIME
    + 0.32 × AIME between $1,286 and $7,749
    + 0.15 × AIME above $7,749
```

rounded down to the next lower ten cents.

The bend points are not arbitrary. They are the 1979 amounts of $180 and $1,085, multiplied by the ratio of the national average wage index for 2024 to the index for 1977:

```
$180   × ($69,846.57 ÷ $9,779.44) = $1,285.7  → $1,286
$1,085 × ($69,846.57 ÷ $9,779.44) = $7,749.4  → $7,749
```

Both reproduce the published figures exactly, which confirms the constants and the method together.

| AIME | PIA | Replacement rate |
|---|---|---|
| $5,000 | $2,345.80 | 46.9% |
| $7,000 | $2,985.80 | 42.7% |
| $10,000 | $3,563.20 | 35.6% |
| $12,000 | $3,863.20 | 32.2% |

The falling replacement rate is the deliberate design of the formula. It is progressive, and a high earner receives a much smaller proportion of their earnings back than a low earner.

#### 5.4 Step three — the claiming adjustment

Claiming before full retirement age reduces the benefit by five ninths of one percent for each of the first thirty-six months, and five twelfths of one percent for each month beyond that. Claiming after full retirement age adds two thirds of one percent a month, to age 70.

| Claiming age | Months from FRA | Factor | On a $3,000 PIA |
|---|---|---|---|
| 62 | 60 early | **70.00%** | $2,100.00 |
| 63 | 48 early | 75.00% | $2,250.00 |
| 64 | 36 early | 80.00% | $2,400.00 |
| 65 | 24 early | 86.67% | $2,600.00 |
| 66 | 12 early | 93.33% | $2,800.00 |
| **67** | — | **100.00%** | $3,000.00 |
| 68 | 12 late | 108.00% | $3,240.00 |
| 69 | 24 late | 116.00% | $3,480.00 |
| **70** | 36 late | **124.00%** | $3,720.00 |

Claiming at 70 rather than 62 produces **77.1 percent more** each month, for life, on the same earnings record — and the difference is itself indexed thereafter.

Full retirement age depends on year of birth:

| Year of birth | Full retirement age |
|---|---|
| 1943–1954 | 66 |
| 1955 | 66 and 2 months |
| 1956 | 66 and 4 months |
| 1957 | 66 and 6 months |
| 1958 | 66 and 8 months |
| 1959 | 66 and 10 months |
| **1960 or later** | **67** |

#### 5.5 Step four — cost-of-living adjustments

Section 215(i) increases benefits by the change in the consumer price index. The increase effective December 2025, payable in 2026, is **2.8 percent**.[24]

The rule that matters for a projection is **when the adjustments begin to accrue**. They accrue from the year the worker attains **age 62** — the year of first eligibility — regardless of when the worker claims. A worker who turns 62 in 2026 and claims at 70 in 2034 receives a first payment reflecting eight years of intervening adjustments **and** the delayed retirement credit, not merely the credit.

```
benefit at claim = PIA(at age 62 eligibility)
                   × Π (1 + COLA) for each year from age 62 to the claiming year
                   × claiming factor
```

Compounding the adjustments only from the claiming age understates a claim-at-70 benefit by roughly the eight years of increases — at 2.8 percent a year, about **24 percent, permanently**. Because the error grows with deferral, it biases every comparison against delaying, which is the opposite of what the arithmetic in § 5.4 supports.

#### 5.6 The earnings test — § 203(f)

Benefits are withheld where a claimant below full retirement age has earned income above an exempt amount. For 2026:[24]

| Situation | Annual exempt amount | Withholding rate |
|---|---|---|
| Under full retirement age for the whole year | **$24,480** | $1 withheld for every $2 above |
| Reaching full retirement age during the year | **$65,160** | $1 withheld for every $3 above, counting only months before FRA |
| Full retirement age and over | No limit | None |

Only **earned** income counts — wages and net earnings from self-employment. Pensions, distributions from retirement accounts, interest, dividends, rents and capital gains are all excluded, which means a retiree living on portfolio income is unaffected however large that income is.

| Situation | Withheld |
|---|---|
| Under FRA all year, earnings $40,000 | $7,760 |
| Under FRA all year, earnings $60,000 | $17,760 |
| Reaching FRA during the year, earnings $90,000 | $8,280 |

**The withholding is not a loss.** Under § 203 and 20 CFR § 404.430, at full retirement age the benefit is recomputed upward to account for the months in which benefits were withheld, by reducing the number of months of early claiming used in the reduction factor. A claimant who had twelve months withheld is treated at full retirement age as having claimed twelve months later than they did. Over a normal life expectancy the recomputation returns most of what was withheld.

Describing the earnings test as a tax is therefore wrong, and a projection that withholds benefits without ever restoring them permanently understates income from full retirement age onwards.

### 6. Examples and Case Calculations

#### Example 1 — A full computation

A worker with an AIME of $7,000, born in 1964, full retirement age 67.

```
PIA   0.90 × 1,286                       =   1,157.40
    + 0.32 × (7,000 − 1,286)             =   1,828.48
    + 0.15 × 0                           =       0.00
                                             --------
                                             2,985.88 → $2,985.80  rounded down to the dime
```

| Claiming age | Monthly benefit before adjustments |
|---|---|
| 62 | $2,090.06 |
| 67 | $2,985.80 |
| 70 | $3,702.39 |

#### Example 2 — Why the adjustment base year matters

The same worker turns 62 in 2026 and defers to 70 in 2034. Assume 2.8 percent annually throughout.

```
Correct:   2,985.80 × 1.028^8 × 1.24  =  $4,617.34 per month
Incorrect: 2,985.80 × 1.24            =  $3,702.39 per month
```

The difference is **$914.95 a month, $10,979 a year**, and it persists for life. The error arises solely from starting the compounding at the claiming age rather than at age 62.

#### Example 3 — The earnings test and its reversal

A claimant takes benefits at 63 with a $2,250 monthly benefit and earns $60,000.

```
Exempt amount                          24,480
Excess                                 35,520
Withheld at $1 per $2                  17,760   — more than seven months of benefit
```

At full retirement age the reduction factor is recomputed as though those months had never been claimed. The claimant's monthly benefit rises permanently. Treating the $17,760 as lost overstates the cost of working by the whole amount.

### 7. Interactions with Other Rules

**Taxation of benefits (Module 14).** Up to 85 percent of the benefit enters taxable income depending on provisional income. The thresholds are fixed in statute and are not indexed, so the taxable share rises across a long projection.

**Spousal and survivor benefits (Module 12).** The worker's primary insurance amount is the anchor for both. A spousal benefit is up to 50 percent of it, and a survivor benefit reflects what the deceased was actually receiving or entitled to.

**Family maximum (Module 13).** Where a spouse and children draw on one record, § 203(a) caps the total payable. The worker's own benefit is not reduced; the auxiliary benefits are.

**Payroll tax (Module 04).** Covered earnings build the record. Earnings above the contribution base bear no old-age tax and add nothing to AIME.

**Medicare (Modules 15 and 16).** Part B premiums are deducted from the benefit. The hold-harmless provision limits the premium increase for most beneficiaries to the dollar amount of the cost-of-living increase, which links the two directly.

**Required distributions (Module 09).** Distributions are not earned income and never trigger the earnings test, but they do raise provisional income and so increase the taxable share of the benefit.

### 8. Common Scenarios and Edge Cases

**Cost-of-living adjustments accrue from 62, not from claiming.** This is the single most common modelling error in the area and it systematically penalises deferral.

**Thirty-five years always count.** A worker with thirty years of earnings has five zeros averaged in. Additional years of work replace zeros, and even modest earnings can raise the benefit materially.

**Earnings above the contribution base do not raise the benefit.** They are not covered earnings and do not enter AIME.

**The earnings test counts only earned income.** A retiree with $400,000 of portfolio income and no wages has nothing withheld.

**Withheld benefits come back.** The recomputation at full retirement age is automatic and is the reason the earnings test is not a penalty on working.

**Delayed credits stop at 70.** There is no benefit to deferring beyond that month, and a claim filed later simply forfeits payments.

**The Windfall Elimination Provision and the Government Pension Offset no longer exist.** Repealed by P.L. 118-273 for benefits payable after December 2023. A teacher, firefighter or federal employee with a non-covered pension receives the ordinary formula and an unreduced spousal or survivor benefit.

**Claiming is effectively irreversible.** A withdrawal of application under § 404.640 is available within twelve months and requires repayment of everything received, once in a lifetime. A voluntary suspension is available from full retirement age.

### 9. Planning Implications

The claiming decision is a trade between a larger inflation-indexed lifetime income and earlier access to capital. The 77 percent difference between 62 and 70 is a real increase, indexed thereafter, and it is also the base from which a survivor benefit is computed — so for a married couple the higher earner's claiming age sets the floor under the survivor's income for the rest of their life. That second effect usually dominates the first.

For a couple, deferring the **higher** earner's benefit and claiming the **lower** earner's earlier is the standard structure, because only the higher of the two survives the first death.

The years between retirement and claiming are the same years identified in Modules 09 and 10 as the conversion window. Deferring the benefit keeps provisional income low, which makes conversions cheaper. The two decisions are best made together rather than separately.

Where a client intends to work between 62 and full retirement age, the earnings test should be presented as deferral rather than forfeiture. Presenting it as a loss has led many claimants to stop working when the arithmetic did not require it.

### 10. Data Tables for the Engine

| Constant | 2026 value | Indexed |
|---|---|---|
| First bend point | $1,286 | Yes — wage index |
| Second bend point | $7,749 | Yes |
| Formula percentages | 90 / 32 / 15 | Fixed |
| 1979 base bend points | $180 and $1,085 | Fixed |
| National average wage index, 2024 | $69,846.57 | — |
| National average wage index, 1977 | $9,779.44 | Fixed |
| Cost-of-living increase | 2.8% | Annual |
| COLA accrual begins | The year the worker attains 62 | Fixed |
| Full retirement age, born 1960 or later | 67 | Fixed |
| Early reduction, first 36 months | 5/9 of 1% a month | Fixed |
| Early reduction, beyond 36 months | 5/12 of 1% a month | Fixed |
| Delayed retirement credit | 2/3 of 1% a month, to 70 | Fixed |
| Earnings test exempt, under FRA | $24,480 a year | Yes |
| Earnings test exempt, year of FRA | $65,160 a year | Yes |
| Withholding rates | $1 per $2, or $1 per $3 in the FRA year | Fixed |
| Quarter of coverage | $1,890 | Yes |
| AIME rounding | Down to the next lower dollar | Fixed |
| PIA rounding | Down to the next lower ten cents | Fixed |

### 11. References

[23] Social Security Fairness Act of 2023, P.L. 118-273. https://www.govinfo.gov/content/pkg/PLAW-118publ273/html/PLAW-118publ273.htm

[24] *Cost-of-Living Increase and Other Determinations for 2026*, Federal Register document 2025-19763. https://www.federalregister.gov/documents/2025/11/03/2025-19763/cost-of-living-increase-and-other-determinations-for-2026

[25] 20 CFR §§ 404.313 and 404.430. Electronic Code of Federal Regulations. https://www.ecfr.gov/current/title-20

### 12. Status in This System

| Layer | Status |
|---|---|
| Projection engine | **Applied in part.** The three-band formula, both bend points, the formula percentages and the round-down-to-the-dime rule are implemented correctly. The bend points are **derived** from the 1979 base amounts and the wage index ratio rather than hard-coded, and the derivation reproduces the published 2026 figures exactly. The claiming adjustment implements both early reduction rates and the delayed retirement credit at two thirds of one percent a month, correctly capped at 70. The earnings test applies the right exempt amounts and both withholding rates, and correctly ceases at full retirement age and applies only to earned income. The absence of the Windfall Elimination Provision and Government Pension Offset is correct following their repeal. |
| Backend (`tax-be`) | **Not applied.** No Social Security logic of any kind. |
| Known limitations | **Cost-of-living adjustments compound from the claiming age rather than from age 62**, which understates a claim-at-70 benefit by approximately 24 percent for life and biases the system against deferral. Recorded as D1. **Benefits withheld under the earnings test are never restored.** The withheld amount is computed and stored but never read again, while a code comment and a note shown to the user both state that it is added back at full retirement age. Neither statement is true of the implementation. Recorded as D2. The average indexed monthly earnings computation is not implemented: the benefit is taken from a statement figure or, failing that, from a crude proxy applied to current wages, so the thirty-five-year averaging, the wage indexing and the effect of replacing zero years are all absent. Quarters of coverage and insured status are not tracked. The family maximum under § 203(a) is absent, recorded as D4 and treated in Module 13. Recomputation for earnings after claiming is not modelled, and the constant `maxMonthlyFRA` is defined but never referenced anywhere in the engine. |


---

## Module 12 — Spousal and Survivor Benefits

**Tax year:** 2026 · **As of:** September 2026 · **Primary authority:** Social Security Act §§ 202(b), (c), (e), (f), (r)

---

### 1. Overview and Purpose

A worker's earnings record can support benefits for people other than the worker. A spouse may draw up to half the worker's primary insurance amount while the worker lives, and a survivor may draw up to the whole of what the worker was receiving after the worker dies. A divorced spouse married for at least ten years has the same rights, and drawing on the record costs the worker nothing.

Three structural points govern everything in this module.

**Benefits do not add.** A person entitled to their own retirement benefit and to a spouse's or survivor's benefit does not receive both. Social Security policy states the principle plainly: a person's benefit amount can never exceed the highest single benefit to which that person is entitled.[26] The mechanics are expressed as own benefit plus an excess, but the result is the higher of the two.

**Spousal and survivor benefits follow different rules.** The spousal benefit is anchored to the worker's primary insurance amount and never receives delayed retirement credits. The survivor benefit is anchored to what the worker was actually *receiving*, subject to a floor, and does inherit the worker's delayed credits. The two use different reduction rates and different full retirement ages.

**The survivor benefit is the reason a higher earner defers.** On the first death the household loses the smaller of two benefits and keeps the larger. Whatever the higher earner did with their claiming age sets the floor under the survivor's income for the rest of their life, which may be twenty or thirty years. That effect usually outweighs the worker's own lifetime arithmetic.

### 2. Governing Law and Authorities

| Type | Citation | What it establishes |
|---|---|---|
| Statute | Social Security Act § 202(b), (c) | Wife's and husband's benefits |
| Statute | Social Security Act § 202(e), (f) | Widow's and widower's benefits |
| Statute | Social Security Act § 202(b)(2), (c)(2) | Divorced spouse's benefits |
| Statute | Social Security Act § 202(q) | Reduction for early claiming |
| Statute | Social Security Act § 202(r) | Deemed filing |
| Statute | Social Security Act § 202(k) | Dual entitlement |
| Statute | Social Security Act § 203(a) | Family maximum — see Module 13 |
| Guidance | POMS RS 00615.020 | Dual entitlement computation methods |
| Guidance | POMS RS 00615.301 | Reduced widow's benefits, the 28.5 percent maximum |
| Guidance | POMS RS 00615.320 | The reduced retirement benefit limitation, RIB-LIM |
| Legislation | Bipartisan Budget Act of 2015 | Closed restricted application and voluntary suspension strategies |
| Legislation | P.L. 118-273 | Repealed the Government Pension Offset |

### 3. Key Definitions

| Term | Definition |
|---|---|
| **Spousal benefit** | Up to 50 percent of the worker's primary insurance amount, payable while the worker lives. |
| **Survivor benefit** | Up to 100 percent of what the deceased worker was receiving or entitled to receive, subject to the RIB-LIM limitation. |
| **Survivor full retirement age** | The age at which an unreduced survivor benefit is payable. It is **not** the same as retirement full retirement age. |
| **Dual entitlement** | Entitlement to benefits on more than one record. The person receives the higher, computed as their own benefit plus the excess of the other.[26] |
| **Deemed filing** | Under § 202(r), a claim for one benefit is treated as a claim for all benefits for which the claimant is then eligible. |
| **RIB-LIM** | The limitation on a survivor benefit where the deceased had claimed a reduced retirement benefit. |

### 4. Who Is Affected

**Spousal.** A current spouse married at least one year, or a divorced spouse married at least ten years who has not remarried. Where the divorce occurred at least two years ago, the divorced spouse may claim independently even if the worker has not filed.

**Survivor.** A surviving spouse married at least nine months, or a surviving divorced spouse married at least ten years. A survivor may claim from age 60, or from 50 if disabled.

Since the repeal of the Government Pension Offset by **P.L. 118-273**, a spouse or survivor with a pension from non-covered employment is no longer offset. This was a two-thirds reduction that frequently eliminated the benefit entirely, and it no longer applies.

### 5. Core Rules and Calculations

#### 5.1 Case Register

| # | Case | Applied |
|---|---|---|
| 1 | Spousal benefit up to 50 percent of the worker's PIA | Yes |
| 2 | Spousal anchored to PIA regardless of the worker's claiming age | Yes |
| 3 | Spousal reduction, 25/36 of 1% for the first 36 months | Yes |
| 4 | Spousal reduction, 5/12 of 1% beyond 36 months | Yes |
| 5 | No delayed retirement credits on a spousal benefit | Yes |
| 6 | Spouse receives the greater of own benefit and spousal | Yes |
| 7 | Spousal requires the worker to have filed | **No** |
| 8 | One-year marriage requirement | **No** |
| 9 | Divorced spouse, ten-year marriage | **No** |
| 10 | Independently entitled divorced spouse after two years | **No** |
| 11 | Deemed filing under § 202(r) | **No** |
| 12 | Restricted application, born on or before 1 January 1954 | **No** |
| 13 | Survivor receives the higher of the two benefits, never both | Yes |
| 14 | Survivor benefit reduced for early claiming | **No** — D3 |
| 15 | Survivor full retirement age, distinct from retirement FRA | **No** — D3 |
| 16 | Maximum survivor reduction of 28.5 percent at age 60 | **No** — D3 |
| 17 | RIB-LIM limitation | **No** — D3 |
| 18 | Survivor inherits the deceased's delayed retirement credits | **No** |
| 19 | Survivor may claim one benefit and switch to the other later | **No** |
| 20 | Remarriage after 60 does not end a survivor benefit | **No** |
| 21 | Surviving divorced spouse | **No** |
| 22 | Family maximum | **No** — D4, Module 13 |
| 23 | Government Pension Offset | Correctly absent — repealed |

#### 5.2 The spousal benefit

The spousal benefit is up to **50 percent of the worker's primary insurance amount**. Two features are commonly misunderstood.

It is anchored to the worker's **primary insurance amount**, not to what the worker actually receives. If the worker claims at 62 and takes a 30 percent reduction, the spousal benefit is still computed from the unreduced primary insurance amount. The worker's early claiming does not reduce the spouse's entitlement.

It never earns **delayed retirement credits**. Deferring a spousal benefit past full retirement age produces nothing. The maximum is 50 percent, reached at the spouse's own full retirement age, and there is no reason to wait beyond it.

The reduction for early claiming uses a different rate from the worker's own benefit — twenty-five thirty-sixths of one percent for the first thirty-six months, then five twelfths of one percent:

| Spouse's claiming age | Percentage of the worker's PIA |
|---|---|
| 62 | **32.500%** |
| 63 | 35.000% |
| 64 | 37.500% |
| 65 | 41.667% |
| 66 | 45.833% |
| **67 and later** | **50.000%** |

A spouse eligible for their own benefit receives the **greater** of the two, not the sum.

#### 5.3 Deemed filing

Section 202(r), as amended by the Bipartisan Budget Act of 2015, treats a claim for one benefit as a claim for every benefit the claimant is then eligible for. A spouse cannot claim only the spousal benefit while letting their own grow.

The **restricted application** — claiming spousal only and switching to one's own benefit at 70 — survives only for those born **on or before 1 January 1954**. Everyone in that cohort is now 72 or older, so the strategy is closed to new claimants and should not appear in any current projection.

**Voluntary suspension** was also curtailed. From full retirement age a claimant may suspend to earn delayed credits, but during suspension no one else may draw on their record, which removed the file-and-suspend strategy.

#### 5.4 The survivor benefit

A survivor may claim from age **60**, four years earlier than any other benefit. The amount is up to 100 percent of what the deceased was receiving or entitled to receive.

**Survivor full retirement age is not retirement full retirement age.** The two schedules were legislated separately:

| Year of birth | Survivor FRA |
|---|---|
| 1956 or earlier | 66 |
| 1957 | 66 and 2 months |
| 1958 | 66 and 4 months |
| 1959 | 66 and 6 months |
| 1960 | 66 and 8 months |
| 1961 | 66 and 10 months |
| **1962 or later** | **67** |

A person born in 1960 has a retirement full retirement age of 67 but a survivor full retirement age of 66 and 8 months.

The reduction is spread so that the maximum is **28.5 percent** at age 60, whatever the survivor's full retirement age.[27] For a survivor whose full retirement age is 67, the period is eighty-four months and the rate is nineteen fifty-sixths of one percent a month:

| Survivor's claiming age | Months early | Reduction | Factor |
|---|---|---|---|
| **60** | 84 | **28.500%** | **71.500%** |
| 61 | 72 | 24.429% | 75.571% |
| 62 | 60 | 20.357% | 79.643% |
| 63 | 48 | 16.286% | 83.714% |
| 64 | 36 | 12.214% | 87.786% |
| 65 | 24 | 8.143% | 91.857% |
| 66 | 12 | 4.071% | 95.929% |
| **67** | 0 | 0% | **100.000%** |

Note that the survivor reduction is gentler than the worker's own. A survivor claiming at 62 keeps 79.6 percent; a worker claiming at 62 keeps 70 percent.

#### 5.5 RIB-LIM — the limitation where the deceased claimed early

Where the deceased was entitled to a **reduced** retirement or disability benefit, the survivor benefit is limited. Social Security policy states it directly: a widow or widower's benefit is limited to the larger of 82½ percent of the deceased's death primary insurance amount, or the reduced retirement or disability amount to which the deceased would have been entitled had they lived.[28]

```
survivorCeiling = max( 0.825 × deceasedPIA ,
                       amount the deceased was actually entitled to )
```

**RIB-LIM is a ceiling on the survivor benefit, and the 82.5 percent is a floor inside that ceiling.** Both descriptions are needed and neither alone is accurate.

Absent the limitation, a survivor claiming at their own full retirement age would receive 100 percent of the deceased's primary insurance amount. Where the deceased claimed a reduced benefit, RIB-LIM **caps** the survivor below that figure. The 82.5 percent element then stops the cap from following the deceased's reduction all the way down.

| Deceased claimed at | Deceased's own amount | 82.5% of PIA | **Survivor ceiling** | Which limb governs |
|---|---|---|---|---|
| 62 | $2,100.00 | $2,475.00 | **$2,475.00** | The 82.5 percent floor |
| 64 | $2,400.00 | $2,475.00 | **$2,475.00** | The 82.5 percent floor |
| 67 | $3,000.00 | $2,475.00 | **$3,000.00** | The deceased's own amount |
| 70 | $3,720.00 | $2,475.00 | **$3,720.00** | The deceased's own amount |

On a $3,000 primary insurance amount the survivor of a worker who claimed at 62 is capped at $2,475 rather than $3,000 — the limitation costs $525 a month. Without the 82.5 percent floor the cap would have been $2,100.

A worker who claimed at 62 leaves a survivor $2,475; one who deferred to 70 leaves $3,720. The difference of $1,245 a month persists for the survivor's whole remaining life, and the survivor inherits the delayed credits in full.

#### 5.6 Sequencing: claiming one benefit and switching later

Deemed filing does **not** apply between retirement and survivor benefits. A survivor may claim a reduced survivor benefit at 60 and switch to their own retirement benefit at 70, or claim their own reduced benefit at 62 and switch to an unreduced survivor benefit at survivor full retirement age. The choice depends on which record is larger.

This is the one significant sequencing opportunity that the 2015 legislation left intact, and it is regularly missed.

### 6. Examples and Case Calculations

#### Example 1 — Spousal where one spouse has no earnings record

Worker's primary insurance amount $3,000. Spouse has no record of their own.

| Spouse claims at | Benefit |
|---|---|
| 62 | $975.00 |
| 65 | $1,250.00 |
| 67 | $1,500.00 |
| 70 | $1,500.00 — no gain from waiting |

Deferring past 67 produces nothing, and three years of payments are forfeited for no increase.

#### Example 2 — Dual entitlement

Worker's primary insurance amount $3,000; spouse's own primary insurance amount $1,200. Both claim at 67.

```
Spouse's own benefit                     1,200.00
Spousal benefit, 50% of 3,000            1,500.00
Spouse receives the greater              $1,500.00
```

The household receives $3,000 plus $1,500, not $3,000 plus $1,200 plus $1,500. The spouse's own record adds nothing here, though it would have supported a benefit had the worker's record been smaller.

#### Example 3 — The first death

The same couple. Both benefits are in payment: $3,000 and $1,500, a household total of $4,500.

```
On the first death, whichever spouse dies:
   survivor keeps the higher benefit                     $3,000
   the smaller benefit ends                              −$1,500
   household income falls by                              33.3%
```

Household income falls by a third. Expenses do not fall by a third, as Module 35 sets out, and the survivor moves to the single rate schedule with roughly half the standard deduction at the same moment.

#### Example 4 — Why the higher earner's claiming age matters most

Worker's primary insurance amount $3,000, spouse's $1,200. Compare the worker claiming at 62 with claiming at 70, ignoring cost-of-living adjustments for clarity.

| | Worker claims 62 | Worker claims 70 |
|---|---|---|
| Worker's own benefit | $2,100 | $3,720 |
| Survivor benefit after the worker's death | **$2,475** (RIB-LIM ceiling) | **$3,720** |
| Difference to the survivor | — | **+$1,245 a month** |

If the survivor lives twenty years beyond the worker, the deferral is worth roughly $298,800 in nominal terms to that survivor, before any cost-of-living increases on the larger base.

#### Example 5 — Claiming one benefit then switching

A widow aged 60 whose deceased husband had a $3,000 primary insurance amount and claimed at 67. Her own primary insurance amount is $2,400.

```
Option A  survivor at 60, own at 70
   Age 60–69   survivor  3,000 × 71.5%          = $2,145
   Age 70+     own       2,400 × 124%           = $2,976

Option B  own at 62, survivor at survivor FRA 67
   Age 62–66   own       2,400 × 70%            = $1,680
   Age 67+     survivor  3,000 × 100%           = $3,000
```

Option A pays more in the early years and slightly less after 70. Option B pays less early and more for life. The right answer depends on health, other resources and the relative size of the two records — but the point is that both are available, and a projection that assumes a single benefit for life misses the choice entirely.

### 7. Interactions with Other Rules

**Retirement benefits (Module 11).** The worker's primary insurance amount and claiming age determine both the spousal and survivor amounts. The delayed retirement credit passes to the survivor; it does not pass to a spousal benefit.

**Family maximum (Module 13).** Where a spouse and children draw on one record simultaneously, § 203(a) caps the total. The auxiliary benefits are reduced proportionately; the worker's own is not.

**Filing status (Module 03).** The survivor moves to the single schedule in the year after death unless § 2(a) is satisfied, which requires a dependent son, stepson, daughter or stepdaughter in the household.

**Taxation of benefits (Module 14).** The provisional income thresholds fall from $32,000 and $44,000 to $25,000 and $34,000 on the change to single filing, so a smaller benefit can be taxed more heavily.

**Medicare surcharge (Module 16).** The income-related threshold halves from $218,000 to $109,000.

**Death of a spouse (Module 35).** This module supplies the income side of that event; Module 35 assembles the income, deduction, rate and premium effects together.

### 8. Common Scenarios and Edge Cases

**Benefits never add.** A person receives the higher of their own and any auxiliary benefit. Projections that sum them overstate household income substantially.

**Spousal benefits earn no delayed credits.** Waiting past full retirement age for a spousal benefit is a pure loss.

**A spousal benefit is computed from the worker's primary insurance amount**, not from the worker's reduced benefit. The worker claiming early does not reduce the spouse's entitlement — though it does reduce the survivor benefit through RIB-LIM.

**Survivor full retirement age differs from retirement full retirement age**, by up to four months for those born between 1957 and 1961.

**A survivor can claim from 60**, four years before any other benefit becomes available, and at a gentler reduction than a worker's own early claim.

**Remarriage after 60 does not end a survivor benefit.** Remarriage before 60 does. This is one of the few places where the date of a marriage has a direct benefit consequence.

**A divorced spouse costs the worker nothing.** A worker may have an ex-spouse and a current spouse both drawing on the record, with no reduction to either and no notice to the worker.

**The restricted application is closed.** Only those born on or before 1 January 1954 retain it, and they are all past 70.

**RIB-LIM is a ceiling containing a floor.** It caps the survivor benefit at the larger of 82.5 percent of the deceased's primary insurance amount or the deceased's own entitlement. Where the deceased claimed at or after full retirement age the cap is the deceased's own amount and bites only in the sense that delayed credits pass through; where the deceased claimed early the 82.5 percent limb prevents the cap falling to the deceased's reduced figure. Describing it as only a floor, or only a cap, gets it wrong in one direction or the other.

### 9. Planning Implications

For a married couple, the dominant consideration is the survivor benefit rather than either spouse's own lifetime total. Deferring the **higher** earner's benefit raises the floor under the survivor's income for a period that may exceed twenty years, and it raises it by the full delayed retirement credit. Claiming the **lower** earner's benefit earlier costs little, because that benefit disappears on the first death in any event.

Where one spouse has no significant record, the spousal benefit should be claimed at that spouse's full retirement age and no later.

A widow or widower should be shown both sequencing options in § 5.6. Claiming the smaller benefit first and switching to the larger later is available, is not defeated by deemed filing, and is frequently worth six figures over a long survivorship.

For clients with a non-covered pension — teachers, firefighters, some state and federal employees — the repeal of the Government Pension Offset means spousal and survivor benefits that were previously eliminated are now payable. Any plan built before 2025 on the assumption that they were worthless should be revisited.

### 10. Data Tables for the Engine

| Constant | Value | Indexed |
|---|---|---|
| Spousal maximum | 50% of the worker's PIA | Fixed |
| Spousal reduction, first 36 months | 25/36 of 1% a month | Fixed |
| Spousal reduction, beyond 36 months | 5/12 of 1% a month | Fixed |
| Spousal delayed credits | None | — |
| Spousal at 62, FRA 67 | 32.500% of PIA | — |
| Survivor maximum | 100% of the deceased's entitlement | Fixed |
| Survivor earliest age | 60, or 50 if disabled | Fixed |
| Survivor maximum reduction | 28.5% at age 60 | Fixed |
| Survivor reduction rate, survivor FRA 67 | 19/56 of 1% a month | Fixed |
| Survivor FRA | 66 for 1956 or earlier, rising to 67 for 1962 or later | Fixed |
| RIB-LIM | larger of 82.5% of death PIA, or the deceased's actual entitlement | Fixed |
| Marriage requirement, spousal | 1 year; 10 years if divorced | Fixed |
| Marriage requirement, survivor | 9 months; 10 years if divorced | Fixed |
| Remarriage | Ends a survivor benefit only if before age 60 | Fixed |
| Restricted application | Born on or before 1 January 1954 | Closed |

### 11. References

[26] Social Security Administration, *POMS RS 00615.020, Dual Entitlement Computation Methods*. https://secure.ssa.gov/poms.nsf/lnx/0300615020

[27] Social Security Administration, *POMS RS 00615.301, Reduced Widow(er)'s Benefits*. https://secure.ssa.gov/poms.nsf/lnx/0300615301

[28] Social Security Administration, *POMS RS 00615.320, Reduced WIB — Deceased NH Entitled to Reduced RIB or Reduced DIB*. https://secure.ssa.gov/poms.nsf/lnx/0300615320

[23] Social Security Fairness Act of 2023, P.L. 118-273. https://www.govinfo.gov/content/pkg/PLAW-118publ273/html/PLAW-118publ273.htm

[24] *Cost-of-Living Increase and Other Determinations for 2026*, Federal Register document 2025-19763. https://www.federalregister.gov/documents/2025/11/03/2025-19763/cost-of-living-increase-and-other-determinations-for-2026

### 12. Status in This System

| Layer | Status |
|---|---|
| Projection engine | **Applied in part.** The spousal side is implemented correctly and carefully: the benefit is anchored to the worker's primary insurance amount rather than to the worker's reduced benefit, the reduction uses the distinct 25/36 of 1% rate for the first thirty-six months, delayed retirement credits are correctly **not** applied, and the spouse receives the greater of their own benefit and the spousal amount rather than the sum. The survivor rule that the household keeps the higher of the two benefits and loses the lower is implemented. |
| Backend (`tax-be`) | **Not applied.** No Social Security logic. |
| Known limitations | **The survivor benefit is computed from the bare primary insurance amount.** No claiming adjustment is applied, so a survivor claiming at 60 is shown 100 percent rather than 71.5 percent. Survivor full retirement age is not used, and the RIB-LIM limitation is not applied, so a survivor of a worker who claimed at 62 is shown the full primary insurance amount rather than the RIB-LIM ceiling. Recorded as D3. The supporting constants exist but are dead: `SURV_FRA` holds the correct survivor full retirement age table and `survivorAt60` holds the correct 0.715 factor, and **neither is referenced anywhere in the engine** — the same pattern as the unused depreciation recapture constant recorded at D18. The survivor does not inherit the deceased's delayed retirement credits, and the option to claim one benefit and switch to the other later is not modelled. Deemed filing, the one-year and ten-year marriage requirements, divorced and surviving divorced spouse benefits, and the effect of remarriage are all absent. The family maximum is absent, recorded as D4 and treated in Module 13. |


---

## Module 13 — Children's Benefits and the Family Maximum

**Tax year:** 2026 · **As of:** September 2026 · **Primary authority:** Social Security Act §§ 202(d), 203(a)

---

### 1. Overview and Purpose

A worker's earnings record supports benefits for dependent children as well as for a spouse. A child of a retired or disabled worker receives one half of the worker's primary insurance amount; a child of a deceased worker receives three quarters.[29] A spouse caring for a child under 16 receives a benefit in their own right regardless of their age.

These benefits are then capped. Section 203(a) limits the **total** payable on one earnings record to a figure derived from the worker's primary insurance amount through a four-band formula. Where the sum of the unreduced auxiliary benefits exceeds the room available under that cap, every auxiliary benefit is reduced proportionately. The worker's own benefit is never reduced.

The cap binds hard. On a $3,000 primary insurance amount, a retired worker with a spouse and two children has $4,500 of unreduced auxiliary entitlement and only $2,287.50 of room. Each auxiliary receives $762.50 rather than $1,500. A projection that pays the unreduced amounts overstates that household by **$26,550 a year**.

This module exists because the family maximum was absent from both the research and the engine, and its absence overstates exactly the households — younger workers with dependent children, and survivors with minor children — where the benefit matters most.

### 2. Governing Law and Authorities

| Type | Citation | What it establishes |
|---|---|---|
| Statute | Social Security Act § 202(d)(1) | Entitlement to a child's benefit |
| Statute | Social Security Act § 202(d)(2) | One half of PIA for a living worker; three quarters for a deceased worker |
| Statute | Social Security Act § 202(g) | Mother's and father's benefit for a spouse caring for a young child |
| Statute | Social Security Act § 203(a) | Maximum family benefit |
| Statute | Social Security Act § 215(i) | Annual adjustment of the family maximum bend points |
| Guidance | POMS RS 00203.001 | Entitlement and non-entitlement provisions for a child's benefit |
| Determination | Federal Register 2025-19763 | 2026 family maximum bend points and percentages |

### 3. Key Definitions

| Term | Definition |
|---|---|
| **Child** | A biological child, adopted child, stepchild, or in some cases a grandchild, who is dependent on the worker.[30] |
| **Family maximum** | The ceiling under § 203(a) on total benefits payable on one earnings record. |
| **Auxiliary benefit** | A benefit payable to someone other than the worker on the worker's record — spouse, child, or a spouse caring for a child. |
| **Mother's or father's benefit** | A benefit under § 202(g) for a surviving spouse caring for the worker's child who is under 16 or disabled. Payable at any age. |
| **Combined family maximum** | Where a child is entitled on the records of two workers, the maxima on both records may be combined, subject to a ceiling. |

### 4. Who Is Affected

A child qualifies if they are the child of a worker entitled to retirement or disability benefits, or of a worker who died fully or currently insured, and the child is:[30]

- **unmarried**, including never married; **and**
- **under 18**; or
- **18 or over and a full-time elementary or secondary school student under 19**; or
- **18 or over with a disability that began before age 22**; and
- **dependent** on the worker.

The student extension reaches only elementary and secondary education. College does not qualify, which surprises families who remember the pre-1981 rules under which it did.

A surviving spouse of any age caring for the worker's child under 16, or a disabled child, is entitled to a mother's or father's benefit under § 202(g). This is the one route to a benefit before age 60 for a survivor.

### 5. Core Rules and Calculations

#### 5.1 Case Register

| # | Case | Applied |
|---|---|---|
| 1 | Child of a living worker at 50 percent of PIA | **No** — D5 |
| 2 | Surviving child at 75 percent of PIA | **No** — D5 |
| 3 | Entitlement under 18 | **No** |
| 4 | Extension to 19 for a full-time secondary student | **No** |
| 5 | Disability beginning before age 22 | **No** |
| 6 | Unmarried requirement | **No** |
| 7 | Dependency requirement | **No** |
| 8 | § 202(g) mother's or father's benefit | **No** |
| 9 | § 203(a) family maximum formula | **No** — D4 |
| 10 | Worker's own benefit not reduced by the cap | **No** — follows from case 9 |
| 11 | Proportional reduction of auxiliary benefits | **No** |
| 12 | A divorced spouse's benefit excluded from the cap | **No** |
| 13 | Combined family maximum across two records | **No** |
| 14 | Family maximum bend points indexed annually | **No** |
| 15 | Benefits ending as each child ages out | **No** |

Nothing in this module is implemented. The projection models a worker and a spouse only.

#### 5.2 The child's benefit amount

Section 202(d)(2) sets the amount directly:[29]

| Situation | Child's benefit |
|---|---|
| Worker is alive and entitled to retirement or disability benefits | **One half** of the worker's primary insurance amount |
| Worker has died | **Three quarters** of the worker's primary insurance amount |

Each eligible child has a separate entitlement. Three children of a living worker have three benefits of 50 percent each, subject to the cap in § 5.3.

#### 5.3 The family maximum — § 203(a)

For a worker who becomes 62, or dies before 62, in 2026, total benefits payable on the record may not exceed:[31]

```
familyMaximum = 1.50 × the first $1,643 of PIA
              + 2.72 × PIA between $1,643 and $2,371
              + 1.34 × PIA between $2,371 and $3,093
              + 1.75 × PIA above $3,093
```

rounded down to the next lower ten cents. The bend points are adjusted annually by the same wage-indexing mechanism that adjusts the primary insurance amount bend points, and they are **different** figures from those in Module 11.

| Worker's PIA | Family maximum | As a share of PIA | Room for auxiliaries |
|---|---|---|---|
| $1,500 | $2,250.00 | 150.0% | $750.00 |
| $2,000 | $3,435.50 | 171.8% | $1,435.50 |
| $2,500 | $4,617.50 | **184.7%** | $2,117.50 |
| $3,000 | $5,287.50 | 176.2% | $2,287.50 |
| $3,500 | $6,124.30 | 175.0% | $2,624.30 |
| $4,000 | $6,999.30 | 175.0% | $2,999.30 |

The share is not monotonic. It rises to about 185 percent for a middle-earning worker and then settles at 175 percent for higher earners. The 272 percent band is what produces the hump, and it means the cap is proportionally most generous to a worker whose primary insurance amount sits near $2,400.

#### 5.4 How the reduction is applied

The worker's own benefit is paid in full and is **not** reduced by the cap. The room remaining is divided among the auxiliaries in proportion to their unreduced entitlements:

```
roomForAuxiliaries = familyMaximum − workerOwnBenefit
reductionFactor    = roomForAuxiliaries ÷ Σ(unreduced auxiliary benefits)
eachAuxiliary      = unreducedEntitlement × reductionFactor
```

Where the worker has died there is no worker benefit to subtract, so the whole family maximum is available to the survivors.

A **divorced spouse's** benefit is excluded from the computation entirely. It does not count against the family maximum and is not reduced by it, which is why a worker can support an ex-spouse, a current spouse and children without the ex-spouse affecting anyone else's amount.

#### 5.5 The mother's and father's benefit

Section 202(g) provides a benefit to a surviving spouse of any age who is caring for the deceased worker's child under 16 or disabled. The amount is three quarters of the worker's primary insurance amount, the same as a surviving child's.

It ends when the youngest child reaches 16, which creates the gap commonly called the blackout period: benefits stop at that point and do not resume until the survivor reaches 60. For a survivor widowed at 40 with a young child, the gap can be two decades long, and it is the principal reason life insurance is recommended for households with young children.

### 6. Examples and Case Calculations

#### Example 1 — Retired worker with a spouse and two children

Worker's primary insurance amount $3,000, claiming at full retirement age. Spouse and two children under 18 all entitled.

```
Family maximum                                   $5,287.50
Worker's own benefit, not reduced                 3,000.00
                                                  --------
Room available to auxiliaries                     2,287.50

Unreduced auxiliary entitlement
   Spouse   50% of 3,000                          1,500.00
   Child 1  50% of 3,000                          1,500.00
   Child 2  50% of 3,000                          1,500.00
                                                  --------
                                                  4,500.00

Reduction factor   2,287.50 ÷ 4,500 = 0.5083
Each auxiliary receives                            $762.50
Household total                                  $5,287.50
```

Without the cap the household would show $7,500 a month. The overstatement is **$2,212.50 a month, or $26,550 a year**, and it persists for as long as the children are entitled.

#### Example 2 — The same record after the worker's death

Worker has died. Two surviving children and a surviving spouse caring for them.

```
Unreduced entitlement
   Spouse, § 202(g)   75% of 3,000                2,250.00
   Child 1            75% of 3,000                2,250.00
   Child 2            75% of 3,000                2,250.00
                                                  --------
                                                  6,750.00

Family maximum                                    5,287.50
Reduction factor   5,287.50 ÷ 6,750 = 0.7833
Each receives                                    $1,762.50
Household total                                  $5,287.50
```

There is no worker benefit to subtract, so the whole cap is available. Each survivor receives more than each auxiliary did while the worker lived, both because the rate is 75 rather than 50 percent and because the worker's own benefit no longer consumes part of the cap.

#### Example 3 — Benefits ending as children age out

Continuing Example 2, as each child ages out the reduction factor rises for those remaining.

| Entitled | Unreduced total | Factor | Each receives |
|---|---|---|---|
| Spouse + 2 children | $6,750.00 | 0.7833 | $1,762.50 |
| Spouse + 1 child | $4,500.00 | 1.0000 | $2,250.00 — cap no longer binds |
| Spouse alone, youngest child turns 16 | — | — | **$0** — the § 202(g) benefit ends |

The last row is the blackout. The surviving spouse's own benefit does not become available until 60.

### 7. Interactions with Other Rules

**Retirement benefits (Module 11).** The worker's primary insurance amount drives both the child's benefit and the family maximum, but through two different sets of bend points.

**Spousal and survivor benefits (Module 12).** A spouse's benefit competes with children's benefits for room under the same cap. Where children are entitled, the spousal benefit is reduced along with theirs.

**Taxation of benefits (Module 14).** A child's benefit is income of the **child**, not of the parent, and is reported on the child's return if a return is required. In most cases the child has no other income and the benefit is untaxed. It is not added to the parent's provisional income.

**Kiddie tax.** Because a child's benefit is the child's own income, unusually large benefits combined with investment income can engage § 1(g). The projection does not model this, as Module 01 records.

**Death of a spouse (Module 35).** Where minor children survive, the household's Social Security income can *rise* on the worker's death rather than fall, because the rate moves from 50 to 75 percent and the worker's own benefit stops consuming the cap. This is the opposite of the pattern for an older couple and is worth modelling separately.

**Filing status (Module 03).** A surviving spouse with a dependent child is one of the few households that actually satisfies § 2(a), and so retains joint rates for two years after the year of death.

### 8. Common Scenarios and Edge Cases

**The cap is on the record, not on the household.** Where children are entitled on two parents' records, a combined family maximum may apply and can exceed either record's own cap.

**A divorced spouse is invisible to the cap.** Their benefit neither counts against it nor is reduced by it.

**The worker's own benefit is never reduced.** Only auxiliaries absorb the cap.

**The student extension stops at secondary school.** A child at university is not entitled beyond 19, or beyond the end of secondary schooling if earlier.

**A disability must have begun before 22** for an adult child to be entitled. A disability arising at 25 does not qualify the adult child on a parent's record.

**The blackout period is real and long.** Benefits for a surviving spouse end when the youngest child turns 16 and do not resume until 60.

**The family maximum share of PIA is not constant.** It peaks near 185 percent for a middle earner and falls to 175 percent for higher earners, so scaling it as a fixed multiple is wrong.

**A child's benefit is the child's income for tax purposes**, not the parent's.

### 9. Planning Implications

For a household with young children, the family maximum is the binding constraint on what Social Security will actually pay, and it is materially lower than the sum of the individual entitlements. Any projection or insurance-needs analysis built on unreduced amounts overstates the safety net and understates the insurance gap.

The blackout period between the youngest child reaching 16 and the surviving spouse reaching 60 is the largest uncovered interval in the system. Term life insurance sized to that gap is the conventional response, and quantifying the gap requires the family maximum rather than the headline benefit.

For an older couple with no dependent children — the population this system mostly serves — none of this module applies, and the family maximum never binds because a worker and one spouse cannot together exceed it. That is why the omission has gone unnoticed. It becomes material the moment a client has minor children, a disabled adult child, or a grandchild in their care.

### 10. Data Tables for the Engine

| Constant | 2026 value | Indexed |
|---|---|---|
| Child of a living worker | 50% of PIA | Fixed |
| Surviving child | 75% of PIA | Fixed |
| Mother's or father's benefit | 75% of PIA | Fixed |
| Family maximum bend point 1 | $1,643 | Yes — wage index |
| Family maximum bend point 2 | $2,371 | Yes |
| Family maximum bend point 3 | $3,093 | Yes |
| Family maximum percentages | 150 / 272 / 134 / 175 | Fixed |
| Family maximum rounding | Down to the next lower $0.10 | Fixed |
| Child age limit | Under 18 | Fixed |
| Student extension | Under 19, elementary or secondary only | Fixed |
| Disabled adult child | Disability began before 22 | Fixed |
| § 202(g) benefit ends | Youngest child reaches 16 | Fixed |
| Divorced spouse | Excluded from the family maximum | Fixed |
| Worker's own benefit | Never reduced by the cap | Fixed |

### 11. References

[29] 42 U.S.C. § 402(d)(2), Social Security Act § 202(d)(2). United States Code, Office of the Law Revision Counsel. https://www.govinfo.gov/app/collection/uscode

[30] Social Security Administration, *POMS RS 00203.001, Entitlement and Non-Entitlement Provisions for Child's Benefits*. https://secure.ssa.gov/poms.nsf/lnx/0300203001

[31] *Cost-of-Living Increase and Other Determinations for 2026*, Federal Register document 2025-19763, family maximum formula. https://www.federalregister.gov/documents/2025/11/03/2025-19763/cost-of-living-increase-and-other-determinations-for-2026

### 12. Status in This System

| Layer | Status |
|---|---|
| Projection engine | **Not applied.** Neither children's benefits nor the family maximum exists in the engine. There is no constant, no function and no input for a dependent child. The projection models a worker and a spouse. |
| Backend (`tax-be`) | **Not applied.** No Social Security logic. |
| Known limitations | Recorded as D4 and D5. The absence has two effects that run in opposite directions. Where a client has dependent children, the projection **omits** children's benefits entirely and understates household income. Where a client has both a spouse and children drawing on one record, applying the individual entitlements without the § 203(a) cap would **overstate** household income substantially — by $26,550 a year on the $3,000 primary insurance amount worked in Example 1. Because the engine models a worker and a spouse only, a two-person household can never breach the cap, which is why the omission is invisible for the retiree population and becomes material as soon as a minor child, a disabled adult child, or a caregiving survivor is present. The § 202(g) mother's and father's benefit and the blackout period between a youngest child reaching 16 and a survivor reaching 60 are likewise absent, and that gap is the single largest uncovered interval in the benefit system. |


---

## Module 14 — Taxation of Social Security Benefits

**Tax year:** 2026 · **As of:** September 2026 · **Primary authority:** IRC § 86

---

### 1. Overview and Purpose

Social Security benefits were untaxed until 1984. Section 86 now includes part of a benefit in gross income where the recipient's other income exceeds a threshold — up to half the benefit above the first threshold, and up to 85 percent above the second.

The provision has two features that make it disproportionately important in a long projection. The thresholds are written into the statute as fixed dollar amounts and have **never been indexed**. The $25,000 and $32,000 base amounts date from 1983 and the $34,000 and $44,000 adjusted base amounts from 1993, and neither has moved since. Every year of inflation therefore brings more beneficiaries above them without anyone gaining in real terms.

The second feature is the shape of the calculation. Because each additional dollar of ordinary income can make 85 cents of benefit taxable, the effective marginal rate over a wide band is 1.85 times the statutory rate. A retiree nominally in the 12 percent bracket faces 22.2 percent on income in that band. This is commonly called the tax torpedo, and it is the reason the years before benefits begin are so valuable for recognising income.

### 2. Governing Law and Authorities

| Type | Citation | What it establishes |
|---|---|---|
| Statute | IRC § 86(a)(1) | The 50 percent tier |
| Statute | IRC § 86(a)(2) | The 85 percent tier |
| Statute | IRC § 86(b)(1) | Provisional income |
| Statute | IRC § 86(b)(2) | Modified adjusted gross income, including tax-exempt interest |
| Statute | IRC § 86(c) | Base amount and adjusted base amount |
| Legislation | P.L. 98-21, Social Security Amendments of 1983 | Introduced taxation at 50 percent |
| Legislation | P.L. 103-66, OBRA 1993 | Added the 85 percent tier |

### 3. Key Definitions

| Term | Definition |
|---|---|
| **Provisional income** | Modified adjusted gross income plus one half of the Social Security benefits received. The statute does not use the phrase; it is the sum described in § 86(b)(1)(A). |
| **Modified adjusted gross income** | Adjusted gross income determined without regard to § 86 and several exclusions, **increased by tax-exempt interest**.[32] |
| **Base amount** | $25,000, or $32,000 on a joint return, or **zero** for a married taxpayer filing separately who did not live apart from their spouse for the whole year. |
| **Adjusted base amount** | $34,000, or $44,000 on a joint return, or zero in the same separate-return case. |

### 4. Who Is Affected

Any recipient of Social Security retirement, survivor or disability benefits whose provisional income exceeds the base amount for their filing status. Supplemental Security Income is not a Social Security benefit and is never taxable.

A married taxpayer filing separately who lived with their spouse at any time during the year has base amounts of **zero**, so benefits are taxable from the first dollar of other income. A separate filer who lived apart for the entire year uses the $25,000 and $34,000 amounts.

### 5. Core Rules and Calculations

#### 5.1 Case Register

| # | Case | Applied |
|---|---|---|
| 1 | Provisional income = MAGI + half the benefit | Yes |
| 2 | Tax-exempt interest added back | Yes |
| 3 | 50 percent tier between the base and adjusted base amounts | Yes |
| 4 | 85 percent tier above the adjusted base amount | Yes |
| 5 | The lesser-of ceiling in each tier | Yes |
| 6 | The carried amount, half the difference between the two thresholds | Yes — derived, not hard-coded |
| 7 | Thresholds by filing status | Yes |
| 8 | Thresholds not indexed | Yes |
| 9 | Zero thresholds for a separate filer living with a spouse | Yes |
| 10 | $25,000 and $34,000 for a separate filer living apart all year | **No** |
| 11 | Benefits never more than 85 percent taxable | Yes |
| 12 | A child's benefit is the child's income | **No** — children's benefits are not modelled |
| 13 | Lump-sum election under § 86(e) for a retroactive award | **No** |
| 14 | Repayment of benefits in a later year | **No** |

#### 5.2 The computation

```
provisionalIncome = MAGI + taxExemptInterest + 0.5 × benefits

if provisionalIncome ≤ baseAmount
    taxable = 0

else if provisionalIncome ≤ adjustedBaseAmount
    taxable = min( 0.5 × (provisionalIncome − baseAmount),
                   0.5 × benefits )

else
    taxable = min( 0.85 × (provisionalIncome − adjustedBaseAmount)
                   + min( 0.5 × (adjustedBase − base), 0.5 × benefits ),
                   0.85 × benefits )
```

The carried amount in the third branch is one half of the difference between the two thresholds — $4,500 for a single filer and $6,000 on a joint return. Both figures follow from the thresholds rather than existing independently, and deriving them rather than hard-coding them keeps the two consistent.

#### 5.3 Thresholds

| Filing status | Base amount | Adjusted base amount | Indexed |
|---|---|---|---|
| Single, head of household, surviving spouse | $25,000 | $34,000 | **No — set in 1983 and 1993** |
| Married filing jointly | $32,000 | $44,000 | **No** |
| Married filing separately, living with spouse | **$0** | **$0** | **No** |
| Married filing separately, living apart all year | $25,000 | $34,000 | **No** |

#### 5.4 How the taxable share rises

A married couple with a $40,000 benefit:

| Other income | Provisional income | Taxable benefit | Share of benefit |
|---|---|---|---|
| $0 | $20,000 | $0 | 0% |
| $10,000 | $30,000 | $0 | 0% |
| $20,000 | $40,000 | $4,000 | 10.0% |
| $25,000 | $45,000 | $6,850 | 17.1% |
| $30,000 | $50,000 | $11,100 | 27.8% |
| $40,000 | $60,000 | $19,600 | 49.0% |
| $60,000 | $80,000 | $34,000 | **85.0% — ceiling reached** |
| $80,000 | $100,000 | $34,000 | 85.0% |

The ceiling of 85 percent is absolute. Once reached, additional income no longer increases the taxable benefit, and the effective marginal rate falls back to the statutory rate.

#### 5.5 The tax torpedo

Between the thresholds and the point at which 85 percent is reached, each additional dollar of ordinary income makes up to 85 cents of benefit taxable. The taxpayer therefore adds $1.85 of taxable income for each $1.00 earned.

| Other income | Extra taxable benefit per $1,000 | Total extra taxable income | Effective rate at a 12% bracket |
|---|---|---|---|
| $20,000 | $500 | $1,500 | 18.0% |
| $24,000 | $850 | $1,850 | **22.2%** |
| $30,000 | $850 | $1,850 | **22.2%** |
| $36,000 | $850 | $1,850 | **22.2%** |
| $50,000 | $850 | $1,850 | **22.2%** |
| $70,000 | $0 | $1,000 | 12.0% — ceiling passed |

A retiree who believes they are in the 12 percent bracket is paying 22.2 percent at the margin across a band that can be $50,000 wide. In the 22 percent bracket the same mechanism produces 40.7 percent.

The band ends. Above the point where 85 percent of the benefit is already taxable, the rate returns to the statutory figure — so the marginal rate is **not** monotonic in income, and a large deliberate recognition of income can be cheaper per dollar than a small one.

### 6. Examples and Case Calculations

#### Example 1 — Below the threshold

Married couple, benefit $40,000, other income $10,000.

```
Provisional income   10,000 + 20,000 = 30,000
Base amount                            32,000
Taxable benefit                            $0
```

The couple's whole income is $50,000 and none of the benefit is taxed.

#### Example 2 — Between the thresholds

Same couple, other income $20,000.

```
Provisional income   20,000 + 20,000 = 40,000
Excess over 32,000                     8,000
Tier 1  min(0.5 × 8,000, 0.5 × 40,000) = $4,000
```

#### Example 3 — Above the adjusted base amount

Same couple, other income $40,000.

```
Provisional income   40,000 + 20,000 = 60,000
Excess over 44,000                    16,000
   0.85 × 16,000                      13,600
   plus min(0.5 × 12,000, 0.5 × 40,000)  6,000
                                      ------
                                      19,600
Ceiling  0.85 × 40,000                34,000
Taxable                              $19,600
```

#### Example 4 — A required minimum distribution triggering the torpedo

The couple in Example 2 reaches the required beginning date and must take $30,000.

```
Before   other income 20,000   taxable benefit  $4,000
After    other income 50,000   taxable benefit $25,600

Additional taxable income
   the distribution itself                     30,000
   additional benefit brought into tax         21,600
                                               ------
                                               51,600
```

A $30,000 distribution produced $51,600 of additional taxable income. This is the compounding effect described in Module 09, and it is the single strongest argument for reducing pre-tax balances before the required beginning date.

#### Example 5 — The widow effect

A couple with a $30,000 benefit and $35,000 of other income. One spouse dies; income and benefit are held constant for comparison.

```
As a married couple   provisional 50,000   taxable benefit $11,100   37.0% of benefit
As a single filer     provisional 50,000   taxable benefit $18,100   60.3% of benefit
Increase in taxable income                                   $7,000
```

The thresholds fall by $7,000 and $10,000 on the change of status, so the same income produces $7,000 more taxable income. In reality the survivor's benefit also falls, because the smaller of the two benefits ends — so income drops while the taxable share rises. Module 35 assembles the whole effect.

### 7. Interactions with Other Rules

**Required minimum distributions (Module 09).** A distribution is ordinary income and enters provisional income in full. Example 4 shows the multiplier.

**Roth conversions (Module 10).** A conversion likewise enters provisional income. Converting **before** benefits begin avoids the interaction entirely, which is a strong argument for the window between retirement and claiming.

**Qualified charitable distributions (Module 09).** Because the amount never enters gross income, a qualified charitable distribution does not raise provisional income. An itemised charitable deduction, taken below the line, does nothing for § 86. This is the clearest case where the two routes differ in substance.

**Tax-exempt interest.** Municipal bond interest is added back by § 86(b)(2)(B). It is exempt from the income tax and **not** exempt for this purpose, so a portfolio shifted into municipals to reduce taxable income does not reduce the taxable share of the benefit.

**Capital gains (Module 24).** A realised gain raises provisional income even where it is taxed at zero percent. A retiree harvesting gains in the zero-rate bracket can find the harvest costs 8.5 cents of benefit taxation per dollar despite a nominal zero rate.

**Filing status (Module 03).** The thresholds fall by roughly a third on a change from joint to single.

**Medicare surcharge (Module 16).** Both respond to income, but on different measures and different timing. A single income event can raise the taxable benefit now and the premium two years later.

### 8. Common Scenarios and Edge Cases

**The thresholds have never been indexed.** They were set in 1983 and 1993. This is deliberate policy, not oversight — the design gradually extends taxation to more beneficiaries — and it means a projection must compute in nominal dollars. Deflating before applying § 86 understates the taxable share in every later year, and the error grows across the horizon.

**Tax-exempt interest is not exempt here.** Municipal income counts in full toward provisional income.

**A zero-rate capital gain still raises provisional income.** The rate on the gain and the effect on the benefit are separate questions.

**Married filing separately while living together is punitive.** The thresholds are zero, so benefits are taxed from the first dollar. Living apart for the entire year restores the single-filer amounts.

**The maximum is 85 percent, not 100.** At least 15 percent of a benefit is never taxable.

**The marginal rate is not monotonic.** It rises through the torpedo band and falls back once 85 percent is reached, so recognising a large amount of income in one year can carry a lower average cost than spreading it.

**A lump-sum retroactive award may be elected into the earlier years** under § 86(e), which usually produces a lower total than taxing it all in the year received.

**A child's benefit is the child's income**, not the parent's, and does not enter the parent's provisional income.

### 9. Planning Implications

The years between retirement and the start of benefits are doubly valuable. Provisional income is low because there is no benefit to add half of, and any income recognised then is taxed at the statutory rate rather than the torpedo rate. Modules 09 and 10 identify the same window for conversions, and the reason is the same.

Once benefits are in payment, the objective is usually to be either **below** the base amount or **beyond** the point at which 85 percent is already taxable. The expensive place is in between. For a client already past the 85 percent ceiling, additional income costs only the statutory rate, which makes further conversions cheaper than they appear.

Qualified charitable distributions are the only mechanism that reduces provisional income without reducing spendable cash, because they replace an included distribution rather than adding a deduction.

Shifting a portfolio into municipal bonds does not help. The interest is added back in full.

Because the thresholds are frozen, a projection should show the taxable share of benefits rising steadily across the horizon even where the client's real income is flat. A model that indexes the thresholds will understate tax in every later year and will understate it by more each year.

### 10. Data Tables for the Engine

| Constant | Value | Indexed |
|---|---|---|
| Base amount, single and head of household | $25,000 | **No — since 1984** |
| Base amount, joint | $32,000 | **No** |
| Base amount, separate filer living with spouse | $0 | **No** |
| Adjusted base amount, single and head of household | $34,000 | **No — since 1994** |
| Adjusted base amount, joint | $44,000 | **No** |
| First tier inclusion rate | 50% | Fixed |
| Second tier inclusion rate | 85% | Fixed |
| Maximum taxable share | 85% | Fixed |
| Carried amount | half the difference between the thresholds: $4,500 single, $6,000 joint | Derived |
| Tax-exempt interest | Added back to provisional income | — |

### 11. References

[32] 26 U.S.C. § 86, *Social security and tier 1 railroad retirement benefits*. United States Code, Office of the Law Revision Counsel. https://www.govinfo.gov/app/collection/uscode

[33] Internal Revenue Service, *Publication 915, Social Security and Equivalent Railroad Retirement Benefits*. https://www.irs.gov/pub/irs-pdf/p915.pdf

### 12. Status in This System

| Layer | Status |
|---|---|
| Projection engine | **Applied, and correctly.** The provisional income computation adds back tax-exempt interest as § 86(b)(2)(B) requires. Both tiers are implemented with the statutory lesser-of ceilings, and the carried amount in the second tier is **derived** as one half of the difference between the two thresholds rather than hard-coded, so the $4,500 and $6,000 figures cannot drift out of step with the thresholds. All four threshold pairs match the statute, including the zero amounts for a separate filer. The thresholds are correctly held constant rather than inflated, which matters more here than almost anywhere else in the system: indexing them would understate tax in every later year and by an increasing amount. |
| Backend (`tax-be`) | **Not applied.** No Social Security logic. |
| Known limitations | The separate-filer case is treated as though the taxpayer always lived with their spouse, so the $25,000 and $34,000 amounts available to a separate filer who lived apart for the whole year are not offered. The § 86(e) lump-sum election for a retroactive award is not modelled, nor is the treatment of benefits repaid in a later year. Because children's benefits are not modelled at all, as Module 13 records, the rule that a child's benefit is the child's own income never arises. |


---

## Module 15 — Medicare Part A, Part B and Part D Premiums

**Tax year:** 2026 · **As of:** September 2026 · **Primary authority:** Social Security Act §§ 1811–1860D

---

### 1. Overview and Purpose

Medicare is not free, and the amounts are large enough over a thirty-year retirement to matter as much as many tax provisions. Part A, covering inpatient hospital care, is premium-free for anyone with forty quarters of coverage but carries a substantial deductible for each benefit period. Part B, covering physician and outpatient services, carries a monthly premium deducted from the Social Security benefit. Part D covers prescription drugs through private plans.

Two features distinguish Medicare cost from ordinary expenditure in a projection. The premiums are deducted directly from the Social Security benefit, so the net benefit a household actually receives is lower than the gross benefit used in the tax computation of Module 14. And the premiums are **income-related** — the surcharge treated in Module 16 can more than triple the Part B premium for a high-income household.

Medicare cost also inflates faster than general prices. The Part B standard premium rose from $185.00 in 2025 to $202.90 in 2026, an increase of 9.7 percent against a Social Security cost-of-living adjustment of 2.8 percent. A projection that inflates healthcare at the general rate understates it materially over a long horizon.

### 2. Governing Law and Authorities

| Type | Citation | What it establishes |
|---|---|---|
| Statute | Social Security Act § 1813 | Part A deductibles and coinsurance |
| Statute | Social Security Act § 1818 | Part A premium for those without sufficient quarters |
| Statute | Social Security Act § 1839 | Part B premium determination |
| Statute | Social Security Act § 1839(f) | The hold-harmless provision |
| Statute | Social Security Act § 1860D-13 | Part D premiums |
| Statute | IRC § 213(d) | Medicare premiums as deductible medical expenses |
| Determination | CMS 2026 Medicare Parts A and B Premiums and Deductibles | All 2026 amounts |

### 3. Key Definitions

| Term | Definition |
|---|---|
| **Benefit period** | For Part A, a period beginning on admission and ending after 60 consecutive days out of a hospital or skilled nursing facility. A beneficiary can have several in one year, each with its own deductible. |
| **Lifetime reserve days** | Sixty additional inpatient days available once in a lifetime, at a higher coinsurance rate. |
| **Hold harmless** | The § 1839(f) provision limiting the Part B premium increase for most beneficiaries to the dollar amount of the Social Security cost-of-living increase. |
| **Late enrolment penalty** | A permanent premium increase for enrolling after first eligibility without creditable coverage. |

### 4. Who Is Affected

Individuals aged 65 or over, and those under 65 who have received Social Security disability benefits for 24 months or who have end-stage renal disease or amyotrophic lateral sclerosis.

Part A is premium-free with forty quarters of coverage. Those with fewer pay a premium — $311 a month with 30 to 39 quarters, and **$565** a month with fewer than 30.

Part B and Part D are voluntary, but declining them without creditable coverage from an employer produces a permanent late enrolment penalty.

### 5. Core Rules and Calculations

#### 5.1 Case Register

| # | Case | Applied |
|---|---|---|
| 1 | Part B standard premium | Yes |
| 2 | Part B annual deductible | Yes, as a constant |
| 3 | Premium counted as a deductible medical expense | Yes |
| 4 | Premium deducted from the Social Security benefit | **No** — gross benefit and premium are tracked separately |
| 5 | Part A premium-free with 40 quarters | Assumed |
| 6 | Part A premium for insufficient quarters | **No** |
| 7 | Part A inpatient deductible per benefit period | **No** |
| 8 | Part A coinsurance days 61–90 and lifetime reserve | **No** |
| 9 | Skilled nursing facility coinsurance days 21–100 | **No** |
| 10 | Part D base premium | Partially — via the surcharge table only |
| 11 | Income-related surcharge | Yes — Module 16 |
| 12 | § 1839(f) hold harmless | **No** |
| 13 | Late enrolment penalties | **No** |
| 14 | Medicare Advantage and supplement premiums | **No** — treated as general healthcare cost |
| 15 | Coverage before 65 through disability | **No** — see Module 37 |
| 16 | Healthcare inflation above general inflation | Yes |

#### 5.2 Part A — 2026 amounts

Part A is premium-free for a beneficiary with forty quarters of coverage, but it is not cost-free.[34]

| Item | 2026 amount |
|---|---|
| Inpatient hospital deductible, per benefit period | **$1,736** |
| Coinsurance, days 61–90 | **$434** a day |
| Coinsurance, lifetime reserve days | **$868** a day |
| Skilled nursing facility coinsurance, days 21–100 | **$217.00** a day |
| Monthly premium, 30–39 quarters of coverage | $311 |
| Monthly premium, fewer than 30 quarters | $565 |

The deductible is **per benefit period**, not per year. A beneficiary admitted in February, discharged, and admitted again in November pays it twice.

The skilled nursing facility benefit is the one most often misunderstood. Days 1 to 20 are fully covered; days 21 to 100 carry $217 a day, which is $17,360 over the eighty days; and after day 100 Medicare pays nothing. Medicare is not long-term care insurance, and the point at which it stops is early. Module 33 treats what happens next.

#### 5.3 Part B — 2026 amounts

| Item | 2026 amount | Change from 2025 |
|---|---|---|
| Standard monthly premium | **$202.90** | up $17.90 from $185.00 |
| Annual deductible | **$283** | up $26 from $257 |

The standard premium is set to cover roughly 25 percent of expected Part B costs for beneficiaries under 65 and for the aged, with general revenue covering the rest. The increase of 9.7 percent for 2026 substantially exceeds the 2.8 percent Social Security cost-of-living adjustment.

The premium is **deducted from the Social Security benefit** where one is in payment. A couple both paying the standard premium give up $4,869.60 of gross benefit in 2026 before any income-related surcharge.

#### 5.4 The hold-harmless provision

Section 1839(f) limits the increase in the Part B premium for most beneficiaries to the dollar amount of their Social Security cost-of-living increase, so that the net benefit cannot fall. It applies only where the premium is deducted from the benefit.

Three groups are excluded: beneficiaries paying an income-related surcharge, those newly enrolled in the year, and those not receiving Social Security benefits. A high-income retiree who has deferred claiming to 70 is outside the protection on two counts at once.

#### 5.5 Part D

Part D is delivered through private plans, so there is no single premium. The national base beneficiary premium is used to compute the income-related surcharge in Module 16 and the late enrolment penalty, but the amount a beneficiary actually pays depends on the plan chosen.

The late enrolment penalty is one percent of the national base beneficiary premium for each full month without creditable coverage after the initial enrolment period, and it is **permanent**.

### 6. Examples and Case Calculations

#### Example 1 — A couple's baseline Medicare cost

Both spouses aged 68, incomes below the surcharge threshold, each in a Part D plan costing $45 a month.

```
Part B   202.90 × 12 × 2                      =  $4,869.60
Part D    45.00 × 12 × 2                      =  $1,080.00
Part B deductible, 283 × 2                    =    $566.00
                                                 ---------
Baseline annual Medicare cost                    $6,515.60
```

This is before any supplement or Advantage premium, before any surcharge, and before any Part A cost.

#### Example 2 — A hospital stay

A beneficiary admitted for 12 days, discharged, and readmitted 90 days later for 8 days.

```
First benefit period    deductible                $1,736
Second benefit period   deductible                $1,736
                                                  ------
Part A cost                                       $3,472
```

Two deductibles in one year, because the second admission began more than 60 days after the first benefit period ended.

#### Example 3 — Skilled nursing after a hospital stay

A beneficiary spends 100 days in a skilled nursing facility following a qualifying hospital stay.

```
Days 1–20     fully covered                            $0
Days 21–100   80 days × $217                      $17,360
Day 101 on    Medicare pays nothing
```

The daily cost after day 100 falls entirely on the beneficiary. At a typical private-room rate this is the point at which a care event begins consuming capital rather than income.

#### Example 4 — Healthcare inflation against general inflation

Projecting the Part B premium forward twenty years at the general 2.8 percent rate against a healthcare rate of 5 percent:

```
At 2.8%   202.90 × 1.028^20 = $352.61 a month
At 5.0%   202.90 × 1.050^20 = $538.35 a month
```

The difference for a couple is $4,457 a year by year twenty. This is why Module 33 and the expense modelling track healthcare separately.

### 7. Interactions with Other Rules

**Income-related surcharge (Module 16).** The amounts here are the base to which the surcharge is added.

**Social Security benefits (Modules 11 and 14).** Premiums are deducted from the gross benefit. The **gross** amount is what enters the § 86 computation, so a beneficiary is taxed on money they never receive. Both figures must be tracked.

**Medical expense deduction (Module 32).** Medicare premiums, deductibles and coinsurance are all qualified medical expenses under § 213(d). In a year with substantial care costs they contribute to an itemised deduction above the 7.5 percent floor.

**Health savings accounts (Module 34).** Contributions must stop when Medicare enrolment begins, but accumulated balances may be used tax free for Medicare premiums other than a supplement.

**Long-term care (Module 33).** Medicare's skilled nursing benefit ends at day 100. Everything beyond it is either private payment, long-term care insurance, or Medicaid.

**Disability (Module 37).** Medicare begins 24 months after entitlement to disability benefits, before age 65.

### 8. Common Scenarios and Edge Cases

**The Part A deductible is per benefit period.** A beneficiary with several separated admissions pays it several times in one year.

**Medicare does not cover long-term care.** The skilled nursing benefit requires a qualifying hospital stay, is limited to 100 days, and requires skilled care rather than custodial care. Custodial care is not covered at any point.

**The hold-harmless provision does not protect high earners.** Anyone paying an income-related surcharge is outside it, as is anyone who has deferred claiming Social Security and so has no benefit from which the premium is deducted.

**Deferring Social Security means paying the premium directly.** A beneficiary enrolled in Part B but not yet claiming Social Security is billed quarterly and receives no hold-harmless protection.

**Late enrolment penalties are permanent.** For Part B the penalty is 10 percent of the standard premium for each full 12-month period without coverage; for Part D it is one percent of the base beneficiary premium a month. Both last for as long as the beneficiary has the coverage.

**Employer coverage past 65 can defer enrolment without penalty**, but only where the employer has 20 or more employees. With a smaller employer, Medicare becomes primary at 65 and failing to enrol leaves the beneficiary largely uninsured.

**Premiums are deducted from the benefit but taxed as though received.** The § 86 computation uses the gross benefit.

### 9. Planning Implications

Medicare cost should be modelled as a distinct line inflating faster than general prices, not folded into a single expense figure. The 2026 increase of 9.7 percent against a 2.8 percent cost-of-living adjustment is the ordinary pattern rather than an anomaly.

The gap between what Medicare covers and what a care event costs is the largest uninsured exposure in most retirement plans. The 100-day limit on skilled nursing, and the exclusion of custodial care entirely, define that gap.

Because premiums are deducted from the gross benefit while tax is computed on the gross amount, the net cash a household receives from Social Security is materially below the figure that appears in the tax calculation. A projection should report both.

For a client deferring Social Security to 70 while enrolled in Part B, the premium must be paid from other funds and the hold-harmless protection is unavailable. This is a modest but real cost of deferral that the claiming analysis in Module 11 should carry.

### 10. Data Tables for the Engine

| Constant | 2026 value | Basis |
|---|---|---|
| Part B standard monthly premium | $202.90 | CMS annual determination |
| Part B annual deductible | $283 | CMS |
| Part A inpatient deductible, per benefit period | $1,736 | CMS |
| Part A coinsurance, days 61–90 | $434 a day | CMS |
| Part A coinsurance, lifetime reserve days | $868 a day | CMS |
| Skilled nursing coinsurance, days 21–100 | $217.00 a day | CMS |
| Skilled nursing benefit ends | Day 100 | Statute |
| Part A premium, 30–39 quarters | $311 a month | CMS |
| Part A premium, under 30 quarters | $565 a month | CMS |
| Part B late enrolment penalty | 10% per 12 months, permanent | Statute |
| Part D late enrolment penalty | 1% of base premium a month, permanent | Statute |
| Eligibility age | 65, or 24 months after disability entitlement | Statute |

### 11. References

[34] Centers for Medicare & Medicaid Services, *2026 Medicare Parts A & B Premiums and Deductibles*. https://www.cms.gov/newsroom/fact-sheets/2026-medicare-parts-b-premiums-deductibles

[35] Centers for Medicare & Medicaid Services, *Medicare Deductible, Coinsurance & Premium Rates: CY 2026 Update*, MM14279. https://www.cms.gov/files/document/mm14279-medicare-deductible-coinsurance-premium-rates-cy-2026-update.pdf

### 12. Status in This System

| Layer | Status |
|---|---|
| Projection engine | **Applied in part.** The Part B standard premium of $202.90 and the annual deductible of $283 match the CMS determination for 2026. Medicare premiums are treated as qualified medical expenses under § 213(d) and are included in the amount tested against the 7.5 percent floor, which is correct. Healthcare cost is inflated at a separate and higher rate than general expenses. |
| Backend (`tax-be`) | **Not applied.** No Medicare logic. |
| Known limitations | Premiums are added to expenses but are **not deducted from the Social Security benefit**, so the gross and net benefit are not distinguished. The tax computation correctly uses the gross figure, but the cash-flow presentation shows a household receiving more than it does and separately paying a premium it has in fact already had withheld. The Part A deductible, the coinsurance tiers and the skilled nursing coinsurance are not modelled at all, so a hospital or skilled nursing episode produces no Part A cost — which understates a care year and interacts with the omission recorded in Module 33. The Part A premium for a beneficiary without forty quarters of coverage is absent, as is any tracking of quarters. The § 1839(f) hold-harmless provision is not implemented, and neither are the Part B or Part D late enrolment penalties. Medicare Advantage and supplement premiums are folded into general healthcare cost rather than modelled separately. |


---

## Module 16 — Income-Related Monthly Adjustment Amount

**Tax year:** 2026 · **As of:** September 2026 · **Primary authority:** Social Security Act § 1839(i); 20 CFR Part 418

---

### 1. Overview and Purpose

Beneficiaries with income above a threshold pay more than the standard Medicare premium. The addition is the income-related monthly adjustment amount, and it applies to both Part B and Part D.

Three features make it unlike a tax and unlike anything else in a retirement projection.

It is a **cliff, not a slope**. One dollar of income above a threshold moves the beneficiary to the next tier for the whole year. There is no phase-in and no proportional adjustment. Crossing the first joint threshold by a single dollar costs a couple $1,948.80 in Part B surcharge alone.

It uses income from **two years earlier**. The 2026 premium is set by the 2024 return. A decision taken today sets a premium two years from now, by which time the income that caused it is long past.

And it is **per person**. A married couple both enrolled pay two surcharges, so every figure in the tables below doubles for a couple.

The combination — a cliff, a two-year lag, and a doubling for couples — makes it the most easily triggered and least easily reversed cost in retirement planning. A Roth conversion, a property sale, or a large required distribution can produce a surcharge that arrives long after the decision and cannot be appealed, because the appeal route covers income that **fell**, not income that spiked once.

### 2. Governing Law and Authorities

| Type | Citation | What it establishes |
|---|---|---|
| Statute | Social Security Act § 1839(i) | Income-related increase in the Part B premium |
| Statute | Social Security Act § 1860D-13(a)(7) | The Part D adjustment |
| Regulation | 20 CFR § 418.1010 | Modified adjusted gross income for this purpose |
| Regulation | 20 CFR § 418.1205 | The major life-changing events |
| Regulation | 20 CFR § 418.1201 | New initial determinations |
| Form | Form SSA-44 | Medicare income-related monthly adjustment amount, life-changing event |
| Determination | CMS 2026 Medicare Parts A and B Premiums and Deductibles | The 2026 tables |

### 3. Key Definitions

| Term | Definition |
|---|---|
| **Modified adjusted gross income** | Adjusted gross income **plus tax-exempt interest**. Narrower than the § 1411 definition and narrower than the definitions used for the senior deduction and the state and local phasedown. |
| **Two-year lookback** | The premium for a year is determined from the return filed for the year two years earlier. |
| **New initial determination** | A redetermination of the surcharge using a more recent year's income, available only after a life-changing event. |
| **Life-changing event** | One of seven events listed in 20 CFR § 418.1205. |

### 4. Who Is Affected

Any Medicare beneficiary whose modified adjusted gross income two years earlier exceeded the first threshold. For 2026 that is **$109,000** for an individual and **$218,000** for a couple filing jointly.

A married beneficiary who files separately and lived with their spouse at any time during the year faces a much compressed schedule, moving to the top tiers at far lower income.

The surcharge is paid by each enrolled individual. A couple both on Medicare pay it twice.

### 5. Core Rules and Calculations

#### 5.1 Case Register

| # | Case | Applied |
|---|---|---|
| 1 | Surcharge based on modified adjusted gross income | Yes |
| 2 | Tax-exempt interest added back | **No** |
| 3 | Two-year lookback | Yes |
| 4 | Cliff structure, no phase-in | Yes |
| 5 | Part B surcharge tiers | Yes |
| 6 | Part D surcharge tiers | Yes |
| 7 | Per-person application, doubled for a couple | Yes |
| 8 | Separate compressed schedule for a separate filer | **No** |
| 9 | Thresholds indexed annually | Partially — inflated by a general factor |
| 10 | Life-changing event redetermination | **No** |
| 11 | A one-time income spike cannot be appealed | Yes, by omission |
| 12 | Surcharge as a deductible medical expense | Yes |
| 13 | Surcharge deducted from the Social Security benefit | **No** |

#### 5.2 The 2026 Part B tables

Modified adjusted gross income from the **2024** return determines the 2026 premium.[36]

| Individual MAGI | Joint MAGI | Part B surcharge | Total Part B premium |
|---|---|---|---|
| $109,000 or less | $218,000 or less | $0.00 | **$202.90** |
| over $109,000 to $137,000 | over $218,000 to $274,000 | $81.20 | $284.10 |
| over $137,000 to $171,000 | over $274,000 to $342,000 | $202.90 | $405.80 |
| over $171,000 to $205,000 | over $342,000 to $410,000 | $324.60 | $527.50 |
| over $205,000 to under $500,000 | over $410,000 to under $750,000 | $446.30 | $649.20 |
| $500,000 or more | $750,000 or more | $487.00 | **$689.90** |

The top tier is **3.4 times** the standard premium.

#### 5.3 The 2026 Part D tables

| Individual MAGI | Joint MAGI | Part D surcharge |
|---|---|---|
| $109,000 or less | $218,000 or less | $0.00 |
| over $109,000 to $137,000 | over $218,000 to $274,000 | $14.50 |
| over $137,000 to $171,000 | over $274,000 to $342,000 | $37.50 |
| over $171,000 to $205,000 | over $342,000 to $410,000 | $60.40 |
| over $205,000 to under $500,000 | over $410,000 to under $750,000 | $83.30 |
| $500,000 or more | $750,000 or more | $91.00 |

The Part D surcharge is added to whatever the beneficiary's chosen plan charges.

#### 5.4 The cost of crossing a threshold

Because the structure is a cliff, the marginal cost of the dollar that crosses a threshold is the whole of the next tier.

| Crossing | Extra monthly, per person | Annual, per person | **Annual, couple** |
|---|---|---|---|
| Into tier 2 | $81.20 + $14.50 = $95.70 | $1,148.40 | **$2,296.80** |
| Into tier 3 | $121.70 + $23.00 = $144.70 | $1,736.40 | **$3,472.80** |
| Into tier 4 | $121.70 + $22.90 = $144.60 | $1,735.20 | **$3,470.40** |
| Into tier 5 | $121.70 + $22.90 = $144.60 | $1,735.20 | **$3,470.40** |
| Into tier 6 | $40.70 + $7.70 = $48.40 | $580.80 | **$1,161.60** |

A couple one dollar over $218,000 of 2024 income pays **$2,296.80** more in 2026 than a couple one dollar under. Expressed as a marginal rate on that dollar it is meaningless; expressed as a planning constraint it is decisive.

#### 5.5 The two-year lookback

| Premium year | Determined by the return for |
|---|---|
| 2026 | 2024 |
| 2027 | 2025 |
| 2028 | 2026 |

A conversion executed in 2026 sets the 2028 premium. For a client retiring at 63 and enrolling at 65, income in the year they turn 63 is what sets the first Medicare premium they ever pay — which is often the last high-income year of their working life.

#### 5.6 The appeal route — Form SSA-44

A beneficiary may request a **new initial determination**, using a more recent year's income, only after a major life-changing event. The regulation lists **seven**:[37]

1. Your spouse dies
2. You marry
3. Your marriage ends through divorce or annulment
4. You or your spouse stop working or reduce the hours you work
5. You or your spouse experiences a loss of income-producing property, provided the loss was not at your direction and is not the result of ordinary investment risk
6. You or your spouse experiences a scheduled cessation, termination or reorganisation of an employer's pension plan
7. You or your spouse receives a settlement from an employer because of the employer's closure, bankruptcy or reorganisation

**A note on the count.** The regulation states seven events, at paragraphs (a) through (g). Form SSA-44 presents **eight** options, because it separates "work stoppage" from "work reduction", which the regulation combines in a single paragraph. Both figures appear in practice; the regulation is the authority and it lists seven.

The list is **closed**. Nothing outside it qualifies, and the most common causes of a spike are all outside it:

| Event | Qualifies? |
|---|---|
| Retirement or reducing hours | **Yes** — event 4 |
| Death of a spouse | **Yes** — event 1 |
| Divorce | **Yes** — event 3 |
| A large Roth conversion | **No** |
| Sale of a business | **No** |
| Sale of a rental property | **No** |
| A large required minimum distribution | **No** |
| An inheritance | **No** |
| Exercise of stock options | **No** |
| Loss of investment property to ordinary market decline | **No** — expressly excluded |

Retirement is the important one. A client retiring at 65 whose premium is set by their final working year at full salary can file Form SSA-44 and have the premium determined on their expected retirement income instead. This is routinely missed and is worth several thousand dollars in the first two years of Medicare.

### 6. Examples and Case Calculations

#### Example 1 — A couple one dollar over the first threshold

2024 modified adjusted gross income of $218,001.

```
Part B   284.10 × 12 × 2                       =  $6,818.40
Part D    14.50 × 12 × 2                       =    $348.00
                                                  ---------
                                                  $7,166.40

A couple at $218,000                              $4,869.60
Cost of one dollar of income                      $2,296.80
```

#### Example 2 — A Roth conversion setting a premium two years later

A couple aged 64 with $150,000 of income convert $120,000 in 2026 to use the 22 and 24 percent brackets.

```
2026 modified adjusted gross income               $270,000
Determines the premium for                            2028
2028 tier, on the 2026 thresholds                  tier 3
Additional cost in 2028, couple                   $3,472.80
```

The conversion may still be correct — $3,472.80 against the bracket arbitrage on $120,000 is usually a good trade — but it must be counted. Being unaware of it is what makes it feel like a penalty.

#### Example 3 — Retirement, and the appeal that works

A client retires in 2026 at 65 with 2024 income of $340,000 from their practice. Expected 2026 income is $95,000.

```
Without Form SSA-44
   2026 premium set on 2024 income of 340,000 → tier 4
   Part B 527.50 + Part D 60.40 = 587.90 a month
   Annual, single beneficiary                     $7,054.80

With Form SSA-44, event 4 — work stoppage
   Redetermined on expected 2026 income of 95,000 → standard
   Part B 202.90 + plan premium
   Annual saving                                  $4,620.00
```

The form must be filed with evidence of the work stoppage. The saving repeats in the following year as well, because 2025 income would otherwise also have been high.

#### Example 4 — A business sale, which cannot be appealed

The same client sells their practice in 2026 for a $900,000 gain.

```
2026 modified adjusted gross income               $995,000
Determines the premium for                            2028
2028 tier                                    top tier — 6
Part B 689.90 + Part D 91.00 = 780.90 a month
Annual, single beneficiary                        $9,370.80
Against the standard premium                      $2,434.80
Additional cost                                   $6,936.00
```

There is no appeal. A sale is not a life-changing event, and the loss-of-property provision expressly excludes disposals at the taxpayer's direction. The only response is to have known in advance — by spreading the gain over years through an instalment sale, or by accepting the cost as part of the transaction.

### 7. Interactions with Other Rules

**Roth conversions (Module 10) and required distributions (Module 09).** Both raise modified adjusted gross income and both set the premium two years later. A conversion programme should be sized against the tier thresholds as well as the tax brackets, because the tier boundaries frequently bind first.

**Qualified charitable distributions (Module 09).** The only mechanism that satisfies a required distribution without raising modified adjusted gross income, and therefore the only one that does not affect the surcharge.

**Tax-exempt interest.** Added back for this purpose. A municipal bond portfolio reduces taxable income and does not reduce the surcharge.

**Net investment income tax (Module 06).** Both are driven by modified adjusted gross income, on slightly different definitions, and a single event triggers one now and the other in two years.

**Filing status (Module 03).** The threshold halves from $218,000 to $109,000 on a change from joint to single. A survivor with unchanged income can move up two tiers.

**Medical expense deduction (Module 32).** The surcharge is a Medicare premium and is a qualified medical expense under § 213(d).

**Death of a spouse (Module 35).** Death is a qualifying life-changing event, which matters because the survivor's threshold halves at the same moment.

### 8. Common Scenarios and Edge Cases

**It is a cliff.** There is no phase-in. The dollar that crosses the line costs the whole tier.

**It applies per person.** Every figure doubles for a couple, and a couple can both be moved by one spouse's income because the threshold is measured on the joint return.

**Tax-exempt interest counts.** This is the most common surprise for a retiree holding municipals.

**A one-time spike cannot be appealed.** The list is closed and does not include conversions, sales, distributions, inheritances or option exercises.

**Retirement can be appealed, and usually should be.** A client enrolling at 65 after a high final working year has a straightforward claim under event 4, and the saving is frequently over $4,000.

**The regulation lists seven events; the form shows eight.** The difference is that Form SSA-44 splits work stoppage from work reduction. Nothing turns on the count, but a document that states one figure without explaining the other invites a challenge.

**Married filing separately is severely treated.** A separate filer who lived with their spouse moves to the upper tiers at income levels far below the joint thresholds.

**The premium is deducted from the Social Security benefit.** A high-income couple can find a substantial share of their gross benefit absorbed before anything reaches them.

### 9. Planning Implications

Any deliberate recognition of income — a conversion, a harvest, an instalment election — should be sized against the tier thresholds two years forward, not merely against the tax brackets. The thresholds are usually the binding constraint for a household with moderate taxable income and large pre-tax balances.

Where a spike is unavoidable, spreading it matters more than in the tax computation. Two years at tier 3 costs less than one year at tier 6, and the tier structure rewards smoothing in a way the rate schedule does not.

For a client retiring after a high-income year, Form SSA-44 should be filed as a matter of routine. It is the one part of this module where the beneficiary has a clear and reliable remedy.

For a survivor, the halving of the threshold coincides with the death of a spouse, which is itself a qualifying event. The redetermination should be filed at the same time as the other post-death administration.

Because the surcharge is a medical expense, in a year with substantial care costs it contributes to an itemised deduction above the 7.5 percent floor, which returns a fraction of it.

### 10. Data Tables for the Engine

| Constant | 2026 value | Basis |
|---|---|---|
| Tier 1 ceiling | $109,000 individual · $218,000 joint | CMS |
| Tier 2 ceiling | $137,000 · $274,000 | CMS |
| Tier 3 ceiling | $171,000 · $342,000 | CMS |
| Tier 4 ceiling | $205,000 · $410,000 | CMS |
| Tier 5 ceiling | under $500,000 · under $750,000 | CMS |
| Part B surcharges | $0 · $81.20 · $202.90 · $324.60 · $446.30 · $487.00 | CMS |
| Part D surcharges | $0 · $14.50 · $37.50 · $60.40 · $83.30 · $91.00 | CMS |
| Lookback | Two years | Statute |
| Structure | Cliff, no phase-in | Statute |
| Application | Per enrolled individual | Statute |
| MAGI definition | AGI plus tax-exempt interest | 20 CFR § 418.1010 |
| Life-changing events | Seven, 20 CFR § 418.1205 | Regulation |

### 11. References

[36] Centers for Medicare & Medicaid Services, *2026 Medicare Parts A & B Premiums and Deductibles*. https://www.cms.gov/newsroom/fact-sheets/2026-medicare-parts-b-premiums-deductibles

[37] 20 CFR § 418.1205, *What is a major life-changing event?* Electronic Code of Federal Regulations. https://www.ecfr.gov/current/title-20/chapter-III/part-418/subpart-B/section-418.1205

[38] Social Security Administration, *Form SSA-44, Medicare Income-Related Monthly Adjustment Amount — Life-Changing Event*. https://www.ssa.gov/forms/ssa-44.pdf

### 12. Status in This System

| Layer | Status |
|---|---|
| Projection engine | **Applied.** All six tiers and both the Part B and Part D surcharge schedules match the CMS determination for 2026. The two-year lookback is implemented — the premium for a year is computed from the modified adjusted gross income recorded two years earlier rather than from current income, which is the detail most models get wrong. The cliff structure is preserved rather than smoothed, and the surcharge is applied per enrolled person and doubled for a couple. It is included in the amount tested against the § 213 medical floor. |
| Backend (`tax-be`) | **Not applied.** No Medicare logic. |
| Known limitations | Tax-exempt interest is **not** added back to modified adjusted gross income for this purpose, so a beneficiary holding municipal bonds is shown a lower tier than 20 CFR § 418.1010 would produce. The compressed schedule for a married beneficiary filing separately is not implemented. The thresholds are inflated by the engine's general inflation factor rather than by the mechanism CMS actually uses, so tier boundaries drift from the published figures in later projected years. There is no representation of a new initial determination under Form SSA-44, so the projection cannot show a client obtaining relief after retirement — an omission that overstates cost in the first two Medicare years for anyone retiring from a high income. As with Module 15, the surcharge is added to expenses rather than deducted from the Social Security benefit. |


---

## Module 17 — Qualified Business Income Deduction

**Tax year:** 2026 · **As of:** September 2026 · **Primary authority:** IRC § 199A

---

### 1. Overview and Purpose

Section 199A allows a deduction of up to 20 percent of qualified business income from a domestic trade or business conducted as a sole proprietorship, partnership, S corporation, trust or estate. It is a deduction against taxable income rather than a reduction of adjusted gross income, and it is available whether or not the taxpayer itemises.

The provision is layered rather than simple. Below a threshold the deduction is a flat 20 percent of qualified business income. Above the threshold two separate limitations phase in over a range, and which one applies depends on whether the business is a **specified service trade or business**. For a service business the deduction disappears entirely by the top of the range. For any other business it is instead capped by reference to W-2 wages paid and the unadjusted basis of qualifying property. An overall ceiling of 20 percent of taxable income less net capital gain sits above everything.

Three changes took effect for tax year 2026. The Tax Cuts and Jobs Act sunset was removed, so the deduction is now permanent. The phase-in range was widened from $50,000 and $100,000 to **$75,000 and $150,000**, which softens the cliff for service businesses. And a new § 199A(i) provides a **minimum deduction of $400** for a taxpayer with at least $1,000 of qualified business income from businesses in which they materially participate.

For the professional-practice owners this system commonly serves, the specified service classification is usually the decisive question, and the answer is generally unfavourable. A dentist, physician, lawyer, accountant or consultant loses the deduction entirely above the top of the range. An engineer or architect at identical income keeps it, because those two professions were deliberately excluded from the service list.

### 2. Governing Law and Authorities

| Type | Citation | What it establishes |
|---|---|---|
| Statute | IRC § 199A(a) | The 20 percent deduction |
| Statute | IRC § 199A(b)(2) | The W-2 wage and unadjusted basis limitation |
| Statute | IRC § 199A(b)(3) | The phase-in range for the wage limitation |
| Statute | IRC § 199A(d)(2) | Definition of a specified service trade or business |
| Statute | IRC § 199A(d)(3) | Phase-in of the service exclusion |
| Statute | IRC § 199A(e)(1) | Taxable income computed without regard to § 68 |
| Statute | IRC § 199A(e)(2) | Threshold amount |
| Statute | IRC § 199A(i) | Minimum deduction for active qualified business income |
| Regulation | Treas. Reg. § 1.199A-1 to -6 | Operating rules, aggregation, and the de minimis rule |
| Legislation | P.L. 119-21, § 70105 | Permanence, wider phase-in range, and the minimum deduction |
| Guidance | Rev. Proc. 2025-32, § 3.26 | 2026 threshold and phase-in amounts |

### 3. Key Definitions

| Term | Definition |
|---|---|
| **Qualified business income** | The net amount of qualified items of income, gain, deduction and loss from a qualified trade or business. Excludes capital gain, dividends, interest not allocable to the business, and reasonable compensation or guaranteed payments paid to the owner. |
| **Specified service trade or business** | A trade or business in the fields listed in § 199A(d)(2), which adopts the § 1202(e)(3)(A) list **minus engineering and architecture**, together with any business whose principal asset is the reputation or skill of its employees or owners, and investing, investment management, trading and dealing in securities. |
| **Threshold amount** | The taxable income level at which the limitations begin. $403,500 joint, $201,775 married filing separately, $201,750 otherwise for 2026. |
| **Phase-in range** | $150,000 above the threshold on a joint return, $75,000 otherwise. |
| **W-2 wages** | Wages paid by the qualified trade or business and properly allocable to qualified business income. |
| **UBIA** | Unadjusted basis immediately after acquisition of qualified property — original cost, undiminished by depreciation, for property still within its depreciable period. |
| **Applicable taxpayer** | For § 199A(i), a taxpayer with at least $1,000 of aggregate qualified business income from active qualified trades or businesses in which they materially participate under § 469(h). |

### 4. Who Is Affected

Any individual, trust or estate with income from a pass-through trade or business. C corporation income is outside § 199A entirely.

Whether the limitations apply depends on **taxable income**, not on business income. A taxpayer with a large service business but low taxable income — because of a spouse's deductions, a loss elsewhere, or a large charitable gift — may sit below the threshold and take the full deduction.

Specified service businesses under § 199A(d)(2), read with § 1202(e)(3)(A):

| In the service list | Excluded from the service list |
|---|---|
| Health, law, accounting, actuarial science | **Engineering** |
| Performing arts, consulting, athletics | **Architecture** |
| Financial services, brokerage services | Real estate, construction |
| Investing and investment management, trading, dealing in securities | Manufacturing, retail, wholesale |
| Any business whose principal asset is the reputation or skill of one or more employees or owners | Restaurants, transport, software, farming |

The exclusion of engineering and architecture is explicit in the statute and is the single most consequential distinction in the provision.

### 5. Core Rules and Calculations

#### 5.1 Case Register

| # | Case | Applied |
|---|---|---|
| 1 | 20 percent of qualified business income below the threshold | Yes |
| 2 | Threshold amounts by filing status | Partially — D23 |
| 3 | Phase-in range of $75,000 and $150,000 | Yes |
| 4 | Specified service classification | Yes |
| 5 | Engineering and architecture excluded from the service list | Yes |
| 6 | Service deduction fully phased out at the top of the range | Yes |
| 7 | W-2 wage limitation, 50 percent of wages | Yes |
| 8 | Alternative limitation, 25 percent of wages plus 2.5 percent of UBIA | Yes |
| 9 | Wage limitation phased in over the range | Yes |
| 10 | Overall cap of 20 percent of taxable income less net capital gain | Yes |
| 11 | § 199A(i) minimum deduction of $400 | **No** — D22 |
| 12 | $1,000 active qualified business income test | **No** |
| 13 | Material participation under § 469(h) for the minimum deduction | **No** |
| 14 | Taxable income computed without regard to § 68 | Not applicable — § 68 is not implemented |
| 15 | Treas. Reg. § 1.199A-1(b)(14) de minimis rule for a mixed business | **No** |
| 16 | Aggregation election under Treas. Reg. § 1.199A-4 | **No** |
| 17 | Qualified REIT dividends and publicly traded partnership income | **No** |
| 18 | Negative qualified business income carried to the next year | Yes |
| 19 | Reasonable compensation and guaranteed payments excluded from QBI | **No** |
| 20 | Deduction available to non-itemisers | Yes |

#### 5.2 The computation

```
Step 1  tentative = 0.20 × qualifiedBusinessIncome

Step 2  if taxableIncomeBefore199A ≤ threshold
            deduction = tentative

Step 3  else
            phase = (taxableIncomeBefore199A − threshold) ÷ rangeWidth , capped at 1

            if specified service trade or business
                applicable = 1 − phase
                deduction  = 0.20 × QBI × applicable

            else
                wageLimit = max( 0.50 × W2 ,
                                 0.25 × W2 + 0.025 × UBIA )
                deduction = tentative − (tentative − min(tentative, wageLimit)) × phase

Step 4  overall cap
            deduction = min( deduction , 0.20 × (taxableIncome − netCapitalGain) )
```

The two limitations work in opposite directions. For a service business the deduction itself shrinks. For any other business the deduction is pulled down toward the wage limit, and where wages are ample the limit never binds.

#### 5.3 The 2026 thresholds

| Filing status | Threshold | Top of the phase-in range | Range width |
|---|---|---|---|
| Married filing jointly | **$403,500** | **$553,500** | $150,000 |
| Married filing separately | **$201,775** | **$276,775** | $75,000 |
| All other returns | **$201,750** | **$276,750** | $75,000 |

The separate-return figures are **$25 higher** than the single figures, in the same way that the § 1 rate schedule thresholds diverge. The difference is small and it is not a typographical error in the Revenue Procedure.[39]

Note also that the separate-return range is the full $75,000, not half the joint range.

#### 5.4 The specified service phase-out

Above the threshold the applicable percentage of a service business's qualified business income falls linearly to zero. On $400,000 of qualified business income, married filing jointly:

| Taxable income | Position in range | Deduction |
|---|---|---|
| $403,500 | 0% | **$80,000** |
| $428,500 | 16.7% | $66,667 |
| $478,500 | 50.0% | $40,000 |
| $528,500 | 83.3% | $13,333 |
| **$553,500** | 100% | **$0** |

Over $150,000 of taxable income the deduction falls by $80,000. That is an implicit marginal rate of 53 percent on top of the statutory rate across the range, and it is the reason income timing matters so much for service-business owners.

Widening the range from $100,000 to $150,000 for 2026 reduced that implicit rate. Under the old range the same $80,000 was lost over $100,000, an implicit 80 percent.

#### 5.5 The wage and property limitation

For a non-service business the deduction above the threshold is limited to the **greater** of:

- 50 percent of W-2 wages paid by the business, or
- 25 percent of W-2 wages plus 2.5 percent of the unadjusted basis of qualified property.

The alternative exists for capital-intensive businesses with few employees. Real estate is the paradigm case: a rental operation may pay almost no wages but hold substantial depreciable property.

On $500,000 of qualified business income, joint, with $80,000 of wages:

| UBIA | Wage/property limit | Deduction at full phase-in |
|---|---|---|
| $0 | $40,000 | $40,000 |
| $500,000 | $40,000 | $40,000 |
| $2,000,000 | $70,000 | $70,000 |
| $4,000,000 | $120,000 | $100,000 — capped by 20% of QBI |

The last row shows the limit ceasing to bind: once the wage and property figure exceeds 20 percent of qualified business income, the full deduction is available.

#### 5.6 The overall cap

The deduction can never exceed 20 percent of taxable income reduced by net capital gain. This binds where business income is large relative to total taxable income, or where much of taxable income is capital gain.

```
QBI 300,000, taxable income 250,000 of which 200,000 is net capital gain

   20% of QBI                          60,000
   20% × (250,000 − 200,000)           10,000   ← binds
   Deduction                          $10,000
```

#### 5.7 The minimum deduction — § 199A(i)

New for 2026. Where a taxpayer's aggregate qualified business income from **active** qualified trades or businesses is at least $1,000, the deduction is the greater of the amount otherwise computed or **$400**.[40]

"Active" means the taxpayer materially participates within the meaning of § 469(h). Both the $400 and the $1,000 are indexed for taxable years beginning after 2026, rounded to the nearest $5.

The provision is small in amount and matters at the bottom of the income range — a taxpayer with modest business income whose computed deduction would be under $400, or a service-business owner fully phased out who nonetheless has $1,000 of active qualified business income.

### 6. Examples and Case Calculations

#### Example 1 — Below the threshold

Married couple, qualified business income $300,000, taxable income before § 199A of $380,000.

```
Taxable income is below the $403,500 threshold
Deduction  20% × 300,000 = $60,000
```

No wage limitation applies and the service classification is irrelevant. A dentist and an engineer at this income receive the same deduction.

#### Example 2 — A dentist and an engineer at identical income

Both married filing jointly, qualified business income $400,000, W-2 wages $150,000, taxable income $553,500.

```
Dentist — a specified service trade or business
   Position in range        100%
   Applicable percentage      0%
   Deduction                  $0

Engineer — not a specified service trade or business
   Tentative 20% × 400,000              80,000
   Wage limit max(75,000, 37,500)       75,000
   Fully phased in, so the limit binds
   Deduction                           $75,000
```

Identical income, identical wages, identical everything except the field. The difference is $75,000 of deduction, worth $26,250 of tax at 35 percent. This distinction is statutory and cannot be planned around by restructuring, only by moving taxable income below the threshold.

#### Example 3 — The wage limitation phasing in

Married couple, non-service business, qualified business income $500,000, W-2 wages $80,000, no qualified property.

| Taxable income | Position in range | Deduction |
|---|---|---|
| $403,500 | 0% | $80,700 |
| $453,500 | 33.3% | $80,000 |
| $503,500 | 66.7% | $60,000 |
| $553,500 | 100% | **$40,000** |

The deduction falls from a tentative $100,000 toward the wage limit of $40,000 as taxable income rises through the range. Note the first row is capped not by wages but by the overall 20-percent-of-taxable-income ceiling.

#### Example 4 — Paying wages to preserve the deduction

The business in Example 3 at full phase-in. If it converts $70,000 of profit into additional W-2 wages:

```
Before   wages 80,000    limit 40,000    deduction 40,000
After    wages 150,000   limit 75,000    QBI falls to 430,000
                                         tentative 86,000
                                         deduction 75,000
```

The deduction rises by $35,000. The cost is payroll tax on the additional wages, and the wages must be reasonable for services actually performed. This is the principal planning lever available to a non-service business above the threshold, and it does nothing at all for a service business.

### 7. Interactions with Other Rules

**Standard and itemised deductions (Module 02).** Taxable income for the § 199A threshold is computed **after** the standard or itemised deduction but **before** the § 199A deduction itself. Section 199A(e)(1) as amended directs that it also be computed without regard to § 68, so the new overall limitation on itemised deductions does not feed back into this calculation.

**Rate schedules (Module 01).** The deduction reduces taxable income and therefore tax, but does not reduce adjusted gross income, so it does not help with any provision keyed to adjusted gross income — the Medicare surcharge, the net investment income tax, or the taxation of Social Security benefits.

**Self-employment tax (Module 04).** The § 164(f) deduction for half the self-employment tax reduces qualified business income where the tax arises from that business. The deduction does not reduce self-employment tax.

**Retirement contributions (Module 07).** A deductible contribution attributable to the business reduces qualified business income, so the combined benefit is less than the sum of the two considered separately.

**Excess business loss (Module 18) and passive losses (Module 25).** A loss allowed in the current year reduces qualified business income. A suspended loss does not, until it is released.

**Real estate (Modules 20 to 23).** A rental operation may qualify as a trade or business for § 199A purposes, and the 2.5 percent of unadjusted basis alternative is designed for exactly that case.

### 8. Common Scenarios and Edge Cases

**The threshold is taxable income, not business income.** A taxpayer with $800,000 of qualified business income and $350,000 of taxable income is below the threshold and takes the full 20 percent.

**Engineering and architecture are excluded from the service list by statute.** This is not an administrative concession and does not extend by analogy to other technical professions.

**Reputation or skill is narrower than it sounds.** The regulations confine it to endorsement income, licensing of an individual's likeness or name, and appearance fees. It does not sweep in every business that depends on a founder's expertise.

**A mixed business may be treated as wholly non-service under the de minimis rule.** Where gross receipts are $25 million or less and less than 10 percent are attributable to service activities, the whole business is treated as non-service. Above $25 million the threshold falls to 5 percent.

**Aggregation can rescue a wage-limited business.** Where one entity has income and little payroll and a commonly controlled entity has payroll, an election under Treas. Reg. § 1.199A-4 may combine them. The election is consistent-year and difficult to revoke.

**A negative amount carries forward.** Where qualified business income across all businesses is negative, the loss carries to the following year and reduces that year's qualified business income before any deduction.

**Reasonable compensation and guaranteed payments are excluded from qualified business income.** An S corporation owner reduces their own qualified business income by paying themselves a salary, while simultaneously creating the W-2 wages the limitation needs. Above the threshold there is an optimum; below it, salary purely reduces the deduction.

**The deduction does not reduce adjusted gross income.** It cannot be used to fall below a Medicare surcharge tier or a net investment income tax threshold.

### 9. Planning Implications

For a service business, the entire question is whether taxable income can be brought below the threshold, or at least lower into the range. Every dollar of taxable income removed across the range returns roughly 53 cents of deduction on a $400,000 qualified business income, on top of the ordinary rate benefit. Retirement plan contributions, charitable giving and the timing of income are all worth more in that band than their headline rate suggests. A defined benefit or cash balance plan — which the backend strategy library already catalogues — is the largest single lever available.

For a non-service business above the threshold, the lever is W-2 wages, and Example 4 quantifies it. The trade is payroll tax against restored deduction, and it usually favours paying the wages where the wage limit is binding.

For a capital-intensive business, the 2.5 percent of unadjusted basis alternative is often more valuable than the wage test, and it survives the end of the depreciable period only while the property remains within it.

The widening of the phase-in range for 2026 is a genuine improvement for service businesses and should be reflected in any plan built on the older $100,000 range.

### 10. Data Tables for the Engine

| Constant | 2026 value | Indexed |
|---|---|---|
| Deduction rate | 20% | Fixed |
| Threshold, married filing jointly | $403,500 | Yes |
| Threshold, married filing separately | $201,775 | Yes |
| Threshold, all other returns | $201,750 | Yes |
| Top of range, married filing jointly | $553,500 | Yes |
| Top of range, married filing separately | $276,775 | Yes |
| Top of range, all other returns | $276,750 | Yes |
| Range width | $150,000 joint, $75,000 otherwise | Fixed by statute |
| Wage limitation | 50% of W-2 wages | Fixed |
| Alternative limitation | 25% of W-2 wages + 2.5% of UBIA | Fixed |
| Overall cap | 20% of taxable income less net capital gain | Fixed |
| Minimum deduction, § 199A(i) | $400 | Yes, after 2026 |
| Active QBI test for the minimum | $1,000 | Yes, after 2026 |
| De minimis service threshold | 10% of gross receipts, 5% above $25m | Fixed |

### 11. References

[39] Internal Revenue Service, *Revenue Procedure 2025-32*, § 3.26. https://www.irs.gov/pub/irs-drop/rp-25-32.pdf

[40] One Big Beautiful Bill Act, P.L. 119-21, § 70105, amending IRC § 199A(b)(3), (d)(3) and (i). https://www.govinfo.gov/content/pkg/PLAW-119publ21/html/PLAW-119publ21.htm

[41] 26 U.S.C. § 199A. United States Code, Office of the Law Revision Counsel. https://www.govinfo.gov/app/collection/uscode

[42] Treas. Reg. §§ 1.199A-1 to 1.199A-6. Electronic Code of Federal Regulations. https://www.ecfr.gov/current/title-26

### 12. Status in This System

| Layer | Status |
|---|---|
| Projection engine | **Applied, and unusually complete.** The 20 percent rate, the threshold and phase-in structure, the specified service phase-out and the W-2 wage limitation are all implemented. The alternative 25 percent of wages plus 2.5 percent of unadjusted basis test is present and computed as the greater of the two, which many models omit. The overall cap of 20 percent of taxable income less net capital gain is applied. The phase-in range reflects the widened OBBBA figures of $75,000 and $150,000 rather than the pre-2026 amounts. The specified service list correctly adopts the § 1202(e)(3)(A) fields **and correctly excludes engineering and architecture**, which is the distinction that decides the outcome for most professional clients. |
| Backend (`tax-be`) | **Not applied.** `strategyPhaseMap.js` catalogues "QBI Deduction Optimization" as a named strategy, but no § 199A computation exists in the backend. |
| Known limitations | The married-filing-separately threshold is held as $201,750 and $276,750; Revenue Procedure 2025-32 gives **$201,775 and $276,775**. The $25 difference is small but it is the same class of divergence the engine handles correctly in the § 1 rate schedules, and it should agree with the published figure. Recorded as D23. The new § 199A(i) minimum deduction is **not applied**: the constant `min: 400` exists in the configuration and is **never referenced** by the deduction function, so a taxpayer entitled to the $400 floor receives nothing. Neither the $1,000 active qualified business income test nor the § 469(h) material participation condition is implemented. Recorded as D22. Also absent: the de minimis rule that can treat a mixed business as wholly non-service, the aggregation election under Treas. Reg. § 1.199A-4, the separate component for qualified REIT dividends and publicly traded partnership income, and the exclusion of reasonable compensation and guaranteed payments from qualified business income — the last meaning that an S corporation owner's salary is not automatically removed from the qualified business income figure. |


---

## Module 18 — Excess Business Loss

**Tax year:** 2026 · **As of:** September 2026 · **Primary authority:** IRC § 461(l)

---

### 1. Overview and Purpose

Section 461(l) limits how much net business loss a non-corporate taxpayer may use against non-business income in a single year. Aggregate deductions from trades or businesses are compared with aggregate business income plus a threshold amount, and anything beyond that is an **excess business loss**. The excess is disallowed for the year and carried forward as a net operating loss.

The provision sits **last** in the ordering of loss limitations. A loss must first survive the basis limitation, then the at-risk limitation, then the passive activity rules, and only what remains is tested here. Module 26 treats the first two and Module 25 the third; this module is the fourth and final gate.

Two changes matter for 2026. The One Big Beautiful Bill Act made the limitation **permanent**, removing the expiry that would otherwise have ended it after 2028. And it reset the indexing base, with the result that the threshold **fell** — from $313,000 and $626,000 in 2025 to **$256,000 and $512,000** in 2026, a decrease of 18.2 percent.[43][44] A decrease in an inflation-adjusted threshold is unusual and is the direct consequence of the statutory change rather than of any price movement.

### 2. Governing Law and Authorities

| Type | Citation | What it establishes |
|---|---|---|
| Statute | IRC § 461(l)(1) | The disallowance |
| Statute | IRC § 461(l)(2) | Treatment of the disallowed amount as a net operating loss |
| Statute | IRC § 461(l)(3)(A) | Definition of excess business loss and the threshold |
| Statute | IRC § 461(l)(3)(C) | Inflation adjustment of the threshold |
| Statute | IRC § 172 | Net operating losses — Module 27 |
| Legislation | P.L. 119-21, § 70601 | Made the limitation permanent; reset the indexing base |
| Guidance | Rev. Proc. 2025-32, § 3.31 | 2026 threshold |
| Form | Form 461 | Limitation on business losses |

### 3. Key Definitions

| Term | Definition |
|---|---|
| **Excess business loss** | The excess of aggregate deductions attributable to trades or businesses over the sum of aggregate gross income from those trades or businesses and the threshold amount. |
| **Threshold amount** | $256,000, or $512,000 on a joint return, for 2026. |
| **Aggregate** | Across all of the taxpayer's trades or businesses combined, not business by business. |
| **Non-business income** | Wages, portfolio income, retirement distributions and similar amounts, against which business losses would otherwise be deductible without limit. |

### 4. Who Is Affected

Any taxpayer other than a C corporation — individuals, trusts and estates. The limitation is applied at the **partner or shareholder level**, not at the entity level, so a partnership or S corporation passes losses through and each owner tests their own aggregate position.

It bites where a taxpayer has a large business loss and substantial income from elsewhere. The archetypal cases are a professional with a high salary who also holds a loss-generating venture, and an owner whose business produces a large loss in a year when a spouse's income or a portfolio gain supplies the other income.

### 5. Core Rules and Calculations

#### 5.1 Case Register

| # | Case | Applied |
|---|---|---|
| 1 | Aggregate business deductions against aggregate business income | Yes |
| 2 | Threshold amount by filing status | Yes |
| 3 | Threshold indexed annually | Partially — inflated by the engine's general factor |
| 4 | Disallowed amount treated as a net operating loss in the next year | Yes |
| 5 | Applied **after** basis, at-risk and passive limitations | Yes |
| 6 | Applied at the owner level, not the entity level | Yes, in effect |
| 7 | Wages excluded from business income for this purpose | **No** |
| 8 | Capital gains and losses limited in the computation | **No** |
| 9 | Limitation made permanent by P.L. 119-21 | Yes, by omission of any expiry |
| 10 | Threshold decrease from 2025 to 2026 | Yes — the constant is current |
| 11 | Form 461 reporting | Not applicable |

#### 5.2 The computation

```
aggregateBusinessDeductions − aggregateBusinessIncome  =  netBusinessLoss

excessBusinessLoss = max(0, netBusinessLoss − thresholdAmount)

allowedThisYear    = netBusinessLoss − excessBusinessLoss
carriedForward     = excessBusinessLoss , as a net operating loss
```

The threshold is the amount of net business loss that **may** be used against non-business income. It is not a floor below which nothing is allowed.

#### 5.3 The 2026 threshold, and why it fell

| Tax year | Single and others | Joint | Change |
|---|---|---|---|
| 2025 | $313,000 | $626,000 | — |
| **2026** | **$256,000** | **$512,000** | **−18.2%** |

Section 70601(b) of P.L. 119-21 changed the indexing reference in § 461(l)(3)(C) from December 31 2018 to December 31 2025, and the base calendar year from 2017 to 2024, effective for taxable years beginning after 31 December 2025.[44] The effect is to restart the inflation adjustment from the original $250,000 and $500,000 amounts against a 2024 base, rather than continuing the series that had run from 2018. The threshold consequently resets downward.

A taxpayer planning a loss year on the 2025 figure has $57,000 less room than expected, or $114,000 less on a joint return.

Section 70601(a) separately struck the expiry date, so the limitation no longer sunsets. That change takes effect for taxable years beginning after 31 December 2026.

#### 5.4 Position in the ordering

Section 461(l) is the fourth and last of the loss limitations, and the order is not interchangeable:

| Gate | Limitation | Module |
|---|---|---|
| 1 | Basis — § 704(d) for partners, § 1366(d) for S corporation shareholders | 26 |
| 2 | At-risk — § 465 | 23 and 26 |
| 3 | Passive activity — § 469 | 25 |
| **4** | **Excess business loss — § 461(l)** | **this module** |

A loss suspended at an earlier gate never reaches this one. Testing § 461(l) first would disallow amounts that were never allowable in the first place, and would understate the carryforwards recorded at the earlier gates.

#### 5.5 What happens to the disallowed amount

The excess business loss is **not** lost. Section 461(l)(2) treats it as a net operating loss carryover to the following taxable year, where it becomes subject to the § 172 rules in Module 27 — principally the limitation of a post-2017 net operating loss deduction to 80 percent of taxable income.

The consequence is a two-stage deferral. The loss is disallowed in year one by § 461(l), becomes a net operating loss in year two, and is then usable only against 80 percent of that year's taxable income.

### 6. Examples and Case Calculations

#### Example 1 — Below the threshold

Married couple. Wages $400,000. A business produces a net loss of $300,000 after surviving the basis, at-risk and passive gates.

```
Net business loss                        300,000
Threshold, joint                         512,000
Excess business loss                           0
Allowed against wages                   $300,000
```

The whole loss is used. Taxable income before deductions is $100,000.

#### Example 2 — Above the threshold

The same couple, but the loss is $800,000.

```
Net business loss                        800,000
Threshold, joint                         512,000
Excess business loss                     288,000   disallowed this year
Allowed against wages                    512,000
Taxable income before deductions           $0  (400,000 − 512,000, floored)
Carried forward as a net operating loss  $288,000
```

#### Example 3 — What the 2026 reset costs

The same $800,000 loss, compared across the two years.

| | 2025 threshold | 2026 threshold |
|---|---|---|
| Net business loss | $800,000 | $800,000 |
| Threshold, joint | $626,000 | $512,000 |
| Allowed currently | $626,000 | $512,000 |
| Disallowed | $174,000 | **$288,000** |

An additional $114,000 is deferred purely because of the statutory reset. At a 32 percent marginal rate that is $36,480 of tax paid a year earlier than it would have been under the 2025 threshold.

#### Example 4 — The disallowed amount in the following year

Continuing Example 2. In the next year the couple has $200,000 of taxable income before the net operating loss.

```
Net operating loss carried in                       288,000
Limitation under § 172, 80% of taxable income       160,000
Deduction allowed                                   160,000
Taxable income after                                 40,000
Remaining carryforward                             $128,000
```

The loss suspended by § 461(l) is not simply released in the next year; it meets a second limitation on arrival.

### 7. Interactions with Other Rules

**Basis, at-risk and passive rules (Modules 23, 25 and 26).** All three come first. Only a loss that has survived them is aggregated here.

**Net operating losses (Module 27).** The disallowed amount becomes a net operating loss in the following year and is then subject to the 80 percent limitation.

**Qualified business income (Module 17).** A loss allowed in the current year reduces qualified business income. A loss disallowed by § 461(l) does not reduce it this year, but the resulting net operating loss will affect the computation when it is used.

**Self-employment tax (Modules 04 and 19).** Section 461(l) has no effect on self-employment tax, which is computed on net earnings from the trade or business itself without reference to this limitation.

**Real estate (Modules 20 to 23).** A real estate professional whose rental losses are non-passive reaches this gate with them, where an ordinary landlord's losses would have been suspended at gate 3. Non-passive treatment moves the loss forward through the ordering rather than releasing it outright.

### 8. Common Scenarios and Edge Cases

**The threshold fell for 2026.** This is the point most likely to be got wrong, because an indexed amount is expected to rise. Any plan built on the 2025 figure overstates the usable loss by $57,000, or $114,000 jointly.

**The limitation is aggregate.** A taxpayer with one profitable business and one loss-making business nets them before applying the threshold. Losses are not tested business by business.

**It is applied at the owner level.** A partnership does not compute it; each partner does, on their own aggregate position including everything else they own.

**The disallowed amount is not lost.** It becomes a net operating loss, and the only cost is timing — though the 80 percent limitation in the following year makes that timing cost larger than it first appears.

**Wages are not business income for this purpose.** They are the non-business income the limitation is designed to protect, so they do not enter the aggregate business income figure that offsets business deductions.

**The limitation is now permanent.** It had been scheduled to expire after 2028, and planning that assumed a return to unlimited loss usage after that date is no longer sound.

### 9. Planning Implications

Because the limitation is aggregate and annual, the timing of deductions across years matters more than their total. A taxpayer facing a loss well above the threshold gains nothing from accelerating further deductions into that year, and may gain from deferring them into a year when they can be used in full.

Bonus depreciation and cost segregation are the deductions most often accelerated into a single year, and they are the ones most likely to create an excess business loss that then sits deferred behind the 80 percent net operating loss limitation. Electing out of bonus depreciation for a class of property, or spreading a cost segregation study across entities and years, can produce a better result than the largest possible first-year deduction.

The 2026 reset should be reflected in any multi-year plan. The threshold is materially lower than it was, and the reduction is permanent rather than a one-year anomaly.

Where a taxpayer expects a large loss, generating business **income** in the same year — through a gain on the sale of business property, or by not deferring revenue — increases the aggregate business income figure and so increases the loss that can be used currently.

### 10. Data Tables for the Engine

| Constant | 2026 value | Indexed |
|---|---|---|
| Threshold, single and all others | $256,000 | Yes, § 461(l)(3)(C) |
| Threshold, married filing jointly | $512,000 | Yes |
| Threshold, 2025, for comparison | $313,000 / $626,000 | — |
| Disallowed amount | Becomes a net operating loss in the next year | Fixed |
| Position in the ordering | Fourth, after basis, at-risk and passive | Fixed |
| Expiry | None — permanent for years after 2026 | — |

### 11. References

[43] Internal Revenue Service, *Revenue Procedure 2025-32*, § 3.31. https://www.irs.gov/pub/irs-drop/rp-25-32.pdf

[44] One Big Beautiful Bill Act, P.L. 119-21, § 70601, amending IRC § 461(l)(1) and (3)(C). https://www.govinfo.gov/content/pkg/PLAW-119publ21/html/PLAW-119publ21.htm

[45] Internal Revenue Service, *Revenue Procedure 2024-40*, § 3.32, for the 2025 threshold. https://www.irs.gov/pub/irs-drop/rp-24-40.pdf

[46] 26 U.S.C. § 461(l). United States Code, Office of the Law Revision Counsel. https://www.govinfo.gov/app/collection/uscode

### 12. Status in This System

| Layer | Status |
|---|---|
| Projection engine | **Applied.** The threshold constants of $256,000 and $512,000 match Revenue Procedure 2025-32, and the engine's own source comment records that the figure is **down** from 2025 — the reset is recognised rather than assumed away. The limitation is applied as the fourth gate, after basis, at-risk and passive, which is the statutory order. The disallowed amount is added to the net operating loss carryforward rather than discarded, and the user is warned in the year it arises. |
| Backend (`tax-be`) | **Not applied.** `strategyPhaseMap.js` catalogues "Excess Business Loss Limitation Planning (§461(l))" as a named strategy, but no computation exists. |
| Known limitations | The threshold is inflated forward by the engine's general inflation factor rather than by the § 461(l)(3)(C) mechanism, so projected thresholds drift from the published series in later years. Wages are not expressly excluded from the aggregate business income figure, and the special treatment of capital gains and losses within the § 461(l) computation is not modelled. Form 461 reporting is outside the scope of a projection. |


---

## Module 19 — Self-Employment Income and Business Deductions

**Tax year:** 2026 · **As of:** September 2026 · **Primary authority:** IRC §§ 162, 179, 1402

---

### 1. Overview and Purpose

Module 04 sets out how self-employment tax is computed once net earnings are known. This module deals with the step before it: how net earnings are arrived at, which deductions reduce them, and how the choice of entity changes the answer.

The distinction matters because the two figures behave differently. A deduction that reduces net earnings from self-employment reduces **both** income tax and self-employment tax, at a combined marginal cost that can exceed 45 percent. A deduction taken further down the return — a retirement plan contribution by a sole proprietor, or the § 199A deduction — reduces income tax only. Treating the two as equivalent overstates the value of the second by roughly fifteen percentage points.

For an owner-operated business the largest single decision is not which expenses to claim but how the business is structured. A sole proprietorship exposes the whole of the return to self-employment tax up to the contribution base and to the Medicare components without limit. An S corporation exposes only reasonable compensation. Module 04 quantifies the difference; this module sets out what the return consists of before that choice is applied.

### 2. Governing Law and Authorities

| Type | Citation | What it establishes |
|---|---|---|
| Statute | IRC § 162(a) | Ordinary and necessary business expenses |
| Statute | IRC § 195 | Start-up expenditures |
| Statute | IRC § 179 | Election to expense depreciable property |
| Statute | IRC § 274(n) | Fifty percent limitation on meals |
| Statute | IRC § 280A(c) | Business use of a home |
| Statute | IRC § 1402(a) | Net earnings from self-employment |
| Statute | IRC § 1402(a)(1) | Exclusion of rentals from real estate |
| Statute | IRC § 1402(a)(12) | The 92.35 percent factor |
| Statute | IRC § 1402(b)(2) | The $400 floor |
| Regulation | Treas. Reg. § 1.62-2 | Accountable plans |
| Guidance | Rev. Proc. 2025-32, § 3.24 | 2026 § 179 amounts |

### 3. Key Definitions

| Term | Definition |
|---|---|
| **Trade or business** | An activity carried on for profit with continuity and regularity, within the meaning of § 162. |
| **Ordinary and necessary** | Ordinary means common and accepted in the taxpayer's field; necessary means helpful and appropriate. Neither requires that the expense be indispensable. |
| **Net earnings from self-employment** | Net profit from the trade or business, adjusted under § 1402(a), then multiplied by 92.35 percent. |
| **Accountable plan** | An arrangement under Treas. Reg. § 1.62-2 under which an employer reimburses substantiated business expenses without the reimbursement being wages. |
| **§ 179 property** | Tangible depreciable property acquired for use in an active trade or business, which may be expensed in the year placed in service rather than depreciated. |

### 4. Who Is Affected

Sole proprietors filing Schedule C, general partners on their distributive share, and members of limited liability companies treated as partnerships or disregarded entities. S corporation shareholders are outside self-employment tax on their distributive share but are subject to employment tax on wages the corporation pays them.

Rentals from real estate are excluded from net earnings by § 1402(a)(1) unless the taxpayer is a dealer or provides substantial services beyond those customary for occupancy. A landlord therefore pays no self-employment tax on rents, and a short-term rental operator providing hotel-like services may.

### 5. Core Rules and Calculations

#### 5.1 Case Register

| # | Case | Applied |
|---|---|---|
| 1 | Net profit as the starting point | Yes — taken as an input |
| 2 | § 1402(a)(12) factor of 92.35 percent | Yes |
| 3 | § 1402(b)(2) $400 floor | **No** |
| 4 | § 1402(a)(1) exclusion of real estate rents | Yes, in effect — rents are modelled separately |
| 5 | § 162 ordinary and necessary expenses | Taken as an input, not itemised |
| 6 | § 179 expensing election | Constants held; applied only to real property components |
| 7 | § 179 phase-out above the investment ceiling | **No** |
| 8 | § 179 sport utility vehicle cap | **No** |
| 9 | § 179 taxable income limitation | **No** |
| 10 | § 274(n) fifty percent limitation on meals | **No** |
| 11 | § 280A(c) business use of a home | **No** |
| 12 | Accountable plan reimbursements | **No** |
| 13 | § 195 start-up expenditure amortisation | **No** |
| 14 | Reasonable compensation for an S corporation shareholder | **No** |
| 15 | § 164(f) deduction for half the self-employment tax | Yes — Module 04 |
| 16 | Interaction with § 199A | Partially |

#### 5.2 From gross receipts to net earnings

```
Gross receipts
  − cost of goods sold
  − ordinary and necessary business expenses under § 162
  − depreciation, including any § 179 election and bonus depreciation
                                                    = net profit

net profit × 0.9235                                 = net earnings from self-employment
   if under $400 → no self-employment tax at all      § 1402(b)(2)
```

The 92.35 percent factor is applied after every business deduction and before the rates. It is not itself a deduction and does not appear on the return as one.

#### 5.3 The deduction stack, and where each one bites

The order in which deductions reduce different taxes is the single most useful thing to understand about a self-employed return.

| Deduction | Reduces net earnings? | Reduces income tax? | Reduces QBI? |
|---|---|---|---|
| Ordinary business expenses, § 162 | **Yes** | Yes | Yes |
| Depreciation and § 179 | **Yes** | Yes | Yes |
| Home office, § 280A(c) | **Yes** | Yes | Yes |
| One half of self-employment tax, § 164(f) | No | Yes | Yes |
| Self-employed health insurance, § 162(l) | No | Yes | No |
| Retirement plan contribution for the owner | No | Yes | Yes |
| § 199A deduction | No | Yes | — |

The first three reduce a combined rate that includes self-employment tax. The remainder reduce income tax only. A $10,000 business expense and a $10,000 retirement contribution are not equivalent, and at a 24 percent marginal rate the difference is roughly $1,500 a year.

#### 5.4 Section 179 — 2026 amounts

| Item | 2026 amount |
|---|---|
| Maximum expensed | **$2,560,000** |
| Investment ceiling before phase-out | **$4,090,000** |
| Sport utility vehicle cap | **$32,000** |

The maximum is reduced dollar for dollar by the cost of § 179 property placed in service above $4,090,000, and is eliminated once placements reach $6,650,000.[47]

Two further limitations apply. The deduction cannot exceed the aggregate taxable income from the active conduct of trades or businesses, with the disallowed amount carried forward indefinitely. And a sport utility vehicle over 6,000 pounds gross vehicle weight is separately capped at $32,000.

Section 179 differs from bonus depreciation in a way that matters here: § 179 is limited by business taxable income and cannot create a loss, while bonus depreciation can. For a taxpayer already facing the excess business loss limitation of Module 18, that distinction determines whether an accelerated deduction is usable at all.

#### 5.5 Expenses that are commonly got wrong

**Meals.** Deductible at 50 percent under § 274(n). Entertainment has been wholly non-deductible since 2018. The One Big Beautiful Bill Act added a narrow exception at § 70305 for meals provided on fishing vessels and at certain northern fish processing facilities, which does not affect the general rule.

**Home office.** Available under § 280A(c) where a part of the home is used regularly and exclusively as the principal place of business or to meet clients. The exclusivity requirement is strict — a room used partly for personal purposes fails entirely. A simplified method allows $5 per square foot up to 300 square feet, capped at $1,500, without substantiating actual costs.

**Vehicle.** Either actual costs apportioned by business use, or the standard mileage rate. The method chosen in the first year the vehicle is placed in service constrains what may be used later.

**Start-up costs.** Section 195 allows up to $5,000 deducted in the first year, reduced dollar for dollar above $50,000 of start-up expenditure, with the balance amortised over 180 months.

**Accountable plans.** Where a business reimburses an owner-employee for substantiated expenses under Treas. Reg. § 1.62-2, the reimbursement is deductible by the business and is not wages. Without such a plan the reimbursement is compensation, taxable to the recipient and subject to employment tax. This is the mechanism by which an S corporation owner recovers home office and vehicle costs, since employee business expenses are otherwise non-deductible.

### 6. Examples and Case Calculations

#### Example 1 — From receipts to net earnings

A consultant, single, with $420,000 of gross receipts.

```
Gross receipts                                     420,000
Ordinary and necessary expenses                   −110,000
Depreciation                                       −18,000
                                                   -------
Net profit                                         292,000

× 0.9235                                           269,662  net earnings

Old-age component  12.4% × min(269,662, 184,500)    22,878
Hospital component 2.9% × 269,662                    7,820
Additional Medicare 0.9% × (269,662 − 200,000)         627
                                                   -------
Self-employment tax                                $31,325

§ 164(f) deduction  0.5 × (22,878 + 7,820)         $15,349
```

#### Example 2 — A business expense against a retirement contribution

The same consultant, marginal income tax rate 32 percent, considering $20,000 of additional spending.

```
As a business expense
   reduces net profit by 20,000
   self-employment tax saved   ≈ 0.9235 × 20,000 × 2.9%   =    536
      (above the contribution base, so only the Medicare components)
      plus additional Medicare 0.9%                        =    166
   income tax saved            0.32 × (20,000 − 351)       =  6,288
                                                              ------
                                                              $6,990

As a retirement plan contribution
   no reduction in self-employment tax                          0
   income tax saved            0.32 × 20,000                =  6,400
                                                              ------
                                                              $6,400
```

The business expense is worth about $590 more, because it reduces a base the retirement contribution does not reach. Below the contribution base the gap is far wider, because the old-age component of 12.4 percent is also in play.

#### Example 3 — Section 179 against the taxable income limitation

A business with $180,000 of taxable income before depreciation places $400,000 of equipment in service.

```
§ 179 election claimed                              400,000
Limited to business taxable income                  180,000
Disallowed, carried forward indefinitely            220,000
```

Bonus depreciation is not subject to this limitation and would have created a loss of $220,000, which would then be tested under § 461(l) in Module 18. Which route is better depends on whether the taxpayer has other income against which a loss could be used.

#### Example 4 — Entity choice at the same economic return

Business producing $300,000 of profit for its owner, married filing jointly. This restates Module 04's comparison from the deduction side.

| | Sole proprietorship | S corporation, $120,000 salary |
|---|---|---|
| Base for old-age tax | $184,500 (capped) | $120,000 |
| Old-age tax | $22,878 | $14,880 |
| Hospital insurance | $8,034 | $3,480 |
| **Employment tax total** | **$30,912** | **$18,360** |
| Qualified business income | $284,651 | $180,000 |
| W-2 wages for § 199A | $0 | $120,000 |

The S corporation saves $12,552 of employment tax and simultaneously creates the W-2 wages that the § 199A wage limitation requires above the threshold. The salary must be reasonable for the services performed, and it reduces qualified business income by the same amount.

### 7. Interactions with Other Rules

**Self-employment tax (Module 04).** This module produces the net earnings figure that Module 04 taxes.

**Qualified business income (Module 17).** Business deductions reduce qualified business income as well as net earnings. For an S corporation owner above the § 199A threshold, salary reduces qualified business income while creating the W-2 wages the limitation needs — there is an optimum, and it is not at either extreme.

**Excess business loss (Module 18).** An accelerated deduction that creates a large loss meets the § 461(l) threshold. Section 179 cannot create a loss; bonus depreciation can.

**Depreciation and cost segregation (Module 22).** The § 179 election and bonus depreciation interact with the recovery periods treated there.

**Retirement plans (Module 07).** A contribution for the owner reduces income tax but not self-employment tax, and the deduction is computed on net earnings **after** the § 164(f) deduction, which makes the effective contribution rate for a sole proprietor lower than the headline percentage.

**Real estate (Modules 20 to 23).** Rents are excluded from net earnings by § 1402(a)(1) unless substantial services are provided.

### 8. Common Scenarios and Edge Cases

**A deduction against net earnings is worth more than a deduction against income alone.** The gap is the self-employment tax rate that applies at that income level — 15.3 percent below the contribution base, 2.9 or 3.8 percent above it.

**The $400 floor is a cliff.** At $399 of net earnings there is no self-employment tax; at $401 the whole amount is subject to it.

**Entertainment is not deductible at all.** Meals remain deductible at 50 percent, and the distinction between a meal and entertainment is now consequential rather than academic.

**The home office exclusivity test admits no partial use.** A room used for personal purposes at any point in the year fails, and the simplified $5 per square foot method does not relax it.

**Section 179 cannot create a loss.** The taxable income limitation defers the excess indefinitely. Bonus depreciation can create a loss and then meets § 461(l) instead.

**Rentals are outside self-employment tax.** This is a different question from whether the activity is passive under § 469, and the two classifications need not agree.

**Reasonable compensation is the constraint on the S corporation saving.** The saving in Example 4 is real, and it is also the position most frequently examined.

**An S corporation owner has no deduction for unreimbursed expenses.** Employee business expenses are non-deductible, so an accountable plan is the only route.

### 9. Planning Implications

The first question for an owner-operated business is entity form, and the answer turns on the size of the return relative to reasonable compensation. Example 4 gives the shape of it; the interaction with § 199A in Module 17 usually reinforces the same answer above the threshold.

Where a deduction is discretionary in timing, taking it against net earnings in a year of high self-employment income is worth more than taking it in a year when the taxpayer is already above the contribution base and the marginal employment tax rate has fallen to 2.9 or 3.8 percent.

For a business with large equipment purchases, the choice between § 179 and bonus depreciation should be made by reference to Module 18 rather than to the size of the first-year deduction. The largest available deduction is not the best one where it creates a loss that will sit behind the excess business loss threshold and then the 80 percent net operating loss limitation.

An accountable plan should be in place for any S corporation with an owner-employee incurring business costs personally. Without it the costs are simply not deductible by anyone.

### 10. Data Tables for the Engine

| Constant | 2026 value | Indexed |
|---|---|---|
| § 1402(a)(12) factor | 0.9235 | Fixed |
| § 1402(b)(2) floor | $400 | Fixed |
| § 179 maximum | $2,560,000 | Yes |
| § 179 investment ceiling | $4,090,000 | Yes |
| § 179 sport utility vehicle cap | $32,000 | Yes |
| § 179 fully eliminated at | $6,650,000 of placements | Derived |
| § 274(n) meals | 50% deductible | Fixed |
| Entertainment | Not deductible | Fixed |
| Home office simplified method | $5 per square foot, 300 square feet, $1,500 cap | Fixed |
| § 195 start-up | $5,000, reduced above $50,000; balance over 180 months | Fixed |

### 11. References

[47] Internal Revenue Service, *Revenue Procedure 2025-32*, § 3.24. https://www.irs.gov/pub/irs-drop/rp-25-32.pdf

[11] 26 U.S.C. § 1402. United States Code, Office of the Law Revision Counsel. https://www.govinfo.gov/app/collection/uscode

[48] 26 U.S.C. §§ 162, 179, 195, 274 and 280A. https://www.govinfo.gov/app/collection/uscode

[49] Treas. Reg. § 1.62-2, *Reimbursements and other expense allowance arrangements*. https://www.ecfr.gov/current/title-26

### 12. Status in This System

| Layer | Status |
|---|---|
| Projection engine | **Applied in part.** Net profit is taken as an input rather than built from receipts and expenses, which is appropriate for a projection. The § 1402(a)(12) factor is applied correctly before the rates, the § 164(f) deduction is taken at one half and computed before adjusted gross income, and rental income is correctly kept outside net earnings from self-employment. The § 179 constants of $2,560,000 and $4,090,000 match Revenue Procedure 2025-32. |
| Backend (`tax-be`) | **Not applied**, though `strategyPhaseMap.js` catalogues several strategies in this area — the accountable plan under Reg. § 1.62-2, the home office deduction, business use of a personal vehicle, business travel, and hiring a spouse or children. None is computed. |
| Known limitations | The $400 floor in § 1402(b)(2) is not applied. The § 179 election is used only for real property components in the cost segregation path; there is no general § 179 election, no investment-ceiling phase-out above $4,090,000, no sport utility vehicle cap, and no taxable income limitation — which matters because that limitation is the principal difference between § 179 and bonus depreciation when a taxpayer is near the excess business loss threshold. The § 274(n) meals limitation, the § 280A(c) home office deduction, § 195 start-up amortisation and accountable plan reimbursements are not modelled; business expenses enter as a single input figure. Reasonable compensation for an S corporation shareholder is not tested, so the wage-versus-distribution split is accepted as entered and the engine cannot flag an unsustainable position. |


---

## Module 20 — Personal Use and Vacation Homes

**Tax year:** 2026 · **As of:** September 2026 · **Primary authority:** IRC § 280A

---

### 1. Overview and Purpose

Section 280A denies deductions attributable to a dwelling unit that the taxpayer uses as a residence. Where a property is both let and personally used, it decides how much of the cost may be deducted at all, and it does so **before** any of the other loss limitations are considered.

This is the first of two gates a rental property passes through, and its position is what makes it consequential. A property caught by § 280A has its deductions capped at gross rental income, so it cannot produce a loss. Nothing is left for the passive activity rules of Module 25 to suspend, nothing reaches the at-risk rules, and nothing reaches the excess business loss limitation. Testing the passive rules first, as many models do, produces a suspended loss that the statute never allowed in the first place.

The section also contains the provision at § 280A(g) that permits a dwelling to be let for fewer than fifteen days a year with the income excluded from gross income entirely. It is commonly called the Augusta rule, and it is one of the few genuinely tax-free receipts in the Code.

### 2. Governing Law and Authorities

| Type | Citation | What it establishes |
|---|---|---|
| Statute | IRC § 280A(a) | General disallowance for a dwelling used as a residence |
| Statute | IRC § 280A(c)(1) | Business use of a home |
| Statute | IRC § 280A(c)(5) | Deductions capped at gross rental income, with carryforward |
| Statute | IRC § 280A(d)(1) | The fourteen-day and ten-percent test |
| Statute | IRC § 280A(d)(2) | What counts as personal use |
| Statute | IRC § 280A(d)(3) | Rental to a family member as a principal residence |
| Statute | IRC § 280A(e) | Allocation of expenses between rental and personal use |
| Statute | IRC § 280A(g) | Rental for fewer than fifteen days |
| Statute | IRC § 267(c)(4) | Definition of family for the personal use test |

### 3. Key Definitions

| Term | Definition |
|---|---|
| **Dwelling unit** | A house, apartment, condominium, mobile home, boat or similar property providing basic living accommodation. |
| **Used as a residence** | Personal use during the year exceeding the **greater** of 14 days or 10 percent of the days the unit is rented at a fair rental.[50] |
| **Personal use** | Use for any part of a day by the taxpayer, any co-owner, or a member of the family of either; use under a reciprocal arrangement; or use by anyone paying less than a fair rental. |
| **Family** | Under § 267(c)(4), brothers and sisters, spouse, ancestors and lineal descendants. Notably **not** cousins, nieces, nephews or in-laws. |
| **Fair rental** | The amount a person not having an interest in the unit would pay, on the facts and circumstances. |

### 4. Who Is Affected

Any individual or S corporation owning a dwelling unit that is both let and used personally. The test is applied unit by unit and year by year, so a property can be caught in one year and not the next.

Three categories of use are **not** personal use and are worth stating because each removes days from the numerator:

- A day on which the taxpayer works substantially full time on repairs and maintenance, even if family members are present and not working.
- A rental at a fair rental to any person, including a family member, who uses the unit as their **principal residence** under § 280A(d)(3).
- Use by an employee where § 119 applies.

### 5. Core Rules and Calculations

#### 5.1 Case Register

| # | Case | Applied |
|---|---|---|
| 1 | § 280A(d)(1) fourteen-day or ten-percent test | Yes |
| 2 | The threshold is the **greater** of the two | Yes |
| 3 | § 280A(d)(2)(A) use by the taxpayer, a co-owner or family | **No** — a single personal-use figure is entered |
| 4 | § 280A(d)(2)(B) reciprocal arrangements | **No** |
| 5 | § 280A(d)(2)(C) use at less than a fair rental | **No** |
| 6 | Repair and maintenance days excluded from personal use | **No** |
| 7 | § 280A(d)(3) rental to a family member as a principal residence | **No** |
| 8 | § 280A(e) allocation by rental days over total days used | **No** |
| 9 | § 280A(c)(5) deductions capped at gross rental income | Yes |
| 10 | Ordering of deductions within the cap | **No** |
| 11 | Carryforward of amounts disallowed by the cap | **No** |
| 12 | § 280A(g) rental for fewer than fifteen days | Yes |
| 13 | § 280A(c)(1) business use of a home | **No** — see Module 19 |
| 14 | Applied before the § 469 classification | Yes |

#### 5.2 The test

```
threshold = max( 14 days , 0.10 × days rented at a fair rental )

if personalUseDays > threshold
    the unit is "used as a residence"
    → deductions are capped at gross rental income, § 280A(c)(5)
```

A day on which the unit is used personally is **not** counted as a day rented at fair rental, so a mixed day reduces the denominator as well as raising the numerator.

| Personal days | Rental days | Threshold | Result |
|---|---|---|---|
| 10 | 200 | 20.0 | Not a residence |
| 20 | 200 | 20.0 | Not a residence — the test is *exceeds* |
| **21** | 200 | 20.0 | **Residence — deductions capped** |
| 13 | 50 | 14.0 | Not a residence |
| 20 | 300 | 30.0 | Not a residence |
| **31** | 300 | 30.0 | **Residence — deductions capped** |

Note the second row. Personal use exactly equal to the threshold does not trigger the section; it must be exceeded.

#### 5.3 Allocation — § 280A(e)

Where there is any personal use at all, whether or not the unit is a residence, expenses attributable to the rental are limited to the proportion:

```
rentalShare = daysRentedAtFairRental ÷ totalDaysUsed
```

The denominator is **days used**, not 365. Days the property sits empty and available are in neither figure. This is favourable to the taxpayer and is regularly got wrong by treating the year as the denominator.

```
Personal 30 days, rented 200 days, total days used 230
   rental share  200 ÷ 230 = 86.96%
   on $40,000 of whole-property expenses, $34,783 is allocable to rental
```

Deductions allowable regardless of rental use — qualified residence interest and property taxes — are excluded from this apportionment by § 280A(e)(2) and follow their own rules.

#### 5.4 The cap and its ordering — § 280A(c)(5)

Where the unit is a residence, deductions attributable to the rental use may not exceed gross rental income less the deductions allowable whether or not the unit was rented. In practice this produces a three-tier ordering:

| Tier | Category | Effect |
|---|---|---|
| 1 | Interest and taxes allocable to rental use | Allowed in full; reduces the room available |
| 2 | Operating expenses — insurance, utilities, repairs, management | Allowed to the extent of the remaining income |
| 3 | Depreciation | Allowed last, to the extent anything remains |

The result can never be a loss. Amounts disallowed carry forward to the succeeding year and are subject to the same limitation again, **whether or not** the unit is used as a residence in that later year.

```
Gross rental income                       45,000
Tier 1  interest and taxes                12,000    remaining  33,000
Tier 2  operating expenses  20,000        20,000    remaining  13,000
Tier 3  depreciation        18,000        13,000    remaining       0

Net rental result                              0
Carried forward: $5,000 of depreciation
```

Depreciation is deliberately last, so the deduction most likely to be deferred is the one that does not represent a cash outlay.

#### 5.5 The fifteen-day rule — § 280A(g)

Where a dwelling unit is used by the taxpayer as a residence **and** is actually rented for fewer than fifteen days in the year:

- no deduction attributable to the rental use is allowed, and
- **the income is not included in gross income at all**.[50]

Fourteen days is the maximum. On the fifteenth day the exclusion is lost entirely and the ordinary rules apply to the whole of the income.

```
14 days at $2,500 a day = $35,000 received, $0 taxable
15 days at $2,500 a day = $37,500 received, fully reportable
```

The rule applies to any dwelling the taxpayer uses as a residence, including a principal residence. Its common application is a closely held business renting the owner's home for meetings, board sessions or events: the business deducts a reasonable rent under § 162, and the owner excludes it under § 280A(g). The rent must be at a genuine fair rental supported by comparable evidence, and the business purpose must be real.

### 6. Examples and Case Calculations

#### Example 1 — A beach house just inside the line

Rented 200 days at a fair rental; the owner uses it 20 days.

```
Threshold  max(14, 20) = 20
Personal use 20 is not more than 20
→ not used as a residence
→ deductions are not capped; a loss may arise and passes to Module 25
Allocation  200 ÷ 220 = 90.9% of whole-property expenses
```

#### Example 2 — One day over

The same property, 21 days of personal use.

```
Threshold  max(14, 20) = 20
Personal use 21 exceeds 20
→ used as a residence
→ deductions capped at gross rental income; no loss possible
Allocation  200 ÷ 221 = 90.5%
```

A single additional day of personal use converts a property that could generate a deductible loss into one that cannot. Where a loss of $25,000 was expected, the whole of it is denied and the depreciation component carries forward.

#### Example 3 — A family member paying fair rent

The owner's daughter occupies the property for 120 days as her principal residence, paying a fair rental. The owner uses it 20 days.

```
§ 280A(d)(3)  the daughter's occupancy is not personal use
Rental days   200 + 120 = 320
Threshold     max(14, 32) = 32
Personal use  20, which does not exceed 32
→ not used as a residence
```

Had the daughter paid below a fair rental, or used it as a second home rather than a principal residence, all 120 days would have counted as personal use and the property would be capped.

#### Example 4 — The fifteen-day exclusion

An owner lets their principal residence for 14 days a year at $2,500 a day to their own S corporation for board meetings.

```
Rent received                              35,000
Included in the owner's gross income            0     § 280A(g)(2)
Deducted by the corporation under § 162    35,000
Rental deductions allowed to the owner          0     § 280A(g)(1)
```

The amount leaves the corporation deductibly and is never taxed to the owner. Documentation of the fair rental and of genuine business use is what the position rests on.

### 7. Interactions with Other Rules

**Passive activity losses (Module 25).** Section 280A is applied **first**. A property capped by § 280A cannot produce a loss, so nothing reaches § 469. Reversing the order creates a suspended loss that was never allowable.

**Short-term rentals (Module 21).** The seven-day average customer use test in the § 469 regulations is a different question from the § 280A personal use test, and a property can be caught by one and not the other. A short-term rental with heavy owner use is capped by § 280A regardless of how favourably § 469 would treat it.

**Depreciation (Module 22).** Depreciation is the last deduction in the § 280A ordering and the first to be deferred. Deferred depreciation still reduces basis in some readings, which affects gain on a later sale.

**Business use of a home (Module 19).** Section 280A(c)(1) governs the home office deduction and is subject to a parallel gross income limitation.

**Self-employment tax (Module 04).** Rents are outside net earnings from self-employment under § 1402(a)(1) unless substantial services are provided, whatever the § 280A outcome.

### 8. Common Scenarios and Edge Cases

**The threshold is the greater of the two figures, and it must be exceeded.** Personal use equal to the threshold does not trigger the section.

**A mixed day counts twice against the taxpayer.** It is a personal day and it is not a fair-rental day, so it raises the numerator and lowers the denominator of the ten percent test.

**Family is defined by § 267(c)(4).** Siblings, spouse, ancestors and lineal descendants. Cousins, nieces, nephews and in-laws are outside it, so their use at a fair rental is not personal use.

**Repair days do not count**, provided the taxpayer works substantially full time on the repairs. Other people being present and not working does not defeat this.

**The allocation denominator is days used, not days in the year.** Vacant days available for rent are in neither figure.

**Disallowed amounts carry forward and are tested again**, even in a year when the property is not a residence.

**Fourteen days is the maximum for the exclusion, not fifteen.** The statute says "fewer than 15 days".

**The fifteen-day rule requires the unit to be used as a residence.** A pure investment property that the owner never occupies cannot use it.

### 9. Planning Implications

For an owner whose personal use is near the threshold, the number of days is worth tracking deliberately. Example 2 shows a single day converting a deductible loss into a capped position, and the decision is entirely within the owner's control.

Where personal use is unavoidably high, the property should be modelled as incapable of producing a loss. Projecting a rental loss for a heavily used vacation home overstates the deduction in every year and misstates the carryforward.

The § 280A(g) exclusion is a small but reliable benefit for any client with a closely held business and a suitable home. It requires evidence of fair rental value and genuine business use, and it is capped at fourteen days.

Where a family member will occupy the property, structuring the arrangement as a principal residence at a fair rental removes those days from personal use entirely, which can keep the property outside the section.

### 10. Data Tables for the Engine

| Constant | Value | Source |
|---|---|---|
| Personal use day threshold | 14 days | § 280A(d)(1)(A) |
| Percentage alternative | 10% of fair-rental days | § 280A(d)(1)(B) |
| Test | Greater of the two, and must be exceeded | § 280A(d)(1) |
| De minimis rental period | Fewer than 15 days | § 280A(g) |
| Allocation denominator | Total days used, not 365 | § 280A(e)(1) |
| Deduction ordering | Interest and taxes, then operating, then depreciation | § 280A(c)(5) |
| Cap | Gross rental income; no loss permitted | § 280A(c)(5) |
| Carryforward | Indefinite, retested each year | § 280A(c)(5) |
| Family definition | § 267(c)(4) | Statute |

### 11. References

[50] 26 U.S.C. § 280A, *Disallowance of certain expenses in connection with business use of home, rental of vacation homes, etc.* United States Code, Office of the Law Revision Counsel. https://www.govinfo.gov/app/collection/uscode

[51] 26 U.S.C. § 267(c)(4). https://www.govinfo.gov/app/collection/uscode

[52] Internal Revenue Service, *Publication 527, Residential Rental Property*. https://www.irs.gov/pub/irs-pdf/p527.pdf

### 12. Status in This System

| Layer | Status |
|---|---|
| Projection engine | **Applied in part.** The § 280A(d)(1) test is implemented as the greater of 14 days and 10 percent of rental days, and it is correctly applied as a **pre-gate** — before the § 469 classification and before the four loss limitations — so a capped property does not generate a suspended loss it was never entitled to. The § 280A(g) fifteen-day exclusion is implemented, and a property meeting it is removed from the rental computation entirely. The gross income cap is applied so that a capped property cannot produce a loss. |
| Backend (`tax-be`) | **Not applied**, though `strategyPhaseMap.js` catalogues the Augusta rule at § 280A(g) as a named strategy and the repository contains a separate `augusta-rule` model and controller directory. No § 280A computation exists in the roadmap projection. |
| Known limitations | Personal use is entered as a single number of days rather than derived from the § 280A(d)(2) categories, so use by a co-owner, by family within § 267(c)(4), under a reciprocal arrangement, or at less than a fair rental is not separately identified. The exclusions that **reduce** personal use are correspondingly absent: repair and maintenance days, and the § 280A(d)(3) rule for a family member occupying at a fair rental as a principal residence. The § 280A(e) allocation by rental days over total days used is not performed, so whole-property expenses are not apportioned. Within the cap, the three-tier ordering is not applied and disallowed amounts are **not carried forward**, so a capped property loses the deferred depreciation permanently rather than deferring it. |


---

## Module 21 — Short-Term Rentals and the Seven-Day Rule

**Tax year:** 2026 · **As of:** September 2026 · **Primary authority:** IRC § 469; Treas. Reg. §§ 1.469-1T(e)(3), 1.469-5T

---

### 1. Overview and Purpose

Section 469(c)(2) treats any rental activity as **per se passive**, without regard to how much the owner does. A landlord who spends every weekend on the property is passive; the losses are suspended until there is passive income or a qualifying disposition.

The regulations then remove certain activities from the definition of "rental activity" altogether. Where the **average period of customer use is seven days or less**, the activity is not a rental activity for § 469 purposes, and the per se rule never applies.[53] What governs instead is the ordinary test for every other trade or business: does the taxpayer materially participate?

The consequence is the most useful structural position in the Code for a high-earning taxpayer with property. A short-term rental in which the owner materially participates produces a **non-passive** loss, deductible against wages and business income without the $25,000 allowance, without the $100,000 to $150,000 phase-out, and without needing real estate professional status under § 469(c)(7) — which requires 750 hours and more than half of all personal services, and is unavailable to anyone with a demanding full-time career.

The position is frequently described as a loophole. It is not: it is the plain operation of a regulation that has been in place since 1988. What makes it fragile is that it depends on two separate factual tests — the average period of customer use, and material participation — and taxpayers routinely document neither.

### 2. Governing Law and Authorities

| Type | Citation | What it establishes |
|---|---|---|
| Statute | IRC § 469(c)(1) | Passive activity means a trade or business in which the taxpayer does not materially participate |
| Statute | IRC § 469(c)(2) | Rental activity is per se passive |
| Statute | IRC § 469(c)(7) | Real estate professional exception |
| Statute | IRC § 469(h)(1) | Material participation means regular, continuous and substantial involvement |
| Regulation | Treas. Reg. § 1.469-1T(e)(3)(i) | Definition of rental activity |
| Regulation | Treas. Reg. § 1.469-1T(e)(3)(ii)(A) | The seven-day exception |
| Regulation | Treas. Reg. § 1.469-1T(e)(3)(ii)(B) | The thirty-day exception with significant personal services |
| Regulation | Treas. Reg. § 1.469-5T(a) | The seven material participation tests |
| Regulation | Treas. Reg. § 1.469-5T(f)(4) | Investor activity does not count |
| Statute | IRC § 1402(a)(1) | Rents excluded from self-employment income unless services are substantial |

### 3. Key Definitions

| Term | Definition |
|---|---|
| **Rental activity** | An activity where tangible property is used by customers and gross income is principally for the use of that property.[53] |
| **Average period of customer use** | Aggregate days of customer use divided by the number of periods of customer use, computed for the year and for each property or, where grouped, for the activity. |
| **Significant personal services** | Services performed by individuals in connection with making the property available, excluding services usually provided with long-term occupancy. |
| **Material participation** | Involvement in the operations on a basis that is regular, continuous and substantial, satisfied by meeting any one of seven regulatory tests. |
| **Real estate professional** | A taxpayer meeting the § 469(c)(7)(B) tests — more than half of personal services in real property trades or businesses **and** more than 750 hours. |

### 4. Who Is Affected

Any owner of property let for short periods — holiday lets, serviced apartments, and similar arrangements. The classification is made **activity by activity**, and grouping decisions can change the average.

The taxpayers for whom it matters most are those with high ordinary income and no route to real estate professional status: a physician, dentist, lawyer or executive whose employment consumes more than half their working time and so fails the § 469(c)(7)(B)(i) test by definition. For them the seven-day exception is the only path to a non-passive rental loss.

### 5. Core Rules and Calculations

#### 5.1 Case Register

| # | Case | Applied |
|---|---|---|
| 1 | § 469(c)(2) rental activity per se passive | Yes |
| 2 | § 1.469-1T(e)(3)(ii)(A) seven-day average | Yes |
| 3 | § 1.469-1T(e)(3)(ii)(B) thirty days with significant personal services | **No** |
| 4 | (C) extraordinary personal services | **No** |
| 5 | (D) rental incidental to a non-rental activity | **No** |
| 6 | (E) property available during defined business hours | **No** |
| 7 | (F) property provided to a partnership or S corporation activity | **No** |
| 8 | Material participation required once outside rental treatment | Yes — taken as an input |
| 9 | The seven § 1.469-5T(a) tests individually | **No** — a single yes or no is entered |
| 10 | § 1.469-5T(f)(4) investor time excluded | **No** |
| 11 | Participation of a spouse counted | **No** |
| 12 | § 469(c)(7) real estate professional status | Yes — taken as an input |
| 13 | Applied after the § 280A pre-gate | Yes |
| 14 | Grouping elections affecting the average | **No** |
| 15 | Self-employment tax where services are substantial | **No** |

#### 5.2 The order of the tests

```
1  § 280A personal use            → capped? then stop, no loss possible   Module 20
2  Is it a "rental activity"?     → average customer use ≤ 7 days?
       yes, ≤ 7 days   → NOT a rental activity; go to 3
       no              → rental activity; per se passive unless § 469(c)(7)
3  Material participation?        → § 1.469-5T(a), any one of seven tests
       yes  → NON-PASSIVE.  Loss deductible against ordinary income
       no   → passive.       Loss suspended
```

Step 1 comes first and is absolute. A short-term rental with personal use above the § 280A threshold is capped at gross rental income no matter how favourable steps 2 and 3 would have been.

#### 5.3 The average period of customer use

```
averagePeriod = total days of customer use ÷ number of separate rental periods
```

The computation is an average, not a maximum. A property let mostly for weekends but occasionally for a month can still average seven days or less.

| Bookings | Total days | Periods | Average | Rental activity? |
|---|---|---|---|---|
| 40 weekend lets of 3 days | 120 | 40 | 3.0 | **No** — outside § 469(c)(2) |
| 25 lets averaging a week | 175 | 25 | 7.0 | **No** — seven or less |
| 24 lets, 23 of 6 days and one of 40 | 178 | 24 | 7.4 | **Yes** — per se passive |
| 12 monthly lets | 360 | 12 | 30.0 | **Yes** |

The third row is the trap. A single long booking can lift the average above seven and convert the whole year's activity to per se passive. The test is applied to the year as a whole, not booking by booking.

The thirty-day alternative in (e)(3)(ii)(B) requires **significant personal services** in addition, and services usually provided with long-term occupancy — heat, light, cleaning of common areas, rubbish collection, routine repairs — are expressly excluded from counting.

#### 5.4 Material participation — the seven tests

Once the activity is outside rental treatment, § 1.469-5T(a) governs. Any **one** of these is sufficient:[54]

| # | Test |
|---|---|
| 1 | More than **500 hours** in the activity during the year |
| 2 | The individual's participation constitutes **substantially all** the participation of all individuals |
| 3 | More than **100 hours**, and not less than the participation of any other individual |
| 4 | The activity is a significant participation activity and aggregate participation in all such activities exceeds **500 hours** |
| 5 | Material participation in **any five of the ten** preceding taxable years |
| 6 | A personal service activity in which the individual materially participated for **any three** preceding years |
| 7 | On all the facts and circumstances, participation on a **regular, continuous and substantial** basis |

Test 3 is the one that usually carries a short-term rental. Where the owner does the bookings, guest communication, scheduling and coordination themselves and no single cleaner or manager spends more hours, 100 hours is achievable and the test is met.

Two limits matter. Section 1.469-5T(f)(4) excludes time spent in an **investor** capacity — studying financial statements, reviewing operations for one's own use, monitoring finances — unless the individual is involved in day-to-day management. And where a management company is engaged, its hours count as another individual's participation, which can defeat test 3 even where the owner exceeds 100 hours.

Participation of a **spouse** counts toward the taxpayer's own participation, whether or not they file jointly and whether or not the spouse has an interest in the activity.

#### 5.5 Why this beats real estate professional status

| | Seven-day short-term rental | Real estate professional, § 469(c)(7) |
|---|---|---|
| Hours required | 100, on test 3 | **750** in real property trades or businesses |
| Time relative to other work | No requirement | **More than half** of all personal services |
| Available to a full-time employee | **Yes** | Effectively no |
| Applies to long-term rentals | No | Yes |
| Material participation still required | Yes | Yes, per property unless aggregated |

A physician working 2,000 hours a year cannot satisfy the more-than-half test under any circumstances, so real estate professional status is closed. The seven-day route is open because it asks only for material participation in the activity itself.

#### 5.6 What the classification is worth

A non-passive loss is deductible against wages and business income in the year it arises, subject only to the at-risk rules and the excess business loss limitation. A passive loss is suspended.

| | Passive | Non-passive |
|---|---|---|
| Deductible against wages | No | **Yes** |
| $25,000 allowance | Available, phasing out from $100,000 of modified adjusted gross income | Not needed |
| Phased out entirely at | $150,000 | — |
| Released on disposition | Yes, § 469(g) | Not applicable |
| Reaches the § 461(l) gate | Only when released | **Yes, currently** |

For a taxpayer with $500,000 of wages the $25,000 allowance is fully phased out and worth nothing, so the difference between passive and non-passive is the entire loss.

### 6. Examples and Case Calculations

#### Example 1 — The classification decides everything

A surgeon with $600,000 of wages buys a holiday property. Average customer use is 4.2 days. Cost segregation and bonus depreciation produce a first-year loss of $180,000. Personal use is 8 days against 190 rental days.

```
§ 280A  threshold max(14, 19) = 19; personal use 8 → not a residence, no cap

Average customer use 4.2 days → not a rental activity

Material participation, test 3
   owner hours 140, largest other individual 95 → satisfied

Loss is NON-PASSIVE
   deductible against wages                          180,000
   tax saved at 37 percent                           $66,600
```

Had the average been 7.4 days, the activity would have been per se passive, the $25,000 allowance would have been fully phased out at $600,000 of income, and the entire $180,000 would have been suspended — a difference of $66,600 in the first year.

#### Example 2 — One long booking

The same property, but one guest takes a 40-day winter let.

```
Bookings   23 lets of 6 days = 138 days, plus one of 40 days
Total      178 days over 24 periods
Average    7.42 days → exceeds seven

→ rental activity → per se passive → loss suspended
```

Declining the long booking, or splitting it into separate contracted periods with genuine gaps, preserves the classification. The revenue forgone is trivial against $66,600 of tax.

#### Example 3 — A management company defeating test 3

The same property, let through an agency that handles bookings, cleaning and guest contact. The owner spends 120 hours; the agency's staff spend 400.

```
Test 1  500 hours              — not met, 120
Test 3  100 hours and not less than any other individual
        — 120 hours, but agency staff exceed it → not met
Test 4  significant participation activities        — no others
Test 7  facts and circumstances                     — weak on these facts

→ no material participation → passive despite the seven-day average
```

The seven-day test and the material participation test are independent, and satisfying the first achieves nothing on its own. This is the most common failure in practice.

#### Example 4 — Documentation

The two tests rest on contemporaneous records:

| Test | Evidence |
|---|---|
| Average period of customer use | The booking platform's reservation report, showing each period |
| Material participation | A contemporaneous log of dates, hours and tasks, excluding investor activity |

A log reconstructed after an enquiry begins is worth very little. The regulation permits reasonable means of proof, but a narrative summary written years later has repeatedly failed in litigation.

### 7. Interactions with Other Rules

**Personal use (Module 20).** Section 280A is tested first and is absolute. A capped property produces no loss whatever its § 469 classification.

**Passive activity losses (Module 25).** Where the seven-day test is failed, the activity is a rental activity and the per se rule applies. Module 25 treats the $25,000 allowance, its phase-out, and the release of suspended losses on disposition.

**Depreciation and cost segregation (Module 22).** The loss that makes the classification worth pursuing is usually created by a cost segregation study and bonus depreciation. The two modules are used together.

**At-risk rules (Module 23).** A non-passive loss must still clear the § 465 at-risk limitation, which for real estate turns on qualified nonrecourse financing.

**Excess business loss (Module 18).** A non-passive loss reaches the § 461(l) gate in the year it arises. At $256,000 or $512,000 the threshold is often the binding constraint on a large first-year loss.

**Self-employment tax (Modules 04 and 19).** Rents are outside net earnings under § 1402(a)(1) unless substantial services are provided. A short-term rental with hotel-like services can fall inside it, which converts a tax saving into a tax cost. The § 469 and § 1402 questions are separate and can be answered differently.

**Qualified business income (Module 17).** A short-term rental rising to a trade or business may generate qualified business income, and the 2.5 percent of unadjusted basis alternative is designed for exactly this kind of low-payroll, property-heavy activity.

### 8. Common Scenarios and Edge Cases

**The seven-day test is an average, not a maximum.** Occasional longer lets are survivable; one very long let may not be.

**Failing the average converts the whole year**, not merely the long booking.

**Satisfying the seven-day test achieves nothing on its own.** Material participation is a separate requirement and is where most positions fail.

**A management company is another individual's participation.** It can defeat test 3 even where the owner is genuinely involved.

**Investor time does not count.** Reviewing statements and monitoring performance are excluded by § 1.469-5T(f)(4).

**A spouse's hours count** toward the taxpayer's participation.

**Grouping changes the average.** Where several properties are grouped as one activity, the average is computed across the activity. Grouping a long-term let with short-term lets can destroy the classification for all of them.

**Substantial services can create self-employment tax.** Daily cleaning, meals and concierge services move the activity toward a hotel, and § 1402(a)(1) then applies at 15.3 percent on income the owner expected to be rent.

**The position is not a loophole and is not aggressive**, but it is factual, and facts must be documented as they occur.

### 9. Planning Implications

The decision to pursue this position should be made **before** the property is bought and let, not at the return. Both tests depend on how the property is operated through the year, and neither can be created retrospectively.

Where the classification is intended, three operating choices follow: set a maximum booking length that protects the average, keep enough of the work in-house that no single other individual exceeds the owner's hours, and keep a contemporaneous log from the first day.

The value is greatest in the first year, when cost segregation and bonus depreciation concentrate the deduction. It is also the year in which the excess business loss threshold in Module 18 is most likely to bind, and at $256,000 or $512,000 that constraint should be modelled alongside the classification rather than after it.

For a taxpayer whose income makes the $25,000 allowance worthless — anyone above $150,000 of modified adjusted gross income — the classification is the difference between a fully deductible loss and a fully suspended one. There is no middle outcome.

Where the owner cannot commit to the operating involvement, the honest answer is that the loss will be suspended, and the property should be evaluated on that basis rather than on a classification the facts will not support.

### 10. Data Tables for the Engine

| Constant | Value | Source |
|---|---|---|
| Seven-day average threshold | 7 days or less | § 1.469-1T(e)(3)(ii)(A) |
| Thirty-day alternative | 30 days or less with significant personal services | (e)(3)(ii)(B) |
| Material participation, hours test | 500 hours | § 1.469-5T(a)(1) |
| Material participation, comparative test | 100 hours and not less than any other individual | § 1.469-5T(a)(3) |
| Significant participation aggregate | 500 hours across such activities | § 1.469-5T(a)(4) |
| Prior-year tests | 5 of 10 years; 3 years for personal service activities | § 1.469-5T(a)(5), (6) |
| Real estate professional | 750 hours and more than half of personal services | § 469(c)(7)(B) |
| Investor time | Excluded | § 1.469-5T(f)(4) |
| Spouse's participation | Counted | § 469(h)(5) |

### 11. References

[53] Treas. Reg. § 1.469-1T(e)(3), *Rental activity*. Electronic Code of Federal Regulations. https://www.ecfr.gov/current/title-26/chapter-I/subchapter-A/part-1/section-1.469-1T

[54] Treas. Reg. § 1.469-5T, *Material participation*. https://www.ecfr.gov/current/title-26

[55] 26 U.S.C. § 469. United States Code, Office of the Law Revision Counsel. https://www.govinfo.gov/app/collection/uscode

### 12. Status in This System

| Layer | Status |
|---|---|
| Projection engine | **Applied.** The classification runs in the correct order: § 280A is tested first as a pre-gate, then the seven-day average determines whether the activity is a rental activity, then material participation determines whether the loss is passive or non-passive. A non-passive loss is routed to the at-risk and excess business loss gates rather than into the passive pool, which is the behaviour the whole position depends on. Real estate professional status is available as a separate input and correctly reaches long-term rentals that the seven-day test does not. |
| Backend (`tax-be`) | **Not applied.** `strategyPhaseMap.js` catalogues "Real Estate Professional Status (IRC §469)" and "§469 Passive Activity Loss Release Strategy" as named strategies, but no classification logic exists. |
| Known limitations | The average period of customer use is entered as a figure rather than computed from booking data, so the engine cannot show a single long booking lifting the average above seven — the failure mode in Example 2. Material participation is entered as a yes or no rather than derived from the seven tests, so the engine cannot distinguish a position resting on the 500-hour test from one resting on the more fragile 100-hour comparative test, and cannot warn where a management company's hours would defeat it. Investor time is not excluded and a spouse's participation is not separately tracked. Only exception (A) of the six in § 1.469-1T(e)(3)(ii) is implemented; the thirty-day alternative with significant personal services and the four remaining exceptions are absent. Grouping elections are not modelled, so the effect of grouping a long-term let with short-term lets on the average cannot be shown. The § 1402(a)(1) substantial services question is not evaluated, so a short-term rental is never brought into self-employment tax. |


---

## Module 22 — Depreciation, Cost Segregation and Recapture

**Tax year:** 2026 · **As of:** September 2026 · **Primary authority:** IRC §§ 167, 168, 1245, 1250

---

### 1. Overview and Purpose

Depreciation is a deduction for the exhaustion of property used in a trade or business or held for the production of income. For real property it is the largest deduction most owners ever claim, and it is the reason a property producing positive cash can still show a tax loss.

Three features drive the planning. Recovery periods are long for buildings — 27.5 years for residential rental property and 39 for non-residential — but much shorter for the components inside them. A **cost segregation** study identifies those components and reclassifies them to five, seven or fifteen year property. Once reclassified they qualify for **bonus depreciation** under § 168(k), which the One Big Beautiful Bill Act restored to **100 percent** and made permanent for property acquired after 19 January 2025.[56]

The deduction is not free. Depreciation reduces basis, and on sale the reduction comes back. Personal property is recaptured as **ordinary income** under § 1245 to the full extent of depreciation taken. Real property is recaptured as **unrecaptured section 1250 gain**, taxed at up to 25 percent. Cost segregation therefore does not eliminate tax; it converts a deduction now into a recapture later, and moves part of that recapture from the 25 percent bucket into the ordinary bucket.

This module also records the most serious defect found in this system. **The engine computes no gain, no recapture, no tax and no proceeds when a property is sold.** The detail is at § 12 and in Appendix B as D18.

### 2. Governing Law and Authorities

| Type | Citation | What it establishes |
|---|---|---|
| Statute | IRC § 167 | Depreciation allowance |
| Statute | IRC § 168(c) | Applicable recovery periods |
| Statute | IRC § 168(d) | Conventions — half-year, mid-quarter, mid-month |
| Statute | IRC § 168(e) | Classification of property |
| Statute | IRC § 168(k) | Additional first-year depreciation |
| Statute | IRC § 179 | Election to expense — Module 19 |
| Statute | IRC § 280F | Limitation for passenger automobiles |
| Statute | IRC § 1245 | Recapture on depreciable personal property |
| Statute | IRC § 1250 | Recapture on depreciable real property |
| Statute | IRC § 1(h)(1)(E) | Unrecaptured section 1250 gain taxed at up to 25 percent |
| Statute | IRC § 1016(a)(2) | Basis reduced by depreciation allowed **or allowable** |
| Legislation | P.L. 119-21, § 70301 | 100 percent bonus depreciation, made permanent |
| Guidance | IRS Publication 946 | How to depreciate property |

### 3. Key Definitions

| Term | Definition |
|---|---|
| **Recovery period** | The number of years over which the cost is recovered, set by § 168(c) according to the property's class. |
| **Cost segregation** | An engineering-based analysis allocating the purchase price of a building among land, structural components, land improvements and tangible personal property. |
| **Bonus depreciation** | Additional first-year depreciation under § 168(k), now 100 percent of the adjusted basis of qualified property. |
| **Qualified property** | Generally property with a recovery period of 20 years or less. Buildings themselves do not qualify; components reclassified to shorter lives do. |
| **Unrecaptured section 1250 gain** | Gain on real property attributable to depreciation, taxed at a maximum of 25 percent rather than the ordinary long-term rate. |
| **Allowed or allowable** | Basis is reduced by depreciation actually taken **or** by the amount that could have been taken, whichever is greater. Failing to claim depreciation does not preserve basis. |

### 4. Who Is Affected

Any owner of depreciable property used in a trade or business or held for the production of income. Land is never depreciable, so the first step in any analysis is separating land from improvements.

Cost segregation is worth its cost on properties above roughly $500,000 of improvement value, and its value is greatest where the owner can use the resulting loss — which returns to the classification question in Modules 20, 21 and 25. A large first-year deduction that is suspended as a passive loss is worth very little in the year it arises.

### 5. Core Rules and Calculations

#### 5.1 Case Register

| # | Case | Applied |
|---|---|---|
| 1 | Residential rental 27.5-year recovery | Yes |
| 2 | Non-residential 39-year recovery | Yes |
| 3 | Land improvements, 15 years | Yes |
| 4 | Tangible personal property, 5 and 7 years | Yes — as a cost segregation input |
| 5 | Land not depreciable | Yes |
| 6 | Mid-month convention for real property | **No** — a full year is taken |
| 7 | Half-year and mid-quarter conventions for personal property | **No** |
| 8 | Straight line for real property | Yes |
| 9 | Declining balance for personal property | **No** — irrelevant where bonus is 100 percent |
| 10 | § 168(k) bonus depreciation at 100 percent | Yes |
| 11 | Bonus permanent for property acquired after 19 January 2025 | Yes |
| 12 | Election out of bonus by class | **No** |
| 13 | Cost segregation allocation to 5 and 15 year components | Yes |
| 14 | § 280F passenger automobile limits | **No** |
| 15 | Basis reduced by depreciation allowed or allowable | Partially — accumulated but never used |
| 16 | § 1245 recapture as ordinary income | **No** — D18 |
| 17 | Unrecaptured § 1250 gain at 25 percent | **No** — D17 and D18 |
| 18 | Gain computed on disposition | **No** — D18 |
| 19 | Sale proceeds credited to the balance sheet | **No** — D18 |
| 20 | § 1031 like-kind exchange deferral | **No** |
| 21 | Depreciation ceasing at the end of the recovery period | Yes |

#### 5.2 Recovery periods and conventions

| Property | Recovery period | Method | Convention |
|---|---|---|---|
| Residential rental building | **27.5 years** | Straight line | Mid-month |
| Non-residential real property | **39 years** | Straight line | Mid-month |
| Land improvements — paving, fencing, landscaping | **15 years** | 150% declining balance | Half-year or mid-quarter |
| Tangible personal property — carpet, cabinetry, specialty electrics | **5 or 7 years** | 200% declining balance | Half-year or mid-quarter |
| Land | Not depreciable | — | — |

The mid-month convention treats real property as placed in service in the middle of the month, so a property acquired in December yields half a month of depreciation in year one, not a full year.

#### 5.3 Cost segregation

A cost segregation study allocates the acquisition cost among asset classes on engineering evidence rather than treating the whole building as a single 27.5 or 39 year asset. Typical allocations for a residential property run to 20 to 30 percent across the shorter classes, though the figure is entirely property-specific and a study that produces a standard percentage regardless of the building is not evidence.

```
Purchase price                          2,000,000
Land, not depreciable                    −400,000
                                        ---------
Depreciable improvements                1,600,000

Without cost segregation
   1,600,000 ÷ 27.5                    =    58,182  a year

With cost segregation
   5-year personal property   15%          240,000  → bonus at 100%
   15-year land improvements  10%          160,000  → bonus at 100%
   27.5-year structure        75%        1,200,000  → 43,636 a year
                                         ---------
   First-year depreciation               443,636
```

The first-year deduction rises from $58,182 to $443,636. What has happened is a timing shift: the same $1,600,000 is recovered either way, and the difference is when.

#### 5.4 Bonus depreciation after the 2025 Act

Section 168(k) allows an additional first-year deduction equal to **100 percent** of the adjusted basis of qualified property. The One Big Beautiful Bill Act struck the phase-down schedule and the expiry, so the deduction is permanent rather than stepping down to 40 and 20 percent as it would otherwise have done.[56]

The change applies to property **acquired after 19 January 2025**, with property under a written binding contract entered into before that date treated as acquired then.

Qualified property is generally property with a recovery period of 20 years or less. A building never qualifies; the five and fifteen year components identified by a cost segregation study do.

Bonus depreciation differs from § 179 in a way that matters for Module 18: **bonus can create a loss**, § 179 cannot. A large bonus deduction therefore flows through to the excess business loss threshold, while a § 179 election is simply deferred by its own taxable income limitation.

#### 5.5 Recapture — where the deduction comes back

| Property type | Recapture provision | Character | Rate |
|---|---|---|---|
| Personal property — the 5 and 7 year components | **§ 1245** | **Ordinary income**, to the full extent of depreciation taken | Up to 37% |
| Land improvements — 15 year | § 1245 | Ordinary income | Up to 37% |
| Real property — the structure | § 1250 | **Unrecaptured section 1250 gain** | **Up to 25%** |
| Gain above all depreciation | § 1231 | Long-term capital gain | 0/15/20% |

Section 1245 recapture is complete: every dollar of depreciation on personal property comes back as ordinary income. Section 1250 recapture is different — because real property is depreciated straight line, there is no "excess" depreciation to recapture as ordinary income, and instead the depreciation component is taxed at a maximum of 25 percent under § 1(h)(1)(E).

This is the point at which cost segregation shows its cost. Reclassifying $400,000 from the structure to five and fifteen year property converts $400,000 of future 25 percent recapture into $400,000 of future **ordinary** recapture. Where the owner's rate at sale is 37 percent, the reclassification costs 12 percentage points on that slice.

The trade is still usually favourable, because the deduction is taken immediately at the owner's full ordinary rate and the recapture is deferred for years. But it is a trade, and presenting cost segregation as a permanent saving misstates it.

#### 5.6 Basis is reduced whether or not depreciation is claimed

Section 1016(a)(2) reduces basis by depreciation **allowed or allowable**. An owner who never claimed depreciation still reduces basis by what could have been claimed, and so pays recapture on a deduction never taken. There is no election to forgo depreciation to preserve basis.

### 6. Examples and Case Calculations

#### Example 1 — The cost segregation trade, in full

The $2,000,000 property from § 5.3, sold after ten years for $2,600,000. Owner's ordinary rate 37 percent, long-term capital gain rate 20 percent.

```
WITHOUT cost segregation
   Depreciation over 10 years   58,182 × 10        =   581,820
   Adjusted basis   2,000,000 − 581,820            = 1,418,180
   Gain             2,600,000 − 1,418,180          = 1,181,820
      unrecaptured § 1250, at 25%      581,820     =   145,455
      § 1231 gain, at 20%              600,000     =   120,000
                                                      --------
   Tax on sale                                         265,455

WITH cost segregation
   Year 1        443,636
   Years 2–10    43,636 × 9                        =   392,727
   Total depreciation                              =   836,363
   Adjusted basis   2,000,000 − 836,363            = 1,163,637
   Gain             2,600,000 − 1,163,637          = 1,436,363
      § 1245 ordinary, at 37%          400,000     =   148,000
      unrecaptured § 1250, at 25%      436,363     =   109,091
      § 1231 gain, at 20%              600,000     =   120,000
                                                      --------
   Tax on sale                                         377,091
```

The sale costs $111,636 more. Against that, the first year deduction was $385,454 larger, worth $142,618 at 37 percent, and the intervening years' deductions were smaller. The position is favourable on present value at ordinary discount rates, and it is not favourable in the way a client hears the words "tax saving".

#### Example 2 — A first-year loss and where it goes

The same property, first year, owner with $600,000 of wages.

```
Rental income                                        140,000
Operating expenses                                   −55,000
Depreciation with cost segregation                  −443,636
                                                    --------
Rental result                                       −358,636
```

Where the loss goes depends entirely on Modules 20, 21 and 25:

| Classification | Outcome |
|---|---|
| Long-term let, passive, income $600,000 | **Suspended in full** — the $25,000 allowance is fully phased out |
| Short-term let, seven-day average, material participation | **Non-passive**, deductible against wages |
| Owner also uses it 30 days, 190 rental days | **Capped by § 280A** — no loss at all |

The depreciation is identical in all three. Only the classification decides whether it is worth $132,695 at 37 percent or nothing at all this year.

#### Example 3 — Depreciation not claimed

An owner holds a residential rental for twelve years and never claims depreciation.

```
Allowable depreciation not taken   58,182 × 12   =   698,184
Basis reduced by § 1016(a)(2) regardless         =   698,184
Recapture on sale                                     at 25%
```

The owner pays recapture on $698,184 of deductions they never received. The remedy is a change of accounting method on Form 3115 with a § 481(a) adjustment, which recovers the missed depreciation in a single year, but it must be claimed.

### 7. Interactions with Other Rules

**Personal use (Module 20).** Depreciation is the last deduction in the § 280A ordering and the first to be deferred.

**Short-term rentals (Module 21).** The classification decides whether the depreciation loss is usable now or suspended. Cost segregation and the seven-day rule are almost always used together.

**At-risk rules (Module 23).** A loss must be within the amount at risk. For real estate, qualified nonrecourse financing counts, which is why leveraged property can still generate deductible losses.

**Passive activity losses (Module 25).** A suspended depreciation loss is released on a fully taxable disposition under § 469(g) — a release the engine does not implement.

**Excess business loss (Module 18).** A non-passive depreciation loss reaches the § 461(l) threshold in the year it arises. At $256,000 or $512,000 the threshold frequently binds on a first-year cost segregation deduction.

**Section 179 (Module 19).** Section 179 cannot create a loss; bonus depreciation can. Where the excess business loss threshold is close, the choice between them changes the outcome.

**Capital gains (Modules 01 and 24).** The 25 percent ceiling on unrecaptured section 1250 gain and the ordinary treatment of § 1245 recapture are both part of the § 1(h) rate structure, only three components of which the engine implements.

**Estate treatment (Module 31).** Death eliminates recapture entirely. A § 1014 basis step-up resets basis to fair market value, and the accumulated depreciation is never recaptured. For an owner with heavily depreciated property and a limited life expectancy, holding until death is worth more than any exchange.

### 8. Common Scenarios and Edge Cases

**Land is never depreciable**, and the land allocation is the first thing an examiner looks at. Using the property tax assessor's ratio is common and is not always defensible.

**Cost segregation converts 25 percent recapture into 37 percent recapture** on the reclassified components. It remains favourable on timing, and it is not a permanent saving.

**Basis falls whether or not depreciation is claimed.** Section 1016(a)(2) says allowed **or allowable**.

**A large first-year deduction is worth nothing if the loss is suspended.** The classification work in Modules 20 and 21 must be done before the study is commissioned, not after.

**Bonus depreciation can create a loss; § 179 cannot.** This is the practical difference between them at the margin.

**Death eliminates recapture.** A step-up under § 1014 wipes out accumulated depreciation, which makes a deathbed sale materially worse than holding.

**A § 1031 exchange defers gain and carries the depreciation history forward.** The recapture is postponed, not forgiven, and the replacement property inherits the reduced basis.

**Property acquired under a binding contract before 20 January 2025** is treated as acquired then, so the pre-Act phase-down percentage applies.

### 9. Planning Implications

The sequence matters more than the study. Establish the § 280A position and the § 469 classification first; commission the cost segregation study second. A study on a property whose losses will be suspended converts a $15,000 professional fee into a deferred benefit of uncertain date.

Where the loss will be non-passive, the first-year deduction should be sized against the excess business loss threshold in Module 18. A deduction that pushes the taxpayer well past $512,000 of net business loss is partly deferred anyway, and electing out of bonus depreciation for one class can produce a better result than the largest possible deduction.

For an owner approaching the end of life, holding depreciated property is worth more than selling it. The § 1014 step-up eliminates both the recapture and the capital gain, and Module 31 sets out the mechanics.

Where depreciation has not been claimed in earlier years, Form 3115 with a § 481(a) adjustment recovers it in one year. This is a common finding on a new client's prior returns and is often the largest single item available.

### 10. Data Tables for the Engine

| Constant | Value | Source |
|---|---|---|
| Residential rental recovery period | 27.5 years | § 168(c) |
| Non-residential recovery period | 39 years | § 168(c) |
| Land improvements | 15 years | § 168(e) |
| Tangible personal property | 5 or 7 years | § 168(e) |
| Real property convention | Mid-month | § 168(d)(2) |
| Personal property convention | Half-year, or mid-quarter | § 168(d)(1), (3) |
| Bonus depreciation | **100 percent**, permanent | § 168(k), P.L. 119-21 § 70301 |
| Bonus effective for property acquired after | 19 January 2025 | P.L. 119-21 § 70301(c) |
| § 1245 recapture | Ordinary income, full extent of depreciation | § 1245(a) |
| Unrecaptured § 1250 gain | Maximum 25 percent | § 1(h)(1)(E) |
| Basis reduction | Depreciation allowed **or allowable** | § 1016(a)(2) |

### 11. References

[56] One Big Beautiful Bill Act, P.L. 119-21, § 70301, amending IRC § 168(k). https://www.govinfo.gov/content/pkg/PLAW-119publ21/html/PLAW-119publ21.htm

[57] 26 U.S.C. §§ 167, 168, 1016, 1245 and 1250. United States Code, Office of the Law Revision Counsel. https://www.govinfo.gov/app/collection/uscode

[58] Internal Revenue Service, *Publication 946, How To Depreciate Property*. https://www.irs.gov/pub/irs-pdf/p946.pdf

[8] 26 U.S.C. § 1(h). https://www.govinfo.gov/app/collection/uscode

### 12. Status in This System

| Layer | Status |
|---|---|
| Projection engine | **Applied while the property is held; absent entirely on sale.** Recovery periods of 27.5 and 39 years are implemented, land is excluded from the depreciable base, cost segregation allocates to five and fifteen year components, and bonus depreciation is applied at 100 percent — which matches the permanent rate set by P.L. 119-21. Depreciation correctly ceases at the end of the recovery period. |
| Backend (`tax-be`) | **Not applied.** `strategyPhaseMap.js` catalogues "Cost Segregation", "Accelerated Depreciation Strategy", "Bonus Depreciation Strategy — §168(k)" and "§168/§168(k) Depreciation Timing Optimization", and `AIStrategyData.json` assigns "Accelerated Depreciation Strategy" and "Cost Segregation" to clients. None is computed. |
| Known limitations | **The disposition of a property produces nothing at all.** Once the projected age passes the property's disposal age the engine marks it sold and returns. No amount realised is computed, no adjusted basis is used, no gain is recognised, and no tax is charged. The constant holding the 25 percent recapture rate is defined and **never referenced**, and the running total of depreciation accumulated over every year of the projection is **never read**. The property's value is then simply removed from net worth rather than converted into after-tax cash. Tax is understated and net worth is understated at the same time, and any projection in which a client sells property is wrong from that year forward. Recorded as **D18**, and it is the most consequential defect in the register. Separately, the § 1245 and unrecaptured § 1250 rate treatments are absent from the capital gain computation itself, recorded as D17. Also not modelled: the mid-month, half-year and mid-quarter conventions, so first-year depreciation is overstated; the election out of bonus depreciation by class; the § 280F limits on passenger automobiles; and § 1031 exchanges. |


---

## Module 23 — At-Risk Rules for Real Estate

**Tax year:** 2026 · **As of:** September 2026 · **Primary authority:** IRC § 465

---

### 1. Overview and Purpose

Section 465 limits a loss to the amount the taxpayer actually has at risk in the activity. Money the taxpayer cannot lose does not support a deduction. The rule was enacted to stop shelters funded with nonrecourse debt that the investor was never going to repay, and it applies to individuals and to closely held C corporations, activity by activity.

Real estate has its own exception, and it is the reason leveraged property still produces deductible losses. Section 465(b)(6) treats a taxpayer as at risk for their share of **qualified nonrecourse financing** secured by real property used in the activity, even though nobody is personally liable for it.[59] Without that provision, ordinary commercial mortgage debt would not support depreciation losses at all, and the whole of the real estate planning treated in Modules 21 and 22 would be unavailable.

The at-risk rules are the **second** of the four loss gates. A loss must first clear basis under § 704(d) or § 1366(d), then this gate, then the passive activity rules, then the excess business loss limitation. Amounts disallowed here carry forward indefinitely and are allowed in a later year when the amount at risk increases.

### 2. Governing Law and Authorities

| Type | Citation | What it establishes |
|---|---|---|
| Statute | IRC § 465(a)(1) | Loss limited to the amount at risk |
| Statute | IRC § 465(a)(2) | Indefinite carryforward of disallowed amounts |
| Statute | IRC § 465(b)(1) | What counts as at risk |
| Statute | IRC § 465(b)(2) | Amounts borrowed |
| Statute | IRC § 465(b)(3) | Amounts borrowed from a person with an interest |
| Statute | IRC § 465(b)(4) | Protection against loss |
| Statute | IRC § 465(b)(6) | Qualified nonrecourse financing for real property |
| Statute | IRC § 465(c)(3) | Application to activities generally |
| Statute | IRC § 465(e) | Recapture where the amount at risk goes below zero |
| Statute | IRC § 752 | A partner's share of liabilities |
| Statute | IRC § 49(a)(1)(D)(iv) | Definition of a qualified person |

### 3. Key Definitions

| Term | Definition |
|---|---|
| **Amount at risk** | Cash contributed, the adjusted basis of property contributed, and amounts borrowed for which the taxpayer is personally liable or has pledged property not used in the activity, adjusted for income, losses and distributions. |
| **Qualified nonrecourse financing** | Financing borrowed for the activity of holding real property, from a qualified person or a government, for which **no person is personally liable**, and which is not convertible debt.[59] |
| **Qualified person** | A person actively and regularly engaged in the business of lending money, taking the § 49(a)(1)(D)(iv) definition. A related-party lender qualifies where the financing is commercially reasonable and on substantially the same terms as arm's-length loans. |
| **Protected against loss** | Covered by a guarantee, stop-loss agreement, or similar arrangement, which removes the amount from the at-risk figure under § 465(b)(4). |
| **Activity of holding real property** | Includes incidental personal property and services provided in making the property available as living accommodation. Excludes mineral property. |

### 4. Who Is Affected

Individuals, and C corporations where five or fewer individuals own more than half the stock. Partnerships and S corporations do not apply the rules; their owners do, on their own share.

Every taxpayer holding real estate with a mortgage is affected, and for most the effect is benign: an ordinary commercial mortgage from a bank is qualified nonrecourse financing, so the debt is included in the amount at risk and the rules rarely bind.

They bind in three situations: seller financing where the seller retains an interest in the property, financing from a related party on non-commercial terms, and any arrangement where a guarantee or indemnity shifts the economic risk away from the taxpayer.

### 5. Core Rules and Calculations

#### 5.1 Case Register

| # | Case | Applied |
|---|---|---|
| 1 | § 465(a)(1) loss limited to the amount at risk | Yes |
| 2 | § 465(a)(2) indefinite carryforward | Yes |
| 3 | Amount at risk reduced by allowed losses | Yes |
| 4 | Amount at risk increased by income | **No** |
| 5 | Amount at risk reduced by distributions | **No** |
| 6 | Cash and contributed property basis included | Yes — entered as an opening figure |
| 7 | Recourse debt included | Yes, in effect |
| 8 | Ordinary nonrecourse debt excluded | **No** |
| 9 | § 465(b)(6) qualified nonrecourse financing included | Yes, in effect |
| 10 | Four conditions of qualified nonrecourse financing tested | **No** |
| 11 | § 465(b)(3) borrowing from a person with an interest | **No** |
| 12 | § 465(b)(4) protection against loss | **No** |
| 13 | § 752 share of partnership liabilities | **No** |
| 14 | § 465(e) recapture where at risk goes negative | **No** |
| 15 | Applied activity by activity | Yes — property by property |
| 16 | Position as gate 2, after basis and before passive | Yes |
| 17 | Conservation identity across the four gates | Yes |

#### 5.2 The computation

```
amountAtRisk(start of year)
   + cash and property contributed
   + qualifying debt
   + income from the activity
   − distributions
   − losses previously allowed
   = amountAtRisk(before this year's loss)

allowedLoss    = min( lossAfterBasisGate , amountAtRisk )
suspendedLoss  = lossAfterBasisGate − allowedLoss      carried forward indefinitely
amountAtRisk   = amountAtRisk − allowedLoss
```

The suspended amount is released in a later year when the amount at risk increases — through additional contributions, additional qualifying debt, or income from the activity.

#### 5.3 What is and is not at risk

| Included | Excluded |
|---|---|
| Cash contributed | Nonrecourse debt that is not qualified nonrecourse financing |
| Adjusted basis of property contributed | Amounts protected by a guarantee or stop-loss, § 465(b)(4) |
| Debt for which the taxpayer is personally liable | Amounts borrowed from a person with an interest in the activity, § 465(b)(3) |
| Property pledged as security, where not used in the activity | Convertible debt |
| **Qualified nonrecourse financing**, § 465(b)(6) | Mineral property financing |

#### 5.4 The four conditions for qualified nonrecourse financing

All must hold:[59]

1. **Borrowed with respect to the activity of holding real property.** Personal property and services incidental to making the property available as living accommodation are included; mineral property is not.
2. **Borrowed from a qualified person, or from or guaranteed by a government.** A qualified person is one actively and regularly engaged in lending. A related-party lender qualifies only where the financing is commercially reasonable and on substantially the same terms as an arm's-length loan.
3. **No person is personally liable for repayment.** A personal guarantee by the taxpayer or anyone else defeats this condition.
4. **Not convertible debt.**

For a partner, the share is determined by their share of partnership liabilities under § 752.

The condition that catches people is the second. Seller financing is the common case: a vendor who takes back a note has an interest in the property, and unless the terms are genuinely commercial the financing is not qualified, so the debt does not enter the at-risk figure at all.

#### 5.5 A personal guarantee cuts both ways

A guarantee makes debt recourse to the guarantor, which **increases** their amount at risk. It simultaneously means that a person is personally liable, which **disqualifies** the debt from being qualified nonrecourse financing for everyone else in the activity.

In a partnership, one partner guaranteeing the mortgage can therefore move the whole of that debt out of the § 465(b)(6) category for the other partners and into the guarantor's own at-risk amount. The guarantor gains capacity; the others lose it.

#### 5.6 Recapture — § 465(e)

Where the amount at risk falls below zero — typically through a distribution, or through a change in the debt structure that removes qualifying financing — previously allowed losses are recaptured as income to the extent of the negative amount. The recaptured amount then becomes a deduction available in later years when the at-risk figure recovers.

This is the mirror image of the suspension rule and is easy to trigger by refinancing.

### 6. Examples and Case Calculations

#### Example 1 — Ordinary leveraged property, the rules do not bind

An investor buys a rental for $2,000,000 with $400,000 of cash and a $1,600,000 commercial mortgage from a bank, nonrecourse. First-year loss after cost segregation is $358,000.

```
Cash contributed                                     400,000
Qualified nonrecourse financing, § 465(b)(6)       1,600,000
                                                   ---------
Amount at risk                                     2,000,000

Loss                                                 358,000
Allowed — well within the amount at risk            $358,000
Amount at risk carried forward                     1,642,000
```

The at-risk gate passes without effect. This is the ordinary case and it is why the rules are often ignored — but they are passing, not absent.

#### Example 2 — Seller financing that is not qualified

The same purchase, but the $1,600,000 is seller financing on non-commercial terms.

```
Cash contributed                                     400,000
Seller note — the seller has an interest in the
   property and the terms are not commercial,
   so § 465(b)(6)(B)(ii) is not satisfied                   0
                                                   ---------
Amount at risk                                       400,000

Loss                                                 358,000
Allowed                                             $358,000
Amount at risk carried forward                        42,000
```

The first year still passes. The second year does not: with $42,000 of capacity and a further loss of $70,000, only $42,000 is allowed and $28,000 is suspended. The identical property with bank financing would have had $1,642,000 of capacity.

#### Example 3 — A guarantee moving capacity between partners

A two-partner partnership, equal shares, with a $2,000,000 nonrecourse mortgage. Partner A guarantees it personally.

```
Before the guarantee
   Each partner's share of qualified nonrecourse financing   1,000,000

After the guarantee
   The debt is no longer nonrecourse — a person is
   personally liable — so § 465(b)(6) does not apply
   Partner A, personally liable                              2,000,000
   Partner B                                                         0
```

Partner B's at-risk amount falls from $1,000,000 to their cash contribution alone. A guarantee given for lender reasons, without tax advice, can suspend a co-owner's losses entirely.

#### Example 4 — The four gates in order

A partner with a $250,000 loss, $180,000 of outside basis, $150,000 at risk, the activity passive, no passive income, and wages of $600,000.

```
Gate 1  § 704(d) basis        allowed 180,000   suspended  70,000
Gate 2  § 465 at risk         allowed 150,000   suspended  30,000
Gate 3  § 469 passive         allowed       0   suspended 150,000
           the $25,000 allowance is fully phased out at $600,000
Gate 4  § 461(l)              nothing reaches it

Deducted this year                          $0
Suspended, by gate    70,000 basis + 30,000 at risk + 150,000 passive = 250,000
```

The conservation identity holds: every dollar is either allowed or suspended at exactly one gate, and the suspensions are tracked separately because each is released by a different event.

### 7. Interactions with Other Rules

**Basis (Module 26).** Gate 1. A loss must clear § 704(d) or § 1366(d) before reaching this gate. Basis and at-risk amounts are usually similar but not identical — nonrecourse debt increases a partner's basis under § 752 but only qualifies for at-risk purposes if it meets § 465(b)(6).

**Passive activity losses (Module 25).** Gate 3. A loss allowed here still faces the passive rules, and for most rental property that is where it stops.

**Excess business loss (Module 18).** Gate 4, reached only by a non-passive loss.

**Short-term rentals (Module 21).** A non-passive short-term rental loss must still clear this gate. The at-risk amount is the practical ceiling on how much of a cost segregation deduction is usable in year one.

**Depreciation (Module 22).** Depreciation creates the loss that this gate measures, and it also reduces the amount at risk as it is allowed.

**Disposition.** Section 465 suspended losses are released on disposition of the activity, in the same way as passive losses under § 469(g), though under a different provision.

### 8. Common Scenarios and Edge Cases

**A commercial bank mortgage is qualified nonrecourse financing.** The rules pass without effect for most ordinary property, which is why they are so often overlooked.

**Seller financing usually is not.** The seller has an interest in the property, and the commercially-reasonable exception must be positively established rather than assumed.

**A personal guarantee disqualifies the debt for everyone else.** It is the single most common way a co-owner's at-risk amount collapses.

**Basis and at-risk are different figures.** Nonrecourse debt raises a partner's basis under § 752 whether or not it is qualified nonrecourse financing; only qualifying debt raises the at-risk amount.

**The amount at risk falls as losses are allowed.** A property generating large losses exhausts its at-risk capacity over time even where the debt is unchanged.

**Distributions reduce the amount at risk** and can trigger § 465(e) recapture where they push it below zero.

**The rules apply activity by activity.** Capacity in one property does not support a loss in another.

**Refinancing can change the answer.** Replacing qualified nonrecourse financing with a guaranteed loan converts everyone else's capacity into the guarantor's.

### 9. Planning Implications

Before accepting seller financing, the § 465(b)(6) conditions should be tested. A note on commercial terms from a seller can qualify; one on soft terms will not, and the difference is the whole of the debt in the at-risk figure.

Personal guarantees should be given deliberately. Where a lender requires one, the consequence for co-owners' at-risk amounts should be understood and, where possible, the guarantee limited or allocated.

For a taxpayer relying on a large first-year cost segregation loss, the amount at risk is the ceiling that binds before the passive rules are even reached. Cash invested and qualifying debt should be confirmed before the study is commissioned.

Suspended at-risk losses are released by contributions and by income from the activity, so a later capital call or a profitable year frees them. They are not lost, and modelling them as lost understates the position.

### 10. Data Tables for the Engine

| Constant | Value | Source |
|---|---|---|
| Position in the ordering | Gate 2, after basis, before passive | § 465, § 469 |
| Carryforward | Indefinite | § 465(a)(2) |
| Qualified nonrecourse financing | Included in the amount at risk | § 465(b)(6)(A) |
| Conditions | Real property activity; qualified person or government; no personal liability; not convertible | § 465(b)(6)(B) |
| Qualified person | § 49(a)(1)(D)(iv), with a related-party exception on commercial terms | § 465(b)(6)(D) |
| Partner's share | By share of liabilities under § 752 | § 465(b)(6)(C) |
| Protection against loss | Removed from the amount at risk | § 465(b)(4) |
| Recapture | Where the amount at risk falls below zero | § 465(e) |
| Application | Activity by activity | § 465(c) |

### 11. References

[59] 26 U.S.C. § 465, *Deductions limited to amount at risk*. United States Code, Office of the Law Revision Counsel. https://www.govinfo.gov/app/collection/uscode

[60] 26 U.S.C. § 752, *Treatment of certain liabilities*. https://www.govinfo.gov/app/collection/uscode

[61] Internal Revenue Service, *Form 6198, At-Risk Limitations*, and instructions. https://www.irs.gov/forms-pubs/about-form-6198

### 12. Status in This System

| Layer | Status |
|---|---|
| Projection engine | **Applied.** The at-risk limitation is implemented as the second gate, after the basis limitation and before the passive activity rules, which is the statutory order. Losses are limited to the amount at risk, the amount at risk is reduced as losses are allowed, and the suspended amount is tracked separately from amounts suspended at the other three gates. The four-gate function asserts a **conservation identity** — that allowed plus each category of suspension equals the original loss — which is a genuine correctness check and one that most implementations do not perform. |
| Backend (`tax-be`) | **Not applied.** `strategyPhaseMap.js` catalogues "§465 At-Risk Limitation Review" and "§465 At-Risk Limitation Planning" as named strategies, but no computation exists. |
| Known limitations | The amount at risk is entered as an opening figure and reduced by allowed losses; it is **not increased by income from the activity** and **not reduced by distributions**, so it drifts from the true figure in any year the property is profitable or cash is taken out. The four conditions of § 465(b)(6) are not tested — the engine accepts an at-risk figure without asking whether the financing behind it is qualified — so the seller-financing case in Example 2 and the guarantee case in Example 3 cannot be represented. Section 465(b)(3) borrowing from a person with an interest and § 465(b)(4) protection against loss are not modelled. A partner's share of liabilities under § 752 is not computed. The § 465(e) recapture where the amount at risk falls below zero is absent, so a distribution-driven recapture never appears. |


---

## Module 24 — Capital Gains and Losses

**Tax year:** 2026 · **As of:** September 2026 · **Primary authority:** IRC §§ 1211, 1212, 1221, 1222

---

### 1. Overview and Purpose

A capital gain or loss arises on the sale or exchange of a capital asset. The character — short-term or long-term — turns on whether the asset was held for more than one year, and the two are netted separately before being netted against each other.

Two asymmetries govern the planning. Gains are taxed in full in the year realised, while **losses are deductible against ordinary income only $3,000 a year**. That figure was set in 1978 and has never been indexed, so a taxpayer with a $55,000 net capital loss and no gains needs eighteen years to absorb it. The second asymmetry is that realisation is voluntary for gains and largely voluntary for losses, which makes timing the principal lever.

The rates themselves are treated in Module 01, which sets out all four components of § 1(h) — the 0, 15 and 20 percent rates on adjusted net capital gain, the 25 percent ceiling on unrecaptured section 1250 gain, and the 28 percent ceiling on collectibles and § 1202 gain. This module deals with what is netted, what is limited, and what carries forward.

One provision changed substantially for 2026. The One Big Beautiful Bill Act rewrote the qualified small business stock exclusion at § 1202, introducing a tiered exclusion at three, four and five years, raising the per-issuer limit to $15,000,000, and raising the corporate gross assets ceiling to $75,000,000.[62]

### 2. Governing Law and Authorities

| Type | Citation | What it establishes |
|---|---|---|
| Statute | IRC § 1221 | Definition of a capital asset |
| Statute | IRC § 1222 | Short-term and long-term; netting definitions |
| Statute | IRC § 1223 | Holding period, including tacking |
| Statute | IRC § 1211(b) | $3,000 annual deduction against ordinary income |
| Statute | IRC § 1212(b) | Indefinite carryforward, character preserved |
| Statute | IRC § 1091 | Wash sales |
| Statute | IRC § 1202 | Qualified small business stock |
| Statute | IRC § 121 | Exclusion of gain on a principal residence |
| Statute | IRC § 1(h) | Rates — Module 01 |
| Legislation | P.L. 119-21, § 70431 | Expanded qualified small business stock exclusion |

### 3. Key Definitions

| Term | Definition |
|---|---|
| **Capital asset** | Property held by the taxpayer, other than inventory, depreciable business property, accounts receivable and certain self-created works. |
| **Long-term** | Held for **more than** one year. A holding of exactly one year is short-term. |
| **Net capital gain** | The excess of net long-term capital gain over net short-term capital loss. |
| **Wash sale** | A sale at a loss where substantially identical stock or securities are acquired within 30 days before or after the sale. |
| **Qualified small business stock** | Stock in a C corporation meeting the § 1202 active business and gross assets tests, acquired at original issue. |

### 4. Who Is Affected

Every taxpayer disposing of a capital asset. The $3,000 limitation applies to individuals; it is $1,500 for a married taxpayer filing separately.

Capital losses of a decedent do not pass to the estate or to heirs. An unused carryforward dies with the taxpayer, which makes the absorption arithmetic in § 5.3 a genuine planning constraint rather than an accounting formality.

### 5. Core Rules and Calculations

#### 5.1 Case Register

| # | Case | Applied |
|---|---|---|
| 1 | Short-term and long-term netted separately | **No** — a single gain figure is used |
| 2 | Net short-term loss offsetting net long-term gain | **No** |
| 3 | Net long-term loss offsetting net short-term gain | **No** |
| 4 | § 1211(b) $3,000 annual deduction | Yes |
| 5 | $1,500 for married filing separately | Yes |
| 6 | § 1212(b) indefinite carryforward | Yes |
| 7 | Character preserved on carryforward | **No** |
| 8 | Holding period, more than one year | **No** — gains are treated as long-term |
| 9 | § 1223 tacking of holding periods | **No** |
| 10 | § 1091 wash sales | **No** |
| 11 | § 1202 qualified small business stock exclusion | Partially — a flat exclusion, not the tiered rules |
| 12 | § 1202 tiered percentages at 3, 4 and 5 years | **No** |
| 13 | § 1202 per-issuer dollar limit | **No** |
| 14 | § 121 principal residence exclusion | **No** |
| 15 | Carryforward extinguished at death | **No** |
| 16 | Specific identification of lots | **No** |
| 17 | Gains raise provisional income and MAGI | Yes |

#### 5.2 Netting — § 1222

```
Step 1   net all short-term gains and losses     → net short-term
Step 2   net all long-term gains and losses      → net long-term
Step 3   if one is negative and the other positive, net them together
```

| Position | Net short-term | Net long-term | Overall |
|---|---|---|---|
| $50,000 short gain, $80,000 long gain | $50,000 | $80,000 | $130,000 |
| $40,000 short loss, $100,000 long gain | $0 | $60,000 | $60,000 |
| $60,000 short gain, $90,000 long loss | $0 | −$30,000 | −$30,000 |
| $25,000 short loss, $30,000 long loss | −$25,000 | −$30,000 | −$55,000 |

The second row matters for rate: a short-term loss absorbs long-term gain that would have been taxed at 15 or 20 percent, rather than sheltering ordinary income at up to 37 percent. Where the taxpayer has both, harvesting losses against **short-term** gains is worth more.

#### 5.3 The $3,000 limitation and the carryforward

Where the overall result is a net capital loss, § 1211(b) permits a deduction against ordinary income of the lesser of the loss or **$3,000** — $1,500 for a married taxpayer filing separately. The remainder carries forward under § 1212(b) indefinitely, retaining its short-term or long-term character.

| Net capital loss | Deducted this year | Carried forward |
|---|---|---|
| $2,000 | $2,000 | $0 |
| $12,000 | $3,000 | $9,000 |
| $55,000 | $3,000 | $52,000 |

At $3,000 a year a $55,000 loss takes **eighteen years** to absorb against ordinary income alone. It can be absorbed far faster against future capital gains, and that is the point: a carryforward is best understood as a stock of tax-free gain capacity rather than as an annual $3,000 deduction.

The $3,000 figure has not changed since 1978.

#### 5.4 Wash sales — § 1091

A loss is disallowed where substantially identical stock or securities are acquired within **30 days before or after** the sale — a 61-day window centred on the disposal. The disallowed loss is added to the basis of the replacement shares and the holding period tacks, so the loss is deferred rather than lost.

Three points are regularly missed. The window runs both ways, so a purchase made three weeks **before** the sale can trigger it. A purchase in an individual retirement account permanently destroys the loss, because there is no basis to add it to. And the rule applies to substantially identical securities, not merely to the same security, so switching between two index funds tracking the same index carries risk that switching between different indices does not.

#### 5.5 Qualified small business stock — § 1202 as amended

The One Big Beautiful Bill Act rewrote the exclusion for stock acquired after the date of enactment.[62]

**Stock acquired after the applicable date:**

| Holding period | Excluded |
|---|---|
| Less than 3 years | **0%** |
| 3 years | **50%** |
| 4 years | **75%** |
| **5 years or more** | **100%** |

**Stock acquired on or before the applicable date** retains the previous structure, requiring more than five years and giving the percentage applicable to its acquisition date.

Two limits were also raised:

| Limit | Before | After, for post-date stock |
|---|---|---|
| Per-issuer gain limit | $10,000,000 | **$15,000,000**, indexed after 2026 |
| Corporate aggregate gross assets | $50,000,000 | **$75,000,000**, indexed after 2026 |

The per-issuer limit is halved for a married taxpayer filing separately. The alternative limit of ten times basis remains.

On a $10,000,000 gain from post-date stock:

| Held | Excluded | Taxable |
|---|---|---|
| 2 years | $0 | $10,000,000 |
| 3 years | $5,000,000 | $5,000,000 |
| 4 years | $7,500,000 | $2,500,000 |
| 5 years | **$10,000,000** | **$0** |

Excluded gain is genuinely excluded — it never enters gross income, so it does not raise adjusted gross income, does not affect the Medicare surcharge, and does not enter the net investment income tax base. That distinguishes it from a deduction and makes it one of the most valuable provisions available to a founder.

#### 5.6 The principal residence exclusion — § 121

Gain on the sale of a principal residence is excluded up to **$250,000**, or **$500,000** on a joint return, where the taxpayer owned and used the property as a principal residence for at least two of the five years preceding the sale. The exclusion may be claimed once every two years.

Gain above the exclusion is capital gain. Depreciation taken for any business use since May 1997 is not excluded and remains unrecaptured section 1250 gain.

### 6. Examples and Case Calculations

#### Example 1 — Harvesting against the right kind of gain

A taxpayer has $60,000 of short-term gain from a concentrated position and $40,000 of unrealised loss elsewhere. Ordinary rate 37 percent, long-term rate 20 percent.

```
Harvest the loss against the short-term gain
   short-term gain reduced 60,000 → 20,000
   tax saved  40,000 × 37%                       = $14,800

If instead the gain had been long-term
   tax saved  40,000 × 20%                       =  $8,000
```

The same loss is worth $6,800 more when it absorbs short-term gain. Where a taxpayer has both, the netting order in § 5.2 does this automatically, but the decision about **which** position to sell is the taxpayer's.

#### Example 2 — A large loss and the eighteen-year problem

A taxpayer realises a $55,000 net capital loss in a year with no gains.

```
Year 1 deduction against ordinary income          3,000
Carried forward                                  52,000
```

Absorbed against ordinary income alone the loss runs to year eighteen. If the taxpayer expects to realise $200,000 of gain in three years, the carryforward is instead absorbed in full at that point, sheltering gain that would have been taxed at 20 percent plus 3.8 percent net investment income tax — a benefit of $13,090 rather than eighteen annual instalments of about $1,110.

#### Example 3 — A wash sale defeating the harvest

A taxpayer sells a fund at a $30,000 loss on 15 December and buys the same fund on 2 January.

```
Days between sale and repurchase                     18
Within the 61-day window                            yes
Loss disallowed                                 $30,000
Added to the basis of the replacement shares    $30,000
```

The loss is deferred, not destroyed — but the harvest achieved nothing for the year in which it was intended. Buying a different fund tracking a different index would have preserved it.

#### Example 4 — Founder stock at four years

A founder holds qualified small business stock acquired after the applicable date, with a $12,000,000 gain, and is offered an exit at the four-year mark.

```
Sell at 4 years    75% excluded          9,000,000 excluded
                   taxable gain          3,000,000
                   tax at 20% + 3.8%       714,000

Wait to 5 years    100% excluded, capped at the
                   $15,000,000 per-issuer limit
                   taxable gain                  0
                   tax                           0
```

Waiting twelve months saves $714,000. Under the pre-Act rules there was no partial exclusion at four years at all, so the tiered structure has made an early exit less punishing while still rewarding the full five years.

### 7. Interactions with Other Rules

**Rates (Module 01).** Section 1(h) supplies four rate components; this module supplies the amounts to which they apply. Ordinary income is stacked first, so a change in ordinary income can change the rate on an unchanged gain.

**Net investment income tax (Module 06).** A realised gain is net investment income **and** raises modified adjusted gross income, so it can cross the threshold and be taxed by the same movement.

**Taxation of Social Security (Module 14).** A gain raises provisional income even where it is taxed at zero percent, so a harvest in the zero-rate band can still cost 8.5 cents of benefit taxation per dollar.

**Medicare surcharge (Module 16).** A gain sets the premium two years later, and the structure is a cliff.

**Depreciation recapture (Module 22).** Unrecaptured section 1250 gain and § 1245 ordinary recapture come out of a property sale before any § 1231 capital gain.

**Passive activity losses (Module 25).** A fully taxable disposition releases suspended passive losses under § 469(g), which can offset the gain on the same sale.

**Step-up at death (Module 31).** Basis is reset to fair market value, so unrealised gain is never taxed. A capital loss carryforward, by contrast, is extinguished.

### 8. Common Scenarios and Edge Cases

**More than one year, not one year.** An asset held exactly twelve months is short-term. The holding period begins the day after acquisition.

**The $3,000 limit is not indexed.** It has been $3,000 since 1978 and is $1,500 for separate filers.

**Character is preserved on carryforward.** A long-term loss carried forward remains long-term and nets against long-term gain first.

**The wash sale window runs both ways.** A purchase before the sale counts.

**A wash sale into an individual retirement account destroys the loss permanently.** There is no basis in the account to which it can be added.

**A capital loss carryforward dies with the taxpayer.** It does not pass to the estate or to heirs, which argues for realising gains against it during life.

**Excluded § 1202 gain is outside adjusted gross income entirely.** It does not affect the Medicare surcharge or the net investment income tax. A widely repeated claim to the contrary is wrong.

**Section 121 does not cover depreciation.** Business-use depreciation since 1997 remains taxable as unrecaptured section 1250 gain even where the rest of the gain is excluded.

**Specific identification must be elected at the time of sale.** Absent an identification, first-in first-out applies, which usually realises the largest gain.

### 9. Planning Implications

A capital loss carryforward should be modelled as capacity to realise future gains tax free, not as a $3,000 annual deduction. The two framings give very different answers about whether to realise a gain.

Losses are worth most against short-term gains and against ordinary income, in that order, and least against long-term gains that would have been taxed at zero percent.

The years between retirement and the required beginning date are the cheapest years to realise gains, for the same reasons set out in Modules 09 and 10. For a taxpayer whose taxable income falls below the § 1(h) zero-rate ceiling — $98,900 on a joint return — gain harvested there is taxed at nothing, though it still raises provisional income and modified adjusted gross income.

For a founder, the five-year § 1202 holding period is now worth quantifying precisely against an earlier exit at 75 percent. The tiered structure means an exit at four years is no longer all-or-nothing.

Where a taxpayer has a large carryforward and a limited life expectancy, realising gains to absorb it is worth doing, because the carryforward is extinguished at death while the gain would otherwise have received a step-up.

### 10. Data Tables for the Engine

| Constant | Value | Indexed |
|---|---|---|
| Long-term holding period | More than 1 year | Fixed |
| § 1211(b) annual deduction | $3,000 | **No — since 1978** |
| § 1211(b), married filing separately | $1,500 | **No** |
| § 1212(b) carryforward | Indefinite, character preserved | Fixed |
| § 1091 wash sale window | 30 days before and after | Fixed |
| § 1202 exclusion, post-date stock | 50% at 3 years, 75% at 4, 100% at 5 | Fixed |
| § 1202 per-issuer limit, post-date | $15,000,000 | Yes, after 2026 |
| § 1202 per-issuer limit, pre-date | $10,000,000 | **No** |
| § 1202 gross assets ceiling | $75,000,000 | Yes, after 2026 |
| § 121 exclusion | $250,000 single, $500,000 joint | **No** |
| § 121 ownership and use | 2 of the preceding 5 years | Fixed |

### 11. References

[62] One Big Beautiful Bill Act, P.L. 119-21, § 70431, amending IRC § 1202(a), (b) and (d). https://www.govinfo.gov/content/pkg/PLAW-119publ21/html/PLAW-119publ21.htm

[63] 26 U.S.C. §§ 121, 1091, 1202, 1211, 1212, 1221, 1222 and 1223. United States Code, Office of the Law Revision Counsel. https://www.govinfo.gov/app/collection/uscode

[8] 26 U.S.C. § 1(h). https://www.govinfo.gov/app/collection/uscode

### 12. Status in This System

| Layer | Status |
|---|---|
| Projection engine | **Applied in part.** The $3,000 annual limitation is implemented with the correct $1,500 figure for married filing separately, and both are correctly held constant rather than inflated — the amount has not moved since 1978. The carryforward is indefinite. Realised gains correctly raise modified adjusted gross income and provisional income as well as being taxed, so the interactions with Modules 06, 14 and 16 behave properly. A qualified small business stock exclusion is present. |
| Backend (`tax-be`) | **Not applied.** `strategyPhaseMap.js` catalogues "1202 Gain Exclusion Stacking via Multiple Entities" and "Gifting Appreciated Stock to Family", but no computation exists. |
| Known limitations | Short-term and long-term are **not netted separately**. The engine carries a single realised gain figure treated as long-term, so it cannot represent a short-term loss absorbing long-term gain, cannot apply the ordinary rate to short-term gain, and cannot preserve character on the carryforward. Holding periods are not tracked, so § 1223 tacking and the more-than-one-year test are absent. Wash sales under § 1091 are not modelled, so a harvested loss is always allowed. The § 1202 exclusion is applied as a flat percentage rather than the tiered 50, 75 and 100 percent structure introduced for 2026, and neither the per-issuer dollar limit nor the corporate gross assets test is checked. The § 121 principal residence exclusion is absent entirely, which matters for any projection in which a client downsizes. Capital loss carryforwards are not extinguished at death. Lot-level specific identification is not modelled. |


---

## Module 25 — Passive Activity Losses

**Tax year:** 2026 · **As of:** September 2026 · **Primary authority:** IRC § 469

---

### 1. Overview and Purpose

Section 469 disallows a loss from a passive activity except against income from passive activities. A passive activity is a trade or business in which the taxpayer does not materially participate, and — by § 469(c)(2) — **any rental activity**, whether or not the taxpayer participates.

The rule was enacted in 1986 to end the shelter industry, and it remains the single most consequential limitation for a high-earning taxpayer with property. A physician earning $600,000 who buys a rental generating a $60,000 depreciation loss deducts none of it. The loss is suspended, accumulates year on year, and is released only when there is passive income, or when the activity is disposed of in a fully taxable transaction.

There are three ways out, and they are treated across three modules. The **seven-day rule** removes short-term rentals from the definition of rental activity altogether, which is Module 21. **Real estate professional status** under § 469(c)(7) removes the per se rule for a taxpayer who meets the 750-hour and more-than-half tests. And the **$25,000 allowance** under § 469(i) permits a limited deduction for an actively participating owner — but it phases out between $100,000 and $150,000 of adjusted gross income and is worth nothing to most of the people who need it.

This is the third of the four loss gates. A loss reaches it only after clearing basis and at-risk, and only a non-passive loss goes on to the excess business loss limitation.

### 2. Governing Law and Authorities

| Type | Citation | What it establishes |
|---|---|---|
| Statute | IRC § 469(a) | Disallowance of the passive activity loss |
| Statute | IRC § 469(b) | Indefinite carryforward |
| Statute | IRC § 469(c)(1) | Passive activity means no material participation |
| Statute | IRC § 469(c)(2) | Rental activity is per se passive |
| Statute | IRC § 469(c)(7) | Real estate professional exception |
| Statute | IRC § 469(e) | Portfolio income excluded from passive income |
| Statute | IRC § 469(g) | Release of suspended losses on a fully taxable disposition |
| Statute | IRC § 469(h) | Material participation; participation of a spouse |
| Statute | IRC § 469(i) | The $25,000 allowance and its phase-out |
| Regulation | Treas. Reg. § 1.469-2(f)(6) | Self-rental recharacterisation |
| Regulation | Treas. Reg. § 1.469-4 | Grouping of activities |
| Regulation | Treas. Reg. § 1.469-5T | Material participation tests — Module 21 |

### 3. Key Definitions

| Term | Definition |
|---|---|
| **Passive activity** | A trade or business in which the taxpayer does not materially participate, or any rental activity. |
| **Passive activity loss** | The excess of aggregate losses from all passive activities over aggregate income from all passive activities for the year. |
| **Active participation** | A lower standard than material participation, requiring bona fide involvement in management decisions. Available only for the § 469(i) allowance, and only to an owner of at least 10 percent. |
| **Portfolio income** | Interest, dividends, annuities and royalties not derived in the ordinary course of a trade or business. Excluded from passive income by § 469(e). |
| **Former passive activity** | An activity that was passive in a prior year and is not passive in the current year. |

### 4. Who Is Affected

Individuals, estates, trusts, closely held C corporations and personal service corporations. Partnerships and S corporations do not apply the rule; their owners do.

The taxpayers for whom it bites hardest are those with high ordinary income and rental property. The $25,000 allowance is fully phased out at $150,000 of adjusted gross income, so for anyone above that figure a passive rental loss is entirely suspended unless one of the two structural exceptions applies.

### 5. Core Rules and Calculations

#### 5.1 Case Register

| # | Case | Applied |
|---|---|---|
| 1 | § 469(a) disallowance of net passive loss | Yes |
| 2 | § 469(b) indefinite carryforward | Yes |
| 3 | Losses pooled across all passive activities | Yes |
| 4 | Passive income absorbing passive loss | Yes |
| 5 | § 469(c)(2) rental per se passive | Yes |
| 6 | § 1.469-1T(e)(3)(ii)(A) seven-day exception | Yes — Module 21 |
| 7 | § 469(c)(7) real estate professional | Yes — taken as an input |
| 8 | § 469(c)(7) 750-hour and more-than-half tests | **No** |
| 9 | § 469(c)(7)(A) per-property election to aggregate | **No** |
| 10 | § 469(i) $25,000 allowance | Yes |
| 11 | Phase-out at 50 cents per dollar above $100,000 | Yes |
| 12 | Allowance requires **active** participation and 10 percent ownership | **No** |
| 13 | § 469(i)(3)(E) modified adjusted gross income definition | **No** — ordinary AGI is used |
| 14 | § 469(e) portfolio income excluded from passive income | Yes, in effect |
| 15 | § 469(g) release on a fully taxable disposition | **No** |
| 16 | § 469(g)(1)(B) related-party disposition does not release | **No** |
| 17 | § 469(g)(2) death — release limited to the excess over the step-up | **No** |
| 18 | § 1.469-2(f)(6) self-rental recharacterisation | **No** |
| 19 | § 1.469-4 grouping elections | **No** |
| 20 | Material participation of a spouse counted | **No** |
| 21 | Position as gate 3 | Yes |

#### 5.2 The pooling rule

Section 469 does not test activity by activity. All passive activities are pooled:

```
aggregate passive income  −  aggregate passive losses  =  net position

if net position ≥ 0        all losses are absorbed; the excess income is taxable
if net position < 0        the net loss is the passive activity loss and is suspended,
                           allocated back across the loss activities pro rata
```

The allocation back matters, because each activity carries its own suspended balance that is released when **that** activity is disposed of.

#### 5.3 The $25,000 allowance — § 469(i)

An individual who **actively participates** in a rental real estate activity may deduct up to $25,000 of loss against non-passive income. Active participation is a lower standard than material participation — bona fide involvement in management decisions such as approving tenants, setting terms and authorising repairs — but it requires at least a 10 percent interest.

The allowance is reduced by **50 cents for every dollar** of adjusted gross income above $100,000, and is gone at $150,000:[64]

| Adjusted gross income | Allowance |
|---|---|
| $100,000 or less | **$25,000** |
| $110,000 | $20,000 |
| $125,000 | $12,500 |
| $140,000 | $5,000 |
| **$150,000 or more** | **$0** |

Neither the $25,000 nor the $100,000 threshold is indexed. Both have stood since 1986, so the allowance reaches fewer taxpayers every year in real terms.

For § 469(i) purposes adjusted gross income is computed without regard to taxable Social Security benefits, certain exclusions, the deductions for individual retirement contributions and student loan interest, and any passive loss itself.

#### 5.4 Real estate professional status — § 469(c)(7)

A taxpayer meeting both tests is not subject to the per se rental rule, and each rental activity is then tested for material participation in the ordinary way:

1. **More than half** of all personal services performed in trades or businesses during the year are performed in real property trades or businesses in which the taxpayer materially participates, **and**
2. **more than 750 hours** of service in those real property trades or businesses.

Both must be satisfied. The first is what closes the route to anyone with a full-time career elsewhere: a taxpayer working 2,000 hours as an employee would need more than 2,000 hours in real property businesses.

Status alone is not enough. Each rental must still meet material participation, unless the taxpayer makes the § 469(c)(7)(A) election to treat all interests in rental real estate as a single activity — which is usually essential for an owner of several properties, and which is difficult to revoke.

#### 5.5 Release on disposition — § 469(g)

When a taxpayer disposes of their **entire interest** in a passive activity in a **fully taxable** transaction, the suspended losses from that activity are freed and treated as **not from a passive activity**.[64] They become ordinary deductions against any income.

Three conditions and two exceptions:

| Requirement | Effect if not met |
|---|---|
| The **entire** interest is disposed of | Partial disposition releases nothing |
| The transaction is **fully taxable** | A § 1031 exchange or gift releases nothing |
| The buyer is **not a related party** under § 267(b) or § 707(b)(1) | Release deferred until the interest reaches an unrelated person |

On **death**, § 469(g)(2) allows the suspended losses only to the extent they exceed the basis step-up under § 1014. Where the step-up is large, the suspended losses are largely lost — the property's basis rises to fair market value and the losses that would have offset the gain simply disappear.

This is the mechanism that makes a long-held suspended loss balance valuable during life and worth very little at death.

#### 5.6 Self-rental recharacterisation

Under Treas. Reg. § 1.469-2(f)(6), where a taxpayer rents property to a trade or business in which they materially participate, **net rental income** from that property is recharacterised as non-passive. A net rental **loss** remains passive.

The rule is deliberately one-way. An owner cannot create passive income to absorb other passive losses by renting a building to their own practice, but a loss on that building stays trapped. It is one of the few genuinely asymmetric provisions in the section and it defeats a structure that would otherwise be obvious.

### 6. Examples and Case Calculations

#### Example 1 — The allowance is worthless where it is needed

Two taxpayers, each with a $30,000 rental loss and active participation.

```
Taxpayer A, adjusted gross income  $95,000
   allowance                        25,000
   deducted this year               25,000
   suspended                         5,000

Taxpayer B, adjusted gross income $600,000
   allowance                             0
   deducted this year                    0
   suspended                        30,000
```

The provision designed to relieve rental losses gives nothing to the taxpayer with the capacity to buy the property.

#### Example 2 — Pooling across activities

A taxpayer with three passive activities:

```
Activity 1  income                    40,000
Activity 2  loss                     −70,000
Activity 3  loss                     −30,000
                                     -------
Net passive position                 −60,000

Passive income absorbs 40,000 of the losses
Suspended, allocated pro rata across activities 2 and 3
   Activity 2   70/100 × 60,000  =   42,000
   Activity 3   30/100 × 60,000  =   18,000
```

Each activity carries its own suspended balance forward, because disposal of one releases only its own.

#### Example 3 — Release on disposition

Activity 2 from Example 2 is sold five years later to an unrelated buyer for a $50,000 gain. Its accumulated suspended losses are $210,000.

```
Gain on sale                                       50,000
Suspended losses released, § 469(g)              −210,000
                                                  -------
Net deduction against ordinary income            −160,000
```

The release is what makes a suspended balance an asset rather than a dead letter. The whole $210,000 becomes deductible against wages and business income in the year of sale.

#### Example 4 — The same disposition by gift, and at death

```
By gift to a child
   Not a fully taxable transaction
   Suspended losses are NOT released
   They are added to the donee's basis in the property
   The donor loses them permanently

At death, § 469(g)(2)
   Basis steps up under § 1014 from 400,000 to 900,000, a step-up of 500,000
   Suspended losses                                  210,000
   Allowed only to the extent they exceed the step-up      0
   The whole 210,000 is lost
```

A taxpayer holding a large suspended balance should be shown that it does not survive death. Realising it by sale during life converts $210,000 of dormant deduction into an immediate offset against ordinary income.

#### Example 5 — Self-rental

A dentist owns the building their practice occupies, and rents it to the practice.

```
Year 1  net rental income   60,000  → recharacterised NON-PASSIVE, § 1.469-2(f)(6)
        cannot absorb the $40,000 passive loss from an unrelated rental

Year 2  net rental loss    −20,000  → remains PASSIVE, suspended
```

Income is pulled out of the passive pool; loss is left in it. Structuring the rent to produce income in the hope of absorbing other passive losses does not work.

### 7. Interactions with Other Rules

**Personal use (Module 20).** Section 280A is applied first. A capped property produces no loss for § 469 to suspend.

**Short-term rentals (Module 21).** The seven-day rule removes the activity from rental treatment entirely, so the per se rule never applies and material participation governs.

**Basis and at-risk (Modules 23 and 26).** Gates 1 and 2 come first. A loss suspended there never reaches § 469.

**Excess business loss (Module 18).** Gate 4, reached only by a loss that is non-passive. A suspended passive loss reaches it in the year it is released, not the year it arose.

**Net investment income tax (Module 06).** Income from a passive activity **is** net investment income; income from an activity in which the taxpayer materially participates is not. The § 469 classification therefore decides the § 1411 treatment.

**Qualified business income (Module 17).** A loss allowed in the current year reduces qualified business income; a suspended loss does not until released.

**Depreciation (Module 22).** Depreciation creates most passive rental losses, and the value of a cost segregation study depends entirely on whether the resulting loss is suspended here.

**Step-up at death (Module 31).** Section 469(g)(2) limits the release to the excess over the step-up, which usually means the suspended balance is lost.

### 8. Common Scenarios and Edge Cases

**All rental activity is passive by default**, regardless of hours worked, unless the seven-day rule or real estate professional status applies.

**The $25,000 allowance is gone at $150,000 of adjusted gross income**, and neither figure has been indexed since 1986.

**Active participation is not material participation.** The allowance uses the lower standard; everything else uses the higher one.

**Portfolio income is not passive income.** Interest and dividends cannot absorb passive losses, which is the most common misunderstanding about the section.

**Disposal must be of the entire interest and fully taxable.** A partial sale, a gift, an exchange or a related-party sale releases nothing.

**A related-party sale defers the release** until the interest reaches an unrelated person, and the loss stays suspended in the meantime.

**Death largely destroys suspended losses.** Only the excess over the basis step-up survives, and where the property has appreciated the step-up usually exceeds the losses.

**Self-rental income is non-passive; self-rental loss is passive.** The rule runs one way only.

**Real estate professional status must be tested every year.** It is not a permanent designation, and a year of reduced hours loses it.

**Grouping elections are effectively permanent.** Treas. Reg. § 1.469-4 permits grouping, but regrouping is allowed only on a material change in facts.

### 9. Planning Implications

For a high earner, the choice is structural rather than incremental. The $25,000 allowance is unavailable, so the question is whether the property can be brought outside rental treatment through the seven-day rule, or whether real estate professional status is genuinely achievable. Where neither is available, the honest projection shows the loss suspended and the property should be evaluated on that basis.

A suspended loss balance should be modelled as a deferred asset with a specific release event. Its value is realised on a fully taxable disposal of the entire interest to an unrelated buyer, and it is largely destroyed at death. That asymmetry argues for selling appreciated passive property during life where a large suspended balance exists, and it runs against the usual advice to hold for the step-up. Which consideration dominates depends on the size of the suspended balance relative to the unrealised gain.

Where several rental properties are held and real estate professional status is claimed, the § 469(c)(7)(A) aggregation election is usually necessary, because material participation in each property separately is difficult to establish.

Passive income is a scarce and useful commodity for a taxpayer with suspended losses. An investment producing genuine passive income — a non-managed interest in an operating partnership, for instance — absorbs suspended losses that would otherwise sit for years.

### 10. Data Tables for the Engine

| Constant | Value | Indexed |
|---|---|---|
| § 469(i) allowance | $25,000 | **No — since 1986** |
| Phase-out start | $100,000 of adjusted gross income | **No** |
| Phase-out rate | 50 percent of the excess | Fixed |
| Fully phased out at | $150,000 | **No** |
| Minimum ownership for the allowance | 10 percent | Fixed |
| Real estate professional, hours | More than 750 | Fixed |
| Real estate professional, proportion | More than half of all personal services | Fixed |
| Carryforward | Indefinite | § 469(b) |
| Release | Entire interest, fully taxable, unrelated party | § 469(g)(1) |
| Release at death | Only the excess over the § 1014 step-up | § 469(g)(2) |
| Self-rental | Net income non-passive; net loss passive | § 1.469-2(f)(6) |
| Position in the ordering | Gate 3 | § 469 |

### 11. References

[64] 26 U.S.C. § 469, *Passive activity losses and credits limited*, including subsections (c)(7), (e), (g) and (i). United States Code, Office of the Law Revision Counsel. https://www.govinfo.gov/app/collection/uscode

[53] Treas. Reg. § 1.469-1T(e)(3). https://www.ecfr.gov/current/title-26/chapter-I/subchapter-A/part-1/section-1.469-1T

[54] Treas. Reg. § 1.469-5T. https://www.ecfr.gov/current/title-26

[65] Treas. Reg. §§ 1.469-2(f)(6) and 1.469-4. https://www.ecfr.gov/current/title-26

### 12. Status in This System

| Layer | Status |
|---|---|
| Projection engine | **Applied in part.** The passive classification, the pooling of losses against passive income, the indefinite carryforward and the position as the third gate are all implemented. The $25,000 allowance is present with the correct 50 percent phase-out beginning at $100,000, and — importantly — the constant is marked as **not indexed**, so the allowance correctly erodes across the projection rather than keeping pace with income. Portfolio income is kept out of the passive pool. Real estate professional status and material participation are available as inputs and correctly change the classification. |
| Backend (`tax-be`) | **Not applied.** `strategyPhaseMap.js` catalogues "Passive Activity Loss — §469 Grouping Election", "§469 Passive Activity Loss Release Strategy" and "Real Estate Professional Status (IRC §469)". None is computed. |
| Known limitations | **Section 469(g) is not implemented**, so suspended passive losses are **never released** — not on a sale, not on any disposition. This compounds the disposition defect recorded at D18: a property sale produces no gain, no recapture, no proceeds, and now also no release of the suspended losses that had accumulated against it. A client who sells a long-held rental should see a large deduction in that year and sees nothing. The related-party rule in § 469(g)(1)(B) and the death limitation in § 469(g)(2) are likewise absent. Self-rental recharacterisation under § 1.469-2(f)(6) is not applied, so net rental income from a building let to the owner's own practice is treated as passive and wrongly absorbs other passive losses. Grouping elections under § 1.469-4 are not modelled. The § 469(c)(7) tests are accepted as an input rather than derived from hours, and the per-property aggregation election is absent. The § 469(i) allowance is applied without testing active participation or the 10 percent ownership requirement, and it uses ordinary adjusted gross income rather than the modified figure defined in § 469(i)(3)(E). |


---

## Module 26 — Basis in Partnerships and S Corporations

**Tax year:** 2026 · **As of:** September 2026 · **Primary authority:** IRC §§ 704(d), 752, 1366(d), 1367

---

### 1. Overview and Purpose

An owner of a pass-through entity may deduct a loss only to the extent of their **basis** in the interest. Basis measures what the owner has economically put at stake: capital contributed, plus income taxed to them and not distributed, less losses already deducted and cash taken out.

This is the **first** of the four loss gates, and it comes before the at-risk rules, before the passive activity rules and before the excess business loss limitation. A loss disallowed here never reaches the others.

The single most important point in this module is that partnerships and S corporations compute basis differently, and the difference is entity-level debt. A partner's basis **includes their share of partnership liabilities** under § 752 — including nonrecourse mortgage debt. An S corporation shareholder's basis **does not include any corporate debt**, however the corporation borrowed it and however personally the shareholder feels responsible. Only money the shareholder lends **directly** to the corporation creates basis, and it creates a separate kind called debt basis.

The practical consequence is severe and routinely discovered too late. Two owners in economically identical positions — same capital, same property, same mortgage — have very different capacity to deduct losses depending on which entity they chose. This is the main reason leveraged real estate is held in partnerships and limited liability companies rather than in S corporations.

### 2. Governing Law and Authorities

| Type | Citation | What it establishes |
|---|---|---|
| Statute | IRC § 704(d) | Partner's loss limited to adjusted basis |
| Statute | IRC § 705 | Determination of a partner's basis |
| Statute | IRC § 752 | Partnership liabilities treated as contributions and distributions |
| Statute | IRC § 1366(d)(1) | Shareholder's loss limited to stock basis plus debt basis |
| Statute | IRC § 1366(d)(2) | Indefinite carryover of disallowed losses |
| Statute | IRC § 1366(d)(3) | Post-termination transition period |
| Statute | IRC § 1367(a) | Adjustments to stock basis |
| Statute | IRC § 1367(b)(2) | Reduction and restoration of debt basis |
| Statute | IRC § 1041 | Transfers between spouses or incident to divorce |
| Regulation | Treas. Reg. § 1.752-1 to -3 | Allocation of recourse and nonrecourse liabilities |

### 3. Key Definitions

| Term | Definition |
|---|---|
| **Outside basis** | The owner's basis in the partnership interest or the stock, as distinct from the entity's basis in its assets. |
| **Stock basis** | For an S corporation shareholder, basis in the shares. |
| **Debt basis** | For an S corporation shareholder, the adjusted basis of indebtedness **of the corporation to the shareholder**. Only direct shareholder loans qualify. |
| **Recourse liability** | A partnership liability for which a partner bears the economic risk of loss. |
| **Nonrecourse liability** | A liability for which no partner bears the economic risk of loss. Still included in a partner's basis. |
| **Post-termination transition period** | Generally the year following the loss of S corporation status, during which suspended losses may be used against restored stock basis. |

### 4. Who Is Affected

Partners in partnerships and members of limited liability companies treated as partnerships; shareholders of S corporations. The limitation is applied at the owner level.

The taxpayers most affected are those in leveraged businesses and property. A partner in a property partnership with a large mortgage has substantial basis from that mortgage alone. An S corporation shareholder in the same position has none of it.

### 5. Core Rules and Calculations

#### 5.1 Case Register

| # | Case | Applied |
|---|---|---|
| 1 | § 704(d) partner loss limited to basis | Yes |
| 2 | § 1366(d)(1) shareholder loss limited to stock plus debt basis | Yes |
| 3 | Indefinite carryforward of disallowed losses | Yes |
| 4 | Basis reduced by losses allowed | Yes |
| 5 | Basis increased by income | **No** |
| 6 | Basis increased by contributions | **No** |
| 7 | Basis reduced by distributions | **No** |
| 8 | § 752 share of partnership liabilities included in basis | **No** |
| 9 | Nonrecourse liabilities included for a partner | **No** |
| 10 | Entity debt **excluded** from S corporation stock basis | **No** — the distinction is not drawn |
| 11 | Debt basis from direct shareholder loans | **No** |
| 12 | Ordering: stock basis reduced first, then debt basis | **No** |
| 13 | § 1367(b)(2)(B) debt basis restored before stock basis | **No** |
| 14 | Distributions in excess of basis as capital gain | **No** |
| 15 | § 1366(d)(3) post-termination transition period | **No** |
| 16 | § 1041 transfer of suspended losses to a spouse | **No** |
| 17 | Position as gate 1 | Yes |
| 18 | Conservation identity across the four gates | Yes |

#### 5.2 The two regimes side by side

| | Partnership / LLC | S corporation |
|---|---|---|
| Capital contributed | Increases basis | Increases stock basis |
| Income allocated | Increases basis | Increases stock basis |
| Losses allocated | Decreases basis | Decreases stock basis, then debt basis |
| Distributions | Decrease basis | Decrease stock basis |
| **Entity-level debt** | **Increases basis, § 752** | **No effect** |
| **Nonrecourse mortgage** | **Increases basis** | **No effect** |
| Direct loan from the owner | Increases basis | Creates **debt basis**, § 1366(d)(1)(B) |
| Personal guarantee of entity debt | May shift the allocation among partners | **No basis** |

The last row is the one that surprises people most. A shareholder who personally guarantees the corporation's bank loan has **no** basis from it. The Tax Court has held so consistently: a guarantee is a contingent obligation, not an economic outlay, and basis arises only when the shareholder actually pays. The remedy is to borrow personally and lend the proceeds to the corporation, which creates genuine debt basis.

#### 5.3 The computation

```
PARTNER — § 704(d)
   basis = contributions + share of income + share of liabilities under § 752
           − distributions − share of losses previously allowed

   allowed   = min(loss, basis)
   suspended = loss − allowed          carried forward indefinitely

S CORPORATION SHAREHOLDER — § 1366(d)(1)
   stockBasis = contributions + income − distributions − losses previously allowed
   debtBasis  = direct loans to the corporation − prior reductions

   allowed   = min(loss, stockBasis + debtBasis)
   applied first against stock basis, then against debt basis
   suspended = loss − allowed          carried forward indefinitely
```

#### 5.4 The ordering rules for an S corporation

Losses reduce **stock basis first**, and only when stock basis reaches zero do they reduce **debt basis**.[66]

Restoration runs the other way. Section 1367(b)(2)(B) requires that any net increase in a later year be applied to **restore debt basis first**, before any of it may increase stock basis.[67]

This asymmetry matters because a distribution can only be taken against stock basis. A shareholder whose losses have consumed both stock and debt basis, and who then has a profitable year, finds the profit rebuilding the loan basis before it rebuilds the shares — so a distribution in that year may exceed stock basis and be taxable as capital gain.

#### 5.5 Distributions in excess of basis

A distribution reduces basis but cannot take it below zero. The excess is treated as gain from the sale of the interest, generally capital gain.

This is the trap that follows a period of losses. Basis has been consumed, the business recovers, cash is distributed, and the distribution is taxable even though the underlying profit has already been taxed to the owner in an earlier year. Tracking basis annually is the only defence.

#### 5.6 What happens to suspended losses

| Event | Partnership | S corporation |
|---|---|---|
| Basis restored by income or contribution | Loss released | Loss released |
| Interest sold | Suspended loss generally lost; basis affects gain | Suspended loss lost |
| Transfer to a spouse under § 1041 | — | Loss **transfers** to the transferee, § 1366(d)(2)(B) |
| S election terminates | — | Usable in the post-termination transition period against restored stock basis, § 1366(d)(3) |
| Death | Suspended loss generally lost | Suspended loss lost |

The § 1041 rule is unusual and useful: on a divorce transfer of S corporation stock, the suspended losses follow the stock to the transferee spouse rather than being extinguished.

### 6. Examples and Case Calculations

#### Example 1 — The same property in two entities

A rental property costing $2,000,000, funded with $400,000 of cash and a $1,600,000 nonrecourse mortgage. First-year loss after cost segregation is $358,000. Single owner.

```
HELD IN AN LLC TAXED AS A PARTNERSHIP
   Capital contributed                              400,000
   Share of liabilities, § 752                    1,600,000
                                                  ---------
   Outside basis                                  2,000,000
   Loss allowed at gate 1                          $358,000

HELD IN AN S CORPORATION
   Capital contributed                              400,000
   Corporate mortgage — no effect on basis                0
                                                  ---------
   Stock basis                                      400,000
   Loss allowed at gate 1                          $358,000
   Remaining basis                                   42,000
```

Year one passes in both. Year two does not. With a further $300,000 loss, the partner has $1,642,000 of basis and deducts it all; the shareholder has $42,000 and suspends $258,000.

#### Example 2 — A guarantee that creates no basis

The shareholder in Example 1 personally guarantees the corporate mortgage.

```
Guarantee given                                  1,600,000
Basis created                                            0
```

No basis arises until the shareholder actually pays under the guarantee. Had the shareholder instead borrowed $1,600,000 personally and lent it to the corporation, debt basis of $1,600,000 would have been created and the position would resemble the partnership.

#### Example 3 — Ordering and restoration

An S corporation shareholder with $100,000 of stock basis and $50,000 of debt basis from a direct loan, allocated a $180,000 loss.

```
Year 1
   Loss                                             180,000
   Against stock basis                              100,000  → stock basis 0
   Against debt basis                                50,000  → debt basis 0
   Allowed                                          150,000
   Suspended                                         30,000

Year 2 — the corporation earns $80,000 allocated to the shareholder
   § 1367(b)(2)(B): restore DEBT basis first
   Debt basis restored                               50,000  → debt basis 50,000
   Remaining to stock basis                          30,000  → stock basis 30,000
   Suspended loss released against restored basis    30,000
```

Had the shareholder taken a $30,000 distribution in year 2 expecting it to be tax free, it would have exceeded stock basis at the moment it was taken and produced capital gain.

#### Example 4 — All four gates in order

A partner with a $250,000 loss, $180,000 of outside basis, $150,000 at risk, the activity passive, no passive income, and $600,000 of wages.

```
Gate 1  § 704(d) basis        allowed 180,000    suspended  70,000
Gate 2  § 465 at risk         allowed 150,000    suspended  30,000
Gate 3  § 469 passive         allowed       0    suspended 150,000
Gate 4  § 461(l)              nothing reaches it

Deducted this year                                       $0
Total suspended, by cause                           250,000
```

Each suspension is released by a different event: basis by a contribution or income, at-risk by qualifying debt or income, passive by passive income or a qualifying disposition. Tracking them in one pooled figure loses that information and releases them at the wrong time.

### 7. Interactions with Other Rules

**At-risk (Module 23).** Gate 2. Basis and at-risk amounts are usually similar but not identical: nonrecourse debt increases a partner's basis under § 752 whether or not it is qualified nonrecourse financing, while only qualifying debt increases the amount at risk.

**Passive activity losses (Module 25).** Gate 3, where most rental losses stop.

**Excess business loss (Module 18).** Gate 4, reached only by non-passive losses.

**Self-employment tax (Modules 04 and 19).** A general partner's distributive share is subject to self-employment tax; an S corporation shareholder's is not. The entity choice that improves basis worsens the employment tax position, and vice versa.

**Qualified business income (Module 17).** An S corporation shareholder's reasonable compensation reduces qualified business income while creating the W-2 wages the § 199A limitation requires.

**Depreciation (Module 22).** Depreciation creates the losses that this gate measures, and entity-level debt is what supports them in a partnership.

**Divorce (Module 36).** Section 1366(d)(2)(B) transfers suspended S corporation losses to a transferee spouse under § 1041, which is a rare instance of a suspended attribute surviving a transfer.

### 8. Common Scenarios and Edge Cases

**Entity debt gives a partner basis and gives a shareholder none.** This is the defining difference and it decides where leveraged property should be held.

**A personal guarantee creates no S corporation basis.** Only actual payment does. Back-to-back lending — borrow personally, lend to the corporation — achieves what the guarantee does not.

**Losses reduce stock basis before debt basis; income restores debt basis before stock basis.** The two orderings are opposite, and the consequence is a distribution trap in the recovery year.

**A distribution in excess of basis is capital gain**, even where the underlying profits were taxed in an earlier year.

**Suspended basis losses are generally lost on a sale of the interest**, unlike suspended passive losses, which are released. The two gates behave differently on disposition.

**A nonrecourse liability still gives a partner basis** under § 752, and this is what makes property partnerships work.

**Basis must be tracked annually.** Neither the entity nor the return computes it for the owner, and reconstructing years of basis history after the fact is one of the most common and most expensive engagements in practice.

**S corporation suspended losses survive a § 1041 transfer** but do not survive a sale or death.

### 9. Planning Implications

Entity choice for leveraged assets should be made with this module in mind. Property with a substantial mortgage belongs in a partnership or limited liability company, because the debt supports basis. An operating business with little debt and a large wage component may be better as an S corporation for the employment tax reasons in Module 19. The two considerations pull in opposite directions and the answer depends on which constraint binds.

Where an S corporation shareholder needs basis, the route is a direct loan, documented as such, with a note and interest. A guarantee will not do, and restructuring after the loss year does not create retroactive basis.

Basis should be tracked in the projection as a running balance from the first year, not estimated when a loss appears. A shareholder who has taken distributions for years may have far less basis than they assume, and the first indication is usually a disallowed loss or an unexpected capital gain.

In the recovery year after a period of losses, distributions should be tested against **stock** basis specifically, because restoration goes to debt basis first.

### 10. Data Tables for the Engine

| Constant | Value | Source |
|---|---|---|
| Position in the ordering | Gate 1, before at-risk | § 704(d), § 1366(d) |
| Partner basis includes entity liabilities | Yes, by § 752 share | § 752 |
| S corporation basis includes entity debt | **No** | § 1366(d)(1) |
| S corporation debt basis | Direct shareholder loans only | § 1366(d)(1)(B) |
| Loss ordering, S corporation | Stock basis, then debt basis | § 1367(b)(2)(A) |
| Restoration ordering | Debt basis first, then stock basis | § 1367(b)(2)(B) |
| Carryforward | Indefinite | § 704(d), § 1366(d)(2) |
| Distribution above basis | Capital gain | § 731, § 1368 |
| Transfer to a spouse | Suspended losses transfer, S corporations | § 1366(d)(2)(B) |
| Post-termination transition period | Losses usable against restored stock basis | § 1366(d)(3) |

### 11. References

[66] 26 U.S.C. § 1366, *Pass-thru of items to shareholders*. United States Code, Office of the Law Revision Counsel. https://www.govinfo.gov/app/collection/uscode

[67] 26 U.S.C. § 1367, *Adjustments to basis of stock of shareholders*. https://www.govinfo.gov/app/collection/uscode

[68] 26 U.S.C. §§ 704(d), 705 and 752. https://www.govinfo.gov/app/collection/uscode

[69] Treas. Reg. §§ 1.752-1 to 1.752-3. Electronic Code of Federal Regulations. https://www.ecfr.gov/current/title-26

### 12. Status in This System

| Layer | Status |
|---|---|
| Projection engine | **Applied in part.** The basis limitation is implemented as the first gate, ahead of at-risk and passive, which is the statutory order. Losses are limited to the entered basis, basis is reduced as losses are allowed, and the amount suspended for want of basis is tracked **separately** from the amounts suspended at the other three gates — which is necessary, because each is released by a different event. The four-gate function asserts a conservation identity across all four categories. |
| Backend (`tax-be`) | **Not applied.** `strategyPhaseMap.js` catalogues "§704(d) Partner Basis Limitation Review", "§1366(d) Shareholder Basis Limitation Optimization", "S-Corp Shareholder Basis Restoration (§1366(d))" and "Partnership Basis Restoration & §704(d) Loss Planning" as named strategies. None is computed. |
| Known limitations | Basis is entered as an opening figure and only ever **decreases**. It is not increased by income or by contributions and not reduced by distributions, so it drifts from the true figure in any year the entity is profitable or cash is taken out, and a distribution in excess of basis never produces the capital gain the statute requires. The engine draws **no distinction between a partnership and an S corporation**: a partner's § 752 share of entity liabilities is not added to basis, and the corresponding rule that entity debt gives an S corporation shareholder nothing is not enforced. There is no separate debt basis, so the § 1367(b)(2) ordering — losses against stock basis first, restoration to debt basis first — cannot be represented, and neither can the distribution trap that follows from it. The § 1366(d)(3) post-termination transition period and the § 1041 transfer of suspended losses to a spouse are absent. |


---

## Module 27 — Net Operating Losses

**Tax year:** 2026 · **As of:** September 2026 · **Primary authority:** IRC § 172

---

### 1. Overview and Purpose

A net operating loss arises where allowable deductions exceed gross income for the year. Section 172 permits the excess to be carried to another year and deducted there, so that a business taxed on a single year's profit is not penalised for the volatility of its results.

The Tax Cuts and Jobs Act changed the provision fundamentally and the change is permanent. A loss arising in a taxable year beginning after 2017 may be carried **forward indefinitely** but generally **not carried back**, and the deduction in any year is limited to **80 percent of taxable income**.[70] The consequence is that a taxpayer with an enormous carryforward still pays tax on 20 percent of income in every year — the loss defers tax, it no longer eliminates it.

For this system the provision matters mainly as the destination of amounts disallowed elsewhere. An excess business loss under § 461(l) is not lost; it becomes a net operating loss in the following year and then meets the 80 percent limitation on arrival. Module 18 describes the first stage and this module the second, and the two together explain why a large deduction concentrated in one year is worth considerably less than its face amount.

### 2. Governing Law and Authorities

| Type | Citation | What it establishes |
|---|---|---|
| Statute | IRC § 172(a)(1) | Pre-2021 rule |
| Statute | IRC § 172(a)(2) | The 80 percent limitation for post-2017 losses |
| Statute | IRC § 172(b)(1)(A) | Indefinite carryforward for post-2017 losses; 20 years for earlier ones |
| Statute | IRC § 172(b)(1)(B) | Two-year carryback for farming losses |
| Statute | IRC § 172(d) | Modifications in computing the loss |
| Statute | IRC § 461(l)(2) | Excess business loss becomes a net operating loss |
| Statute | IRC § 382 | Limitation after an ownership change |
| Legislation | P.L. 115-97 | Removed the carryback and imposed the 80 percent limitation |

### 3. Key Definitions

| Term | Definition |
|---|---|
| **Net operating loss** | The excess of deductions over gross income, computed with the modifications in § 172(d). |
| **Carryforward** | A loss applied against income of a later year. |
| **80 percent limitation** | The cap on the deduction for post-2017 losses, measured against taxable income computed **without** § 172, § 199A and § 250.[70] |
| **Pre-2018 loss** | A loss arising in a taxable year beginning before 1 January 2018. Carried forward 20 years and **not** subject to the 80 percent limitation. |
| **Ownership change** | A more than 50 percentage point shift in ownership over a testing period, which limits the use of the loss under § 382. |

### 4. Who Is Affected

Individuals, estates, trusts and corporations. For an individual, the loss must arise from business activity; § 172(d) removes personal deductions, the standard deduction, and non-business capital losses in excess of non-business capital gains from the computation, so a large investment loss or a big charitable gift does not create a net operating loss.

The taxpayers most affected are business owners with volatile results, and anyone whose deductions have been deferred into a carryforward by the excess business loss limitation.

### 5. Core Rules and Calculations

#### 5.1 Case Register

| # | Case | Applied |
|---|---|---|
| 1 | Loss carried forward indefinitely | Yes |
| 2 | No carryback for post-2017 losses | Yes, by omission |
| 3 | 80 percent of taxable income limitation | Yes |
| 4 | Limitation measured before § 199A and § 250 | **No** |
| 5 | Pre-2018 losses deducted in full, ahead of later ones | **No** |
| 6 | Twenty-year expiry for pre-2018 losses | **No** |
| 7 | § 461(l) excess business loss becoming an NOL | Yes |
| 8 | § 172(d) modifications to the computation | **No** |
| 9 | Farming loss two-year carryback | **No** |
| 10 | § 382 limitation after an ownership change | **No** |
| 11 | Ordering: oldest loss used first | **No** — a single pooled balance |
| 12 | Carryforward extinguished at death | **No** |

#### 5.2 The computation

For a taxable year beginning after 2020, the deduction is:

```
   the whole of any pre-2018 losses carried to the year
 + the lesser of
       post-2017 losses carried to the year, or
       80% × ( taxable income before § 172, § 199A and § 250
               − the pre-2018 amount already used )
```

The exclusion of § 199A and § 250 from the base is a specific ordering rule. Taxable income for this purpose is computed **before** the qualified business income deduction, so the 80 percent ceiling is measured against a larger figure than final taxable income.

#### 5.3 The 80 percent limitation in operation

A carryforward of $500,000 against varying income:

| Year | Taxable income before the loss | 80% ceiling | Deducted | Taxable income after | Remaining |
|---|---|---|---|---|---|
| 1 | $200,000 | $160,000 | $160,000 | **$40,000** | $340,000 |
| 2 | $300,000 | $240,000 | $240,000 | **$60,000** | $100,000 |
| 3 | $150,000 | $120,000 | $100,000 | $50,000 | $0 |
| 4 | $400,000 | $320,000 | $0 | $400,000 | $0 |

Twenty percent of income is taxed in years 1 and 2 despite a carryforward far exceeding it. Under the pre-2018 rules the loss would have eliminated the liability in both years entirely.

#### 5.4 The pipeline from § 461(l)

The two provisions operate in sequence and the combined effect is a two-stage deferral:

```
Year 1   business loss                                     800,000
         § 461(l) threshold, joint                         512,000
         excess business loss disallowed                   288,000
         allowed against other income in year 1            512,000

Year 2   the 288,000 arrives as a net operating loss
         taxable income before the loss                    200,000
         § 172 ceiling, 80%                                160,000
         deducted                                          160,000
         remaining carryforward                            128,000
```

The $288,000 disallowed in year one is not restored in year two. It is capped again on arrival, and $128,000 moves on to year three.

#### 5.5 Ordering, expiry and ownership changes

**Ordering.** Pre-2018 losses are deducted first and in full, because they are not subject to the 80 percent limitation. Within each category the oldest loss is used first.

**Expiry.** A pre-2018 loss expires 20 years after the year in which it arose. A post-2017 loss does not expire.

**Ownership change.** Section 382 limits the annual use of a corporation's loss after a more than 50 percentage point ownership shift, to roughly the value of the corporation multiplied by a published long-term tax-exempt rate. This matters on the sale or recapitalisation of a loss-making company, and it can make a carryforward substantially less valuable to a buyer than its face amount.

**Death.** An individual's net operating loss carryforward is extinguished on death. It does not pass to the estate or to heirs. Where a large carryforward exists, generating income to absorb it during life is worth doing.

### 6. Examples and Case Calculations

#### Example 1 — Volatility across a cycle

A business owner with results of −$400,000, $250,000 and $350,000 over three years, filing jointly.

```
Year 1   loss                                             400,000
         within the § 461(l) threshold of 512,000, so allowed in full
         no other income, so an NOL of                    400,000 arises

Year 2   taxable income before the loss                   250,000
         § 172 ceiling  80% × 250,000                     200,000
         deducted                                         200,000
         taxable income                                    50,000
         carryforward remaining                           200,000

Year 3   taxable income before the loss                   350,000
         § 172 ceiling  80% × 350,000                     280,000
         deducted                                         200,000
         taxable income                                   150,000
         carryforward remaining                                 0
```

Over three years the owner earned $200,000 net and paid tax on $200,000. The timing differs from the economics by two years, and tax was paid in year 2 despite a carryforward twice the size of the income.

#### Example 2 — The interaction with the qualified business income deduction

A taxpayer with $300,000 of taxable income before the net operating loss and the § 199A deduction, and a $500,000 carryforward.

```
§ 172 ceiling, measured before § 199A
   80% × 300,000                                          240,000
Deducted                                                  240,000
Taxable income before § 199A                               60,000

§ 199A deduction, 20% of qualified business income,
   capped at 20% of taxable income less net capital gain
   20% × 60,000                                            12,000
Final taxable income                                       48,000
```

Measuring the ceiling before the § 199A deduction gives a larger allowance than measuring it afterwards would. Reversing the order would produce a smaller deduction and a circular computation.

#### Example 3 — What the carryforward is worth to a buyer

A corporation with a $5,000,000 carryforward is sold, triggering an ownership change under § 382.

```
Value of the corporation                                4,000,000
Long-term tax-exempt rate, illustrative                      4.0%
Annual § 382 limitation                                   160,000
Years to use the carryforward                        31.25 years
```

Face value $5,000,000; usable at $160,000 a year. A buyer valuing the loss at its face amount will overpay substantially, and the § 382 calculation is a standard part of pricing a loss-making acquisition.

### 7. Interactions with Other Rules

**Excess business loss (Module 18).** The principal source of net operating losses for an individual in this system. The § 461(l) disallowance converts to an NOL in the following year and meets the 80 percent limitation there.

**Qualified business income (Module 17).** The § 172 ceiling is measured before the § 199A deduction, and the § 199A deduction is then computed on income already reduced by the net operating loss.

**Basis, at-risk and passive limitations (Modules 23, 25 and 26).** All four loss gates come before a net operating loss can arise. Only a loss that has survived all of them and exceeds other income becomes an NOL.

**Capital losses (Module 24).** Non-business capital losses in excess of non-business capital gains are removed from the net operating loss computation by § 172(d), so an investment loss does not create one.

**Roth conversions (Module 10).** A conversion in a year with a large carryforward is unusually cheap, because the conversion income is absorbed at up to 80 percent by the loss. This is one of the few places where a bad business year creates a genuine opportunity.

### 8. Common Scenarios and Edge Cases

**Twenty percent of income is always taxed.** However large the carryforward, a post-2017 loss cannot eliminate a year's liability entirely.

**There is no carryback.** A loss cannot be used to reclaim tax paid in an earlier profitable year, other than for farming losses. This removed a significant source of liquidity for volatile businesses.

**Post-2017 losses never expire**, so there is no urgency to use them beyond the time value of money — and no protection either, since they die with the taxpayer.

**Pre-2018 losses are better.** They are used first, are not capped at 80 percent, and expire after 20 years.

**The ceiling is measured before § 199A.** This is favourable and is easy to get wrong.

**Personal deductions do not create a net operating loss.** Section 172(d) removes the standard deduction and non-business items from the computation.

**A carryforward dies with the taxpayer.** Unlike a basis step-up, it confers nothing on heirs.

**Section 382 can render a corporate carryforward nearly worthless** after an ownership change, and the limitation is annual rather than absolute.

### 9. Planning Implications

A large carryforward is a reason to accelerate income, not to defer it. Roth conversions, gain realisation and the exercise of options are all cheaper in a year when 80 percent of the resulting income is absorbed by the loss.

Because the carryforward is extinguished at death, an older taxpayer holding one should be shown a plan to use it. The alternative is that it disappears.

Where a business is likely to be sold, the § 382 limitation should be modelled before the carryforward is treated as an asset in the price.

For a taxpayer facing a large accelerated deduction — a cost segregation study, for instance — the pipeline in § 5.4 is the reason to consider spreading it. A deduction that creates an excess business loss is deferred once by § 461(l) and then capped again by § 172, so its present value can be materially below its face amount. Electing out of bonus depreciation for one class of property, as Module 22 sets out, may produce a better result than the largest possible first-year deduction.

### 10. Data Tables for the Engine

| Constant | Value | Source |
|---|---|---|
| Limitation on post-2017 losses | 80 percent of taxable income | § 172(a)(2)(B)(ii) |
| Base for the limitation | Taxable income before § 172, § 199A and § 250 | § 172(a)(2)(B)(ii)(I) |
| Carryforward, post-2017 | Indefinite | § 172(b)(1)(A)(ii)(II) |
| Carryforward, pre-2018 | 20 years | § 172(b)(1)(A)(ii)(I) |
| Carryback | None, except 2 years for farming losses | § 172(b)(1)(B) |
| Ordering | Pre-2018 losses first, then oldest post-2017 | § 172(a)(2) |
| Source from § 461(l) | Excess business loss becomes an NOL in the next year | § 461(l)(2) |
| Death | Carryforward extinguished | — |

### 11. References

[70] 26 U.S.C. § 172, *Net operating loss deduction*. United States Code, Office of the Law Revision Counsel. https://www.govinfo.gov/app/collection/uscode

[46] 26 U.S.C. § 461(l). https://www.govinfo.gov/app/collection/uscode

[71] 26 U.S.C. § 382, *Limitation on net operating loss carryforwards and certain built-in losses following ownership change*. https://www.govinfo.gov/app/collection/uscode

### 12. Status in This System

| Layer | Status |
|---|---|
| Projection engine | **Applied.** The 80 percent limitation is implemented, the carryforward is indefinite with no carryback, and amounts disallowed by the excess business loss limitation are correctly added to the net operating loss balance rather than discarded — so the two-stage pipeline in § 5.4 behaves as the statute requires. |
| Backend (`tax-be`) | **Not applied.** `strategyPhaseMap.js` catalogues "§172 Net Operating Loss Carryforward Planning (C-Corp)", "NOL Carryforward Optimization & Utilization Planning (§172)", "Net Operating Loss (NOL) Strategy" and "§382 NOL Limitation — Ownership Change Risk Assessment". None is computed. |
| Known limitations | The 80 percent ceiling is measured against taxable income as the engine computes it rather than against taxable income determined **before** the § 199A deduction, which understates the ceiling for any taxpayer claiming § 199A. Losses are held as a single pooled balance, so pre-2018 losses are not deducted first and in full, the 20-year expiry for those losses is not applied, and the oldest-first ordering within the post-2017 category is not tracked. The § 172(d) modifications are not applied, so the engine does not test whether a loss is genuinely a net operating loss rather than the product of personal deductions. Farming carrybacks and the § 382 ownership-change limitation are absent, and the carryforward is not extinguished at death. |


---

## Module 28 — Federal Estate Tax

**Tax year:** 2026 · **As of:** September 2026 · **Primary authority:** IRC §§ 2001, 2010, 2031–2056

---

### 1. Overview and Purpose

The estate tax is imposed on the transfer of the taxable estate of every decedent who is a citizen or resident of the United States. It is a **transfer** tax, computed on the value of everything owned or controlled at death, not an income tax and not a tax on the recipient.

For 2026 the basic exclusion amount is **$15,000,000**, raised from $13,990,000 by the One Big Beautiful Bill Act and — importantly — made **permanent**.[72] The scheduled reversion to roughly half that figure after 2025 no longer exists. A married couple with a portability election can shelter $30,000,000.

At those levels the tax reaches very few estates directly, and for most households in this system the estate module matters for three other reasons. Life insurance is included in the estate where the decedent held incidents of ownership, which can push an otherwise modest estate over the line. Pre-tax retirement accounts are **income in respect of a decedent** and receive no basis step-up, so they are taxed twice where the estate is taxable. And several states impose their own estate tax at thresholds far below the federal figure, some with a cliff that taxes the entire estate once the threshold is passed.

### 2. Governing Law and Authorities

| Type | Citation | What it establishes |
|---|---|---|
| Statute | IRC § 2001(a), (c) | Imposition of tax and the rate schedule |
| Statute | IRC § 2010(c) | Applicable credit; basic exclusion amount; portability |
| Statute | IRC § 2031 | Definition of the gross estate |
| Statute | IRC § 2032 | Alternate valuation date |
| Statute | IRC § 2033 | Property in which the decedent had an interest |
| Statute | IRC § 2035 | Transfers within three years of death |
| Statute | IRC § 2042 | Proceeds of life insurance |
| Statute | IRC § 2053 | Deductions for expenses, debts and claims |
| Statute | IRC § 2055 | Charitable deduction |
| Statute | IRC § 2056 | Unlimited marital deduction |
| Statute | IRC § 2631(c) | Generation-skipping transfer exemption |
| Statute | IRC § 691 | Income in respect of a decedent |
| Legislation | P.L. 119-21, § 70106 | Raised the exclusion to $15,000,000 and made it permanent |
| Guidance | Rev. Proc. 2025-32, § 3.14 | 2026 exclusion and generation-skipping exemption |

### 3. Key Definitions

| Term | Definition |
|---|---|
| **Gross estate** | Everything the decedent owned or controlled at death, at fair market value, including property passing outside probate. |
| **Basic exclusion amount** | $15,000,000 for 2026, indexed from a 2025 base.[73] |
| **Applicable exclusion amount** | The basic exclusion amount plus any deceased spousal unused exclusion. |
| **DSUE** | Deceased spousal unused exclusion — the portion of a predeceased spouse's exclusion not used, available to the survivor if elected. |
| **Portability** | The election, made on a timely Form 706, that transfers the DSUE to the surviving spouse. |
| **Income in respect of a decedent** | Income the decedent had a right to receive but had not recognised. Taxed to the recipient and **not** given a basis step-up. |

### 4. Who Is Affected

Estates of decedents dying after 31 December 2025 with a gross estate, plus adjusted taxable gifts, exceeding $15,000,000 — or a lower figure where lifetime gifts have consumed part of the exclusion.

Filing is required where the gross estate exceeds the exclusion. A return is also filed, voluntarily, to elect portability, and § 5.4 explains why that election is usually worth making even for a small estate.

Non-resident aliens are subject on United States situs property with an exclusion of only $60,000, which is a very different regime and outside the scope of this projection.

### 5. Core Rules and Calculations

#### 5.1 Case Register

| # | Case | Applied |
|---|---|---|
| 1 | Gross estate valued at date of death | Yes |
| 2 | § 2010(c) basic exclusion of $15,000,000 | Yes |
| 3 | Exclusion indexed | Partially — by the engine's general factor |
| 4 | § 2001(c) rate, 40 percent on the excess | Yes |
| 5 | § 2053 deduction for debts | Yes |
| 6 | Prior taxable gifts reducing the exclusion | Yes |
| 7 | DSUE from a predeceased spouse | Yes — taken as an input |
| 8 | Portability requires a timely Form 706 | **No** |
| 9 | § 2056 unlimited marital deduction | Partially |
| 10 | § 2055 charitable deduction | **No** |
| 11 | § 2042 life insurance included where incidents of ownership are held | Yes |
| 12 | § 2035 three-year rule for transferred policies | Yes |
| 13 | § 2032 alternate valuation date | **No** |
| 14 | § 2032A special use valuation | **No** |
| 15 | § 691 income in respect of a decedent | Yes — heir rate applied |
| 16 | § 691(c) deduction for estate tax on the IRD | **No** |
| 17 | § 2631 generation-skipping transfer tax | **No** |
| 18 | State estate tax | Yes, for the listed states |
| 19 | State cliff structures | Yes — the New York 105 percent cliff |
| 20 | Non-resident alien regime | Not applicable |

#### 5.2 The computation

```
gross estate
  − debts and administration expenses, § 2053
  − marital deduction, § 2056
  − charitable deduction, § 2055
                                    = taxable estate
  + adjusted taxable gifts
                                    = the base for the tentative tax

tentative tax at the § 2001(c) rates
  − applicable credit (the exclusion, plus any DSUE)
                                    = estate tax payable
```

**On the rate.** Section 2001(c) is a graduated schedule running from 18 percent to 40 percent, with the top rate beginning at $1,000,000 of cumulative taxable transfers. Because the exclusion of $15,000,000 absorbs every bracket below the 40 percent band, **every dollar above the exclusion is taxed at exactly 40 percent**. Applying a flat 40 percent to the excess is not an approximation; it is the correct answer.

| Gross estate | Exclusion | Taxable | Tax |
|---|---|---|---|
| $10,000,000 | $15,000,000 | $0 | $0 |
| $15,000,000 | $15,000,000 | $0 | $0 |
| $20,000,000 | $15,000,000 | $5,000,000 | **$2,000,000** |
| $30,000,000 | $15,000,000 | $15,000,000 | **$6,000,000** |

#### 5.3 What is in the gross estate

| Included | Authority |
|---|---|
| Property owned outright | § 2033 |
| The decedent's share of jointly held property | § 2040 |
| Life insurance where the decedent held **incidents of ownership** | § 2042 |
| Life insurance transferred within **three years** of death | § 2035 |
| Retirement accounts and annuities | § 2039 |
| Property over which the decedent held a general power of appointment | § 2041 |
| Revocable trust assets | § 2038 |

A revocable living trust avoids probate. It does **not** remove anything from the gross estate, because the decedent retained the power to revoke. This is the most commonly misunderstood point in estate planning.

#### 5.4 Portability, and why the election matters

Section 2010(c) permits the unused portion of a deceased spouse's exclusion to pass to the survivor, but **only if a Form 706 is filed** for the first estate and the election is made — even where no tax is due and no return would otherwise be required.

A couple with $28,000,000, unequally owned:

```
WITH the election
   First death — spouse A owns 8,000,000, all to spouse B
      unlimited marital deduction, no tax
      A's unused exclusion of 15,000,000 elected as DSUE
   Second death — B's estate 28,000,000
      exclusion 15,000,000 own + 15,000,000 DSUE = 30,000,000
      taxable 0                                      tax $0

WITHOUT the election
   Second death — B's exclusion alone            15,000,000
      taxable 13,000,000                          tax $5,200,000
```

The cost of not filing a return at the first death is **$5,200,000**. The election is due nine months after death, extendable to fifteen months, with a simplified late-election procedure available for several years afterwards in estates below the filing threshold.

The DSUE is **not indexed** after it is fixed. The survivor's own exclusion continues to grow with inflation; the inherited amount does not.

#### 5.5 Income in respect of a decedent

A pre-tax retirement account is income in respect of a decedent under § 691. Two consequences follow:

- It receives **no basis step-up** under § 1014. The heir inherits the decedent's basis, which for a fully deductible account is zero.
- It is included in the gross estate at full value, and the heir then pays income tax on withdrawal.

```
Pre-tax account in a taxable estate                2,000,000
   Estate tax at 40 percent                          800,000
   Heir's income tax at 35 percent on the remainder  420,000
                                                   ---------
   Combined                                        1,220,000    61.0 percent
```

Section 691(c) allows the heir an itemised deduction for the estate tax attributable to the income in respect of a decedent, which reduces the double burden materially. It is frequently unclaimed, because the heir has to know the estate tax computation to calculate it.

The comparison with a taxable account is stark. A taxable investment account of the same value receives a full step-up, so the heir pays no income tax on the accumulated gain at all. **A dollar in a pre-tax account is worth materially less to an heir than a dollar in a taxable account**, and Module 31 develops the point.

#### 5.6 State estate taxes

Several states impose their own tax at thresholds far below the federal exclusion, and there is no portability between the two systems. Two structures matter:

- **Ordinary threshold.** Tax applies only to the excess over the state exclusion.
- **Cliff.** Once the estate exceeds a stated multiple of the threshold, the **entire** estate becomes taxable, not merely the excess. New York applies this at 105 percent of its threshold, which produces a marginal rate approaching infinity at the cliff edge.

A resident of a cliff state whose estate is close to the threshold has a very strong reason to make charitable or lifetime gifts sufficient to stay below it.

### 6. Examples and Case Calculations

#### Example 1 — Life insurance pushing an estate over the line

An estate of $13,000,000 plus a $4,000,000 policy the decedent owned.

```
Assets                                            13,000,000
Life insurance, § 2042 incidents of ownership      4,000,000
                                                  ----------
Gross estate                                      17,000,000
Exclusion                                        −15,000,000
                                                  ----------
Taxable                                            2,000,000
Tax at 40 percent                                   $800,000
```

Had the policy been owned by an irrevocable trust from inception, the proceeds would have been outside the estate and no tax would arise. Transferring an existing policy to a trust works only if the insured survives **three years** — § 2035 pulls it back otherwise.

#### Example 2 — The three-year rule

The decedent transferred the policy to a trust 26 months before death.

```
Transfer within three years, § 2035
   Proceeds included in the gross estate anyway     4,000,000
   Tax at 40 percent                                 $800,000
```

The transfer achieved nothing for estate tax purposes. A new policy purchased **by** the trust, rather than transferred to it, has no three-year exposure at all.

#### Example 3 — Annual exclusion gifting

A couple with six children and grandchildren, gift-splitting under § 2513, using the $19,000 annual exclusion over twenty years.

```
6 donees × 20 years × $19,000                      2,280,000
With gift-splitting, both spouses                  4,560,000
Removed from the estate                            4,560,000
Estate tax saved at 40 percent                    $1,824,000
```

Plus all growth on the gifted assets after the date of the gift, which is often the larger part of the benefit. Annual exclusion gifts do not consume any part of the $15,000,000 exclusion.

#### Example 4 — A cliff state

An estate of $7,800,000 in a state with a $7,350,000 threshold and a 105 percent cliff.

```
105 percent of the threshold                       7,717,500
Estate                                             7,800,000  — above the cliff
Taxable base                                       7,800,000  — the ENTIRE estate
```

A charitable gift of $500,000 would bring the estate to $7,300,000, below the threshold entirely, and eliminate the state tax on the whole amount. The gift costs less than the tax it avoids.

### 7. Interactions with Other Rules

**Step-up in basis (Module 31).** The other side of death. Property receives a basis step-up under § 1014; income in respect of a decedent does not.

**Life insurance (Module 30).** Sections 2042 and 2035 decide whether proceeds are in the estate, and Module 30 treats ownership structures.

**Gift tax (Module 29).** A unified system. Lifetime gifts above the annual exclusion consume the same $15,000,000.

**Required distributions (Module 09).** Reducing a pre-tax balance before death reduces the amount that will be income in respect of a decedent.

**Roth conversions (Module 10).** A conversion shifts the income tax burden from the heir to the owner at the owner's own rate, and reduces the estate by the tax paid. For a taxable estate it does both jobs at once.

**Passive activity losses (Module 25).** Section 469(g)(2) allows suspended losses at death only to the extent they exceed the basis step-up, so they are usually lost.

**Capital loss carryforwards (Module 24).** Extinguished at death.

### 8. Common Scenarios and Edge Cases

**The exclusion is permanent now.** The scheduled reversion after 2025 was removed by P.L. 119-21. Plans built on a sunset assumption should be revisited.

**A revocable trust does not reduce the gross estate.** It avoids probate and nothing more.

**Portability requires a filed return.** No return, no DSUE — and the cost can be millions.

**The DSUE is frozen; the survivor's own exclusion is not.** Over a long survivorship the inherited amount loses real value.

**Life insurance is in the estate if the decedent held incidents of ownership** — the right to change the beneficiary, to borrow against the policy, or to surrender it. Merely paying the premiums is not an incident of ownership.

**The three-year rule catches transferred policies**, not policies bought by the trust in the first place.

**Retirement accounts are the worst asset to leave to a taxable estate** and the best to leave to charity, which pays no income tax on them.

**Annual exclusion gifts do not consume the lifetime exclusion**, and their growth escapes as well.

**State thresholds are much lower**, and a cliff structure taxes the whole estate rather than the excess.

**The marital deduction defers rather than exempts.** Everything left to a spouse is untaxed at the first death and fully in the estate at the second.

### 9. Planning Implications

Portability should be treated as a default. Filing a Form 706 at the first death costs a professional fee and preserves an exclusion worth up to $6,000,000 of tax. Not filing is the single most expensive omission available in this area.

For a household near a state threshold — particularly a cliff state — the state tax is the binding constraint long before the federal tax is, and charitable or lifetime gifting is the ordinary response.

Life insurance intended to fund estate liquidity should be owned outside the estate from inception. Buying a policy inside an irrevocable trust avoids the three-year rule entirely; transferring an existing policy starts a three-year clock.

Where an estate will be taxable and includes large pre-tax retirement balances, Roth conversions during life do double duty: they reduce the estate by the tax paid and remove the income in respect of a decedent problem for the heir.

Charitable bequests should be funded from pre-tax retirement accounts wherever possible. A charity pays no income tax on the distribution, so the full amount reaches the charity, while the same amount left to a child is reduced twice.

### 10. Data Tables for the Engine

| Constant | 2026 value | Indexed |
|---|---|---|
| Basic exclusion amount | **$15,000,000** | Yes, from a 2025 base |
| Top rate, and the effective rate on the excess | **40 percent** | Fixed |
| 40 percent bracket begins | $1,000,000 of cumulative transfers | Fixed |
| Generation-skipping transfer exemption | **$15,000,000** | Yes |
| Annual gift exclusion | **$19,000** | Yes |
| Gift to a non-citizen spouse | **$194,000** | Yes |
| Marital deduction | Unlimited, citizen spouse | § 2056 |
| Charitable deduction | Unlimited | § 2055 |
| Three-year rule for transferred policies | 3 years | § 2035 |
| Portability election | Form 706, 9 months, extendable to 15 | § 2010(c)(5) |
| DSUE indexation | **None once fixed** | — |

### 11. References

[72] One Big Beautiful Bill Act, P.L. 119-21, § 70106, amending IRC § 2010(c)(3). https://www.govinfo.gov/content/pkg/PLAW-119publ21/html/PLAW-119publ21.htm

[73] Internal Revenue Service, *Revenue Procedure 2025-32*, § 3.14 and § 4.42. https://www.irs.gov/pub/irs-drop/rp-25-32.pdf

[74] 26 U.S.C. §§ 2001, 2010, 2031–2056, 2631 and 691. United States Code, Office of the Law Revision Counsel. https://www.govinfo.gov/app/collection/uscode

### 12. Status in This System

| Layer | Status |
|---|---|
| Projection engine | **Applied.** The exclusion of $15,000,000, the 40 percent rate and the $19,000 annual gift exclusion all match Revenue Procedure 2025-32. The flat 40 percent applied to the excess is **exactly correct**, not an approximation, because the exclusion absorbs every bracket below the 40 percent band. Prior taxable gifts reduce the exclusion, a deceased spousal unused exclusion is accepted as an input and added to it, and debts are deducted. Life insurance is included where incidents of ownership are held, and the § 2035 three-year rule is applied to transferred policies. State estate taxes are modelled for the states that impose them, **including the New York cliff at 105 percent of the threshold**, which taxes the entire estate rather than the excess — a structure most models omit. Income in respect of a decedent is recognised and the heir's income tax on inherited pre-tax balances is applied at an assumed rate. |
| Backend (`tax-be`) | **Not applied.** The roadmap projection allocates 3 percent of deployed savings to a "legacy" bucket and compounds it; there is no transfer tax computation. |
| Known limitations | The generation-skipping transfer tax is absent entirely, and the $15,000,000 § 2631(c) exemption is not held as a constant. The § 691(c) deduction for the estate tax attributable to income in respect of a decedent is not applied, so the double-tax figure in § 5.5 is overstated for a taxable estate. Portability is accepted as an input without testing whether a Form 706 was or could be filed, and the deceased spousal unused exclusion is inflated forward by the general factor although it is **frozen** once fixed. The § 2055 charitable deduction is not modelled, which matters for the cliff-state planning in Example 4. The § 2032 alternate valuation date and § 2032A special use valuation are absent. The exclusion is indexed by the engine's general inflation factor rather than by the § 2010(c)(3) mechanism from its 2025 base. |


---

## Module 29 — Gift Tax

**Tax year:** 2026 · **As of:** September 2026 · **Primary authority:** IRC §§ 2501–2524

---

### 1. Overview and Purpose

The gift tax applies to gratuitous transfers made during life. It exists to prevent the estate tax being avoided by giving property away before death, and the two are **unified**: a single $15,000,000 exclusion covers lifetime gifts and transfers at death together, and lifetime gifts that consume it reduce what remains at death.

Two exclusions sit outside that unified amount and are far more useful in practice than the headline figure. The **annual exclusion** under § 2503(b) permits $19,000 a year to each of any number of recipients, without limit on the number and without consuming any lifetime exclusion. And § 2503(e) excludes **unlimited** amounts paid directly to a school for tuition or to a provider for medical care.

The tax is paid by the **donor**, not the recipient. A gift is not income to the person receiving it, which is the point most often misunderstood by clients.

One asymmetry governs the planning. A gift carries the donor's **basis** to the recipient under § 1015; property inherited at death receives a **step-up** to fair market value under § 1014. Giving appreciated property during life therefore transfers an unrealised capital gain along with it, while holding the same property until death eliminates that gain entirely. Module 31 develops the comparison.

### 2. Governing Law and Authorities

| Type | Citation | What it establishes |
|---|---|---|
| Statute | IRC § 2501 | Imposition of the tax |
| Statute | IRC § 2502 | Rate schedule, unified with the estate tax |
| Statute | IRC § 2503(b) | Annual exclusion; present interest requirement |
| Statute | IRC § 2503(e) | Unlimited exclusion for tuition and medical payments |
| Statute | IRC § 2505 | Unified credit against gift tax |
| Statute | IRC § 2513 | Gifts by a spouse treated as made one half by each |
| Statute | IRC § 2522 | Charitable deduction |
| Statute | IRC § 2523 | Marital deduction; § 2523(i) for a non-citizen spouse |
| Statute | IRC § 1015 | Basis of property acquired by gift |
| Statute | IRC § 2035(b) | Gift tax paid within three years of death added back |
| Guidance | Rev. Proc. 2025-32, § 4.42 | 2026 annual exclusion amounts |

### 3. Key Definitions

| Term | Definition |
|---|---|
| **Present interest** | An unrestricted right to the immediate use, possession or enjoyment of property or of the income from it. Required for the annual exclusion. |
| **Future interest** | Any interest limited to commence at a future date. **Does not** qualify for the annual exclusion. |
| **Gift-splitting** | An election under § 2513 by which a gift by one spouse is treated as made one half by each, doubling the annual exclusion available. |
| **Adjusted taxable gifts** | Lifetime taxable gifts added back to the estate tax base at death, so the unified system is not gamed by timing. |
| **Crummey power** | A beneficiary's temporary right to withdraw a contribution to a trust, used to convert a future interest into a present interest. |

### 4. Who Is Affected

Any individual making a gratuitous transfer. A gift tax return, Form 709, is required where gifts to any one recipient exceed the annual exclusion, where a gift of a future interest is made whatever the amount, or where gift-splitting is elected.

Filing a return does not mean tax is payable. In practice almost no one pays gift tax; the return records the use of lifetime exclusion so that the estate tax computation at death is correct.

### 5. Core Rules and Calculations

#### 5.1 Case Register

| # | Case | Applied |
|---|---|---|
| 1 | § 2503(b) annual exclusion of $19,000 | Yes — as a constant |
| 2 | Annual exclusion per recipient, unlimited recipients | **No** |
| 3 | Present interest requirement | **No** |
| 4 | § 2513 gift-splitting | **No** |
| 5 | § 2503(e) unlimited tuition and medical exclusion | **No** |
| 6 | § 2523 unlimited marital deduction | **No** |
| 7 | § 2523(i) non-citizen spouse limit of $194,000 | **No** |
| 8 | § 2522 charitable deduction | **No** |
| 9 | Lifetime exclusion shared with the estate tax | Yes — prior gifts reduce the estate exclusion |
| 10 | Adjusted taxable gifts added back at death | Yes, in effect |
| 11 | § 1015 carryover basis to the donee | **No** |
| 12 | Dual basis rule for property gifted at a loss | **No** |
| 13 | § 2035(b) gift tax paid within three years added back | **No** |
| 14 | Form 709 filing requirement | Not applicable |

#### 5.2 The 2026 amounts

| Item | 2026 amount | Indexed |
|---|---|---|
| Annual exclusion, § 2503(b) | **$19,000** per recipient | Yes[75] |
| Gift to a non-citizen spouse, § 2523(i)(2) | **$194,000** | Yes |
| Lifetime exclusion, shared with the estate tax | **$15,000,000** | Yes |
| Rate on transfers above the exclusion | 40 percent | Fixed |
| Tuition and medical, § 2503(e) | **Unlimited** | — |
| Gift to a citizen spouse, § 2523 | **Unlimited** | — |
| Gift to charity, § 2522 | **Unlimited** | — |

#### 5.3 The annual exclusion

Section 2503(b) excludes the first $19,000 of gifts to **each** recipient in each calendar year. There is no limit on the number of recipients and no aggregate cap.

The exclusion applies only to a gift of a **present interest**. A transfer into a trust from which the beneficiary cannot draw is a future interest and does not qualify, however clearly it is intended for them. A **Crummey power** — a limited window, typically thirty days, in which the beneficiary may withdraw the contribution — converts the transfer into a present interest and preserves the exclusion. The power must be genuine and the beneficiary must be notified.

**Gift-splitting.** Section 2513 allows a married couple to treat a gift by one spouse as made one half by each, so a couple can give $38,000 to each recipient even where all the property belongs to one of them. The election is made on Form 709 and requires both spouses to consent.

#### 5.4 The tuition and medical exclusion

Section 2503(e) excludes, without limit and without consuming any exclusion:

- amounts paid **directly to an educational organisation** for tuition, and
- amounts paid **directly to a provider** for medical care.

Two constraints. The payment must go straight to the institution or provider — reimbursing the student or the patient does not qualify. And tuition means tuition: room, board, books and supplies are outside it.

For a grandparent funding education, this is materially better than the annual exclusion, because it is unlimited and can be used **in addition** to the $19,000.

#### 5.5 Basis — the reason not to give appreciated property

Section 1015 gives the donee the donor's basis, increased by any gift tax paid attributable to the appreciation. The unrealised gain travels with the asset.

Where the property's fair market value at the date of gift is **below** the donor's basis, a dual basis rule applies: the donee uses the donor's basis to compute a gain and the lower fair market value to compute a loss, so a sale between the two figures produces neither. The practical consequence is that a loss cannot be transferred by gift, and depreciated property should be sold by the donor so that the loss is realised.

| | Gift during life | Inheritance at death |
|---|---|---|
| Basis to the recipient | **Donor's basis**, § 1015 | **Fair market value**, § 1014 |
| Unrealised gain | Transferred to the recipient | **Eliminated** |
| Uses lifetime exclusion | Yes, above the annual exclusion | Yes |
| Future growth | Outside the donor's estate | Inside it |

The trade is between removing **future growth** from the estate and preserving the **step-up** on existing gain. Highly appreciated property is generally better held; property expected to grow sharply from a low basis is generally better given.

#### 5.6 Gift tax paid within three years of death

Section 2035(b) adds back to the gross estate any gift tax paid on gifts made within three years of death. This prevents the estate being reduced by the tax itself in a deathbed transfer. It applies to the **tax paid**, not to the gift, and does not affect gifts on which no tax was paid — which, given the $15,000,000 exclusion, is nearly all of them.

### 6. Examples and Case Calculations

#### Example 1 — Annual exclusion gifting at scale

A couple with three children, three children-in-law and six grandchildren — twelve recipients — gift-splitting.

```
Per recipient, both spouses    19,000 × 2        =    38,000
Twelve recipients                                     456,000  a year
Over fifteen years                                  6,840,000

Lifetime exclusion consumed                                 0
Estate tax saved at 40 percent                     $2,736,000
```

Plus all growth on the gifted property after the date of each gift. No return is required, because no gift to any one recipient exceeds the exclusion — except that gift-splitting itself requires a Form 709 to be filed to make the election.

#### Example 2 — Tuition paid directly

A grandparent pays $60,000 of university tuition directly to the institution and also gives the grandchild $19,000 in cash.

```
Tuition paid directly, § 2503(e)                       60,000    excluded
Cash gift, § 2503(b)                                   19,000    excluded
                                                       ------
Total removed from the estate                          79,000
Lifetime exclusion consumed                                 0
```

Paying the same $60,000 to the grandchild to settle their own bill would have been a taxable gift of $60,000, of which $41,000 would consume lifetime exclusion.

#### Example 3 — Giving appreciated stock, and the alternative

Shares worth $500,000 with a basis of $50,000. The donee is in the 15 percent capital gains bracket; the donor's estate is not taxable.

```
GIVE DURING LIFE
   Basis carries over, § 1015                          50,000
   Donee sells:  gain 450,000 × 15%                    67,500 of tax

HOLD UNTIL DEATH
   Basis steps up to 500,000, § 1014
   Heir sells immediately:  gain 0                          0 of tax
```

Where the estate is **not** taxable, holding is plainly better. Where the estate **is** taxable, the calculation reverses: removing $500,000 plus its future growth saves 40 percent estate tax, which exceeds the 15 or 20 percent capital gain the donee inherits.

#### Example 4 — A non-citizen spouse

A gift of $300,000 to a spouse who is not a United States citizen.

```
§ 2523 unlimited marital deduction — not available
§ 2523(i)(2) annual exclusion                         194,000
Taxable gift                                          106,000
Lifetime exclusion consumed                           106,000
```

The unlimited marital deduction is unavailable for a non-citizen spouse, because the property could leave the United States tax system. A qualified domestic trust achieves a similar deferral at death, but during life the $194,000 annual limit is the constraint.

### 7. Interactions with Other Rules

**Estate tax (Module 28).** Unified. Lifetime taxable gifts are added back as adjusted taxable gifts, so the exclusion is used once across both.

**Step-up in basis (Module 31).** The § 1015 carryover and the § 1014 step-up are the two halves of the same decision, and Example 3 sets out the trade.

**Life insurance (Module 30).** Premium payments to an irrevocable trust are gifts, and Crummey powers are what makes the annual exclusion available for them.

**Generation-skipping transfer tax.** A gift to a grandchild may attract it in addition to the gift tax, with a separate $15,000,000 exemption that must be allocated.

**Kiddie tax.** Income-producing property given to a child under 19, or a full-time student under 24, may have its income taxed at the parents' rate under § 1(g). Module 01 records that this is not modelled.

**Divorce (Module 36).** Transfers incident to divorce are outside the gift tax under § 2516 where they meet its conditions, and outside the income tax under § 1041.

### 8. Common Scenarios and Edge Cases

**The donor pays, not the recipient.** A gift is never income to the person receiving it.

**The annual exclusion is per recipient and uncapped in number.** Twelve recipients means twelve exclusions.

**A future interest does not qualify.** A gift into a trust needs a Crummey power to secure the exclusion, and the power must be real.

**Tuition and medical payments must go directly to the institution.** Reimbursement fails.

**Tuition means tuition.** Room, board and books are outside § 2503(e), though they can be covered by the annual exclusion.

**Gift-splitting requires a return** even where no gift exceeds the exclusion.

**Basis carries over on a gift.** Appreciated property transfers its gain; depreciated property should be sold rather than given, because the loss cannot be transferred.

**The non-citizen spouse limit is $194,000**, not unlimited.

**Paying someone else's tax or debt is a gift**, as is an interest-free loan to the extent of the forgone interest.

**Gifts to a § 529 plan may be front-loaded** by electing to treat a contribution as made over five years, giving $95,000 per beneficiary in one year, or $190,000 for a couple.

### 9. Planning Implications

Annual exclusion gifting is the most reliable estate reduction technique available, and its power comes from repetition and from the number of recipients rather than from the size of each gift. Example 1 removes $6,840,000 without touching the lifetime exclusion.

Direct payment of tuition and medical costs should be used before the annual exclusion, not after it, because it is unlimited and the annual exclusion then remains available for cash.

For a household whose estate will not be taxable — which, at a $15,000,000 exclusion per person, is most households — the analysis inverts. There is no estate tax to save, so the **step-up** is the valuable thing and appreciated property should be held rather than given. Advising annual gifting to a non-taxable estate transfers capital gains to the recipient for no benefit.

Where the estate will be taxable, gifting assets expected to appreciate sharply is worth more than gifting cash, because the future growth escapes as well as the principal.

The § 529 five-year election is a useful way to move a substantial sum for a grandchild in one year while keeping it within the annual exclusion.

### 10. Data Tables for the Engine

| Constant | 2026 value | Indexed |
|---|---|---|
| Annual exclusion, per recipient | **$19,000** | Yes |
| Non-citizen spouse annual limit | **$194,000** | Yes |
| Lifetime exclusion, unified | **$15,000,000** | Yes |
| Rate above the exclusion | 40 percent | Fixed |
| Tuition and medical, paid directly | Unlimited | § 2503(e) |
| Citizen spouse | Unlimited | § 2523 |
| Charity | Unlimited | § 2522 |
| Gift-splitting | Doubles the annual exclusion | § 2513 |
| § 529 front-loading | 5 years, $95,000 per beneficiary | § 529(c)(2)(B) |
| Basis to the donee | Donor's basis | § 1015 |
| Gift tax paid within 3 years of death | Added back to the estate | § 2035(b) |

### 11. References

[75] Internal Revenue Service, *Revenue Procedure 2025-32*, § 4.42. https://www.irs.gov/pub/irs-drop/rp-25-32.pdf

[76] 26 U.S.C. §§ 2501–2524 and 1015. United States Code, Office of the Law Revision Counsel. https://www.govinfo.gov/app/collection/uscode

[72] One Big Beautiful Bill Act, P.L. 119-21, § 70106. https://www.govinfo.gov/content/pkg/PLAW-119publ21/html/PLAW-119publ21.htm

### 12. Status in This System

| Layer | Status |
|---|---|
| Projection engine | **Applied in part.** The annual exclusion of $19,000 and the unified lifetime exclusion of $15,000,000 both match Revenue Procedure 2025-32. Prior taxable gifts reduce the exclusion available at death, so the unified structure is respected and the estate computation in Module 28 is correct on that point. |
| Backend (`tax-be`) | **Not applied.** `strategyPhaseMap.js` catalogues "Gifting Appreciated Stock to Family" and "Intra-Family Loans with AFR" as named strategies; neither is computed. |
| Known limitations | The annual exclusion is held as a constant but is **not applied per recipient**, so a gifting programme cannot be modelled — the engine has no concept of recipients, and Example 1 cannot be represented. Gift-splitting under § 2513 is absent, as is the present interest requirement and therefore any treatment of Crummey powers. The unlimited § 2503(e) exclusion for tuition and medical payments is not modelled, which understates what a client can move out of an estate. The § 2523 marital deduction and the $194,000 non-citizen limit are absent, as is the § 2522 charitable deduction. Most consequentially for a projection, **§ 1015 carryover basis is not applied**: property modelled as gifted does not carry the donor's basis to the recipient, so the central trade-off against the § 1014 step-up in Module 31 cannot be shown. The dual basis rule for property gifted at a loss and the § 2035(b) add-back of gift tax paid within three years of death are likewise absent. |


---

## Module 30 — Life Insurance and Estate Inclusion

**Tax year:** 2026 · **As of:** September 2026 · **Primary authority:** IRC §§ 101, 2035, 2042, 7702, 7702A

---

### 1. Overview and Purpose

Life insurance receives two distinct advantages, and they are governed by different provisions that are frequently conflated.

The **death benefit is excluded from gross income** under § 101(a)(1). This is nearly unconditional and applies whoever owns the policy.

The proceeds are **included in the gross estate** under § 2042 where the decedent held incidents of ownership, or where the policy was transferred within three years of death under § 2035. Income tax free and estate tax free are separate questions, and a policy can easily be the first without being the second.

A permanent policy also accumulates **cash value** that grows without current income tax under § 72(e), and can be accessed by withdrawal to basis and then by policy loan. Whether that access is tax free depends on whether the contract is a **modified endowment contract** under § 7702A, which turns on how quickly it was funded in its first seven years.

For a projection to age 90, insurance appears in three places: as a death benefit that may or may not be in the taxable estate, as a cash value asset on the balance sheet, and as a source of tax-advantaged liquidity in retirement. Each depends on structure decided years earlier.

### 2. Governing Law and Authorities

| Type | Citation | What it establishes |
|---|---|---|
| Statute | IRC § 101(a)(1) | Death benefit excluded from gross income |
| Statute | IRC § 101(a)(2) | Transfer for valuable consideration |
| Statute | IRC § 101(a)(3) | Reportable policy sales |
| Statute | IRC § 101(j) | Employer-owned contracts |
| Statute | IRC § 72(e) | Taxation of amounts not received as an annuity |
| Statute | IRC § 264 | Denial of interest deductions on policy loans |
| Statute | IRC § 2035(a) | Transfers within three years of death |
| Statute | IRC § 2042 | Proceeds of life insurance in the gross estate |
| Statute | IRC § 7702 | Definition of a life insurance contract |
| Statute | IRC § 7702A | Modified endowment contracts and the seven-pay test |
| Regulation | Treas. Reg. § 20.2042-1(c) | Meaning of incidents of ownership |

### 3. Key Definitions

| Term | Definition |
|---|---|
| **Incidents of ownership** | Any right in the policy of an economic nature — to change the beneficiary, surrender or cancel it, assign it, pledge it, or borrow against the cash value. |
| **Irrevocable life insurance trust** | A trust holding a policy so that the insured holds no incidents of ownership and the proceeds are outside the estate. |
| **Modified endowment contract** | A contract failing the seven-pay test of § 7702A(b), taxed on distributions income-first with a 10 percent additional tax before 59½. |
| **Seven-pay test** | The accumulated amount paid in the first seven contract years may not exceed the sum of the net level premiums that would have been paid had the contract provided paid-up benefits after seven level annual premiums.[77] |
| **Transfer for value** | A transfer of a policy for valuable consideration, which limits the income tax exclusion to the consideration plus subsequent premiums.[78] |

### 4. Who Is Affected

Anyone owning or insured under a life insurance contract. The estate consequence attaches to the **owner**, so the identity of the policyholder is what matters rather than who pays the premiums.

The exposure arises where an estate is close to or above the exclusion in Module 28, or where a state threshold is much lower. A $4,000,000 policy on a $13,000,000 estate is the difference between no federal tax and $800,000 of it.

### 5. Core Rules and Calculations

#### 5.1 Case Register

| # | Case | Applied |
|---|---|---|
| 1 | § 101(a)(1) death benefit excluded from income | Yes |
| 2 | § 101(a)(2) transfer for value | **No** |
| 3 | § 101(a)(3) reportable policy sale | **No** |
| 4 | § 101(j) employer-owned contracts | **No** |
| 5 | § 2042 inclusion where incidents of ownership are held | Yes |
| 6 | § 2035 three-year rule on a transferred policy | Yes |
| 7 | Policy owned by a trust from inception — no three-year exposure | Yes, in effect |
| 8 | § 7702 definitional limits on premium and cash value | **No** |
| 9 | § 7702A seven-pay test | **No** |
| 10 | Modified endowment contract distribution ordering | **No** |
| 11 | Non-MEC withdrawal to basis, then loans | Partially |
| 12 | § 72(e) inside build-up untaxed | Yes |
| 13 | Policy lapse with an outstanding loan | Partially |
| 14 | § 264 denial of interest deductions | **No** |
| 15 | Premium payments to a trust as gifts | **No** |
| 16 | Crummey powers securing the annual exclusion | **No** |

#### 5.2 Income tax — § 101

The death benefit is excluded from gross income. Three exceptions matter.

**Transfer for value, § 101(a)(2).** Where a policy is transferred for valuable consideration, the exclusion is limited to the consideration paid plus subsequent premiums. The excess is ordinary income to the recipient. There are safe harbours: a transfer to the **insured**, to a **partner of the insured**, to a **partnership in which the insured is a partner**, or to a **corporation in which the insured is a shareholder or officer**, and any transfer with a carryover basis.[78]

Note what is absent from that list. A transfer to a **co-shareholder** is not protected. A cross-purchase buy-sell arrangement in which shareholders buy policies from one another falls outside the safe harbour, while a transfer to the corporation itself is inside it. This is a well-known trap in buy-sell planning.

**Reportable policy sale, § 101(a)(3).** Where the acquirer has no substantial family, business or financial relationship with the insured apart from the policy, the safe harbours do not apply. This targets the life settlement market.

**Employer-owned contracts, § 101(j).** Notice and consent requirements must be met before the policy is issued, or the exclusion is limited to premiums paid.

#### 5.3 Estate tax — § 2042 and § 2035

Proceeds are in the gross estate where the decedent possessed **any incident of ownership** at death. The list in Treas. Reg. § 20.2042-1(c) is broad: the right to change the beneficiary, to surrender or cancel, to assign, to pledge, or to borrow against the cash value. Paying the premiums is **not** an incident of ownership.

Where an existing policy is transferred to remove those incidents, § 2035 pulls the proceeds back into the estate if the insured dies within **three years**. A policy purchased by an irrevocable trust at inception has no such exposure, because there was never a transfer.

The practical rule follows directly: for a new policy intended to be outside the estate, the **trust should apply for and own the policy from the start**. Transferring later is a second-best solution that carries a three-year risk.

#### 5.4 The seven-pay test and modified endowment contracts

Section 7702A treats a contract as a modified endowment contract where the accumulated premiums in the first seven contract years exceed the sum of the net level premiums that would have been payable had the contract provided paid-up benefits after seven level annual premiums.[77]

The consequence is confined to **living** distributions. The death benefit remains excluded either way.

| | Non-MEC | Modified endowment contract |
|---|---|---|
| Withdrawal ordering | **Basis first**, then gain | **Gain first**, then basis |
| Policy loans | Not a distribution; untaxed | **Treated as a distribution** |
| Additional tax before 59½ | None | **10 percent** on the taxable part |
| Death benefit | Excluded | Excluded |

Funding a policy quickly to maximise cash value is exactly what causes it to fail the test. Where the policy is intended as a source of retirement liquidity, staying inside the seven-pay limits is essential and the insurer monitors it.

Once a contract is a modified endowment contract it remains one permanently, and a contract received in exchange for one is also one.

#### 5.5 Accessing cash value

For a contract that is not a modified endowment contract:

```
Withdraw up to basis — the cumulative premiums paid — tax free, § 72(e)
Then borrow against the remaining cash value — a loan, not a distribution
```

Two cautions. Loan interest accrues and is generally **not deductible**, by § 264. And if the policy **lapses or is surrendered** with a loan outstanding, the loan is treated as a distribution at that moment and the entire gain becomes taxable — in a year when there is no cash to pay the tax, because the cash value has been consumed by the loan.

This is the failure mode of an over-borrowed policy in late retirement, and it is the reason a projection should test whether the policy remains in force to age 90 rather than assuming it does.

### 6. Examples and Case Calculations

#### Example 1 — Ownership decides the estate result

A $4,000,000 policy, an estate otherwise worth $13,000,000.

```
OWNED PERSONALLY
   Gross estate  13,000,000 + 4,000,000              17,000,000
   Exclusion                                        −15,000,000
   Taxable                                            2,000,000
   Estate tax at 40 percent                            $800,000
   Income tax on the proceeds                                $0

OWNED BY AN IRREVOCABLE TRUST FROM INCEPTION
   Gross estate                                      13,000,000
   Exclusion                                        −15,000,000
   Estate tax                                                $0
   Income tax on the proceeds                                $0
```

The death benefit is income tax free in both cases. The $800,000 difference is entirely a function of who owned the policy.

#### Example 2 — The three-year rule

The same policy, owned personally and transferred to a trust 26 months before death.

```
§ 2035 — transfer within three years
   Proceeds included in the gross estate                4,000,000
   Estate tax at 40 percent                              $800,000
```

The transfer achieved nothing. Had the trust bought the policy originally, or had the insured survived a further ten months, the result would have been nil.

#### Example 3 — The cross-purchase transfer for value trap

Two shareholders each own a policy on their own life and, on restructuring a buy-sell agreement, transfer them to each other for value.

```
Transfer to a co-shareholder — not within any § 101(a)(2) safe harbour
   Death benefit                                       5,000,000
   Excluded: consideration paid plus later premiums      600,000
   Taxable as ordinary income to the recipient         4,400,000
```

Had the policies instead been transferred to the **corporation**, the transfer would have fallen within the safe harbour for a transfer to a corporation in which the insured is a shareholder, and the whole benefit would have remained excluded.

#### Example 4 — A modified endowment contract on a withdrawal

A policy with $400,000 of cash value and $250,000 of premiums paid. The owner, aged 55, takes $100,000.

```
NOT a MEC
   Withdrawal to basis first — basis 250,000
   Taxable                                                     $0

A MEC
   Gain first — gain is 150,000
   Taxable                                                $100,000
   10 percent additional tax, under 59½                    $10,000
                                                          --------
   Total cost at a 32 percent rate                          $42,000
```

The same policy, the same withdrawal, a $42,000 difference — decided by how quickly the contract was funded in its first seven years.

#### Example 5 — A lapse with a loan outstanding

At age 84 a policy has $520,000 of cash value, $480,000 of loans outstanding, and $300,000 of premiums paid. Rising cost of insurance causes it to lapse.

```
Deemed distribution on lapse                            520,000
Basis                                                  −300,000
                                                       --------
Taxable gain                                            220,000
Tax at 24 percent                                       $52,800
Cash actually received                                        $0
```

A tax bill with no cash. Testing whether the policy sustains itself to the end of the projection is what prevents this appearing as a surprise.

### 7. Interactions with Other Rules

**Estate tax (Module 28).** Sections 2042 and 2035 decide inclusion; Module 28 computes the tax.

**Gift tax (Module 29).** Premiums paid to an irrevocable trust are gifts to the beneficiaries. Crummey withdrawal powers convert them into present interests so that the annual exclusion applies.

**Long-term care (Module 33).** Hybrid policies with long-term care riders are governed by § 7702B, and qualified benefits are excluded from income within a per-diem limit.

**Retirement income.** Cash value withdrawals and loans do not enter adjusted gross income, so they do not raise provisional income for Social Security taxation, do not affect the Medicare surcharge, and are outside the net investment income tax. That is the substantive argument for using policy loans in retirement, and it holds only for a contract that is not a modified endowment contract and that stays in force.

**Step-up in basis (Module 31).** Not relevant to the death benefit, which is excluded from income by § 101 rather than by a basis adjustment.

### 8. Common Scenarios and Edge Cases

**Income tax free and estate tax free are different questions.** Nearly every policy is the first; only correctly structured ones are the second.

**Paying premiums is not an incident of ownership.** An insured may fund a trust-owned policy without bringing it into the estate.

**The trust should buy the policy, not receive it.** Transferring an existing policy starts a three-year clock; original ownership has no exposure.

**A transfer to a co-shareholder is not protected.** The safe harbours cover the insured, a partner, a partnership and a corporation — not a fellow shareholder.

**A modified endowment contract stays one for life**, and so does any contract exchanged for it.

**The death benefit of a modified endowment contract is still excluded.** Only living distributions are affected.

**An over-borrowed policy that lapses produces tax without cash.** This is the most damaging outcome in the whole module and it arrives late in life.

**Loan interest is not deductible** under § 264.

**Employer-owned policies need notice and consent before issue.** Section 101(j) is not curable afterwards.

### 9. Planning Implications

Where a policy is intended to be outside the estate, the trust should be established and should apply for the policy before it is issued. This is a sequencing decision that cannot be improved on later, and the alternative carries three years of mortality risk.

For an estate comfortably below $15,000,000 per person, the § 2042 analysis is often unnecessary and the complexity of a trust may not be warranted — but state thresholds should be checked first, because several are far lower and some carry a cliff.

Where a permanent policy is intended as a retirement income source, the seven-pay test governs the funding schedule. Paying in faster produces more cash value and destroys the tax treatment that made the strategy worthwhile.

Any projection that draws on policy loans should model the policy to age 90 or beyond and test that it remains in force. A lapse in the final years converts a tax-free income stream into a taxable event at the worst possible moment, and the exposure grows precisely as the cost of insurance rises with age.

### 10. Data Tables for the Engine

| Constant | Value | Source |
|---|---|---|
| Death benefit | Excluded from gross income | § 101(a)(1) |
| Transfer for value safe harbours | Insured; a partner; a partnership; a corporation in which the insured is a shareholder or officer | § 101(a)(2)(B) |
| Estate inclusion | Any incident of ownership at death | § 2042 |
| Three-year rule | Transfers within 3 years of death | § 2035(a) |
| Seven-pay test | First 7 contract years | § 7702A(b) |
| MEC withdrawal ordering | Gain first | § 72(e)(10) |
| MEC additional tax | 10 percent before 59½ | § 72(v) |
| Non-MEC withdrawal ordering | Basis first | § 72(e) |
| Policy loan interest | Not deductible | § 264 |
| Lapse with a loan | Deemed distribution of the full cash value | § 72(e) |

### 11. References

[77] 26 U.S.C. § 7702A, *Modified endowment contract defined*. United States Code, Office of the Law Revision Counsel. https://www.govinfo.gov/app/collection/uscode

[78] 26 U.S.C. § 101, *Certain death benefits*. https://www.govinfo.gov/app/collection/uscode

[79] 26 U.S.C. §§ 72, 264, 2035, 2042 and 7702. https://www.govinfo.gov/app/collection/uscode

[80] Treas. Reg. § 20.2042-1(c), *Incidents of ownership*. Electronic Code of Federal Regulations. https://www.ecfr.gov/current/title-26

### 12. Status in This System

| Layer | Status |
|---|---|
| Projection engine | **Applied in part.** The death benefit is treated as excluded from income under § 101(a)(1). Estate inclusion under § 2042 is applied where the insured holds incidents of ownership, and the § 2035 three-year rule is applied to a policy transferred within three years of death — so the Example 1 and Example 2 outcomes can both be represented. Cash value accumulates without current income tax, and a policy owned by a trust from inception is correctly kept out of the estate. |
| Backend (`tax-be`) | **Not applied** as a computation. The roadmap projection allocates 25 percent of deployed savings to an "insurance" bucket and compounds it at the scenario rate. `strategyPhaseMap.js` catalogues "Buy-Sell Stock Redemption with Life Insurance", "Employer-Provided Life Insurance", "Key-Person Insurance Deduction" and "Executive Bonus Plan (with Gross-Up)"; none is computed. |
| Known limitations | The § 7702A seven-pay test is **not applied**, so the engine cannot distinguish a modified endowment contract from an ordinary policy, and the distribution ordering that follows — gain first with a 10 percent additional tax, rather than basis first — is absent. The $42,000 difference in Example 4 cannot be shown. The § 101(a)(2) transfer for value rule and its safe harbours are not modelled, so the cross-purchase trap in Example 3 is invisible; nor are reportable policy sales under § 101(a)(3) or the notice and consent requirements for employer-owned contracts under § 101(j). Premium payments into an irrevocable trust are not treated as gifts, so Crummey powers and the annual exclusion interaction with Module 29 are absent. Policy loan interest is not tracked and § 264 is not applied. Lapse is only partially modelled: the engine does not compute the deemed distribution of the full cash value that § 72(e) produces when a policy with an outstanding loan terminates, which is the failure mode in Example 5. |


---

## Module 31 — Step-Up in Basis at Death

**Tax year:** 2026 · **As of:** September 2026 · **Primary authority:** IRC §§ 1014, 1015, 691

---

### 1. Overview and Purpose

Property acquired from a decedent takes a basis equal to its fair market value at the date of death. The unrealised appreciation accumulated over the owner's lifetime is never taxed — not to the decedent, and not to the heir.

For most households this is now the **most valuable provision in the Code**. With the estate exclusion permanently at $15,000,000 per person, very few estates pay transfer tax, so the planning question has shifted from avoiding estate tax to **capturing the step-up**. Techniques that remove property from the estate to save a tax that will not be payable also forfeit a step-up that would have been.

Two categories are excluded and both matter. **Income in respect of a decedent** under § 1014(c) receives no step-up, which is why a pre-tax retirement account is the worst asset to leave to an individual heir. And property **gifted to the decedent within one year of death** and returning to the donor is denied the step-up under § 1014(e), which closes an obvious circular arrangement.

### 2. Governing Law and Authorities

| Type | Citation | What it establishes |
|---|---|---|
| Statute | IRC § 1014(a) | Basis equal to fair market value at death |
| Statute | IRC § 1014(b)(6) | Community property — both halves adjusted |
| Statute | IRC § 1014(b)(9) | Property included in the gross estate, reduced by depreciation allowed before death |
| Statute | IRC § 1014(c) | No step-up for income in respect of a decedent |
| Statute | IRC § 1014(e) | One-year rule for appreciated property gifted to the decedent |
| Statute | IRC § 1014(f) | Basis must be consistent with the estate tax return |
| Statute | IRC § 1015 | Carryover basis for lifetime gifts |
| Statute | IRC § 691 | Income in respect of a decedent |
| Statute | IRC § 2032 | Alternate valuation date |
| Statute | IRC § 1223(9) | Inherited property is automatically long-term |

### 3. Key Definitions

| Term | Definition |
|---|---|
| **Step-up** | The adjustment of basis to fair market value at death. The provision is neutral in direction — depreciated property receives a **step-down**. |
| **Income in respect of a decedent** | An item of income the decedent had a right to receive but had not recognised. Excluded from § 1014 by subsection (c). |
| **Community property** | Property held under the community property regime of one of nine states. Both halves are adjusted on the first death, not merely the decedent's. |
| **Consistent basis** | Under § 1014(f), the basis claimed by the recipient may not exceed the value reported on the estate tax return. |

### 4. Who Is Affected

Every heir of every decedent. The provision applies whether or not an estate tax return is required.

The households for whom it matters most are those with substantial unrealised gains and estates comfortably below the exclusion — which, at $15,000,000 per person, is the large majority. For them there is no estate tax to plan against and the step-up is pure benefit.

### 5. Core Rules and Calculations

#### 5.1 Case Register

| # | Case | Applied |
|---|---|---|
| 1 | § 1014(a) basis to fair market value at death | Yes, in effect |
| 2 | Step-**down** for depreciated property | **No** |
| 3 | § 1014(b)(6) community property double adjustment | **No** |
| 4 | § 1014(c) no step-up for income in respect of a decedent | Yes |
| 5 | Heir's income tax on inherited pre-tax balances | Yes — at an assumed rate |
| 6 | § 691(c) deduction for estate tax on the IRD | **No** |
| 7 | § 1014(e) one-year rule | **No** |
| 8 | § 1014(f) consistent basis reporting | Not applicable |
| 9 | § 1015 carryover basis on lifetime gifts | **No** |
| 10 | § 2032 alternate valuation date | **No** |
| 11 | § 1223(9) inherited property treated as long-term | **No** |
| 12 | Depreciation recapture eliminated by the step-up | **No** — follows from D18 |
| 13 | § 469(g)(2) suspended losses limited by the step-up | **No** |
| 14 | Capital loss carryforward extinguished at death | **No** |

#### 5.2 The basic rule

```
basis to the heir = fair market value at the date of death
                    (or at the alternate valuation date if elected under § 2032)
```

The adjustment is in whichever direction the facts require. Property worth less than its basis receives a **step-down**, and the unrealised loss is destroyed rather than transferred. Holding a depreciated asset until death is therefore the opposite of good planning: the loss should be realised during life, where it is at least available against gains and $3,000 of ordinary income a year under Module 24.

Inherited property is automatically treated as held long-term under § 1223(9), whatever the actual holding period of either the decedent or the heir.

#### 5.3 What does not get a step-up

| Asset | Treatment |
|---|---|
| Traditional individual retirement account, 401(k), 403(b) | **No step-up** — income in respect of a decedent, § 1014(c) |
| Annuity gain | **No step-up** |
| Accrued but unpaid compensation, deferred compensation | **No step-up** |
| Instalment sale receivable | **No step-up** |
| Accounts receivable of a cash-basis business | **No step-up** |
| Savings bond accrued interest | **No step-up** |
| Roth account | Step-up irrelevant — distributions are tax free anyway |
| Taxable brokerage account | **Full step-up** |
| Real estate | **Full step-up**, and accumulated depreciation is never recaptured |
| Closely held business interests | **Full step-up** |

The contrast between the first row and the last four is the central planning fact of this module.

#### 5.4 Community property — the double step-up

In the nine community property states, § 1014(b)(6) adjusts the **surviving spouse's half** as well as the decedent's, provided at least half the community interest was includible in the decedent's gross estate.

| | Community property state | Common law state, joint tenancy |
|---|---|---|
| Decedent's half | Stepped up | Stepped up |
| Survivor's half | **Stepped up** | **Not adjusted** |

On a $2,000,000 asset with a $400,000 basis, the survivor in a community property state has a basis of $2,000,000 after the first death; in a common law state the basis is $1,200,000. Selling immediately, the difference is $800,000 of gain — $190,400 of tax at 20 percent plus the net investment income tax.

Several common law states permit an election into community property treatment through a community property trust, which is worth considering for a couple with substantial appreciated assets.

#### 5.5 The one-year rule — § 1014(e)

Where **appreciated** property is given to a decedent within one year of death and passes back to the donor or the donor's spouse, the basis in the donor's hands is the decedent's basis immediately before death — not fair market value.[81]

The rule closes the arrangement in which a healthy spouse transfers appreciated property to a dying spouse in order to obtain a step-up on its return. Property must be given more than a year before death for the step-up to apply, and the same rule reaches property sold by the estate or by a grantor trust where the donor is entitled to the proceeds.

#### 5.6 The gift-versus-inherit decision

Section 1015 gives a lifetime donee the donor's basis. Section 1014 gives an heir fair market value. The comparison is the central estate planning trade-off:

| | Gift during life | Held until death |
|---|---|---|
| Basis to the recipient | Donor's basis | **Fair market value** |
| Unrealised gain | Transferred | **Eliminated** |
| Future growth | Outside the estate | Inside the estate |
| Estate tax | Reduced | Not reduced |

The rule of thumb follows from the exclusion. Where the estate will **not** be taxable, hold appreciated property. Where it **will** be taxable, the 40 percent estate rate exceeds the 20 to 23.8 percent capital gain rate, so gifting wins on the principal and wins again on the growth.

### 6. Examples and Case Calculations

#### Example 1 — Two assets of the same value

An heir inherits a $2,000,000 brokerage account with a $500,000 basis and a $2,000,000 traditional individual retirement account. The heir's marginal rate is 35 percent, and the estate is not taxable.

```
BROKERAGE ACCOUNT
   Basis steps up to                                2,000,000
   Heir sells immediately: gain                             0
   Tax                                                     $0
   Net to the heir                                 $2,000,000

TRADITIONAL IRA
   No step-up, § 1014(c)
   Heir withdraws over the 10-year period
   Income tax at 35 percent                           700,000
   Net to the heir                                 $1,300,000
```

Two assets with identical statements are worth $700,000 apart. Any plan that treats them as equivalent misallocates bequests.

#### Example 2 — Community property against joint tenancy

A couple owns a property worth $2,000,000 with a basis of $400,000. One spouse dies; the survivor sells.

```
COMMUNITY PROPERTY STATE
   Both halves adjusted, § 1014(b)(6)
   Basis                                            2,000,000
   Gain on sale                                             0
   Tax                                                     $0

COMMON LAW STATE, JOINT TENANCY
   Decedent's half stepped up   1,000,000
   Survivor's half unchanged      200,000
   Basis                                            1,200,000
   Gain on sale                                       800,000
   Tax at 20% plus 3.8%                              $190,400
```

#### Example 3 — Real estate, and why holding beats selling

A rental property worth $2,600,000, basis $1,163,637 after ten years of cost-segregated depreciation, owner aged 88.

```
SELL DURING LIFE — from Module 22
   § 1245 recapture at 37 percent                     148,000
   Unrecaptured § 1250 at 25 percent                  109,091
   § 1231 gain at 20 percent                          120,000
                                                     --------
   Tax                                                377,091

HOLD UNTIL DEATH
   Basis steps up to                                2,600,000
   Depreciation recapture                                   0
   Capital gain                                             0
   Tax                                                     $0
```

The step-up eliminates the recapture as well as the gain. For an owner with a limited life expectancy and heavily depreciated property, holding is worth $377,091 and no exchange or deferral technique matches it.

#### Example 4 — The one-year rule defeating a transfer

A healthy spouse transfers $1,500,000 of stock with a $200,000 basis to a terminally ill spouse, who dies eight months later leaving it back.

```
§ 1014(e) applies — appreciated property, within one year, returning to the donor
   Basis in the donor's hands                          200,000
   Step-up obtained                                          0
```

Had the transfer been made thirteen months before death, the basis would have become $1,500,000.

#### Example 5 — What dies with the taxpayer

```
Capital loss carryforward, Module 24              extinguished
Suspended passive losses, Module 25       allowed only to the extent
                                          they exceed the step-up
Net operating loss carryforward, Module 27        extinguished
Unrealised capital gain                           eliminated by the step-up
Unrealised capital loss                           destroyed by the step-down
```

The asymmetry is systematic: unrealised **gains** are forgiven at death, and unused **losses** are lost. Everything in the second category argues for realisation during life.

### 7. Interactions with Other Rules

**Estate tax (Module 28).** The step-up is available whether or not an estate tax return is required, but § 1014(f) requires consistency with any value reported.

**Gift tax (Module 29).** Section 1015 carryover basis is the alternative, and § 5.6 sets out the trade.

**Depreciation and recapture (Module 22).** The step-up eliminates accumulated depreciation. Nothing is recaptured.

**Passive activity losses (Module 25).** Section 469(g)(2) allows suspended losses at death only to the extent they exceed the step-up, so a large step-up destroys them.

**Capital losses (Module 24) and net operating losses (Module 27).** Both carryforwards are extinguished.

**Required distributions (Module 09) and Roth conversions (Module 10).** Conversion shifts the income tax on a pre-tax balance from the heir to the owner. Where the owner's rate is below the heir's, conversion improves the family result; where it is above, it does not.

### 8. Common Scenarios and Edge Cases

**The adjustment goes both ways.** Depreciated property is stepped **down** and the loss is destroyed. Realise losses during life.

**Retirement accounts get nothing.** This is the most consequential exclusion and the one clients find most surprising.

**Community property adjusts both halves.** The difference against joint tenancy in a common law state can be very large, and several common law states now permit an election into the regime.

**Property gifted to a dying person within a year does not work.** Section 1014(e) is specific and reaches property sold by the estate as well.

**Inherited property is always long-term** under § 1223(9), so an heir selling the next day has long-term treatment.

**The step-up applies to jointly held property only to the extent it is in the estate.** For a non-spouse joint tenant that depends on contribution; for spouses in a common law state it is generally one half.

**Charity is the right recipient for a pre-tax account.** A charity pays no income tax on the distribution, so the full amount is applied; a child receives it net of income tax.

**A basis step-up is worth nothing on an asset that will not be sold**, which is why the analysis should look at the heir's likely behaviour rather than at the asset alone.

### 9. Planning Implications

For estates below the exclusion — most estates — the planning objective is the reverse of the traditional one. Appreciated assets should be **held**, not given, and techniques that remove property from the estate should be examined for what step-up they cost.

Asset location for bequests follows directly. Leave taxable investment accounts and real estate to individuals, where the step-up applies; leave pre-tax retirement accounts to charity, where the income tax is irrelevant. Reversing that allocation costs the family the difference in Example 1 on every dollar.

Losses should be realised during life in every category. Capital loss carryforwards, net operating losses and unrealised depreciation all disappear at death, and suspended passive losses largely do.

For a couple in a common law state with substantial appreciated assets, the community property election available in several states is worth investigating, because it converts a half step-up into a full one at the first death.

For an elderly owner of heavily depreciated real estate, holding to death is usually the single most valuable decision available, and Example 3 quantifies it against a sale.

### 10. Data Tables for the Engine

| Constant | Value | Source |
|---|---|---|
| Basis to an heir | Fair market value at death | § 1014(a) |
| Alternate valuation | 6 months after death, if elected | § 2032 |
| Community property | Both halves adjusted | § 1014(b)(6) |
| Income in respect of a decedent | **No** adjustment | § 1014(c) |
| Property gifted to the decedent within 1 year | Decedent's basis | § 1014(e) |
| Holding period of inherited property | Long-term automatically | § 1223(9) |
| Basis of a lifetime gift | Donor's basis | § 1015 |
| Suspended passive losses at death | Allowed only above the step-up | § 469(g)(2) |
| Capital loss and NOL carryforwards | Extinguished | — |

### 11. References

[81] 26 U.S.C. § 1014, *Basis of property acquired from a decedent*, including subsections (b)(6), (c), (e) and (f). United States Code, Office of the Law Revision Counsel. https://www.govinfo.gov/app/collection/uscode

[82] 26 U.S.C. §§ 691, 1015, 1223 and 2032. https://www.govinfo.gov/app/collection/uscode

[74] 26 U.S.C. §§ 2001–2056. https://www.govinfo.gov/app/collection/uscode

### 12. Status in This System

| Layer | Status |
|---|---|
| Projection engine | **Applied in part.** The central distinction is respected: pre-tax retirement balances are treated as income in respect of a decedent, receive no step-up, and are reduced by an assumed heir income tax rate before reaching the estate figure, while other assets pass without that reduction. That is the substance of § 1014(c) and it is the point most models get wrong. |
| Backend (`tax-be`) | **Not applied.** The roadmap projection compounds a "legacy" bucket; no basis or transfer analysis exists. |
| Known limitations | The adjustment is modelled only as favourable. There is no **step-down** for depreciated property, so an unrealised loss held to death is not destroyed as the statute requires. The § 1014(b)(6) community property double adjustment is absent, so the $190,400 difference in Example 2 cannot be shown for a client in one of the nine states. The § 691(c) deduction for estate tax attributable to income in respect of a decedent is not applied, which overstates the heir's burden on a taxable estate. The § 1014(e) one-year rule is absent. Section 1015 carryover basis on lifetime gifts is not modelled, so the gift-versus-hold comparison in § 5.6 — the central decision of this module — cannot be run inside the engine. Because a property sale produces no gain at all under **D18**, the elimination of depreciation recapture by the step-up in Example 3 is not visible either. The § 469(g)(2) limitation on suspended losses at death and the extinguishment of capital loss and net operating loss carryforwards are likewise absent. |


---

## Module 32 — Medical Expense Deduction

**Tax year:** 2026 · **As of:** September 2026 · **Primary authority:** IRC § 213

---

### 1. Overview and Purpose

Section 213 allows an itemised deduction for unreimbursed medical and dental expenses to the extent they exceed **7.5 percent of adjusted gross income**. The floor makes the deduction irrelevant in most years and decisive in a few.

For a retirement projection the provision matters at one point in particular. A year of substantial long-term care cost can produce medical expenses of $100,000 or more against a modest income, which turns a taxpayer who has taken the standard deduction for forty years into an itemiser with a very large deduction. That year is frequently the **lowest-tax year of a person's life**, and it arrives without being planned for.

Two features shape the arithmetic. The floor is a percentage of income, so **reducing** income in a heavy medical year does not help proportionally — it lowers the floor, but it lowers the deduction's value more. And the deduction is allowed in full for alternative minimum tax purposes, because the AMT floor has matched the regular 7.5 percent floor since 2019. That second point is a common source of error in projections, which add medical expenses back into alternative minimum taxable income when they should not.

### 2. Governing Law and Authorities

| Type | Citation | What it establishes |
|---|---|---|
| Statute | IRC § 213(a) | Deduction for expenses above 7.5 percent of adjusted gross income |
| Statute | IRC § 213(d)(1) | Definition of medical care |
| Statute | IRC § 213(d)(10) | Limitation on eligible long-term care premiums by age |
| Statute | IRC § 213(f) | The 7.5 percent floor, made permanent |
| Statute | IRC § 56(b)(1)(B) | Alternative minimum tax treatment |
| Statute | IRC § 7702B(c) | Qualified long-term care services |
| Guidance | Rev. Proc. 2025-32, § 3.27 | 2026 long-term care premium limits |
| Guidance | IRS Publication 502 | Medical and dental expenses |

### 3. Key Definitions

| Term | Definition |
|---|---|
| **Medical care** | Amounts paid for the diagnosis, cure, mitigation, treatment or prevention of disease, or for the purpose of affecting a structure or function of the body, and for transportation essential to that care. |
| **Eligible long-term care premium** | The portion of a premium for a qualified long-term care insurance contract that counts as medical care, limited by the insured's attained age. |
| **Qualified long-term care services** | Necessary diagnostic, preventive, therapeutic, curing, treating, mitigating, rehabilitative and maintenance or personal care services required by a chronically ill individual under a plan of care prescribed by a licensed health care practitioner. |
| **Chronically ill individual** | A person unable to perform at least two activities of daily living for at least 90 days, or requiring substantial supervision because of severe cognitive impairment. |

### 4. Who Is Affected

Any taxpayer who itemises and has unreimbursed medical costs above the floor. Expenses paid for the taxpayer, a spouse and dependants all count, and a person may be treated as a dependant for this purpose even where they fail the gross income test that applies elsewhere — which matters for an adult child paying a parent's care costs.

The floor makes the deduction inaccessible to most taxpayers in most years. It becomes available in a care year, a year of major surgery, or a year of unusually low income.

### 5. Core Rules and Calculations

#### 5.1 Case Register

| # | Case | Applied |
|---|---|---|
| 1 | 7.5 percent of adjusted gross income floor | Yes |
| 2 | Deduction available only where itemising | Yes |
| 3 | Medicare premiums as medical care | Yes |
| 4 | Medicare surcharge as medical care | Yes |
| 5 | Long-term care services as medical care | Yes |
| 6 | § 213(d)(10) age-banded premium limits | Yes |
| 7 | Premium limits indexed annually | Partially — by the general factor |
| 8 | Medical expenses **allowed** for alternative minimum tax | Yes |
| 9 | Expenses for a dependent parent | **No** |
| 10 | Capital improvements to a residence for medical care | **No** |
| 11 | Transportation and lodging for care | **No** |
| 12 | Nursing home costs where care is the primary purpose | Yes, in effect |
| 13 | Reimbursements reducing the deductible amount | **No** |

#### 5.2 The computation

```
qualifiedMedicalExpenses
  − 0.075 × adjustedGrossIncome
  = deductible amount, if positive

then: itemise only if
   deductibleMedical + stateAndLocalTaxes + interest + charitable
   exceeds the standard deduction
```

The floor is applied before the comparison with the standard deduction, so a taxpayer can have large medical costs and still take the standard deduction.

#### 5.3 What counts

| Included | Excluded |
|---|---|
| Medicare Part B, Part D and supplement premiums | Cosmetic surgery |
| The Medicare income-related surcharge | Non-prescription medicines, other than insulin |
| Long-term care services for a chronically ill individual | General health items — gym membership, vitamins |
| Eligible long-term care insurance premiums, within the age caps | Premiums paid with pre-tax dollars |
| Nursing home costs where medical care is the principal reason | Funeral and burial expenses |
| Prescription drugs, insulin | Amounts reimbursed by insurance |
| Transportation essential to medical care | Household help that is not nursing care |
| Capital improvements, to the extent they exceed the increase in property value | |

Employer-paid premiums and amounts paid from a health savings account are already excluded from income and cannot be deducted again.

#### 5.4 Long-term care premiums — the age bands

Only part of a long-term care insurance premium counts as medical care, and the limit rises with the insured's attained age before the close of the year:[83]

| Attained age | 2026 limitation |
|---|---|
| 40 or less | **$500** |
| 41 to 50 | **$930** |
| 51 to 60 | **$1,860** |
| 61 to 70 | **$4,960** |
| **71 and over** | **$6,200** |

The limit is **per person**, so a couple both over 70 may count up to $12,400. Premiums above the cap are simply not medical care and are not deductible at all.

The amounts are indexed annually and the age bands are fixed. A policy bought at 55 has a small allowance for a decade and a much larger one thereafter, which is the opposite of the premium profile most policies have.

#### 5.5 The alternative minimum tax point

Before 2019 the alternative minimum tax used a 10 percent floor while the regular tax floor was 7.5 percent, so the difference was an adjustment. Since the floors were aligned, **medical expenses are allowed in full for alternative minimum tax purposes** and there is no add-back.

This matters because a care year produces a very large deduction, and adding it back into alternative minimum taxable income generates a phantom liability that does not exist. Only the standard deduction, or state and local taxes where the taxpayer itemises, are added back.

### 6. Examples and Case Calculations

#### Example 1 — An ordinary year

A retired couple with adjusted gross income of $120,000 and $14,000 of medical costs, mostly Medicare premiums.

```
Medical expenses                                     14,000
Floor  7.5% × 120,000                                 9,000
                                                     ------
Deductible                                            5,000

Itemised total, with $10,000 of state and local tax  15,000
Standard deduction, both over 65                     35,500
→ the couple takes the standard deduction
```

The deduction exists but is worthless, because itemising is worse. This is the position in most years.

#### Example 2 — A care year

The same couple. One spouse enters memory care at $135,000 a year. Adjusted gross income rises to $190,000 because distributions are taken to pay for it.

```
Care costs                                          135,000
Medicare premiums and other medical                  16,000
                                                    -------
Qualified medical expenses                          151,000
Floor  7.5% × 190,000                                14,250
                                                    -------
Deductible medical                                  136,750
State and local tax                                  10,000
                                                    -------
Itemised deductions                                 146,750
Standard deduction                                   35,500

Taxable income  190,000 − 146,750                    43,250
Federal tax                                          $4,891
```

Against $190,000 of income the couple pays $4,891. Without the medical deduction the tax would have been approximately $17,222. The care year is genuinely the cheapest tax year of their retirement.

#### Example 3 — The Roth conversion window a care year creates

Continuing Example 2, the couple has $1,100,000 in pre-tax accounts and the 22 percent bracket runs to $100,800.

```
Taxable income before conversion                     43,250
Room to the top of the 22 percent bracket            57,550
Conversion of                                        57,550
Tax on the conversion at 12 and 22 percent          $10,140
```

Converting $57,550 costs $10,140 — an effective rate of 17.6 percent on money that would otherwise be distributed at 24 percent or more, and taxed at the survivor's single rate after the first death. A care year is the best conversion window most clients will ever have, and it is invisible unless the projection models the medical deduction properly.

#### Example 4 — Long-term care premiums at two ages

A couple, one aged 58 and one aged 72, paying $4,200 and $7,500 of long-term care premiums.

```
Aged 58   premium 4,200, cap 1,860        counted   1,860
Aged 72   premium 7,500, cap 6,200        counted   6,200
                                                    -----
Eligible as medical care                            8,060
Not deductible at any level                         3,640
```

### 7. Interactions with Other Rules

**Standard deduction (Module 02).** The medical deduction is the usual reason a lifelong non-itemiser itemises for the first time. The comparison must be made annually.

**Medicare (Modules 15 and 16).** Premiums, deductibles, coinsurance and the income-related surcharge are all medical care under § 213(d).

**Long-term care (Module 33).** Care costs are the main source of a deduction large enough to clear the floor.

**Health savings accounts (Module 34).** Amounts paid from a health savings account are already tax free and cannot be deducted again. Paying from taxable funds and preserving the account is sometimes better.

**Roth conversions (Module 10).** A care year creates unusual conversion capacity, as Example 3 shows.

**Alternative minimum tax.** Medical expenses are allowed in full and must **not** be added back.

**Required distributions (Module 09).** Distributions taken to fund care raise adjusted gross income and therefore the floor, so the deduction rises more slowly than the cost.

### 8. Common Scenarios and Edge Cases

**The floor moves with income.** Taking a large distribution to pay for care raises adjusted gross income and raises the floor by 7.5 cents in the dollar, so the deduction does not keep pace with the withdrawal.

**Nursing home costs are fully deductible where medical care is the principal reason for being there**, including meals and lodging. Where residence is primarily personal, only the medical component counts.

**Long-term care premiums are capped by age, per person.** Amounts above the cap are not deductible at all.

**A parent can be a dependant for medical purposes** even where their income is too high for a dependency exemption, provided the taxpayer furnishes more than half their support. This is regularly missed by adult children paying a parent's care costs.

**Medical expenses are not added back for alternative minimum tax.** The floors have matched since 2019.

**Capital improvements count only above the increase in property value.** A stairlift usually adds nothing to value and is fully deductible; a lift may add value and only the excess counts.

**Expenses paid with pre-tax dollars cannot be deducted.** Employer premiums and health savings account distributions are already untaxed.

**Timing matters at the year end.** Where costs straddle a year boundary, concentrating them in one year clears the floor once rather than twice.

### 9. Planning Implications

A care year should be identified in the projection as a planning opportunity rather than only as a cost. The combination of a very large deduction and continuing low ordinary income produces the cheapest conversion window a client will see, and it is temporary.

Because the floor rises with income, funding care from sources that do **not** raise adjusted gross income — Roth withdrawals, taxable account principal, life insurance cash value within the limits in Module 30 — preserves more of the deduction than funding it from pre-tax distributions.

Where costs can be shifted across a year end, bunching them clears the floor once.

Long-term care premiums should be assessed against the age caps rather than assumed deductible. For a couple in their fifties the deductible portion is a small fraction of the premium; from 71 it is $6,200 each.

An adult child paying a parent's care costs should test the § 213 support test, which is more generous than the general dependency rules.

### 10. Data Tables for the Engine

| Constant | 2026 value | Indexed |
|---|---|---|
| Floor | **7.5 percent of adjusted gross income** | Fixed, permanent |
| Alternative minimum tax floor | 7.5 percent — same, no add-back | Fixed |
| LTC premium cap, age 40 or less | $500 | Yes |
| LTC premium cap, 41–50 | $930 | Yes |
| LTC premium cap, 51–60 | $1,860 | Yes |
| LTC premium cap, 61–70 | $4,960 | Yes |
| LTC premium cap, 71 and over | $6,200 | Yes |
| Application of the caps | Per person | Fixed |
| Medicare premiums and surcharge | Qualified medical care | § 213(d) |

### 11. References

[83] Internal Revenue Service, *Revenue Procedure 2025-32*, § 3.27. https://www.irs.gov/pub/irs-drop/rp-25-32.pdf

[84] 26 U.S.C. § 213, *Medical, dental, etc., expenses*. United States Code, Office of the Law Revision Counsel. https://www.govinfo.gov/app/collection/uscode

[85] Internal Revenue Service, *Publication 502, Medical and Dental Expenses*. https://www.irs.gov/pub/irs-pdf/p502.pdf

### 12. Status in This System

| Layer | Status |
|---|---|
| Projection engine | **Applied, and correctly on the point most models get wrong.** The 7.5 percent floor is implemented, Medicare premiums and the income-related surcharge are included in qualified medical expenses, and long-term care costs feed the same computation. The age-banded § 213(d)(10) premium caps are implemented with all five bands matching Revenue Procedure 2025-32. Most importantly, **medical expenses are not added back for alternative minimum tax purposes** — the engine adds back only the standard deduction, or state and local taxes where the taxpayer itemises. An earlier version of this system added the whole medical deduction back and produced a phantom alternative minimum tax liability of roughly $175,000 in care years; the correction is in place and the reasoning is recorded in the code. |
| Backend (`tax-be`) | **Not applied.** The roadmap projection allocates 2 percent of deployed savings to a "disability and long-term care" bucket. `strategyPhaseMap.js` catalogues "Section §105 Medical Reimbursement Plan HRA Flexibility" and "Health/Medical Expense Reimbursement Arrangement (HRA)"; neither is computed. |
| Known limitations | The premium caps are inflated forward by the engine's general factor rather than by the § 213(d)(10) mechanism, so projected caps drift from the published series. Expenses paid for a dependent parent are not modelled, and the more generous § 213 support test is therefore unavailable. Capital improvements to a residence, transportation and lodging for care, and the reduction for insurance reimbursements are not separately handled — medical cost enters as a single figure. |


---

## Module 33 — Long-Term Care

**Tax year:** 2026 · **As of:** September 2026 · **Primary authority:** IRC §§ 7702B, 213(d)(10), 101(g)

---

### 1. Overview and Purpose

Long-term care is assistance with the activities of daily living — bathing, dressing, eating, transferring, toileting, continence — or supervision required because of cognitive impairment. It is **not medical treatment**, and that distinction is why Medicare does not pay for it.

Module 15 sets out where Medicare stops: a skilled nursing benefit requiring a qualifying hospital stay, limited to 100 days, with $217 a day of coinsurance from day 21, and nothing at all for custodial care. Everything beyond that is private payment, insurance, or Medicaid after assets are exhausted.

For a projection to age 90 this is the largest uninsured exposure most households carry. A care event lasting several years at $100,000 or more a year can consume a portfolio that was otherwise adequate, and the probability of needing some period of care is high while the probability of needing a long one is much lower — a distribution that is poorly suited to self-funding and well suited to insurance.

The tax treatment is favourable in three places. Qualified long-term care services are medical care under § 213, so costs feed the deduction in Module 32. Premiums for a qualified contract count as medical care within the age-banded caps. And benefits received under a qualified contract are **excluded from income** within a per diem limit of **$430 a day** for 2026.[86]

### 2. Governing Law and Authorities

| Type | Citation | What it establishes |
|---|---|---|
| Statute | IRC § 7702B(b) | Qualified long-term care insurance contract |
| Statute | IRC § 7702B(c)(1) | Qualified long-term care services |
| Statute | IRC § 7702B(c)(2) | Chronically ill individual |
| Statute | IRC § 7702B(d) | Per diem limitation on excluded benefits |
| Statute | IRC § 7702B(e) | Riders on life insurance contracts |
| Statute | IRC § 101(g) | Accelerated death benefits for the terminally or chronically ill |
| Statute | IRC § 213(d)(1)(C), (d)(10) | Care services and premiums as medical care |
| Statute | IRC § 1035 | Exchange into a qualified long-term care contract |
| Guidance | Rev. Proc. 2025-32, §§ 3.27 and 3.62 | 2026 premium caps and per diem limit |

### 3. Key Definitions

| Term | Definition |
|---|---|
| **Chronically ill individual** | Certified within the preceding 12 months as unable to perform at least **two activities of daily living** without substantial assistance for a period expected to last at least **90 days**, or requiring **substantial supervision** to protect against threats to health and safety due to severe cognitive impairment. |
| **Activities of daily living** | Eating, toileting, transferring, bathing, dressing and continence. A contract must take at least five of the six into account. |
| **Qualified long-term care services** | Necessary diagnostic, preventive, therapeutic, curing, treating, mitigating and rehabilitative services, and maintenance or personal care services, required by a chronically ill individual under a plan of care prescribed by a licensed health care practitioner. |
| **Per diem contract** | A contract paying a fixed daily amount without regard to actual expense. Subject to the § 7702B(d) limit. |
| **Reimbursement contract** | A contract paying actual costs incurred. Not subject to the per diem limit. |

### 4. Who Is Affected

Anyone reaching advanced age. The tax provisions reach those holding a qualified contract, those paying for care, and those accelerating a life insurance death benefit under § 101(g).

Medicaid is the payer of last resort and has its own eligibility rules, including a **five-year look-back** on asset transfers and recovery against the estate. Planning for it is a specialist area outside the scope of this projection, but its existence is why a care event does not simply run until the money is gone.

### 5. Core Rules and Calculations

#### 5.1 Case Register

| # | Case | Applied |
|---|---|---|
| 1 | Care costs as an expense in the projection | Yes |
| 2 | Care costs as medical care under § 213 | Yes |
| 3 | § 213(d)(10) age-banded premium caps | Yes |
| 4 | § 7702B(d) per diem limit on excluded benefits | **No** |
| 5 | Benefits from a reimbursement contract excluded in full | **No** |
| 6 | Chronically ill certification requirement | **No** |
| 7 | Two-of-six activities of daily living test | **No** |
| 8 | Elimination period before benefits begin | **No** |
| 9 | Benefit period and lifetime maximum | **No** |
| 10 | Inflation rider on benefits | **No** |
| 11 | § 101(g) accelerated death benefits | **No** |
| 12 | § 7702B(e) hybrid policy riders | **No** |
| 13 | § 1035 exchange into a qualified contract | **No** |
| 14 | Medicare's 100-day skilled nursing limit | **No** — Module 15 |
| 15 | Medicaid eligibility and look-back | **No** |
| 16 | Care inflation above general inflation | Yes |

#### 5.2 What a qualified contract must do

Section 7702B(b) requires that the contract provide only coverage of qualified long-term care services, be guaranteed renewable, not have a cash surrender value, and apply refunds only to reduce future premiums or increase benefits. A contract meeting these conditions is treated as an accident and health insurance contract, which is what produces the tax treatment below.

#### 5.3 The three tax consequences

**Premiums.** Eligible premiums count as medical care within the § 213(d)(10) caps, which for 2026 run from $500 at age 40 or less to **$6,200** from age 71, per person. Module 32 sets out the full table. Amounts above the cap are not deductible at any level.

**Services.** Qualified long-term care services are medical care under § 213(d)(1)(C), so the whole cost enters the medical expense computation and is deductible above the 7.5 percent floor.

**Benefits.** Amounts received under a qualified contract are excluded from gross income. For a **per diem** contract the exclusion is capped at the greater of the § 7702B(d) limit — **$430 a day for 2026**, or $156,950 in a 365-day year — or the actual costs incurred.[86] A **reimbursement** contract pays actual costs and is excluded in full without reference to the limit.

The per diem limit is the point most often missed on a hybrid policy paying a fixed monthly amount. Where the daily benefit exceeds $430 and actual costs are lower, the excess is taxable.

#### 5.4 Accelerated death benefits — § 101(g)

A life insurance policy may pay a benefit before death to an insured who is terminally ill — certified as reasonably expected to die within 24 months — or chronically ill. The amount is treated as paid by reason of death and excluded under § 101(a), subject for a chronically ill insured to the same per diem limit.

This is the mechanism behind hybrid life and long-term care policies, and § 7702B(e) confirms that a rider providing qualified long-term care coverage is treated as a separate contract for these purposes.

#### 5.5 What a care event does to a projection

A care event changes four things at once, and modelling only the first understates its effect:

| Change | Direction |
|---|---|
| Expenses rise by the cost of care | Large increase |
| Withdrawals rise to fund it, raising adjusted gross income | Increase |
| Medical expenses clear the 7.5 percent floor, producing a large deduction | Tax falls sharply |
| Where one spouse enters care and the other remains at home, household costs do **not** fall | No offset |

The third row is the one that produces the planning opportunity described in Module 32: a care year is frequently the lowest-tax year of a client's life and the best Roth conversion window available.

**On cost assumptions.** No federal agency publishes an authoritative national schedule of long-term care costs. Figures used in a projection are therefore **assumptions set by the adviser**, not law, and they should be presented as such and varied in sensitivity testing. Costs differ by a factor of three or more between states and between care settings, and care cost inflation has historically exceeded general inflation.

### 6. Examples and Case Calculations

#### Example 1 — A per diem contract above the limit

A hybrid policy pays $200 a day. Actual care costs are $180 a day.

```
Benefit received      200 × 365                       73,000
Per diem limit        430 × 365                      156,950
Actual costs          180 × 365                       65,700
Excludable: the greater of the limit and actual costs 156,950
Taxable                                                    $0
```

The benefit is fully excluded because it is below the limit. Now the same policy paying $500 a day:

```
Benefit received      500 × 365                      182,500
Per diem limit                                       156,950
Actual costs          180 × 365                       65,700
Excludable: greater of 156,950 and 65,700            156,950
Taxable                                              $25,550
```

#### Example 2 — Premium caps across a couple's ages

A couple aged 58 and 72 paying $4,200 and $7,500 of premiums for qualified contracts.

```
Aged 58    premium 4,200   cap 1,860   counted as medical care    1,860
Aged 72    premium 7,500   cap 6,200   counted as medical care    6,200
                                                                  -----
                                                                  8,060
Not medical care at any level                                     3,640
```

Whether the $8,060 produces a deduction depends on clearing the 7.5 percent floor, which in an ordinary year it will not.

#### Example 3 — Medicare's contribution to a care event

A 100-day skilled nursing stay followed by two years of custodial care.

```
Days 1–20      Medicare pays in full                            $0 to the client
Days 21–100    coinsurance 80 × $217                       $17,360
Day 101 on     Medicare pays nothing
Two years of custodial care at an assumed $110,000 a year  $220,000
                                                           --------
Total borne by the household                               $237,360
```

Medicare covered twenty days. This is the gap that the whole module exists to describe.

#### Example 4 — The tax position in a care year

Continuing Example 3, second year. Retired couple, one in care.

```
Adjusted gross income, after distributions to fund care     190,000
Care costs                                                  110,000
Medicare premiums and other medical                          16,000
                                                            -------
Qualified medical expenses                                  126,000
Floor  7.5% × 190,000                                        14,250
Deductible medical                                          111,750
Plus state and local tax                                     10,000
                                                            -------
Itemised deductions                                         121,750
Standard deduction, both over 65                             35,500  — itemising wins

Taxable income                                               68,250
```

Against $190,000 of income the couple has $68,250 of taxable income. The conversion capacity this creates is quantified in Module 32.

### 7. Interactions with Other Rules

**Medical expense deduction (Module 32).** Care costs are the principal source of a deduction large enough to clear the floor, and premiums count within the age caps.

**Medicare (Module 15).** The 100-day skilled nursing limit and the exclusion of custodial care define the gap.

**Life insurance (Module 30).** Hybrid policies with long-term care riders are governed by § 7702B(e) and § 101(g), and the same per diem limit applies to a chronically ill insured.

**Roth conversions (Module 10) and required distributions (Module 09).** A care year's deduction creates conversion capacity; distributions taken to fund care raise the 7.5 percent floor.

**Death of a spouse (Module 35).** A care event is frequently followed by a death, and the two together produce the largest sequence of changes in a projection.

**Estate (Module 28).** Medicaid estate recovery, where Medicaid has paid, is a claim against the estate.

### 8. Common Scenarios and Edge Cases

**Medicare does not pay for long-term care.** It pays for skilled care after a hospital stay, for up to 100 days, and not for custodial care at all.

**The per diem limit applies to indemnity contracts, not reimbursement contracts.** A policy paying actual costs is excluded in full.

**A contract must satisfy § 7702B(b) to be qualified.** A contract with a cash surrender value is not, and its benefits are not excluded on the same basis.

**The chronically ill test requires certification within the preceding twelve months** and re-certification annually.

**Premium caps are per person and rise with age**, so a couple's deductible amount changes as they cross the bands.

**An elimination period is not a deductible.** It is a waiting period during which the insured pays, and it typically runs 30 to 100 days from the start of eligibility.

**Where one spouse enters care, household costs do not fall.** The home is maintained and the well spouse's expenses continue. Modelling a care event as a substitution rather than an addition understates it badly.

**Medicaid has a five-year look-back** on transfers, so gifting to qualify is ineffective unless done well in advance and carries its own consequences.

### 9. Planning Implications

The care event should be modelled explicitly rather than absorbed into a general expense inflation assumption. Its four simultaneous effects — expenses, withdrawals, the medical deduction and the unchanged household cost of the well spouse — cannot be represented by a single higher spending figure.

Because a care year produces an unusually low taxable income, it is the best Roth conversion window most clients will have. A projection that models the deduction correctly will surface it; one that does not will show a care year as pure loss.

The per diem limit should be checked against any indemnity policy under consideration. A benefit set well above $430 a day produces taxable income in years when actual costs are lower.

Premium deductibility should be assessed against the age caps rather than assumed. For a couple in their fifties the deductible fraction is small; from 71 it is substantial and may itself help clear the floor.

Cost assumptions should be stated as assumptions and stress-tested. There is no authoritative federal figure, regional variation is very large, and the sensitivity of the outcome to the duration of care is usually greater than its sensitivity to the annual rate.

### 10. Data Tables for the Engine

| Constant | 2026 value | Indexed |
|---|---|---|
| § 7702B(d)(4) per diem limit | **$430 a day** | Yes |
| Annual equivalent, 365 days | $156,950 | Derived |
| LTC premium caps, § 213(d)(10) | $500 · $930 · $1,860 · $4,960 · $6,200 | Yes |
| Premium caps applied | Per person, by attained age | Fixed |
| Chronically ill — activities of daily living | Unable to perform 2 of 6 for 90 days | Fixed |
| Activities of daily living | Eating, toileting, transferring, bathing, dressing, continence | Fixed |
| Reimbursement contracts | Excluded in full, no per diem cap | § 7702B(d) |
| Medicare skilled nursing | 100 days maximum; $217 a day from day 21 | Module 15 |
| Care cost | **An adviser assumption, not a statutory figure** | — |

### 11. References

[86] Internal Revenue Service, *Revenue Procedure 2025-32*, §§ 3.27 and 3.62. https://www.irs.gov/pub/irs-drop/rp-25-32.pdf

[87] 26 U.S.C. § 7702B, *Treatment of qualified long-term care insurance*. United States Code, Office of the Law Revision Counsel. https://www.govinfo.gov/app/collection/uscode

[88] 26 U.S.C. §§ 101(g) and 213(d). https://www.govinfo.gov/app/collection/uscode

[34] Centers for Medicare & Medicaid Services, *2026 Medicare Parts A & B Premiums and Deductibles*. https://www.cms.gov/newsroom/fact-sheets/2026-medicare-parts-b-premiums-deductibles

### 12. Status in This System

| Layer | Status |
|---|---|
| Projection engine | **Applied in part.** A long-term care event is modelled as a distinct expense with its own start age and duration, care costs are included in qualified medical expenses under § 213, and the age-banded premium caps are applied per person with all five bands matching Revenue Procedure 2025-32. Care cost is inflated at a rate separate from and higher than general inflation. The interaction that matters most — a care year producing a large medical deduction and therefore an unusually low tax — is modelled correctly, including the alternative minimum tax treatment recorded in Module 32. |
| Backend (`tax-be`) | **Not applied.** The roadmap projection allocates 2 percent of deployed savings to a "disability and long-term care" bucket and compounds it at the scenario rate. There is no care event, no benefit computation and no tax treatment. |
| Known limitations | Insurance **benefits** are not modelled at all. There is no per diem limit under § 7702B(d), no distinction between an indemnity contract and a reimbursement contract, and no policy structure — elimination period, benefit period, lifetime maximum or inflation rider — so a client holding a long-term care policy sees the premium as a cost and never sees the benefit as an offset. The § 7702B(c)(2) chronically ill certification and the two-of-six activities of daily living test are not applied, so the event begins on an entered age rather than on a qualifying condition. Section 101(g) accelerated death benefits and § 7702B(e) hybrid riders are absent, as is the § 1035 exchange route into a qualified contract. Medicare's 100-day skilled nursing limit and its coinsurance are not modelled, so the first phase of a care event carries no Part A cost. Medicaid eligibility, the five-year look-back and estate recovery are outside the projection entirely. |


---

## Module 34 — Health Savings Accounts

**Tax year:** 2026 · **As of:** September 2026 · **Primary authority:** IRC § 223

---

### 1. Overview and Purpose

A health savings account is the only vehicle in the Code with three separate tax advantages on the same money. Contributions are deductible, earnings accumulate without tax, and withdrawals for qualified medical expenses are tax free. No other account does all three — a traditional retirement account taxes the withdrawal, a Roth account taxes the contribution.

Eligibility depends on being covered by a **high deductible health plan** and having no other disqualifying coverage. For 2026 that means a deductible of at least **$1,700** for self-only cover or **$3,400** for family cover, with out-of-pocket exposure capped at **$8,500** and **$17,000** respectively.[89]

The provision is most valuable when used least. An account funded annually and left untouched, with medical costs paid from other funds, compounds for decades and then meets exactly the expense it was designed for — because health costs in later life are large and certain. After age 65 the account also becomes a general retirement account: withdrawals for any purpose are permitted, taxed as ordinary income but without penalty.

Eligibility ends on enrolment in Medicare, which makes the years before 65 the whole of the contribution window for most people.

### 2. Governing Law and Authorities

| Type | Citation | What it establishes |
|---|---|---|
| Statute | IRC § 223(a) | Deduction for contributions |
| Statute | IRC § 223(b) | Contribution limits and the age-55 catch-up |
| Statute | IRC § 223(b)(8) | Last-month rule and the testing period |
| Statute | IRC § 223(c)(1) | Eligible individual; disqualifying coverage |
| Statute | IRC § 223(c)(2) | High deductible health plan |
| Statute | IRC § 223(d)(2) | Qualified medical expenses |
| Statute | IRC § 223(f)(4) | 20 percent additional tax before 65 |
| Statute | IRC § 223(f)(8) | Treatment on death |
| Legislation | P.L. 119-21, §§ 71306–71308 | Telehealth safe harbour, bronze and catastrophic plans, direct primary care |
| Guidance | Rev. Proc. 2025-19 | 2026 contribution and plan limits |

### 3. Key Definitions

| Term | Definition |
|---|---|
| **Eligible individual** | An individual covered by a high deductible health plan, not covered by other health coverage with limited exceptions, not enrolled in Medicare, and not claimed as another's dependant. |
| **High deductible health plan** | A plan with a deductible at or above the statutory minimum and out-of-pocket exposure at or below the statutory maximum.[89] |
| **Qualified medical expense** | An expense that would be deductible under § 213(d), determined without regard to the 7.5 percent floor. Insurance premiums generally do not qualify, with four exceptions. |
| **Last-month rule** | An individual eligible on 1 December may contribute the full annual amount for that year, subject to remaining eligible throughout the following calendar year. |
| **Testing period** | The 12 months following the last month of the year in which the last-month rule was used. |

### 4. Who Is Affected

Anyone covered by a qualifying plan and not otherwise disqualified. Three disqualifiers catch people unexpectedly:

- **Medicare enrolment**, including Part A alone. Enrolment is often automatic on claiming Social Security, so a person working past 65 who claims benefits loses eligibility.
- **A general-purpose health flexible spending arrangement**, including a spouse's, because it constitutes other coverage.
- **Being claimed as a dependant** on someone else's return.

An adult child under 26 covered by a parent's family high deductible plan but **not** a dependant may open their own account and contribute the **family** maximum, which is a substantial and widely missed opportunity.

### 5. Core Rules and Calculations

#### 5.1 Case Register

| # | Case | Applied |
|---|---|---|
| 1 | Deductible contribution | **No** — no health savings account is modelled |
| 2 | Self-only and family limits | Constants held only in the backend |
| 3 | Age-55 catch-up of $1,000 | **No** |
| 4 | Catch-up is per individual, requiring separate accounts | **No** |
| 5 | Tax-free growth | **No** |
| 6 | Tax-free withdrawal for qualified medical expenses | **No** |
| 7 | Contributions cease on Medicare enrolment | **No** |
| 8 | Six-month Medicare look-back on late enrolment | **No** |
| 9 | 20 percent additional tax before 65 for non-medical use | **No** |
| 10 | Ordinary income treatment after 65 for non-medical use | **No** |
| 11 | Reimbursement of prior-year expenses without time limit | **No** |
| 12 | Last-month rule and the testing period | **No** |
| 13 | Spouse as beneficiary — account continues | **No** |
| 14 | Non-spouse beneficiary — fully taxable in the year of death | **No** |
| 15 | Premiums qualifying after 65 | **No** |

Nothing in this module is implemented in the projection engine.

#### 5.2 The 2026 amounts

| Item | Self-only | Family |
|---|---|---|
| Contribution limit, § 223(b)(2) | **$4,400** | **$8,750** |
| Minimum plan deductible, § 223(c)(2)(A) | **$1,700** | **$3,400** |
| Maximum out-of-pocket | **$8,500** | **$17,000** |
| Catch-up, age 55 and over, § 223(b)(3) | **$1,000** | **$1,000 each** |

All figures except the catch-up are indexed. The **$1,000 catch-up is fixed by statute and has never been adjusted**.

The catch-up is **per eligible individual**, not per account. A married couple both aged 55 or over may contribute $8,750 plus $1,000 each — but the second $1,000 must go into a **separate account in the other spouse's name**, because an account has a single owner. This is the most common administrative error in the area.

#### 5.3 The three exemptions, and the fourth stage

```
Contribution     deductible above the line — no itemising required
Growth           no tax on interest, dividends or gains
Withdrawal       tax free if used for qualified medical expenses
```

A contribution made through payroll under a cafeteria plan also escapes **employment tax**, which no other retirement contribution does. That makes payroll funding worth roughly 7.65 percent more than writing a cheque.

After age 65 a fourth stage opens. Withdrawals for **any** purpose are permitted without the 20 percent additional tax, and are simply ordinary income — the account behaves like a traditional individual retirement account. Before 65 a non-medical withdrawal is ordinary income **plus 20 percent**.

#### 5.4 What qualifies, and premiums

Qualified medical expenses are those deductible under § 213(d) without regard to the floor. Insurance **premiums** are generally excluded, with four exceptions:

- long-term care insurance, within the § 213(d)(10) age caps in Module 32;
- health coverage while receiving unemployment compensation;
- continuation coverage under COBRA; and
- for an individual aged 65 or over, **Medicare Part B, Part D and Medicare Advantage premiums** — but **not** a Medigap supplement.

The Medicare exception is what makes the account so well suited to retirement. Part B alone is $2,434.80 a year per person in 2026, before any income-related surcharge, and it can be paid from the account tax free.

#### 5.5 The reimbursement rule

There is **no time limit** on reimbursing a qualified expense from the account, provided the expense was incurred after the account was established and was not otherwise deducted or reimbursed.

A taxpayer may therefore pay medical costs from taxable funds, keep the receipts, allow the account to compound for thirty years, and withdraw tax free at any later time against those preserved receipts. The account becomes, in substance, a Roth account with no required distributions and no five-year rule.

The whole of that strategy rests on record-keeping. Without receipts the withdrawal is a non-medical distribution.

#### 5.6 The Medicare cut-off and the six-month look-back

Eligibility ends in the month Medicare coverage begins. Where enrolment is delayed past 65, Part A coverage is granted **retroactively for up to six months**, so contributions made in that retrospective window become excess contributions subject to a 6 percent excise tax.

The practical rule is to stop contributions six months before Medicare enrolment, and the year of enrolment is pro-rated by month.

#### 5.7 Changes for 2026

The One Big Beautiful Bill Act made three changes that widen eligibility:[90]

| Change | Effect |
|---|---|
| § 71306 | The telehealth safe harbour is **permanent** — a plan does not fail to be a high deductible health plan by having no deductible for telehealth and other remote care |
| § 71307 | **Bronze and catastrophic** plans on an Exchange are treated as high deductible health plans, so purchasers of those plans become eligible |
| § 71308 | A **direct primary care service arrangement** is not other coverage, so it no longer disqualifies — subject to a fee cap of **$150 a month**, or $300 for an arrangement covering more than one individual |

#### 5.8 On death

| Beneficiary | Treatment |
|---|---|
| **Spouse** | The account becomes the spouse's own health savings account. No tax. |
| **Non-spouse** | The account **ceases to be** a health savings account. The full fair market value is **ordinary income to the beneficiary in the year of death**, reduced only by the decedent's qualified medical expenses paid within one year. |
| **Estate** | Included in the decedent's final return as income. |

The non-spouse outcome is severe: no ten-year spread, no step-up, immediate full taxation. A health savings account is therefore a poor asset to leave to children and an excellent one to spend, or to leave to a spouse or to charity.

### 6. Examples and Case Calculations

#### Example 1 — The receipt-preservation strategy

A couple both aged 50 contribute the family maximum for fifteen years, pay medical costs from taxable funds, and keep receipts. Assume 7 percent growth and, for clarity, a level $8,750 contribution.

```
Contributed over 15 years        8,750 × 15                131,250
Value at 7 percent after 15 years                        ≈ 234,000
Income tax saved on contributions at 24 percent             31,500
Employment tax saved if funded through payroll at 7.65%      10,041
Preserved receipts available to withdraw against            131,250+
```

The account is worth $234,000, none of it has been taxed, and the accumulated receipts permit a large tax-free withdrawal at any time.

#### Example 2 — Paying Medicare from the account

A retired couple, both 68, both paying the standard Part B premium and a Part D plan.

```
Part B   202.90 × 12 × 2                                   4,869.60
Part D    45.00 × 12 × 2                                   1,080.00
                                                           --------
Paid from the health savings account, tax free             5,949.60

The equivalent from a traditional IRA, at a 22 percent rate,
would require a gross withdrawal of                        7,627.69
```

A Medigap supplement premium would **not** qualify, which is a distinction worth checking before setting up the payment.

#### Example 3 — The married catch-up trap

A couple both aged 57 with family coverage.

```
Family limit, one account                                     8,750
Catch-up, spouse A                                            1,000
Catch-up, spouse B                                            1,000
                                                             ------
Total contributable                                          10,750

But: the second $1,000 must be contributed to a SEPARATE
account in spouse B's name. Putting $10,750 into one account
creates a $1,000 excess contribution, taxed at 6 percent a year
until corrected.
```

#### Example 4 — Death with a non-spouse beneficiary

An account worth $300,000 passes to a child in the 32 percent bracket.

```
Fair market value at death                                  300,000
Income to the beneficiary in the year of death              300,000
Tax at 32 percent                                           $96,000
Net to the child                                           $204,000
```

The same $300,000 in a taxable brokerage account would have received a step-up under Module 31 and passed with no income tax at all.

### 7. Interactions with Other Rules

**Medical expense deduction (Module 32).** Expenses paid from a health savings account cannot also be deducted. The two are alternatives, and the account is generally better because it does not face the 7.5 percent floor.

**Medicare (Modules 15 and 16).** Enrolment ends eligibility, but the account may then pay Part B, Part D and Advantage premiums — and the income-related surcharge — tax free.

**Long-term care (Module 33).** Long-term care premiums qualify within the § 213(d)(10) age caps.

**Required distributions (Module 09).** A health savings account has **none** during the owner's lifetime, which distinguishes it from every pre-tax retirement account.

**Roth accounts (Module 10).** With receipts preserved, the account behaves better than a Roth: deductible going in, tax free coming out, and no five-year rule.

**Step-up in basis (Module 31).** A health savings account receives no step-up and is fully taxable to a non-spouse beneficiary, which places it alongside pre-tax retirement accounts as an asset to spend rather than bequeath.

### 8. Common Scenarios and Edge Cases

**Medicare enrolment ends eligibility**, including Part A alone, and Part A is often automatic on claiming Social Security.

**Stop contributing six months before enrolment** because of the retroactive coverage rule.

**A spouse's general-purpose flexible spending arrangement disqualifies both.** A limited-purpose arrangement covering only dental and vision does not.

**The catch-up needs two accounts.** One account cannot hold two people's catch-up contributions.

**There is no deadline for reimbursement.** Receipts from twenty years ago remain valid if the expense was incurred after the account was opened.

**Premiums generally do not qualify** — except long-term care, COBRA, coverage while unemployed, and Medicare after 65. A Medigap supplement never qualifies.

**An adult child on a parent's family plan who is not a dependant can contribute the family maximum** to their own account.

**A non-spouse beneficiary is taxed on the whole value immediately.** There is no spreading.

**Excess contributions attract 6 percent a year** until corrected.

**Bronze and catastrophic Exchange plans now qualify**, which is new for 2026 and widens eligibility considerably for the self-employed.

### 9. Planning Implications

For a client with a qualifying plan, the account should be funded to the maximum before any non-matched retirement contribution. The three exemptions, plus the employment tax saving when funded through payroll, make it the most efficient dollar available.

Medical costs should be paid from taxable funds where cash flow permits, with receipts preserved. The account then compounds untaxed and the accumulated receipts provide a tax-free withdrawal capacity available at any time and for any reason.

The contribution window closes at Medicare. For a client approaching 65, maximising contributions in the final eligible years — including the year of enrolment on a pro-rated basis, and stopping six months before — is worth doing deliberately.

In retirement the account should be used for Medicare premiums, where it converts a certain expense into a tax-free one.

For estate purposes the account should be spent, left to a spouse, or left to charity. Leaving it to a child produces immediate full taxation, and Example 4 quantifies the difference against a taxable account.

### 10. Data Tables for the Engine

| Constant | 2026 value | Indexed |
|---|---|---|
| Contribution limit, self-only | **$4,400** | Yes |
| Contribution limit, family | **$8,750** | Yes |
| Catch-up, age 55 and over | **$1,000** | **No — fixed by statute** |
| Minimum deductible, self-only | **$1,700** | Yes |
| Minimum deductible, family | **$3,400** | Yes |
| Maximum out-of-pocket, self-only | **$8,500** | Yes |
| Maximum out-of-pocket, family | **$17,000** | Yes |
| Additional tax, non-medical before 65 | 20 percent | Fixed |
| After 65, non-medical | Ordinary income, no additional tax | Fixed |
| Direct primary care fee cap | $150 a month, $300 for more than one individual | P.L. 119-21 § 71308 |
| Excess contribution excise | 6 percent a year | § 4973 |
| Required distributions | **None during life** | — |

### 11. References

[89] Internal Revenue Service, *Revenue Procedure 2025-19*, § 2.01. https://www.irs.gov/pub/irs-drop/rp-25-19.pdf

[90] One Big Beautiful Bill Act, P.L. 119-21, §§ 71306, 71307 and 71308, amending IRC § 223(c). https://www.govinfo.gov/content/pkg/PLAW-119publ21/html/PLAW-119publ21.htm

[91] 26 U.S.C. § 223, *Health savings accounts*. United States Code, Office of the Law Revision Counsel. https://www.govinfo.gov/app/collection/uscode

[92] Internal Revenue Service, *Publication 969, Health Savings Accounts and Other Tax-Favored Health Plans*. https://www.irs.gov/publications/p969

### 12. Status in This System

| Layer | Status |
|---|---|
| Projection engine | **Not applied.** No health savings account exists in the projection. There is no contribution, no balance, no growth and no withdrawal, so the most tax-efficient account available to a pre-Medicare client is absent from the plan entirely. |
| Backend (`tax-be`) | **Constants only, and stale.** `taxRoadmapController.js` holds `hsaSelf: 4300` and `hsaFamily: 8550`, which are the **2025** figures against 2026 amounts of $4,400 and $8,750. They are reference data and are not used in any computation. `strategyPhaseMap.js` catalogues "Health Savings Account (HSA) Optimization" as a named strategy. |
| Known limitations | The whole module is unimplemented. The practical consequences for a projection are three. A client funding an account to the maximum from age 45 to 64 accumulates a substantial balance that never appears on the balance sheet. The tax-free payment of Medicare premiums from age 65 is not available, so those premiums are modelled as being met from taxed dollars. And the account's estate treatment — no step-up, and full immediate taxation to a non-spouse beneficiary — is not reflected in the legacy figure, which overstates what reaches heirs where a client holds one. The stale backend constants should also be corrected to the 2026 amounts, and are recorded with the other 2025 figures at D6. |


---

## Module 35 — Death of a Spouse

**Tax year:** 2026 · **As of:** September 2026 · **Primary authority:** IRC §§ 1, 2(a), 63, 86, 401(a)(9)(B)(iv), 6013; Social Security Act § 202

---

### 1. Overview and Purpose

The death of a spouse is the largest single change in a retirement projection, and it is the only one that is certain to occur. It changes income, deductions, rate schedule, benefit entitlement, retirement account rules and Medicare premiums simultaneously, and every change moves in the same direction.

Income falls, because the smaller of two Social Security benefits ends. Tax rises, because the survivor moves from the joint rate schedule to the single schedule and the standard deduction roughly halves. The taxable share of the remaining benefit rises, because the § 86 thresholds fall by a third. And the Medicare surcharge threshold halves, so the same income can move a survivor up two tiers.

The combined effect on cash after tax is substantially worse than the fall in gross income alone suggests. In the worked case at § 6, gross income falls 12 percent while federal tax rises 29.5 percent, so cash after tax falls **16.9 percent**.

This module assembles the consequences that the other modules establish individually. It also sets out the one area with genuine choice — how a surviving spouse takes over a retirement account — where the rules changed in 2024 and the right answer depends on facts a projection can identify in advance.

**A note on the examples.** Every rate, threshold and rule in this module is taken from the sources cited. The client figures in the worked cases are **stated inputs** chosen to show the mechanism, not data drawn from any source, and are identified as such.

### 2. Governing Law and Authorities

| Type | Citation | What it establishes |
|---|---|---|
| Statute | IRC § 6013(a)(3) | Joint return for the year of death |
| Statute | IRC § 2(a) | Surviving spouse status for two following years |
| Statute | IRC § 1(j)(2) | The rate schedules |
| Statute | IRC § 63(c), (f) | Standard deduction and the age-65 addition |
| Statute | IRC § 86(c) | Base amounts for taxing benefits |
| Statute | IRC § 401(a)(9)(B)(iv) | Surviving spouse election to be treated as the employee |
| Legislation | SECURE 2.0 Act § 327, P.L. 117-328 | Enacted that election; Uniform Lifetime Table applies |
| Statute | Social Security Act § 202(e), (f) | Survivor benefits |
| Regulation | 20 CFR § 418.1205 | Death of a spouse as a Medicare life-changing event |
| Guidance | POMS RS 00615.020, RS 00615.301, RS 00615.320 | Dual entitlement; survivor reduction; RIB-LIM |
| Guidance | IRS Publication 590-B | Spousal beneficiary options and tables |

### 3. Key Definitions

| Term | Definition |
|---|---|
| **Year of death** | The taxable year in which the spouse died. A joint return may be filed for it. |
| **Surviving spouse, § 2(a)** | A taxpayer entitled to use the joint rate schedule for the **two years following** the year of death, requiring a dependent son, stepson, daughter or stepdaughter in the household and no remarriage. |
| **Qualifying survivor benefit** | The higher of the two Social Security benefits. The smaller ends. |
| **Spousal rollover** | The survivor treats an inherited retirement account as their own. |
| **Section 327 election** | An irrevocable election by a sole-beneficiary spouse to be treated as the deceased employee for distribution purposes.[93] |

### 4. Who Is Affected

Every married household, at a date that is unknown but certain. The magnitude of the effect depends on three things: the gap between the two Social Security benefits, the size of pre-tax retirement balances, and whether income sits near a Medicare surcharge threshold.

Households with **similar** benefits and modest pre-tax balances see a small effect. Households with one large benefit and one small one, and substantial required distributions, see the largest.

### 5. Core Rules and Calculations

#### 5.1 Case Register

| # | Case | Applied |
|---|---|---|
| 1 | Joint return permitted for the year of death | Yes |
| 2 | § 2(a) surviving spouse status for two years | Yes — on the clock alone |
| 3 | § 2(a) dependent child requirement | **No** — Module 03 |
| 4 | Change to the single rate schedule | Yes |
| 5 | Standard deduction falls to the single amount | Yes |
| 6 | § 63(f) addition rises from $1,650 to $2,050 | Yes |
| 7 | Smaller Social Security benefit ends | Yes |
| 8 | Survivor benefit reduced for early claiming | **No** — D3 |
| 9 | RIB-LIM limitation | **No** — D3 |
| 10 | § 86 thresholds fall to $25,000 and $34,000 | Yes |
| 11 | Medicare surcharge threshold halves | Yes |
| 12 | Death as a Medicare life-changing event | **No** |
| 13 | Net investment income tax threshold falls | Yes |
| 14 | Capital loss limitation unchanged at $3,000 | Yes |
| 15 | Spousal rollover of retirement accounts | Yes, in effect |
| 16 | Remaining a beneficiary instead | **No** |
| 17 | § 327 election to be treated as the employee | **No** |
| 18 | § 72(t) exposure differing between the two routes | **No** |
| 19 | Household expenses do not halve | Yes |
| 20 | Basis step-up on the decedent's assets | Partially — Module 31 |
| 21 | Suspended passive losses limited by the step-up | **No** |
| 22 | Portability election preserving the DSUE | Yes — as an input |

#### 5.2 The sequence of filing status

| Year | Status | Schedule | Standard deduction, both over 65 |
|---|---|---|---|
| Year of death | Married filing jointly, § 6013(a)(3) | Joint | $35,500 |
| Following year | **Single**, unless § 2(a) is met | Single | $18,150 |
| Second following year | Single, unless § 2(a) is met | Single | $18,150 |

Surviving spouse status under § 2(a) requires a dependent son, stepson, daughter or stepdaughter maintained in the household. Most retired households have none, so the change to the single schedule happens **in the year after death**, not three years later. Module 03 sets out the test.

#### 5.3 What changes, and by how much

| Item | Married filing jointly | Single | Change |
|---|---|---|---|
| Standard deduction, both over 65 | $35,500 | $18,150 | **−$17,350** |
| 22 percent bracket begins | $100,800 | $50,400 | Halved |
| 24 percent bracket begins | $211,400 | $105,700 | Halved |
| § 86 first threshold | $32,000 | $25,000 | −$7,000 |
| § 86 second threshold | $44,000 | $34,000 | −$10,000 |
| Medicare surcharge, first tier | $218,000 | $109,000 | Halved |
| Net investment income tax threshold | $250,000 | $200,000 | −$50,000 |
| Social Security received | Both benefits | **Higher only** | Smaller benefit lost |

Every line moves against the survivor.

#### 5.4 Retirement accounts — the one real choice

A surviving spouse who is the sole beneficiary has three routes, and they differ in ways that matter.[94]

| | Treat as own | Remain a beneficiary | § 327 election |
|---|---|---|---|
| Table used | **Uniform Lifetime**, survivor's age | **Single Life**, survivor's age | **Uniform Lifetime**[93] |
| Distributions begin | Survivor's own applicable age, 73 or 75 | 31 December of the year after death, if the deceased had reached the required beginning date | When the **deceased** would have reached the applicable age |
| § 72(t) 10 percent additional tax before 59½ | **Applies** | **Does not apply** | Does not apply |
| Revocable | — | Can later roll over to own | **Irrevocable** except with the Secretary's consent |

Two decision rules follow directly.

**A survivor under 59½ who needs the money should remain a beneficiary.** Distributions from an inherited account escape the 10 percent additional tax entirely; the same withdrawal after a rollover attracts it. Rolling over first and withdrawing afterwards is a costly error that cannot be undone.

**Where the deceased spouse was the younger of the two, the § 327 election defers distributions.** Enacted by SECURE 2.0 § 327 and effective for calendar years beginning after 31 December 2023, it treats the survivor as the deceased employee, so distributions need not begin until the deceased **would have** reached the applicable age.[93] The statute also directs that the **Uniform Lifetime Table** apply, which produces a smaller required amount than the Single Life Table. The election is irrevocable and requires timely notice to the plan administrator.

Where the deceased was older and the survivor is over 59½, a spousal rollover is usually simplest and gives the longest deferral on the survivor's own schedule.

#### 5.5 Expenses do not halve

A survivor keeps the same house, the same property tax, the same insurance and the same maintenance. Research on single-person against two-person consumer units supports a survivor's spending at roughly **70 to 80 percent** of the couple's, not 50 percent.

Healthcare falls to one person's Medicare premiums, which is a genuine reduction, but it is the only large one.

Modelling a survivor's expenses at half the couple's is the most common error in this area and it conceals the shortfall that the income and tax changes create.

### 6. Examples and Case Calculations

The client figures below are **stated inputs** chosen to show the mechanism. Every rate, threshold and deduction is from the sources cited.

#### Example 1 — The full effect, at age 78

A couple with Social Security of $3,600 and $1,800 a month, required distributions of $95,000, and $20,000 of other income. Both over 65.

**As a couple**

```
Social Security received                            64,800
Required distributions                              95,000
Other income                                        20,000
Taxable Social Security, § 86                       55,080   85% of benefit
Adjusted gross income                              170,080
Standard deduction  32,200 + 2 × 1,650              35,500
Taxable income                                     134,580
Federal tax                                        $19,032
Cash after federal tax                            $160,768
```

**As a survivor, the following year — same distributions, same other income**

```
Social Security received                            43,200   smaller benefit lost
Required distributions                              95,000
Other income                                        20,000
Taxable Social Security, § 86                       36,720   85% of benefit
Adjusted gross income                              151,720
Standard deduction  16,100 + 2,050                  18,150
Taxable income                                     133,570
Federal tax                                        $24,655
Cash after federal tax                            $133,545
```

**The effect**

| | Couple | Survivor | Change |
|---|---|---|---|
| Gross income | $179,800 | $158,200 | **−12.0%** |
| Taxable income | $134,580 | $133,570 | −0.8% |
| Federal tax | $19,032 | $24,655 | **+29.5%** |
| Cash after federal tax | $160,768 | $133,545 | **−16.9%** |

Taxable income barely moves, because the $21,600 of lost benefit is almost exactly offset by the $17,350 fall in the standard deduction and the narrower § 86 thresholds. The **tax** rises by nearly 30 percent because the same taxable income is now run through the single schedule.

#### Example 2 — A survivor under 59½

A spouse aged 54 inherits a $900,000 individual retirement account and needs $60,000 a year.

```
ROLLED OVER TO HER OWN ACCOUNT
   Withdrawal                                          60,000
   Ordinary income tax at 22 percent                    13,200
   § 72(t) additional tax, 10 percent                    6,000
                                                        ------
                                                        19,200

REMAINED A BENEFICIARY
   Withdrawal                                          60,000
   Ordinary income tax at 22 percent                    13,200
   § 72(t) additional tax                                    0
                                                        ------
                                                        13,200
```

$6,000 a year, for the eleven years to 59½ — $66,000 — turns entirely on a decision made in the weeks after a death. Remaining a beneficiary preserves the option to roll over later; rolling over first forecloses it.

#### Example 3 — The § 327 election where the deceased was younger

A survivor aged 74 whose spouse died at 66, born in 1960 so with an applicable age of 75.

```
SPOUSAL ROLLOVER
   Survivor's own applicable age                           75
   Distributions begin next year, on the survivor's age

§ 327 ELECTION
   Treated as the deceased employee
   Distributions need not begin until the deceased
   would have reached 75 — nine years away
   Uniform Lifetime Table applies when they do
```

Nine years of deferral, and nine years of low taxable income in which Roth conversions can be made at the survivor's single-filer rates. The election is irrevocable, so it should be modelled before it is made.

#### Example 4 — The Medicare consequence

The couple in Example 1, with modified adjusted gross income of $170,080 two years before.

```
As a couple    threshold 218,000    below it        standard premium
As a survivor  threshold 109,000    above it        tier 3

Part B  405.80 a month against 202.90
Part D   37.50 a month against 0
Additional annual cost, one person                   $2,884.80
```

Death **is** a life-changing event under 20 CFR § 418.1205(a), so a new initial determination can be requested on Form SSA-44 using the survivor's expected income. This is one of the few reliefs available and it should be filed alongside the other post-death administration.

### 7. Interactions with Other Rules

**Filing status (Module 03).** Supplies the § 2(a) test and the year-of-death rule.

**Standard deduction (Module 02).** The $17,350 fall is half of the arithmetic in Example 1.

**Spousal and survivor benefits (Module 12).** Supplies the income side, including RIB-LIM and the survivor reduction that the engine does not apply.

**Taxation of benefits (Module 14).** The § 86 thresholds fall by roughly a third.

**Required distributions (Module 09).** The spousal options in § 5.4 determine the survivor's distribution schedule for the rest of their life.

**Medicare surcharge (Module 16).** The threshold halves, and death is a qualifying life-changing event.

**Estate tax (Module 28).** The portability election at the first death preserves up to $15,000,000 of exclusion and requires a return.

**Step-up in basis (Module 31).** The decedent's assets are stepped up; in a community property state both halves are.

**Passive activity losses (Module 25).** Section 469(g)(2) allows suspended losses at death only above the step-up, so they are usually lost.

### 8. Common Scenarios and Edge Cases

**The change happens in the year after death, not three years later.** Surviving spouse status needs a dependent child, which most retired households lack.

**A joint return is still available for the year of death.**

**Taxable income can be almost unchanged while tax rises sharply.** Example 1 shows a 0.8 percent fall in taxable income producing a 29.5 percent rise in tax.

**A survivor under 59½ should not roll over before withdrawing.** The 10 percent additional tax applies to a rollover account and not to an inherited one.

**The § 327 election is irrevocable.** It is valuable where the deceased was younger and harmful where the deceased was older.

**Expenses fall by 20 to 30 percent, not by half.**

**Death is a Medicare life-changing event**, so Form SSA-44 is available.

**The portability return is due nine months after death**, extendable to fifteen, with a late procedure available for smaller estates.

**Two Social Security benefits never continue.** The survivor keeps the higher.

### 9. Planning Implications

The asymmetry between the joint and single schedules is the strongest argument in the system for recognising income while both spouses are alive. A Roth conversion made jointly is taxed on the wider schedule with the larger deduction; the same conversion by a survivor is taxed on the narrower one. Modules 09, 10 and 14 all point at the same window, and this module supplies the reason it closes.

Deferring the **higher** earner's Social Security benefit raises the floor under the survivor's income for what may be twenty or more years, and Module 12 quantifies it. That single decision does more for a survivor than any post-death action.

The retirement account decision in § 5.4 should be made deliberately and modelled first, because two of the three routes are effectively irreversible. For a survivor under 59½ the answer is almost always to remain a beneficiary; where the deceased was younger the § 327 election is worth years of deferral.

Reducing pre-tax balances before the first death reduces the required distributions that will be taxed on the survivor's narrower schedule. This is the same argument as Module 09 makes for the pre-distribution window, with an additional reason.

A survivor's expenses should be modelled at 70 to 80 percent of the couple's, and the projection should show the cash shortfall that follows rather than assuming the household simply costs half as much.

### 10. Data Tables for the Engine

| Change on the death of a spouse | From | To |
|---|---|---|
| Rate schedule | § 1(j)(2)(A) joint | § 1(j)(2)(C) single |
| Standard deduction | $32,200 | $16,100 |
| § 63(f) addition, per person | $1,650 | $2,050 |
| § 86 base amount | $32,000 | $25,000 |
| § 86 adjusted base amount | $44,000 | $34,000 |
| Medicare surcharge first tier | $218,000 | $109,000 |
| Net investment income tax threshold | $250,000 | $200,000 |
| Social Security | Both benefits | Higher only |
| Household expenses | 100% | **70–80%** |
| Year of death filing | Joint permitted | § 6013(a)(3) |
| § 2(a) status | Two years, with a dependent child | Otherwise single immediately |

### 11. References

[93] SECURE 2.0 Act of 2022, § 327, Division T of P.L. 117-328, amending IRC § 401(a)(9)(B)(iv). https://www.govinfo.gov/content/pkg/PLAW-117publ328/html/PLAW-117publ328.htm

[94] Internal Revenue Service, *Publication 590-B, Distributions from Individual Retirement Arrangements*. https://www.irs.gov/publications/p590b

[26] Social Security Administration, *POMS RS 00615.020*. https://secure.ssa.gov/poms.nsf/lnx/0300615020

[28] Social Security Administration, *POMS RS 00615.320*. https://secure.ssa.gov/poms.nsf/lnx/0300615320

[37] 20 CFR § 418.1205. https://www.ecfr.gov/current/title-20/chapter-III/part-418/subpart-B/section-418.1205

[9] 26 U.S.C. §§ 2, 6013 and 7703. https://www.govinfo.gov/app/collection/uscode

### 12. Status in This System

| Layer | Status |
|---|---|
| Projection engine | **Applied, and it is one of the better-modelled events in the system.** Filing status changes on death, and joint filing is correctly retained for the year of death itself rather than switching immediately. The standard deduction moves to the single amount and the § 63(f) addition correctly rises from $1,650 to $2,050. The smaller Social Security benefit ends and the survivor keeps the higher. The § 86 thresholds, the Medicare surcharge threshold and the net investment income tax threshold all move to their single-filer values. Household expenses are reduced by a survivor factor rather than halved. The engine therefore reproduces the shape of Example 1 correctly. |
| Backend (`tax-be`) | **Not applied.** No life events of any kind. |
| Known limitations | The survivor benefit itself is computed from the bare primary insurance amount with no claiming adjustment, no survivor full retirement age and no RIB-LIM, so the **amount** the survivor keeps is overstated where the deceased claimed early — recorded as D3 and set out in Module 12. Surviving spouse status is applied on the two-year clock without testing the § 2(a) dependent-child requirement, so a household with no qualifying child is given two years of joint rates it is not entitled to, recorded in Module 03. The retirement account decision in § 5.4 is not modelled at all: the engine assumes a spousal rollover, so it cannot show the § 72(t) exposure that makes remaining a beneficiary correct for a survivor under 59½, and it cannot represent the § 327 election that defers distributions where the deceased was younger. Death is not treated as a Medicare life-changing event, so no relief is available in the projection. The § 469(g)(2) limitation on suspended passive losses at death is absent. |


---

## Module 36 — Divorce

**Tax year:** 2026 · **As of:** September 2026 · **Primary authority:** IRC §§ 1041, 414(p), 72(t)(2)(C), 408(d)(6)

---

### 1. Overview and Purpose

Divorce divides assets that carry embedded tax attributes, and the division is only equal if those attributes are taken into account. Two accounts of identical statement value can be worth materially different amounts after tax, and a settlement that splits balances rather than after-tax values transfers value from one party to the other without either intending it.

Three provisions do most of the work. Section 1041 makes transfers between spouses, and transfers incident to divorce, **non-taxable** — but with **carryover basis**, so the gain travels with the asset. A **qualified domestic relations order** under § 414(p) is the only route by which an employer retirement plan may be divided, and a distribution to an alternate payee under one escapes the 10 percent additional tax by § 72(t)(2)(C). And individual retirement accounts are divided by a different mechanism entirely, under § 408(d)(6), which a QDRO does not reach.

Alimony changed fundamentally for instruments executed after 2018. It is no longer deductible by the payer and no longer income to the recipient, which reversed the economics of every settlement negotiated on the old basis.

### 2. Governing Law and Authorities

| Type | Citation | What it establishes |
|---|---|---|
| Statute | IRC § 1041(a) | No gain or loss on transfers between spouses or incident to divorce |
| Statute | IRC § 1041(b) | Treated as a gift; transferee takes the transferor's basis |
| Statute | IRC § 1041(c) | "Incident to divorce" defined |
| Statute | IRC § 414(p) | Qualified domestic relations order |
| Statute | IRC § 401(a)(13) | Anti-alienation, and the QDRO exception to it |
| Statute | IRC § 72(t)(2)(C) | No 10 percent additional tax on a payment to an alternate payee |
| Statute | IRC § 408(d)(6) | Transfer of an individual retirement account incident to divorce |
| Statute | IRC § 1366(d)(2)(B) | Suspended S corporation losses transfer with the stock |
| Statute | IRC § 2516 | Certain property settlements not treated as gifts |
| Statute | IRC § 121(d)(3) | Principal residence exclusion after divorce |
| Statute | IRC § 7703(a) | Marital status at the close of the year |
| Legislation | P.L. 115-97, § 11051 | Repealed the alimony deduction and inclusion |

### 3. Key Definitions

| Term | Definition |
|---|---|
| **Incident to divorce** | A transfer occurring **within one year** after the marriage ceases, or **related to the cessation** of the marriage.[95] |
| **Qualified domestic relations order** | A domestic relations order creating or recognising an alternate payee's right to receive all or part of a participant's plan benefits, and meeting the specification requirements of § 414(p)(2) and (3).[96] |
| **Alternate payee** | A spouse, former spouse, child or other dependant of a participant recognised by a QDRO. |
| **Divorce or separation instrument** | A decree of divorce or separate maintenance, a written separation agreement, or a support decree. Its **execution date** determines the alimony treatment. |

### 4. Who Is Affected

Any divorcing couple. Marital status for the whole tax year is determined **at the close of the year** under § 7703(a), so a decree entered on 31 December makes both parties unmarried for that entire year, and one entered on 2 January leaves them married for all of the preceding year.

The provisions matter most where the marital estate contains retirement accounts, appreciated property or a closely held business — that is, where the embedded tax attributes are large relative to the balances.

### 5. Core Rules and Calculations

#### 5.1 Case Register

| # | Case | Applied |
|---|---|---|
| 1 | § 1041 non-recognition on transfer | **No** — divorce is not modelled |
| 2 | § 1041(b) carryover basis to the transferee | **No** |
| 3 | § 1041(c) one-year and related-to-cessation tests | **No** |
| 4 | § 414(p) QDRO division of an employer plan | **No** |
| 5 | § 72(t)(2)(C) exception for an alternate payee | **No** |
| 6 | § 408(d)(6) transfer of an individual retirement account | **No** |
| 7 | Alimony not deductible for post-2018 instruments | **No** |
| 8 | Pre-2019 instruments grandfathered | **No** |
| 9 | Filing status determined at year end | Partially — status is an input |
| 10 | § 121(d)(3) residence exclusion after divorce | **No** |
| 11 | § 1366(d)(2)(B) transfer of suspended losses | **No** |
| 12 | § 2516 property settlements outside the gift tax | **No** |
| 13 | Divorced spouse Social Security benefit | **No** — Module 12 |
| 14 | Divorce as a Medicare life-changing event | **No** |

Divorce is not modelled anywhere in the projection.

#### 5.2 Section 1041 — the transfer rule

```
Transfer to a spouse, or to a former spouse incident to divorce
   → no gain or loss recognised
   → treated as acquired by GIFT
   → transferee takes the TRANSFEROR'S adjusted basis
```

A transfer is incident to divorce if it occurs within one year after the marriage ceases, **or** is related to the cessation of the marriage.[95] The second limb is broader and covers transfers made under the divorce instrument some years later.

The consequence that matters is **carryover basis**. The recipient inherits the gain, and two assets of equal value are not of equal worth.

```
Brokerage account   value 500,000   basis 500,000   embedded gain        0
Brokerage account   value 500,000   basis 100,000   embedded gain  400,000

At a 15 percent long-term rate the second is worth 60,000 less after tax.
```

An equal split of statement values is an unequal split of after-tax value.

#### 5.3 Dividing retirement accounts — two different mechanisms

This is the most consequential technical point in the module, and the two mechanisms are not interchangeable.

| | Employer plan — 401(k), 403(b), pension | Individual retirement account |
|---|---|---|
| Mechanism | **Qualified domestic relations order**, § 414(p) | **Transfer incident to divorce**, § 408(d)(6) |
| Why | § 401(a)(13) prohibits assignment; a QDRO is the sole exception | No anti-alienation rule applies |
| Document | A court order meeting § 414(p)(2) and (3), qualified by the plan administrator | The divorce instrument, plus a trustee-to-trustee transfer |
| 10 percent additional tax | **Does not apply** to a payment to an alternate payee, § 72(t)(2)(C) | **Applies** to a withdrawal by the recipient before 59½ |

A QDRO cannot divide an individual retirement account, and a divorce instrument alone cannot divide an employer plan. Using the wrong instrument produces either a rejected order or a fully taxable distribution to the participant.

**The § 72(t)(2)(C) window.** A distribution made to an alternate payee **directly under the QDRO** escapes the 10 percent additional tax at any age. Once the alternate payee rolls the amount into their own individual retirement account, the exception is gone and normal § 72(t) rules apply.

For a non-participant spouse under 59½ who needs cash from the settlement, taking it directly under the QDRO — rather than rolling over first and withdrawing later — saves 10 percent. The decision is made once and cannot be reversed.

#### 5.4 Alimony

Section 11051 of P.L. 115-97 struck § 215, which gave the payer a deduction, and § 71, which included the payment in the recipient's income. The amendments apply to:[97]

1. any divorce or separation instrument **executed after 31 December 2018**, and
2. any instrument executed on or before that date and **modified** after it, **but only if the modification expressly provides** that the amendments apply.

| Instrument | Payer | Recipient |
|---|---|---|
| Executed **after** 2018 | **No deduction** | **Not income** |
| Executed **before** 2019, unmodified | Deduction | Income |
| Executed before 2019, modified with an express opt-in | No deduction | Not income |
| Executed before 2019, modified without an opt-in | Deduction retained | Income retained |

The economics reversed. Under the old rule, income shifted from a higher-rate payer to a lower-rate recipient and the tax saving could be shared. That is gone for new instruments, so the same after-tax outcome for the recipient now costs the payer more.

Child support has never been deductible or includible, and payments are allocated to child support first where an instrument provides for both and payment is short.

#### 5.5 Other attributes that move, or do not

| Attribute | Treatment |
|---|---|
| Suspended S corporation losses | **Transfer** with the stock to the transferee spouse, § 1366(d)(2)(B) |
| Suspended passive losses | Added to the basis of the transferred interest; not usable by the transferor |
| Capital loss carryforward | Remains with the spouse who generated it |
| Net operating loss carryforward | Remains with the spouse who generated it |
| Principal residence exclusion | § 121(d)(3) allows use by a spouse under a divorce instrument, preserving the $250,000 exclusion for a spouse who has moved out |
| Basis | Carries over under § 1041(b) |

#### 5.6 Filing status and other consequences

Status is determined at the close of the year. A spouse who is divorced or legally separated by 31 December files as single, or as head of household where § 2(b) or the § 7703(b) living-apart rule in Module 03 is satisfied.

Divorce is a **life-changing event** for Medicare purposes under 20 CFR § 418.1205(c), so a new initial determination may be requested on Form SSA-44 where income falls.

A divorced spouse married for at least ten years retains a Social Security benefit on the former spouse's record, which costs the worker nothing and is treated in Module 12.

### 6. Examples and Case Calculations

The client figures below are **stated inputs** chosen to show the mechanism. Every rule and rate is from the sources cited.

#### Example 1 — Equal balances, unequal value

A settlement divides two accounts of $600,000 each.

```
SPOUSE A takes the Roth IRA
   Value                                              600,000
   Tax on withdrawal, qualified                             0
   After-tax value                                   $600,000

SPOUSE B takes the traditional 401(k)
   Value                                              600,000
   Tax on withdrawal at 24 percent                    144,000
   After-tax value                                   $456,000
```

A split described as equal transfers $144,000 of value. The correction is to divide **after-tax** values, which in this case means allocating roughly $756,000 of the traditional account against $600,000 of the Roth.

#### Example 2 — The QDRO window

A non-participant spouse aged 48 is awarded $400,000 from a 401(k) and needs $100,000 for a house deposit.

```
TAKEN DIRECTLY UNDER THE QDRO
   Distribution                                       100,000
   Ordinary income tax at 22 percent                   22,000
   § 72(t) additional tax — § 72(t)(2)(C) applies            0
                                                       ------
                                                       22,000

ROLLED TO HER OWN IRA FIRST, THEN WITHDRAWN
   Distribution                                       100,000
   Ordinary income tax at 22 percent                   22,000
   § 72(t) additional tax, 10 percent                  10,000
                                                       ------
                                                       32,000
```

$10,000 turns on the order of two steps. The remaining $300,000 should still be rolled over, so the correct sequence is to take the cash needed directly under the order and roll the balance.

#### Example 3 — Carryover basis on the family home

A spouse takes the marital home, worth $900,000 with a basis of $300,000, in exchange for other assets of equal value.

```
§ 1041   no gain recognised on the transfer                    0
         basis carries over                              300,000

On a later sale at 900,000
   Gain                                                  600,000
   § 121 exclusion, single                              −250,000
   Taxable gain                                          350,000
   Tax at 15 percent plus 3.8 percent                    $65,800
```

The spouse who took the house takes a $65,800 liability with it. Had they taken $900,000 of cash instead, there would be none. Divorce settlements that treat the home as worth its market value overstate what the recipient receives.

#### Example 4 — Alimony under the two regimes

$60,000 a year, payer in the 35 percent bracket, recipient in the 22 percent bracket.

```
INSTRUMENT EXECUTED BEFORE 2019, UNMODIFIED
   Payer deducts 60,000, saving                          21,000
   Recipient includes 60,000, paying                     13,200
   Net cost to the two of them                          $52,200

INSTRUMENT EXECUTED AFTER 2018
   Payer deducts nothing                                      0
   Recipient includes nothing                                 0
   Net cost to the two of them                          $60,000
```

The old rule created $7,800 a year of value out of the rate differential, which the parties could share. That value no longer exists, and a settlement negotiated on pre-2019 assumptions overstates what the payer can afford.

### 7. Interactions with Other Rules

**Filing status (Module 03).** Determined at year end; head of household may be available under § 2(b) or § 7703(b).

**Spousal and survivor benefits (Module 12).** A ten-year marriage preserves a divorced spouse's Social Security benefit, and it costs the worker nothing.

**Step-up in basis (Module 31).** Section 1041 gives carryover basis, not a step-up. The contrast with death is complete.

**Basis in pass-throughs (Module 26).** Suspended S corporation losses follow the stock under § 1366(d)(2)(B) — one of the few suspended attributes that survives a transfer.

**Medicare surcharge (Module 16).** Divorce is a qualifying life-changing event.

**Capital gains (Module 24).** The § 121 exclusion is preserved for a departed spouse by § 121(d)(3).

**Gift tax (Module 29).** Section 2516 keeps qualifying property settlements outside the gift tax.

### 8. Common Scenarios and Edge Cases

**Equal balances are not equal value.** Pre-tax, Roth and taxable accounts each carry a different embedded liability.

**A QDRO does not divide an individual retirement account**, and a divorce instrument does not divide an employer plan.

**The § 72(t)(2)(C) exception is lost on rollover.** Cash needed now should be taken directly under the order.

**Section 1041 gives carryover basis.** The recipient inherits the gain.

**The alimony rule depends on the instrument's execution date**, not on the year of payment. Pre-2019 instruments keep the old treatment unless a modification expressly opts in.

**Status is set at 31 December.** A decree a day either side of the year end changes the whole year.

**Payments are allocated to child support first** where an instrument covers both and payment is short.

**A ten-year marriage preserves a Social Security benefit** on the former spouse's record; a nine-year marriage does not.

**Suspended passive losses do not transfer usefully.** They are added to the basis of the transferred interest rather than remaining with the transferor.

### 9. Planning Implications

Settlements should be negotiated on **after-tax** values. The correction in Example 1 is arithmetic, not judgement, and it is routinely omitted.

Where the non-participant spouse needs cash and is under 59½, the QDRO should specify a direct distribution of that amount, with the balance rolled over. Example 2 shows the cost of reversing the order.

The marital home should be valued net of the embedded gain and net of the § 121 exclusion available to the recipient. A spouse taking the house and a spouse taking cash of the same nominal amount are not treated equally.

For pre-2019 instruments, any modification should be checked before it is made: an express opt-in to the current rules removes the payer's deduction permanently, and there is rarely a reason to include one.

Where the marriage is close to ten years, the Social Security consequence in Module 12 is worth quantifying before the date of the decree is fixed. It costs the other party nothing.

### 10. Data Tables for the Engine

| Constant | Value | Source |
|---|---|---|
| § 1041 non-recognition | No gain or loss | § 1041(a) |
| Basis to the transferee | Transferor's adjusted basis | § 1041(b)(2) |
| Incident to divorce | Within 1 year, or related to the cessation | § 1041(c) |
| Employer plan division | Qualified domestic relations order | § 414(p) |
| IRA division | Transfer incident to divorce | § 408(d)(6) |
| 10 percent additional tax, alternate payee | **Does not apply** | § 72(t)(2)(C) |
| Alimony, instruments after 2018 | Not deductible, not income | P.L. 115-97 § 11051 |
| Alimony, instruments before 2019 | Old treatment, unless expressly modified | § 11051(c) |
| Marital status | Determined at the close of the year | § 7703(a) |
| Suspended S corporation losses | Transfer with the stock | § 1366(d)(2)(B) |
| Divorced spouse Social Security | 10 years of marriage | Module 12 |

### 11. References

[95] 26 U.S.C. § 1041, *Transfers of property between spouses or incident to divorce*. United States Code, Office of the Law Revision Counsel. https://www.govinfo.gov/app/collection/uscode

[96] 26 U.S.C. §§ 414(p), 401(a)(13), 72(t)(2)(C) and 408(d)(6). https://www.govinfo.gov/app/collection/uscode

[97] Tax Cuts and Jobs Act, P.L. 115-97, § 11051. https://www.govinfo.gov/content/pkg/PLAW-115publ97/html/PLAW-115publ97.htm

[37] 20 CFR § 418.1205. https://www.ecfr.gov/current/title-20/chapter-III/part-418/subpart-B/section-418.1205

### 12. Status in This System

| Layer | Status |
|---|---|
| Projection engine | **Not applied.** Divorce is not a modelled life event. Filing status can be entered as single, but no transfer of assets, no division of retirement accounts, no basis consequence and no alimony treatment exists. |
| Backend (`tax-be`) | **Not applied.** No life events. |
| Known limitations | The whole module is unimplemented, and the consequences for a projection are substantial where a divorce occurs. Assets transferred under § 1041 carry the transferor's basis, so a projection continuing after a divorce with market values and no basis history will understate tax on every subsequent disposal. The two mechanisms for dividing retirement accounts, and the § 72(t)(2)(C) exception that makes the timing of a QDRO distribution worth 10 percent, cannot be represented. Alimony has no treatment at all, so a projection cannot distinguish a pre-2019 instrument from a post-2018 one — a difference worth $7,800 a year on the facts of Example 4. Divorce is not available as a Medicare life-changing event, and the divorced-spouse Social Security benefit is absent along with the rest of Module 12's auxiliary benefits. |


---

## Module 37 — Disability and Early Retirement

**Tax year:** 2026 · **As of:** September 2026 · **Primary authority:** Social Security Act § 223; IRC § 72(t)

---

### 1. Overview and Purpose

Disability interrupts a plan more abruptly than any other event. Earned income stops, contributions stop, and money must come out of accounts that were built for a much later date — often decades before the owner reaches 59½, when the 10 percent additional tax on early distributions applies.

Two bodies of rule govern the outcome, and they use different standards for the same word.

**Social Security disability insurance** replaces part of the lost earnings. Entitlement requires an inability to engage in any substantial gainful activity because of a medically determinable impairment expected to result in death or to last at least **12 months**, and it carries a **five consecutive month waiting period** before the first payment.[98] For 2026 substantial gainful activity means monthly earnings above **$1,690**, or **$2,830** for a statutorily blind individual.[99]

**Section 72(t)** determines whether money can be taken from retirement accounts without the 10 percent additional tax. It contains a disability exception using a similar but not identical standard, and a dozen other exceptions — including the rule that a separation from service after age 55 permits penalty-free access to an employer plan.

A projection that models disability only as lost income misses most of it. The tax rules decide how expensive it is to replace that income, and the Social Security rules decide how much of it is replaced.

### 2. Governing Law and Authorities

| Type | Citation | What it establishes |
|---|---|---|
| Statute | Social Security Act § 223(a) | Entitlement to disability insurance benefits |
| Statute | Social Security Act § 223(c)(2) | The five-month waiting period |
| Statute | Social Security Act § 223(d)(1) | Definition of disability |
| Statute | Social Security Act § 222(c) | Trial work period |
| Statute | Social Security Act § 226(b) | Medicare after 24 months of entitlement |
| Statute | IRC § 72(t)(1) | The 10 percent additional tax |
| Statute | IRC § 72(t)(2)(A)(iii) | Disability exception |
| Statute | IRC § 72(t)(2)(A)(iv) | Substantially equal periodic payments |
| Statute | IRC § 72(t)(2)(A)(v) | Separation from service after attaining age 55 |
| Statute | IRC § 72(t)(2)(B) | Medical expenses |
| Statute | IRC § 72(m)(7) | Meaning of disabled for § 72 purposes |
| Determination | Federal Register 2025-19763 | 2026 substantial gainful activity and trial work amounts |

### 3. Key Definitions

| Term | Definition |
|---|---|
| **Disability, Social Security** | Inability to engage in any substantial gainful activity by reason of a medically determinable physical or mental impairment expected to result in death or which has lasted or can be expected to last for a continuous period of **not less than 12 months**.[98] |
| **Disabled, § 72(m)(7)** | Unable to engage in any substantial gainful activity by reason of a medically determinable impairment expected to result in death or to be of **long-continued and indefinite duration**. Proof must be furnished. |
| **Substantial gainful activity** | Monthly earnings above **$1,690** in 2026, or **$2,830** if statutorily blind.[99] |
| **Waiting period** | The earliest period of **five consecutive calendar months** meeting the statutory conditions. |
| **Trial work period** | Nine months, not necessarily consecutive, in which a beneficiary may test working without losing benefits. A month counts where earnings exceed **$1,210** in 2026. |
| **Substantially equal periodic payments** | A series of payments over life or life expectancy that escapes the 10 percent tax under § 72(t)(2)(A)(iv). |

### 4. Who Is Affected

**Social Security disability** requires insured status — recent work as well as the forty quarters needed for retirement — and reaches workers of any age before full retirement age.

**Section 72(t)** reaches anyone taking a distribution before 59½, whether or not disabled.

The two standards differ. Section 72(m)(7) requires an impairment of "long-continued and indefinite duration"; the Social Security Act requires one lasting or expected to last at least 12 months. An approved Social Security disability determination is strong evidence for § 72(t) purposes but the provisions are independent, and a taxpayer may satisfy one without the other.

### 5. Core Rules and Calculations

#### 5.1 Case Register

| # | Case | Applied |
|---|---|---|
| 1 | Disability as a modelled event | **No** |
| 2 | Earned income ceasing on disability | **No** |
| 3 | Social Security disability benefit | **No** |
| 4 | Five-month waiting period | **No** |
| 5 | Substantial gainful activity threshold | **No** |
| 6 | Trial work period and the 36-month extended period | **No** |
| 7 | Conversion to a retirement benefit at full retirement age | **No** |
| 8 | Medicare after 24 months of entitlement | **No** |
| 9 | Taxation of disability benefits under § 86 | **No** |
| 10 | § 72(t) 10 percent additional tax generally | **No** |
| 11 | § 72(t)(2)(A)(iii) disability exception | **No** |
| 12 | § 72(t)(2)(A)(v) separation after age 55 | **No** |
| 13 | § 72(t)(2)(A)(iv) substantially equal periodic payments | **No** |
| 14 | § 72(t)(3) modification recapture | **No** |
| 15 | § 72(t)(2)(B) medical expense exception | **No** |
| 16 | Private disability insurance benefits | **No** |
| 17 | Taxability depending on who paid the premium | **No** |

Nothing in this module is implemented.

#### 5.2 Social Security disability — the sequence

```
Onset of disability
   ↓  five consecutive calendar months, § 223(c)(2) — no benefit payable
First payment, in the sixth month
   ↓  24 months of entitlement, § 226(b)
Medicare begins, whatever the beneficiary's age
   ↓
Full retirement age — the benefit CONVERTS to a retirement benefit
   at the same amount, with no reduction for early claiming
```

Two features are worth stating plainly. **Amyotrophic lateral sclerosis** is exempt from the waiting period, and a beneficiary is entitled from the first month of entitlement. And the benefit at full retirement age **converts** rather than ending — it becomes the retirement benefit at the same amount, computed as though the worker had reached full retirement age, so a person who is disabled at 50 does not suffer the early-claiming reduction that a person retiring at 62 does.

The amount is the primary insurance amount computed under Module 11, but on a shortened earnings record, because the computation drops years for a worker disabled young.

#### 5.3 Returning to work

The rules are deliberately protective and are frequently misunderstood as a cliff.

| Stage | Duration | Effect |
|---|---|---|
| **Trial work period** | 9 months, not necessarily consecutive | Benefits continue **in full** regardless of earnings. A month counts where earnings exceed **$1,210** |
| **Extended period of eligibility** | **36 months** after the trial work period | Benefits are paid in any month earnings fall below substantial gainful activity |
| **Termination** | The third month after the first month of substantial gainful activity following the extended period | Entitlement ends |

A beneficiary may therefore work for nine months at any earnings level without losing anything, and for three further years may move in and out of payment as earnings fluctuate.

#### 5.4 The 10 percent additional tax and its exceptions

Section 72(t)(1) adds 10 percent to the tax on the includible portion of a distribution from a qualified retirement plan before 59½. Paragraph (2) lists the exceptions. Those that matter in a disability or early retirement context:

| Exception | Provision | Available from |
|---|---|---|
| Age 59½ | § 72(t)(2)(A)(i) | Both |
| Death of the employee | (A)(ii) | Both |
| **Disability** under § 72(m)(7) | (A)(iii) | Both |
| **Substantially equal periodic payments** | (A)(iv) | Both |
| **Separation from service after attaining age 55** | (A)(v) | **Employer plans only** |
| Levy under § 6331 | (A)(vii) | Both |
| **Medical expenses** deductible under § 213 | (B) | Both |
| Alternate payee under a QDRO | (C) | Employer plans only |
| Health insurance premiums while unemployed | (D) | **Individual retirement accounts only** |
| Higher education expenses | (E) | **Individual retirement accounts only** |
| First home purchase, $10,000 lifetime | (F) | Individual retirement accounts only |
| Birth or adoption | (H) | Both |

The distinction between the two columns is where most errors occur, and two are worth stating directly.

**The rule of 55 does not apply to individual retirement accounts.** Section 72(t)(2)(A)(v) reaches a distribution "made to an employee after separation from service after attainment of age 55" — that is, from the **employer's plan**. A participant who retires at 56 and immediately rolls the 401(k) into an individual retirement account **destroys the exception**. The correct sequence is to leave the money in the plan, draw what is needed, and roll over the balance later.

**Higher education and first-home exceptions do not apply to employer plans.** They are individual retirement account provisions only.

#### 5.5 Substantially equal periodic payments

Section 72(t)(2)(A)(iv) permits a series of payments over life or joint life expectancy, at any age, without the additional tax. It is the general-purpose route to early access where no other exception fits.

The constraint is § 72(t)(3). If the series is **modified** — other than by reason of death or disability — before the later of five years from the first payment or the taxpayer attaining 59½, the tax that would have applied to every earlier payment is imposed in the year of modification, **plus interest**.

A taxpayer beginning a series at 50 is committed until 59½; one beginning at 57 is committed until 62. The commitment is the reason the route is used less often than its flexibility suggests.

#### 5.6 Taxation of the benefits themselves

**Social Security disability benefits** are taxed under § 86 in exactly the same way as retirement benefits, on the same frozen thresholds. Module 14 applies without modification.

**Private disability insurance** depends on who paid the premium:

| Premium paid | Benefit |
|---|---|
| By the individual with **after-tax** dollars | **Not taxable** |
| By an employer, or by the individual with **pre-tax** dollars | **Fully taxable** as ordinary income |
| Shared | Taxable in proportion to the employer-paid share |

An employer-paid policy replacing 60 percent of income therefore replaces materially less than 60 percent after tax. Paying the premium personally with after-tax dollars converts a taxable benefit into a tax-free one, and the cost of doing so is usually small relative to the difference.

### 6. Examples and Case Calculations

The client figures below are **stated inputs** chosen to show the mechanism. Every rate, threshold and rule is from the sources cited.

#### Example 1 — The waiting period gap

A worker becomes disabled on 15 March.

```
Waiting period      five consecutive calendar months, § 223(c)(2)
                    April, May, June, July, August
First month of entitlement                          September
First payment received                              October

Months with no earned income and no benefit                6
```

Six months of income must come from savings, an employer policy, or a state programme. This gap is the reason short-term disability cover exists, and a projection that starts the benefit at the date of onset overstates liquidity by about half a year of income.

#### Example 2 — The rule of 55, applied and destroyed

A participant separates from service at 56 with $1,400,000 in a 401(k), needing $80,000 a year until 59½.

```
LEFT IN THE 401(k)
   Withdrawal                                          80,000
   § 72(t)(2)(A)(v) applies — separation after 55
   Additional tax                                            0

ROLLED TO AN IRA FIRST
   Withdrawal                                          80,000
   The exception does not reach individual retirement accounts
   Additional tax at 10 percent                          8,000
```

$8,000 a year for three and a half years — $28,000 — turns on whether the rollover happened before or after the withdrawals. The rollover is usually recommended for investment choice and is frequently done immediately.

#### Example 3 — Substantially equal periodic payments and the commitment

A taxpayer aged 52 with $900,000 begins a series producing roughly $38,000 a year.

```
Payments run from age 52 to age 59½ — seven and a half years
Modification before then, other than for death or disability:
   the 10 percent tax on every prior payment is imposed in the
   year of modification, plus interest, § 72(t)(3)

Illustrative: modification at 57, five years of payments of 38,000
   10 percent of 190,000                                19,000
   plus interest for the deferral period
```

The route works, and it cannot be abandoned when circumstances change.

#### Example 4 — Who paid the premium

A disability policy replacing $9,000 a month, taxpayer in the 24 percent bracket.

```
EMPLOYER-PAID PREMIUM
   Benefit                                            108,000 a year
   Taxable in full; tax at 24 percent                  25,920
   After-tax benefit                                  $82,080

INDIVIDUAL-PAID, AFTER-TAX PREMIUM
   Benefit                                            108,000
   Not taxable                                              0
   After-tax benefit                                 $108,000
```

The same policy is worth $25,920 a year more when the premium is paid personally with after-tax dollars. For a policy costing perhaps $3,000 a year, paying it personally rather than through the employer is one of the highest-return decisions available.

#### Example 5 — Working during the trial work period

A beneficiary returns to work earning $4,000 a month.

```
Months 1–9      trial work period — every month counts, earnings exceed 1,210
                benefits continue IN FULL alongside the earnings
Months 10–45    extended period of eligibility, 36 months
                4,000 exceeds SGA of 1,690, so no benefit in those months
                but entitlement continues; benefit resumes in any month
                earnings fall below 1,690
Month 46 on     termination follows the third month of SGA after the
                extended period
```

Nine months of full benefits **plus** full earnings, and three further years of protection. A beneficiary told that returning to work ends benefits immediately has been misinformed.

### 7. Interactions with Other Rules

**Social Security retirement benefits (Module 11).** The disability benefit converts at full retirement age with no early-claiming reduction. The earnings test does not apply to a disability benefit; substantial gainful activity does.

**Taxation of benefits (Module 14).** Disability benefits are taxed under § 86 on the same frozen thresholds.

**Medicare (Module 15).** Entitlement begins 24 months after disability entitlement, before 65.

**Medical expense deduction (Module 32).** A disabled taxpayer with large medical costs may reach the § 72(t)(2)(B) exception as well as the § 213 deduction.

**Required distributions (Module 09).** Disability accelerates access; it does not accelerate the required beginning date.

**Roth accounts (Module 10).** Disability is a qualifying event for a Roth distribution under § 408A(d)(2)(A)(iii), so earnings come out tax free once the five-year period has run.

**Death of a spouse (Module 35).** A disabled surviving spouse may claim a survivor benefit from age 50 rather than 60.

### 8. Common Scenarios and Edge Cases

**Five months with no benefit.** The waiting period is statutory and there is no hardship exception, except for amyotrophic lateral sclerosis.

**The two disability standards differ.** Section 72(m)(7) requires "long-continued and indefinite duration"; the Social Security Act requires 12 months. An approval under one is evidence, not proof, under the other.

**The rule of 55 dies on rollover.** This is the most expensive avoidable error in early retirement planning.

**Education and first-home exceptions are IRA-only**; the rule of 55 and the QDRO exception are plan-only.

**A substantially equal series is a commitment**, not a facility, and modification is expensive.

**Employer-paid disability benefits are fully taxable.** A 60 percent replacement policy replaces about 45 percent after tax.

**The trial work period is nine months, and benefits continue in full during it.**

**The benefit converts at full retirement age** with no reduction, so a worker disabled at 50 reaches full retirement age on the unreduced amount.

**Substantial gainful activity is much higher for the blind** — $2,830 against $1,690 in 2026.

### 9. Planning Implications

Disability should be modelled as a distinct scenario rather than as an unspecified reduction in income, because the five-month gap, the tax treatment of the replacement benefit, and the cost of accessing retirement accounts early all behave differently from ordinary retirement.

For anyone separating from service between 55 and 59½, the sequencing of the rollover is worth more than the investment options that usually drive the decision. Draw what is needed from the plan first.

Disability insurance premiums should be paid personally with after-tax dollars wherever the employer permits it. Example 4 quantifies the difference and it is very large relative to the premium.

A substantially equal series should be a last resort, chosen only where the commitment period is short and the need is durable.

For a client already receiving disability benefits, the trial work period is worth explaining explicitly, because fear of losing entitlement keeps people out of work who could return under the protection the statute provides.

### 10. Data Tables for the Engine

| Constant | 2026 value | Source |
|---|---|---|
| Substantial gainful activity, non-blind | **$1,690 a month** | Federal Register 2025-19763 |
| Substantial gainful activity, blind | **$2,830 a month** | Same |
| Trial work period month | **$1,210 a month** | Same |
| Waiting period | **5 consecutive calendar months** | SSA § 223(c)(2) |
| Duration requirement | 12 months, or expected to result in death | SSA § 223(d)(1) |
| ALS | No waiting period | SSA § 223(a)(1)(ii) |
| Trial work period | 9 months | SSA § 222(c) |
| Extended period of eligibility | 36 months | SSA § 223(a) |
| Medicare | 24 months after entitlement | SSA § 226(b) |
| Conversion to retirement | At full retirement age, unreduced | SSA § 223(a) |
| § 72(t) additional tax | 10 percent | § 72(t)(1) |
| Rule of 55 | Employer plans only | § 72(t)(2)(A)(v) |
| SEPP modification window | Later of 5 years or age 59½ | § 72(t)(3) |

### 11. References

[98] 42 U.S.C. § 423, Social Security Act § 223. United States Code, Office of the Law Revision Counsel. https://www.govinfo.gov/app/collection/uscode

[99] *Cost-of-Living Increase and Other Determinations for 2026*, Federal Register document 2025-19763. https://www.federalregister.gov/documents/2025/11/03/2025-19763/cost-of-living-increase-and-other-determinations-for-2026

[100] 26 U.S.C. § 72, subsections (m)(7), (t)(1), (t)(2) and (t)(3). https://www.govinfo.gov/app/collection/uscode

### 12. Status in This System

| Layer | Status |
|---|---|
| Projection engine | **Not applied.** Disability is not a modelled event. There is no disability benefit, no waiting period, no substantial gainful activity test and no trial work period. The § 72(t) additional tax is not implemented at all, so no early distribution anywhere in the projection attracts it and none of the twelve exceptions is available. |
| Backend (`tax-be`) | **Not applied.** The roadmap projection allocates 2 percent of deployed savings to a "disability and long-term care" bucket and compounds it at the scenario rate. There is no disability event and no benefit computation. |
| Known limitations | The whole module is unimplemented, and three consequences matter for a projection. A client who becomes disabled has no replacement income modelled, so the plan shows a loss of earnings with nothing against it and no five-month gap either. The absence of § 72(t) means every early withdrawal in the projection is untaxed by the additional 10 percent — which understates the cost of early access generally, and makes the rule-of-55 sequencing decision in Example 2 invisible. And private disability insurance is not modelled at all, so the difference between an employer-paid and a personally-paid policy, worth $25,920 a year on the facts of Example 4, cannot be shown. |


---

## Module 38 — Windfalls and One-Time Gains

**Tax year:** 2026 · **As of:** September 2026 · **Primary authority:** IRC §§ 102, 453, 1(h), 1411

---

### 1. Overview and Purpose

A single large receipt — the sale of a business, the exercise of options, an inheritance, a legal settlement — interacts with more provisions at once than any other event in a projection. The rate on the gain itself is usually the smallest part of the answer.

The reason is that the Code contains a large number of thresholds keyed to income, and a windfall crosses most of them simultaneously. In the worked case at § 6, a $3,000,000 gain produces $700,745 of federal tax at an effective rate of 22.85 percent on the gain, and in the same year it eliminates the qualified business income deduction, eliminates the senior deduction, drives the state and local tax limitation to its $10,000 floor, and engages the rewritten § 68 haircut on what itemised deductions remain. Two years later it adds $13,872 of Medicare surcharge.

Several of these effects are avoidable by timing, and one — the Medicare surcharge — cannot be appealed once the income has arisen, because a one-time gain is not among the life-changing events in Module 16.

Not every windfall is taxable. An **inheritance is not income** under § 102, and property received from a decedent takes a stepped-up basis under Module 31. The two most common large receipts a household actually experiences are therefore often the least taxable.

### 2. Governing Law and Authorities

| Type | Citation | What it establishes |
|---|---|---|
| Statute | IRC § 102(a) | Gifts and inheritances excluded from gross income |
| Statute | IRC § 61 | Gross income generally |
| Statute | IRC § 453 | Instalment method |
| Statute | IRC § 453A | Interest charge on large instalment obligations |
| Statute | IRC § 1(h) | Rates on net capital gain |
| Statute | IRC § 1411 | Net investment income tax |
| Statute | IRC § 1202 | Qualified small business stock — Module 24 |
| Statute | IRC § 421, § 422 | Incentive stock options |
| Statute | IRC § 83 | Property transferred for services |
| Statute | IRC § 55 | Alternative minimum tax |
| Statute | IRC § 170(b) | Charitable percentage limitations |
| Regulation | 20 CFR § 418.1205 | Medicare life-changing events — a sale is not one |

### 3. Key Definitions

| Term | Definition |
|---|---|
| **Instalment sale** | A disposition where at least one payment is received after the close of the taxable year of the sale. Gain is recognised as payments are received, under § 453. |
| **Incentive stock option** | An option meeting § 422. No regular tax on exercise, but the spread is an alternative minimum tax preference item. |
| **Non-qualified stock option** | An option outside § 422. The spread is ordinary compensation income on exercise, subject to employment tax. |
| **Bunching year** | A year in which a windfall pushes income far above the normal level, so that deductions taken in that year are worth more. |

### 4. Who Is Affected

Any household receiving a large one-time amount. The size of the interaction depends on where the receipt places income relative to the thresholds, and on whether the taxpayer is over 65, claiming § 199A, itemising, or on Medicare.

A recipient of an **inheritance** is generally unaffected for income tax purposes. A recipient of a **gift** is likewise unaffected; the donor bears any gift tax under Module 29.

### 5. Core Rules and Calculations

#### 5.1 Case Register

| # | Case | Applied |
|---|---|---|
| 1 | One-time gain modelled as an event | Yes |
| 2 | Long-term capital gain rates, stacked above ordinary income | Yes |
| 3 | Net investment income tax on the gain | Yes |
| 4 | Medicare surcharge two years later | Yes |
| 5 | § 199A deduction lost at high taxable income | Yes |
| 6 | Senior deduction phased out | Yes |
| 7 | State and local limitation driven to the floor | **No** — D9 |
| 8 | § 68 haircut on itemised deductions | **No** — D15 |
| 9 | § 102 inheritance excluded from income | **No** — an inheritance is modelled as an asset addition |
| 10 | § 453 instalment method | **No** |
| 11 | § 453A interest charge | **No** |
| 12 | Incentive stock option spread as an AMT preference | Yes |
| 13 | Non-qualified option spread as compensation | **No** |
| 14 | § 1202 exclusion on a qualifying sale | Partially — Module 24 |
| 15 | § 1245 and unrecaptured § 1250 on a business sale | **No** — D17, D18 |
| 16 | Charitable bunching against the windfall | **No** |
| 17 | A one-time gain is not a Medicare life-changing event | Yes, by omission |

#### 5.2 The stacking of effects

A windfall does not simply add a layer of tax. It moves the taxpayer across every income-sensitive threshold at once.

| Provision | Threshold | Effect of crossing |
|---|---|---|
| § 1(h) capital gain rate | $613,700 joint | 15 percent becomes 20 percent |
| § 1411 net investment income tax | $250,000 joint | 3.8 percent on the lesser of net investment income and the excess |
| § 199A | $553,500 joint | Service business deduction gone; wage limit fully phased in for others |
| § 151(d)(5)(C) senior deduction | $350,000 for a qualifying couple | Fully phased out |
| § 164(b)(7) state and local | $606,333 joint | Limitation at the $10,000 floor |
| § 68 | $768,700 joint | Itemised deductions reduced by two thirty-sevenths |
| Medicare surcharge | $750,000 joint | Top tier, **two years later** |

The last row is the one that cannot be undone. A sale is not a life-changing event under 20 CFR § 418.1205, so no new initial determination is available and the surcharge is payable in full.

#### 5.3 The instalment method — § 453

Where at least one payment is received after the close of the year of sale, gain is recognised proportionately as payments are received. The gross profit ratio is applied to each payment:

```
grossProfitRatio = gross profit ÷ contract price
gainRecognised   = payment received × grossProfitRatio
```

Spreading a gain across years keeps more of it below the § 1(h) 20 percent breakpoint and below the net investment income tax threshold, and can keep modified adjusted gross income out of the upper Medicare tiers.

Three constraints. **Depreciation recapture** under § 1245 and § 1250 is recognised **in full in the year of sale**, whatever the payment schedule. An election out is available and is irrevocable. And § 453A imposes an interest charge where the aggregate face amount of instalment obligations outstanding at year end exceeds $5,000,000, which reduces the benefit for very large transactions.

#### 5.4 Options

| | Incentive stock option | Non-qualified stock option |
|---|---|---|
| On grant | Nothing | Nothing |
| **On exercise** | No regular tax; the spread is an **alternative minimum tax preference** | The spread is **ordinary compensation**, subject to employment tax |
| On sale, holding met | Long-term capital gain on the whole appreciation | Capital gain on movement since exercise |
| Holding requirement | 2 years from grant **and** 1 year from exercise | None |
| Disqualifying disposition | Spread becomes ordinary income | — |

The incentive stock option is the trap. Exercising and holding produces no regular tax and a potentially very large alternative minimum tax liability on unrealised gain — a tax bill with no cash, in a year when the shares may subsequently fall. The minimum tax credit recovers it in later years, but slowly.

#### 5.5 What is not taxable

| Receipt | Treatment |
|---|---|
| **Inheritance** | Excluded from gross income, § 102(a). Property takes a stepped-up basis, Module 31 |
| **Gift** | Excluded from the recipient's income, § 102(a). Carryover basis, Module 29 |
| Life insurance death benefit | Excluded, § 101(a) — Module 30 |
| Qualifying § 1202 gain | Excluded, and outside adjusted gross income entirely — Module 24 |
| Damages for physical injury or sickness | Excluded, § 104(a)(2) |
| Punitive damages, interest, lost wages | **Taxable** |

The distinction between a receipt that is excluded and one that is merely taxed at a favourable rate matters, because an exclusion keeps the amount out of adjusted gross income and therefore out of every threshold in § 5.2.

### 6. Examples and Case Calculations

The client figures below are **stated inputs** chosen to show the mechanism. Every rate and threshold is from the sources cited in the modules referenced.

#### Example 1 — A business sale, and everything it touches

Married couple, ordinary income $150,000, long-term gain of $3,000,000, taking the standard deduction.

```
Ordinary taxable income   150,000 − 32,200            117,800
Tax on ordinary income                                 15,340
Long-term capital gains tax, stacked above it         575,205
Net investment income tax  3.8% × 3,000,000           110,200
                                                      -------
Federal tax                                          $700,745
Effective rate on the gain                             22.85%
```

**In the same year**

| Provision | Consequence |
|---|---|
| § 199A | Taxable income of $3,117,800 is far above $553,500 — a service business loses the deduction entirely |
| Senior deduction | Modified adjusted gross income of $3,150,000 is far above $350,000 — fully phased out |
| State and local tax | Above $606,333 — limitation at the $10,000 floor |
| § 68 | Far above $768,700 — remaining itemised deductions cut by two thirty-sevenths |

**Two years later**

```
Modified adjusted gross income of 3,150,000 — top Medicare tier
   Part B surcharge, couple                          11,688.00
   Part D surcharge, couple                           2,184.00
                                                     ---------
   Additional cost in that year                     $13,872.00
```

No appeal is available.

#### Example 2 — The same sale on instalments

The same $3,000,000 gain received as $500,000 a year for six years.

```
Total tax on the gain, spread over six years          542,430
Total tax on the gain, taken at once                  685,405
                                                      -------
Saving                                               $142,975
```

Each year's gain stays below the $613,700 breakpoint, so more of it is taxed at 15 rather than 20 percent, and the net investment income tax applies to a smaller excess. Modified adjusted gross income also stays below the upper Medicare tiers in every year.

The saving is not free. The seller bears credit risk on the buyer, depreciation recapture is still accelerated into year one, and § 453A may impose an interest charge on a balance of this size.

#### Example 3 — Charitable bunching against a windfall

The couple in Example 1 intends to give $50,000 a year to charity for the next ten years.

```
GIVING $50,000 A YEAR
   In ordinary years the standard deduction of 32,200 exceeds
   itemised deductions, so much of the gift produces no benefit

BUNCHING $500,000 INTO THE SALE YEAR, VIA A DONOR ADVISED FUND
   Deduction in the sale year, within the 30 or 60 percent
   limitation of § 170(b), against income of 3,150,000     500,000
   Value at a 37 percent marginal rate                     185,000
   less the § 68 reduction of 2/37 of the deduction        −27,027
   Net benefit                                            $157,973
```

The gift is made once, the charity is funded over ten years from the fund, and the deduction is taken in the year it is worth most. Contributing **appreciated stock** rather than cash removes the gain from the sale as well.

#### Example 4 — An incentive stock option exercise

An exercise producing a $900,000 spread, held past the year end.

```
Regular tax on exercise                                     $0
Alternative minimum taxable income increased by        900,000
AMT exemption for a couple, 140,200, phasing out above 1,000,000

The taxpayer pays alternative minimum tax on a gain that has
not been realised, in cash they do not have.
```

If the shares then fall, the tax remains payable on the exercise-date spread. The minimum tax credit recovers it against future regular tax, but only as regular tax exceeds tentative minimum tax in later years.

### 7. Interactions with Other Rules

**Capital gains (Module 24).** Supplies the rates, the § 1202 exclusion and the netting.

**Net investment income tax (Module 06).** A gain is both net investment income and an increase in modified adjusted gross income, so it can cross the threshold and be taxed by the same movement.

**Medicare surcharge (Module 16).** Two-year lag, cliff structure, no appeal for a one-time gain.

**Qualified business income (Module 17).** A sale year usually destroys the deduction for that year.

**Standard deduction (Module 02).** The senior deduction, the state and local limitation and § 68 all move against the taxpayer in a windfall year.

**Depreciation recapture (Module 22).** On a sale of business or rental property, recapture comes out first and is not eligible for instalment deferral.

**Estate and step-up (Modules 28 and 31).** An inheritance is not income and carries a stepped-up basis.

**Alternative minimum tax.** An incentive stock option exercise is the most common route into it for an otherwise ordinary taxpayer.

### 8. Common Scenarios and Edge Cases

**An inheritance is not income.** Section 102(a) excludes it, and the assets are stepped up.

**A one-time gain cannot be appealed for Medicare.** The list in 20 CFR § 418.1205 is closed and does not include a sale, a conversion, an option exercise or an inheritance.

**Recapture is not deferred by an instalment sale.** It is recognised in full in the year of sale.

**The instalment election is out by default in reverse** — the method applies automatically, and electing **out** is what requires action. The election out is irrevocable.

**Section 453A adds an interest charge** where instalment obligations outstanding exceed $5,000,000.

**An incentive stock option can produce tax without cash.** The spread is an alternative minimum tax item even though nothing has been sold.

**A disqualifying disposition converts the spread to ordinary income** but removes the alternative minimum tax problem.

**Damages are taxable except for physical injury or sickness.** Interest and punitive damages are always taxable.

**Charitable percentage limitations apply.** Cash to a public charity is limited to 60 percent of the contribution base; appreciated property to 30 percent. Excess carries forward five years.

### 9. Planning Implications

The tax on the gain is rarely the largest planning variable. Spreading the receipt across years, where the transaction permits it, changes the rate on the gain, the net investment income tax, and two years of Medicare premiums at once. Example 2 quantifies the first two.

Where spreading is impossible, the sale year should carry every deduction that can be moved into it. A donor advised fund contribution, a defined benefit plan contribution, and the acceleration of deductible expenses are all worth more in that year than in any other — subject to the § 68 haircut, which now reduces their value from 37 to 35 cents in the dollar.

The Medicare consequence should be shown as a line item two years forward at the time the transaction is being considered, not discovered when the premium notice arrives. It is the most common unpleasant surprise following a business sale.

For a founder, the § 1202 analysis in Module 24 should be done before the transaction is structured. An exclusion keeps the amount out of adjusted gross income entirely and therefore out of every threshold listed in § 5.2 — which is worth considerably more than the rate difference alone.

For an incentive stock option holder, exercising in tranches across years, and considering a disqualifying disposition where the alternative minimum tax exposure is large relative to the benefit, are the two standard responses.

### 10. Data Tables for the Engine

| Threshold crossed by a windfall, joint filers | 2026 amount |
|---|---|
| Net investment income tax | $250,000 |
| § 199A phase-out complete | $553,500 |
| Senior deduction fully phased out | $350,000 |
| § 1(h) 20 percent breakpoint | $613,700 |
| State and local limitation at the floor | $606,333 |
| § 68 begins | $768,700 |
| Medicare top surcharge tier | $750,000, **two years later** |
| Instalment method | § 453; recapture accelerated |
| § 453A interest charge | Obligations above $5,000,000 |
| Inheritance | Not income, § 102(a) |
| Charitable limitation, cash | 60 percent of the contribution base |
| Charitable limitation, appreciated property | 30 percent |

### 11. References

[101] 26 U.S.C. §§ 102, 453, 453A and 104. United States Code, Office of the Law Revision Counsel. https://www.govinfo.gov/app/collection/uscode

[102] 26 U.S.C. §§ 421, 422, 83 and 55. https://www.govinfo.gov/app/collection/uscode

[37] 20 CFR § 418.1205. https://www.ecfr.gov/current/title-20/chapter-III/part-418/subpart-B/section-418.1205

[73] Internal Revenue Service, *Revenue Procedure 2025-32*. https://www.irs.gov/pub/irs-drop/rp-25-32.pdf

### 12. Status in This System

| Layer | Status |
|---|---|
| Projection engine | **Applied in part, and the core stacking is right.** A one-time windfall is available as a modelled event. The gain is taxed under the stacked § 1(h) rates, the net investment income tax is applied on the lesser-of basis, the § 199A deduction is lost where taxable income exceeds the ceiling, and the senior deduction phases out. The Medicare surcharge is applied **two years later** from the recorded modified adjusted gross income, which is the detail that makes the event realistic, and no appeal is offered — correctly, since a sale is not a life-changing event. An incentive stock option spread is available as an input to the alternative minimum tax computation. |
| Backend (`tax-be`) | **Not applied.** No life events. |
| Known limitations | Two of the seven threshold effects in § 5.2 are absent, both recorded elsewhere: the state and local limitation is not driven to its floor because the § 164(b)(7) phasedown is unimplemented (D9), and the § 68 haircut on itemised deductions is unimplemented (D15). The instalment method under § 453 is not modelled, so the $142,975 saving in Example 2 cannot be shown and a client cannot compare a lump-sum sale with a spread one. Where the windfall is a sale of business or rental property, the depreciation recapture that would come out first is absent (D17 and D18), so the effective rate on that kind of sale is understated. An inheritance is modelled as an addition to assets rather than through § 102, which produces the right answer but does not distinguish an excluded receipt from a taxable one. Non-qualified option exercises are not modelled as compensation. Charitable bunching against a windfall year cannot be represented, because charitable contributions are not tracked at all (D14). |


---

## Module 39 — Tax Savings Deployment Framework

**As of:** September 2026 · **Status:** **Proprietary methodology — not law**

---

### 1. Overview and Purpose

Every other module in this document describes a rule imposed by statute or regulation. This one does not. The six-bucket deployment framework is **this firm's own methodology** — a set of modelling conventions and allocation assumptions chosen by the practice, not required or endorsed by any authority.

The distinction is stated here plainly because the rest of the document is sourced to primary law, and a reader moving from Module 38 to this one is entitled to know that the basis has changed. Nothing in this module can be cited to the Internal Revenue Code, and nothing in it should be presented to a client as though it could.

What the framework does is answer a question the tax rules do not address. Once a planning strategy has produced a tax saving, that saving is cash. The framework projects what happens if the cash is invested rather than spent, divides it across six categories of use, and compares the resulting balance against a baseline in which the saving was never generated. The output is the roadmap the client sees.

### 2. Basis and Authorities

| Element | Basis |
|---|---|
| The six buckets and their percentages | **Firm methodology.** No statutory basis |
| Scenario growth rates | **Assumptions.** Set per plan |
| Strategy effectiveness factor | **Assumption.** Set per scenario |
| The tax savings figure being deployed | Derived from the strategies in Modules 01 to 38, which **are** sourced |
| Implementation | `tax-be/src/controllers/taxRoadmapController.js`; `models/TaxPlan.js` |

The inputs are grounded in law. The deployment of the output is not, and is a modelling choice.

### 3. Key Definitions

| Term | Definition |
|---|---|
| **Base tax saved** | The aggregate federal and state tax saving attributed to the approved strategies for the plan. |
| **Strategy effectiveness** | A percentage applied to the base saving to reflect expected realisation. 80, 100 or 125 percent in the preset scenarios. |
| **Baseline** | Current savings compounded at the scenario rate, with no strategy and no further contribution. |
| **Plan** | The baseline plus the accumulated value of deployed tax savings. |
| **Extra wealth** | Plan less baseline — the amount attributed to the strategy. |
| **Allocatable plan** | The plan balance less the compounded qualified savings, which is what the six percentages are applied to. |
| **Qualified savings** | Current savings less cash on hand. Compounded separately and added to the retirement bucket. |

### 4. Who It Applies To

Every client for whom a roadmap is produced. The framework is applied uniformly, with the percentages varied per plan where a plan defines its own allocation.

### 5. Core Mechanics

#### 5.1 Case Register

| # | Element | Implemented in `tax-be` |
|---|---|---|
| 1 | Strategy effectiveness multiplier | Yes |
| 2 | Annual tax saving grown by income growth | Yes |
| 3 | Contributions frozen at retirement | Yes |
| 4 | Baseline compounding | Yes |
| 5 | Plan = baseline + invested savings | Yes |
| 6 | Six-bucket allocation of the allocatable plan | Yes |
| 7 | Qualified savings compounded into the retirement bucket | Yes |
| 8 | Milestone snapshots, including fractional ages | Yes |
| 9 | Three preset scenarios | Yes |
| 10 | Per-plan override of the allocations | Yes |
| 11 | Any tax computation | **No** |
| 12 | Inflation applied to the projected balances | **No** — see § 8 |
| 13 | Withdrawals, spending or drawdown | **No** |
| 14 | The allocations summing to 100 percent | **Not enforced** |

#### 5.2 The computation

```
totalTaxSaved  =  baseTotalTaxSaved × (strategyEffectiveness ÷ 100)

for each year from the current age to the end age:

    investedTax = investedTax × (1 + rate)

    if the year is after the first and the client is not retired:
        taxThisYear  = totalTaxSaved × (1 + incomeGrowth)^(year − 1)
        investedTax += taxThisYear

    baseline = currentSavings × (1 + rate)^year
    plan     = baseline + investedTax
    delta    = plan − baseline
```

Contributions stop once the client's age exceeds the retirement age, and the cumulative contribution figure is frozen at that point. The invested balance continues to compound after retirement; nothing further is added.

#### 5.3 The six buckets

The allocation is applied to the **allocatable plan**, which is the plan balance less the separately compounded qualified savings:

```
allocatablePlan = max(0, plan − compoundedQualifiedSavings)
```

| Bucket | Default share | Purpose |
|---|---|---|
| Retirement | **35%** | plus the whole of the compounded qualified savings |
| Insurance | **25%** | |
| Real estate | **25%** | |
| Liquidity | **10%** | |
| Legacy | **3%** | |
| Disability and long-term care | **2%** | |
| | **100%** | |

The retirement bucket is computed as the compounded qualified savings **plus** 35 percent of the allocatable plan. The other five are straight percentages of the allocatable plan.

The defaults are held in `models/TaxPlan.js` and may be overridden per plan and per scenario. Nothing validates that an overridden set sums to 100 percent.

#### 5.4 The three preset scenarios

| | Conservative | Expected | Accelerated |
|---|---|---|---|
| Income growth | 2.0% | 3.0% | 4.0% |
| Retirement return | 5.0% | 7.0% | 9.0% |
| Real estate return | 3.5% | 5.0% | 6.5% |
| Inflation | 0% | 3% | 0% |
| Strategy effectiveness | 80% | 100% | 125% |

Two observations follow from the table and are addressed in § 8. The inflation figure is **0 percent in two of the three scenarios**, and the field is carried but is not applied to the projected balances in any of them. And effectiveness above 100 percent assumes the strategies outperform their own estimate.

### 6. Worked Example

The figures below are **stated inputs**, chosen to show the mechanism.

Client aged 45, retiring at 65, current savings $500,000, cash on hand $50,000, base tax saved $80,000 a year, Expected scenario.

```
Strategy effectiveness 100 percent
   totalTaxSaved                                       80,000

Qualified savings   500,000 − 50,000                  450,000

Year 1   baseline    500,000 × 1.07              =    535,000
         investedTax                                        0
         plan                                          535,000

Year 2   taxThisYear  80,000 × 1.03^0            =     80,000
         investedTax  0 × 1.07 + 80,000          =     80,000
         baseline     500,000 × 1.07²            =    572,450
         plan                                          652,450
         delta                                          80,000

Age 65   contributions freeze; the balance continues to compound
Age 90   the plan balance is split across the six buckets
```

At any milestone the snapshot is:

```
compoundedQualified = 450,000 × 1.07^n
allocatablePlan     = plan − compoundedQualified

retirement    = compoundedQualified + 0.35 × allocatablePlan
insurance     = 0.25 × allocatablePlan
realestate    = 0.25 × allocatablePlan
liquidity     = 0.10 × allocatablePlan
legacy        = 0.03 × allocatablePlan
disabilityLtc = 0.02 × allocatablePlan
```

### 7. Relationship to the Rest of This Document

The framework consumes what the other modules produce and does not itself apply any of them.

| Input | Where it comes from |
|---|---|
| The tax saving being deployed | Modules 01 to 38, via the approved strategies on the plan |
| Growth rates | Scenario assumptions |
| Retirement age | Client data |

The retirement bucket does **not** apply the contribution limits in Module 07, the distribution rules in Module 09, or any tax on withdrawal. The insurance bucket does not apply Module 30. The real estate bucket does not apply Modules 20 to 23. Each bucket is a compounding balance with a label.

That is a legitimate design for a high-level illustration, and it is the reason the projection engine described throughout the rest of this document exists separately.

### 8. Limitations to State When Presenting

Six, and each should be disclosed rather than discovered.

**The buckets are not tax-aware.** A dollar shown in the retirement bucket will be taxed on withdrawal; a dollar in the liquidity bucket has already been taxed; a dollar in the insurance bucket may be accessible tax free. The framework shows them as equivalent. The estate consequences differ too, as Module 31 sets out — a pre-tax retirement dollar reaching an heir is worth materially less than a taxable-account dollar.

**Inflation is carried but not applied.** The scenario field exists and is displayed, and it is **0 percent in the Conservative and Accelerated presets**. No deflation is applied to the projected balances, so every figure is in nominal dollars while being presented as though comparable to today's. Over 45 years at 3 percent, a nominal figure overstates purchasing power by roughly a factor of 3.8.

**Effectiveness above 100 percent is an assumption about outperformance.** The Accelerated scenario applies 125 percent to the base saving, which asserts that the strategies deliver a quarter more than estimated. That is a modelling choice and should be presented as one.

**There is no drawdown.** Balances compound to age 90 with no withdrawals, so the projection shows accumulation and not sufficiency. It cannot answer whether the plan funds the client's spending.

**The allocations are not validated.** An overridden set that does not sum to 100 percent will be applied without warning.

**The percentages are not derived from anything.** They are a house view of a sensible spread, and a different practice would choose differently. They should not be described to a client as optimal, as recommended by any authority, or as the product of analysis they did not undergo.

### 9. Planning Implications

The framework is an illustration of the compounding value of a tax saving, and it is effective at that. Its purpose is to show a client that a saving retained and invested is worth a multiple of the saving itself.

It is not a financial plan and does not answer the questions a plan answers — whether the money lasts, what tax is due on withdrawal, what reaches heirs after tax. Those require the year-by-year engine described in Modules 01 to 38.

The honest framing is that the roadmap shows the **scale** of what a strategy is worth over time, and that a separate projection determines what it is worth **after tax and after spending**. Presenting the bucket figures as a plan invites a question about withdrawals that the framework cannot answer.

Where a client asks what the retirement bucket is worth to them, the answer requires Module 09 for the required distributions, Modules 01 and 14 for the tax on them, and Module 31 for what reaches heirs.

### 10. Data Tables

| Constant | Default | Source |
|---|---|---|
| Retirement bucket | 0.35 | `TaxPlan.js` |
| Insurance bucket | 0.25 | `TaxPlan.js` |
| Real estate bucket | 0.25 | `TaxPlan.js` |
| Liquidity bucket | 0.10 | `TaxPlan.js` |
| Legacy bucket | 0.03 | `TaxPlan.js` |
| Disability and long-term care bucket | 0.02 | `TaxPlan.js` |
| Conservative scenario | 2 / 5 / 3.5 / 0 / 80 | `taxRoadmapController.js` |
| Expected scenario | 3 / 7 / 5 / 3 / 100 | Same |
| Accelerated scenario | 4 / 9 / 6.5 / 0 / 125 | Same |
| End age | 90 | Same |
| Contributions cease | Age > retirement age | Same |

### 11. References

There are no external references for this module. The framework is proprietary and its implementation is:

- `tax-be/src/controllers/taxRoadmapController.js` — `buildTrajectory`, `calculateYearSnapshot`, `buildMilestoneSnapshots`, `resolveRoadmapScenario`
- `tax-be/src/models/TaxPlan.js` — `roadmapScenarioSchema` and `bucketAllocations`

The tax savings figures it consumes are derived from the strategies documented in Modules 01 to 38, which are sourced to primary authority.

### 12. Status in This System

| Layer | Status |
|---|---|
| Backend (`tax-be`) | **This is the backend.** The framework is the whole of what `taxRoadmapController.js` does. It resolves a scenario, applies the effectiveness multiplier, compounds the deployed savings against a baseline, freezes contributions at retirement, and produces milestone snapshots split across the six buckets. |
| Projection engine (`research/index.html`) | **Does not use it.** The front-end engine implements the tax rules in Modules 01 to 38 and does not deploy savings into buckets. The two systems answer different questions and share no computation. |
| Known limitations | Recorded in § 8 and, for the backend defects, in Appendix B. The framework holds **tax year 2025** constants for contribution limits and standard deductions (D6), and its one tax computation, `computeIrsProjectedSavings`, applies **capital gain brackets to ordinary income** (D7). Neither affects the bucket allocation, because the allocation does not compute tax — but both appear in the same file and should be corrected or removed to avoid their being relied on. The inflation field is stored on every scenario and applied to nothing, which is the most likely source of a misunderstanding when the roadmap is presented. |


---

## Module 40 — Glossary

**As of:** September 2026

---

### 1. Overview and Purpose

Every term defined anywhere in this document, collected in one place with the module that defines it. Definitions are reproduced as they appear in the module, which is where the supporting citation will be found.

Where a term is defined differently for different provisions — "modified adjusted gross income" has four distinct definitions in this document — each is listed separately with its own module reference, because using the wrong one produces the wrong answer.

### 2. Abbreviations

| Abbreviation | Expansion |
|---|---|
| AGI | Adjusted gross income |
| AIME | Average indexed monthly earnings |
| AMT | Alternative minimum tax |
| BEA | Basic exclusion amount |
| CFR | Code of Federal Regulations |
| CMS | Centers for Medicare & Medicaid Services |
| DSUE | Deceased spousal unused exclusion |
| FRA | Full retirement age |
| HoH | Head of household |
| HSA | Health savings account |
| IRC | Internal Revenue Code, Title 26 of the United States Code |
| IRD | Income in respect of a decedent |
| IRMAA | Income-related monthly adjustment amount |
| MAGI | Modified adjusted gross income |
| MEC | Modified endowment contract |
| MFJ | Married filing jointly |
| MFS | Married filing separately |
| NIIT | Net investment income tax |
| NOL | Net operating loss |
| OASDI | Old-age, survivors and disability insurance |
| OBBBA | One Big Beautiful Bill Act, P.L. 119-21 |
| PIA | Primary insurance amount |
| POMS | Program Operations Manual System, Social Security Administration |
| QBI | Qualified business income |
| QCD | Qualified charitable distribution |
| QDRO | Qualified domestic relations order |
| QSBS | Qualified small business stock |
| QSS | Qualifying surviving spouse |
| RBD | Required beginning date |
| RIB-LIM | Reduced retirement insurance benefit limitation |
| RMD | Required minimum distribution |
| SECA | Self-Employment Contributions Act |
| SGA | Substantial gainful activity |
| SSTB | Specified service trade or business |
| TCJA | Tax Cuts and Jobs Act, P.L. 115-97 |
| UBIA | Unadjusted basis immediately after acquisition |
| ULT | Uniform Lifetime Table |

### 3. Terms

| Term | Definition | Module |
|---|---|---|
| **80 percent limitation** | The cap on the deduction for post-2017 losses, measured against taxable income computed **without** § 172, § 199A and § 250.[70] | 27 |
| **Account balance** | The balance as of the last valuation date in the preceding calendar year, adjusted for subsequent contributions and outstanding rollovers.[2] | 09 |
| **Accountable plan** | An arrangement under Treas. Reg. § 1.62-2 under which an employer reimburses substantiated business expenses without the reimbursement being wages. | 19 |
| **Active participant** | An individual covered by an employer retirement plan for the year. Determined by plan participation, not by whether the individual contributed. | 08 |
| **Active participation** | A lower standard than material participation, requiring bona fide involvement in management decisions. Available only for the § 469(i) allowance, and only to an owner of at least 10 percent. | 25 |
| **Activities of daily living** | Eating, toileting, transferring, bathing, dressing and continence. A contract must take at least five of the six into account. | 33 |
| **Activity of holding real property** | Includes incidental personal property and services provided in making the property available as living accommodation. Excludes mineral property. | 23 |
| **Additional standard deduction** | The § 63(f) amount for age 65 or over, and separately for blindness. Each condition counts once per qualifying person. | 02 |
| **Adjusted base amount** | $34,000, or $44,000 on a joint return, or zero in the same separate-return case. | 14 |
| **Adjusted taxable gifts** | Lifetime taxable gifts added back to the estate tax base at death, so the unified system is not gamed by timing. | 29 |
| **Aggregate** | Across all of the taxpayer's trades or businesses combined, not business by business. | 18 |
| **Aggregation rule** | Under § 408(d)(2), all traditional, SEP and SIMPLE accounts are treated as a single account when determining the taxable portion of any distribution or conversion. | 08 |
| **Allocatable plan** | The plan balance less the compounded qualified savings, which is what the six percentages are applied to. | 39 |
| **Allowed or allowable** | Basis is reduced by depreciation actually taken **or** by the amount that could have been taken, whichever is greater. Failing to claim depreciation does not preserve basis. | 22 |
| **Alternate payee** | A spouse, former spouse, child or other dependant of a participant recognised by a QDRO. | 36 |
| **Amount at risk** | Cash contributed, the adjusted basis of property contributed, and amounts borrowed for which the taxpayer is personally liable or has pledged property not used in the activity, adjusted for income, losses and distributions. | 23 |
| **Annual additions** | The sum of elective deferrals, employer contributions and forfeitures allocated to a participant's account in a plan for a year. Catch-up contributions are excluded. | 07 |
| **Applicable age** | The age at which distributions must begin. 73 or 75, determined by year of birth. | 09 |
| **Applicable denominator** | The life expectancy factor from the governing table, using the age the owner attains during the distribution year. | 09 |
| **Applicable exclusion amount** | The basic exclusion amount plus any deceased spousal unused exclusion. | 28 |
| **Applicable limitation amount** | The § 164(b)(7) ceiling on the state and local tax deduction. | 02 |
| **Applicable taxpayer** | For § 199A(i), a taxpayer with at least $1,000 of aggregate qualified business income from active qualified trades or businesses in which they materially participate under § 469(h). | 17 |
| **Applicable wages** | Wages under chapter 21, railroad retirement compensation under chapter 22, and net earnings from self-employment, aggregated against a single threshold. | 05 |
| **Auxiliary benefit** | A benefit payable to someone other than the worker on the worker's record — spouse, child, or a spouse caring for a child. | 13 |
| **Average indexed monthly earnings (AIME)** | The highest thirty-five years of covered earnings, each indexed to the national average wage index for the year the worker attains 60, summed and divided by 420. Rounded **down** to the next lower dollar. | 11 |
| **Average period of customer use** | Aggregate days of customer use divided by the number of periods of customer use, computed for the year and for each property or, where grouped, for the activity. | 21 |
| **Base amount** | $25,000, or $32,000 on a joint return, or **zero** for a married taxpayer filing separately who did not live apart from their spouse for the whole year. | 14 |
| **Base tax saved** | The aggregate federal and state tax saving attributed to the approved strategies for the plan. | 39 |
| **Baseline** | Current savings compounded at the scenario rate, with no strategy and no further contribution. | 39 |
| **Basic exclusion amount** | $15,000,000 for 2026, indexed from a 2025 base.[73] | 28 |
| **Basic standard deduction** | The § 63(c)(2) amount determined by filing status. | 02 |
| **Basis** | The cumulative total of non-deductible contributions, tracked on Form 8606, that has already been taxed and is recovered tax free on distribution. | 08 |
| **Bend points** | The two AIME levels at which the formula percentage changes. $1,286 and $7,749 for workers first eligible in 2026. | 11 |
| **Benefit period** | For Part A, a period beginning on admission and ending after 60 consecutive days out of a hospital or skilled nursing facility. A beneficiary can have several in one year, each with its own deductible. | 15 |
| **Bonus depreciation** | Additional first-year depreciation under § 168(k), now 100 percent of the adjusted basis of qualified property. | 22 |
| **Bracket** | A band of taxable income to which a single rate applies. | 01 |
| **Bunching year** | A year in which a windfall pushes income far above the normal level, so that deductions taken in that year are worth more. | 38 |
| **Capital asset** | Property held by the taxpayer, other than inventory, depreciable business property, accounts receivable and certain self-created works. | 24 |
| **Carryforward** | A loss applied against income of a later year. | 27 |
| **Catch-up contribution** | An additional deferral permitted from the year the participant attains age 50. | 07 |
| **Child** | A biological child, adopted child, stepchild, or in some cases a grandchild, who is dependent on the worker.[30] | 13 |
| **Chronically ill individual** | A person unable to perform at least two activities of daily living for at least 90 days, or requiring substantial supervision because of severe cognitive impairment. | 32 |
| **Combined family maximum** | Where a child is entitled on the records of two workers, the maxima on both records may be combined, subject to a ceiling. | 13 |
| **Community property** | Property held under the community property regime of one of nine states. Both halves are adjusted on the first death, not merely the decedent's. | 31 |
| **Compensation** | For § 219 purposes, wages, salaries, professional fees, and net earnings from self-employment. Investment income, pension income and Social Security are not compensation, so they cannot support a contribution. | 08 |
| **Considered not married** | Under § 7703(b), a married individual filing separately who maintains a household that is for more than half the year the principal place of abode of a dependent child, who furnishes over half the cost, and whose spouse is not a member of the household during the last six months of the year.[10] | 03 |
| **Consistent basis** | Under § 1014(f), the basis claimed by the recipient may not exceed the value reported on the estate tax return. | 31 |
| **Contribution and benefit base** | The annual ceiling on wages and self-employment income subject to the old-age component. $184,500 for 2026. | 04 |
| **Contribution base** | For § 170 purposes, adjusted gross income computed without regard to any net operating loss carryback. It is the base against which the 0.5 percent charitable floor and the percentage ceilings are measured. | 02 |
| **Conversion** | A transfer from a traditional account to a Roth account. Taxable to the extent it is not a return of basis. No income limit applies. | 08 |
| **Conversion clock** | A separate five-taxable-year period beginning with the year of each conversion, governing only the ten percent additional tax. | 10 |
| **Cost segregation** | An engineering-based analysis allocating the purchase price of a building among land, structural components, land improvements and tangible personal property. | 22 |
| **Crummey power** | A beneficiary's temporary right to withdraw a contribution to a trust, used to convert a future interest into a present interest. | 29 |
| **Debt basis** | For an S corporation shareholder, the adjusted basis of indebtedness **of the corporation to the shareholder**. Only direct shareholder loans qualify. | 26 |
| **Deemed filing** | Under § 202(r), a claim for one benefit is treated as a claim for all benefits for which the claimant is then eligible. | 12 |
| **Delayed retirement credit** | An increase of two thirds of one percent for each month claiming is deferred past full retirement age, to age 70. | 11 |
| **Designated Roth account** | A Roth subaccount within an employer plan, as distinct from a Roth IRA. | 09 |
| **Designated Roth contribution** | An elective deferral the participant irrevocably designates as includible in income, so that qualified distributions are tax free. | 07 |
| **Disability, Social Security** | Inability to engage in any substantial gainful activity by reason of a medically determinable physical or mental impairment expected to result in death or which has lasted or can be expected to last for a continuous period of **not less than 12 months**.[98] | 37 |
| **Disabled, § 72(m)(7)** | Unable to engage in any substantial gainful activity by reason of a medically determinable impairment expected to result in death or to be of **long-continued and indefinite duration**. Proof must be furnished. | 37 |
| **Distribution calendar year** | A calendar year for which a minimum distribution is required. | 09 |
| **Divorce or separation instrument** | A decree of divorce or separate maintenance, a written separation agreement, or a support decree. Its **execution date** determines the alimony treatment. | 36 |
| **DSUE** | Deceased spousal unused exclusion — the portion of a predeceased spouse's exclusion not used, available to the survivor if elected. | 28 |
| **Dual entitlement** | Entitlement to benefits on more than one record. The person receives the higher, computed as their own benefit plus the excess of the other.[26] | 12 |
| **Dwelling unit** | A house, apartment, condominium, mobile home, boat or similar property providing basic living accommodation. | 20 |
| **Effective rate** | Total tax divided by a stated base. The base must always be identified, because the effective rate on taxable income and the effective rate on gross income are different numbers. | 01 |
| **Elective deferral** | An amount a participant elects to have contributed to a plan rather than paid as salary. Includes pre-tax and designated Roth amounts. | 07 |
| **Eligible designated beneficiary** | A beneficiary who escapes the ten-year rule: a surviving spouse, a minor child of the owner, a disabled or chronically ill individual, or a person not more than ten years younger than the owner. | 09 |
| **Eligible individual** | An individual covered by a high deductible health plan, not covered by other health coverage with limited exceptions, not enrolled in Medicare, and not claimed as another's dependant. | 34 |
| **Eligible long-term care premium** | The portion of a premium for a qualified long-term care insurance contract that counts as medical care, limited by the insured's attained age. | 32 |
| **Excess business loss** | The excess of aggregate deductions attributable to trades or businesses over the sum of aggregate gross income from those trades or businesses and the threshold amount. | 18 |
| **Extra wealth** | Plan less baseline — the amount attributed to the strategy. | 39 |
| **Fair rental** | The amount a person not having an interest in the unit would pay, on the facts and circumstances. | 20 |
| **Family** | Under § 267(c)(4), brothers and sisters, spouse, ancestors and lineal descendants. Notably **not** cousins, nieces, nephews or in-laws. | 20 |
| **Family maximum** | The ceiling under § 203(a) on total benefits payable on one earnings record. | 13 |
| **Former passive activity** | An activity that was passive in a prior year and is not passive in the current year. | 25 |
| **Full retirement age (FRA)** | The age at which the primary insurance amount is payable unreduced. 67 for those born in 1960 or later. | 11 |
| **Future interest** | Any interest limited to commence at a future date. **Does not** qualify for the annual exclusion. | 29 |
| **Gift-splitting** | An election under § 2513 by which a gift by one spouse is treated as made one half by each, doubling the annual exclusion available. | 29 |
| **Gross estate** | Everything the decedent owned or controlled at death, at fair market value, including property passing outside probate. | 28 |
| **Head of household** | Under § 2(b), an individual who is not married at the close of the year, is not a surviving spouse, and either maintains a household that is for more than half the year the principal place of abode of a qualifying child or other dependant, or maintains a household that is the principal place of abode of the taxpayer's father or mother who is the taxpayer's dependant.[9] | 03 |
| **High deductible health plan** | A plan with a deductible at or above the statutory minimum and out-of-pocket exposure at or below the statutory maximum.[89] | 34 |
| **Highly compensated employee** | Under § 414(q)(1)(B), an employee with prior-year compensation above $160,000 for 2026, or a more-than-five-percent owner. Used for non-discrimination testing, not for the Roth catch-up rule. | 07 |
| **Hold harmless** | The § 1839(f) provision limiting the Part B premium increase for most beneficiaries to the dollar amount of the Social Security cost-of-living increase. | 15 |
| **Hospital insurance** | The Medicare component. Uncapped. | 04 |
| **Incentive stock option** | An option meeting § 422. No regular tax on exercise, but the spread is an alternative minimum tax preference item. | 38 |
| **Incident to divorce** | A transfer occurring **within one year** after the marriage ceases, or **related to the cessation** of the marriage.[95] | 36 |
| **Incidents of ownership** | Any right in the policy of an economic nature — to change the beneficiary, surrender or cancel it, assign it, pledge it, or borrow against the cash value. | 30 |
| **Income in respect of a decedent** | Income the decedent had a right to receive but had not recognised. Taxed to the recipient and **not** given a basis step-up. | 28 |
| **Indexing** | Annual adjustment of a threshold under § 1(f), measured by the Chained Consumer Price Index for All Urban Consumers (C-CPI-U). | 01 |
| **Instalment sale** | A disposition where at least one payment is received after the close of the taxable year of the sale. Gain is recognised as payments are received, under § 453. | 38 |
| **Irrevocable life insurance trust** | A trust holding a policy so that the insured holds no incidents of ownership and the proceeds are outside the estate. | 30 |
| **Itemised deductions** | Deductions other than those allowable in computing adjusted gross income and other than the standard deduction. Principally state and local taxes, qualified residence interest, charitable contributions, and medical expenses above the floor. | 02 |
| **Last-month rule** | An individual eligible on 1 December may contribute the full annual amount for that year, subject to remaining eligible throughout the following calendar year. | 34 |
| **Late enrolment penalty** | A permanent premium increase for enrolling after first eligibility without creditable coverage. | 15 |
| **Life-changing event** | One of seven events listed in 20 CFR § 418.1205. | 16 |
| **Lifetime reserve days** | Sixty additional inpatient days available once in a lifetime, at a higher coinsurance rate. | 15 |
| **Long-term** | Held for **more than** one year. A holding of exactly one year is short-term. | 24 |
| **Maintaining a household** | Furnishing **over half** the cost of maintaining the household during the taxable year. The test applies to both § 2(a) and § 2(b). | 03 |
| **Marginal rate** | The rate applied to the next dollar of ordinary income. | 01 |
| **Material participation** | Involvement in the operations on a basis that is regular, continuous and substantial, satisfied by meeting any one of seven regulatory tests. | 21 |
| **Medical care** | Amounts paid for the diagnosis, cure, mitigation, treatment or prevention of disease, or for the purpose of affecting a structure or function of the body, and for transportation essential to that care. | 32 |
| **Modified adjusted gross income** | For the senior deduction and the state and local phasedown, adjusted gross income increased by amounts excluded under §§ 911, 931 or 933. | 02 |
| **Modified endowment contract** | A contract failing the seven-pay test of § 7702A(b), taxed on distributions income-first with a 10 percent additional tax before 59½. | 30 |
| **Mother's or father's benefit** | A benefit under § 202(g) for a surviving spouse caring for the worker's child who is under 16 or disabled. Payable at any age. | 13 |
| **Net capital gain** | The excess of net long-term capital gain over net short-term capital loss. | 24 |
| **Net earnings from self-employment** | Net profit from a trade or business, reduced to 92.35 percent under § 1402(a)(12) before the rates are applied. | 04 |
| **Net investment income** | Interest, dividends, annuities, royalties, rents, net capital gain, and income from a passive trade or business or from trading in financial instruments, less properly allocable deductions. | 06 |
| **Net operating loss** | The excess of deductions over gross income, computed with the modifications in § 172(d). | 27 |
| **New initial determination** | A redetermination of the surcharge using a more recent year's income, available only after a life-changing event. | 16 |
| **Non-business income** | Wages, portfolio income, retirement distributions and similar amounts, against which business losses would otherwise be deductible without limit. | 18 |
| **Non-qualified stock option** | An option outside § 422. The spread is ordinary compensation income on exercise, subject to employment tax. | 38 |
| **Nonexclusion period** | The five-taxable-year period beginning with the first taxable year for which the individual made any contribution to any Roth individual retirement account. One period per person, for life. | 10 |
| **Nonrecourse liability** | A liability for which no partner bears the economic risk of loss. Still included in a partner's basis. | 26 |
| **OASDI** | Old-age, survivors and disability insurance. The capped component. | 04 |
| **Ordinary and necessary** | Ordinary means common and accepted in the taxpayer's field; necessary means helpful and appropriate. Neither requires that the expense be indispensable. | 19 |
| **Outside basis** | The owner's basis in the partnership interest or the stock, as distinct from the entity's basis in its assets. | 26 |
| **Ownership change** | A more than 50 percentage point shift in ownership over a testing period, which limits the use of the loss under § 382. | 27 |
| **Passive activity** | A trade or business in which the taxpayer does not materially participate, or any rental activity. | 25 |
| **Passive activity loss** | The excess of aggregate losses from all passive activities over aggregate income from all passive activities for the year. | 25 |
| **Per diem contract** | A contract paying a fixed daily amount without regard to actual expense. Subject to the § 7702B(d) limit. | 33 |
| **Personal use** | Use for any part of a day by the taxpayer, any co-owner, or a member of the family of either; use under a reciprocal arrangement; or use by anyone paying less than a fair rental. | 20 |
| **Phase-in range** | $150,000 above the threshold on a joint return, $75,000 otherwise. | 17 |
| **Plan** | The baseline plus the accumulated value of deployed tax savings. | 39 |
| **Portability** | The election, made on a timely Form 706, that transfers the DSUE to the surviving spouse. | 28 |
| **Portfolio income** | Interest, dividends, annuities and royalties not derived in the ordinary course of a trade or business. Excluded from passive income by § 469(e). | 25 |
| **Post-termination transition period** | Generally the year following the loss of S corporation status, during which suspended losses may be used against restored stock basis. | 26 |
| **Pre-2018 loss** | A loss arising in a taxable year beginning before 1 January 2018. Carried forward 20 years and **not** subject to the 80 percent limitation. | 27 |
| **Present interest** | An unrestricted right to the immediate use, possession or enjoyment of property or of the income from it. Required for the annual exclusion. | 29 |
| **Primary insurance amount (PIA)** | The benefit payable at full retirement age, produced by applying the three-band formula to AIME. Rounded **down** to the next lower ten cents. | 11 |
| **Protected against loss** | Covered by a guarantee, stop-loss agreement, or similar arrangement, which removes the amount from the at-risk figure under § 465(b)(4). | 23 |
| **Provisional income** | Modified adjusted gross income plus one half of the Social Security benefits received. The statute does not use the phrase; it is the sum described in § 86(b)(1)(A). | 14 |
| **Qualified business income** | The net amount of qualified items of income, gain, deduction and loss from a qualified trade or business. Excludes capital gain, dividends, interest not allocable to the business, and reasonable compensation or guaranteed payments paid to the owner. | 17 |
| **Qualified charitable distribution (QCD)** | A direct transfer from an IRA to a qualifying charity, excluded from gross income, available from age 70½. | 09 |
| **Qualified distribution** | A distribution made after the five-taxable-year nonexclusion period **and** on or after age 59½, on death, on disability within § 72(m)(7), or as a qualified special purpose distribution.[21] Both conditions must hold. | 10 |
| **Qualified domestic relations order** | A domestic relations order creating or recognising an alternate payee's right to receive all or part of a participant's plan benefits, and meeting the specification requirements of § 414(p)(2) and (3).[96] | 36 |
| **Qualified long-term care services** | Necessary diagnostic, preventive, therapeutic, curing, treating, mitigating, rehabilitative and maintenance or personal care services required by a chronically ill individual under a plan of care prescribed by a licensed health care practitioner. | 32 |
| **Qualified medical expense** | An expense that would be deductible under § 213(d), determined without regard to the 7.5 percent floor. Insurance premiums generally do not qualify, with four exceptions. | 34 |
| **Qualified nonrecourse financing** | Financing borrowed for the activity of holding real property, from a qualified person or a government, for which **no person is personally liable**, and which is not convertible debt.[59] | 23 |
| **Qualified person** | A person actively and regularly engaged in the business of lending money, taking the § 49(a)(1)(D)(iv) definition. A related-party lender qualifies where the financing is commercially reasonable and on substantially the same terms as arm's-length loans. | 23 |
| **Qualified property** | Generally property with a recovery period of 20 years or less. Buildings themselves do not qualify; components reclassified to shorter lives do. | 22 |
| **Qualified savings** | Current savings less cash on hand. Compounded separately and added to the retirement bucket. | 39 |
| **Qualified small business stock** | Stock in a C corporation meeting the § 1202 active business and gross assets tests, acquired at original issue. | 24 |
| **Qualified special purpose distribution** | A first-time homebuyer distribution to which § 72(t)(2)(F) applies, capped at $10,000 in a lifetime. | 10 |
| **Qualifying survivor benefit** | The higher of the two Social Security benefits. The smaller ends. | 35 |
| **Quarter of coverage** | The unit in which insured status is earned. $1,890 of covered earnings in 2026, with a maximum of four in any year. | 04 |
| **Real estate professional** | A taxpayer meeting the § 469(c)(7)(B) tests — more than half of personal services in real property trades or businesses **and** more than 750 hours. | 21 |
| **Recourse liability** | A partnership liability for which a partner bears the economic risk of loss. | 26 |
| **Recovery period** | The number of years over which the cost is recovered, set by § 168(c) according to the property's class. | 22 |
| **Reimbursement contract** | A contract paying actual costs incurred. Not subject to the per diem limit. | 33 |
| **Rental activity** | An activity where tangible property is used by customers and gross income is principally for the use of that property.[53] | 21 |
| **Required beginning date (RBD)** | 1 April of the year following the year the owner reaches the applicable age. | 09 |
| **RIB-LIM** | The limitation on a survivor benefit where the deceased had claimed a reduced retirement benefit. | 12 |
| **Roth catch-up wage threshold** | The prior-year wage level above which catch-up contributions must be designated Roth. $150,000 for 2026 purposes.[15] | 07 |
| **Section 327 election** | An irrevocable election by a sole-beneficiary spouse to be treated as the deceased employee for distribution purposes.[93] | 35 |
| **Self-employment income** | Net earnings from self-employment, excluding the excess over the contribution base less wages already paid, and excluding the whole amount if it is less than $400. | 04 |
| **Senior deduction** | The temporary § 151(d)(5)(C) deduction of $6,000 per qualified individual. Distinct from the § 63(f) addition and allowed in addition to it. | 02 |
| **Seven-pay test** | The accumulated amount paid in the first seven contract years may not exceed the sum of the net level premiums that would have been paid had the contract provided paid-up benefits after seven level annual premiums.[77] | 30 |
| **Significant personal services** | Services performed by individuals in connection with making the property available, excluding services usually provided with long-term occupancy. | 21 |
| **Specified service trade or business** | A trade or business in the fields listed in § 199A(d)(2), which adopts the § 1202(e)(3)(A) list **minus engineering and architecture**, together with any business whose principal asset is the reputation or skill of its employees or owners, and investing, investment management, trading and dealing in securities. | 17 |
| **Spousal benefit** | Up to 50 percent of the worker's primary insurance amount, payable while the worker lives. | 12 |
| **Spousal rollover** | The survivor treats an inherited retirement account as their own. | 35 |
| **Step-up** | The adjustment of basis to fair market value at death. The provision is neutral in direction — depreciated property receives a **step-down**. | 31 |
| **Stock basis** | For an S corporation shareholder, basis in the shares. | 26 |
| **Strategy effectiveness** | A percentage applied to the base saving to reflect expected realisation. 80, 100 or 125 percent in the preset scenarios. | 39 |
| **Substantial gainful activity** | Monthly earnings above **$1,690** in 2026, or **$2,830** if statutorily blind.[99] | 37 |
| **Substantially equal periodic payments** | A series of payments over life or life expectancy that escapes the 10 percent tax under § 72(t)(2)(A)(iv). | 37 |
| **Surviving spouse** | A taxpayer entitled under § 2(a) to use the joint-return rate schedule for the two years following the year of a spouse's death. | 01 |
| **Surviving spouse, § 2(a)** | A taxpayer entitled to use the joint rate schedule for the **two years following** the year of death, requiring a dependent son, stepson, daughter or stepdaughter in the household and no remarriage. | 35 |
| **Survivor benefit** | Up to 100 percent of what the deceased worker was receiving or entitled to receive, subject to the RIB-LIM limitation. | 12 |
| **Survivor full retirement age** | The age at which an unreduced survivor benefit is payable. It is **not** the same as retirement full retirement age. | 12 |
| **Taxable income** | Gross income less deductions allowed by chapter 1, including the standard or itemized deduction. It is the figure the rate schedules operate on — not gross income, and not adjusted gross income. | 01 |
| **Testing period** | The 12 months following the last month of the year in which the last-month rule was used. | 34 |
| **Threshold amount** | $250,000 for a joint return, $125,000 for married filing separately, $200,000 in every other case. Fixed by statute. | 05 |
| **Trade or business** | An activity carried on for profit with continuity and regularity, within the meaning of § 162. | 19 |
| **Transfer for value** | A transfer of a policy for valuable consideration, which limits the income tax exclusion to the consideration plus subsequent premiums.[78] | 30 |
| **Trial work period** | Nine months, not necessarily consecutive, in which a beneficiary may test working without losing benefits. A month counts where earnings exceed **$1,210** in 2026. | 37 |
| **Two-year lookback** | The premium for a year is determined from the return filed for the year two years earlier. | 16 |
| **UBIA** | Unadjusted basis immediately after acquisition of qualified property — original cost, undiminished by depreciation, for property still within its depreciable period. | 17 |
| **Unrecaptured section 1250 gain** | Gain on real property attributable to depreciation, taxed at a maximum of 25 percent rather than the ordinary long-term rate. | 22 |
| **Used as a residence** | Personal use during the year exceeding the **greater** of 14 days or 10 percent of the days the unit is rented at a fair rental.[50] | 20 |
| **W-2 wages** | Wages paid by the qualified trade or business and properly allocable to qualified business income. | 17 |
| **Waiting period** | The earliest period of **five consecutive calendar months** meeting the statutory conditions. | 37 |
| **Wash sale** | A sale at a loss where substantially identical stock or securities are acquired within 30 days before or after the sale. | 24 |
| **Withholding threshold** | The $200,000 of wages paid by a single employer at which withholding must begin, without regard to filing status. | 05 |
| **Year of death** | The taxable year in which a spouse dies. Marital status is determined as of the date of death, and a joint return may still be filed. | 03 |
| **§ 179 property** | Tangible depreciable property acquired for use in an active trade or business, which may be expensed in the year placed in service rather than depreciated. | 19 |

### 4. Definitions That Differ by Provision

Four terms carry more than one meaning in this document. Using the wrong definition is a common and consequential error.

**Modified adjusted gross income** — four distinct definitions:

| Purpose | Definition | Module |
|---|---|---|
| Net investment income tax, § 1411(d) | AGI plus the § 911(a)(1) exclusion, less § 911(d)(6) disallowed amounts | 06 |
| Medicare surcharge, 20 CFR § 418.1010 | AGI **plus tax-exempt interest** | 16 |
| Senior deduction and state and local phasedown | AGI increased by amounts excluded under §§ 911, 931 and 933 | 02 |
| Taxation of Social Security, § 86(b)(2) | AGI without regard to § 86 and certain exclusions, **increased by tax-exempt interest** | 14 |

**Disability** — two definitions:

| Purpose | Standard | Module |
|---|---|---|
| Social Security, SSA § 223(d)(1) | Unable to engage in substantial gainful activity; impairment expected to result in death or to last **at least 12 months** | 37 |
| Early distribution exception, § 72(m)(7) | Unable to engage in substantial gainful activity; impairment of **long-continued and indefinite duration** | 37 |

**Full retirement age** — two schedules:

| Purpose | Age for those born 1960 or later | Module |
|---|---|---|
| Retirement benefit | 67 | 11 |
| **Survivor** benefit | 67 for those born 1962 or later; 66 and 8 months for 1960 | 12 |

**Material participation and active participation** — different standards:

| Term | Standard | Module |
|---|---|---|
| Material participation, § 1.469-5T | Any one of seven tests, the lowest being 100 hours | 21, 25 |
| Active participation, § 469(i) | Bona fide involvement in management decisions; 10 percent ownership required | 25 |
| Active participant, § 219(g) | Covered by an employer retirement plan | 08 |

### 5. Frozen Thresholds

Amounts that are **not** indexed and have not changed since the year shown. Their reach expands every year in real terms, which is why this document computes in nominal dollars.

| Threshold | Amount | Fixed since | Module |
|---|---|---|---|
| Social Security taxation, base amount | $25,000 single, $32,000 joint | 1984 | 14 |
| Social Security taxation, adjusted base | $34,000 single, $44,000 joint | 1994 | 14 |
| Net investment income tax | $200,000 / $250,000 / $125,000 | 2013 | 06 |
| Additional Medicare Tax | $200,000 / $250,000 / $125,000 | 2013 | 05 |
| Capital loss deduction | $3,000, $1,500 separate | 1978 | 24 |
| § 469(i) allowance and phase-out | $25,000, from $100,000 | 1986 | 25 |
| Health savings account catch-up | $1,000 | Enactment | 34 |
| Roth IRA and IRA phase-out, separate filers | $0 to $10,000 | Enactment | 08, 10 |
| Senior deduction and its thresholds | $6,000; $75,000 / $150,000 | 2025, expires 2028 | 02 |

---

## Module 41 — Index of Code Sections

**As of:** September 2026

---

### 1. Overview and Purpose

Every provision cited in this document, with the modules that treat it. Compiled from the document itself rather than assembled by hand, so it is complete as at the date above.

Three bodies of law are indexed separately, because their section numbers overlap and conflating them causes real confusion. Internal Revenue Code § 215 was the alimony deduction, repealed in 2017; Social Security Act § 215 is the benefit formula and is very much in force.

### 2. Internal Revenue Code

| Section | Subject | Modules |
|---|---|---|
| § 25B | Retirement savings contributions credit | 08 |
| § 101 | Death benefits | 30, 33, 38 |
| § 102 | Gifts and inheritances | 38 |
| § 104 | Compensation for injuries | 38 |
| § 105 | Employer health plans | 32 |
| § 119 | Meals and lodging | 20 |
| § 121 | Principal residence exclusion | 06, 24, 36 |
| § 151 | Personal exemptions; senior deduction | 02, 03, 38, 39 |
| § 152 | Dependant defined | 03 |
| § 162 | Trade or business expenses | 19, 20 |
| § 163 | Interest | 01, 02, 39 |
| § 164 | Taxes; state and local limitation | 02, 04, 05, 17, 19, 38, 39 |
| § 165 | Losses | 02 |
| § 167 | Depreciation | 22 |
| § 168 | MACRS; bonus depreciation | 22 |
| § 170 | Charitable contributions | 02, 38, 39 |
| § 172 | Net operating losses | 18, 27 |
| § 179 | Election to expense | 19, 22 |
| § 195 | Start-up expenditures | 19 |
| § 199A | Qualified business income | 01, 02, 04, 07, 17, 19, 26, 27, 38, 39 |
| § 213 | Medical expenses | 02, 15, 16, 32, 33, 34, 37 |
| § 219 | IRA contributions | 08 |
| § 250 | Foreign-derived income | 27 |
| § 264 | Insurance interest | 30 |
| § 267 | Related party; family defined | 20, 25 |
| § 274 | Meals and entertainment | 19 |
| § 280A | Business use of home; vacation homes | 19, 20, 21, 22 |
| § 280F | Luxury automobiles | 22 |
| § 382 | NOL limitation after ownership change | 27 |
| § 401 | Qualified plans; required distributions | 06, 07, 09, 35, 36 |
| § 402 | Elective deferrals; rollovers | 07, 09, 13, 39 |
| § 402A | Designated Roth contributions | 07, 10 |
| § 403 | Annuity plans | 06 |
| § 408 | Individual retirement accounts | 06, 07, 08, 09, 10, 36 |
| § 408A | Roth IRAs | 06, 08, 10, 37 |
| § 414 | Definitions; catch-ups; QDRO | 07, 36 |
| § 415 | Contribution and benefit limits | 07, 09, 39 |
| § 416 | Top-heavy plans | 07 |
| § 421 | Statutory stock options | 38 |
| § 422 | Incentive stock options | 38 |
| § 423 | Employee stock purchase plans | 37 |
| § 453 | Instalment method | 38 |
| § 453A | Interest on instalment obligations | 38 |
| § 457 | Deferred compensation plans | 06, 07 |
| § 461 | Excess business loss | 18, 19, 21, 22, 23, 26, 27 |
| § 465 | At-risk limitation | 18, 21, 23, 26 |
| § 469 | Passive activity losses | 04, 06, 17, 18, 19, 20, 21, 22, 23, 24, 25, 26, 31, 35, 39 |
| § 481 | Change of accounting method | 22 |
| § 509 | Supporting organisations | 02 |
| § 529 | Qualified tuition programmes | 29 |
| § 691 | Income in respect of a decedent | 09, 28, 31 |
| § 704 | Partner basis limitation | 18, 23, 26 |
| § 705 | Partner basis determination | 26 |
| § 707 | Partner transactions | 25 |
| § 731 | Partnership distributions | 26 |
| § 752 | Partnership liabilities | 23, 26 |
| § 911 | Foreign earned income | 02, 06 |
| § 931 | Possessions income | 06 |
| § 1014 | Basis of property from a decedent | 22, 25, 28, 29, 31 |
| § 1015 | Basis of gifts | 29, 31 |
| § 1016 | Adjustments to basis | 22 |
| § 1031 | Like-kind exchanges | 22, 25 |
| § 1035 | Insurance exchanges | 33 |
| § 1041 | Transfers between spouses | 26, 29, 36 |
| § 1091 | Wash sales | 24 |
| § 1202 | Qualified small business stock | 01, 17, 24, 38, 39 |
| § 1211 | Capital loss limitation | 24 |
| § 1212 | Capital loss carryovers | 24 |
| § 1221 | Capital asset defined | 24 |
| § 1222 | Capital gains and losses | 24 |
| § 1223 | Holding period | 24, 31 |
| § 1231 | Business property | 22, 24, 31 |
| § 1245 | Recapture, personal property | 22, 24, 31, 38 |
| § 1250 | Recapture, real property | 01, 22, 31, 38 |
| § 1366 | S corporation pass-through | 18, 23, 26, 36 |
| § 1367 | S corporation basis adjustments | 26 |
| § 1368 | S corporation distributions | 26 |
| § 1401 | Self-employment tax | 04, 05, 06 |
| § 1402 | Net earnings from self-employment | 04, 19, 20, 21, 39 |
| § 1411 | Net investment income tax | 06, 16, 25, 38, 39 |
| § 2001 | Estate tax imposed | 28, 31 |
| § 2010 | Unified credit; portability | 28 |
| § 2031 | Gross estate | 28 |
| § 2032 | Alternate valuation | 28, 31 |
| § 2032A | Special use valuation | 28 |
| § 2033 | Property owned at death | 28 |
| § 2035 | Transfers within three years | 28, 29, 30 |
| § 2038 | Revocable transfers | 28 |
| § 2039 | Annuities | 28 |
| § 2040 | Joint interests | 28 |
| § 2041 | Powers of appointment | 28 |
| § 2042 | Life insurance proceeds | 28, 30 |
| § 2053 | Estate deductions | 28 |
| § 2055 | Charitable deduction | 28 |
| § 2056 | Marital deduction | 28 |
| § 2501 | Gift tax imposed | 29 |
| § 2502 | Gift tax rate | 29 |
| § 2503 | Annual exclusion | 29 |
| § 2505 | Unified credit against gift tax | 29 |
| § 2513 | Gift-splitting | 28, 29 |
| § 2516 | Property settlements | 29, 36 |
| § 2522 | Charitable gifts | 29 |
| § 2523 | Marital gifts | 29 |
| § 2631 | Generation-skipping exemption | 28 |
| § 3101 | FICA, employee | 04, 05, 39 |
| § 3102 | Withholding | 05 |
| § 3111 | FICA, employer | 04 |
| § 3201 | Railroad retirement | 05 |
| § 4966 | Donor advised funds | 02 |
| § 4973 | Excess contributions | 08, 34 |
| § 4974 | Excise tax on missed distributions | 09 |
| § 6013 | Joint returns | 03, 35 |
| § 6015 | Innocent spouse relief | 03 |
| § 6331 | Levy | 37 |
| § 7702 | Life insurance defined | 30 |
| § 7702A | Modified endowment contracts | 30 |
| § 7702B | Qualified long-term care | 30, 32, 33 |
| § 7703 | Marital status | 01, 03, 36 |
| § 70305 | — | 19 |

### 3. Social Security Act

| Section | Subject | Modules |
|---|---|---|
| § 202 | Old-age, survivor and auxiliary benefits | 11, 12, 13, 35 |
| § 203 | Family maximum; earnings test | 11, 12, 13 |
| § 215 | Primary insurance amount; COLA | 11, 13, 36, 39 |
| § 222 | Trial work period | 37 |
| § 223 | Disability insurance benefits | 34, 37 |
| § 226 | Medicare entitlement | 37 |
| § 230 | Contribution and benefit base | 04 |
| § 1811 | Medicare Part A | 15 |
| § 1813 | Part A deductibles and coinsurance | 15 |
| § 1818 | Part A premiums | 15 |
| § 1839 | Part B premiums; hold harmless | 15, 16 |
| § 1860D | Part D premiums | 15, 16 |

### 4. Public Laws

| Law | Short name | Provisions used | Modules |
|---|---|---|---|
| **P.L. 119-21** | One Big Beautiful Bill Act | § 70103 senior deduction · § 70105 QBI · § 70106 estate exclusion · § 70120 state and local tax · § 70301 bonus depreciation · § 70424 and § 70425 charitable · § 70431 QSBS · § 70601 excess business loss · §§ 71306–71308 health savings accounts · rewrite of § 68 | 02, 17, 18, 22, 24, 28, 29, 34, 38, 39 |
| **P.L. 117-328** | SECURE 2.0 Act | § 107 applicable age · § 109 higher catch-up · § 325 Roth accounts · § 327 surviving spouse election · § 603 mandatory Roth catch-up | 07, 09, 10, 35 |
| **P.L. 118-273** | Social Security Fairness Act | Repeal of the Windfall Elimination Provision and Government Pension Offset | 11, 12 |
| **P.L. 115-97** | Tax Cuts and Jobs Act | § 11051 alimony repeal · net operating loss limitation · § 199A | 24, 27, 36 |
| **P.L. 116-94** | SECURE Act | Ten-year rule for most beneficiaries | 09 |
| **P.L. 111-152** | Health Care and Education Reconciliation Act | Enacted § 1411 | 06 |

### 5. Regulations

| Regulation | Subject | Modules |
|---|---|---|
| Treas. Reg. § 1.199A-1 to -6 | Qualified business income | 17 |
| Treas. Reg. § 1.401(a)(9)-5 | Determining the required distribution | 09 |
| Treas. Reg. § 1.401(a)(9)-9 | Life expectancy tables | 09 |
| Treas. Reg. § 1.469-1T(e)(3) | Rental activity; the seven-day exception | 21, 25 |
| Treas. Reg. § 1.469-2(f)(6) | Self-rental recharacterisation | 25 |
| Treas. Reg. § 1.469-4 | Grouping of activities | 21, 25 |
| Treas. Reg. § 1.469-5T | Material participation, the seven tests | 21, 25 |
| Treas. Reg. § 1.62-2 | Accountable plans | 19 |
| Treas. Reg. § 1.752-1 to -3 | Partnership liabilities | 26 |
| Treas. Reg. § 20.2042-1(c) | Incidents of ownership | 30 |
| Treas. Reg. § 1.1411-2 | Net investment income tax for individuals | 06 |
| 20 CFR § 404.313 | Delayed retirement credits | 11 |
| 20 CFR § 404.430 | Recomputation at full retirement age | 11 |
| 20 CFR § 418.1010 | Modified adjusted gross income for the Medicare surcharge | 16 |
| 20 CFR § 418.1205 | Major life-changing events | 16, 35, 36, 38 |

### 6. Administrative Guidance

| Item | Subject | Modules |
|---|---|---|
| Rev. Proc. 2025-32 | 2026 inflation adjustments | 01, 02, 03, 17, 18, 19, 28, 29, 32, 33 |
| Rev. Proc. 2025-19 | 2026 health savings account amounts | 34 |
| Rev. Proc. 2024-40 | 2025 amounts, used for comparison | 18 |
| Notice 2025-67 | 2026 retirement plan amounts | 07, 08, 09, 10 |
| Notice 2023-62 | Roth catch-up transition period | 07 |
| Federal Register 2025-19763 | 2026 Social Security determinations | 04, 11, 12, 13, 37 |
| CMS 2026 Parts A and B fact sheet | Medicare premiums and surcharge tables | 15, 16 |
| POMS RS 00203.001 | Child's benefit entitlement | 13 |
| POMS RS 00615.020 | Dual entitlement | 12 |
| POMS RS 00615.301 | Reduced widow's benefits | 12 |
| POMS RS 00615.320 | RIB-LIM | 12 |
| Publication 502 | Medical and dental expenses | 32 |
| Publication 590-A | IRA contributions | 08 |
| Publication 590-B | IRA distributions | 09, 35 |
| Publication 946 | Depreciation | 22 |
| Publication 969 | Health savings accounts | 34 |

---

## Appendix C — Remediation Record

**As of:** September 2026

Appendix B recorded 25 defects found while writing this documentation, on the basis that they were documented and not fixed. That is no longer the position. The projection engine `../index.html` has since been corrected, and this appendix records what changed, what was verified, and what remains outstanding.

### Verification method

A headless harness runs the engine's constants and pure functions outside the browser, and a second harness runs full projections. **97 assertions** were written directly from the worked examples in this document — not from the code — and all 97 pass. Where a test failed, the cause was established by reading the code before anything was changed; three apparent failures turned out to be errors in the tests rather than the engine, and one exposed a defect this documentation had not previously found.

### Fixed

| # | Defect | Verified by |
|---|---|---|
| **D1** | Cost-of-living adjustments now accrue from age 62, not the claiming age | A claim at 70 is now exactly 1.24× a claim at 67 on the same record — the delayed retirement credit and nothing else |
| **D2** | Benefits withheld under the earnings test are restored at full retirement age | Withholding occurs before FRA; the benefit rises permanently at FRA and the user-facing note is now true |
| **D3** | Survivor benefit takes the claiming adjustment, survivor FRA and RIB-LIM | `ribLim(3000,62,67)` = $2,475; `ribLim(3000,70,67)` = $3,720; survivor factor at 60 = 71.5% |
| **D4** | § 203(a) family maximum implemented | `famMax(3000)` = $5,287.50. Two children fit the room and are not capped; four breach it and $35,666 is correctly withheld |
| **D5** | § 202(d)(2) children's benefits implemented, and they stop at 18 | Benefits appear while the child is under 18 and cease exactly when the child ages out |
| **D8–D10** | § 164(b)(7) schedule, 30 percent phasedown and 2030 reversion | $40,400 for 2026; $11,900 at MAGI $600,000; $10,000 floor; reverts to $10,000 in 2030 |
| **D11–D12** | Senior deduction now tests **each** spouse's age, denies married filing separately, and does not index the thresholds | Matches § 151(d)(5)(C) including (v) |
| **D13** | Additional Medicare Tax reaches self-employment income | A sole proprietor with $400,000 of profit and no wages now pays $35,115, including $1,525 under § 1401(b)(2) |
| **D14** | Qualified residence interest and charitable contributions enter itemised deductions | Both now reduce tax where itemising wins |
| **D15** | § 68 implemented | `sec68(60000,900000,'mfj')` = $56,756.76, matching Module 02 |
| **D16** | § 170(p) non-itemiser deduction and the § 170(b)(1)(I) 0.5 percent floor | Both applied |
| **D17** | The 25 percent ceiling on unrecaptured § 1250 gain | Applied as a **ceiling**, not a flat rate — the lower of 25 percent and the taxpayer's own marginal rate |
| **D18** | **A property disposition now computes a gain.** Amount realised, adjusted basis, § 1245 ordinary recapture, unrecaptured § 1250 gain, § 1231 gain, and net proceeds to the taxable account | A sale now produces materially more tax than no sale, and net worth is preserved rather than destroyed |
| **D19** | Tax-exempt interest is added back for the Medicare surcharge | Raises the surcharge tier, and separately raises the taxable share of Social Security under § 86 |
| **D22** | § 199A(i) $400 minimum deduction | An actively participating owner of a fully phased-out service business now receives $400; a passive owner receives nothing |
| **D23** | § 199A separate-return thresholds corrected to $201,775 and $276,775 | Matches Rev. Proc. 2025-32 § 3.26 |
| **D24** | § 469(g) releases suspended passive losses on a fully taxable disposition | Released on sale, alongside D18 |
| **D25** | § 1.469-2(f)(6) self-rental recharacterisation | Self-rental income no longer absorbs unrelated passive losses |

### Found during remediation and fixed

**D26 — a phantom spousal benefit was paid to single filers.** The spousal benefit block tested only that the taxpayer was not widowed and had reached the spouse's claiming age. It never tested that a spouse existed. A single filer with a $3,000 primary insurance amount was therefore credited an extra 50 percent of their own amount — $25,774 a year at age 75 in the tested scenario — for the whole projection.

This defect was **present in the original engine** and was not found while writing Modules 11 to 14, because those modules were verified against the statute and the code's stated intent rather than against its behaviour. It surfaced only when a test asserted that deferring a claim from 67 to 70 should raise the benefit by exactly 24 percent and the engine returned 16 percent. The lesson is the one recorded in Appendix A about keyword searching: reading code establishes what it says, and only running it establishes what it does.

### Not fixed

| # | Defect | Why |
|---|---|---|
| **D6** | Backend holds tax year 2025 constants | `tax-be` is treated as read-only in this work |
| **D7** | Backend applies capital gain brackets to ordinary income | As above |
| **D20** | Medicare premiums are added to expenses rather than deducted from the Social Security benefit | Presentation rather than computation; the tax result is unaffected because § 86 correctly uses the gross benefit |
| **D21** | Medicare surcharge thresholds are inflated by the engine's general factor rather than the published series | Requires a published forward series that does not exist |
| — | The 28 percent ceiling on collectibles and § 1202 gain | The constant is defined, but the wizard collects no collectibles gain, so there is nothing to apply it to |

### Consequential change to the intake

The wizard was reduced from **twelve steps to six** and gained the inputs the corrected engine needs: number and age of dependent children (Modules 11 to 13), tax-exempt interest (Modules 14 and 16), mortgage interest and charitable giving (Module 02), a self-rental flag on each property (Module 25), and a material participation flag on the business (Module 17). No existing field was removed.

---

## Appendix D — Competitor Benchmark

**As of:** September 2026

The engine was compared against the products that do this work commercially. Only their **flow** was examined — how they take intake, how they sequence the calculation, and how they let an adviser steer a conversion. No competitor's numbers were copied, and no competitor was treated as authority on the law; the law in this document comes from the sources in Module 41.

**On source quality.** Vendor help documentation is the vendors' own description of their products and is reliable for what a product does. One source used below is a competitor's published comparison of rival tools; it is marketing-adjacent and is used only for the features it claims about **its own** product and for the questions it raised, not as an assessment of anyone else.

### What the comparison set actually does

| Product | Withdrawal sequencing | Conversion targeting | Notes |
|---|---|---|---|
| **RightCapital** | Default taxable → tax-deferred → tax-free, with alternatives selectable | To an **ordinary bracket**, a **capital-gains bracket**, or a **Medicare surcharge threshold** — not a dollar amount | Also offers an asset-location strategy across the three account types[D1] |
| **Boldin** | Taxable → tax-deferred → Roth → health savings account | Basic | States its tax estimates are "directional"; publishes no detail on the surcharge, the net investment income tax, or § 86 mechanics[D2] |
| **Income Lab** | — | "Fill the 12% bracket" and "fill the 22% bracket" | Positions bracket-filling as the core technique[D3] |
| **MaxiFi** | — | Optimises a sustainable living standard after taxes, surcharges and Social Security interactions | Optimisation rather than adviser-steered targeting[D3] |
| **Covisum** | — | Sizes conversions to **effective marginal rate band** boundaries | Separate products rather than one workflow[D3] |
| **Holistiplan** | — | Bracket visualisation with conversion overlay | Reported not to model the Medicare surcharge inside the conversion analysis[D3] |

### The one material gap, and what was done about it

Every product in the set targets a conversion to a **ceiling**. This system took a **fixed dollar amount** and nothing else.

That was also an internal inconsistency. This documentation teaches ceiling-filling throughout — Module 01 § 9 describes the room between brackets as the capacity for deliberate recognition, Module 09 and Module 10 identify the pre-distribution window, Module 32 Example 3 sizes a conversion against the top of the 22 percent bracket, and Module 38 sizes a windfall against the surcharge tiers. The engine could not do any of it.

Conversion targeting has been implemented in three modes:

| Mode | Ceiling | Verified |
|---|---|---|
| Fixed amount | — | Unchanged behaviour |
| **Fill to a bracket** | Top of the 12, 22, 24, 32 or 35 percent band | Fills to $211,399 against a $211,400 ceiling, and to $403,550 against $403,550 |
| **Fill under a surcharge tier** | One dollar below the chosen Medicare tier | Lands at $217,999 against the $218,000 tier-1 ceiling |

An optional annual cap is available on both ceiling modes, and no mode can convert more than the pre-tax balance holds.

The room is a **fixed point**, not a subtraction: the senior deduction phases out against adjusted gross income, and adjusted gross income includes the conversion. The implementation iterates and then trims, so it lands at or just below the ceiling. Overshooting would place income in the very bracket the client asked to stay out of, which would make the feature worse than useless.

### Where this system is ahead of the set

Two of the reported weaknesses in the comparison set are things this engine already does, and the corrections in Appendix C strengthened both.

The **Medicare surcharge is modelled with its two-year lag and its cliff structure**, and it is available as a conversion target. The published comparison reports that one product does not model the surcharge inside its conversion analysis at all, and that another has only limited awareness of the cliff.

The **§ 86 taxation of benefits, the net investment income tax, and the surcharge are all driven off the same year's income assembly**, so a conversion moves all three together rather than being scored against tax alone.

### Withdrawal sequencing

This engine draws taxable, then pre-tax, then Roth. That is RightCapital's default and Boldin's default, and it is the conventional ordering. It is **not selectable**, where RightCapital offers alternatives. That is a genuine remaining difference and is recorded rather than claimed away — alternative sequencing is worth having, and it is not present.

Health savings accounts sit last in Boldin's order and are absent here entirely, as Module 34 records.

### Defect found during this comparison

**D27 — a deliberate zero was silently replaced by a default.** Nine numeric settings used the pattern `N(field)/100 || default`. In JavaScript a zero is falsy, so a client who entered **0 percent inflation was given 2.5 percent**, one who entered a 0 percent heir tax rate was given 35 percent, and one who entered 0 percent strategy effectiveness was given 100 percent. Blank and zero were indistinguishable.

This was pre-existing and is exactly the class of defect that reading code does not reveal — the expression is idiomatic and looks correct. It surfaced only because a test set inflation to zero and the projection inflated anyway. All nine now default only when the field is genuinely blank.


### Intake flow — how the comparison set orders its questions

RightCapital publishes its default data-entry order. It is **six steps**:

```
Family  →  Income  →  Savings  →  Net Worth  →  Expenses  →  Goals
```

and the order is customisable.[D4] Set against this system's six steps:

| # | RightCapital | This system | Comment |
|---|---|---|---|
| 1 | **Family** — names, birthdays, planning horizon, resident state | **About you** — the same, plus dependent children | Aligned |
| 2 | **Income** — salaries, Social Security, self-employment, pensions | **Income & business** — the same, plus entity type and the § 199A field | Aligned; ours carries the business detail § 199A needs |
| 3 | **Savings** — annual contributions to 401(k), IRA, taxable, Roth, 529 | **Retirement & Social Security** — balances, contributions, and the benefit | Ours merges the benefit here; RightCapital puts it in Income |
| 4 | **Net Worth** — assets and liabilities | **Property & investments** — properties, K-1s, taxable accounts | Ours is deeper: § 280A use, the seven-day test, basis and at-risk per property |
| 5 | **Expenses** — living costs, medical, debt payments, fees, **and filing status** | **Protection, health & life events** — insurance, health costs, estate, events | Ours puts filing status in step 1, which is where it belongs — it drives every threshold |
| 6 | **Goals** — key events and financial goals | **Tax savings & review** | Different purpose: theirs is goal funding, ours is strategy deployment |

Two observations follow.

The **step count and the broad sequence match**, which is a reasonable check that the six-step structure is neither too coarse nor too fine for this kind of intake.

**Filing status is asked far earlier here, and that is deliberate.** RightCapital collects it in the Expenses step. In this system it selects the rate schedule, the standard deduction, and the threshold for the § 86 taxation of benefits, the net investment income tax, the Additional Medicare Tax and the Medicare surcharge — Module 03 sets out the whole dependency. Asking for it last would mean every threshold shown before that point was provisional.

### Links for further research

Verified reachable in September 2026.

**RightCapital — intake order and tax strategies**

| Page | Link |
|---|---|
| Creating plans and data entry — the six-step order | https://help.rightcapital.com/data-entry/creating-plans-and-data-entry |
| Family profile | https://help.rightcapital.com/module-overview/client-portal/profile/family-profile |
| Income | https://help.rightcapital.com/data-entry/income |
| Savings | https://help.rightcapital.com/module-overview/client-portal/profile/savings |
| Expenses | https://help.rightcapital.com/data-entry/expenses |
| Goals | https://help.rightcapital.com/data-entry/goals |
| Profile overview | https://help.rightcapital.com/module-overview/client-portal/profile/profile |
| **Tax strategies — conversion targeting, withdrawal sequencing, asset location** | https://help.rightcapital.com/module-overview/client-portal/tax/tax-strategies |
| Distribution and conversion tool | https://help.rightcapital.com/article/98-distributions/ |
| Tax planning product page | https://www.rightcapital.com/tax-planning/ |

**Boldin — assumptions and tax treatment**

| Page | Link |
|---|---|
| Planner operations: taxes | https://help.boldin.com/en/articles/8482297-planner-operations-taxes |
| Assumptions behind a plan | https://help.boldin.com/en/articles/4789289-understanding-the-assumptions-behind-your-boldin-plan |
| Where to enter retirement income | https://help.boldin.com/en/articles/9221753-where-do-i-enter-retirement-income |

**Others**

| Product | Link | Note |
|---|---|---|
| Income Lab comparison of conversion tools | https://incomelaboratory.com/best-roth-conversion-software/ | A competitor's own comparison — read as marketing, not assessment. Blocks automated access; opens in a browser |
| Boldin "how it works" | https://www.boldin.com/retirement/how-it-works/ | Blocks automated access; opens in a browser |
| eMoney fact-finding workflow | https://emoneyadvisor.com/blog/financial-fact-finding-workflows-to-kickstart-planning-relationships/ | eMoney publishes less operational detail than the other two |
| MaxiFi | https://maxifiplanner.com | Optimisation-based; methodology described on the site |
| Holistiplan | https://www.holistiplan.com | Tax-return-driven analysis |
| Covisum | https://www.covisum.com | Tax Clarity and Social Security Timing are separate products |

[D4] RightCapital, *Creating Plans & Data Entry*, Help Center. https://help.rightcapital.com/data-entry/creating-plans-and-data-entry

### References for this appendix

[D1] RightCapital, *Tax Strategies*, Help Center. https://help.rightcapital.com/module-overview/client-portal/tax/tax-strategies

[D2] Boldin, *Planner Operations: Taxes*, Help Center. https://help.boldin.com/en/articles/8482297-planner-operations-taxes

[D3] Income Lab, *Best Roth Conversion Software for Advisors*. https://incomelaboratory.com/best-roth-conversion-software/ — a competitor's own comparison; used for its claims about its own product and for the questions it raised.

---

## Appendix A — Verification Log

Every figure published in this document has been checked against its primary source and against the two internal registers. This log records what was checked and when.

### September 2026 — rate schedules and capital gains

Source: Revenue Procedure 2025-32, § 3.01 and § 3.03, retrieved as PDF from `irs.gov` and extracted to text rather than read through a summariser.[V1]

All five individual rate schedules and the estate and trust schedule were compared threshold by threshold against the frozen `C.BRACKETS` object in `../index.html`. **Every threshold matches.** This includes the two divergences that a careless table conflates: the 24 percent bracket ends at $201,750 for a head of household and $201,775 for a single filer, and the 32 percent bracket at $256,200 and $256,225 respectively. The separate-return schedule reaches 37 percent at $384,350, and that too matches.

The capital gain breakpoints were compared against `C.LTCG` for all five statuses. **Every breakpoint matches.**

The computation method was validated by applying it to the top of two schedules and comparing against the cumulative amounts the Revenue Procedure itself prints: $206,583.50 at $768,700 for joint filers, and $192,979.25 at $640,600 for single filers. Both reproduce exactly, which confirms the thresholds and the arithmetic together.

### September 2026 — retirement plan amounts

Source: Notice 2025-67, retrieved as PDF from `irs.gov` and extracted to text.[V2]

| Amount | Notice 2025-67 | Engine `C.LIM` | Result |
|---|---|---|---|
| § 402(g) elective deferral | $24,500 | 24500 | Match |
| Age-50 catch-up | $8,000 | 8000 | Match |
| Ages 60–63 catch-up | $11,250 | 11250 | Match |
| IRA contribution | $7,500 | 7500 | Match |
| IRA catch-up | $1,100 | 1100 | Match |
| SIMPLE deferral | $17,000 | 17000 | Match |
| SIMPLE catch-up | $4,000 | 4000 | Match |
| Roth catch-up wage threshold | $150,000 | 150000 | Match |
| Qualified charitable distribution | $111,000 | 111000 | Match |
| Roth IRA phase-out, single | $153,000–$168,000 | [153000, 168000] | Match |
| § 415(c) annual additions | $72,000 | not held | Not implemented |

### September 2026 — statutory text of P.L. 119-21

The public law was downloaded in full from govinfo and searched directly, rather than relying on any summary. Four provisions affecting tax year 2026 were confirmed from the enacted text:

| Provision | Confirmed |
|---|---|
| § 164(b)(7) applicable limitation amount | $40,000 for 2025, **$40,400 for 2026**, 101 percent annually through 2029, $10,000 thereafter |
| § 164(b)(7)(B) phasedown | 30 percent of modified adjusted gross income over $505,000 in 2026, floor of $10,000 |
| § 151(d)(5)(C) senior deduction | $6,000 per qualified individual, reduced by 6 percent of modified adjusted gross income over $75,000, or $150,000 on a joint return; joint return required for a married taxpayer; taxable years beginning before 1 January 2029 |
| § 68 as rewritten | Itemised deductions reduced by two thirty-sevenths of the lesser of the deductions and taxable income increased by them over the 37 percent bracket floor; applied after all other limitations; disregarded for § 199A |
| § 170(p) and § 170(b)(1)(I) | $1,000 and $2,000 for non-itemisers making cash gifts; 0.5 percent floor for itemisers; both from taxable years beginning after 31 December 2025 |

All five apply to tax year 2026 and none were reflected in the engine. They are recorded as D8 through D16.

### September 2026 — United States Code sections read in full

Sections 1, 2, 170, 1402, 1411 and 7703 were retrieved from govinfo and read rather than paraphrased. Four points that a summary would have missed:

- § 1(h) imposes **four** preferential rates, not three. The 0, 15 and 20 percent rates apply to adjusted net capital gain; unrecaptured section 1250 gain is capped at 25 percent and 28-percent rate gain at 28 percent.
- § 2(a) requires specifically a son, stepson, daughter or stepdaughter, not merely any dependant.
- § 2(b)(1)(B) allows head of household status for a dependent parent **without** requiring the parent to live with the taxpayer.
- § 1402(b)(2) excludes self-employment income entirely where net earnings are under $400, and § 1402(b)(1) is the authority for coordinating the contribution base with wages already paid.
- § 1411(c)(6) is the provision that prevents any dollar bearing both the net investment income tax and the Additional Medicare Tax.

### September 2026 — the qualified charitable distribution figure

A domain-restricted search returned $108,000, drawn from Publication 590-B for 2025. Notice 2025-67 states the amount is increased from $108,000 to **$111,000** for 2026, and the engine holds the correct figure. This is the reason search results are never treated as citations in this document.

### September 2026 — Social Security and Medicare figures

Source: Federal Register 2025-19763 and the CMS 2026 premiums fact sheet.[V3][V4]

Confirmed and in agreement with the engine: contribution and benefit base $184,500; primary insurance amount bend points $1,286 and $7,749; cost-of-living adjustment 2.8 percent; retirement earnings test exempt amounts $24,480 and $65,160 annually. Medicare Part B standard premium $202.90, annual deductible $283, income-related adjustment beginning above $109,000 for an individual and $218,000 for a couple.

### September 2026 — Social Security and Medicare primary sources

POMS was reached directly for the survivor and children's rules, and each figure below was taken from the cited section rather than from any summary.

| Point | Source | Result |
|---|---|---|
| Benefits do not add; the higher is paid | POMS RS 00615.020 | Confirmed |
| Maximum survivor reduction of 28.5 percent at 60 | POMS RS 00615.301 | Confirmed, with the 19/56 of 1 percent monthly rate |
| RIB-LIM, the larger of 82.5 percent of death PIA or the deceased's actual entitlement | POMS RS 00615.320 | Confirmed, quoted verbatim |
| Child's benefit of one half of PIA for a living worker, three quarters for a deceased worker | 42 U.S.C. § 402(d)(2) | Confirmed from the statute |
| Child entitlement conditions | POMS RS 00203.001 | Confirmed |
| Family maximum formula and bend points | Federal Register 2025-19763 | Confirmed: 150/272/134/175 at $1,643, $2,371 and $3,093 |
| PIA bend point derivation | Federal Register 2025-19763 | Reproduced exactly from $180 and $1,085 × ($69,846.57 ÷ $9,779.44) |
| Medicare Part A and Part B amounts | CMS 2026 fact sheet | Confirmed |

**A correction to the existing research.** `research/10-SOURCES-AND-COMPETITORS.md` records the Medicare surcharge appeal as having **eight** closed life-changing events. The regulation, 20 CFR § 418.1205, lists **seven**, at paragraphs (a) through (g). The discrepancy arises because Form SSA-44 presents eight options, splitting "work stoppage" from "work reduction", which the regulation combines in paragraph (d). The regulation is the authority. Module 16 states both figures and explains the difference rather than choosing one silently.

### September 2026 — regulations

Treasury Regulation § 1.401(a)(9)-5 and § 1.469-5T were retrieved in full text from `ecfr.gov` and used directly rather than paraphrased. The seven material participation tests and the substitution of the Joint and Last Survivor Table for a sole beneficiary spouse more than ten years younger are quoted from the regulation itself.

### September 2026 — post-completion review

The finished set was reviewed for legal error, internal contradiction and misleading framing. Five items were found and corrected; they are recorded here rather than silently amended.

**One outright error.** Module 12 described the RIB-LIM limitation as "a floor protecting the survivor, not a cap", while the table immediately beneath it was headed "Survivor ceiling". Both statements cannot be right. POMS RS 00615.320 provides that a widow's benefit is **limited to** the larger of 82½ percent of the deceased's primary insurance amount or the deceased's own entitlement — so it is a **ceiling**, computed as the greater of two figures, with the 82.5 percent limb acting as a floor inside that ceiling. Absent the limitation a survivor would receive the full primary insurance amount. The section has been rewritten to say so, and the edge-case note that asserted the opposite has been replaced.

**Three omissions in the qualified charitable distribution rules**, each capable of destroying the exclusion. Section 408(d)(8)(B)(i) bars a qualified charitable distribution to a **donor advised fund** or a § 509(a)(3) supporting organisation — the vehicle a charitably minded client is most likely already to hold. Section 408(d)(8)(A) reduces the excludable amount by deductible individual retirement account contributions made after 70½. Section 408(d)(8)(D) displaces the ordinary § 72 pro-rata rule so that the distribution comes out of the pre-tax portion first, preserving basis. All three are now in Module 09 § 5.8.

**One rule referenced but never stated.** The SECURE Act ten-year rule appeared in the glossary and in an example but was set out nowhere. It is now in Module 09 § 5.9. The limb that could be verified by direct quotation — that no distribution is required in years 1 to 9 where the owner died **before** the required beginning date — is quoted from Publication 590-B. The limb that could **not** be verified by direct quotation, that annual distributions are required where death was on or after the required beginning date, is stated on the authority of § 401(a)(9)(B)(i) and the final regulations and is expressly marked as needing confirmation for a specific account. Asserting it as a quotation would have breached the sourcing standard this document sets for itself.

### September 2026 — completion of the module set

All 41 modules were written and verified between the dates recorded above. Every figure published in this document was taken from a primary source retrieved during that work, and the sources are listed in Module 41 § 6.

Primary documents retrieved and read in full rather than summarised:

| Document | Used for |
|---|---|
| Rev. Proc. 2025-32 | 2026 rate schedules, standard deduction, § 199A, § 461(l), § 179, long-term care premium caps, estate and gift amounts |
| Notice 2025-67 | 2026 retirement plan limits, qualified charitable distribution |
| Rev. Proc. 2025-19 | 2026 health savings account amounts |
| Rev. Proc. 2024-40 | 2025 excess business loss threshold, for the comparison in Module 18 |
| Notice 2023-62 | Roth catch-up administrative transition period |
| P.L. 119-21 | Ten provisions taking effect in 2026, listed in Module 41 § 4 |
| P.L. 117-328 | SECURE 2.0 §§ 107, 109, 325, 327, 603 |
| P.L. 118-273 | Repeal of the Windfall Elimination Provision and Government Pension Offset |
| P.L. 115-97 | § 11051 alimony repeal, with its effective-date conditions |
| Federal Register 2025-19763 | All 2026 Social Security determinations |
| CMS 2026 fact sheet | Medicare Part A and Part B amounts and the full surcharge tables |
| United States Code | 40 individual sections read directly, listed in Module 41 § 2 |
| eCFR | Treasury and Social Security regulations, listed in Module 41 § 5 |
| POMS | Four sections, listed in Module 41 § 6 |

**Three findings that a summary would have produced incorrectly.**

The excess business loss threshold **fell** for 2026, from $313,000 and $626,000 to $256,000 and $512,000. An indexed amount decreasing is unusual enough to look like an error; it is the consequence of P.L. 119-21 § 70601(b) resetting the indexing base, and it was confirmed by reading both the 2025 and the 2026 revenue procedures.

The § 199A threshold for a married taxpayer filing separately is **$201,775**, not the $201,750 that applies to all other returns. The $25 divergence is published and deliberate.

Section 1(h) imposes **four** preferential rates, not three. The 0, 15 and 20 percent rates apply to adjusted net capital gain; unrecaptured section 1250 gain is capped at 25 percent and 28-percent rate gain at 28 percent.

**Structural verification.** Every module carries the twelve required sections and a case register; Modules 40 and 41 are reference sections and use their own structure. Every inline citation marker resolves to an entry in its module's reference list. The finished set was checked for promotional vocabulary and second-person address and contains neither.

### Statutory change confirmed

The Windfall Elimination Provision and the Government Pension Offset were repealed by the Social Security Fairness Act, P.L. 118-273, signed 5 January 2025 and applying to benefits payable for months after December 2023.[V5] Neither provision appears in this system, and that absence is correct. It is recorded here because practitioners continue to assume the Windfall Elimination Provision applies to clients with non-covered pensions.

### References for this appendix

[V1] Internal Revenue Service, *Revenue Procedure 2025-32*, Internal Revenue Bulletin 2025-45, 3 November 2025. https://www.irs.gov/pub/irs-drop/rp-25-32.pdf

[V2] Internal Revenue Service, *Notice 2025-67, 2026 Amounts Relating to Retirement Plans and IRAs*. https://www.irs.gov/pub/irs-drop/n-25-67.pdf

[V3] *Cost-of-Living Increase and Other Determinations for 2026*, 90 Fed. Reg., document 2025-19763. https://www.federalregister.gov/documents/2025/11/03/2025-19763/cost-of-living-increase-and-other-determinations-for-2026

[V4] Centers for Medicare & Medicaid Services, *2026 Medicare Parts A & B Premiums and Deductibles*. https://www.cms.gov/newsroom/fact-sheets/2026-medicare-parts-b-premiums-deductibles

[V5] Social Security Fairness Act of 2023, P.L. 118-273. https://www.govinfo.gov/content/pkg/PLAW-118publ273/html/PLAW-118publ273.htm

---

## Appendix B — Defects on Record

These were established by reading the implementing code, not by searching it.

**Status:** the engine defects listed here have since been **corrected**, and the corrections are verified in Appendix C. The backend defects D6 and D7 remain, because `tax-be` is read-only in this work. This appendix is retained as the record of what was found.

### Projection engine — `../index.html`

**D1 — Cost-of-living adjustments compound from the claiming age rather than from age 62.**
Line 1043 computes the benefit as `Math.pow(1 + C.SS.cola, age - claim)`. Under § 215(i) adjustments accrue from the year the worker attains 62, whatever age they claim at, so a person claiming at 70 already has eight years of adjustment in the first payment. At 2.8 percent the omission understates a late claimer's benefit by approximately 24 percent for life, and it biases every comparison against delayed claiming.

**D2 — Benefits withheld under the earnings test are never restored.**
`earningsTest` returns the withheld amount, line 1059 assigns it, line 1348 stores it on the row, and nothing reads it again. Section 203(f) and 20 CFR § 404.430 require an upward recomputation at full retirement age. The comment at line 773 states that withheld benefits are restored, and the note shown to the user at line 1061 says the amount "is added back later." Neither is true of the current implementation.

**D3 — The survivor benefit is computed from the bare primary insurance amount.**
Line 1054 applies no claiming adjustment, no survivor full retirement age, and no RIB-LIM limitation. This is the calculation behind the widow's penalty, which is the largest single change most projections contain.

**D4 — The family maximum is absent.**
Section 203(a) caps the total payable on one earnings record at roughly 150 to 188 percent of the primary insurance amount. There is no constant and no function. A household drawing a spousal benefit together with children's benefits is overstated.

**D5 — Children's benefits are absent.**
A child of a retired worker is entitled to 75 percent of the primary insurance amount, generally until 18, or 19 while still in secondary school, or without limit if disabled before 22. Not modelled.

### Projection engine — deductions and payroll, added September 2026

**D8 — The state and local tax limitation is the wrong amount and the wrong mechanism.**
Line 1201 computes `saltCap = 40000 * iAdj`. Section 164(b)(7) as added by P.L. 119-21 sets the applicable limitation amount at $40,000 for 2025 and **$40,400 for 2026**, growing at exactly 101 percent a year through 2029. The engine starts from the 2025 figure and applies a general inflation factor instead, so the amount is wrong in every year and the mechanism does not match the statute.

**D9 — The state and local phasedown is absent.**
Section 164(b)(7)(B) reduces the limitation by 30 percent of modified adjusted gross income above $505,000 in 2026, subject to a floor of $10,000. None of this is implemented. A taxpayer with $600,000 of modified adjusted gross income is shown a $40,400 deduction where the statute allows $11,900.

**D10 — The limitation never reverts to $10,000.**
Section 164(b)(7)(A)(iv) restores the $10,000 ceiling for taxable years beginning after 2029. The engine continues to inflate its figure indefinitely, so every projected year from 2030 to age 90 overstates the deduction.

**D11 — The senior deduction is doubled without testing the spouse's age.**
Line 1194 computes `C.SENIOR.amt * (married ? 2 : 1)` while line 1192 tests only `age >= 65`. Section 151(d)(5)(C)(ii) allows $6,000 for each qualified individual, and the spouse is a qualified individual only if the spouse has also attained 65. A couple aged 66 and 60 receives $12,000 in the projection and $6,000 under the statute.

**D12 — The senior deduction is allowed to married taxpayers filing separately, and its thresholds are indexed.**
`C.SENIOR.start` carries a $75,000 threshold for married filing separately, but § 151(d)(5)(C)(v) denies the deduction outright unless a married taxpayer files jointly. Separately, line 1193 multiplies the threshold by `iAdj`; the statute contains no indexing provision for either the $6,000 amount or the $75,000 and $150,000 thresholds, because the deduction expires after 2028.

**D13 — The Additional Medicare Tax never reaches self-employment income.**
Line 1138 applies the 0.9 percent tax inside a `w2 > 0` branch and only to `w2`. Section 1401(b)(2) imposes the same tax on net earnings from self-employment, against a threshold shared with wages. A sole proprietor with $250,000 of Schedule C profit and no wages is shown no liability; the correct amount is $277.88. The error grows with profit and is larger for married taxpayers filing separately, whose threshold is $125,000.

**D14 — Itemised deductions omit mortgage interest and charitable contributions.**
Line 1203 computes `itemized = medDed + saltPaid`. Qualified residence interest under § 163(h) and charitable contributions under § 170 are absent entirely. A taxpayer whose itemised total rests on a mortgage or on regular giving is understated, and the engine may show them taking the standard deduction in years when they would in fact itemise.

**D15 — The rewritten § 68 is not implemented.**
P.L. 119-21 replaced § 68 in full, effective for taxable years beginning after 31 December 2025 — that is, from tax year 2026. Itemised deductions are reduced by two thirty-sevenths of the lesser of the deductions themselves and the excess of taxable income, increased by those deductions, over the 37 percent bracket floor. The effect is to cap the value of an itemised deduction at 35 cents in the dollar for top-bracket taxpayers. Nothing in the engine applies it, so those taxpayers are shown deductions worth 37 cents.

**D16 — Neither new charitable rule is implemented.**
Section 170(b)(1)(I) imposes a floor of 0.5 percent of the contribution base on charitable deductions for itemisers, and § 170(p) restores a deduction of $1,000, or $2,000 on a joint return, for non-itemisers making cash gifts. Both apply from tax year 2026. Neither appears in the engine, which does not track charitable contributions at all.

**D17 — Only three of the four § 1(h) rate components are implemented.**
`ltcgTax` applies the stacked 0, 15 and 20 percent table and nothing else. Section 1(h)(1)(E) caps unrecaptured section 1250 gain at 25 percent and § 1(h)(1)(F) caps 28-percent rate gain — collectibles gain and § 1202 gain — at 28 percent. Neither is applied. The 0/15/20 rates are also applied to the whole of net capital gain rather than to adjusted net capital gain, which the statute defines as net capital gain reduced by those two components.

**D18 — Selling a property produces no gain, no tax, and no proceeds.**
At line 1074, once the projected age passes a property's `sellAge`, the engine sets `p._sold = true` and returns. Nothing else happens. No amount realised is computed, no adjusted basis is used, no gain is recognised, and no capital gains tax is charged. The constant `C.RE.recapture` of 0.25 is defined at line 389 and **never referenced anywhere in the file**, and the running total `p._accum`, built up at line 1086 from every year's depreciation, is never read. Line 1320 then excludes sold properties from the equity total, so the property's value simply disappears from net worth rather than converting to cash.

The effect runs in two directions at once. Tax is understated, because a sale that should produce unrecaptured section 1250 gain at up to 25 percent and long-term gain above that produces nothing. Net worth is also understated, because the after-tax proceeds never arrive in any account. Suspended passive losses are not released either, which § 469(g) requires on a fully taxable disposition. Any projection in which a client sells a property is wrong from that year forward.

### Projection engine — Social Security and Medicare, added September 2026

**D19 — Tax-exempt interest is not added back for the Medicare surcharge.**
20 CFR § 418.1010 defines modified adjusted gross income for the income-related monthly adjustment amount as adjusted gross income **plus tax-exempt interest**. The engine uses adjusted gross income alone. A beneficiary holding municipal bonds is placed in a lower tier than the regulation produces, and because the structure is a cliff the error is the whole of a tier rather than a proportion of it — up to $3,472.80 a year for a couple. The § 86 computation in the same engine **does** add tax-exempt interest back correctly, so the two treatments are inconsistent with each other.

**D20 — Medicare premiums are added to expenses but never deducted from the Social Security benefit.**
Premiums are withheld from the benefit before payment. The engine adds them to the expense side while continuing to credit the household with the gross benefit, so the cash-flow presentation shows income the household never receives alongside a payment it has already made. The tax computation is unaffected, because § 86 correctly operates on the gross benefit, but net cash is overstated and then offset rather than stated correctly.

**D21 — Medicare surcharge thresholds are inflated by the engine's general factor.**
The tier boundaries are published annually by CMS and do not follow the engine's general inflation assumption. Projected tier boundaries drift from the published series in every year after the first.

**D22 — The § 199A minimum deduction is never applied.**
P.L. 119-21 § 70105 added § 199A(i), giving a taxpayer with at least $1,000 of qualified business income from actively conducted businesses a deduction of the greater of the computed amount or **$400**, for taxable years beginning after 31 December 2025. The engine holds the constant `min: 400` in its § 199A configuration and **never references it** in `qbiDeduction`. This is the fourth dead constant found — alongside `C.RE.recapture`, `maxMonthlyFRA`, and the `SURV_FRA` and `survivorAt60` pair.

**D23 — The married-filing-separately § 199A threshold is $25 low.**
Revenue Procedure 2025-32 § 3.26 sets the separate-return threshold at **$201,775** and the top of the phase-in range at **$276,775**, against $201,750 and $276,750 for all other returns. The engine uses the "all other returns" figures for married filing separately. The amount is trivial but the divergence is real and published, and the same engine handles the equivalent $25 divergence in the § 1 rate schedules correctly.

**D24 — Suspended passive losses are never released.**
Section 469(g) frees a suspended loss when the taxpayer disposes of an entire interest in a passive activity in a fully taxable transaction to an unrelated party, and treats it as not from a passive activity — an ordinary deduction against any income. The engine has no release mechanism at all. Combined with D18, the disposition of a rental property produces no gain, no depreciation recapture, no tax, no sale proceeds, **and** no release of the losses accumulated against it. A client selling a long-held rental with a large suspended balance should see a substantial deduction in that year and sees nothing.

**D25 — Self-rental income is not recharacterised.**
Treas. Reg. § 1.469-2(f)(6) treats net rental income from property let to a trade or business in which the taxpayer materially participates as non-passive, while leaving a net loss passive. The engine treats such income as ordinary passive income, so it wrongly absorbs suspended losses from unrelated passive activities. This affects the common case of a professional who owns the building their practice occupies.

### Backend — `tax-be`

**D6 — Constants are for tax year 2025.**
`taxRoadmapController.js` lines 109 to 128 hold a $23,500 elective deferral limit and standard deductions of $15,000 and $30,000. The 2026 figures are $24,500, $16,100 and $32,200.

**D7 — Capital gain rates are applied to ordinary income.**
`computeIrsProjectedSavings` at line 142 runs ordinary taxable income through `IRS_LONG_TERM_CAPITAL_GAINS_BRACKETS`.

### Verified correct — recorded so they are not re-flagged

Confirmed by reading the implementing code in September 2026: the basic standard deduction and the § 63(f) addition for all filing statuses including the $2,050 unmarried amount; all five rate schedules and the capital gain breakpoints; the § 1402(a)(12) factor of 92.35 percent; wage base coordination between wages and self-employment income; the § 164(f) deduction taken at one half and computed before adjusted gross income; the exemption of S corporation distributive shares from self-employment tax; the net investment income tax lesser-of computation; and the decision to hold the § 1411 and § 3101(b)(2) thresholds constant rather than inflating them, which is correct because neither is indexed.

### Scope of the backend

`taxRoadmapController.js` is not a tax engine. It takes approved tax savings, applies a strategy effectiveness factor, divides the result across six buckets — retirement 35 percent, insurance 25 percent, real estate 25 percent, liquidity 10 percent, legacy 3 percent, disability and long-term care 2 percent — compounds each at scenario rates, and produces a trajectory with milestone snapshots. It holds no rules for required distributions, Social Security, Medicare surcharges, the net investment income tax, the alternative minimum tax, qualified business income, or the loss limitation gates. Where a section of this document records that a rule is applied by the projection engine and not present in the backend, that is why.
