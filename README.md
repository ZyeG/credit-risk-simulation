# Tail-Risk Estimation for Two 100-Bond Portfolios  
*(Credit-State Migration Model – Monte-Carlo Study)*

---

## Scenario Setup

| Scenario | Paths | Construction | Loss Distribution |
|----------|-------|--------------|-------------------|
| **MC1**  | 5 000 | 1 000 systemic × 5 idiosyncratic draws | Non-normal |
| **MC2**  | 5 000 | 5 000 systemic × 1 idiosyncratic draw | Non-normal |
| **OUT**  | 10 000 | 10 000 systemic × 1 idiosyncratic draw | Non-normal *(benchmark / “true”)* |
| **N₀ (No)** | 5 × 1 000 | Same as MC1 but **normal** loss generator | Normal |
| **N₁** | 5 000 | Same size as MC2, normal | Normal |
| **N₂** | 10 000 | Same size as OUT, normal | Normal |

- **Instrument data**: `instrum_data.csv` (driver, β, recovery, migration probs & exposures).  
- **Driver correlations**: `credit_driver_corr.csv` (used for Cholesky shocks).

### Portfolios
1. **Portfolio 1** – one unit in each of 100 bonds.  
2. **Portfolio 2** – equal dollar value in each bond.

---

## Tasks

1. **Sampling error**  
   Compare VaR & CVaR (99 % and 99.9 %) of `MC1` vs. `OUT` and `MC2` vs. `OUT`.

2. **Model error**  
   Replace each non-normal generator with a Gaussian fit (N₀, N₁, N₂).  
   Compare VaR & CVaR of each **normal** run vs. `OUT`.

---

## Numerical Results (USD)

| Portfolio 1 | VaR₉₉ | CVaR₉₉ | VaR₉₉․₉ | CVaR₉₉․₉ |
|-------------|-------|--------|---------|----------|
| **OUT** | 37 319 329 | 44 771 038 | 53 666 664 | 59 629 799 |
| MC1      | 37 312 228 | 44 052 010 | 54 245 958 | 50 150 230 |
| MC2      | 37 021 022 | 43 675 988 | 53 603 777 | 50 102 162 |
| N₀       | 26 223 851 | 29 112 906 | 32 736 461 | 35 096 853 |
| N₁       | 26 261 723 | 29 159 081 | 32 793 048 | 35 160 223 |
| N₂       | 26 148 477 | 29 032 176 | 32 649 013 | 35 005 028 |

| Portfolio 2 | VaR₉₉ | CVaR₉₉ | VaR₉₉․₉ | CVaR₉₉․₉ |
|-------------|-------|--------|---------|----------|
| **OUT** | 27 539 970 | 33 553 301 | 41 139 937 | 46 182 956 |
| MC1      | 27 420 303 | 33 082 724 | 41 461 345 | 39 141 760 |
| MC2      | 27 326 047 | 32 873 720 | 41 227 565 | 39 039 430 |
| N₀       | 21 179 147 | 23 349 885 | 26 072 501 | 27 846 020 |
| N₁       | 21 133 038 | 23 301 791 | 26 021 918 | 27 793 815 |
| N₂       | 21 084 626 | 23 248 884 | 25 963 372 | 27 731 596 |

See `report.pdf` for plots
---

## Findings

### Sampling Error (MC vs. OUT)
* Both MC1 and MC2 **under-estimate extreme losses**, especially CVaR at 99.9 %.  
* MC2 shows slightly smaller bias than MC1 → more systemic draws (5 000 vs. 1 000) help.

### Model Error (Normal vs. OUT)
* All normal runs produce **negative deltas**: Gaussian tails are too light.  
* Under-estimation is larger for CVaR than VaR and grows at 99.9 % confidence.

---

## Capital-Adequacy Implications
Banks using MC1/MC2 figures would carry **significantly less capital** than required by the OUT benchmark—critical under Basel III, which bases capital on tail metrics (often CVaR at 99.9 %).

---

## Mitigation Techniques
1. **Increase scenario size** (≥ 100 000 paths).  
2. **Retain non-normal loss generators**; avoid normality.  
3. Use **hybrid** models: historical + Monte-Carlo, empirical copulas, or variance-reduction sampling.

