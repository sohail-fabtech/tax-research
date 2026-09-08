# Client Cases — Roman Urdu + English

---

## MONEY COMING IN

### Client abhi working hai. Income kaise grow karti hai?

```
w2 = (client W-2 + spouse W-2 + bonus) x (1 + income growth)^years
business profit x (1 + income growth)^years
other income    x (1 + income growth)^years
```

Output: sab kuch ek hi rate se grow karta hai. Expected 3%, Conservative 2%, Accelerated 4%.

Rule: ye assumption hai, law nahi.

Missing: jis client ka bonus har saal upar neeche hota hai, ya business lumpy hai, wo model nahi hota. Sab pe ek hi rate lagta hai.

**Also touches:** Tax · Putting money in · Growth

---

### Retirement wale saal mein kya hota hai?

Output: W-2 aur business income retirement age pe **completely** stop ho jati hai. Koi wind-down nahi, koi part year nahi.

Agar part-time work select kiya tha to wo income start hoti hai aur jo age set ki thi wahan tak chalti hai.

Rule: ye humara apna calculation hai. Law nahi.

**Also touches:** Social Security (part-time earning se earnings test lag sakta hai) · Taking money out (yahin se conversion window open hoti hai)

---

### Mere spouse ka inteqal ho gaya. Unki salary ka kya hoga?

Output: unki W-2 us saal se zero ho jati hai. Lekin Social Security khatam nahi hoti — survivor ko dono benefits mein se bara wala milta rehta hai. Wo bilkul alag calculation hai.

Rule: salary ke liye humara calculation. Benefit ke liye asli rule.

**Also touches:** Social Security · Estate and family

---

### Kaunsi income kis cheez pe asar karti hai?

Teen alag tests hain aur teenon alag income count karte hain. Log inko hamesha confuse karte hain.

| Test | Kya count hota hai |
|---|---|
| Social Security **earnings test** | sirf earned income — salary aur self-employment |
| Social Security pe **tax** | AGI + tax-free interest + aadha benefit |
| **Medicare surcharge** | AGI + tax-free interest, magar **do saal purana** |

Matlab IRA se withdrawal karne se aapka early Social Security cheque kam nahi hota. Lekin us cheque pe tax zyada lagta hai, aur do saal baad Medicare bill barh jata hai.

Rule: Social Security Act §203(f); IRC §86; Social Security Act §1839(i).

**Also touches:** Social Security · Medicare · Forced withdrawals

---

### Business structure se jawab badal jata hai.

Output: wohi profit agar S corporation, partnership ya sole trade se guzre to employment tax alag hoga, retirement contribution room alag hogi, aur sab se important, agar business mein kabhi loss hua to **basis** ka result bilkul alag hoga.

Business type explicitly poocha jata hai, guess nahi kiya jata. Aur 20% wale deduction ke liye service business ko product business se alag treat kiya jata hai.

Rule: IRC §1402; §199A(d)(2).

**Also touches:** K-1 and business losses · Putting money in · Tax

---

## TAX

### Tax actually calculate kaise hota hai?

Output: bracket by bracket, slice by slice. **Kabhi bhi** poori income ko top rate se multiply mat karo — ye sab se common mistake hai.

2026, married filing jointly:

| Yahan tak | Rate |
|---|---|
| $24,800 | 10% |
| $100,800 | 12% |
| $211,400 | 22% |
| $403,550 | 24% |
| $512,450 | 32% |
| $768,700 | 35% |
| us se upar | 37% |

Single brackets har step pe roughly **aadhe** hote hain. Ye baat yaad rakhein — isi wajah se spouse ke inteqal ke baad tax itna barh jata hai.

Rule: IRC §1; Rev. Proc. 2025-32.

**Also touches:** Estate and family · Taking money out

---

### Brackets lagne se pehle kya minus hota hai?

```
Standard deduction   $32,200 joint  /  $16,100 single  /  $24,150 head of household
Age 65 addition      $1,650 per person joint  /  $2,050 single
Senior deduction     $6,000 per person, 65+
```

Output: married couple jinki dono ki age 65+ hai, unko roughly $47,500 pehle hi free milta hai.

**Careful — ye $6,000 senior deduction 2028 ke baad expire ho raha hai.** 2029 mein wohi couple $12,000 zyada pe tax dega, income mein koi change nahi hoga. Age 90 tak ki projection bana rahe hain to isko switch off karna zaroori hai.

Rule: IRC §63(c),(f), §151(d)(5)(C); P.L. 119-21.

**Also touches:** Events · Age by age

---

### Capital gain ordinary income ke **upar** lagta hai, saath mein nahi.

```
Married, 2026
  0%   $98,900 tak
  15%  $613,700 tak
  20%  us se upar
```

Output: pehle ordinary income space bharti hai, phir gain uske upar stack hota hai. To jis saal ordinary income kam ho, us saal bara gain **0%** pe realise kiya ja sakta hai. Wohi gain high income wale saal mein 20% plus 3.8% ka parta hai.

Do ceilings jo simple table mein nahi dikhte:
- Property depreciation recapture pe **25%** ka ceiling — 25% ya client ka apna rate, jo kam ho.
- Collectibles pe 28%.

Rule: IRC §1(h).

**Also touches:** Property · Taking money out

---

### Ordinary tax ke upar aur kya lagta hai?

| | Rate | Start (joint) | Inflation se barhta hai? |
|---|---|---|---|
| Net investment income tax | 3.8% | $250,000 | **Nahi — 2013 se frozen** |
| Additional Medicare tax | 0.9% | $250,000 | **Nahi** |
| Social Security tax salary pe | 6.2% | $184,500 tak | haan |
| Medicare tax salary pe | 1.45% | koi limit nahi | — |

Output: upar wali do lines **kabhi inflation se adjust nahi hotin**. Har saal zyada households inki range mein aa jate hain — ye ek chhupa hua tax increase hai jis pe kabhi vote nahi hua.

Rule: IRC §1411, §3101(b)(2), §3121.

**Also touches:** Growth · Medicare

---

### 20% wala business deduction mujhe milega?

```
2026 threshold   $403,500 joint  /  $201,750 baaki
Fully phased     $553,500 joint  /  $276,750 baaki
```

Output: threshold se neeche clean 20% milta hai. Us se upar do cheezein ek saath hoti hain — wage aur property limit lagti hai, aur **service businesses ka poora khatam ho jata hai**.

Service ka matlab: health, law, accounting, consulting, financial services, performing arts, athletics. **Engineering aur architecture service business NAHI hain** — ye har baar logon ko surprise karta hai.

Rule: IRC §199A(b),(d)(2); §199A(i) minimum.

**Also touches:** K-1 and business losses · Money coming in

---

### State tax.

Output: nau states kuch nahi lete. California, New York, Oregon aur Hawaii federal ke upar roughly 13% tak lete hain.

Jo client top bracket ke qareeb hai, uske liye **state change karna** baaki saari tax strategies se zyada faida deta hai — aur estate tax position bhi badal deta hai.

Rule: state statute.

**Also touches:** Estate and family · Events

---

### AMT 2026 mein aur sakht ho gaya.

```
Exemption          $140,200 joint
Phase out start    $1,000,000
Phase out rate     50%   — pehle 25% tha, DOUBLE ho gaya
```

Output: exemption ab do guna tezi se khatam hoti hai. Jis client ke deductions bare hain ya stock options hain aur pehle clear tha, ab shayad na ho.

Rule: IRC §55–§59; P.L. 119-21 §70107.

**Also touches:** Events

---

### State and local deduction ka schedule fix hai.

```
2026    $40,400, $505,000 se upar 30% phase down, $10,000 se neeche kabhi nahi
2030    wapas $10,000 flat
```

Output: ye **law mein likha hua schedule** hai, inflation-indexed figure nahi. Projection mein har saal step forward karna parega, aur 2030 mein drop karna parega.

Rule: IRC §164(b)(7); P.L. 119-21.

**Also touches:** Events

---

### Capital losses.

