

## Scenario Sets

| Label | Size | Construction | Distribution |
|-------|------|--------------|--------------|
| **MC1** | 5 000 (N = 1 000 × 5) | 1 000 systemic sims × 5 idiosyncratic draws each | Non-normal |
| **MC2** | 5 000 (N = 5 000 × 1) | 5 000 systemic sims × 1 idiosyncratic draw | Non-normal |
| **OUT** | 100 000 | 100 000 systemic sims × 1 idiosyncratic draw | “True” distribution |
| **N0/N1/N2** | 1 000 × 5, 5 000, 100 000 | Same sizes as MC, **but** sampled from a fitted normal | Normal (model-error test) |

---

## Portfolios Evaluated
1. **Portfolio 1 (Unit Weights)** – one \$1 unit in each bond  
2. **Portfolio 2 (Equal \$ Value)** – equal dollar allocation across bonds

---

## Key Results (single experiment)

### Portfolio 1
| Data set | VaR 99 % | CVaR 99 % | VaR 99.9 % | CVaR 99.9 % |
|----------|---------:|----------:|-----------:|------------:|
| **OUT** | \$37.3 M | \$44.8 M | \$53.7 M | \$59.6 M |
| **MC1** | 37.3 M | 44.1 M | 54.2 M | 50.2 M |
| **MC2** | 37.0 M | 43.7 M | 53.6 M | 50.1 M |
| **Normal (N0/N1/N2)** | ≈ \$26 M | ≈ \$29 M | ≈ \$32 M | ≈ \$35 M |

### Portfolio 2
| Data set | VaR 99 % | CVaR 99 % | VaR 99.9 % | CVaR 99.9 % |
|----------|---------:|----------:|-----------:|------------:|
| **OUT** | \$27.5 M | \$33.6 M | \$41.1 M | \$46.2 M |
| **MC1** | 27.4 M | 33.1 M | 41.5 M | 39.1 M |
| **MC2** | 27.3 M | 32.9 M | 41.2 M | 39.0 M |
| **Normal (N0/N1/N2)** | ≈ \$21 M | ≈ \$23 M | ≈ \$26 M | ≈ \$28 M |

> Plots see in notebook.

---

## Findings

### Sampling Error  
*MC1* and *MC2* under-estimate extreme losses; MC2 (more systemic sims) performs slightly better.  
CVaR bias is larger than VaR, especially at 99.9 %.

### Model Error (Normal vs. Non-normal)  
Normal-assumed datasets significantly understate tail risk. Bias is strongest for CVaR at high confidence levels.

### Capital-Adequacy Impact  
Banks relying on MC1/MC2 could under-capitalize—critical at 99.9 % CVaR (Basel III).

### Mitigation Strategies  
- Increase scenario size (e.g., 100 000).  
- Retain non-normal structure.  
- Blend historical simulations with Monte Carlo; use variance-reduction.
