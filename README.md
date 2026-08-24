# Reliability of the Incremental Cost-Effectiveness Ratio (ICER)

> **Note:** `icer_reliability_bootstrap_simulation.py` was originally written and run as a Google Colab notebook, then exported to a plain `.py` file for this repo. Because of that, some code may behave unexpectedly or throw an error if run outside Colab (e.g. file upload steps, missing runtime state). For the full, working experience — including outputs and plots — please follow the notebook link below.
>
> 🔗 [Open the original Colab notebook](https://colab.research.google.com/drive/1wGhpWslDC7Np6D07TZ_cePLIXlIoJwg8)

## What this is

A coursework assignment quantifying the cost-effectiveness of a cancer treatment trial, and — more importantly — how *reliable* that single-number estimate actually is. Based on a randomized trial (409 patients) comparing standard chemotherapy vs. standard chemotherapy plus osimertinib, on 1-year survival and total health-care costs.

## What I did

- **Point estimate**: calculated the event (survival) proportions and mean costs per treatment arm, and computed the Incremental Cost-Effectiveness Ratio (ICER = cost difference / effect difference).
- **Delta-method confidence interval**: derived an asymptotic 95% confidence interval for the ICER analytically, propagating variance through the ratio via a first-order Taylor expansion, including the covariance term between costs and outcome within each arm (rather than assuming independence).
- **Bootstrap confidence interval**: resampled the trial data to build an empirical distribution of the ICER, checked it for bias, and applied a bias-correction method. Visualized the bootstrap estimates of cost-difference vs. effect-difference on a cost-effectiveness plane, and quantified how many fell in each of the four quadrants (dominant, dominated, and the two ambiguous quadrants).
- **Parametric distribution fitting**: fit and compared several candidate distributions (normal, logistic, Weibull, gamma, lognormal) to the cost data in each treatment arm, using QQ-plots to assess fit.
- **Monte Carlo simulation**: simulated 1,000 trials of the same size by drawing costs from the fitted distributions and events from binomial distributions, recomputing the ICER each time, and compared this simulated sampling distribution against the bootstrap distribution (center, spread, and shape).

## Key finding

The bootstrap and simulated ICER distributions had similar central estimates but the simulation showed a noticeably wider spread: suggesting the fitted parametric distributions (lognormal for costs) don't fully capture the tail behavior of the real cost data, and that the non-parametric bootstrap is likely the more trustworthy reliability estimate here.

## Tools

Python · pandas · numpy · scipy · statsmodels · matplotlib · seaborn

## Notes

This was a coursework exercise for a biostatistics / health economics module, not a production project. It's shared here to demonstrate comparing multiple approaches to quantifying uncertainty (analytical, bootstrap, and simulation) for a ratio estimator, rather than reporting a single point estimate without any sense of its reliability.
