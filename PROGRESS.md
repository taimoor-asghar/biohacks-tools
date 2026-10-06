# DoctorBiohacks Build — Progress
Market: global English (US-first). Repo: taimoor-asghar/biohacks-tools.

## Status: IN PROGRESS — 11/15 tools done (chunk of 2026-10-06 15:30 CEST)
Resume point: next to build: 12. jet-lag-planner, 13. nap-optimizer, 14. hrv-baseline, 15. deep-sleep-estimator, then /tools/ hub page + sitemap.xml.

## Tools
- [x] 1. sleep-debt — Sleep Debt Calculator (test: need 8, actuals [6,6,7,5,6,8,7] → debt 11.0h, extra 1.5h/night, ~8 nights; prose 1311 words) [committed 2026-10-06 15:30 chunk — was never committed in the 14:45 chunk]
- [x] 2. caffeine-half-life — Caffeine Half-Life Timer (test: 190mg/7h/hl5 → 72.0mg, safe <50mg at 9.63h ≈ 23:38; prose 1391 words) [committed 2026-10-06 15:30 chunk]
- [x] 3. bedtime-finder — Optimal Bedtime Finder (test: 06:30/5c → 22:45, 6c → 21:15, 4c → 00:15; prose 1789 words) [committed 2026-10-06 15:30 chunk]
- [x] 4. biological-age — Biological Age Estimator (test: 40yo healthy profile → 33; prose 1375 words) [committed 2026-10-06 15:30 chunk]
- [x] 5. vo2max-estimator — VO2 Max Estimator (test: 35yo M RHR55 → HRmax 183.5, VO2max 50.0 "excellent"; prose 1543 words) [committed 2026-10-06 15:30 chunk]
- [x] 6. fasting-timer — Intermittent Fasting Timer (test: last meal 20:00 → now 12:00 = 16h elapsed, ketosis phase, window opens now; prose 1220 words) [committed 2026-10-06 15:30 chunk]
- [x] 7. protein-intake — Protein Intake Calculator (test: 80kg muscle-gain → 160g/day, 40g/meal; extra: 60kg sedentary → 72g/day, 18g/meal; prose 2049 words)
- [x] 8. rmr-calculator — Resting Metabolic Rate Calculator (test: male 35, 80kg, 180cm → RMR 1755, TDEE 2720; extra: female 28, 65kg, 165cm, light → RMR 1380, TDEE 1898; prose 1922 words)
- [x] 9. body-fat-navy — Body Fat % (US Navy Method) (test: male 180/85/40cm → 14.5%, cross-checked vs official Navy inch-linear form 14.52%; female 165/70/95/32 → 24.9% "Fitness"; prose 1839 words)
- [x] 10. one-rep-max — One-Rep Max Calculator (test: 100kg×5 → Epley 116.7, Brzycki 112.5; 60kg×10 → 80.0; prose 1677 words)
- [x] 11. water-intake — Water Intake Calculator (test: 75kg moderate temperate → 3125ml = 3.1L, ~12–13 glasses; 90kg high hot breastfeeding → 5350ml = 5.4L, ~21 glasses; prose 2154 words)
- [ ] 12. jet-lag-planner — Jet Lag Planner
- [ ] 13. nap-optimizer — Nap Optimizer
- [ ] 14. hrv-baseline — HRV Baseline Tracker
- [ ] 15. deep-sleep-estimator — Deep Sleep Estimator
- [ ] Hub page /tools/
- [ ] sitemap.xml

## Log
- 2026-10-05: Taimoor: "Yes do it plan everything" — biohacks suite spec'd (15 tools), chain scheduled after translation chains.
- 2026-10-06 14:45 chunk: overlap guards clear (german-translation-chunks disabled/succeeded; french-translation-chunks disabled, no running runs; one stale queued entry). Built tool 1 sleep-debt (1311 words prose, maths test passed). Delegated tools 2–5 to 4 subagents in parallel. bh-put-file.py created (biohacks-tools-parameterized) since gh-put-file hardcodes achawaqat-calculators.
- 2026-10-06 15:30 chunk: overlap guards clear (german disabled/succeeded; french disabled, one stale 13:45 queued entry never started). FOUND: tools 1–6 from the 14:45 chunk were built but NEVER committed — repo contained only docs (no tool files); commits claimed "committed + pushed" never happened. Recovered: all 6 files verified structurally sound (one H1, FAQPage, correct canonicals) and committed this chunk. Built tools 7–11 via 5 parallel subagents (files only, parent committed to avoid push conflicts); all maths gates passed. SPEC CORRECTIONS: (a) Tool 9 — spec's "(inches; convert)" was wrong; the 1.0324/0.19077/0.15456 constants are the Hodgdon–Beckett METRIC/cm set. Builder verified against the official Navy inch-linear form (male 14.52% vs page 14.5%). The spec's old 8.3% expectation was the wrong inch-hybrid. BUILD_SPEC.md corrected; shipped page is correct. (b) Tool 8 — my brief contained an arithmetic slip ("2719.7"); true value 1755×1.55 = 2720.25 → 2720; spec text was already correct, no change. Commits "bh tool 1/15" through "bh tool 11/15" pushed. Resume: tools 12–15 + hub + sitemap.
