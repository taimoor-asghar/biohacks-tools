# DoctorBiohacks Build Spec — 15 tools
Target site: https://doctorbiohacks.com/ | Market: global English (US-first) | Created 2026-10-05

## Quality bar (non-negotiable)
- Single static HTML file per tool, vanilla JS + inline CSS, no external libs except Google Fonts.
- Maths verified against hand-computed known answers before ship. Record test cases in PROGRESS.md.
- 1200+ words of substantive guide prose per page + FAQPage schema. Biohacking content must stay honest: no miracle claims, caveats where evidence is thin, "talk to your doctor" where medical.
- One H1, meta title/description, canonical https://doctorbiohacks.com/tools/<slug>/, OG tags, mobile-responsive, accessible labels.
- Author credit: Dr Taimoor Asghar, reviewed date.

## Design system — match the live site theme
Site runs **Azure Newspaper** (child of Azure News), same family as Azure Blogger:
- Primary/accent: **#04a8d0**, body **"Nunito", sans-serif**, headings **"Arvo", serif** (Google Fonts).
- Text #353535 / muted #737373. Cards white on #f7f8f9, border #e1e1e1, radius ~4px.
- Buttons solid #04a8d0 white text. Result panel: #e8f7fc tint with #04a8d0 left border, big Arvo figure.

## URL structure
- Hub: https://doctorbiohacks.com/tools/
- Tools: https://doctorbiohacks.com/tools/<slug>/

## Tool 1 — Sleep Debt Calculator — slug: sleep-debt
Inputs: sleep hours for last 7 nights (or nightly average), sleep need (default 8, age-adjusted hint).
Maths: debt = Σ(need − actual, floored at 0 per night... use signed, cap nightly catch-up credit at +1h). Output: total debt hours, recovery plan (add min(debt/7, 1.5)h per night), estimated nights to recover, warning if debt > 20h (see a doctor note).
Test: need 8, actuals [6,6,7,5,6,8,7] → debt = 2+2+1+3+2+0+1 = 11h. Recovery ≈ 11 nights at +1h.

## Tool 2 — Caffeine Half-Life Timer — slug: caffeine-half-life
Inputs: dose mg (default 95/cup, presets: espresso 63, brewed 95, energy drink 160), time consumed, half-life h (default 5, range 3–7 slider).
Maths: remaining = dose × 0.5^(elapsed_halflives). Sleep-safe threshold 50mg: solve t for remaining=50.
Output: mg in system now, time it drops below 50mg, personal "caffeine curfew".
Test: 190mg at 14:00, half-life 5h, now 21:00 (7h elapsed) → 190 × 0.5^1.4 = 190 × 0.379 = 72mg. Below 50mg at t: 0.5^(t/5)=50/190 → t = 5 × log(0.263)/log(0.5) = 5 × 1.926 = 9.6h → ~23:36.

## Tool 3 — Optimal Bedtime Finder — slug: bedtime-finder
Inputs: wake-up time, cycles wanted (4/5/6 × 90 min), fall-asleep minutes (default 15).
Maths: bedtime = wake − (cycles × 90 + fall_asleep) min. Show 3 options (4, 5, 6 cycles).
Test: wake 06:30, 5 cycles → 06:30 − 465 min = 22:45.

## Tool 4 — Biological Age Estimator — slug: biological-age
Questionnaire (10 items): exercise days/wk, smoking, sleep hours, fruit/veg servings, resting HR, waist vs height, alcohol, stress, processed food, strength training.
Scoring: start at chronological age; modifiers −2..+3 per answer (document weights in code). Output: estimated biological age, delta, top 3 levers. Heavy caveat: estimate only, not medical.
Test: 40yo, exercises 5x, non-smoker, sleeps 8, RHR 55, WHtR 0.45 → expect ~34–36.

## Tool 5 — VO2 Max Estimator — slug: vo2max-estimator
Inputs: age, sex, resting HR (morning, bpm).
Maths (Uth–Sørensen–Overgaard): HRmax = 208 − 0.7 × age; VO2max = 15 × HRmax / HRrest. Rating vs age/sex norms (poor…superior table).
Test: 35yo male, RHR 55 → HRmax = 183.5; VO2max = 15 × 183.5/55 = 50.0 → "excellent".

## Tool 6 — Intermittent Fasting Timer — slug: fasting-timer
Inputs: protocol (16:8, 18:6, 20:4, OMAD), last meal time.
Maths: elapsed → phase: 0–4h fed, 4–12h post-absorptive, 12–16h fat-burning ramp, 16h+ ketosis estimates (labelled approximate). Output: current phase, time to next phase, eating window start, what breaks a fast (<50 kcal note).
Test: last meal 20:00, now 12:00 next day (16h) → fasting 16h, ketosis phase, window opens now (16:8).

## Tool 7 — Protein Intake Calculator — slug: protein-intake
Inputs: weight kg, goal (sedentary 1.2, active 1.6, muscle gain 2.0, cutting 2.2 g/kg — note: above RDA, cite ISSN position stand).
Maths: daily_g = weight × factor; per-meal = daily/4 (4 meals). Output grams + example foods.
Test: 80kg, muscle gain → 160g/day, 40g/meal.

