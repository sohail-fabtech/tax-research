# Roadmap to Age 90™ — Intake UI: What I Built and What I Sourced It From

**Prepared for:** senior review
**Author:** _[your name]_
**Date:** September 2026
**Files:** `research/index.html` (the UI) · `research/docs/ROADMAP-TO-AGE-90-DOCUMENTATION.md` (the reference documentation behind it)

---

## 1. Summary

I rebuilt the client intake and projection interface at `research/index.html`. It is a single offline HTML file — 123,351 bytes, 2,146 lines, no dependencies, no build step, no network calls — containing a six-step intake wizard, a federal tax and retirement projection engine, and a year-by-year output to age 90.

Alongside it I wrote the reference documentation the UI is built against: 137,023 words across 41 modules and four appendices, in `ROADMAP-TO-AGE-90-DOCUMENTATION.md`. Every rule the engine applies is documented there with its statutory authority, its worked arithmetic, and a case register recording which cases the system handles and which it does not.

The documentation was written first and the UI was corrected against it. That order matters, and it is the substance of section 4 below: writing the rules out in full exposed twenty-seven defects in the previous engine, twenty-three of which are now fixed and verified.

---

## 2. The intake flow

The previous version asked for information across twelve steps. It now asks across six:

| Step | Collects | Inputs |
|---|---|---|
| 0 | About you | 14 |
| 1 | Income & business | 12 |
| 2 | Retirement & Social Security | 10 + 4 per account |
| 3 | Property & investments | 13 + 43 per property / K-1 |
| 4 | Protection, health & life events | 34 + 12 per policy |
| 5 | Tax savings & review | 17 + 6 per strategy |

165 inputs in total. The reduction from twelve steps to six removed no data — it removed screens. Fields that were spread across separate pages for topics that are computed together are now on the same page, because the client answers them together and the engine consumes them together.

Two structural decisions are worth flagging:

**Filing status is asked in step 0.** It selects the rate schedule, the standard deduction, and the thresholds for § 86, the net investment income tax, the Additional Medicare Tax and the Medicare surcharge. Nothing downstream can be computed without it.

**Real estate is gated in the documented order.** § 280A personal use is tested first, then § 469 classification (the seven-day rule), then the four loss gates in statutory sequence: § 704(d)/§ 1366(d) basis, § 465 at-risk, § 469 passive, § 461(l) excess business loss. Order is not cosmetic here. A loss that survives the basis gate but fails at-risk is treated differently from one that fails basis outright, and running the gates out of order produces a different number.

---

## 3. Sources

This is the part I want on the record. Every figure and every legal statement in the documentation, and therefore every constant in the engine, comes from a primary US federal source that I fetched and read. No figure was taken from a search result summary, a financial media site, or an AI-generated page.

### 3.1 Primary documents

| Source | Used for |
|---|---|
| **Rev. Proc. 2025-32** | Tax year 2026 inflation-adjusted figures — brackets, standard deduction, AMT exemption and phase-out, estate exclusion, § 199A thresholds, gift exclusion |
| **Notice 2025-67** | 2026 retirement plan limits — § 402(g) deferrals, catch-up, IRA, QCD limit |
| **Rev. Proc. 2025-19** | Health savings account limits |
| **Notice 2023-62** | SECURE 2.0 § 603 Roth catch-up administrative transition |
| **P.L. 119-21** (OBBBA) | The 2026 changes: SALT schedule and phasedown, senior deduction, § 68 rewrite, § 170(p), § 199A(i), permanence of the 2017 rate schedule |
| **P.L. 115-97** | The 2017 rate structure and § 199A as enacted |
| **P.L. 117-328** (SECURE 2.0) | §§ 107, 109, 325, 327, 603 |
| **P.L. 118-273** | Social Security Fairness Act — repeal of WEP and GPO |
| **P.L. 116-94** (SECURE 1.0), **P.L. 111-152**, **P.L. 103-66** | Ten-year rule; NIIT; the 85% tier of Social Security taxation |
| **IRS Publications 502, 527, 590-A, 590-B, 915, 946, 969** | Operational detail and the IRS's own worked examples |
| **Federal Register 2025-19763** and the **CMS 2026 Medicare Parts A & B fact sheet** | Part B premium, deductible, and the IRMAA tier table |
| **SSA POMS RS 00203.001, RS 00615.020, RS 00615.301, RS 00615.320** | Children's benefits, family maximum, and RIB-LIM at SSA's own operating-manual level |
| **US Code (via govinfo.gov) and eCFR Titles 20 and 26** | 131 IRC sections and the implementing regulations, indexed in Module 41 |

