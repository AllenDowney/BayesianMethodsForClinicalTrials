# Course outline — Bayesian methods aligned with FDA draft guidance

This document maps **hands-on PyMC notebooks** (under `notebooks/`) to the themes in the FDA draft *Use of Bayesian Methodology in Clinical Trials of Drug and Biological Products* ([media 190505](https://www.fda.gov/media/190505/download); see `papers/fda-media-190505/`). The guidance explains **when** Bayesian approaches appear in drug development and **what** sponsors must justify (priors, success criteria, operating characteristics); the course supplies **how** (implementation) and **why** (interpretation and advantages) through worked examples.

---

## Applications and themes 

Section III lists **settings where Bayesian methods have been used** in submissions (examples, not an exhaustive list):

| Topic | Guidance section | What to highlight in code |
|--------|------------------|---------------------------|
| **Borrowing from previous trials** (same drug) | III.A | Hierarchical / partial pooling; power priors or discounting; prior–data conflict |
| **External / nonconcurrent controls** | III.B | Bias/temporal drift; borrowing strength; sensitivity |
| **Pediatric extrapolation** | III.C | Informative priors from adults; relevance; discounting |
| **Borrowing across diseases / subtypes** (e.g. basket) | III.D | Hierarchical models; exchangeability vs effect modification |
| **Subgroup analysis** (shrinkage) | III.E | BHMs; borrowing strength across subgroups |
| **Dose-finding (oncology)** | III.F | CRM, BLRM, BOIN, mTPI; utility-based designs; MTD vs optimized dose |

Cross-cutting (Sections IV–VIII): **success criteria** (e.g. posterior probability thresholds; calibration to Type I error when appropriate), **operating characteristics** (Bayesian power, simulations), **prior choice** (noninformative, skeptical, informative), **ESS / influence of prior**, **sensitivity analyses**, **estimands & missing data** (ICH alignment), **MCMC/software**, **documentation & reporting**.

---

## PyMC ecosystem tools for Beta and binomial quantities

The following matches the **workflow in PyMC Labs’ workshop** ([`Session1-Prior_and_Posterior`](https://github.com/pymc-labs/pymc-workshop/blob/main/solutions/Session1-Prior_and_Posterior.md)): explore priors, build a `Beta`–`Binomial` model, sample, then use posterior draws for decisions and contrasts. See that notebook for full code; here is a compact map.

| Tool | Role |
|------|------|
| **PreliZ** (`preliz.Beta`, `Binomial`, …) | Plot PDFs/PMFs (`plot_pdf`, `moments="mv"`), check means/SDs, **tune priors** before or alongside PyMC—good for teaching **informative vs weakly informative** shapes. |
| **`pm.Beta("name", alpha, beta)`** | **Named random variable** in a `pm.Model`; pairs with **`pm.Binomial("obs", p=..., n=..., observed=...)`** for the likelihood. Use **`pm.model_to_graphviz(model)`** for the DAG. |
| **`pm.Beta.dist` / `pm.Binomial.dist`** | **Distribution objects** outside (or inside) a full model: use **`pm.draw(dist, draws=...)`** to simulate (workshop uses `pm.Binomial.dist` + `pm.draw` as an RNG). Fits the **conjugate-update** pattern: build a **posterior** as another **`pm.Beta.dist`**, then draw for RR/OR without MCMC. |
| **`pm.sample_prior_predictive()`** | Samples from the **prior** (and prior predictive); visualize with ArviZ **`group="prior"`** (e.g. `az.plot_posterior(..., group="prior")`). |
| **`pm.sample()`** | **MCMC** for the **posterior** when the model is not fully conjugate or you want the standard `InferenceData` workflow. |
| **`pm.sample_posterior_predictive(idata)`** | **Posterior predictive** for future counts (binomial replicates); extend `idata` and plot with `group="posterior_predictive"`. |
| **ArviZ** | **`az.plot_posterior`**, **`az.plot_dist_comparison`** (prior vs posterior on same scale), **`az.extract`** / **`idata.posterior`** to get **arrays of draws**, then **numpy** for contrasts (difference, RR, OR, **P(*A* superior)** = `(samples_A > samples_B).mean()`). **`az.plot_kde`** to overlay two arm posteriors. |
| **Moments → Beta parameters** | If specifying a prior by **mean and SD** (workshop “rookie” exercise), convert to **α, β** with the usual formulas (see workshop `compute_params`) before passing to **`pm.Beta`** or **`pm.Beta.dist`**. |

**Course emphasis for notebook 1:** lean on **`pm.Beta.dist`** + conjugate update + **`pm.draw`** for per-arm posteriors and contrast Monte Carlo; use **`pm.Beta` / `pm.Binomial` + `pm.sample`** when showing equivalence or bridging to the **full PyMC + ArviZ** pipeline used in later sessions.

---

## Proposed notebook sequence (draft)

Statuses: planned / outlined / drafted.

### 1. Proportions and treatment contrasts — LEAP study

**Status:** outlined  

**Goal:** Tie **HOW** (PyMC) to **WHY** (transparent uncertainty and prior choice) using a real randomized trial.

**Data / estimand:** LEAP (or public summary data) — **binary outcomes** by arm; estimate **proportion** of events (or primary endpoint) in each group; derive **posteriors for contrasts**—e.g. **risk difference**, **relative risk (RR)**, **odds ratio (OR)**, **log odds ratio**—with estimands documented consistently (ICH E9(R1)).

**PyMC pedagogy (conjugate first, sampling later):** (See **PyMC ecosystem tools** above and pymc-workshop Session 1.)

- Represent Beta priors and posteriors with **`pm.Beta.dist`** (distribution objects), not only equations on paper. Implement the **Beta–Binomial conjugate update** as a small function that **takes a `Beta` prior (or its shape parameters) plus binomial counts and returns a new `pm.Beta.dist` for the posterior** (standard α, β updates). Inference per arm stays **exact**—no MCMC yet.
- For **RR** and **OR** (and derived quantities): **`pm.draw`** from the two Beta posteriors and **build a Monte Carlo sample of contrasts**—e.g. ratio of sampled arm probabilities for **RR**; ratio of **odds** for **OR**. Optionally show the **same** model with **`pm.Beta` + `pm.Binomial` + `pm.sample`** and ArviZ plots to show agreement with the conjugate path.
- **PreliZ** optional: plot candidate **Beta** priors (informative vs weak) before updating.
- **Why this order:** Students use **`dist` + `draw`** then the **Model + `sample`** pattern already used in the workshop; **full MCMC** in later notebooks extends the same ArviZ tooling.

**FDA themes:**

- Primary inference with **posterior summaries** and **credible intervals** (Section II, IV).
- **Informative vs minimally informative priors** on each arm’s proportion (Section V.B–D): same data, different Beta priors → different Beta posteriors; compare width of contrasts and (if useful) **ESS**-style intuition.
- Optional: **skeptical prior** on large effect size (Section V.C) as a sensitivity analysis—e.g. encode skepticism on a contrast via prior choice on logits or arms.

**Deliverables:** One notebook (or split: `01a` data + conjugate updates, `01b` contrasts and priors) with short narrative linking to `papers/fda-media-190505/summary.md`.

---

### 2. (Planned) Borrowing — two-phase or historical data

**Goal:** Implement **partial borrowing** (e.g. power prior, mixture, or hierarchical) for a binomial or Gaussian endpoint, echoing **Section III.A** and **V.D**.

**Why:** Shows **why** Bayes when trial data are sparse: combine with external information in a **documented** way, with **prior–data conflict** and **sensitivity** plots.

---

### 3. (Planned) External / synthetic control flavor

**Goal:** Simple simulated or public example where concurrent control is augmented with **historical** data; discuss **temporal drift** and **relevance** (Section III.B).

---

### 4. (Planned) Hierarchical / subgroup shrinkage

**Goal:** BHM for **subgroup** or **region** effects (Section III.E); contrast with independent estimates.

---

### 5. (Planned) Dose-finding (simplified)

**Goal:** Small simulation of a **Bayesian dose-finding** rule (e.g. 2-parameter logistic toxicity + escalation) or citation-driven replication of a toy BOIN/CRM-style update (Section III.F)—not full regulatory depth, but **why** Bayes for sequential decisions.

---

### 6. (Optional) Rates or counts

**Goal:** Poisson–Gamma or regression for **count / rate** endpoints—pedagogical bridge to “background rate” and count endpoints in oncology or epidemiology. **If time is tight**, fold a **short** rates example into notebook 1 (e.g. secondary count endpoint) or skip as a standalone.

---

### 7. Outro

**Goal:** Map course back to **documentation** (protocol, SAP, simulation report) and **reporting** (Section VIII); **resources** (FDA draft, ICH E9(R1), PyMC/ArviZ docs).

---

## Alignment with original JSM proposal

The original half-day outline (`proposal.md`) used **grid methods** and conjugacy first. This track still **starts with conjugacy** (Beta–Binomial per arm via **`pm.Beta.dist`** and an explicit posterior map), then uses **sampling for derived quantities** (RR/OR)—so PyMC appears **day one** with a gentle ramp to **full MCMC** in later notebooks. Grids can remain optional sanity checks.

---

## References

- FDA draft guidance PDF and summary: `papers/fda-media-190505/`
- ICH E9(R1) estimands (cited in the FDA draft)
- PyMC examples: <https://www.pymc.io/projects/examples/>
- PyMC Labs workshop (Session 1 — prior/posterior, bandits, hierarchical Beta): <https://github.com/pymc-labs/pymc-workshop> (local reference: `~/pymc-workshop/solutions/Session1-Prior_and_Posterior.md`)


## Notes


### Are “rates” in the FDA draft?

**Not as a standalone topic.** The guidance does **not** walk through Poisson/Gamma models or “estimating an event rate” the way it walks through **informative priors**, **borrowing**, **discounting**, and **dose-finding**.

It **does** mention rate-type concepts in passing, for example:

- **Annualized relapse rate** as an endpoint in a pediatric MS case (CID program; modeling with external/historical data).
- **Tumor response** and other efficacy outcomes in platform-trial / nonconcurrent-control examples.
- **Simulation**: “variance or **background rate** of the endpoint” when discussing operating characteristics.

So **estimating rates** (Poisson–Gamma, time-to-event framing, etc.) remains a **useful statistical course topic** for count and incidence data—and it supports reading the guidance’s **endpoint** and **simulation** language—but it is **not** a named regulatory application block in the draft the way **borrowing** or **pediatric extrapolation** are. We can keep a rates module as **optional** or **short**, or fold rate-like examples into **dose-finding / toxicity** or **count endpoints** where the FDA *does* emphasize Bayesian designs (oncology early phase).

---