# Comprehensive Teaching Guide: Probabilistic Modeling & Inference
## "The Palpatine Poll" - Extracting Hidden Truths from Sensitive Questions

---

## TABLE OF CONTENTS
1. [Foundational Concepts](#foundational-concepts)
2. [Random Variables](#random-variables)
3. [Distributions & Their Types](#distributions--their-types)
4. [Probability Mass Function (PMF) & Probability Density Function (PDF)](#probability-mass-function-pmf--probability-density-function-pdf)
5. [Generative vs Discriminative Models](#generative-vs-discriminative-models)
6. [Probabilistic Models as Stories](#probabilistic-models-as-stories)
7. [The List Experiment / Sensitive Questions Problem](#the-list-experiment--sensitive-questions-problem)
8. [The Palpatine Poll Case Study](#the-palpatine-poll-case-study)
9. [Additional Problems & Extensions](#additional-problems--extensions)
10. [Common Misconceptions](#common-misconceptions)

---

# SECTION 1: FOUNDATIONAL CONCEPTS

## What is Probability?

### Definition
**Probability** is a numerical measure (between 0 and 1) that quantifies the likelihood or chance that an event will occur.

- **0** = Impossible (will never happen)
- **1** = Certain (will definitely happen)
- **0.5** = Even chance (equally likely to happen or not happen)

### Teaching Points
- Probability is about **uncertainty**
- We use probability when we don't know the future outcome, but we know the possible outcomes
- Example: Rolling a die has 6 possible outcomes, each with probability 1/6

### Real-World Relevance
- Medical tests: "There's a 95% chance this test result is correct"
- Weather: "30% probability of rain tomorrow"
- Politics: "Polls suggest 55% support for Policy X"
- Hidden truths: How do we measure things people won't admit?

---

## Key Probability Rules

### Rule 1: Probabilities Sum to 1
For all possible outcomes of an experiment, the probabilities must sum to 1.
$$P(\text{all outcomes}) = 1$$

**Example**: When flipping a coin:
- P(Heads) + P(Tails) = 0.5 + 0.5 = 1 ✓

### Rule 2: Independence
Two events are **independent** if one occurring doesn't change the probability of the other.

**Example**: 
- Flipping a coin twice: The second flip's probability doesn't depend on the first
- P(2nd flip is Heads | 1st flip was Heads) = P(2nd flip is Heads) = 0.5

### Rule 3: Multiplication Rule (for independent events)
If events are independent:
$$P(A \text{ AND } B) = P(A) \times P(B)$$

**Example**: Getting Heads twice in a row:
$$P(\text{HH}) = P(\text{H}) \times P(\text{H}) = 0.5 \times 0.5 = 0.25$$

---

## Why Do We Need Probability Models?

### The Core Problem: Uncertainty & Incomplete Information
- We can't observe everything
- People don't always tell the truth
- Future events are unknown
- We need a framework to reason under uncertainty

### Benefits of Probabilistic Thinking
1. **Quantify uncertainty**: Put a number on "how uncertain" we are
2. **Make decisions**: Compare options by their probability of success
3. **Learn from data**: Update beliefs when we see new evidence
4. **Reveal hidden truths**: Infer what people won't say directly

---

## Questions for Students (Foundational Concepts)

1. **What's the difference between probability 0.7 and probability 0.3? Why does this matter?**
   - Expected answer: 0.7 means something is more likely to happen; we'd base different decisions on these

2. **If you roll a fair die, what's the sum of probabilities for all outcomes? Why?**
   - Expected answer: 1.0, because one outcome must occur; probabilities for all possibilities must sum to 1

3. **Give me an example of something in your life where you use probability thinking without realizing it.**
   - Expected answers: Choosing which route to take based on traffic, deciding whether to bring an umbrella, etc.

4. **Why can't a single event have probability greater than 1?**
   - Expected answer: Because 1 means "certain" and you can't be more certain than that

5. **If I flip a coin and it comes up Heads, does that change the probability that the next flip is Heads?**
   - Expected answer: No, each flip is independent; past results don't affect future probabilities

---

# SECTION 2: RANDOM VARIABLES

## What is a Random Variable?

### Definition
A **random variable** is a variable whose value is determined by the outcome of a random phenomenon. It's a function that assigns numerical values to the outcomes of an experiment.

**Symbol**: Usually denoted by capital letters: $X$, $Y$, $Z$, etc.

### Key Insight
A random variable is NOT random—the **outcome** is random. The variable itself is a well-defined rule for assigning numbers to outcomes.

### Examples

**Example 1: Coin Flip**
- Experiment: Flip a coin
- Random Variable $X$ = outcome of flip
- Possible values: {Heads, Tails} or {1, 0}

**Example 2: Die Roll**
- Experiment: Roll a die
- Random Variable $X$ = number showing
- Possible values: {1, 2, 3, 4, 5, 6}

**Example 3: Penalty Kick**
- Experiment: Player takes a penalty kick
- Random Variable $X$ = outcome
- Possible values: {Goal, No Goal} or {1, 0}

---

## Types of Random Variables

### 1. Discrete Random Variables
A random variable is **discrete** if it can take on a countable number of values (often integers).

**Characteristics**:
- Finite or countably infinite possible values
- "Gaps" between possible values
- We can list all possibilities

**Examples**:
- Number of heads in 10 coin flips: {0, 1, 2, ..., 10}
- Number of cars in a parking lot: {0, 1, 2, 3, ...}
- Test score (0-100): {0, 1, 2, ..., 100}
- Number of people with a certain opinion in a survey: {0, 1, 2, ..., n}

### 2. Continuous Random Variables
A random variable is **continuous** if it can take any value within a range (infinitely many values).

**Characteristics**:
- Uncountably infinite possible values
- No gaps—any number in a range is possible
- Smooth, flowing values

**Examples**:
- Height of a person: could be 5.6234... feet
- Temperature tomorrow: could be 72.31°F
- Time to complete a task: could be 15.3 seconds
- Weight of a newborn: could be 7.254 pounds

---

## Why Distinguish Between Discrete and Continuous?

The **type of random variable determines:**

1. **How we calculate probabilities**
   - Discrete: Use PMF (Probability Mass Function)
   - Continuous: Use PDF (Probability Density Function)

2. **How we visualize distributions**
   - Discrete: Bar charts (bars have width/area)
   - Continuous: Smooth curves

3. **What questions we ask**
   - Discrete: "What's P(X = 5)?" (specific value)
   - Continuous: "What's P(X ≤ 5)?" (need ranges, not single values)

---

## The Most Important Thing About a Random Variable: Its "Bars"

### The Probability Distribution
The **most important thing to know** about a random variable is **its bars**—what are the possible values and how likely is each one?

**This is called the Probability Mass Function (PMF) for discrete variables.**

### Visual Representation: The Histogram

A histogram shows:
- **X-axis**: Possible values of the random variable
- **Y-axis**: Probability of each value
- **Bar height**: How likely each outcome is (probability)
- **Bar area**: Represents the probability mass

### Key Property
All bars sum to 1 (because probabilities of all outcomes sum to 1).

### Examples

**Fair Coin Flip**:
```
P(X = Heads) = 0.5
P(X = Tails) = 0.5
Sum = 1.0 ✓
```
[BAR CHART: Two equal-height bars at 0.5]

**Unfair Coin Flip** (bent towards heads):
```
P(X = Heads) = 0.7
P(X = Tails) = 0.3
Sum = 1.0 ✓
```
[BAR CHART: Taller bar at 0.7, shorter bar at 0.3]

**Penalty Kick** (chance player scores):
```
P(X = Goal) = 0.79
P(X = Miss) = 0.21
Sum = 1.0 ✓
```

---

## Questions for Students (Random Variables)

1. **What's a random variable? Give an example from something you do daily.**
   - Expected answer: A variable whose value depends on something random. Example: "Whether I need an umbrella (depends on if it rains)"

2. **Is the random variable itself random, or is its outcome random? Explain the difference.**
   - Expected answer: The outcome is random; the rule for assigning values is fixed

3. **Name one discrete and one continuous random variable. How do they differ?**
   - Expected answers: Discrete: number of people; Continuous: height or temperature
   - Difference: Discrete has "gaps," continuous doesn't

4. **Look at this histogram of coin flips. Why must the bars sum to 1?**
   - Expected answer: Because the coin must land on something; all possible outcomes must account for 100% probability

5. **What's the difference between asking "What's P(X = 5)?" vs "What's P(X ≤ 5)?"?**
   - Expected answer: First asks for exact value; second asks for range. This matters for continuous variables

6. **Why is the "shape" of the distribution (where the bars are) more important than the actual number of trials?**
   - Expected answer: The shape tells you what outcomes are likely vs unlikely

---

# SECTION 3: DISTRIBUTIONS & THEIR TYPES

## What is a Probability Distribution?

### Definition
A **probability distribution** is a complete description of:
- All possible outcomes of a random variable
- The probability of each outcome

### Why Do We Need Distributions?

**The Problem**: Without a distribution, we don't know what outcomes are possible or how likely each is.

**The Solution**: A distribution is like a "recipe" or "template" that tells us:
- What kinds of outcomes to expect
- How often each occurs
- What's typical vs. unusual

### Distribution as a "Data-Making Machine"

A distribution is fundamentally a **story about how data gets created**.

If you **run** (sample from) the distribution many times:
- You get a collection of outcomes
- The histogram of these outcomes matches the distribution
- This is how real data gets generated

---

## Why Are There Different Types of Distributions?

### The Short Answer
Different **situations** require different distributions because:
- Some have 2 outcomes (yes/no), some have many
- Some are rare events, some are common
- Some have symmetry, some are skewed
- Real-world processes have different structures

### The Key Insight
**Choose a distribution based on the story of how the data is created**, not the data itself.

---

## Common Probability Distributions for Discrete Random Variables

### 1. BERNOULLI DISTRIBUTION
**Symbol**: $X \sim \text{Ber}(p)$

#### What It Models
A single trial with two possible outcomes:
- Success (1) with probability $p$
- Failure (0) with probability $1-p$

#### The Story
"Flip a coin once. It lands heads with probability $p$."

#### Parameters
- $p$ = probability of success (0 to 1)
- Single trial, single flip

#### When to Use It
- One penalty kick: does it go in?
- One medical test: is it positive?
- One person: do they support X?
- Does it rain tomorrow? (yes/no)

#### The Distribution
```
P(X = 1) = p
P(X = 0) = 1 - p
```

[BAR CHART: Two bars—one at height p for success, one at height (1-p) for failure]

#### Examples

**Fair Penalty Kick** ($p = 0.79$):
```
P(Goal) = 0.79
P(Miss) = 0.21
```

**Unfair Coin** ($p = 0.6$):
```
P(Heads) = 0.6
P(Tails) = 0.4
```

#### Important Property
**Mean (Expected Value)**: $E[X] = p$

This makes intuitive sense: if you repeat the trial many times, the fraction of successes approaches $p$.

---

### 2. BINOMIAL DISTRIBUTION
**Symbol**: $X \sim \text{Bin}(n, p)$

#### What It Models
The number of successes in $n$ independent trials, each with success probability $p$.

#### The Story
"Flip a coin $n$ times. Each flip has probability $p$ of being heads. Count how many heads you get."

#### Parameters
- $n$ = number of trials (1, 2, 3, ...)
- $p$ = probability of success on each trial (0 to 1)
- Must have **independence**: each trial's outcome doesn't affect the others

#### When to Use It
- Flipping a coin 10 times: count the heads
- Taking 5 penalty kicks: count how many go in
- Surveying 100 people: count how many support X
- Testing 50 products: count how many are defective

#### The Distribution
The binomial tells us: "What's the probability of getting exactly $k$ successes in $n$ trials?"

[BAR CHART: Multiple bars showing probabilities for 0, 1, 2, ..., n successes]

#### Examples

**Bin(10, 0.5)**: 10 fair coin flips
```
P(0 heads) ≈ 0.001
P(1 head)  ≈ 0.010
P(2 heads) ≈ 0.044
...
P(5 heads) ≈ 0.246  (most likely)
...
P(10 heads) ≈ 0.001
```
[BAR CHART: Bell-shaped, centered around 5]

**Bin(10, 0.9)**: 10 biased coin flips (90% heads)
```
Bars heavily skewed to the right
P(8 heads) ≈ 0.194
P(9 heads) ≈ 0.387  (most likely)
P(10 heads) ≈ 0.349
```
[BAR CHART: Skewed right, most probability at 9-10]

**Bin(100, 0.1)**: 100 trials with 10% success rate
```
Expected: ~10 successes
Distribution is skewed, but centered around 10
```

#### Important Property
**Mean (Expected Value)**: $E[X] = n \times p$

This is intuitive: if you do $n$ trials each with success probability $p$, you expect about $n \times p$ successes.

**Example**: 10 coin flips with $p = 0.5$ gives $E[X] = 10 \times 0.5 = 5$ heads expected.

#### Connection to Bernoulli
Binomial is the sum of independent Bernoulli random variables:
$$X \sim \text{Bin}(n, p) = X_1 + X_2 + ... + X_n$$
where each $X_i \sim \text{Ber}(p)$

**Intuition**: A single Bernoulli trial is just a Bin(1, p).

---

## Why These Two Distributions?

### The Hierarchy
- **Bernoulli**: 1 trial, 2 outcomes (yes/no)
- **Binomial**: $n$ trials, 2 outcomes per trial, count successes

### Why Start Here?
1. **Simplicity**: Easy to understand and visualize
2. **Ubiquity**: Many real-world questions fit this pattern
3. **Foundation**: Other distributions build on these concepts
4. **Interpretability**: Results are easy to explain to others

---

## Continuous Distributions (Brief Introduction)

### Key Difference from Discrete

For **discrete** random variables:
- We can ask: "What's P(X = exactly 5)?"
- We use PMF (Probability Mass Function)

For **continuous** random variables:
- We ask: "What's P(X ≤ 5)?" or "What's P(3 ≤ X ≤ 5)?"
- We use PDF (Probability Density Function)
- The probability of any single exact value is 0

### Why?
With infinite possible values, the probability of hitting any one exact value is infinitesimal.

---

## Questions for Students (Distributions)

1. **What's the key difference between a Bernoulli and a Binomial distribution?**
   - Expected answer: Bernoulli is one trial; Binomial is multiple independent trials

2. **If I flip a fair coin 100 times, what should I expect to get? Why?**
   - Expected answer: ~50 heads. Because E[X] = n × p = 100 × 0.5 = 50

3. **Can a Binomial distribution have $n = 1$? What would it be called?**
   - Expected answer: Yes; it's just a Bernoulli distribution (Bin(1, p) = Ber(p))

4. **If $p = 0.1$ and $n = 100$, what should the Binomial distribution look like? Sketch it.**
   - Expected answer: Bars mostly on the left (small values), with highest bar around 10

5. **Why do we need the requirement that trials be "independent" for Binomial?**
   - Expected answer: Because if one trial affects the next, the probabilities change; we can't just multiply

6. **A basketball player makes 70% of their free throws. They take 20. What's the distribution of makes?**
   - Expected answer: Bin(20, 0.7); expected value is 20 × 0.7 = 14 makes

7. **How is "the bars" (distribution) different from "one bar" (a single outcome)?**
   - Expected answer: Distribution shows all possible outcomes and their probabilities; one bar is just one outcome

---

# SECTION 4: PROBABILITY MASS FUNCTION (PMF) & PROBABILITY DENSITY FUNCTION (PDF)

## What is a PMF (Probability Mass Function)?

### Definition
For a **discrete random variable** $X$, the **PMF** is a function that gives the probability of each possible value:
$$\text{PMF: } f(x) = P(X = x)$$

### Interpretation
- **Input**: A specific value $x$
- **Output**: The probability that the random variable equals that value
- Called "mass" because probability is "concentrated" at specific points

### Properties of a PMF
1. **Non-negative**: $f(x) \geq 0$ for all $x$
2. **Sum to 1**: $\sum_{\text{all } x} f(x) = 1$
3. **Valid range**: Always between 0 and 1

### Example: Fair Die Roll

```
X = outcome of rolling a fair die
f(1) = 1/6 ≈ 0.167
f(2) = 1/6 ≈ 0.167
f(3) = 1/6 ≈ 0.167
f(4) = 1/6 ≈ 0.167
f(5) = 1/6 ≈ 0.167
f(6) = 1/6 ≈ 0.167
Sum = 1.0 ✓
```

[BAR CHART: Six equal-height bars, each at 1/6]

### Example: Bernoulli Distribution PMF

```
X ~ Ber(p) where p = 0.7
f(0) = P(X = 0) = 1 - p = 0.3
f(1) = P(X = 1) = p = 0.7
Sum = 0.3 + 0.7 = 1.0 ✓
```

[BAR CHART: Bar at 0 with height 0.3, bar at 1 with height 0.7]

---

## What is a PDF (Probability Density Function)?

### Definition
For a **continuous random variable** $X$, the **PDF** is a function $f(x)$ such that:
$$P(a \leq X \leq b) = \int_a^b f(x) \, dx$$

### Key Insight: The Critical Difference
- **PMF**: Direct probability of a value (P(X = x))
- **PDF**: Probability density; integrate to get probability over a range

### Interpretation
- **Height of the curve**: How "dense" probability is at that point
- **Area under the curve**: Actual probability
- The total area under a PDF is always 1

### Important Property
**For any single value**: $P(X = c) = 0$ for a continuous variable

This is counterintuitive but crucial: the probability of hitting any exact point is 0 because there are infinitely many points.

### Example: Normal Distribution PDF

The classic "bell curve":
```
Shape: Symmetric, bell-shaped
Peak: At the mean μ
Area under curve: Equals 1
Specific points: P(X = 172.5) = 0 (but P(170 ≤ X ≤ 175) > 0)
```

[CURVE DIAGRAM: Classic normal distribution bell curve]

---

## Comparing PMF and PDF

| Aspect | PMF (Discrete) | PDF (Continuous) |
|--------|----------------|------------------|
| **Random Variable** | Discrete (countable values) | Continuous (uncountable values) |
| **Probability of a value** | $P(X = x) = f(x)$ | $P(X = x) = 0$ |
| **Probability of a range** | $P(a \leq X \leq b) = \sum_{x=a}^b f(x)$ | $P(a \leq X \leq b) = \int_a^b f(x) dx$ |
| **Visualization** | Bar chart | Smooth curve |
| **Sum/Integral** | $\sum f(x) = 1$ | $\int f(x) dx = 1$ |
| **Height meaning** | Actual probability | Probability density |
| **Example** | Coin flips, die rolls | Height, temperature |

---

## Cumulative Distribution Function (CDF)

### Definition
The **CDF** for any random variable (discrete or continuous) is:
$$F(x) = P(X \leq x)$$

### Interpretation
"What's the probability that the random variable is at most $x$?"

### Properties
1. Always between 0 and 1
2. Never decreases (monotone increasing)
3. Starts at 0 as $x \to -\infty$
4. Ends at 1 as $x \to +\infty$

### Example: Fair Coin Flip

```
X ~ Ber(0.5)
F(0) = P(X ≤ 0) = 0.5  (just the probability of 0)
F(1) = P(X ≤ 1) = 1.0   (includes 0 and 1)
```

### Example: Fair Die Roll

```
X ~ Uniform on {1,2,3,4,5,6}
F(3) = P(X ≤ 3) = 3/6 = 0.5
F(5) = P(X ≤ 5) = 5/6 ≈ 0.833
```

---

## Why Distinguish Between PMF and PDF?

### The Core Reason: Mathematical Correctness

For **discrete** variables, saying "P(X = 5)" makes sense and is useful.

For **continuous** variables, saying "P(X = 5)" gives 0, which isn't useful. We need to ask about ranges instead.

### Practical Reasons

1. **Different computations**: Sums vs. integrals
2. **Different visualization**: Bars vs. curves
3. **Different interpretations**: Exact probabilities vs. probability density
4. **Different software**: Different functions to call

### The Fundamental Insight

Both PMF and PDF are ways of **encoding the same information**: the probability distribution.

But the mathematics reflects the underlying reality: discrete values are distinct points, continuous values form a continuum.

---

## Questions for Students (PMF and PDF)

1. **For a fair die, what's the PMF value f(3)? What does this tell you?**
   - Expected answer: 1/6 ≈ 0.167; there's a 16.7% chance of rolling a 3

2. **Why can't you use a bar chart for the height of people? What should you use instead?**
   - Expected answer: Too many possible values; use a smooth curve (PDF)

3. **If I have a PDF, how do I find the probability that X is between 170 and 175 cm?**
   - Expected answer: Integrate the PDF between 170 and 175; find the area under the curve

4. **For a continuous variable, what's P(X = exactly 172)? Why?**
   - Expected answer: 0; infinite possible values means probability of any one is 0

5. **What does the area under a PDF equal? Why?**
   - Expected answer: 1; because all possible outcomes must have total probability 1

6. **Draw a CDF for a fair coin flip. What shape should it have?**
   - Expected answer: Starts at 0, jumps to 0.5 at x=0, jumps to 1.0 at x=1

---

# SECTION 5: GENERATIVE VS DISCRIMINATIVE MODELS

## What Are These Terms?

These terms describe **two different philosophies for building models** and solving problems.

---

## GENERATIVE MODELS

### Definition
A **generative model** specifies the **complete probability distribution** of all variables, including how the data itself is generated.

### The Story
"I'm going to write down a complete story of how all the data comes into being."

### Characteristic Question
"If I **run** (simulate) this model, will I get realistic-looking data?"

### Example: Coin Flips

**Generative Model Story**:
1. We have a fair coin with P(Heads) = 0.5
2. Flip the coin $n = 10$ times
3. Each flip is independent
4. Count the number of heads

**Result**: We generate a number like 6, 5, 7, 4, 8, etc.

If we run this story 1000 times, we get 1000 numbers that look like real coin flip results.

### Example: Predicting Height from Age and Gender

**Generative Model**:
1. Choose random gender (50% male, 50% female)
2. Choose random age (uniform from 18-65)
3. Draw height from a normal distribution (parameters depend on age/gender)

**Result**: A realistic "person" with age, gender, and height

### How Generative Models Work

```
Model parameters (e.g., p for Bernoulli)
         ↓
Run the generative process
         ↓
Generate synthetic data
         ↓
Compare to real data
         ↓
Adjust parameters to match real data better
```

---

## DISCRIMINATIVE MODELS

### Definition
A **discriminative model** focuses only on the **conditional probability** of one variable given another, without modeling the full joint distribution.

### The Story
"I only care about predicting one thing from other things. I don't care how the input data is distributed."

### Characteristic Question
"Given an input, what's the probability of the output?"

### Example: Email Spam Filter

**Discriminative Model**:
- **Input**: The words in an email
- **Output**: Is it spam?
- **What we model**: P(Spam | Words in email)
- **What we ignore**: How are emails distributed? What's P(Words)?

**Result**: Given an email, we predict whether it's spam.

### Example: Predicting Height from Age and Gender

**Discriminative Model**:
- **Input**: Age and gender
- **Output**: Height
- **What we model**: P(Height | Age, Gender)
- **What we ignore**: How are people's ages distributed?

**Result**: Given age/gender, predict likely height.

### How Discriminative Models Work

```
Training data with inputs and outputs
         ↓
Learn patterns that predict output from input
         ↓
Given new input, predict output probability
         ↓
(We never generate fake inputs)
```

---

## Generative vs Discriminative: Direct Comparison

| Aspect | Generative | Discriminative |
|--------|-----------|-----------------|
| **What it models** | Full joint distribution P(all variables) | Conditional probability P(output\|input) |
| **Can generate data?** | Yes—run the model to create fake data | No—only predicts, doesn't create |
| **Complexity** | More complex (models everything) | Simpler (focuses on what matters) |
| **Transparency** | Very transparent—clear story of process | Less transparent—learns patterns |
| **Data efficiency** | Often needs more data | Often needs less data |
| **Missing data** | Can handle (generate missing parts) | Struggles with missing inputs |
| **Interpretability** | Highly interpretable | Often a "black box" |
| **Use case** | Understanding process, simulation, inference | Prediction, classification |

---

## When to Use Each?

### Use GENERATIVE Models When:

1. **You want to understand the process**
   - "How is data created?"
   - "What's the mechanism?"

2. **You need to generate synthetic data**
   - Simulation
   - Testing systems
   - What-if analysis

3. **Data is incomplete or missing**
   - Can fill in missing values by generating them

4. **You want interpretability**
   - Each part has a clear meaning
   - Easy to explain to non-experts

5. **You care about the full picture**
   - "What's the probability of both input AND output?"

### Use DISCRIMINATIVE Models When:

1. **You only care about prediction**
   - "Given X, predict Y"
   - No need to understand the full process

2. **You have lots of labeled training data**
   - Discriminative models excel with abundant data

3. **You want maximum prediction accuracy**
   - Often (but not always) more accurate

4. **You only need to predict one thing**
   - Focused on one output variable

5. **You care about efficiency**
   - Simpler, faster to train

---

## Why This Matters for the Palpatine Poll

The **Palpatine Poll is fundamentally generative**:

- We **specify a complete story** of how people answer
- We write down the **joint distribution** of:
  - How many harmless questions they answer yes to (H)
  - Whether they really support Palpatine (S)
  - What number they report (A)
- We **run this story** 1000 times to generate synthetic responses
- We **compare synthetic to real** to infer hidden support

This is classic generative modeling!

---

## Questions for Students (Generative vs Discriminative)

1. **The model says "Flip a coin, then look at the result and decide if you like heads." Is this generative or discriminative?**
   - Expected answer: Generative (we're specifying how data is created: coin flip → outcome)

2. **I want to predict whether someone will buy a product based on their age and income. Should I use generative or discriminative?**
   - Expected answer: Discriminative (we only care about P(Buy | Age, Income))

3. **Why might a generative model be better for handling incomplete data?**
   - Expected answer: It can generate the missing parts; a discriminative model needs the input to make predictions

4. **For the Palpatine Poll, why is a generative model necessary instead of discriminative?**
   - Expected answer: We need to model the entire process (harmless answers AND hidden truth), not just predict from one variable

5. **Can a generative model also be used for prediction? Can a discriminative model generate data?**
   - Expected answers: Yes and No; generative can predict (use P(Y|X)); discriminative cannot generate without knowing P(X)

---

# SECTION 6: PROBABILISTIC MODELS AS STORIES

## The Core Concept

### Definition
A **probabilistic model** is a mathematical description of how data gets generated. It's a **story** with random variables.

### The Key Insight
**Every probabilistic model has the same three components**:

1. **Define random variables**: What's uncertain?
2. **Specify distributions**: What are the possible values and their probabilities?
3. **Show how variables relate**: How do they depend on each other?

---

## Models as Stories, Not Just Math

### Why "Stories"?

The term "story" emphasizes that a model is:
- **Sequential**: Things happen in order
- **Causal**: Each step depends on previous steps
- **Interpretable**: A person should be able to understand it

### Example: The Flu Prediction Model

**The Story**:
1. Start with the true flu rate in the population (p)
2. For each person in the survey:
   - Flip a "coin" with probability p: do they have flu?
   - If yes: they have flu
   - If no: they don't have flu
3. Count total number with flu
4. This count is what we observe

**The Math**:
- True rate: $p \sim \text{Beta}(2, 2)$ (uncertain parameter)
- For person $i$: $X_i \sim \text{Ber}(p)$
- Total: $\sum X_i$ follows some distribution

**Key insight**: The story makes the math understandable.

---

## Three Uses of Probabilistic Models

### 1. GENERATE FAKE DATA
**Why**: Test if the model is reasonable

**How**:
1. Plug in parameter values
2. Run the model (sample from distributions)
3. See if you get data that "looks like" real data

**Example**: "If people really support Palpatine with probability 0.09, would we see data like this?"

### 2. COUNT TO ANSWER QUESTIONS
**Why**: Estimate probabilities from simulated data

**How**:
1. Generate 10,000 instances of data from the model
2. For each instance, check if event happened
3. Count: (# times event happened) / 10,000 = probability

**Example**: "In 10,000 simulations, how many resulted in nobody reporting 0?"

### 3. MULTIPLY ALONG THE STORY
**Why**: Calculate probability of one specific outcome

**How**:
1. Break the outcome into pieces following the story
2. Find probability of each piece
3. Multiply them together

**Example**: 
- P(H=3, S=1, A=4) = P(H=3) × P(S=1|H=3) × P(A=4|H=3,S=1)
- Three steps in the story, multiply probabilities

---

## Key Rule: Independence

### What It Means
Two random variables are **independent** if knowing one doesn't change the probability of the other.

**Notation**: $X \perp Y$ (read as "X is independent of Y")

### When It's True

**Example 1: Fair Coin Flips**
- Flip 1 is independent of Flip 2
- Knowing Flip 1 is Heads doesn't change P(Flip 2 = Heads) = 0.5

**Example 2: Random People**
- Person A's height is (roughly) independent of Person B's height
- Knowing A is tall doesn't change B's height distribution

### When It's False

**Example 1: Parent and Child Height**
- Not independent
- Knowing parent is tall increases probability child is tall

**Example 2: Today's Weather and Tomorrow's Weather**
- Not independent
- Today's weather predicts tomorrow's weather

### Why It Matters for Probability

If $X \perp Y$:
$$P(X \text{ and } Y) = P(X) \times P(Y)$$

This is the **multiplication rule** for independent events.

**Example**: 
$$P(\text{2 heads in a row}) = P(\text{H}_1) \times P(\text{H}_2) = 0.5 \times 0.5 = 0.25$$

---

## Example: The Simple Flu Model

### The Story

**Step 1: Nature chooses the flu rate**
- There's an unknown true probability $p$ that any random person has flu
- $p \sim \text{Uniform}(0, 1)$ (we're completely uncertain)

**Step 2: For each survey respondent**
- We draw from $X_i \sim \text{Ber}(p)$
- Interpretation: Bernoulli "coin flip" with probability $p$
- Result: 1 (has flu) or 0 (doesn't have flu)

**Step 3: Pool the results**
- Total number with flu: $\sum_{i=1}^{n} X_i$
- This follows $\text{Bin}(n, p)$

**Step 4: We observe this number**
- In our sample, let's say 25 out of 100 had flu
- This is our data: $(n=100, \text{count}=25)$

### Using the Model

**Generate fake data**:
- Assume $p = 0.3$ (30% of population has flu)
- Generate $n=100$ Bernoulli trials with $p=0.3$
- Might get 28, 32, 31, etc. (should be around 30)
- Does this match real data? If yes, $p=0.3$ is plausible

**Count to answer questions**:
- "What's P(fewer than 20 have flu)?"
- Simulate 10,000 datasets with $p=0.25$
- Count: in how many is the count < 20?
- Result: probability ≈ 0.0013 (very rare)

**Multiply along story**:
- "P(p=0.3 AND observe 25 out of 100)?"
- P(observe 25 | p=0.3) = $\binom{100}{25} (0.3)^{25} (0.7)^{75}$ ≈ 0.00073
- P(p=0.3) = 1 (uniform, density = 1)
- P(both) ≈ 0.00073

---

## Questions for Students (Models as Stories)

1. **Tell me the three components of a probabilistic model.**
   - Expected answer: (1) Random variables—what's uncertain, (2) Distributions—possible values and probabilities, (3) Relationships—how variables depend

2. **Why is "story" a good word for what a probabilistic model is?**
   - Expected answer: It's sequential, interpretable, shows cause-and-effect

3. **You have a coin flip. If you use it to predict tomorrow's weather, why would that be a bad model?**
   - Expected answer: The coin flip is independent of weather, but real weather depends on today's weather

4. **In a Binomial(10, 0.5) model, which trials are independent? Why does this matter?**
   - Expected answer: All trials are independent; lets us multiply probabilities together

5. **I want to generate 100 fake datasets using a Bernoulli(0.6) model. What are the steps?**
   - Expected answer: (1) Set p=0.6, (2) Run Ber(0.6) 100 times, (3) For each run, flip and record outcome

---

# SECTION 7: THE LIST EXPERIMENT / SENSITIVE QUESTIONS PROBLEM

## The Core Problem

### The Situation
**Some people won't tell the truth about sensitive topics.**

Examples:
- Do you use illegal drugs?
- Do you cheat on exams?
- Do you hold xenophobic views?
- Do you support an authoritarian regime?

### Why They Won't Answer Truthfully
- **Fear of consequences**: Legal trouble, social judgment
- **Social desirability bias**: Want to appear better
- **Privacy concerns**: Don't want information recorded
- **Shame or guilt**: Uncomfortable admitting certain things

### The Challenge
**Direct questions get systematically false answers.**

If you ask "Do you support Palpatine?" directly:
- True supporters might deny it (fear)
- Opponents might agree (to seem cooperative)
- You get biased data

---

## The Solution: Hide the Question in a List

### The Idea
**Ask about the sensitive question hidden among harmless questions.**

Instead of:
> "Do you support Palpatine?"

Do this:
> "How many of the following do you agree with?"
> 1. Do you like surprises?
> 2. Do you prefer beaches to mountains?
> 3. Do you like paper books over e-books?
> 4. Would you rather have more time than more money?
> 5. Do you prefer home holidays over foreign travel?
> 6. **Do you support Palpatine?**
>
> **Answer only with a number (0-6). Don't say which ones.**

### Why This Works: The Insight

**Individual responses**: Tell us nothing about question 6
- Person says "3"
- We don't know: Do they support Palpatine or not?

**Aggregate responses**: Reveal hidden support
- If everyone answered the first 5 questions honestly
- And the first 5 average to 2.5
- But actual answers average 3.5
- The difference (1.0) = hidden support

---

## The Mathematical Framework

### The Setup

**Notation**:
- $H_i$ = number of "yes" answers to harmless questions for person $i$ (out of 5)
- $S_i$ = whether person $i$ really supports Palpatine (0 or 1)
- $A_i$ = what person $i$ reports (0 to 6)

### The Relationship

$$A_i = H_i + S_i$$

**Interpretation**:
- If you answer 3 harmless questions with "yes" and support Palpatine: $A_i = 3 + 1 = 4$
- If you answer 2 harmless questions with "yes" and don't support: $A_i = 2 + 0 = 2$

### The Aggregate Calculation

**Expected value**:
$$E[A] = E[H] + E[S]$$

**Rearranged**:
$$E[S] = E[A] - E[H]$$

**In words**:
> The proportion supporting Palpatine = (Average reported answer) - (Average harmless answers)

---

## Why This Reveals Truth

### The Scenario

**Two groups take the survey**:

1. **Group 1**: Asked only the 5 harmless questions
   - Average answer: 2.5
   - This estimates $E[H]$

2. **Group 2**: Asked all 6 questions (with Palpatine hidden)
   - Average answer: 3.5
   - This estimates $E[H] + E[S]$

### The Inference

$$E[S] = 3.5 - 2.5 = 1.0$$

Wait, that can't be right. $E[S]$ should be between 0 and 1, not 1.0.

**Correction**: 
The true calculation is about **proportions**, not just expected values.

If Group 1 averages 2.5 harmless yeses out of 5:
- Proportion of harmless support: $p = 2.5 / 5 = 0.5$

If Group 2 averages 3.5:
- This includes harmless + support for Palpatine
- Subtract expected harmless: $3.5 - 2.5 = 1.0$
- But we need to think about this as a **count** not a probability

**Better approach**:
- Average harmless answers: 2.5 per person
- Average total answers: 3.5 per person
- Difference: 1.0 = number answering "yes" to Palpatine
- Since there are 1000 people: 1000 people × 1.0 yeses = 1000 Palpatine supports
- But wait, only one Palpatine question, so this should be (1000 × 1.0) / 1 = 1.0... 

**Actually**: Looking at the study that motivated this:
- Direct question: 1 in 10 said yes (10%)
- List method: 1 in 4 said yes (25%)
- **The list method revealed hidden support**.

---

## The Palpatine Poll Study Reference

### The Real Study
In Vietnam (2023), researchers asked about cheating with ChatGPT:

**Direct question**:
- 9.6% admitted to cheating

**List method** (hiding cheating among harmless questions):
- ~23.7% revealed

### The Inference
$$\text{True rate} = \text{(List average)} - \text{(Harmless average)}$$

With proper analysis, this revealed that actual cheating was much higher than direct responses suggested.

---

## Why the List Method Works

### Key Insight #1: Randomness Protects Privacy

When you report just a number (0-6), nobody knows which questions you answered yes to.

- You're protected by **aggregate results**
- Nobody can single you out

### Key Insight #2: Expected Values Reveal Totals

If people are honest on harmless questions:
- Average harmless answers = fixed, known value
- Difference from total = support for hidden question

### Key Insight #3: Requires Independence

**Critical assumption**: 
Answers to harmless questions are **independent** of answers to Palpatine question.

If someone's answers are correlated (e.g., Palpatine supporters also like surprises), the method fails.

---

## The Assumptions (Critical)

1. **Harmless questions are truly 50/50**
   - If everyone naturally likes beaches, the baseline changes
   - "Pick questions near 50/50"

2. **People are honest about harmless questions**
   - Nobody has incentive to lie
   - Safe questions

3. **Answers to 5 harmless are independent of Palpatine answer**
   - Being a Palpatine supporter doesn't predict if you like surprises
   - Usually reasonable

4. **People follow instructions**
   - Actually count all 6 answers
   - Report honestly

---

## Questions for Students (List Experiments)

1. **Why doesn't asking "Do you support Palpatine?" directly give us the truth?**
   - Expected answer: People fear consequences, so lie

2. **If you report "3" on the list, does that reveal your Palpatine support? Why or why not?**
   - Expected answer: No; we don't know which 3 questions you answered yes to

3. **If the average of Group 1 (harmless only) is 2.6 and Group 2 (all 6) is 3.5, what does this suggest about Palpatine support?**
   - Expected answer: The difference (3.5 - 2.6 = 0.9) suggests hidden support

4. **Why is it important that the harmless questions are answered truly 50/50?**
   - Expected answer: If not, the baseline changes and we can't isolate the hidden question effect

5. **If everyone who supports Palpatine also loves surprises, would the list method still work?**
   - Expected answer: No; the assumption of independence would be violated

---

# SECTION 8: THE PALPATINE POLL CASE STUDY

## Complete Overview

### The Setup

**Context**:
- Emperor Palpatine (Star Wars villain) rules a galaxy
- Political surveys are dangerous: supporting him is dangerous
- Asking directly: "Do you support Palpatine?" gets lies

**Our Goal**:
- Estimate the **true proportion** of Palpatine supporters using a list experiment

---

## The Complete Model Story

### Step 1: The Harmless Questions

**Random Variable**: $H$ = number of "yes" answers to 5 harmless questions

**The Story**:
- Each person answers 5 questions
- Each question: person answers "yes" with probability 0.5
- We count total "yes" answers
- Possible values: 0, 1, 2, 3, 4, 5

**Distribution**: $H \sim \text{Binomial}(n=5, p=0.5)$

**Intuition**: Like flipping a fair coin 5 times

**The PMF**:
```
P(H = 0) = 0.031  (3.1% chance)
P(H = 1) = 0.156  (15.6% chance)
P(H = 2) = 0.313  (31.3% chance)
P(H = 3) = 0.313  (31.3% chance)
P(H = 4) = 0.156  (15.6% chance)
P(H = 5) = 0.031  (3.1% chance)
```

**Visualization**: Bell-shaped histogram centered at 2.5

---

### Step 2: The Secret Question

**Random Variable**: $S$ = whether person really supports Palpatine

**The Story**:
- Each person has some true opinion (secret)
- Nobody answers directly; this is hidden
- They support Palpatine with probability $p = 0.09$ (estimated)

**Distribution**: $S \sim \text{Bernoulli}(p=0.09)$

**Intuition**: Flip a biased coin; 9% heads (support)

**The PMF**:
```
P(S = 0) = 0.91  (91% don't support, won't admit it)
P(S = 1) = 0.09  (9% do support, won't admit it)
```

---

### Step 3: The Answer They Report

**Random Variable**: $A$ = what the person actually reports (0 to 6)

**The Relationship**:
$$A = H + S$$

**The Story**:
- Person answers the 6-question list
- They count honestly: harmless yeses + Palpatine yes
- They report that number

**Interpretation**:
- If $H = 2$ and $S = 0$ (doesn't support): reports 2
- If $H = 3$ and $S = 1$ (does support): reports 4
- If $H = 5$ and $S = 1$ (does support): reports 6

**The PMF**:
Since $A = H + S$:
```
P(A = 0) = P(H=0, S=0) = 0.031 × 0.91 ≈ 0.028
P(A = 1) = P(H=1, S=0) + P(H=0, S=1) ≈ 0.171
P(A = 2) = P(H=2, S=0) + P(H=1, S=1) ≈ 0.299
P(A = 3) = P(H=3, S=0) + P(H=2, S=1) ≈ 0.313
P(A = 4) = P(H=4, S=0) + P(H=3, S=1) ≈ 0.159
P(A = 5) = P(H=5, S=0) + P(H=4, S=1) ≈ 0.028
P(A = 6) = P(H=5, S=1) ≈ 0.003
```

**Visualization**: Bell-shaped but shifted; centered around 2.5 + 0.09 = 2.59

---

## Running the Model

### What We Do

Generate synthetic responses from the model and compare to real data.

### Step-by-Step

**For 1000 simulated people**:

1. For each person $i = 1$ to 1000:
   - Sample $H_i \sim \text{Bin}(5, 0.5)$
   - Sample $S_i \sim \text{Ber}(0.09)$
   - Compute $A_i = H_i + S_i$
   - Record $A_i$

2. Compute distribution of $A$ values:
   - Count: how many reported 0? 1? 2? ... 6?
   - Divide by 1000 to get fractions

3. Compare to real data distribution:
   - Real: 17% reported 1, 30% reported 2, etc.
   - Model: ~17% reported 1, ~30% reported 2, etc.
   - Do they match?

### Results (from the presentation)

**Real data distribution** (1000 people):
- 17% reported 1
- 30% reported 2
- 33% reported 3
- 17% reported 4
- 4% reported 5
- <1% reported 6
- **Average**: 2.62

**Model simulation** (p=0.09, n=1000):
- ~19% reported 1
- ~29% reported 2
- ~32% reported 3
- ~16% reported 4
- ~5% reported 5
- ~<1% reported 6
- **Average**: 2.58

**Conclusion**: Model matches reality well! The parameter $p = 0.09$ is plausible.

---

## Inferring Hidden Support

### The Calculation

From real data:
- Average answer: 2.62
- Average harmless answers: Should be ~2.5 (expected value of Bin(5, 0.5))
- Difference: 2.62 - 2.5 = 0.12

**But this is about expected values, not proportions.**

### Proper Interpretation

Expected value of $A$:
$$E[A] = E[H + S] = E[H] + E[S] = 2.5 + 0.09 = 2.59$$

From data, we estimate:
$$\hat{E}[A] = 2.62$$

Rearranged:
$$\hat{E}[S] = 2.62 - 2.5 = 0.12$$

**Interpretation**: Approximately 9-12% support Palpatine (hidden support)

---

## Risk: Giving People Away

### The Problem

An answer of 6 means **yes to everything, including Palpatine**.
An answer of 0 means **no to everything, including Palpatine**.

These are dangerous answers!

### The Math

**P(A = 6)**:
$$P(A = 6) = P(H = 5 \text{ AND } S = 1)$$
$$= P(H = 5) \times P(S = 1 | H = 5)$$
$$= P(H = 5) \times P(S = 1)  \quad \text{(by independence)}$$
$$= 0.031 \times 0.09$$
$$≈ 0.003$$

**Interpretation**: About 3 people per 1000 would report 6, accidentally revealing support.

**P(A = 0)**:
$$P(A = 0) = P(H = 0 \text{ AND } S = 0)$$
$$= 0.031 \times 0.91$$
$$≈ 0.028$$

**Interpretation**: About 28 people per 1000 would report 0, revealing opposition (if that's dangerous).

### The Protection Trade-off

The list experiment provides **privacy** but imperfectly:
- People who answer extreme (0 or 6) are exposed
- Protection requires trusting the aggregate, not analyzing individual answers
- In a totalitarian regime, 28 per 1000 is still too many at risk

---

## Questions for Students (Palpatine Poll)

1. **What's the distribution of H? What values are possible and how likely is each?**
   - Expected answer: Bin(5, 0.5); values 0-5, with 2 and 3 most likely (~31% each)

2. **If someone reports 4, what are the possible combinations of (H, S)?**
   - Expected answers: (4,0)—answers 4 harmless yes, (3,1)—answers 3 harmless yes and supports, (2,2)—impossible, etc.
   - Correct: Only (4,0), (3,1)

3. **What's the expected value of H? Of S? Of A?**
   - Expected answers: E[H] = 5 × 0.5 = 2.5; E[S] = 0.09; E[A] = 2.59

4. **From the real data (average 2.62), what can we infer about Palpatine support?**
   - Expected answer: About 12% support (2.62 - 2.5 = 0.12)

5. **Why is an answer of 6 or 0 dangerous? What are the probabilities?**
   - Expected answers: 
     - A=6 means yes to Palpatine (give yourself away): P≈0.003 (0.3%)
     - A=0 means no to everything (reveal opposition): P≈0.028 (2.8%)

6. **Does the model match the real data? What does that mean?**
   - Expected answer: Yes; simulated average ~2.58, real average 2.62; model is plausible

---

# SECTION 9: ADDITIONAL PROBLEMS & EXTENSIONS

## Problem 1: Different Support Rates

### Scenario
Suppose the true support for Palpatine is **15%** instead of 9%.

### The Task
1. What should the average answer be?
2. Generate a histogram for this scenario
3. Compare to the p=0.09 scenario

### Solution

**E[A] with p=0.15**:
$$E[A] = E[H] + E[S] = 2.5 + 0.15 = 2.65$$

**Comparison**:
- p=0.09: E[A] ≈ 2.59
- p=0.15: E[A] ≈ 2.65
- Difference: 0.06 per person = 6 per 100 = 60 per 1000

**Histogram**: Shifted slightly right compared to p=0.09

**Inference**: If we see average 2.65, we'd infer 15% support

---

## Problem 2: Harmful Harmless Questions

### Scenario
Suppose one "harmless" question isn't actually 50/50. It's 80% yes because everyone likes it.

Question: "Do you like food?" (80% yes, 20% no)

### The Problem
The baseline shifts. Now people are expected to answer more "yes" responses overall.

### The Task
1. Calculate new E[H]
2. Explain why this breaks the inference
3. How would you fix it?

### Solution

**New E[H]**:
If people answer:
- 50% yes to Q1
- 50% yes to Q2
- 50% yes to Q3
- 50% yes to Q4
- **80% yes to Q5** ← This one

Expected: $0.5 + 0.5 + 0.5 + 0.5 + 0.8 = 3.3$

**Why it breaks**:
- We expect harmless to average 3.3, not 2.5
- If real average is 3.5, difference is only 0.2
- We'd infer just 2% support (instead of actual 9%)

**How to fix**:
- Ask people ONLY Q1-4 in one group
- Ask people Q1-6 in another group
- Calculate: (difference in averages)
- Or: Survey only the first 4 questions separately to get true baseline

**Key lesson**: All harmless questions must truly be 50/50

---

## Problem 3: Correlated Questions

### Scenario
Suppose Palpatine supporters also happen to like surprises (they're adventurous).

So:
- P(like surprises | support Palpatine) = 80%
- P(like surprises | don't support) = 40%

These are correlated!

### The Task
1. Does this break the method?
2. What would the inference error be?
3. How would you detect it?

### Solution

**Does it break the method?**
Yes! The assumption of independence is violated.

**Why the inference fails**:
- Palpatine supporters report higher H values (because they answer yes to more questions)
- The method assumes **high H + high S are independent**
- But they're now positively correlated
- The difference (total - baseline) **underestimates** support

**What happens**:
- Actual support: 9%
- Method inference: ~5% (too low)
- Error: misses ~4% of support

**How to detect**:
- Compare the survey to an anonymous poll (if available)
- Check if answers to harmless questions correlate with support
- Use advanced statistical techniques (conditional probability analysis)

**Lesson**: Independence assumption is critical

---

## Problem 4: Extreme Responders

### Scenario
Some people always answer yes (or always no) regardless of the question.

Example: 5% of people answer "yes" to everything

### The Task
1. How does this change the distributions?
2. What inference error results?
3. How would you protect against this?

### Solution

**How it changes**:
- P(A = 6) increases (more people answer yes to everything)
- P(A = 0) might decrease (fewer people answer no to everything)
- The distribution becomes less bell-shaped

**Inference error**:
- These people inflate the average
- We'd overestimate hidden support
- Example: If 5% answer yes to everything, they contribute 5% × 1 = 0.05 to average A
- We might interpret this as 5% support, when it's actually just careless responding

**Protection**:
- Quality control on responses
- Remove obvious pattern responders
- Ask validation questions ("Did you read carefully?")
- Statistical modeling to detect and adjust for pattern responses

---

## Problem 5: The Math Behind Joint Probabilities

### Scenario
Calculate P(A = 3) analytically (not just by simulation).

### The Task
1. What are the ways to get A = 3?
2. Calculate the probability of each combination
3. Sum them

### Solution

**Ways to get A = 3**:
- (H=3, S=0): Answer 3 harmless yes, don't support Palpatine
- (H=2, S=1): Answer 2 harmless yes, do support Palpatine

**Calculate each**:

P(H=3, S=0):
$$P(H=3) = \binom{5}{3} (0.5)^3 (0.5)^2 = 10 \times 0.03125 = 0.3125$$
$$P(S=0) = 0.91$$
$$P(H=3, S=0) = 0.3125 \times 0.91 = 0.28438$$

P(H=2, S=1):
$$P(H=2) = \binom{5}{2} (0.5)^2 (0.5)^3 = 10 \times 0.03125 = 0.3125$$
$$P(S=1) = 0.09$$
$$P(H=2, S=1) = 0.3125 \times 0.09 = 0.02813$$

**Sum**:
$$P(A=3) = 0.28438 + 0.02813 = 0.31251 ≈ 0.313$$

**Interpretation**: About 31.3% of people report 3

---

## Problem 6: Inferring the True Parameter

### Scenario
We observe data: average answer is 2.62.

We want to infer: What's the true p (support rate)?

### The Task
1. Write down the relationship between observed data and unknown p
2. Solve for p
3. Check if this matches the true p = 0.09

### Solution

**Relationship**:
$$E[A] = E[H] + E[S]$$
$$E[A] = 2.5 + p$$

**From data**:
$$\hat{E}[A] = 2.62$$

**Solve for p**:
$$2.62 = 2.5 + \hat{p}$$
$$\hat{p} = 0.12$$

**Comparison**:
- True p: 0.09 (9%)
- Estimated p: 0.12 (12%)
- Error: 3 percentage points too high

**Why the error**?
- Sampling variability (with only 1000 people)
- Possible violations of assumptions
- Measurement error

**Lesson**: This is the basic inference method! In practice, use more sophisticated statistics to account for uncertainty.

---

## Problem 7: What If People Lie About Harmless Questions?

### Scenario
Suppose 10% of people lie on the harmless questions too (say yes when true answer is no).

### The Task
1. How does this change E[H]?
2. What inference error results?
3. Is the method salvageable?

### Solution

**Effect on E[H]**:
Without lying:
- For each question: 50% natural yes
- Expected from 5 questions: 2.5

With lying:
- 10% lie on each question
- Probability person says yes: P(natural yes) + P(natural no but lie yes)
- = 0.5 + (0.5 × 0.1) = 0.55

Expected:
- E[H] = 5 × 0.55 = 2.75 (instead of 2.5)

**Inference error**:
- We expect baseline 2.5 but true baseline is 2.75
- If observed average is 2.62:
  - Method says: 2.62 - 2.5 = 0.12 support
  - Reality: 2.62 - 2.75 = -0.13 (negative! impossible!)
  - Or: People are lying on harmless questions

**Is it salvageable?**
- If lying is systematic and known: Yes, adjust the baseline
- If unknown: This breaks the method
- Better: Use questions people have no incentive to lie about

**Lesson**: Method assumes honest responses to harmless questions

---

## Problem 8: Challenge Problem—Multiple Hidden Questions

### Scenario
Suppose the list has 2 hidden questions:
- Do you support Palpatine?
- Do you use illegal substances?

And 4 harmless questions.

### The Task
Can you estimate support for BOTH? Explain why or why not.

### Solution

**Can you estimate both?**
No! You'd have only one extra variable (the sum of the 2 hidden yes answers) but 2 unknowns.

**The math**:
- $A = H + S_1 + S_2$
- You observe $A$ but not $S_1$ and $S_2$ separately
- You can't solve for two unknowns with one equation

**What you CAN do**:
- Estimate: P(support Palpatine OR use substances) = ?
- But not: P(support Palpatine) and P(use substances) separately

**Fix**:
- Use two separate list experiments (different random samples)
- Or use advanced statistical methods (Bayesian hierarchical models)
- Or use additional information to identify the parameters

**Lesson**: The method works for 1 hidden question per list

---

## Questions for Students (Additional Problems)

1. **If support increased from 9% to 15%, what would the average answer change to?**
   - Expected answer: 2.59 → 2.65 (increase of 0.06)

2. **If a "harmless" question is 80% yes instead of 50%, what happens to your inference?**
   - Expected answer: You overestimate support (baseline is wrong)

3. **Why does correlation between harmless and hidden questions break the method?**
   - Expected answer: Assumption of independence is violated; high H values correlate with high S

4. **How would you test whether the list experiment actually worked?**
   - Expected answer: Compare to an anonymous poll, check for obvious patterns, validate quality

5. **Can you estimate two hidden questions with one list experiment? Why or why not?**
   - Expected answer: No; one equation, two unknowns (needs two list experiments)

---

# SECTION 10: COMMON MISCONCEPTIONS

## Misconception 1: "Random means unpredictable"

### The Wrong Belief
"If something is random, I can't say anything about it."

### The Reality
Random variables are **completely predictable in distribution**, even if individual outcomes are unpredictable.

**Example**:
- Individual coin flip: unpredictable (could be H or T)
- 1000 coin flips: predictable (~500 will be heads)
- The distribution is deterministic

### The Lesson
Randomness in individual outcomes doesn't prevent patterns in aggregates.

---

## Misconception 2: "Probability of 0.5 means no information"

### The Wrong Belief
"If P = 0.5, I'm completely uncertain."

### The Reality
Uncertainty is relative. P = 0.5 is less certain than P = 0.9 but more certain than P = 0.01.

**Example**:
- Coin flip: P = 0.5, maximally uncertain
- Loaded die (60% ones): P = 0.6, somewhat confident in getting a one
- Rare disease: P = 0.001, very confident someone doesn't have it

### The Lesson
Probability measures degrees of uncertainty, not binary "information" vs "no information."

---

## Misconception 3: "The multiplication rule always applies"

### The Wrong Belief
"P(A and B) = P(A) × P(B) always."

### The Reality
This only works if A and B are **independent**.

**Example** (wrong):
- P(person is tall) = 0.3
- P(person plays basketball) = 0.1
- P(tall AND plays basketball) = 0.3 × 0.1 = 0.03? NO!

**Why**: Tall people are more likely to play basketball (not independent).

**Correct formula**:
$$P(A \text{ and } B) = P(A) \times P(B | A)$$

### The Lesson
Always check independence before using the multiplication rule.

---

## Misconception 4: "More data always means more accuracy"

### The Wrong Belief
"If we survey 10,000 people instead of 1000, we'll get a perfect answer."

### The Reality
More data helps, but other factors matter:
- **Quality of data**: Are people answering honestly?
- **Model correctness**: Is your model realistic?
- **Assumption violations**: Is independence really true?

**Example**:
- 10,000 people lying about sensitive topics = bad data
- 100 people answering honestly = better data

### The Lesson
Data quantity matters, but quality and model correctness matter more.

---

## Misconception 5: "Correlation means causation"

### The Wrong Belief
"If X and Y are correlated, X causes Y."

### The Reality
Correlation can arise from:
1. X causes Y
2. Y causes X
3. Z causes both X and Y
4. Pure coincidence (in small samples)
5. Other complex relationships

**Example**:
- Ice cream sales and deaths are correlated (both higher in summer)
- Ice cream doesn't cause deaths; heat causes both

### The Lesson
Correlation is a start, but causation requires careful reasoning and often intervention (experiments).

---

## Misconception 6: "The distribution doesn't matter, only the mean"

### The Wrong Belief
"If E[X] = 100, that's all I need to know."

### The Reality
The **entire distribution** matters.

**Example**:
Two games with E[payoff] = $100:

Game A: Always win exactly $100
Game B: 50% chance win $200, 50% chance win $0

Same mean, very different risk!

### The Lesson
Mean is important but incomplete. Always consider the full distribution.

---

## Misconception 7: "Model = reality"

### The Wrong Belief
"Our probabilistic model is exactly how the real world works."

### The Reality
All models are approximations. The question is: **Is this model useful?**

**Example**:
- Bernoulli model assumes independence
- Real human opinions might be influenced by friends, media, etc.
- But the model is still useful for rough estimates

### The Lesson
Models are simplifications. Usefulness depends on whether they capture the important features.

---

## Misconception 8: "Simulation is less rigorous than math"

### The Wrong Belief
"Running a simulation 1000 times is less formal than calculating analytically."

### The Reality
Simulation is a **perfectly valid method**:
- Exact for the model (sampling error only)
- Often easier to understand
- Sometimes the only practical way

**Example**:
- Calculate P(A=3) analytically: complex binomial math
- Simulate 1000 instances, count: simple and clear
- Both give same answer (within sampling error)

### The Lesson
Simulation is a powerful tool. For learning, often better than formulas.

---

## Misconception 9: "Privacy means no data collection"

### The Wrong Belief
"The list experiment reveals nothing personal; it's completely private."

### The Reality
Privacy is imperfect. Extreme answers (0 or 6) still risk exposure.

**Lesson**: The list experiment improves privacy but doesn't guarantee it. In dangerous regimes, even aggregate methods have risks.

---

## Misconception 10: "If the model matches data, it's correct"

### The Wrong Belief
"Because our simulated distribution matches real data, we know the true parameter."

### The Reality
Multiple parameter values might produce similar distributions. You need more to claim correctness.

**Example**:
- p = 0.08 might also produce average ~2.6
- p = 0.10 might also produce average ~2.6
- Which is true? You need more information (confidence intervals, hypothesis tests)

### The Lesson
Model-data match is necessary but not sufficient for claiming truth.

---

## Questions for Students (Common Misconceptions)

1. **If something is random, can we predict it at all?**
   - Expected answer: Not individual outcomes, but patterns in aggregates (distribution)

2. **Is a probability of 0.5 the same as having no information?**
   - Expected answer: No; it's maximal uncertainty but not "no information" — we know it's fair

3. **If P(A) = 0.4 and P(B) = 0.3, is P(A and B) = 0.12? When is this true?**
   - Expected answer: Only if A and B are independent; otherwise need P(B|A)

4. **Does surveying 100,000 people always give better results than 1000?**
   - Expected answer: Not if they're all lying; quality matters more than quantity

5. **If X and Y are correlated, can you conclude X causes Y?**
   - Expected answer: No; could be Y causes X, Z causes both, or coincidence

6. **Is knowing E[X] = 50 enough to understand the distribution?**
   - Expected answer: No; you need to know the spread and shape

7. **Is a computer simulation less rigorous than a mathematical formula?**
   - Expected answer: No; both are valid, simulation is often clearer for learning

8. **If our model produces data matching reality, is the model correct?**
   - Expected answer: Not necessarily; other parameters might also work

---

# FINAL SUMMARY: KEY TAKEAWAYS

## Conceptual Framework

1. **Random Variables**: Rules that assign numbers to random outcomes
   - Discrete: countable values (Bernoulli, Binomial)
   - Continuous: infinite values (Normal, Uniform)

2. **Distributions**: Complete description of possible outcomes and probabilities
   - Discrete: PMF (probability mass function)
   - Continuous: PDF (probability density function)
   - Why types differ: mathematical correctness for each setting

3. **Probabilistic Models**: Stories with random variables
   - Generative: specify full joint distribution
   - Discriminative: focus on prediction only
   - Both are useful in different contexts

4. **Inference**: Learning from data
   - How to estimate unknown parameters
   - How to test model assumptions
   - How to handle uncertainty

## Technical Skills

1. **Reading a distribution**: Understand what outcomes are likely vs. unlikely
2. **Computing expectations**: E[X] for discrete and continuous
3. **Using independence**: When to apply multiplication rule
4. **Thinking generatively**: Tell a story of how data comes to be
5. **Simulation**: Generate fake data to understand models
6. **Aggregation**: Extract hidden signals from noisy data

## The Palpatine Poll Lesson

**The core insight**: 
> By hiding sensitive questions among harmless ones and analyzing aggregate responses, you can infer hidden truths while protecting individual privacy.

**This works because**:
1. Independence assumption holds (harmless answers ≠ hidden answer)
2. Aggregate patterns reveal individual behaviors
3. Individual answers reveal nothing (privacy protection)

**This fails when**:
1. Harmless questions are not 50/50
2. People lie about harmless questions
3. Harmless and hidden answers are correlated
4. Extreme responders exist

**Applications**:
- Sensitive topic surveys
- Policy evaluation in oppressive regimes
- Academic dishonesty detection
- Any hidden behavior measurement

---

# TEACHING TIPS

## For Maximum Learning

1. **Always start with the story**, not the math
   - "Here's how data gets made..."
   - Then show the probability distributions
   - Finally, show the equations

2. **Use simulation as your primary tool**
   - Students understand simulation intuitively
   - Math becomes clearer after seeing simulation
   - Mistakes become obvious in simulation

3. **Ask students to predict first**
   - "If we increase p, what happens to E[X]?"
   - "Do you think this model matches the data?"
   - Then show them they're right (or discuss why they're wrong)

4. **Use real examples constantly**
   - Medical testing, politics, surveys
   - Makes abstract concepts concrete

5. **Emphasize independence and assumptions**
   - This is where models fail in practice
   - Forces deeper thinking about the setup

6. **Have students generate their own models**
   - "Model how many people will attend class"
   - "Model how many will pass the test"
   - Builds deep understanding

---

# ASSESSMENT QUESTIONS

## Basic Understanding (Foundational)

1. Explain the difference between a Bernoulli and Binomial distribution.
2. Draw a histogram for Bin(10, 0.3). Label axes and explain heights.
3. What's E[X] for Bin(20, 0.7)? Explain why.

## Applied Understanding (Intermediate)

4. In the Palpatine Poll, what does H represent? What's its distribution?
5. Why do we need independence for the list experiment to work?
6. If harmless questions average 2.4 and total average is 2.7, what's estimated support?

## Deep Understanding (Advanced)

7. Why does the list experiment protect privacy for most people but not extreme responders?
8. How would you test whether the independence assumption holds in the Palpatine poll?
9. Design a modified list experiment for 2 hidden questions. What's the fundamental problem?
10. Compare generative and discriminative approaches for the Palpatine problem. Which fits better and why?

---

**End of Teaching Guide**

This comprehensive guide covers all material from the slides and provides detailed explanations, examples, and questions for each concept.
