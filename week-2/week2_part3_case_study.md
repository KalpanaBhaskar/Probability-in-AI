# Week 2: Advanced Topics & Research Extensions
## Part 3: Bayesian Inference, Model Validation, and Open Questions

---

## 📚 Table of Contents

1. [Beyond Point Estimates: Uncertainty](#beyond-point-estimates-uncertainty)
2. [Bayesian Inference Foundations](#bayesian-inference-foundations)
3. [Prior, Likelihood, Posterior](#prior-likelihood-posterior)
4. [Bayesian Inference for the List Experiment](#bayesian-inference-for-the-list-experiment)
5. [Model Validation & Diagnostics](#model-validation--diagnostics)
6. [Generative vs Discriminative Models](#generative-vs-discriminative-models)
7. [Information & Entropy](#information--entropy)
8. [Privacy Guarantees & Formal Metrics](#privacy-guarantees--formal-metrics)
9. [Research Frontiers](#research-frontiers)
10. [Synthesis & Next Steps](#synthesis--next-steps)

---

## Beyond Point Estimates: Uncertainty

### The Problem with Point Estimates

In Part 2, we estimated: "θ₂ ≈ 0.09"

**Question**: How confident are we in this estimate?

**Possibilities**:
- θ₂ is definitely 0.09 (very confident)
- θ₂ could be anywhere from 0.02 to 0.20 (not very confident)

### Why Uncertainty Matters

**Example**: Palpatine support estimation

**Scenario 1**: 
- Estimate: 9% support
- 95% confidence interval: [8%, 10%]
- Conclusion: Palpatine is genuinely unpopular

**Scenario 2**:
- Estimate: 9% support
- 95% confidence interval: [0%, 50%]
- Conclusion: Could be very popular or very unpopular; we're unsure

**Same point estimate, very different implications!**

### Sources of Uncertainty

1. **Sampling variability**: Random variation in which 1000 people we survey
2. **Model uncertainty**: Maybe our assumptions are wrong
3. **Parameter uncertainty**: Given data, θ₂ could plausibly be several values

### Three Approaches to Uncertainty

**1. Confidence intervals (frequentist)**
- "If we repeated this study infinitely, 95% of such intervals would contain true parameter"
- Frequentist interpretation (not a probability statement about true parameter)

**2. Credible intervals (Bayesian)**
- "Given our data and prior knowledge, there's 95% probability the parameter is in this range"
- Bayesian interpretation (direct probability statement)

**3. Bootstrap/Simulation**
- Resample data, recompute estimate
- See distribution of estimates
- Simple, intuitive, avoids philosophy

---

## Bayesian Inference Foundations

### The Bayesian Approach

**Core idea**: Treat unknown parameters as random variables with probability distributions.

**Philosophy**: 
- Start with prior belief about parameter
- Observe data
- Update to posterior belief
- Use posterior for decisions/inference

### The Bayes' Rule

$$P(\text{Parameter} | \text{Data}) = \frac{P(\text{Data} | \text{Parameter}) \times P(\text{Parameter})}{P(\text{Data})}$$

**In words**:
$$\text{Posterior} = \frac{\text{Likelihood} \times \text{Prior}}{\text{Evidence}}$$

**Intuition**:
- Posterior = updated belief after seeing data
- Likelihood = how well parameter explains data
- Prior = belief before data
- Evidence = overall probability of data (marginalizing over all parameters)

### Example: Coin Flip Bias

**Scenario**: You flip a coin 10 times, get 8 heads.

**Question**: What's the probability the coin is fair (p = 0.5)?

**Bayesian approach**:

*Step 1 - Prior belief*:
```
P(p = 0.5) = 0.6  (assume coin is probably fair)
P(p = 0.7) = 0.4  (less likely to be biased)
```

*Step 2 - Observe data*:
```
Flipped 10 times: 8 heads, 2 tails
```

*Step 3 - Likelihood*:
```
P(8 heads | p = 0.5) = Bin(10, 0.5) at k=8 ≈ 0.044
P(8 heads | p = 0.7) = Bin(10, 0.7) at k=8 ≈ 0.233
```

*Step 4 - Posterior*:
```
P(p = 0.5 | 8 heads) = 0.044 × 0.6 / (0.044×0.6 + 0.233×0.4)
                      ≈ 0.026 / 0.119 ≈ 0.22

P(p = 0.7 | 8 heads) = 0.233 × 0.4 / 0.119
                      ≈ 0.78
```

**Conclusion**: After seeing 8 heads in 10 flips, it's 78% likely the coin is biased toward heads.

---

## Prior, Likelihood, Posterior

### The Three Components

#### 1. Prior: P(θ)

**Definition**: Your belief about the parameter *before* seeing any data.

**Sources**:
- Previous studies
- Domain expertise
- Theoretical reasoning
- Uninformative priors (if no prior knowledge)

**Example: Support for Palpatine**
```
Uninformed prior: θ ∈ [0, 1] equally likely
Knowledge-based prior: θ ∈ [0, 0.3] likely (authoritarian ruler)
Skeptical prior: θ ∈ [0, 0.1] (very few support oppressors)
```

**Common priors**:

*Uniform(0, 1)*: No prior information
```
P(θ) = 1 for all θ ∈ [0, 1]
Effect: Data dominates posterior
```

*Beta(α, β)*: Flexible with parameters
```
Beta(1, 1) = Uniform (no information)
Beta(2, 2) = U-shaped (extremes more likely)
Beta(5, 1) = Skewed right (support likely high)
Beta(1, 5) = Skewed left (support likely low)
```

#### 2. Likelihood: P(Data | θ)

**Definition**: Probability of observing the data given a parameter value.

**Role**: "How well does this parameter explain the observed data?"

**Formula for list experiment**:
$$P(A_1, A_2, ..., A_n | \theta_2) = \prod_{i=1}^{n} P(A_i | \theta_2)$$

**Example**:
- Observed: 1000 people, mean count = 2.62
- If θ₂ = 0.09:
  - P(Data | θ₂ = 0.09) = [high, data well-explained]
- If θ₂ = 0.50:
  - P(Data | θ₂ = 0.50) = [low, data poorly explained]

#### 3. Posterior: P(θ | Data)

**Definition**: Updated belief about parameter after observing data.

**Interpretation**: Probability distribution over parameter values.

**Properties**:
- Incorporates both prior and data
- Used for inference/decisions
- Valid probability distribution (sums/integrates to 1)

### The Posterior as Summary

A posterior distribution provides:

**Point estimate**:
- Mean of posterior
- Median of posterior
- Mode of posterior (most likely value)

**Interval estimate**:
- 95% credible interval (middle 95% of posterior)
- Highest density interval (most likely 95% of posterior)

**Full distribution**:
- Visualize as histogram or curve
- See all plausible parameter values
- Understand uncertainty

---

## Bayesian Inference for the List Experiment

### Setting Up the Bayesian Model

**Components**:

*Prior on θ₂*: 
$$P(\theta_2) = \text{Beta}(1, 19)$$
(Skeptical: expect low support; before data, E[θ₂] ≈ 1/20 = 5%)

*Likelihood*:
$$P(A_i | \theta_2) = \sum_{h=0}^{5} P(H=h) \times P(A_i - h | \theta_2)$$

*Posterior by Bayes' rule*:
$$P(\theta_2 | \text{Data}) \propto P(\text{Data} | \theta_2) \times P(\theta_2)$$

### Computing the Posterior: MCMC

**Problem**: Computing posterior requires integration (hard math)

**Solution**: Markov Chain Monte Carlo (MCMC)
- Computer simulation to approximate posterior
- Generates random samples from posterior distribution
- More samples = better approximation

**Algorithm** (simplified):
```
1. Start with guess: θ₂ = 0.05

2. Repeat 10,000 times:
   a. Propose new value: θ₂_new = θ₂_old + random_step
   b. Compute ratio:
      ratio = P(Data | θ₂_new) × P(θ₂_new) / 
              P(Data | θ₂_old) × P(θ₂_old)
   c. Accept new value with probability = min(1, ratio)
   d. Store accepted value

3. Discard first 1000 samples (burn-in)
4. Analyze remaining 9000 samples
```

**Result**: 9000 samples from posterior distribution

### Interpreting the Posterior

**Histogram of MCMC samples**:
```
Frequency
    |     
  8 |    █
  7 |   ██
  6 |   ██  
  5 |  ███
  4 |  ███
  3 | █████
  2 | █████
  1 |████████
  0 |████████████
    └─────────────── θ₂
     0.05 0.10 0.15 0.20
```

**Posterior summaries**:
```
Mean: 0.098
Median: 0.096
95% credible interval: [0.065, 0.135]
```

**Interpretation**:
- Best estimate: θ₂ ≈ 0.10 (10% support)
- Plausible range: 6.5% to 13.5% (95% credible)
- Support is probably not below 5% or above 20%

### Prior Sensitivity Analysis

**Question**: How much does posterior change with different priors?

**Comparison**:

*Skeptical prior: Beta(1, 19)*
```
E[θ₂] = 0.098
95% CI: [0.065, 0.135]
```

*Neutral prior: Beta(1, 1)* (uniform)
```
E[θ₂] = 0.102
95% CI: [0.068, 0.140]
```

*Generous prior: Beta(5, 5)* (less informative)
```
E[θ₂] = 0.100
95% CI: [0.060, 0.145]
```

**Conclusion**: All priors lead to similar posterior (data dominates)

**Lesson**: If data is strong, prior doesn't matter much. If data is weak, prior choice is crucial.

---

## Model Validation & Diagnostics

### Why Validate?

Even if posterior looks nice, doesn't mean model is correct.

**Possible problems**:
- Prior is wrong
- Likelihood (model) is wrong
- Data quality is poor
- Independence assumption violated

### Posterior Predictive Check

**Idea**: "Does data simulated from posterior look like actual data?"

**Algorithm**:
```
1. From posterior samples of θ₂:
   For each sample θ₂_i:
   
   a. Simulate 1000 new people's responses:
      For each person:
         H ~ Bin(5, 0.5)
         S ~ Ber(θ₂_i)
         A = H + S
   
   b. Compute mean of simulated A
   
2. Collect means from all posterior samples

3. Compare distribution of simulated means to actual mean
```

**Result**: Two distributions
- Actual mean = 2.62
- Simulated means = histogram of means

**Interpretation**:
- If actual mean is in middle of simulated distribution: ✓ Model is reasonable
- If actual mean is in tail: ✗ Model has problems

### Residual Analysis

**Idea**: Look at deviations between actual and predicted.

**Approach**:
```
For each count k ∈ {0, 1, 2, 3, 4, 5, 6}:
    Actual frequency = observed count of k
    Predicted frequency = P(A = k | posterior mean of θ₂)
    Residual = Actual - Predicted
    Standardized residual = Residual / √(Predicted)
```

**Interpretation**:
- Residuals close to 0: Good fit
- Large residuals: Poor fit in that region
- Systematic pattern: Model misspecified

### Checking Independence Assumption

**Null hypothesis**: H and S are independent

**Test**:
```
1. Divide people into two groups:
   Group 1: Reported A = 0, 1, 2 (low counts)
   Group 2: Reported A = 4, 5, 6 (high counts)

2. Within each group, look at responses to harmless questions
   Do low-count people answer same way to harmless?
   Do high-count people answer same way to harmless?

3. If independence holds:
   Pattern of harmless answers should be similar in both groups
   
   If violated:
   Groups show different patterns
   (e.g., low-count people always say no to surprises)
```

**Implication of violation**:
- Hidden question correlates with harmless questions
- Estimates become biased
- Need to adjust model

---

## Generative vs Discriminative Models

### Two Frameworks

#### Generative Models

**Approach**: Model the full data-generating process.

**For list experiment**:
```
Step 1: Generate S ~ Ber(θ₂)
Step 2: Generate H ~ Bin(5, 0.5)
Step 3: Generate A = H + S
```

**Advantages**:
- Complete story of how data arises
- Can generate synthetic data
- Can answer many types of questions
- Interpretable
- Incorporates domain knowledge

**Disadvantages**:
- May include unnecessary assumptions
- Can be computationally complex

#### Discriminative Models

**Approach**: Model directly P(Output | Input), skip the process.

**For list experiment**:
```
Learn function: A → θ₂
(directly map from counts to support estimate)
```

**Advantages**:
- Simpler, more efficient
- Only model what matters for prediction
- Often better predictions

**Disadvantages**:
- Black box (no interpretation)
- Can't generate synthetic data
- May miss important structure

### When to Use Each

| Scenario | Generative | Discriminative |
|----------|-----------|----------------|
| Predicting next observation | ✓ | - |
| Understanding mechanisms | ✓ | - |
| Few observations | ✓ | - |
| Many observations | - | ✓ |
| Missing data/imputation | ✓ | - |
| Simple prediction task | - | ✓ |
| Interpretability needed | ✓ | - |
| Speed critical | - | ✓ |

**List experiment choice**: **Generative** (we care about the story and mechanism)

---

## Information & Entropy

### Information: A Measure of Surprise

**Definition**: Information content is inversely related to probability.

Rare events carry more information.

$$I(x) = -\log P(x)$$

**Intuition**:
- P(x) = 1 (certain) → I(x) = 0 bits (no surprise)
- P(x) = 0.5 (fair coin) → I(x) = 1 bit (some surprise)
- P(x) = 0.01 (rare) → I(x) ≈ 6.6 bits (high surprise)

**Example**:
```
"It's raining in monsoon season" → low information (expected)
"It's raining in desert" → high information (surprising)
```

### Entropy: Average Surprise

**Definition**: Entropy is the expected information (average surprise).

For discrete X:
$$H(X) = -\sum_x P(x) \log P(x)$$

**Interpretation**:
- H = 0: No uncertainty (X always has same value)
- H = large: High uncertainty (X could be many values)

**Maximum entropy**: 
- Discrete with n values: H_max = log(n)
- Achieved when all values equally likely

**Examples**:

*Fair coin*:
$$H = -(0.5 \log 0.5 + 0.5 \log 0.5) = 1 \text{ bit}$$

*Unfair coin (p = 0.9)*:
$$H = -(0.9 \log 0.9 + 0.1 \log 0.1) ≈ 0.47 \text{ bits}$$

*Certain outcome (p = 1)*:
$$H = -(1 \log 1 + 0 \log 0) = 0 \text{ bits}$$

### Entropy and Inference

**Principle**: Maximum entropy = maximum uncertainty

**Application to list experiment**:

*Prior entropy* (before experiment):
- Uniform prior on θ₂ ∈ [0, 1]
- H(prior) = log(# possible values)

*Posterior entropy* (after data):
- Distribution of θ₂ after observing means and counts
- H(posterior) < H(prior) (data reduces uncertainty)

**Information gained**:
$$I_{\text{gained}} = H(\text{prior}) - H(\text{posterior})$$

**Interpretation**: How much did the list experiment teach us?

### Mutual Information

**Definition**: How much information does one variable contain about another?

$$I(X; Y) = H(X) - H(X | Y)$$

**For list experiment**:
```
I(S; A) = how much does reported count A 
          tell us about hidden support S?
```

**High mutual information**:
- A strongly predicts S
- Counts contain signal

**Low mutual information**:
- A weakly predicts S
- Noise dominates signal

**Design goal**: Maximize I(S; A) while maintaining privacy

---

## Privacy Guarantees & Formal Metrics

### Privacy: What Does It Mean?

**Formal definition** (Differential Privacy):
> A mechanism is ε-differentially private if, for any two adjacent datasets D and D' (differing by one person), and any output y:
> $$P(\text{mechanism}(D) = y) \leq e^\epsilon \times P(\text{mechanism}(D') = y)$$

**In words**: Adding or removing one person's data doesn't change output probability too much.

### List Experiment Privacy

**Question**: If you report A = 6, is your secret out?

**Mathematical answer**:
```
A = 6 can only come from H = 5, S = 1
(must have said yes to all 5 harmless + hidden question)

P(A = 6 | S = 0) = 0 (impossible)
P(A = 6 | S = 1) = P(H = 5) = 0.031

Ratio = P(A = 6 | S = 1) / P(A = 6 | S = 0) = ∞
```

**Interpretation**: If you report 6, you're exposed (secret is out).

### Measuring Privacy Loss

**Definition**: Privacy loss of outcome a given secret s:
$$L(a, s) = \log \frac{P(a | s = 1)}{P(a | s = 0)}$$

**Examples**:

*A = 0*:
```
P(A = 0 | S = 0) = 0.031
P(A = 0 | S = 1) = 0
L(0, 0) = -∞ (you're definitely not a supporter)
```

*A = 3*:
```
P(A = 3 | S = 0) = 0.313
P(A = 3 | S = 1) = 0.156
L(3, ?) = log(0.156/0.313) ≈ -0.7
(count of 3 slightly suggests you're not a supporter)
```

*A = 6*:
```
P(A = 6 | S = 0) = 0
P(A = 6 | S = 1) = 0.031
L(6, 1) = ∞ (you're definitely a supporter)
```

### Quantifying Privacy Breaches

**Fraction exposed**:
- About 0.3% of respondents report A = 0 or 6
- These ~30 people out of 1000 have privacy breached

**Expected privacy loss** (averaged):
```
E[L] = Σ P(A = a) × L(a)
     = Σ P(a|s=1)×L(a|s=1) + Σ P(a|s=0)×L(a|s=0)
```

### Improving Privacy

**Problem**: Extreme counts (0 or 6) expose secrets

**Solutions**:

1. **Add more harmless questions**
   - More questions → harder to get 0 or 6
   - Example: 10 harmless questions
   - P(A = 0) = P(H = 0) = (0.5)^10 ≈ 0.001
   - Much harder to expose (only 1 in 1000)

2. **Add noise/rounding**
   - Round counts to nearest 2: {0, 2, 4, 6}
   - Blur individual responses
   - Trade off: more noise, less accurate inference

3. **Use randomized response**
   - Even if asked truthfully, respondent gets deniability
   - Higher privacy guarantee
   - Lower information from each response

---

## Research Frontiers

### Open Problem 1: Correlated Responses

**Issue**: Harmless and hidden questions might correlate.

**Example**: 
- People who like surprises might also be risk-takers
- Risk-takers might be more likely to support Palpatine
- Violates independence

**Research question**: How to detect and adjust for correlation?

**Approaches**:
- Test for correlation (statistical tests)
- Use auxiliary information (demographics, behaviors)
- Model correlation explicitly (more complex model)

### Open Problem 2: Heterogeneous Privacy

**Issue**: Privacy loss is unequal.

**Example**:
- Extreme counts (0 or 6): high privacy loss (~100% exposed)
- Middle counts (3): low privacy loss (~10% exposed)

**Research question**: How to provide uniform privacy?

**Approaches**:
- Differential privacy mechanisms (formal guarantees)
- Randomized response (everyone gets deniability)
- Hybrid approaches (combine methods)

### Open Problem 3: Multiple Hidden Questions

**Issue**: Want to ask about 2+ sensitive topics.

**Naive approach**: Two surveys (inefficient)

**Research question**: Can one survey ask about multiple hidden topics?

**Challenges**:
- Interactions between hidden questions
- More complex inference
- Lower power (signal spread across more dimensions)

**Possible solutions**:
- Conjoint analysis (combinations of topics)
- Multidimensional list experiments
- Sequential designs (ask about topic 1, then 2)

### Open Problem 4: Handling Liars

**Issue**: Some people lie about harmless questions.

**Example**:
- Person always says "yes" to everything (pattern respondent)
- Adds artificial noise
- Biases estimates

**Research question**: How to detect and adjust for liars?

**Approaches**:
- Consistency checks (ask same question twice)
- Validate harmless questions (compare to truth)
- Robust estimation (use methods that downweight outliers)

### Open Problem 5: Optimal Design

**Issue**: Many choices in list experiment design.

**Decisions**:
- How many harmless questions? (5, 6, 10, 20?)
- What difficulty level? (40/60, 45/55, 50/50?)
- Sample size? (100, 1000, 10000?)

**Research question**: What's the optimal design?

**Optimization goal**:
- Maximize information about hidden question
- Maintain desired privacy level
- Minimize cost/effort

**Approach**: 
- Compute information for each design choice
- Simulate privacy loss
- Optimize trade-off

---

## Synthesis & Next Steps

### What You've Learned

#### Part 1: Foundations
- Distributions completely describe random variables
- Discrete vs continuous requires different math
- Common distributions model common situations
- Mean and variance summarize distributions

#### Part 2: Case Studies
- List experiments solve sensitive questions problems
- Privacy + accuracy is possible with clever design
- Probability models as stories (generative)
- Simulation to verify and understand

#### Part 3: Advanced Topics
- Uncertainty quantification via Bayesian inference
- Validation and diagnostics (is model correct?)
- Privacy formally defined and measured
- Research frontiers (open problems)

### The Bigger Picture

**Theme**: Probabilistic thinking transforms uncertainty into knowledge.

**Tools**:
1. **Probability distributions**: Model outcomes
2. **Statistical inference**: Learn from data
3. **Simulation**: Explore and understand
4. **Bayesian methods**: Incorporate knowledge
5. **Privacy techniques**: Protect individuals

**Applications**:
- Science (hypothesis testing, measurement)
- Business (forecasting, decisions)
- Public policy (evaluation, hidden behaviors)
- Technology (machine learning, optimization)

### From Theory to Practice

**Recipe for building a probabilistic model**:

1. **Understand the problem**
   - What's the question?
   - Why is direct observation hard?
   - What data can we collect?

2. **Tell the story**
   - What random variables?
   - What distributions?
   - How do they relate?

3. **Encode assumptions**
   - Independence?
   - Parameter values?
   - Known vs unknown?

4. **Collect data**
   - Design experiment/survey
   - Maintain data quality
   - Record carefully

5. **Fit the model**
   - Estimate parameters
   - Quantify uncertainty
   - Validate assumptions

6. **Draw conclusions**
   - Interpret estimates
   - Discuss implications
   - Report limitations

### Next Steps in Probability & Inference

**To deepen your learning**:

1. **More distributions**
   - Exponential (waiting times)
   - Gamma (sums of exponentials)
   - Dirichlet (distributions over probabilities)
   - Multivariate normal (correlated variables)

2. **More inference methods**
   - Hypothesis testing (frequentist)
   - Maximum likelihood estimation
   - Variational inference (scalable Bayesian)
   - Causal inference (not just associations)

3. **Applications**
   - Measurement error models
   - Missing data imputation
   - Time series forecasting
   - Network analysis

4. **Advanced Bayesian methods**
   - Hierarchical models (data with structure)
   - Mixture models (multiple populations)
   - Latent variable models (unobserved factors)

---

## Final Reflections

### On Uncertainty

> "Uncertainty is not weakness. A well-calibrated probabilistic model that admits uncertainty is stronger than a confident lie." — Adapted from uncertainty philosophy

### On Inference

> "We use probability not to predict the future, but to extract signal from noisy data. The future is unknown, but the past and present can be understood." — Statistical philosophy

### On Privacy

> "Privacy and utility need not be enemies. With clever design, we can learn population-level truths while protecting individual secrets." — Differential privacy principle

### On Learning

> "The goal is not to memorize formulas, but to develop intuition for how randomness creates patterns, and how patterns reveal truth." — Pedagogical philosophy

---

## Final Assessment & Reflection

### Core Questions to Reflect On

1. **Conceptual**:
   - What makes two distributions "different" in a way that matters?
   - Why can't we just ask people directly? What are the fundamental barriers?
   - How does adding noise (harmless questions) help us find truth?

2. **Technical**:
   - How would you modify the list experiment if 30% of people support Palpatine (not 9%)?
   - Why is the independence assumption between H and S so critical?
   - How would you teach someone else why E[A] = E[H] + E[S]?

3. **Practical**:
   - Design a list experiment for a real sensitive question (without collecting actual data)
   - What could go wrong in your design? How would you diagnose it?
   - How would you present results to non-technical stakeholder?

4. **Research**:
   - What's one research question about the list experiment you'd want to investigate?
   - What data would you need?
   - How would you know if your approach worked?

### Integration with Week 1

**Week 1 foundation**: 
- Random variables
- Bernoulli & Binomial
- Probabilistic models as stories

**Week 2 builds on this**:
- Full probability distributions
- Inference from data
- Practical applications (list experiments)
- Advanced methods (Bayesian, privacy)

**Synthesis**: Probability theory provides a unified language for:
- Modeling uncertainty
- Learning from data
- Making decisions
- Protecting privacy

---

## Recommended Reading & Resources

### Textbooks
- **"Probability & Statistics" by DeGroot & Schervish**: Rigorous, comprehensive
- **"Statistical Rethinking" by Richard McElreath**: Intuitive, Bayesian-focused
- **"Intro to Statistical Learning"**: Applied, machine learning perspective

### Research Papers
- **Imai et al. (2011)**: "Multivariate Regression Discontinuity Design for Causal Inference" (list experiments foundations)
- **Nguyen & Goto (2024)**: "Unmasking Academic Cheating with List Experiments" (modern application)
- **Dwork (2006)**: "Differential Privacy" (privacy theory)

### Online Resources
- **Statistical Rethinking course** (free, by McElreath)
- **MIT OpenCourseWare**: Probability and statistics courses
- **Stan documentation**: Bayesian inference software

---

## Closing Thought

> Probability is humanity's attempt to reason logically about an uncertain world. The list experiment exemplifies this beautifully: by combining probability theory with clever design, we extract truth while respecting privacy. This is not just mathematics—it's humanism with equations.

---

**End of Week 2 Part 3**

---

## Quick Reference: Week 2 Formulas

### Distributions
- Bernoulli: P(X=1) = p
- Binomial: P(X=k) = C(n,k) × p^k × (1-p)^(n-k)
- Geometric: P(X=k) = (1-p)^(k-1) × p
- Poisson: P(X=k) = λ^k × e^(-λ) / k!

### Expected Values
- E[Bernoulli(p)] = p
- E[Binomial(n,p)] = np
- E[Geometric(p)] = 1/p
- E[Poisson(λ)] = λ

### Variances
- Var[Bernoulli(p)] = p(1-p)
- Var[Binomial(n,p)] = np(1-p)
- Var[Geometric(p)] = (1-p)/p²
- Var[Poisson(λ)] = λ

### List Experiment
- E[H] = 5 × 0.5 = 2.5
- E[A] = E[H] + E[S] = 2.5 + θ₂
- P(A=k) = P(H=k)(1-θ₂) + P(H=k-1)θ₂
- Estimate: θ₂ = E[A] - 2.5

### Bayesian
- Posterior ∝ Likelihood × Prior
- P(θ | Data) ∝ P(Data | θ) × P(θ)

---

**Congratulations on completing Week 2!**

You now understand:
✓ Probability distributions deeply
✓ How to model real-world problems  
✓ How inference works (Bayesian)
✓ Privacy-preserving methods
✓ Validation and diagnosis

**Ready for Week 3?** Bring these foundations forward!
