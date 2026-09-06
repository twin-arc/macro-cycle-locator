# macro-cycle-locator

> An opinionated macro-cycle positioning skill for WorkBuddy that combines a six-dimension scorecard, ETF fund-flow calibration, and a three-layer transmission chain to locate the current macro stage (recession → recovery → overheating → stagflation) and rate individual sectors and stocks against that stage.

## What problem this solves

Macro frameworks for stock-market timing — cyclical rotation, the four-season clock, the
meridian clock — are everywhere, but **none of them tell you "where are we *right now"** in
defensible, reproducible terms. Most failures trace to two causes:

1. Treating the framework as qualitative narrative instead of measurable signals.
2. Jumping from macro conclusion to individual stock calls without checking the sector fit.

This skill pins the framework to:

- **Six measurable dimensions** of the macro state, each with explicit data sources and thresholds.
- **ETF fund-flow calibration** for high-frequency verification (daily vs. monthly macro data).
- **A three-layer transmission chain** that explicitly delimits where macro reasoning is allowed
  to operate — and where it must hand over to fundamentals.

## How it works

### Layer 1 — Macro positioning
A six-dimension scorecard:

| Dimension | What it measures |
|---|---|
| Growth momentum | PMI, fixed-asset investment, retail, property, exports, high-tech PMI |
| Inflation structure | PPI, CPI, PPI−CPI spread, PMI input vs. output prices |
| China liquidity | 10Y/1Y CGB yields, DR007, LPR, MLF |
| External liquidity | Fed funds rate, FOMC probabilities, US 10Y/30Y yields, PCE, China−US 10Y spread |
| Credit transmission | M1, M2, M1−M2 spread, social financing stock growth |
| Market pricing | Index level, PE-TTM and percentile, PB and percentile, turnover, sector concentration |

**Hard switch-confirmation signals** (see `references/scorecard.md`) — for example, the most
inflexible one is M1−M2 turning positive. Until that happens, no upgrade to Stage 2 is allowed.

**Noise-exclusion rule (the most important step):** when upstream commodities rally, the
default reaction is to call it Stage 3 overheating. The skill forces a four-criterion test
for supply-type inflation first — the most sensitive probe being whether midstream processors
are profitable alongside upstream.

### Layer 2 — Sector adaptation
Once the stage is fixed, the skill maps each sector (upstream cyclical / midstream processing
/ consumer staples / growth tech / pharma / dividend) to a fit grade: *hold / watch / avoid /
left-side opportunity*. The **first question** for any cyclical stock is *does this company
sell the resource, or buy it?* — the same macro fact produces opposite conclusions on
opposite sides of the value chain.

### Layer 3 — Stock verification
Macro reasoning stops at Layer 2. Individual stocks require fundamental verification:
earnings reports, cash flow, margins, sector-specific metrics. A stock-level checklist
is provided by asset type.

### ETF calibration
ETF fund flows run daily, macro data runs monthly. When they disagree, **the ETF signal
wins** — money is more honest than models. The core tool is the price-volume divergence
four-quadrant matrix.

## Project structure

```
macro-cycle-locator/
├── SKILL.md                          # Main workflow and rules
├── references/
│   ├── scorecard.md                  # Six-dimension scorecard, switch signals, noise exclusion
│   ├── sector-map.md                 # Three-layer chain, sector × stage matrix
│   ├── stock-checklist.md            # Layer-3 stock verification by asset type
│   ├── etf-calibrator.md             # ETF fund-flow calibration, divergence matrix
│   └── pitfalls.md                   # Ten known traps and pre-output checklist
├── assets/
│   └── report_template.html          # Light-theme, mobile-friendly single-file report template
├── dist/
│   └── macro-cycle-locator.zip       # Packaged distributable
├── README.md
├── LICENSE
└── .gitignore
```

## Installation

### Option A — As a WorkBuddy skill (recommended)

Copy or clone this repository into your WorkBuddy skills directory:

```bash
# User-level (all projects)
git clone https://github.com/yeqian1989-creator/macro-cycle-locator \
    ~/.workbuddy/skills/macro-cycle-locator
```

WorkBuddy will auto-discover the skill on next session start. No restart required for
already-running sessions.

### Option B — Load a specific release zip

1. Download `dist/macro-cycle-locator.zip` from the latest release.
2. Extract into `~/.workbuddy/skills/` so the resulting `SKILL.md` sits at
   `~/.workbuddy/skills/macro-cycle-locator/SKILL.md`.
3. Restart WorkBuddy (or trigger skill re-scan).

## Usage examples

Once installed, the skill triggers automatically on natural-language queries:

- "What stage are we in right now?"
- "Locate this stock — how is its sector positioned in the current cycle?"
- "Can I still buy dividend names at this stage?"
- "Is the upstream rally real overheating or a supply shock?"
- "Help me check 东方钽业 000962 against the current cycle."

## Honesty and known limits

The skill explicitly publishes its failure modes in `references/pitfalls.md`:

1. **Macro conclusions cannot directly pick stocks.** Stop at Layer 2.
2. **Supply-type inflation is mistaken for Stage 3** unless midstream profitability is checked.
3. **Stage upgrades need hard confirmation**, not price action alone.
4. **US−China cycle divergence** must be handled as an independent dimension — A-share
   liquidity ≠ Hong Kong / China-concept liquidity.
5. **Industry cycles can decouple from macro cycles.** When high-tech PMI diverges from total
   PMI, industry data explains more.

## License

MIT — see `LICENSE`.