```
Pehle gains ko poora offset karo
Phir sirf $3,000 saal ordinary income se
Baaki carry forward, indefinitely
```

Output: bara loss $3,000 saal ke hisaab se use karne mein decades lag sakte hain. Ye expire nahi hota — **lekin client ke inteqal pe khatam ho jata hai**. To zindagi mein use karna kahin behtar hai.

Rule: IRC §1211(b), §1212(b).

**Also touches:** K-1 and business losses · Estate and family

---

## SPENDING AND CARE

### Spending projection mein kaise change hoti hai?

```
working ke doran     monthly spend x 12 x (1 + inflation)^years
retirement ke baad   wohi, x 85%
spouse ke inteqal    wohi, x 75%
   ke baad
```

Output: do step-downs, dono adjustable. **75% wala zyada important hai** — ghar aur uske bills aadhe nahi hote jab ek person chala jata hai, lekin income aksar aadhi ho jati hai.

Rule: dono assumptions hain.

**Also touches:** Estate and family (widow ki aadhi problem ye hai, aadhi tax hai)

---

### Medical alag se inflate kyun hota hai?

```
general spending   2.5% saal
medical spending   5.0% saal
```

Output: healthcare general inflation se roughly **double** speed se barhta hai. 48 saal ki projection mein ye start se kahin bara hissa ban jata hai.

Real example: 2026 mein Medicare Part B premium **9.7%** barha jabke Social Security sirf **2.8%**. Premium benefit se hi deduct hota hai — to logon ka benefit barha aur cheque phir bhi chhota ho gaya.

Rule: rates assumption hain. 2026 ke figures asli rule hain.

**Also touches:** Medicare · Social Security

---

### Long-term care start ho gayi. Plan ka kya hoga?

Inputs: annual care cost · start age · duration · care inflation

Output: roughly **$110,000–$135,000 saal** normal spending ke upar add ho jata hai, aur ye medical rate se inflate hota hai, general rate se nahi.

**Is ka koi government figure hai hi nahi.** Yahan har number adviser ki apni choice hai.

Rule: assumption. Law nahi.

**Also touches:** Life insurance · Medicare · Estate and family

---

### Care ka paisa kaunse bucket se aata hai?

Output: **kisi se nahi.** Care cost general expenses mein chala jata hai, aur phir normal withdrawal order se fund hota hai — pehle brokerage, phir pre-tax, phir Roth.

Picture pe jo "Disability / LTC Protection" bucket hai, jismein 3% saal jata hai — **wo kabhi touch hi nahi hota.** Wo investment rate pe compound hota rehta hai, jabke jis care ke liye bana tha uska paisa kahin aur se ja raha hai.

Rule: humara calculation — ye defect hai.

**Also touches:** The seven buckets · Taking money out

---

### Care wale saal mera tax bilkul gir gaya. Ye theek hai?

Output: haan, aur is pe planning karni chahiye. Income floor se upar ka medical cost deduct hota hai, aur bara care wala saal zyadatar taxable income khatam kar deta hai.

Real example: $190,000 AGI ke against $151,000 expenses — $136,750 deductible nikla, aur federal tax **$4,891** aya, warna roughly $17,222 hota.

Wo khali space client ki zindagi ki **sab se sasti Roth conversion** ki jagah hai — neeche Taking money out ke cases dekhein.

Rule: IRC §213(a).

**Also touches:** Taking money out · Life insurance

---

### Paisa khatam ho gaya to kya hoga?

Output: pehle brokerage khali hoti hai, phir pre-tax, phir Roth. Agar teenon empty hain aur phir bhi shortfall hai, to plan saaf likh deta hai:

> "Age 87: accounts run out. The plan is short by $42,000 this year."

Ye chup chaap negative balance le kar continue nahi karta. **Is line ko kabhi scroll kar ke mat guzrein** — kisi bhi projection ki sab se important line yehi hai.

Rule: humara calculation. Law nahi.

**Also touches:** Taking money out · Growth

---

## PUTTING MONEY IN

### Is saal main 61 ka hua. Kya $11,250 wala catch-up $8,000 ke upar lagega?

```
Age 50-59    24,500 +  8,000  =  $32,500
Age 60-63    24,500 + 11,250  =  $35,750     NOT 24,500 + 8,000 + 11,250
Age 64+      24,500 +  8,000  =  $32,500
```

Output: **bara wala chhote ki jagah leta hai. Dono stack nahi hote.** $35,750, na ke $43,750.

Rule: IRC §414(v)(2)(E)(i); SECURE 2.0 §109.

**Also touches:** Money coming in

---

### Main 64 ka ho raha hoon aur payroll abhi bhi pichle saal wala set hai.

```
Age 63    $35,750
Age 64    $32,500      capacity $3,250 kam
```

Output: bara catch-up sirf ages 60, 61, 62 aur 63 ke liye hai. 64 pe close ho jata hai, aur agar payroll change na ki to client over-defer kar dega.

Rule: IRC §414(v)(2)(E)(i).

**Also touches:** Tax

---

### Meri income $150,000 se upar hai aur catch-up ka deduction khatam ho gaya.

Inputs: **pichle calendar year ki FICA wages usi employer se** · catch-up amount

Output: us wage line se upar, catch-up Roth side pe jana zaroori hai. Abhi deduction nahi, baad mein tax-free.

Teen cheezein jo log ghalat samajhte hain:
- Ye **pichle** saal ko dekhta hai, is saal ko nahi.
- Ye **ek employer ki wages** dekhta hai, total income nahi.
- Self-employment income FICA wages nahi hai, is liye ye trigger nahi karti.

Rule: IRC §414(v)(7); SECURE 2.0 §603; Notice 2023-62.

**Software mein ye ghalat hai.** Wo current year income test karta hai, pichle saal ki wages ki jagah.

**Also touches:** Taking money out (Roth balance pe forced withdrawal nahi lagti)

---

### Meri ek salaried job hai aur ek unrelated side business. Total kitna daal sakta hoon?

```
Ek  $24,500 limit  — ye PERSON ke saath chalti hai, sab plans mein ek hi
Ek  $72,000 limit  — ye PLAN ke saath, har unrelated employer ke liye alag
```

Output: $24,500 do dafa nahi daal sakte. Lekin $72,000 wali limit har unrelated employer pe alag lagti hai, to side business ke plan mein profit sharing se bohat zyada ja sakta hai.

Rule: IRC §402(g)(1), §415(c)(1)(A).

**Also touches:** K-1 and business losses (side business ka structure isko change karta hai)

---

### Do employers ke darmiyan over-defer kar diya, February mein pata chala.

Output: **15 April tak correct kar lein.** Agar na kiya to us paise pe **do dafa** tax lagega — ek dafa jate waqt, dobara nikalte waqt.

Ek employer doosre ka plan dekh nahi sakta, is liye ye catch karna sirf client ka kaam hai.

Rule: IRC §402(g)(2).

**Also touches:** Tax

---

### Meri income Roth IRA ke liye zyada hai, to non-deductible daal kar convert kar loon?

```
Basis fraction   7,500 ÷ 207,500  =  3.6%
Tax-free hissa                       $271
Taxable hissa                      $7,229     — 96.4%
```

Output: conversion **tax-free nahi hai.** Aapki saari traditional, SEP aur SIMPLE IRA 31 December ko **ek hi pot** count hoti hain, to purana pre-tax paisa nayi contribution ko kharab kar deta hai.

Fix, agar employer plan accept kare: pehle purana IRA ka paisa **401(k) mein roll kar dein**. Plan balance pot mein count nahi hota; IRA balance hota hai.

Rule: IRC §408(o), §408A(d)(3), §408(d)(2).

**Also touches:** Taking money out

---

### Saalon non-deductible contribute kiya aur ab paperwork nahi mil raha.

```
Basis fraction  75,000 ÷ 600,000  =  har future withdrawal ka 12.5% tax-free
```

Output: wo 12.5% zindagi bhar real paisa banata hai — **lekin sirf tab jab Form 8606 file hua ho.** Filing history na ho to client wohi paisa do dafa tax de sakta hai.