### 3.2 Domains used

| Fetched and cited | Count |
|---|---|
| `govinfo.gov` — US Code, Public Laws, Federal Register archive | 75 |
| `irs.gov` — Revenue Procedures, Notices, Publications, Internal Revenue Bulletin | 37 |
| `ecfr.gov` — Titles 20 and 26 | 16 |
| `federalregister.gov` | 6 |
| `secure.ssa.gov/poms.nsf` — SSA Program Operations Manual System | 6 |
| `cms.gov` | 5 |

I tested each domain rather than assuming it would work. `www.ssa.gov` returns 403 to automated access and `uscode.house.gov` refuses connections; I substituted the Federal Register and POMS for the first and govinfo for the second, which is why those hosts carry the volume they do.

### 3.3 What I excluded, and why

No figure comes from Investopedia, NerdWallet, SmartAsset, Kiplinger, Forbes, Motley Fool, Google Finance, Yahoo Finance, or any AI-generated summary page. These sites are frequently a year behind and are not correctable — they publish no erratum when a figure changes.

One concrete example of why this matters. A domain-restricted search for the 2026 qualified charitable distribution limit returned **$108,000**. That is the 2025 figure, and it appeared in a snippet from an IRS publication page. The correct 2026 figure is **$111,000**, stated in Notice 2025-67. Had I taken the snippet, the engine would have understated a QCD strategy by $3,000 per year per client for the life of the projection. This is the reason a search result is only ever used to locate a document, never to source a number: the document is then fetched and read.

The same discipline caught a case citation. `AmeriSouth XVI` — which appears in secondary commentary on cost segregation — is wrong; the case is `AmeriSouth XXXII`, T.C. Memo. 2012-67. A second case I found cited in commentary could not be confirmed in any primary source, so I dropped it rather than carry it.

### 3.4 Three-way constant check

Every constant in the engine was checked against the primary source and against the working research notes, and any disagreement was resolved at the source. Twenty-two constants were verified this way, including the standard deduction ($32,200 / $16,100 / $24,150), the MFJ bracket schedule to $768,700, the AMT exemption ($90,100 / $140,200 phasing at $500,000 / $1,000,000), the estate exclusion ($15,000,000), the Social Security wage base ($184,500), the PIA bend points ($1,286 / $7,749), the earnings test ($24,480 / $65,160), and the Part B premium and deductible ($202.90 / $283). The full log is Appendix A of the documentation.

One result from that check is counterintuitive enough that I want it stated explicitly: the § 461(l) excess business loss threshold **fell** for 2026, from $313,000/$626,000 to $256,000/$512,000. Thresholds normally rise with inflation, so this reads like a transcription error. It is not — I read both Revenue Procedures to confirm it.

---

## 4. What the documentation exposed in the engine

Writing each rule out in full, with a case register enumerating every case, surfaced twenty-seven defects. Twenty-three are fixed and verified; four are recorded and not fixed, for the reasons given.

**The most expensive one was invisible to inspection.** The spousal benefit block never checked that a spouse existed. A single filer with no spouse in the projection was receiving a spousal Social Security benefit worth $25,774 per year. It was not found by reading the code — it was found because a regression test asserted that a claim at 70 should be exactly 1.24× a claim at 67, and the ratio came back 1.16. The extra benefit was distorting the ratio. Reading alone would not have found it; running it did.

Other corrections of consequence:

