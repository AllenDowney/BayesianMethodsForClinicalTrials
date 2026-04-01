# Project board — Bayesian methods for clinical trials

Task tracking for course development. Update statuses as work progresses.

**Legend:** `[ ]` not started · `[~]` in progress · `[x]` done

---

## Course infrastructure

- [ ] Finalize conda env (`make create_environment`) and document activation in README
- [ ] Add notebook layout under `notebooks/` (or chosen directory) and align `make tests`
- [ ] Optional: CI workflow (e.g. micromamba + `make tests`) when notebooks exist

---

## Notebooks & materials (by proposal section)

### Introduction

- [ ] Learning objectives slide/notebook section
- [ ] Jupyter on Colab setup notes
- [ ] Pandas for discrete distributions

### Estimating proportions

- [ ] Binomial likelihood, beta prior, grid update
- [ ] Application: medical test specificity

### From beliefs to decisions

- [ ] Posterior probability of superiority
- [ ] Thompson sampling
- [ ] Application: Bayesian trial / A/B testing

### Conjugate priors

- [ ] Beta–binomial, Rookie Problem, informative priors
- [ ] Credible intervals vs conventional CIs

### Estimating rates

- [ ] Gamma–Poisson, applications (accidents, disease, arrivals)
- [ ] Tail / catastrophe probabilities

### Prediction

- [ ] Posterior predictive distributions
- [ ] World Cup / goal-scoring, negative binomial

### Difference of means

- [ ] Normal–normal model, distribution of differences
- [ ] Bayesian hypothesis testing, educational intervention example

### Beyond conjugate priors

- [ ] German Tank Problem
- [ ] Eliciting priors from experts
- [ ] Grizzly Bear Problem

### Beyond grid methods

- [ ] Computational limits of grids
- [ ] MCMC introduction (PyMC / ArviZ / PreliZ alignment)

### Outro

- [ ] Myths about Bayes
- [ ] When to use Bayesian methods
- [ ] Resources and further reading

---

## Learning outcomes checklist

Map each notebook/exercise to the outcomes listed in `proposal.md`; tick when covered.

- [ ] Grid posteriors for proportions, rates, means
- [ ] Conjugate priors (Beta, Gamma, Normal) and interpretation
- [ ] Posterior visualization and uncertainty
- [ ] Credible vs confidence intervals
- [ ] Posterior probability of superiority + decisions (A/B, trials)
- [ ] Thompson sampling
- [ ] Posterior predictive distributions
- [ ] Gamma–Poisson for counts/rates
- [ ] Normal–normal and Bayesian hypothesis testing
- [ ] Informative priors and expert elicitation
- [ ] Limits of grids + rationale for MCMC
- [ ] When Bayes helps + how to keep learning

---

## Admin & delivery

- [ ] Submission / JSM paperwork as required
- [ ] Participant handouts or Colab links
- [ ] Dry run timing (4 hours)