Rule: IRC §408(o), §408(d)(2); Form 8606.

**Also touches:** Forced withdrawals · Estate and family

---

### Mere spouse ka koi workplace plan nahi, mera hai. Deduction milega?

```
Jiska plan hai         $129,000 - $149,000
Jiska plan NAHI hai    $242,000 - $252,000
```

Output: ek hi household mein do bilkul alag ranges. Jiska plan nahi hai, usko aksar deduction mil jata hai jab doosre ko nahi milta.

Rule: IRC §219(g), §219(g)(7).

**Also touches:** Tax

---

### Plan actually mujhe kitna contribute karne deta hai?

Teen cheezon mein se **sab se kam**: jo aap ne manga, legal limit, aur aapki salary.

To jis client ka business profit bara hai lekin W-2 salary chhoti, wo salary se cap ho jata hai. Aur retirement pe sab stop.

**Also touches:** Money coming in · The seven buckets (401k bucket in limits ko ignore karta hai)

---

## GROWTH

### Projection kaunse rates use karti hai?

| | Conservative | Expected | Accelerated |
|---|---|---|---|
| Income growth | 2.0% | 3.0% | 4.0% |
| Retirement accounts | 5.0% | **7.0%** | 9.0% |
| Real estate | 3.5% | **5.0%** | 6.5% |
| Inflation | 0% | **3%** | 0% |
| Strategy effectiveness | 80% | 100% | 125% |

Brokerage 5.75% pe grow karta hai, insurance cash value 5.5% pe.

Output: **in mein se har ek assumption hai.** Kisi ka koi government source nahi, aur kisi ko bhi client ke saamne fact bana kar present nahi karna chahiye.

**Teen mein se do scenarios 0% inflation use karte hain.** 48 saal ki projection 0% inflation pe conservative nahi hai — ye chup chaap ending value ko asal se bohat bara dikhati hai.

**Also touches:** The seven buckets · Checking the picture

---

### "Strategy effectiveness 125%" ka kya matlab hai?

Output: matlab ye ke strategies adviser ke apne estimate se **ek chauthai zyada** deliver karengi. Ye ummeed hai, calculation nahi. Isko kabhi client ka default nahi banana chahiye.

Rule: assumption. Law nahi.

**Also touches:** The seven buckets

---

### Sab kuch future dollars mein calculate kar ke aaj ke dollars mein kyun dikhate hain?

Output: kyunke tax brackets inflation se barhte hain lekin kuch limits law mein **hamesha ke liye frozen** hain:

```
Bracket ceilings          har saal indexed
Social Security pe tax    $32,000 / $44,000  — 1983 aur 1993 se frozen
Net investment income     $250,000           — 2013 se frozen
$25,000 rental allowance                     — 1986 se frozen
```

Agar pehle dollars chhote kar dein to chhoti income ko frozen limits se compare karenge, aur har agle saal ka tax kam dikhega.

Rule: kaunse thresholds frozen hain — asli rule. Method — humara calculation.

**Also touches:** Social Security · Tax

---

### Contributions ko poore saal ki growth milti hai?

Output: nahi, **aadhe saal ki**. Paisa poore saal mein spread ho kar aata hai, 1 January ko nahi. Full year growth dein to har saal balance thora zyada dikhega — aur wo error pachas saal compound hoti rehti hai.

Rule: humara calculation. Law nahi.

**Also touches:** Putting money in

---

### Advisory fee ka kya asar hai?

```
retirement return = return - advisory fee
bucket returns    = return - admin fee - cost of investment
```

Output: fee return se seedha deduct hoti hai, compound hone se pehle. **48 saal mein 1% fee, 1% nuqsan nahi hoti — us se kai guna zyada hoti hai.**

Rule: assumption. Law nahi.

**Also touches:** The seven buckets

---

### Retirement ke bilkul start mein market gir jaye to?

Output: **plan ye dikha hi nahi sakta.** Har saal ek flat rate apply hota hai — na crash, na recovery, na returns ka order.

Aur ye matter karta hai: withdrawal ke pehle saalon ka bura return, baad ke buray saal se **kahin zyada** damage karta hai, kyunke aap sasta bech kar guzara kar rahe hote hain.

Rule: assumption — aur ye limitation client ko saaf batani chahiye.

Missing: crash ki koi modelling nahi hai. Is sawal ka jawab abhi "model ye nahi dikha sakta" hai.

**Also touches:** Taking money out · Events

---

## SOCIAL SECURITY

### 62 pe loon, 67 pe ya 70 pe?

Jiski full retirement age 67 hai:

| Kab claim karein | Monthly benefit |
|---|---|
| 62 | roughly **70%** |
| 67 | 100% |
| 70 | roughly **124%** |

Output: dono ends ka farq roughly **77% zyada per month** hai — aath saal wait karne ka. Ye permanent hai, aur survivor benefit mein bhi carry hota hai.

Rule: Social Security Act §202(q), §202(w); 20 CFR §404.313.

**Also touches:** Taking money out (wait karne se sab se sasti conversion years free hoti hain) · Estate and family

---

### 70 tak wait karne ka number mere expectation se chhota hai. Kyun?

Output: cost-of-living increases **age 62 se** accrue hona start ho jate hain, chahe aap claim karein ya na karein. Jo 70 tak wait karta hai, uske pehle cheque se pehle hi aath saal ke increases jama ho chuke hote hain.

Agar isko claiming age se count karein to wait karne wale client ka number roughly **24% for life** kam dikhta hai — aur poora system wait karne ke khilaf ho jata hai.

Rule: Social Security Act §215(i).

**Also touches:** Age by age

---

### 63 pe claim kiya aur part-time kaam bhi kar raha hoon. Cheque stop kar diye.

```
2026 exempt amount                $24,480 saal
Withhold                          har $2 upar pe $1
Jis saal full age aati hai        $65,160, aur har $3 pe $1
Full age ke baad                  kuch withhold nahi hota, chahe income kitni ho
```

Output: benefit **withhold** hua hai, khatam nahi. Neeche wala sawal zaroor poochein.

Rule: Social Security Act §203(f).

**Also touches:** Money coming in

---

### Wo withheld paisa hamesha ke liye gaya?

Output: **Nahi.** Full retirement age pe benefit dobara upar recalculate hota hai aur withheld months ka credit mil jata hai.

Zyadatar logon ko sirf pehla aadha bataya jata hai, aur wo zaroorat se zyada wait kar lete hain.

Rule: Social Security Act §203; 20 CFR §404.430.

**Also touches:** Age by age

---

### Mere paas $400,000 IRA aur portfolio income hai. Kya isse mera early benefit katega?

Output: **Nahi.** Earnings test sirf **earned income** count karta hai — salary aur self-employment. Pension, IRA withdrawal, interest, dividend, rent, capital gain aur K-1 income, sab is test mein ignore hote hain.

Haan, ye is baat pe asar karte hain ke benefit pe **kitna tax** lagega. Do alag tests hain, aur log inko hamesha confuse karte hain.

Rule: Social Security Act §203(f).

**Also touches:** Forced withdrawals · Property · K-1 and business losses

---

### Meri wife ne kabhi job nahi ki. Wo mere record pe kya le sakti hai?

Output: uski full retirement age pe husband ke benefit ka **50% tak**. Pehle claim kare to kam.

Full age se aage wait karne se spousal benefit mein **kuch nahi barhta** — jo delayed credits banday ka apna benefit barhate hain, wo yahan apply hi nahi hote.

Rule: Social Security Act §202(b), (c), (q).

**Also touches:** Estate and family

---

### Mera apna chhota benefit hai aur spousal bara. Dono milenge?

Output: **Nahi. Benefits kabhi add nahi hote.** Jo bara hai wohi milta hai, dono ka total nahi.

Ye is poore topic ki sab se common misunderstanding hai.

Rule: Social Security Act §202(k); POMS RS 00615.020.

**Also touches:** Estate and family (widow ko ek benefit milta hai, do nahi)

---

### Sirf spousal abhi le loon aur apna 70 tak barhne doon?