- **Social Security COLA now accrues from age 62, not from the claiming age** (§ 215(i)). The previous behaviour understated a client claiming at 70 by roughly 24% for life, which biased the entire system against delayed claiming.
- **A property sale now computes a gain.** Previously a disposition set a flag and returned. It now computes amount realised, adjusted basis, § 1245 ordinary recapture, unrecaptured § 1250 gain, § 1231 gain, and net proceeds — and releases suspended passive losses under § 469(g).
- **The § 203(a) family maximum and § 202(d) children's benefits are implemented.** Without the family maximum, a household drawing spouse and children's benefits on one earnings record was overstated.
- **The survivor benefit takes the claiming adjustment, the survivor full retirement age (which differs from the retirement FRA), and RIB-LIM.** This is the widow's-penalty calculation and it was previously using bare PIA.
- **§ 68 as rewritten by OBBBA, the SALT schedule with its 30% phasedown, § 170(p), § 170(b)(1)(I) and § 199A(i)** — all effective for 2026 and all previously absent.
- **The 25% rate on unrecaptured § 1250 gain is applied as a ceiling, not as a flat rate** — the lower of 25% and the taxpayer's own marginal rate, which is what § 1(h) actually says.

One correction I want to note because it is a class of bug rather than a single instance: nine numeric fields used the pattern `N(x) || default`, which silently discards a deliberate zero. A client entering 0% inflation got 2.5%; a client entering a 0% heir tax rate got 35%. All nine now use a parser that distinguishes empty from zero.

**Not fixed, deliberately:** two backend defects in `tax-be` (2025 constants, and capital gain brackets applied to ordinary income) — that service is read-only in this work; Medicare premiums presented as an expense rather than netted from the benefit — presentation only, the tax result is correct because § 86 uses the gross benefit; and IRMAA thresholds inflated by the general factor, which needs a published forward series that does not exist.

---

## 5. Verification

The engine runs headless under a test harness that loads the computation layer out of `index.html` and executes it in an isolated context. **105 assertions, all passing.**

The tests were written from the documentation, not from the code. That is the point of them — a test written from the code asserts that the code does what it does. Each assertion checks the engine against a worked example that was computed from the statute, so a test failure means the engine disagrees with the law rather than with a previous version of itself.

The three test-design errors I hit were themselves informative, and I proved each rather than adjusting the expectation to match the output: an MFS SALT expectation where the phasedown legitimately applied; a client sitting in the 0% capital gains band, so additional taxable Social Security produced no additional tax; and two children who legitimately fitted inside the family maximum room.

Current state: 6 wizard steps, 105 assertions passing, JavaScript syntax clean, a full projection producing 49 rows with no non-finite values.

---

## 6. Competitor comparison

I benchmarked the intake flow — flow only, not pricing or features — against RightCapital, Boldin, Holistiplan, Covisum, MaxiFi, Income Lab and eMoney. Thirteen URLs verified; eleven return 200, and two (Income Lab, and Boldin's "how it works" page) block automated access but open normally in a browser. The full list is Appendix D of the documentation.

RightCapital publishes its default intake order, and it is six steps: Family → Income → Savings → Net Worth → Expenses → Goals. Our six-step structure lines up closely with it, which I take as independent confirmation that six is the right number for this kind of intake.

One deliberate divergence: RightCapital collects filing status in step 5 of 6. We ask it in step 0, for the reason given in section 2 — nothing downstream is computable without it.

We also added Roth conversion targeting for parity with RightCapital and Boldin, which offer it. It supports three modes — fill to a bracket, fill to an IRMAA tier, or a fixed dollar amount — and it iterates to a fixed point, because the senior deduction phases out against AGI and the conversion is itself part of AGI. A single-pass calculation overshot the target bracket by $10,643.

---

## 7. Known gaps

Stated plainly rather than left to be discovered:

- Health savings accounts are documented (Module 34) but no input collects them.
- The 28% collectibles ceiling exists as a constant; no input collects a collectibles gain.
- Withdrawal sequencing is fixed and not user-selectable. RightCapital offers alternative orderings.
- The two backend defects in section 4 remain, as that service was out of scope.

---

## 8. Where to look

| | |
|---|---|
| The UI and engine | `research/index.html` |
| The reference documentation | `research/docs/ROADMAP-TO-AGE-90-DOCUMENTATION.md` |
| Constant verification log | Appendix A |
| Defect register, D1–D27 | Appendix B |
| What was fixed and how it was verified | Appendix C |
| Competitor flow comparison and links | Appendix D |
| Glossary — 187 terms | Module 40 |
| Index of IRC sections — 131 sections | Module 41 |

Modules 40 and 41 are generated from the document itself rather than maintained by hand, so they cannot drift out of step with it.
