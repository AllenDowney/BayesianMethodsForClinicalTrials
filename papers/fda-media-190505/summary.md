# Summary: FDA draft guidance — Use of Bayesian Methodology in Clinical Trials

**Full title:** *Use of Bayesian Methodology in Clinical Trials of Drug and Biological Products: Guidance for Industry*  
**Source:** [FDA media 190505](https://www.fda.gov/media/190505/download) (downloaded PDF in this folder as `document.pdf`)  
**Status:** **DRAFT** — nonbinding recommendations; distributed for public comment (not for implementation as-is).  
**Date on document:** January 2026  
**Agency:** FDA, CDER and CBER (Office of Biostatistics / Division of Biostatistics)

---

## What it is

The guidance explains how sponsors may use **Bayesian methods** in clinical trials submitted under INDs, NDAs, BLAs, and supplements. It covers adaptive timing/rules, design choices (e.g., dose selection), and—its main emphasis—**Bayesian methods for primary inference** on effectiveness and safety. It does not create legal rights; alternative approaches are allowed if they meet statutes and regulations.

---

## Core statistical concepts (as defined)

- **Prior:** Pre-study distribution over parameters.  
- **Likelihood:** Links parameters to the data via the chosen model.  
- **Posterior:** Updated distribution after seeing trial data; supports inference (e.g., posterior mean, **credible intervals**, posterior probabilities such as Pr(effect > threshold)).  
- **Bayes theorem:** Combines prior and likelihood into the posterior.

---

## Where Bayesian methods have appeared (illustrative settings)

Examples include: **borrowing from earlier trials** of the same drug (e.g., REBYOTA phase 3); **external or nonconcurrent controls** (e.g., oncology platform trials, pediatric MS via CID); **pediatric extrapolation** with priors from adults (e.g., diabetes programs); **borrowing across related diseases** (basket trials, epilepsy subgroup example); **subgroup shrinkage** via **Bayesian hierarchical models** (e.g., regional effects, Drug Trials Snapshots); and **oncology dose-finding** (CRM, BLRM, BOIN, mTPI, etc., and designs targeting optimized doses rather than MTD alone).

---

## Success criteria and operating characteristics

- Frequentist trials often target **familywise Type I error (FWER)** ≤ 0.025 one-sided; with Bayesian primary inference that default may **not** apply (especially with borrowing), so **success criteria must be carefully pre-specified**—often as posterior probability that the treatment effect exceeds a clinically meaningful threshold.  
- **Approaches to success criteria** include: (1) **calibration to Type I error** (simulation when algebra is intractable); (2) **direct posterior interpretation** when the prior is a defensible summary of external belief/evidence; (3) **benefit–risk or decision-theoretic** criteria (including loss functions); (4) **interim** criteria consistent with FWER when calibration is used.  
- **Operating characteristics** depend on the prior and data. For designs **calibrated** to Type I error, frequentist OC (error rates, power, bias, MSE, interval coverage) apply. For **non-calibrated** Bayesian designs, emphasis shifts to **Bayesian power**, probability of correct decisions, expected bias/MSE/credible-interval behavior under **design priors** (sampling scenarios) vs **analysis priors** (used at analysis)—with sensitivity when they differ. Simulations should span plausible assumptions.

---

## Prior distributions (major themes)

- **General:** Priors must be **systematic, transparent, pre-specified, and justified** in the protocol, with OC discussed.  
- **Noninformative / minimally informative:** Often for “little external info”; watch small samples and **induced priors under reparameterization**. Useful as **reference** for sensitivity and **effective sample size (ESS)** comparisons.  
- **Skeptical priors:** Downweight very large effects when context warrants; can interact with **adaptive designs** and error-rate calibration.  
- **Informative priors (borrowing):** Requires strong justification—**feasibility** of non-borrowing designs, **relevance** of external data, sufficiency of prospective data for safety/benefit–risk, and **prior–data conflict** assessed via simulations and sensitivity analyses. Topics include: data quality (including RWD), **pre-specification** of sources, **relevance** (population, endpoint, measurement, recency, standard of care), design of source studies (RCT vs non-randomized), **patient-level vs summary data**, **evidence synthesis**, **exchangeability** vs effect modification, **discounting** (static vs dynamic; power priors, mixtures, BHMs, elastic priors, etc.), and **expert elicitation** (coordinate with FDA).  
- **Quantifying prior influence:** Prior mean, **ESS**, ratios of prior ESS to trial size; **not recommended** to use Type I error inflation alone as the measure of borrowing strength.  
- **Sensitivity analyses:** Alternative reasonable priors, especially when ESS is large.

---

## Estimands, missing data, software, reporting

- **Estimands / missing data:** Align with **ICH E9 / E9(R1)**; Bayesian methods can handle missingness in primary or sensitivity analyses. When borrowing, **align estimands and estimators** across external and prospective data where possible; discuss gaps with FDA.  
- **Software:** FDA does not mandate specific software; algorithms must be **reliable for the model** (MCMC convergence, etc.), with verification documentation as appropriate.  
- **Documentation:** Protocol/SAP should detail priors, likelihood, success criteria, OC, simulations; **reporting** includes posteriors, credible intervals, success criteria, sensitivity analyses, prior–data conflict / model checking, computation details (e.g., MCMC settings, seeds, code for reproducibility).

---

## Files in this folder

| File | Role |
|------|------|
| `document.pdf` | Original FDA PDF |
| `document.txt` | Plain text extracted with **pdfplumber** (structure and line breaks may differ from the PDF) |
| `summary.md` | This summary |

---

## Suggested use

For teaching or applied work, pair this regulatory framing with hands-on **prior construction, simulation, and sensitivity analysis** (e.g., PyMC, ArviZ, PreliZ) and with the ICH estimand framework referenced in the guidance.