Output: **Nahi, ye option close ho chuka hai.** Ye sirf un logon ke liye bacha hai jo 1 January 1954 ya us se pehle paida hue. Baaki sab ke liye samjha jata hai ke unhon ne dono ke liye file kar diya, aur bara wala mil jata hai.

Rule: Social Security Act §202(r); Bipartisan Budget Act 2015.

**Also touches:** Taking money out

---

### Mere husband ka inteqal ho gaya. Ab mujhe kya milega?

Output: widow ko dono benefits mein se bara mil jata hai, uske claiming age ke hisaab se adjust ho kar. Teen cheezein isko mushkil banati hain:

- Survivor ki full age retirement wali full age se **alag** hai. Table alag hai.
- Agar unhon ne 62 pe early claim kiya tha, wo reduction widow ke saath chalti hai.
- Ek alag ceiling bhi lagti hai us par jo wo actually receive kar rahe the.
- 60 pe survivor benefit roughly **71.5%** hota hai.

Rule: Social Security Act §202(e), (f); POMS RS 00615.320, RS 00615.301.

**Also touches:** Estate and family

---

### Main 60 saal ki widow hoon. Kya ek benefit permanently choose karna parega?

Output: **Nahi** — aur ye bohat valuable baat hai. Survivor benefit aur apna retirement benefit ek doosre ke against lock nahi hote. Ek abhi le lein, aur baad mein doosra jab barh jaye tab switch kar lein.

Rule: Social Security Act §202(e), (f).

**Also touches:** Taking money out

---

### Unke jane ke baad meri income mushkil se badli, lekin tax bohat barh gaya.

Output: isko widow's penalty kehte hain, aur ye **teen cheezein ek saath** hain:

| | Married | Akele |
|---|---|---|
| Brackets | chaure | roughly **aadhe** |
| Social Security pe tax is se upar | $32,000 / $44,000 | **$25,000 / $34,000** |
| Investment tax is se upar | $250,000 | **$200,000** |
| Medicare surcharge start | $218,000 | **$109,000** |

Real numbers: income **12% kam**, federal tax **29.5% zyada**, haath mein paisa **16.9% kam**.

Rule: IRC §1(j)(2), §86(c), §1411; Social Security Act §1839(i).

**Also touches:** Estate and family (jaldi Roth conversion ki sab se bari wajah yehi hai) · Medicare · Taking money out

---

### 12 saal ki shaadi ke baad divorce hua. Kya main ex-husband ke record pe claim kar sakti hoon?

Output: **Haan** — shaadi das saal ya zyada, abhi remarried nahi, aur dono kam az kam 62 ke. Divorce ko do saal ho gaye to wo claim kar sakti hai chahe usne khud file na kiya ho.

Isse unko koi nuqsan nahi hota, unka ya unki nayi wife ka benefit kam nahi hota, aur unko notify bhi nahi kiya jata.

Rule: Social Security Act §202(b)(2), (c)(2).

Missing: **software mein ye implement nahi hua.**

**Also touches:** Events

---

### Main 63 ki widow hoon. Remarry karne se survivor benefit chala jayega?

Output: **Nahi.** 60 ya us ke baad remarry karne se survivor benefit khatam nahi hota. 60 se pehle karne se hota hai.

Rule: Social Security Act §202(e), (f).

**Also touches:** Estate and family · Events

---

### Main retired teacher hoon, mujhe bataya gaya tha ke benefit cut hoga.

Output: **ab nahi.** Wo rules jo government pension walon ka benefit reduce karte the, December 2023 ke baad ke months ke liye repeal kar diye gaye.

Rule: P.L. 118-273, Social Security Fairness Act.

**Also touches:** Money coming in

---

### Mere benefit pe actually kitna tax lagta hai, aur har saal bura kyun ho raha hai?

```
Provisional income = AGI + tax-free interest + aadha benefit

Married      $32,000 tak      koi tax nahi
             $32,000-$44,000  50% tak taxable
             $44,000 se upar  85% tak taxable
```

Output: **ye thresholds kabhi indexed nahi hue.** 1983 aur 1993 mein set hue the aur tab se nahi hile. Har saal ki inflation zyada households inke upar le aati hai — wohi real income har saal zyada tax hoti hai.

Rule: IRC §86; P.L. 98-21; P.L. 103-66.

**Also touches:** Forced withdrawals · Taking money out

---

### Maine sab kuch municipal bonds mein daal diya taake benefit pe tax na lage.

Output: **ye kaam nahi karta.** Tax-free interest ko naam le kar wapas provisional income mein add kiya jata hai. Wo income tax se exempt hai, yahan se nahi — aur Medicare surcharge ke liye bhi count hota hai.

Rule: IRC §86(b)(2)(B); 20 CFR §418.1010.

**Also touches:** Medicare · Growth

---

## FORCED WITHDRAWALS

Ek age ke baad government pre-tax account mein paisa parha rehne nahi deti. Har saal ek fixed amount nikalna parta hai aur us pe ordinary income tax dena parta hai — chahe zaroorat ho ya na ho.

---

### Mere kab start honge — 73 ya 75?

| Birth year | Pehli forced withdrawal |
|---|---|
| 1951 se pehle | 72 |
| 1951 – 1959 | **73** |
| 1960 ya baad | **75** |

Output: ek hi age, sirf birth year se fix. Koi overlap nahi, koi choice nahi.

Rule: IRC §401(a)(9)(C)(v); SECURE 2.0 §107.

**Also touches:** Taking money out (is age se pehle wale saal convert karne ke liye sab se saste hain) · Age by age

---

### Amount calculate kaise hota hai?

```
1,000,000 ÷ 24.6  =  $40,650     (age 75)
```

Pichle 31 December ka balance, table ke divisor se divide. **Us saal jo age aap ko lagi**, wohi count hoti hai — withdrawal wale din ki age nahi. 30 December ki birthday wohi answer deti hai jo 2 January ki.

Rule: IRC §401(a)(9); Treas. Reg. §1.401(a)(9)-9(c); Pub 590-B Table III.

**Also touches:** Tax

---

### Mera balance hil hi nahi raha lekin forced amount har saal barh raha hai.

$1,200,000 age 73 pe, 6% growth, har saal poori withdrawal:

| Age | Divisor | Forced out | Balance baad mein | Hissa |
|---|---|---|---|---|
| 73 | 26.5 | $45,283 | $1,224,000 | 3.77% |
| 75 | 24.6 | $50,673 | $1,267,640 | 4.07% |
| 80 | 20.2 | $65,988 | $1,342,986 | 4.95% |
| 85 | 16.0 | $84,362 | $1,341,361 | 6.25% |
| 90 | 12.2 | $103,190 | $1,225,069 | 8.20% |

Output: 73 se 90 tak forced income **double se zyada** ho jati hai, jabke balance almost wahin ka wahin. Client mein kuch nahi badla — **divisor chhota ho gaya.**

Isko log tax bomb kehte hain. Balance safe lagta hai, is liye kisi ko aata hua nazar nahi aata.

Rule: divisors asli rule hain. 6% growth assumption hai.

**Also touches:** Social Security (zyada benefit tax mein aa jata hai) · Medicare (surcharge upar chala jata hai) · Taking money out (jaldi convert karna hi asli defence hai)

---

### Kya pehli wali 1 April tak defer kar sakta hoon?

```
Age-73 ka amount, agle saal mein   $32,075
Age-74 ka amount                   $35,333
Agle saal taxable                  $67,409
Waqt pe le lete to                 $35,333
Ek saal mein extra income          $32,075
```

Output: haan, allowed hai. Aur aksar mistake hoti hai. **Do saal ki forced income ek hi bracket mein** aa girti hai, aur wohi saal do saal baad ka Medicare surcharge bhi set kar deta hai.

Ye sirf tab theek hai jab is saal ka rate agle saal se genuinely zyada ho.

Rule: IRC §401(a)(9)(C).

Missing: software April wali deadline aur do-in-one-year wala outcome model nahi karta.

**Also touches:** Medicare · Tax

---

### Mere teen purane 401(k) aur do IRA hain. Sab ek se nikal loon?

