# Biomarq

A biomarker-first longevity tracker. Log your bloodwork and it turns it into an estimated biological age, specific suggestions for anything out of range, and honest research context on cardiometabolic, cardiovascular, cognitive, and cancer risk. Lifestyle and nutrition are tracked too, as supporting context, not the headline.

Live app: `https://YOUR_USERNAME.github.io/YOUR_REPO/`

## What it does

**Home page** — a landing page describing the app, with a "Get started" button that leads into sign-up/login.

**Guided flow** — instead of one long dashboard, the app walks you through a sequence: Profile → Biomarkers → Habits → Food journal → Results. Every step auto-saves as you move to the next one; there's no separate "Save" button to remember to click. Step numbers at the top are clickable shortcuts to jump to any page directly.

**Profile** — sex, age, weight, height, and a weight goal (maintain/lose/gain), which power your macro targets and biological age estimate.

**Biomarkers** — fasting glucose, HbA1c, fasting insulin, HDL/LDL, ApoB, Lp(a), triglycerides, CRP, homocysteine, Vitamin D, blood pressure, resting heart rate. Optional add-ons (collapsed by default, clearly marked as not required):
- Specialist tumor markers: PSA, CA-125, CEA, CA 19-9, AFP, and a multi-cancer early detection test result field
- Genetic testing & family history: APOE4 genotype, amyloid/tau blood test result, and family history of cancer, Alzheimer's, heart disease, and diabetes
- "Find a lab near me" and "Where can I get these tested?" buttons that use geolocation to open a nearby Google Maps search, with fallback links to Quest Diagnostics, Labcorp, Walk-In Lab, Galleri, and other credentialed directories
- "Upload labs" — reads a PDF or photo of a lab report and auto-fills matching fields. PDF text is extracted with position-aware row reconstruction (so tabular lab reports parse correctly); if a PDF has no real text layer, it falls back to OCR. Everything runs client-side, nothing is uploaded to a server. Always shown as a best-effort read, meant to be double-checked, not trusted blindly

**Habits** — sleep, exercise (minutes and type), and stress level.

**Food journal** — log meals with a USDA FoodData Central-backed food search that auto-fills calories and macros, scaled to serving size. Daily macro goals are computed from your profile (Mifflin-St Jeor BMR + activity multiplier from your logged exercise + AMDR ranges) and shown as progress bars.

**Results dashboard** — a single page with collapsible sections (only the most important ones open by default) so there's a lot of information without it all being on screen at once:
- Biological age estimate (rings showing biomarker score vs. lifestyle score)
- Quick-glance summary cards for profile, latest biomarkers, today's habits, and today's food — each fully clickable to jump straight to editing that step
- Recommended next steps — location-based referral suggestions (dietitian, personal trainer, sleep specialist, therapist, endocrinologist, cardiologist, genetic counselor) that only appear when your own logged data actually suggests one would help, each gated on a real, sustained pattern rather than a single day's reading
- Biomarker suggestions — specific, evidence-informed levers for each marker outside range
- Lifestyle notes — sleep, activity, stress, and macro balance
- Disease risk context — cardiometabolic, cardiovascular, cognitive, and cancer-risk associations from population-level research, with an explicit disclaimer that this is not a diagnostic tool
- Trend chart and recent entries history
- Sources & methodology — a plain-language breakdown of exactly where every number and reference range comes from

**Auth** — email/password sign-up and login, plus "Continue with Google."

## Tech stack

- Single-file HTML/CSS/JS, no build step, no framework
- [Supabase](https://supabase.com) for Postgres, authentication, and row-level security
- [Chart.js](https://www.chartjs.org/) for trend visualization
- [pdf.js](https://mozilla.github.io/pdf.js/) and [Tesseract.js](https://tesseract.projectnaught.com/) for client-side lab document parsing
- [USDA FoodData Central API](https://fdc.nal.usda.gov/) for nutrition lookups
- Fonts: Libre Baskerville (headings) and Sarala (body), via Google Fonts
- Hosted on GitHub Pages

## Methodology and sources

- **Biomarker reference ranges**: CDC, American Heart Association, and NCEP ATP III clinical guidelines
- **Specialist markers** (ApoB, Lp(a), homocysteine, Vitamin D, fasting insulin): commonly-cited ranges from cardiology/endocrinology literature, not a single official body's cutoffs
- **Biological age**: a simplified estimate based on biomarker score deviation from neutral, not a clinical epigenetic clock or an implementation of the Levine PhenoAge algorithm
- **Calorie/macro targets**: Mifflin-St Jeor BMR equation, standard PAL activity multipliers, AMDR ranges from the USDA Dietary Guidelines for Americans
- **Disease risk context**: general epidemiological associations (inflammation and cancer risk, insulin resistance and dementia risk, homocysteine and cognitive decline, hypertension and dementia), explicitly not diagnostic
- **Professional directories**: Quest Diagnostics, Labcorp, Walk-In Lab, Galleri/GRAIL, NSGC, C2N Diagnostics/PrecivityAD, EatRight.org, ACE Fitness, AASM, Psychology Today, CBDCE

This app is not a diagnostic tool and does not replace medical advice. Every section that touches disease risk, genetic testing, or clinical thresholds says so explicitly in the UI.

## Known limitations

- The biological age estimate and disease risk context are intentionally simplified and are labeled as such throughout the UI — they are not clinical-grade calculations
- Lab document parsing (PDF/OCR) accuracy varies by report format and image quality; it's a best-effort reader, not a guaranteed-accurate one
- No HIPAA compliance — this is a personal project, not built for use by a medical office with real patient data. See disclaimer below.

## Disclaimer

Biomarq is a personal portfolio project. It is not a medical device, does not provide diagnoses, and should not replace a conversation with a doctor, genetic counselor, or other qualified professional.