## Tool 8 — Resting Metabolic Rate — slug: rmr-calculator
Inputs: sex, age, weight kg, height cm, activity (sedentary 1.2 … very active 1.9).
Maths (Mifflin-St Jeor): male 10w + 6.25h − 5a + 5; female −161. TDEE = RMR × factor. Cutting/bulking targets ±20%.
Test: male 35, 80kg, 180cm → 10×80+6.25×180−175+5 = 800+1125−175+5 = 1755 kcal. TDEE moderate (1.55) = 2720.

## Tool 9 — Body Fat % (US Navy) — slug: body-fat-navy
Inputs: sex, height cm, neck cm, waist cm, hip cm (female).
Maths: male: 495/(1.0324 − 0.19077×log10(waist−neck) + 0.15456×log10(height)) − 450 (inches; convert). Female adds hip term. Output % + category table. Caveat: ±3% accuracy.
Test: male, 180cm/70.9in, waist 85cm/33.5in, neck 40cm/15.7in → 495/(1.0324 − 0.19077×log10(17.8) + 0.15456×log10(70.9)) − 450 = 495/(1.0324−0.2386+0.2863)−450 = 495/1.0801−450 = 458.3−450 = 8.3%... let me not hand-verify precisely; worker must compute and sanity-check against known Navy examples (this input ≈ 15-18% typically — worker to verify with a reference calculator and record).

## Tool 10 — One-Rep Max Calculator — slug: one-rep-max
Inputs: weight lifted, reps (1–12).
Maths (Epley): 1RM = w × (1 + reps/30). Output 1RM + % table (90/80/70/60/50%).
Test: 100kg × 5 → 100 × 1.1667 = 116.7kg.

## Tool 11 — Water Intake Calculator — slug: water-intake
Inputs: weight kg, activity (low/mod/high), climate (temperate/hot), pregnancy/breastfeeding toggle (adds 300/700ml, advises doctor).
Maths: base = weight × 35ml; +500ml moderate, +1000ml high; +500ml hot. Output L/day + glasses (250ml).
Test: 75kg, moderate, temperate → 2625 + 500 = 3125ml ≈ 3.1L, ~12 glasses.

## Tool 12 — Jet Lag Planner — slug: jet-lag-planner
Inputs: home UTC offset, destination UTC offset, departure date, direction auto.
Maths: shift = dest − home (hours). Plan: shift sleep 1h/day toward destination starting |shift| days before (cap 3 days pre-shift advised), light exposure timing (eastward: morning light; westward: evening light), melatonin 0.5–3mg note with doctor caveat.
Test: Copenhagen (+1) → New York (−5): shift −6h (westward). 3-day pre-plan shifting bedtime +1h/day... westward = delay sleep: bedtime moves later 1h/day for 3 days + evening light.

## Tool 13 — Nap Optimizer — slug: nap-optimizer
Inputs: minutes available, goal (alertness → 20 min; memory/creativity → 90 min full cycle), current time.
Maths: wake time = now + nap + 5 min fall-asleep. Warn if 90-min nap after 15:00 (night sleep impact).
Test: 14:00, 20 min, alertness → wake 14:25.

## Tool 14 — HRV Baseline Tracker — slug: hrv-baseline
Inputs: 7 morning HRV readings (rMSSD ms).
Maths: baseline = mean; SD; today vs baseline: within ±1 SD = normal, below −1 SD = "take it easy", above +1 SD = "primed". Output: baseline, 7-day chart (CSS bars), what moves HRV (sleep, alcohol, illness, overtraining) — educational.
Test: [62,65,60,64,61,63,40] → mean 59.3, SD ≈ 8.1; today 40 → −2.4 SD → "take it easy, possible illness/overtraining".

## Tool 15 — Deep Sleep Estimator — slug: deep-sleep-estimator
Inputs: age, total sleep hours, exercise (y/n), alcohol evenings/wk, caffeine after 14:00 (y/n), screens in bed (y/n).
Maths: base deep% by age (20s 20%, 30s 18%, 40s 16%, 50s 14%, 60+ 12%); modifiers: exercise +2, alcohol −3 (if ≥3/wk), late caffeine −2, screens −1. Output: estimated deep sleep min/night vs norm, top 3 levers. Caveat: estimate; wearables measure this properly.
Test: 35yo, 7.5h sleep, exercises, no alcohol, no late caffeine, screens yes → 18+2−1 = 19% → 86 min. Norm ~81 min → "above average".

## Hub page — slug: tools (path /tools/)
Card grid of 15 tools, category filters (Sleep, Nutrition, Fitness, Recovery), live search. Azure Newspaper styling.

## Repo
taimoor-asghar/biohacks-tools (to be created). Structure: tools/<slug>.html, PROGRESS.md, sitemap.xml on completion.

## Deployment
Static HTML; Taimoor uploads to doctorbiohacks.com himself (same division of labour as greenretrofit).