| Account | Combine kar sakte hain? |
|---|---|
| Traditional / SEP / SIMPLE IRA | Haan — total karein, kisi ek se nikal lein |
| 403(b) | Sirf aapas mein |
| **Har 401(k)** | **Nahi — har ek separately** |
| **Har 457(b)** | **Nahi — har ek separately** |

Output: sab ek 401(k) se nikal liya to baaki har plan mein shortfall reh jata hai — **aur har shortfall pe apna alag penalty lagta hai.**

Rule: Treas. Reg. §1.401(a)(9)-8.

**Also touches:** Taking money out

---

### Maine kuch nikala hi nahi. Ab kya?

```
Penalty 25% pe                       $10,500
Do saal ke andar correct karein, 10%  $4,200
```

Output: jitna nikalna chahiye tha us pe excise tax. Reasonable error ho to Form 5329 se waive bhi ho sakta hai.

Rule: IRC §4974.

Missing: software assume karta hai ke client hamesha comply karta hai, is liye ye kabhi dikhata hi nahi.

**Also touches:** Tax

---

### Main 74 ka hoon aur abhi bhi working hoon. Start karna parega?

Output: sirf **us employer ke plan** ke liye jahan client **abhi bhi kaam kar raha hai**, aur wo bhi tab jab plan document allow kare.

Do traps jo bilkul un logon ko pakarte hain jo is baare mein sab se zyada confident hote hain:
- Jo us business ka **5% se zyada** owner hai, wo ye bilkul use nahi kar sakta.
- Ye **kisi bhi IRA pe kabhi apply nahi hota** — traditional, SEP ya SIMPLE — chahe aap kahin bhi kaam karein.

Puranay employers ke plans apna schedule alag rakhte hain.

Rule: IRC §401(a)(9)(C)(i)(II).

**Also touches:** K-1 and business losses (business owners hi ye sawal poochte hain)

---

### Meri wife 14 saal chhoti hai aur wohi akeli beneficiary hai.

Output: forced amount **kam ho jata hai.** Jab sole beneficiary spouse das saal se zyada chhota ho to alag table apply hota hai.

Wo **poore saal** sole beneficiary honi chahiye. Contingent beneficiary theek hai; doosra primary beneficiary sab khatam kar deta hai.

Rule: Treas. Reg. §1.401(a)(9)-9(d), Joint and Last Survivor Table.

**Software mein ye ghalat hai.** Ye table implement hi nahi hua — plan hamesha ordinary table use karta hai — to is household ko **zyada** withdrawal aur zyada tax dikhaya jata hai, poori projection ke liye.

**Also touches:** Estate and family · Taking money out

---

### Main waise bhi charity deta hoon. Seedha IRA se bhej sakta hoon?

```
Required amount   900,000 ÷ 23.7  =  $37,975
Charity ko bheja                     $30,000   (income mein aata hi nahi)
Taxable remainder                     $7,975
```

Output: AGI $37,975 ki jagah sirf **$7,975** barhta hai. Wo $30,000 income mein appear hi nahi hota — to na Social Security tax mein aata hai, na Medicare bill barhata hai. **Normal donation ye nahi kar sakta.**

2026 limit: **$111,000** per person.

Teen tareeqe jin se ye spoil hota hai:
- **Donor advised fund mein nahi ja sakta.** Ye sab se common failure hai, kyunke client ke paas pehle se hi wo fund hota hai.
- IRA se aana chahiye, 401(k) se nahi.
- Age 70½ — ye forced withdrawal age se pehle aati hai.

Rule: IRC §408(d)(8); §408(d)(8)(B)(i).

**Also touches:** Medicare · Social Security · Estate and family

---

### Mujhe father ka IRA mila. Kitni jaldi empty karna hoga?

| Wo inteqal kar gaye | Saal 1–9 | Saal 10 |
|---|---|---|
| Apni start date se **pehle** | kuch required nahi | empty hona chahiye |
| Start date pe ya **baad** | har saal kuch **required hai** | empty hona chahiye |

Doosri line logon ko pakarti hai. Wo nau saal kuch nahi nikalte, phir penalty **aur** ek hi saal mein bohat bara taxable amount, dono aa jate hain.

Surviving spouse ke paas kuch extra options hote hain jo bachon ke paas nahi.

Rule: IRC §401(a)(9)(B),(H); SECURE Act; SECURE 2.0 §327.

**Also touches:** Estate and family (heir ko is paise pe basis step-up bhi nahi milta)

---

## LIFE INSURANCE

Roadmap har deployed dollar ka 20% yahan daalta hai, aur plan ye hai ke client retirement mein policy se loan le kar tax-free income le. Ye chalta hai — **jab tak nahi chalta**, aur jab fail hota hai to bohat mehnga parta hai.

---

### Main har saal policy se tax-free income lena chahta hoon.

Output: jo policy in force hai, us se liya gaya loan income nahi hai. Paisa AGI mein aata hi nahi — to na Social Security tax mein aata hai, na Medicare surcharge barhata hai. Yehi is ki poori attraction hai.

**Ye sirf tab tak chalta hai jab tak policy zinda hai.** Is pe rely karne se pehle agla case zaroor parhein.

Rule: IRC §72(e), §7702, §101(a).

**Also touches:** Taking money out · Social Security · Medicare · Spending and care

---

### Loan compound hota gaya aur ek saal policy lapse ho gayi. Ab jo paisa maine saalon pehle kharch kiya us pe tax aa gaya.

```
Poori cash value distribution maani gayi      $520,000
Basis minus                                   $300,000
Taxable gain                                  $220,000
Tax 24% pe                                     $52,800
Cash actually mila                                  $0
```

Output: **$52,800 ka bill aur dene ke liye kuch nahi.** Income stream bhi stop, aur jo death benefit family ke liye tha wo bhi gaya.

**Interest hi ye karta hai.** Jo loan interest pay nahi hota wo balance mein capitalise ho kar compound hota rehta hai — to loan cash value se tez barhta hai, bilkul un saalon mein jab cost of insurance bhi barh raha hota hai.

Rule: IRC §72(e).

Software ye model karta hai. Har saal test karta hai aur note likhta hai. **Wo warning kabhi switch off mat karein.**

**Also touches:** Tax · Medicare (aisa spike do saal baad surcharge set kar deta hai) · Estate and family

---

### Maine jaldi jaldi fund kar ke cash value banai.

```
Ordinary policy   $100,000 ka loan               $0 taxable
MEC               $100,000 gain-first nikalta    $100,000 taxable
                  plus 10% agar 59.5 se kam       $10,000
                  total                           $42,000
```

Output: pehle saat saal mein zyada premium daalne se contract **permanently** MEC ban jata hai. Uske baad har distribution **gain-first** nikalta hai aur pehle dollar se taxable hota hai. Ye status wapas nahi hota.

Rule: IRC §7702A(b) seven-pay test; §72(e)(10); §72(v).

**Also touches:** The seven buckets (bara insurance bucket bilkul yehi karne pe encourage karta hai)

---

### Illustration mein 7% tha. Agar 4% credit hua to?

Output: aage sab kuch hil jata hai. Kam crediting matlab kam cash value, matlab loan cash value tak jaldi pohanchta hai, matlab upar wala lapse case **kai saal pehle** aa jata hai.

Software 5.5% default rakhta hai, aur ye wo input hai jo client illustration ke mutabiq set kar sakta hai. **Ye check karne wali cheez hai, accept karne wali nahi.**

Rule: assumption. AG 49-B insurance regulator ki limit hai, tax law nahi.

**Also touches:** Growth · The seven buckets

---

### Main 84 ka hoon aur internal charges barhte ja rahe hain. Ye 90 tak chalegi?

Output: cost of insurance death benefit aur cash value ke **farq** pe charge hota hai, aur age ke saath tezi se barhta hai. Jis policy mein premium ja hi nahi raha aur loan nikal raha hai, wo **dono taraf se** drain ho rahi hai.

Ye har saal test karna parega, assume karna kaafi nahi.

