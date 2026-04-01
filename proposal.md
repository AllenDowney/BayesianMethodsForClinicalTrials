# JSM Continuing Education Course Proposal

## COURSE TITLE
**Adding Bayes to Your Bag of Tricks**

---

## INSTRUCTOR

**Allen B. Downey**
Professor Emeritus, Olin College
Principal Data Scientist at PyMC Labs
Email: [downey@allendowney.com]

---

## ABSTRACT

In the standard statistics curriculum, Bayesian methods are often presented mathematically and theoretically -- and it's easy to miss their elegance and power. But Bayesian thinking can be simple, practical, and immediately useful.

This course introduces Bayesian methods using discrete grid algorithms and conjugate priors — tools that are easy to implement, easy to explain, and sufficient for many real-world problems. Using examples from *Think Bayes*, we’ll show how Bayesian methods can solve estimation, prediction, and decision problems with clarity and flexibility.

If you’ve ever said, “I’ve been meaning to learn Bayesian statistics,” this course is for you. You’ll leave with working code, a conceptual foundation, and the confidence to apply Bayes when it belongs in your bag of tricks.

**Prerequisites:** Experience with Python at an intermediate level, including NumPy, and familiarity with common probability distributions.

---

## COURSE OUTLINE (Half-Day — 4 Contact Hours)

Introduction
* Learning objectives
* Introduction to Jupyter notebooks on Colab
* Using Pandas to represent discrete distributions

Estimating proportions
* The binomial distribution as a likelihood
* The beta distribution as a prior
* The Bayesian update using grids
* Application: estimating the specificity of a medical test

From beliefs to decisions
* Posterior probability of superiority
* Thompson sampling
* Application: Bayesian medical trial (or A/B testing)

Conjugate priors
* The beta-binomial model
* The Rookie Problem: choosing informative priors
* Comparing Bayesian credible intervals with conventional CIs

Estimating rates
* The gamma prior
* The Poisson likelihood
* Applications: accidents, incidence of disease, customer arrivals
* Tail probabilities: predicting catastrophe

Prediction
* Posterior predictive distributions
* Example: goal-scoring rate and The World Cup Problem
* The negative binomial distribution

Difference of means
* The Normal-Normal model
* Distribution of differences
* Bayesian hypothesis testing
* Application: testing an educational intervention

Beyond conjugate priors
* The German Tank Problem
* Eliciting prior distributions from experts
* The Grizzly Bear Problem

Beyond grid methods
* Computational limits
* Introduction to MCMC

Outro
* A few myths about Bayes
* When to use Bayesian methods
* Resources and further reading

---



## Learning Outcomes

By the end of this course, participants will be able to:

- Use grid algorithms to compute posterior distributions for proportions, rates, and means
- Select and interpret conjugate priors (e.g., Beta, Gamma, Normal) and understand their role in analytical Bayesian updates
- Evaluate and visualize posterior distributions to quantify uncertainty and support inference
- Compare Bayesian credible intervals to conventional confidence intervals, and explain key interpretational differences
- Compute posterior probabilities of superiority and apply them in decision contexts such as A/B testing and medical trials
- Understand and implement Thompson sampling as a Bayesian decision strategy
- Derive and use posterior predictive distributions for forecasting and uncertainty quantification
- Model count data and estimate rates using the Gamma-Poisson model
- Analyze differences between group means using the Normal-Normal model, and perform Bayesian hypothesis testing
- Construct and critique informative priors, including methods for eliciting expert knowledge
- Identify the limitations of grid methods and describe the rationale for using MCMC in more complex models
- Recognize when Bayesian methods are advantageous, and know how to continue learning and applying them


---

## CONTENT AND INSTRUCTIONAL METHODS

- The course is taught using **interactive Jupyter Notebooks**, with explanatory text, code, and results.
- Each topic includes both **conceptual explanation** and **computational implementation**.
- Emphasis is on **practical understanding**, not mathematical derivation.
- This course uses active learning methods, including surveys, exercises, and opportunities for participants to discuss and collaborate.

---

## INSTRUCTOR BACKGROUND

**Allen B. Downey** is Professor Emeritus at Olin College, Principal Data Scientist at PyMC Labs, and the author of several popular textbooks, including *Think Bayes*, *Think Stats*, and *Think Python*. His work focuses on making complex statistical concepts clear and accessible through computation and interactive learning. He has decades of experience teaching Bayesian methods to undergraduate students, graduate students, and working professionals.


