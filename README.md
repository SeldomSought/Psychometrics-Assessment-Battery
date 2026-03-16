# Psychometrics Assessment Battery

A research-grade, open-source psychometric assessment battery built from scratch. Novel, non-copyrighted items. Runs entirely in the browser — no data transmitted, no accounts.

## Live Assessment

→ [seldomsought.com/projects/psychometrics-battery](https://seldomsought.github.io/projects/psychometrics-battery/index.html)

## What's in this repo

| Path | Contents |
|---|---|
| `data/hexaco-short-form.json` | 96-item HEXACO short-form (4 items × 24 facets × 6 domains) |
| `data/fc-blocks.json` | 100 forced-choice triplet blocks for Thurstonian IRT scoring |
| `data/blueprint.json` | Full assessment blueprint (all modules, score inventory, branching rules) |
| `docs/analysis-plan.md` | Psychometric analysis plan (EFA/CFA, IRT, DIF, CAT design) |
| `docs/report-templates.md` | Interpretive report templates (user + professional versions) |
| `docs/scoring-guide.md` | Scoring methodology and normative conversion |

## Assessment Modules

### Module 1 — HEXACO Personality Profile (96 items)
Six-factor personality model: **H**onesty-Humility, **E**motionality, e**X**traversion, **A**greeableness, **C**onscientiousness, **O**penness. Four facets per domain, four items per facet. 5-point Likert scale (Strongly Disagree → Strongly Agree). ~50% reverse-keyed.

### Module 2 — Forced-Choice Blocks (100 blocks)
Rank-order triplets for Thurstonian IRT scoring. 10 domain combinations × 10 blocks each. Rank-ABC response suppresses acquiescence and social desirability bias that Likert items cannot detect. FC score weighted at 30% of composite domain score.

### Planned modules (data files included, UI pending)
- **Situational Judgment Test** — 60 scenarios across 5 constructs (teamwork, leadership, self-regulation, integrity, empathy)
- **Cognitive Aptitude Battery** — 7 domains (Gf, Gc, WM, PS, VC, QR, SA), 14 task types
- **Schwartz 19 Values** — circumplex values ranking
- **RIASEC Interests** — Holland occupational interest types

## Scoring

**Likert composite:**
- Items reverse-scored where `keying == "reverse"`: `score = 6 - raw`
- Facet mean = mean of 4 items
- Domain mean = mean of 4 facet means
- T-score: `T = 50 + 10 × ((mean - 3.0) / 0.75)`
- Percentile: Φ(z) where `z = (mean - 3.0) / 0.75`

**FC composite (Thurstonian-lite):**
- Rank 1 = +2 pts, Rank 2 = +1 pt, Rank 3 = 0 pts
- Domain FC score = mean points per domain appearance, normalized to 1–5 scale
- Final composite: 70% Likert + 30% FC

**Score bands:**
| Band | Percentile |
|---|---|
| Exceptionally Low | ≤ 7th |
| Very Low | 8–16th |
| Low Average | 17–29th |
| Average | 30–70th |
| High Average | 71–83rd |
| High | 84–92nd |
| Exceptionally High | ≥ 93rd |

## Item design principles

- Novel items — no copyrighted or licensed content
- 6th–8th grade reading level
- ~50% reverse-keyed per facet to suppress acquiescence
- Social desirability–matched within FC blocks (empirical calibration pending)
- Bias risk documented in full item metadata (`data/` JSON files)

## Psychometric roadmap

1. **Pilot data collection** (n ≥ 300) for internal structure analysis
2. **EFA/CFA** — confirm six-factor HEXACO structure
3. **IRT calibration** — GRM for Likert items, Thurstonian IRT for FC blocks
4. **DIF analysis** — demographic group invariance
5. **CAT implementation** — EAP estimation, max-information item selection, Sympson-Hetter exposure control
6. **Normative sample** — n ≥ 1,000 stratified by age/gender/education

See `docs/analysis-plan.md` for full methodology.

## Model reference

Lee, K., & Ashton, M. C. (2004). Psychometric properties of the HEXACO Personality Inventory. *Multivariate Behavioral Research, 39*(2), 329–358.

Ashton, M. C., & Lee, K. (2007). Empirical, theoretical, and practical advantages of the HEXACO model of personality structure. *Personality and Social Psychology Review, 11*(2), 150–166.

Brown, A., & Maydeu-Olivares, A. (2011). Item response modeling of forced-choice questionnaires. *Educational and Psychological Measurement, 71*(3), 460–502.

## License

Item content and methodology: MIT License. See `LICENSE`.