Rule: test assumption hai. Sirf consequence asli rule hai.

**Also touches:** Age by age

---

### Meri apni jaan pe $4,000,000 ki policy hai. Kya ye mere estate mein aayegi?

```
Apne naam pe          $17,000,000 estate  →  roughly $800,000 estate tax
Shuru se trust ke naam                     →  $0
```

Output: death benefit **income tax** se dono soorton mein free hai. Lekin **estate tax** se free hoga ya nahi, ye poori tarah is pe hai ke **rights kis ke paas hain** — beneficiary change karna, surrender karna, loan lena, ya assign karna.

Rule: IRC §2042; §101(a)(1).

**Also touches:** Estate and family · The seven buckets

---

### Maine do saal pehle policy trust mein transfer ki thi. Ab theek hai?

Output: **Nahi — abhi nahi.** Death se teen saal ke andar transfer ki gayi policy poori wapas estate mein aa jati hai. Ek example mein death se 26 mahine pehle transfer karne pe poore $4,000,000 wapas aaye aur $800,000 ka tax laga.

Trust ko policy **shuru mein buy karni** chahiye, baad mein receive nahi karni chahiye.

Rule: IRC §2035(a).

**Also touches:** Estate and family

---

### Policy loan ka interest to kam az kam deduct ho jayega?

Output: **Nahi.** Policy loan interest generally deductible nahi hai.

Rule: IRC §264.

**Also touches:** Tax

---

### Mujhe policy surrender karni hai. Kitna taxable hoga?

Output: jitna premium diya us se upar sab kuch — aur ye **ordinary income** hai, capital gain nahi. Jo loan outstanding hai wo bhi received paisa count hota hai — isi liye log aksar cheque se **zyada** amount pe tax dete hain.

Rule: IRC §72(e).

**Also touches:** Tax · Medicare

---

## LONG-TERM CARE

### Care ka actual cost kitna hai aur kitne saal?

Output: **koi government figure hai hi nahi.** Koi federal agency real cost schedule publish nahi karti. Roadmap $110,000–$135,000 saal use karta hai (national median private room roughly $129,575), aur isko general inflation se upar wale healthcare rate se inflate karta hai.

Is ka har hissa adviser ki apni choice hai, aur waise hi dikhana chahiye.

Rule: assumption.

**Also touches:** Spending and care · Medicare · Estate and family

---

### Mera $7,500 ka LTC premium — kitna deduct hoga?

| Age | Deductible |
|---|---|
| 40 ya kam | $500 |
| 41 – 50 | $930 |
| 51 – 60 | $1,860 |
| 61 – 70 | $4,960 |
| 71 aur upar | $6,200 |

Example: ages 58 aur 72 — $1,860 + $6,200 count hote hain, **$3,640 kisi bhi level pe deduct nahi hota.** Aur jo count hota hai wo bhi sirf medical deduction mein jata hai, jiska apna income floor hai.

Rule: IRC §213(d)(10), §7702B(b); Rev. Proc. 2025-32.

**Also touches:** Tax · Spending and care

---

### Meri policy $500 daily deti hai lekin care sasti hai. Extra pe tax lagega?

```
Mila            $500 x 365    =  $182,500
2026 limit      $430 daily    =  $156,950
Taxable                          $25,550
```

Output: sirf indemnity ya per-diem contract pe. Jo contract actual cost reimburse karta hai, us mein excess hota hi nahi.

Rule: IRC §7702B(d); Rev. Proc. 2025-32.

**Also touches:** Tax · Medicare

---

### Care wale saal meri income tabah ho gayi. Us saal convert karoon?

Output: aksar **haan**, aur ye counter-intuitive lagta hai. Bara medical deduction taxable income itni neeche le aata hai ke us space mein convert karna bohat sasta parta hai.

Real numbers: us room mein $57,550 convert karne pe sirf $10,140 laga — yani effective **17.6%**.

Rule: §213 room banata hai; §408A conversion govern karta hai.

**Also touches:** Taking money out · Estate and family (ye surviving spouse ko bhi protect karta hai)

---

## PROPERTY

Rental loss ko wohi four gates paas karne parte hain jo K-1 loss ko. Lekin property ke do gates **un se pehle** hain, aur order optional nahi hai.

```
Gate 0   §280A    personal use — pehle test hota hai
Gate 0b  §469     passive hai bhi ya nahi? (7-day rule)
phir     §704(d) → §465 → §469 → §461(l)
```

---

### Maine rental li aur cost segregation study ne isko bara paper loss bana diya.

Output: cost segregation building ko chhoti life wale parts mein divide karta hai, aur 100% bonus depreciation un parts ko foran write off kar deta hai. Jo property cash mein profit de rahi hai wo paper pe bara loss dikha sakti hai.

Wo loss kisi kaam ka hai ya nahi, ye bilkul alag sawal hai — agla case dekhein.

Rule: IRC §167, §168(c),(e), §168(k); §1016(a)(2).

**Also touches:** K-1 and business losses (ab loss ko chaar gates paas karne hain) · Tax

---

### Meri income $600,000 hai aur mujhe bataya gaya ke loss is saal bekaar hai.

Output: long-term rental **definition se hi** passive hai, client chahe kuch bhi kare. $25,000 wala allowance $150,000 income se upar khatam ho jata hai. To loss suspend ho jata hai aur is saal kuch nahi karta.

Paper loss real hai. Tax benefit abhi nahi hai.

Rule: IRC §469(c)(2); §469(i).

**Also touches:** K-1 and business losses · Money coming in

---

### Wohi property short-term rental ke tor pe meri salary offset kar deti hai. Kyun?

```
Average stay  =  total rental days / number of stays

7 din ya kam  +  material participation   →  passive NAHI
                                          →  W-2 income offset karta hai
```

Output: ye poore property section ka sab se bara swing hai. Wohi building, wohi loss, aur jawab poori tarah **average booking length** pe badal jata hai.

Rule: Treas. Reg. §1.469-1T(e)(3)(ii)(A); §1.469-5T(a).

**Also touches:** K-1 and business losses (phir bhi at-risk aur overall cap clear karna hai) · Medicare (bara W-2 offset AGI hilata hai, jo surcharge hilata hai)

---

### Ek lambi winter booking ne mera average saat din se upar kar diya.

Output: **poora saal fail ho jata hai.** Wo ek booking nahi — poora saal. Property har din ke liye wapas passive ho jati hai, aur poora loss suspend ho jata hai.

7.4 din ka average bhi failure count hota hai.

Rule: Treas. Reg. §1.469-1T(e)(3)(ii)(A).

**Also touches:** K-1 and business losses

---

### Maine management company rakhi hai, aur loss phir bhi suspend ho gaya.

Output: seven-day test to paas ho gaya, lekin material participation fail ho gaya. Manager ke hours doosre individual ki participation hain, aur wo kai tests mein client ke against count hote hain.

Investor ke tor pe lagaya gaya waqt — statements parhna, finances review karna — participation count hota hi nahi.

Rule: Treas. Reg. §1.469-5T(a)(1)–(7); §1.469-5T(f)(4).

**Also touches:** K-1 and business losses

---

### Kya main real estate professional ban kar apne saare rentals free kar sakta hoon?

```
750 hours   real property business mein
   AUR
saal ki TOTAL working time ka aadhe se zyada
```

Output: doosra test hi zyadatar logon ko rok deta hai. Kahin aur full-time job ho to "aadhe se zyada" arithmetic ke lehaz se mumkin hi nahi, chahe property pe kitne hours lagayein.

Aggregation election rentals ko group kar deta hai — lekin phir sirf ek property bechne pe loss release block ho jata hai.

Rule: IRC §469(c)(7)(B); Treas. Reg. §1.469-9(g).

**Also touches:** Money coming in · K-1 and business losses

---

### Hum beach house khud bhi kuch hafte use karte hain.

```
Personal use 14 din ya rental days ke 10%, jo bara ho, us se zyada
  →  expenses allocate hoti hain
  →  deductions rental income tak cap ho jati hain
  →  koi loss bachta hi nahi
```

