# Week 2: Probability Distributions & Inference Foundations
## Part 1: Concepts & Theory

---

## 📚 Table of Contents

1. [Quick Recap: Week 1 Essentials](#quick-recap-week-1-essentials)
2. [Distributions: The Complete Picture](#distributions-the-complete-picture)
3. [Discrete vs Continuous: Why It Matters](#discrete-vs-continuous-why-it-matters)
4. [Probability Mass Function (PMF)](#probability-mass-function-pmf)
5. [Probability Density Function (PDF)](#probability-density-function-pdf)
6. [Expected Value & Variance](#expected-value--variance)
7. [Common Discrete Distributions](#common-discrete-distributions)
8. [Independence & Dependence](#independence--dependence)
9. [Simulation as a Learning Tool](#simulation-as-a-learning-tool)
10. [Key Concepts Summary](#key-concepts-summary)

---

## Quick Recap: Week 1 Essentials

### What You Should Remember

Last week, we learned:
- **Random variables** are rules that assign numbers to random outcomes
- **Bernoulli distribution** Ber(p) models a single yes/no trial
  - Example: "Does this person support Palpatine?" (Yes=1, No=0)
- **Binomial distribution** Bin(n,p) counts successes in n independent trials
  - Example: "How many of 5 games did the team win?"
- **Probability mass function (PMF)** shows all possible values and their probabilities
- **The key insight**: A probabilistic model is a story with random variables that makes data

### Visual Reminder: Bernoulli vs Binomial

```
Bernoulli: One trial
X ~ Ber(p)
Possible values: {0, 1}
P(X=1) = p
P(X=0) = 1-p

Binomial: Count successes in n trials
X ~ Bin(n,p)
Possible values: {0, 1, 2, ..., n}
P(X=k) = C(n,k) × p^k × (1-p)^(n-k)
```

---

## Distributions: The Complete Picture

### What is a Distribution?

A **probability distribution** completely specifies all possible outcomes of a random variable and the probability of each outcome.

**In everyday terms**: A distribution answers three questions:
1. What outcomes are possible?
2. How likely is each outcome?
3. What patterns emerge when we observe many outcomes?

### Why Distributions Matter

Imagine you're a teacher grading a test:
- **Same average (mean = 70) can come from:**
  - Everyone scores exactly 70
  - Half score 40, half score 100
  
These have identical means but very different distributions. **The distribution tells the whole story.**

### The Distribution Hierarchy

```
Random Variable (e.g., X)
        ↓
Type: Discrete or Continuous
        ↓
Distribution Family (e.g., Binomial, Normal)
        ↓
Parameter Values (e.g., n=10, p=0.5)
        ↓
The Complete Picture (PMF/PDF)
```

---

## Discrete vs Continuous: Why It Matters

### Discrete Random Variables

**Definition**: Can take only specific, countable values (usually integers).

**Characteristics**:
- You can list all possible values
- There are "gaps" between possible values
- Each specific value has a non-zero probability

**Examples**:
- Number of heads in 10 coin flips: {0, 1, 2, ..., 10}
- Number of students present: {0, 1, 2, ..., n}
- Dice roll: {1, 2, 3, 4, 5, 6}
- Survey response: "How many times did you cheat?" (0, 1, 2, 3, ...)

**Probability**: We ask "What's P(X = 5)?" (exact value)

### Continuous Random Variables

**Definition**: Can take any value in a range (infinite possibilities).

**Characteristics**:
- Uncountably infinite possible values
- No gaps—any number in a range is possible
- Individual values have zero probability
- We only have probability for ranges

**Examples**:
- Height: Could be 5.6237849... feet
- Temperature: Could be 72.314159...°F
- Time to solve a problem: Could be 23.456... seconds
- Weight of a product: Could be 9.99999... kg

**Probability**: We ask "What's P(X ≤ 5)?" or "What's P(4 < X < 6)?"

### Why The Difference?

This isn't just academic. The **type determines:**

| Aspect | Discrete | Continuous |
|--------|----------|-----------|
| Probability function | PMF (Probability Mass) | PDF (Probability Density) |
| Single value probability | Can be > 0 | Always 0 |
| Visualization | Bar chart | Smooth curve |
| Sum of probabilities | All outcomes: Σ P(X=k) = 1 | All outcomes: ∫ PDF(x) dx = 1 |
| Question we ask | P(X=5)? | P(a ≤ X ≤ b)? |

---

## Probability Mass Function (PMF)

### Definition

For a **discrete** random variable X, the **PMF** is a function that gives the probability of each possible value:

$$\text{PMF: } p(x) = P(X = x)$$

### Key Properties

1. **All PMF values are between 0 and 1**: $0 \leq p(x) \leq 1$
2. **PMF values sum to 1**: $\sum_x p(x) = 1$
3. **PMF can only be defined for possible values**

### Example 1: Fair Die Roll

```
X = outcome of rolling a fair die
Possible values: {1, 2, 3, 4, 5, 6}

PMF:
p(1) = 1/6 ≈ 0.167
p(2) = 1/6 ≈ 0.167
p(3) = 1/6 ≈ 0.167
p(4) = 1/6 ≈ 0.167
p(5) = 1/6 ≈ 0.167
p(6) = 1/6 ≈ 0.167

Check: 6 × (1/6) = 1 ✓
```

**Visualization**: Six equal-height bars at 0.167

### Example 2: Unfair Coin (Heads-biased)

```
X = outcome of flipping a bent coin
Possible values: {0 (Tails), 1 (Heads)}

PMF:
p(0) = 0.4  (probability of Tails)
p(1) = 0.6  (probability of Heads)

Check: 0.4 + 0.6 = 1 ✓
```

**Visualization**: Two bars, one at height 0.4, one at height 0.6

### Example 3: Bernoulli Distribution Ber(p)

The **Bernoulli distribution** is the simplest discrete distribution.

$$X \sim \text{Ber}(p)$$

**PMF**:
$$p(x) = \begin{cases} 1-p & \text{if } x = 0 \\ p & \text{if } x = 1 \\ 0 & \text{otherwise} \end{cases}$$

Or more compactly:
$$p(x) = p^x (1-p)^{1-x} \text{ for } x \in \{0, 1\}$$

**Interpretation**:
- p = probability of "success" (outcome = 1)
- 1-p = probability of "failure" (outcome = 0)

**Examples**:
- Ber(0.79): Penalty kick scoring probability (Messi's famous conversion rate)
- Ber(0.5): Fair coin flip
- Ber(0.09): Hidden support for Palpatine in the list experiment

### Example 4: Binomial Distribution Bin(n, p)

The **Binomial distribution** counts successes in n independent Bernoulli trials.

$$X \sim \text{Bin}(n, p)$$

**PMF**:
$$p(k) = P(X = k) = \binom{n}{k} p^k (1-p)^{n-k}$$

Where:
- $\binom{n}{k} = \frac{n!}{k!(n-k)!}$ (binomial coefficient, "n choose k")
- k is the number of successes
- n is the number of trials
- p is the probability of success on each trial

**Interpretation**: 
- n independent yes/no trials
- Each has probability p of success
- X counts total successes

**Examples**:
- Bin(10, 0.5): Number of heads in 10 coin flips
- Bin(5, 0.6): Number of wins in 5 games
- Bin(30, 0.2): Number of classmates with same birthday as you

---

## Probability Density Function (PDF)

### Definition

For a **continuous** random variable X, the **PDF** is a function such that the probability of X falling in an interval [a, b] is:

$$P(a \leq X \leq b) = \int_a^b f(x) \, dx$$

### Key Properties

1. **PDF is always non-negative**: $f(x) \geq 0$ for all x
2. **Total area under PDF is 1**: $\int_{-\infty}^{\infty} f(x) \, dx = 1$
3. **Individual values have zero probability**: $P(X = c) = 0$ for any single value c
4. **Probabilities are areas under the curve**

### Why Individual Values Have Zero Probability

This is counterintuitive but mathematically necessary:

**Discrete case**: 
- Height of 180 cm: "exactly 180.000000..." cm
- Probability = 0 (one point has no area)
- But probability of range [179.9, 180.1] > 0

**Intuition**: 
- There are infinitely many possible heights between 179 and 181 cm
- If each had probability > 0, total would exceed 1
- So each individual value must have probability 0

### Example 1: Uniform Distribution

The simplest continuous distribution: **Uniform on [a, b]**

$$X \sim \text{Uniform}(a, b)$$

**PDF**:
$$f(x) = \begin{cases} \frac{1}{b-a} & \text{if } a \leq x \leq b \\ 0 & \text{otherwise} \end{cases}$$

**Interpretation**: All values in [a, b] are equally likely.

**Example**: Random number generator gives values between 0 and 1
- X ~ Uniform(0, 1)
- f(x) = 1 for 0 ≤ x ≤ 1
- Area of rectangle = height × width = 1 × 1 = 1 ✓

### Example 2: Normal Distribution

The famous "bell curve": **Normal(μ, σ²)**

$$X \sim \text{Normal}(\mu, \sigma^2)$$

**PDF**:
$$f(x) = \frac{1}{\sigma\sqrt{2\pi}} \exp\left(-\frac{(x-\mu)^2}{2\sigma^2}\right)$$

**Interpretation**:
- μ (mu) = mean (center of distribution)
- σ (sigma) = standard deviation (spread)
- σ² = variance

**Properties**:
- Bell-shaped, symmetric around μ
- ~68% of data within μ ± σ
- ~95% of data within μ ± 2σ
- Models many real-world phenomena (heights, test scores, measurement errors)

**Examples**: 
- Human height: Normal(5.8, 0.3²) feet
- IQ scores: Normal(100, 15²)
- Measurement error in scientific instruments

---

## Expected Value & Variance

### Expected Value (Mean)

**Definition**: The **expected value** (or mean) of a random variable is its long-run average.

$$E[X] = \sum_x x \cdot p(x) \quad \text{(discrete)}$$
$$E[X] = \int_{-\infty}^{\infty} x \cdot f(x) \, dx \quad \text{(continuous)}$$

**Interpretation**: If you repeat the experiment infinitely many times, the average outcome is E[X].

**Examples**:

*Fair die*:
$$E[X] = 1 \cdot \frac{1}{6} + 2 \cdot \frac{1}{6} + ... + 6 \cdot \frac{1}{6} = \frac{21}{6} = 3.5$$

*Bernoulli(p)*:
$$E[X] = 0 \cdot (1-p) + 1 \cdot p = p$$

*Binomial(n, p)*:
$$E[X] = np$$
(Intuition: n trials, each with success probability p, gives n×p successes on average)

### Variance

**Definition**: **Variance** measures spread or dispersion. It's the average squared deviation from the mean.

$$\text{Var}(X) = E[(X - E[X])^2] = E[X^2] - (E[X])^2$$

**Interpretation**: 
- Variance = 0: No variability (always the same value)
- Variance = large: Highly variable outcomes
- Units: (original units)²

**Standard deviation**: $\sigma = \sqrt{\text{Var}(X)}$ (returns to original units)

**Examples**:

*Bernoulli(p)*:
$$\text{Var}(X) = p(1-p)$$
Maximum variance at p = 0.5 (most uncertainty)

*Binomial(n, p)*:
$$\text{Var}(X) = np(1-p)$$

*Uniform(a, b)*:
$$\text{Var}(X) = \frac{(b-a)^2}{12}$$

### Why Both Matter

**Example**: Two investments
- Investment A: Always returns $100 (E[X] = 100, Var = 0)
- Investment B: 50% chance $50, 50% chance $150 (E[X] = 100, Var = 2500)

Same expected return, very different risk!

---

## Common Discrete Distributions

### 1. Bernoulli Distribution: Ber(p)

**Use**: Single yes/no question, one trial with success probability p

**Parameters**: p ∈ (0, 1)

**Values**: {0, 1}

**PMF**: $P(X = 1) = p$, $P(X = 0) = 1 - p$

**Mean**: E[X] = p

**Variance**: Var(X) = p(1-p)

**Real example**: "Does this person support Palpatine?" → Ber(0.09)

---

### 2. Binomial Distribution: Bin(n, p)

**Use**: Count successes in n independent yes/no trials

**Parameters**: 
- n = number of trials (n ≥ 1)
- p = success probability (p ∈ (0, 1))

**Values**: {0, 1, 2, ..., n}

**PMF**: 
$$P(X = k) = \binom{n}{k} p^k (1-p)^{n-k}$$

**Mean**: E[X] = np

**Variance**: Var(X) = np(1-p)

**Real example**: 
- Ber(5, 0.5) = number of heads in 5 coin flips
- Bin(100, 0.8) = number of students passing a test (if 80% pass)

**Shape**:
- Symmetric when p = 0.5
- Skewed left when p > 0.5 (more successes likely)
- Skewed right when p < 0.5 (more failures likely)

---

### 3. Geometric Distribution: Geom(p)

**Use**: How many trials until the first success?

**Parameters**: p = success probability

**Values**: {1, 2, 3, ...} (number of trials, starting at 1)

**PMF**: 
$$P(X = k) = (1-p)^{k-1} p$$

**Mean**: E[X] = 1/p

**Intuition**: If p = 0.5, on average need 2 trials for first success. If p = 0.1, need 10.

**Real example**: "How many times must a student attempt the entrance exam before passing (if pass probability is 0.3)?"

---

### 4. Poisson Distribution: Poisson(λ)

**Use**: Count rare events in fixed time/space intervals

**Parameters**: λ = average number of events

**Values**: {0, 1, 2, ...} (any non-negative integer)

**PMF**:
$$P(X = k) = \frac{\lambda^k e^{-\lambda}}{k!}$$

**Mean**: E[X] = λ

**Variance**: Var(X) = λ

**Real examples**:
- Number of typos in a page of text
- Number of customer arrivals per hour
- Number of radioactive decays per second

**Key property**: Mean = Variance (unique to Poisson)

---

## Independence & Dependence

### Independence: The Key Assumption

**Definition**: Two events A and B are **independent** if:
$$P(A \text{ and } B) = P(A) \times P(B)$$

Or equivalently: Knowing that A occurred doesn't change the probability of B.

### Why It Matters

**Binomial assumption**: The n trials are independent.
- Each coin flip doesn't depend on previous flips
- Each student's passing is independent (if no cheating)
- Each person's yes/no opinion is independent (if no social pressure)

**When independence fails**, Binomial breaks:
- Coin flips with memory (not truly random)
- Students cheating (outcomes correlated)
- Opinions influenced by friends (correlated responses)

### Examples

**Independent**:
- Two coin flips: P(HH) = 0.5 × 0.5 = 0.25 ✓
- Two dice rolls: P(both 6) = 1/6 × 1/6 = 1/36 ✓
- Unrelated people's heights: multiply probabilities ✓

**Dependent**:
- Parent and child height: correlated
- Student 1 and student 2 test scores: correlated
- Temperature today and tomorrow: correlated

---

## Simulation as a Learning Tool

### What is Simulation?

**Simulation**: Generate fake data by running the probabilistic model many times.

**Process**:
1. Write down the story (probability model)
2. Sample from each random variable
3. Repeat 1000+ times
4. Analyze the results

### Why Simulate?

**Advantages**:
- Intuitive: See actual samples, not just formulas
- Flexible: Works even when math is complex
- Exploratory: Easy to try "what if" scenarios
- Verifiable: Check if model matches reality

**When math is hard**, simulation often works.
When learning, simulation clarifies concepts.

### Example: Simulating Bin(5, 0.5)

**Story**: Flip a coin 5 times, count heads.

**Simulation** (pseudocode):
```
repeat 1000 times:
    heads_count = 0
    repeat 5 times:
        flip = random() < 0.5  # true with probability 0.5
        if flip: heads_count += 1
    record heads_count

analyze the 1000 counts
```

**Result**: Histogram of results should match Binomial(5, 0.5) distribution.

### The Simulation-Math Connection

- **Simulation**: "Run the story 1000 times"
- **Formula**: "The exact probability formula"
- Both give same answer (within sampling error)
- Simulation easier to understand; formulas more elegant

---

## Key Concepts Summary

### The Core Ideas

1. **Distributions describe everything** about a random variable
   - What outcomes are possible?
   - How likely is each outcome?
   
2. **Discrete vs Continuous** determines how we calculate and visualize
   - Discrete: PMF, bars, exact values
   - Continuous: PDF, curves, ranges
   
3. **Mean and Variance** summarize the distribution
   - Mean: long-run average
   - Variance: spread/uncertainty
   
4. **Common distributions** model common situations
   - Bernoulli: one trial
   - Binomial: count successes
   - Geometric: trials until success
   - Poisson: rare events
   
5. **Independence** is crucial for many models
   - Binomial assumes independent trials
   - When independence fails, model fails
   
6. **Simulation** is a powerful learning and research tool
   - Run the story many times
   - See patterns emerge
   - Verify theories

---

## Discussion Questions

1. **Can a probability distribution be "wrong"?** When is a distribution a good model for real data?

2. **Why does the sum of probabilities have to equal 1?** What would it mean if it didn't?

3. **Which distribution would you use to model:**
   - Time between customer arrivals at a store?
   - Number of students in a class of 30 who pass?
   - Number of attempts until someone passes a test?

4. **Is simulation "cheating" compared to doing the math?** What are pros and cons of each?

5. **How would you test whether two random variables are truly independent?**

---

## Practice Problems

### Easy

1. For Bin(10, 0.5), what's the most likely outcome? (Hint: think about symmetry)

2. If E[X] = 5 and E[X²] = 30, what's Var(X)?

3. Name one example of a discrete random variable from your own life.

### Medium

4. Two Bernoulli trials: Ber(0.6) and Ber(0.6), independent. What's P(both succeed)?

5. For Poisson(3), what's P(X = 0)? P(X = 1)?

6. Why does Binomial(1, p) equal Bernoulli(p)?

### Hard

7. Compare Bin(100, 0.01) and Poisson(1). Which probabilities are more similar, and why?

8. Simulate Bin(3, 0.5) in your head. What's the approximate shape?

9. For Geometric(p), as p decreases, what happens to the mean? Why is this intuitive?

---

**End of Week 2 Part 1**

Next: Part 2 covers **Case Studies & Applications** with the Palpatine Poll and list experiments.
