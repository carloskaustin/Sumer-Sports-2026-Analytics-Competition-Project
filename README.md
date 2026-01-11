# Sumer-Sports-2026-Analytics-Competition-Project

# NCAA Transfer Portal Effects on NFL Opportunity and Production

This project analyzes how college football players who interacted with the NCAA transfer portal performed in the NFL relative to players who did not transfer. Specifically, it examines **early NFL opportunity** (rookie snap counts) and **rookie production** (position-specific production scores), and evaluates whether **college résumé + transfer history** help explain differences in early professional outcomes.

---

## Project Motivation

The NCAA transfer portal has reshaped college football career paths, allowing athletes to move between programs more freely than ever before. As collegiate careers increasingly span multiple programs, coaches, schemes, and competitive environments, questions emerge about how these varied developmental paths shape readiness for the NFL.

NFL draft evaluation is an extensive process that examines every aspect of a player’s collegiate career and personal background. Transfer history adds an additional layer of context to a player’s story, raising questions about development, adaptability, and how college movement translates to opportunity and performance at the next level.

This project investigates whether transfer history is associated with differences in:
- Draft likelihood
- Early NFL playing time
- Rookie-year on-field production

---

## Research Questions

1. **College production:** How does college production differ between transfer and non-transfer players?  
2. **Drafting & opportunity:** Are transfers drafted at different rates than non-transfers, and do they receive different levels of early NFL opportunity (rookie snaps)?  
3. **Rookie production:** Conditional on opportunity, do transfer players produce more or less than non-transfer players in their rookie NFL season?

---

## Data

This project uses two primary datasets:

- **College seasonal statistics (player-season level):** Multiple rows per player, one for each collegiate season.
- **NFL rookie statistics (player level):** One row per player representing rookie-year outcomes.

College seasons were aggregated into **player-level career features**, then merged with NFL rookie outcomes.

Analyses are conducted **by position group** to account for role differences and position-specific production metrics.

---

## Position Groups Analyzed

- Quarterbacks (QB) *(exploratory only — small drafted sample)*
- Defensive Backs / Safeties (DB)
- Defensive Line (DL)
- Wide Receivers / Tight Ends (WR/TE)
- Running Backs / Fullbacks (RB/FB)

---

## Production Score Construction

To compare player performance across seasons and positions, **custom production scores** were constructed for both college and NFL data. Because each position contributes differently on the field, production scores were calculated **separately by position group**, using key statistics relevant to each role. This allows performance to be summarized into a single continuous metric while preserving positional context.

The guiding principle was to reward **impactful plays** (yards gained, touchdowns, sacks, pressures, interceptions, coverage efficiency) while maintaining consistency across datasets.

### Offensive Positions

**Quarterbacks (QB)**  
Production combines passing yards, rushing yards, total touchdowns, and penalties for interceptions to reflect total offensive contribution.

**Running Backs / Fullbacks (RB/FB)**  
Production incorporates rushing yards, receiving yards, and total touchdowns to capture all-purpose offensive output.

**Wide Receivers / Tight Ends (WR/TE)**  
Production uses receiving yards and receiving touchdowns to measure pass-catching impact.

### Defensive Front Seven

**Defensive Line (DL)**  
Production combines tackles, quarterback pressures (as a proxy for sacks where sack data was unavailable), and interceptions to reflect disruption and playmaking.

**Linebackers (LB)**  
Production incorporates tackles, pressures, interceptions, and coverage involvement to capture both run defense and pass coverage responsibilities.

### Defensive Backs / Safeties (DB)

Defensive back production emphasizes **coverage efficiency** and playmaking, combining:
- Tackles  
- Interceptions  
- Pass breakups  
- Coverage workload (targets faced)  
- Yards allowed in coverage (penalized to reward efficiency)

This captures both activity level and effectiveness in pass defense.

### College vs NFL Scores

- **College production scores** were built from NCAA seasonal statistics.
- **NFL rookie production scores** were constructed using available rookie-year NFL statistics.
- Exact inputs differ slightly between datasets due to data availability, but the conceptual framework remains consistent.

### Purpose of the Production Scores

These scores are not intended to replicate fantasy or scouting grades. Instead, they provide:
- A consistent way to summarize on-field impact
- A method to compare players within the same position group
- Inputs for modeling opportunity and efficiency at the NFL level

---

## Feature Engineering

### Transfer Features
- `any_transfer`: Indicator for whether a player transferred at least once during college

### College Production Features
- `final_season_production`: Production score in final collegiate season  
- `career_production`: Total production score across all college seasons  
- `production_growth_slope`: Year-to-year trend in production (positive = improvement, negative = decline)

### School Context Features
- `final_school_tier`: Competitive tier of final college program (Tier 1 = most competitive, Tier 3 = least competitive)
- `net_tier_change`: Change from initial school tier to final school tier

---

## Target Variables (NFL Rookie Outcomes)

### Opportunity
- `rookie_snaps`: Total snaps played during rookie season

### Rookie Production
- `rookie_production`: Position-specific rookie production score constructed from NFL rookie statistics

---

## Methodology

### Exploratory Analysis
Exploratory analysis was conducted by position group to examine collegiate and NFL trends and how patterns differ between transfer and non-transfer players.

### Regression Models
Linear regression models were used to assess whether college résumé characteristics and transfer history are associated with:
- Early NFL opportunity (rookie snaps)
- Rookie-year production (conditional on opportunity)

These models evaluated whether reframing outcomes as threshold-based classifications improved predictability.

---

## Key Findings

### Exploratory Trends
- College production profiles are largely similar between transfer and non-transfer players across positions.
- Non-transfer players are drafted at slightly higher rates and often receive greater early NFL opportunity, especially at DB and DL.
- Once playing time is earned, transfer players generally match or exceed non-transfer production efficiency.
- Among defensive backs, transfer players allowed fewer yards per target despite receiving fewer snaps.

### Modeling Results
- Early NFL opportunity (snaps) is difficult to predict across positions, reflecting the influence of depth charts, coaching decisions, scheme fit, and injuries.
- Rookie production is more predictable once playing time is accounted for, particularly for WR/TE and DL groups.
- Transfer status primarily correlates with **early opportunity**, not **on-field efficiency** once players see the field.
- Classification models showed limited ability to predict which individual players would become high-opportunity or high-production rookies.

### Core Insight
College résumé data explains **group-level tendencies**, but has limited power in predicting **individual NFL outcomes**.

---

## Repository Structure
- README.md
Project overview, research questions, methodology, and key findings

- Sumer_Analytics_Competition.ipynb
Complete data cleaning, feature engineering, exploratory analysis, and modeling workflow

- Exploratory_Findings.md
Written summaries of exploratory analysis by position group

- Opportunity and Production Model Findings.md
Written summaries of regression and classification model results

- Sumer 2026 Analytics Competition Presentatiom
Final Sumer 2026 Analytics Competition presentation deck