Output: ye **sab se pehle** test hota hai, chaar gates se pehle. Agar ye lag gaya to gates tak kuch pohanchta hi nahi. Jo client aisi property pe loss plan kar raha hai jahan wo chhutti bhi manata hai, wo asal mein kuch plan nahi kar raha.

Family ka use bhi count hota hai, aur family ki definition wusee hai.

Rule: IRC §280A(d)(1), (d)(2), (e), (c)(5).

**Also touches:** K-1 and business losses

---

### Mera beta rental mein rehta hai. Kya isse sab kharab ho jayega?

Output: family ka use personal use count hota hai — **magar** agar wo family member poora market rent de raha hai aur wahi uska principal residence hai to nahi. Dono conditions, ek nahi.

Rule: IRC §280A(d)(2)(A), (d)(3); §267(c)(4).

**Also touches:** Estate and family

---

### Kya main apna ghar apni company ko 14 din ke liye tax free rent kar sakta hoon?

Output: **haan**, aur ye un chand cheezon mein se hai jo waqai free hain. Saal mein 14 din tak, wo rent client ki income mein aata hi nahi, aur company phir bhi deduct karti hai.

Comparables se supported daily rate aur real business purpose chahiye. 15 din pe poori cheez khatam ho jati hai aur sab kuch income ban jata hai.

Rule: IRC §280A(g).

**Also touches:** K-1 and business losses · Tax

---

### Maine rental bech di aur unexpected recapture aa gaya.

Output: jitni depreciation saalon mein li thi wo sab wapas aati hai. Aur bura ye ke jo cost segregation ne fast early deductions diye the, wo **ordinary rates** pe wapas aate hain, us 25% pe nahi jo building pe lagta hai.

| Component | Sale pe rate |
|---|---|
| Cost-segregated personal property (§1245) | **ordinary** |
| Building ki depreciation (§1250) | 25% ceiling |
| Baqi gain (§1231) | capital gain |
| Upar se, agar apply ho | 3.8% investment tax |

25% **ceiling** hai, flat rate nahi — 25% ya client ka apna marginal rate, jo kam ho.

Rule: IRC §1245, §1250, §1(h)(1)(E), §1231, §1411.

**Also touches:** Medicare (sale wala saal surcharge set kar deta hai aur appeal nahi hoti) · K-1 and business losses (sale suspended losses release karti hai)

---

### Maine kabhi depreciation claim hi nahi ki, to recapture kis baat ka?

Output: **ghalat.** Recapture us depreciation pe calculate hoti hai jo **allowed ya allowable** thi. Client un deductions pe tax deta hai jo usne kabhi li hi nahi.

Ye recover ho sakti hai — accounting method change kar ke missed depreciation ek saal mein le aayein — lekin ye deliberately karna parta hai.

Rule: IRC §1016(a)(2); §446/§481(a), Form 3115.

**Also touches:** Tax

---

### Kya main sale ko doosri property mein roll kar sakta hoon?

Output: haan, lekin ye defer karta hai, maaf nahi karta. Purana basis aur poori depreciation history nayi property mein carry ho jati hai, to recapture abhi bhi wait kar rahi hai.

Hard deadlines: 45 din identify karne ke, 180 din close karne ke, aur paisa qualified intermediary ke paas rehna chahiye — client kabhi touch nahi kar sakta. Jo cash nikaal liya wo foran taxable hai.

Death tak hold karein to poori chain step-up se clear ho jati hai.

Rule: IRC §1031(a),(b),(d),(a)(3).

**Also touches:** Estate and family

---

### Hum family home bech rahe hain.

```
Pichle 5 saal mein se 2 saal own kiya aur waha rahe
Exclude:  $250,000 single  /  $500,000 married
```

Output: us se upar ka gain taxable hai. Aur ye exclusion **us depreciation ko cover nahi karta** jo May 1997 ke baad home office ya rental period ke liye claim ki gayi — wo hissa har haal mein taxable hai.

Har do saal mein ek dafa use ho sakta hai.

Rule: IRC §121(a),(b),(b)(3),(d)(6).

**Also touches:** Medicare · Tax

---

### Meri equity barh rahi hai. Kya ye mortgage utarne se hai?

```
Pehle saal principal utra   $5,589
```

$500,000 ka loan 6.5% pe.

Output: shuru ki almost saari equity appreciation hai, repayment nahi. Pehle saal loan ka mushkil se 1% utarta hai. Clients is ko hamesha zyada samajhte hain.

Rule: assumption — standard amortisation aur assumed growth rate.

**Also touches:** Growth · Estate and family

---

### Property mortgage se kam ki hai aur main chhorna chahta hoon.

Output: ye poori tarah is pe hai ke debt recourse hai ya nonrecourse, aur dono ke jawab bilkul alag hain. Jo recourse debt maaf hoti hai wo income hai jab tak koi exclusion na lage; nonrecourse debt seedha sale price mein add ho jati hai. At-risk recapture bhi fire kar sakti hai.

Rule: IRC §1001; §61(a)(11); §108(a)(1)(B),(D); §465(e).

Missing: is ka koi dedicated case likha hua nahi hai. Ye har Case Register se bahar hai aur specialist advice chahiye.

**Also touches:** K-1 and business losses · Tax

---

### Software ke baare mein ek baat

Property list aur "current real estate value" wali field engine ke do alag hisson mein jati hain — projection, aur real estate bucket. Jo client ek hi ghar dono jagah daal deta hai, wo **do dafa** count hota hai.

**Also touches:** The seven buckets

---

## K-1 AND BUSINESS LOSSES

Client kisi deal mein paisa lagata hai. K-1 aata hai jis pe loss hai. Wo tax refund expect karta hai. Aksar kuch nahi milta.

Business loss **chaar gates se, isi fixed order mein** guzarta hai. Har gate clear karna zaroori hai agle tak pohanchne ke liye. Jo gate isko rokta hai wohi decide karta hai ke ye baad mein kaise free hoga — aur har gate alag event se free hota hai.

```
Gate 1   §704(d) / §1366(d)   basis
Gate 2   §465                 at risk
Gate 3   §469                 passive
Gate 4   §461(l)              excess business loss
```

Order badal dein to jawab bhi badal jata hai.

---

### K-1 pe $250,000 ka loss hai. Is saal tax mein kitna kam hoga?

Inputs: loss $250,000 · basis $180,000 · at risk $150,000 · client business mein kaam nahi karta · koi doosri passive income nahi · salary $600,000

```
Gate 1  §704(d) basis     allowed 180,000   suspended  70,000
Gate 2  §465 at risk      allowed 150,000   suspended  30,000
Gate 3  §469 passive      allowed       0   suspended 150,000
        $25,000 allowance $600,000 income pe poora khatam
Gate 4  §461(l)           yahan tak kuch pohanchta hi nahi

Is saal deduct hua    $0
Suspended             70,000 + 30,000 + 150,000  =  250,000
```

Output: **is saal tax mein $0 kami.** Poore $250,000 wait karte hain, teen hisson mein bante hue. Har dollar exactly ek gate pe ruka hai, aur teenon piles interchangeable nahi hain.

Rule: IRC §704(d) → §465 → §469 → §461(l), isi order mein.

Missing: kya kisi ne partnership debt guarantee ki thi — isse sirf gate 2 badalta hai, aur kuch nahi.

**Also touches:** Tax (AGI nahi badalti, to koi knock-on nahi) · Property (rental loss inhi gates pe marta hai) · Estate and family (har pile client ke inteqal pe alag tareeke se marta hai)

---

### Loss us se bara hai jitna maine actually lagaya tha.

Output: extra amount gate 1 pe ruk jata hai aur tab tak wait karta hai jab tak basis dobara ban na jaye — future income se ya aur paisa daal kar. Ye kabhi expire nahi hota, lekin apne aap kabhi move bhi nahi karta.

Rule: §704(d) with §705 aur §752 partner ke liye; §1366(d)(1) with §1367(a) S-corp shareholder ke liye.

**Also touches:** Estate and family (basis pe ruke hue losses death pe khatam ho jate hain, heirs ko nahi milte)

---

### Partnership pe mortgage hai to mera basis hai — lekin kehte hain main "at risk" nahi hoon.

Output: basis aur at-risk do alag numbers hain aur alag tareeke se move karte hain. Nonrecourse debt basis barhata hai chahe wo qualify kare ya na kare. Lekin at-risk amount sirf **qualified nonrecourse financing** se barhta hai.

Real property pe normal bank mortgage aksar qualify kar jata hai, is liye zyadatar clients ko pata hi nahi chalta ke gate 2 exist karta hai. Seller financing aksar qualify **nahi** karti — seller ka us property mein interest hota hai.

Rule: §465(b)(6); §465(b)(3).

**Also touches:** Property (seller-financed purchases)

---

### Mere partner ne personally loan guarantee kiya, aur ab MERE losses block hain.

Output: kisi bhi shakhs ki personal guarantee us debt ko **baaki sab ke liye** qualified nonrecourse financing se disqualify kar deti hai. Jisne guarantee ki usko at-risk amount mil jata hai; baaki partners ka khatam ho jata hai.

Ye co-owner ka at-risk amount girne ka sab se common tareeqa hai.

Rule: §465(b)(6)(B)(iii); §465(b)(1)(B).

**Also touches:** Property · Life insurance (guarantees aur indemnities)

---

### Suna tha $25,000 rental loss deduct hota hai. Mujhe kuch kyun nahi mila?

```
AGI  $95,000   →   poora $25,000 allowance
AGI $120,000   →   25,000 − 0.50 × (120,000 − 100,000)  =  $15,000
AGI $150,000   →   $0
```

Output: allowance $100,000 se upar har dollar pe 50 cents girta hai aur $150,000 pe khatam. **Dono figures 1986 se indexed nahi hue**, is liye har saal zyada logon ko pakarte hain.

Rule: §469(i).

**Also touches:** Forced withdrawals (forced distribution wohi AGI barhati hai jo isko khatam karti hai) · Medicare (wohi AGI surcharge chalati hai)

---

### Loss passive hai hi nahi, phir bhi poora use nahi kar sakta.

```
2026 threshold   $256,000 single   ·   $512,000 joint
```

Output: threshold se upar jo hai wo is saal disallow ho jata hai aur agle saal net operating loss ban jata hai.

**2026 mein is pe nazar rakhein.** Threshold $313,000 / $626,000 se **gira** hai — 18.2% ki kami. Thresholds normally barhte hain. Ye nahi barha.

Rule: §461(l)(1) aur (3)(A); §461(l)(2).

**Also touches:** Property (itna bara loss aksar cost segregation se banta hai) · Events (projection ke beech mein law change)

---

## INCOME WITH NO CASH

### K-1 pe $150,000 income likhi hai. Partnership ne mujhe kuch bheja hi nahi. Phir bhi tax dena hai.

Output: client poore $150,000 pe tax deta hai. Isse basis bhi barhta hai, jo future loss mein kaam aata hai — lekin April mein ye koi tasalli nahi.

Tax dene ka cash kahin se to aana hai, aur har source ki apni cost hai.

Rule: §702 aur §704 — distributive share pe tax lagta hai chahe distribution mili ho ya nahi.

Missing: kya operating agreement mein tax-distribution clause hai.

**Also touches:** Taking money out (tax bill kaunse account se fund hoga) · Medicare (ye phantom income bhi surcharge chalati hai)

---

### Kai loss wale saalon ke baad distribution li aur capital gain aa gaya.

Output: losses pehle stock basis khate hain, phir debt basis. Jab basis zero ho jaye, us se upar ki koi bhi distribution capital gain hai — chahe client ko lage ke wo sirf apna hi paisa nikal raha hai.

Rule: §1367(b)(2); §1368 / §731.

**Also touches:** Tax

---

### Bank ne mujhse S corporation ka loan guarantee karwaya. Isse basis nahi milta?

Output: **Nahi.** S-corp shareholder ko debt basis sirf us qarz se milta hai jo **shareholder ne khud company ko diya** ho. Guarantee se kuch nahi milta jab tak shareholder actually pay na kare.

Fix ye hai ke khud loan lein aur company ko aage lend karein — back-to-back. Loss wale business ke liye LLC aur S corporation ka ye sab se mehnga farq hai, kyunke partnership mein partner ko partnership ke debt ka basis **milta hai**.

Rule: §1366(d)(1)(B).

**Also touches:** Money coming in (yehi choice employment tax pe ulta asar karti hai)

---

## GETTING THE LOSSES BACK

### Maine partnership interest bech diya. Kya saare suspended losses wapas aa jayenge?

Output: passive wala pile haan — lekin sirf tab jab **teenon** baatein sach hon: poora interest becha, sale fully taxable thi, aur buyer related party nahi tha. Ek bhi miss ho jaye to release hota hi nahi.

| Kahan suspend tha | Sale pe release? |
|---|---|
| §469 passive | Haan, poora |
| §465 at risk | Haan |
| §704(d) / §1366(d) basis | **Nahi — generally khatam** |

Gift sale nahi hai: suspended loss donee ke basis mein add ho jata hai aur donor ka khatam. Related party ko sale release deti nahi, defer kar deti hai.

Rule: §469(g)(1); §469(g)(1)(B).

**Also touches:** Property (rentals aggregate karne se sirf ek bechne pe release block ho jata hai) · Estate and family

---

### Meri apni practice jis building mein hai wo bhi meri hai. Kya wo rent mere doosre suspended losses kha sakta hai?

Output: **Nahi, aur ye ulta client ke against jata hai.** Apni hi business ko rent dene ka **profit** non-passive recharacterise ho jata hai, to wo passive losses absorb nahi kar sakta. Aur us pe **loss** passive hi rehta hai. Rule sirf ek taraf chalta hai.

Rule: Treas. Reg. §1.469-2(f)(6).

**Also touches:** Property

---

### Mere paas bara carryforward hai. Kab tak actually use hoga?

Output: NOL kisi bhi baad wale saal mein taxable income ka sirf **80%** khatam kar sakta hai, to 20% hamesha taxable rehta hai. Ye indefinitely carry forward hota hai, peeche nahi ja sakta.

Rule: §172(a)(2); §172(b)(1)(A).

**Also touches:** Taking money out (Roth conversion carryforward ko income dene ka acha tareeqa hai)

---

### Mere paas bare suspended losses hain aur meri umar barh rahi hai. Marne pe kya hoga?

Output: zyadatar bura. Ye wo case hai jo clients tab tak nahi poochte jab tak bohat der na ho jaye.

| Pile | Death pe |
|---|---|
| NOL carryforward | **Khatam. Kuch nahi bachta.** |
| §469 passive suspended | Sirf §1014 step-up se upar release hota hai — step-up jitna bara, utna kam wapas |
| §704(d) / §1366(d) basis suspended | **Khatam** |

Rule: §172; §469(g)(2); §1014.

Saada matlab: losses zindagi mein use karne se kahin zyada qeemti hote hain, heirs ke liye chhorne se. Yehi wajah hai ke deliberately income banana — Roth conversion ya gain realise karna — jab tak losses zinda hain, sahi ho sakta hai.

**Also touches:** Taking money out · Estate and family · Age by age

---

## WHAT THE SOFTWARE DOES NOT TELL THE CLIENT

Engine chaaron gates theek chalata hai. Wo exactly calculate karta hai ke har gate pe kitna ruka — basis, at risk, passive — **aur phir wo breakdown phenk deta hai.** Parked amounts har row pe store hote hain lekin **year table ke kisi column mein aur kisi note mein nazar nahi aate.**

To jis client ka $250,000 loss poora suspend ho gaya, uski screen bilkul waisi hi dikhti hai jaise kisi aise client ki jiska koi loss tha hi nahi. Usko kabhi nahi bataya jata ke kis gate ne roka, kitna wait kar raha hai, aur kya cheez isko free karegi.

Isi liye is sawal ka koi jawab nahi tha.

**Also touches:** Checking the picture
