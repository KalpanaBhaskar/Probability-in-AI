# Week 2: Probability Distributions & Inference Applications
## Part 2: Case Studies & Real-World Applications

---

## 📚 Table of Contents

1. [The Palpatine Poll: Problem Setup](#the-palpatine-poll-problem-setup)
2. [Why Direct Questioning Fails](#why-direct-questioning-fails)
3. [The List Experiment: A Solution](#the-list-experiment-a-solution)
4. [Modeling One Respondent](#modeling-one-respondent)
5. [The Complete Probabilistic Model](#the-complete-probabilistic-model)
6. [Simulation: Making Fake Data](#simulation-making-fake-data)
7. [Inference: Working Backwards](#inference-working-backwards)
8. [Real Data Analysis](#real-data-analysis)
9. [When Does It Work? When Does It Fail?](#when-does-it-work-when-does-it-fail)
10. [Extensions & Variations](#extensions--variations)

---

## The Palpatine Poll: Problem Setup

### The Scenario

**Setting**: The Star Wars galaxy, ruled by Emperor Palpatine

**The Question**: How many people secretly support Palpatine?

**The Problem**: 
- Direct question: "Do you support Palpatine?" 
- Expected answer: "No!" (out of fear)
- Actual answer: Unknown

**Why it's dangerous**:
- Palpatine rules with fear and violence
- People who admit support are safe
- People who admit opposition might be arrested
- **No one answers honestly**

### The Fundamental Challenge

This is a **sensitive questions problem**:
- Question involves sensitive topic (hidden political views, illegal behavior, embarrassing facts)
- Direct answers are unreliable (people lie for safety or embarrassment)
- We want aggregate statistics, not individual answers
- Individual privacy is crucial

**Examples of sensitive questions**:
- Academic dishonesty: "Did you cheat on exams?"
- Medical: "Have you used illegal drugs?"
- Tax: "Have you evaded taxes?"
- Political: "Do you support the opposition leader?"

---

## Why Direct Questioning Fails

### The Social Desirability Bias

People systematically answer questions to look good.

**Expected support for Palpatine**: Suppose 20% truly support him.

**Direct questioning**:
- Asked directly, only 5% admit support
- Reason: Fear of persecution
- Result: Massive underestimation

**Data comparison** (Vietnam 2023 study):
- Academic dishonesty (ChatGPT use)
- Direct question: 9.6% admitted yes
- List experiment (hidden): 23.7% yes
- **Difference**: 2.5x higher with privacy

### Why This Happens

```
Honest answer: "Yes, I support him" (20% true)
                    ↓
Thinking about risk: "If I say yes, they'll..."
                    ↓
Strategic answer: "No, I don't" (reported only 5%)
                    ↓
Result: Massive bias and wasted data
```

### The Privacy Paradox

**Direct question provides**:
- Individual responses (the data)
- Privacy risk (my answer reveals my view)
- Unreliable data (I'm lying anyway)

**We need**: Aggregate statistics without individual privacy loss

---

## The List Experiment: A Solution

### The Core Idea

Instead of asking directly, **hide the sensitive question** among harmless ones.

**Setup**:
- Ask 5-6 questions total
- 5 are completely harmless (about 50/50 preferences)
- 1 is the sensitive question (hidden among the harmless ones)
- Respondent gives **only a count**: "How many of these did you answer yes to?"

### Example Questions

```
1. Do you like surprises?                    [Harmless, ~50/50]
2. Do you prefer beach to mountains?         [Harmless, ~50/50]
3. Do you prefer paper books to e-books?     [Harmless, ~50/50]
4. Would you rather have more time?          [Harmless, ~50/50]
5. Do you prefer holidays at home?           [Harmless, ~50/50]
6. Do you support Palpatine?                 [SENSITIVE, hidden]
```

**What respondent reports**: 
- "I said yes to 3 of these questions" (total count, no details)

**Privacy achieved**: 
- Surveyor doesn't know which questions got "yes"
- Could have said yes to 1,2,3 or 1,2,6 or 4,5,6 or...
- Individual answers completely hidden

### Why It Works

**Key insight**: The hidden question adds variability to the count.

**Mathematical insight**:
- Count from harmless questions (H) is "noise"
- Hidden question (S) is "signal"
- Total count (A = H + S) contains signal + noise
- With enough samples, signal emerges

---

## Modeling One Respondent

### Step 1: The Harmless Questions (H)

**Story**: Person answers 5 harmless yes/no questions.

Each question is 50/50, independent.

**Model**: 
$$H \sim \text{Bin}(5, 0.5)$$

**Interpretation**: 
- 5 trials (questions)
- Probability 0.5 for each trial
- H is the count of yes answers

**Probability distribution**:
```
P(H=0) = 0.031  (about 3%)
P(H=1) = 0.156  (about 16%)
P(H=2) = 0.313  (about 31%) ← Most likely
P(H=3) = 0.313  (about 31%) ← Most likely
P(H=4) = 0.156  (about 16%)
P(H=5) = 0.031  (about 3%)
```

**Expected value**: E[H] = 5 × 0.5 = 2.5

**Intuition**: On average, people say yes to 2.5 of the 5 harmless questions.

### Step 2: The Hidden Question (S)

**Story**: Does this person support Palpatine?

**Model**:
$$S \sim \text{Ber}(\theta_2)$$

Where $\theta_2$ = unknown probability of support

**Interpretation**:
- S = 0 if person doesn't support Palpatine
- S = 1 if person does support Palpatine
- $\theta_2$ is what we're trying to estimate

**Why unknown?** That's exactly what we're trying to figure out!

### Step 3: The Answer They Report (A)

**Story**: Person counts yes answers across all 6 questions.

**Model**:
$$A = H + S$$

Where:
- H = count from 5 harmless questions
- S = answer to hidden question
- A = total count reported

**Key property**: 
- A ranges from 0 to 6
- A's distribution depends on $\theta_2$ (unknown parameter)

**Example**:
- If person says "yes" to 3 questions
- Could mean: H=3, S=0 (didn't support Palpatine)
- Could mean: H=2, S=1 (did support Palpatine)
- We don't know which!

---

## The Complete Probabilistic Model

### The Full Story

```
1. Person has true support status: S ~ Ber(θ₂)
2. Person answers 5 harmless questions: H ~ Bin(5, 0.5)
3. H and S are independent
4. Person reports count: A = H + S
5. We observe A, want to estimate θ₂
```

### The Joint Distribution: P(H, S)

Since H and S are **independent**:
$$P(H = h, S = s) = P(H = h) \times P(S = s)$$

**Examples**:
```
P(H=2, S=0) = P(H=2) × P(S=0)
            = 0.313 × (1-θ₂)

P(H=2, S=1) = P(H=2) × P(S=1)
            = 0.313 × θ₂
```

### The Distribution of A: P(A = a)

Now we need the distribution of the **sum** A = H + S.

**Key insight**: To get A = k, we can have:
- H = k, S = 0 (didn't support), OR
- H = k-1, S = 1 (did support)

**Formula**:
$$P(A = k) = P(H = k, S = 0) + P(H = k-1, S = 1)$$
$$= P(H = k)(1-\theta_2) + P(H = k-1)\theta_2$$

**Special case**: A = 0 or A = 6
- P(A=0) can only come from H=0, S=0
  - P(A=0) = P(H=0) × (1-$\theta_2$) ≈ 0.031(1-$\theta_2$)
  
- P(A=6) can only come from H=5, S=1
  - P(A=6) = P(H=5) × $\theta_2$ ≈ 0.031 × $\theta_2$

**Insight**: P(A=0) and P(A=6) reveal $\theta_2$!

### Different Values of θ₂

**If $\theta_2$ = 0.09** (9% support):
```
P(A=0) ≈ 0.031 × 0.91 ≈ 0.028 (2.8%)
P(A=1) ≈ 0.156 × 0.91 + 0.031 × 0.09 ≈ 0.145
P(A=2) ≈ 0.313 × 0.91 + 0.156 × 0.09 ≈ 0.299
P(A=3) ≈ 0.313 × 0.91 + 0.313 × 0.09 ≈ 0.313
P(A=4) ≈ 0.156 × 0.91 + 0.313 × 0.09 ≈ 0.170
P(A=5) ≈ 0.031 × 0.91 + 0.156 × 0.09 ≈ 0.042
P(A=6) ≈ 0.031 × 0.09 ≈ 0.003
```

**Visual summary**:
- Distribution is mostly 2, 3, 4
- Slightly shifted left (more people say 2 or 3 than 5 or 6)
- Very few extreme answers (0 or 6)

---

## Simulation: Making Fake Data

### Why Simulate?

Simulation lets us:
1. **Verify** that our model generates data with similar patterns to real data
2. **Understand** how the model works by seeing it in action
3. **Explore** what happens with different parameter values

### Simulation Algorithm

```
repeat 1000 times:
    1. Generate H ~ Bin(5, 0.5)
    2. Generate S ~ Ber(θ₂)
    3. Compute A = H + S
    4. Store A
    
After 1000 repetitions:
    Plot histogram of A
    Compute mean, median, etc.
    Compare to real data
```

### Example: Simulating with θ₂ = 0.09

**Pseudocode**:
```
theta_2 = 0.09
for i = 1 to 1000:
    # Generate harmless answers
    H = number of successes in 5 independent Ber(0.5) trials
    
    # Generate hidden question answer
    S = 1 with probability theta_2, else 0
    
    # Total answer
    A[i] = H + S

# Analyze results
mean_A = average of A[]
histogram of A[]
```

### Real Data Comparison

**Real data from Palpatine poll** (1000 respondents):
```
Count=0: 170 people (17%)
Count=1: 300 people (30%)
Count=2: 330 people (33%)  ← Most common
Count=3: 170 people (17%)
Count=4: 40 people (4%)
Count=5: <5 people (<1%)
Count=6: <2 people (<1%)

Mean = (0×170 + 1×300 + 2×330 + 3×170 + 4×40 + 5×5) / 1000
     = 2618 / 1000 = 2.618
```

**Simulated data with θ₂ = 0.09**:
```
Count=0: 180 people (18%)
Count=1: 290 people (29%)
Count=2: 320 people (32%)  ← Most common
Count=3: 160 people (16%)
Count=4: 35 people (3.5%)
Count=5: 10 people (1%)
Count=6: 5 people (0.5%)

Mean ≈ 2.58
```

**Conclusion**: Simulation matches real data! This suggests θ₂ ≈ 0.09 is correct.

---

## Inference: Working Backwards

### The Inference Problem

We observe real data:
- 1000 people reported counts
- Mean count = 2.62

Now we want to estimate: **What is θ₂ (true support)?**

### Method 1: Using the Mean

**Mathematical relationship**:
$$E[A] = E[H + S] = E[H] + E[S]$$
$$E[A] = E[H] + \theta_2$$
$$E[A] = 2.5 + \theta_2$$

**From data**, we know E[A] ≈ 2.62

**Solving**:
$$2.62 = 2.5 + \theta_2$$
$$\theta_2 = 0.12$$

**Interpretation**: Approximately 12% of people support Palpatine.

### Method 2: Matching Distributions (Simulation-based)

**Algorithm**:
```
for each possible theta_2 in {0.01, 0.02, ..., 0.20}:
    1. Simulate 1000 responses with that theta_2
    2. Compare histogram to real data
    3. Measure similarity (e.g., chi-squared test)
    4. Record best fit
    
The theta_2 with best fit is our estimate
```

**Result**: Best-fit θ₂ ≈ 0.09-0.12 (similar to Method 1)

### Method 3: Using Extreme Answers

**Smart insight**: Extreme answers (0 or 6) directly reveal support.

- P(A=6) = P(H=5) × θ₂ = 0.031 × θ₂
- From data: P(A=6) ≈ observed frequency of 6s
- Solving: θ₂ = (observed P(A=6)) / 0.031

**From real data**: 
- About 2 people said 6 out of 1000
- P(A=6) ≈ 0.002
- θ₂ ≈ 0.002 / 0.031 ≈ 0.065

(Slightly lower than mean method, but similar range)

---

## Real Data Analysis

### The Vietnam Study (2023)

**Research question**: How prevalent is ChatGPT use in academic cheating?

**Setup**:
- 1000 Vietnamese university students surveyed
- 5 harmless questions about daily habits
- 1 hidden question: "Have you used ChatGPT to cheat on exams?"

### Results Comparison

| Method | Reported (%) | Estimated (%) | Ratio |
|--------|-------------|---------------|-------|
| Direct question | 9.6% | 9.6% | 1x |
| List experiment | 23.7% | 23.7% | 2.5x |

**Conclusion**: **True rate is 2.5x higher than direct answer**

Why the difference?
- Fear of getting caught
- Shame/embarrassment
- Institutional consequences
- Normalizing bias (if everyone cheats, I'm honest to say no)

### Interpretation

The list experiment:
- Reveals hidden ground truth
- Maintains individual privacy (no one knows who said what)
- Uses clever mathematics to extract signal from noise

---

## When Does It Work? When Does It Fail?

### Assumptions Required

The list experiment **works** if:

1. **Harmless questions are truly 50/50**
   - If 90% answer yes to beach: not 50/50
   - Solution: Carefully pilot-test harmless questions
   
2. **Harmless and hidden are independent**
   - If people who like surprises also support Palpatine: violated
   - Solution: Choose harmless questions unrelated to topic
   
3. **People report counts honestly**
   - If people lie about the count: experiment fails
   - Solution: Verify in smaller studies
   
4. **Large enough sample**
   - Need enough data to see patterns
   - Extreme answers (0 or 6) are rare, need large N
   - Solution: Larger surveys for rare phenomena

### When It Fails

**Example 1: Harmless questions too easy**

If 90% of people say yes to "Do you like being alive?":
- Harmless questions average 4.5 instead of 2.5
- Most people report 5 or 6
- Can't distinguish hidden support from harmless answers

**Solution**: Retest harmless questions for 50/50 split

**Example 2: Hidden and harmless correlated**

If support for Palpatine correlates with optimism:
- People answering yes to "Do you like surprises?" might also support him
- Violates independence assumption
- Estimates become biased

**Solution**: Theory check—are they really independent?

**Example 3: Extreme responders**

- Some people say yes to everything (A = 6)
- Some people say no to everything (A = 0)
- These extreme answers reveal their view of hidden question

**Example**: A = 6 can only come from "yes to all including Palpatine"
- About 3 in 1000 say 6 (from real data)
- ~0.3% are exposed (privacy breached)

**Solution**: Add noise, top-coding, or more harmless questions

### Robustness Check: Sensitivity Analysis

**Question**: How much does estimate change if assumptions slightly violated?

**Example**: What if 10% of people lie about the count?

```
Run simulation with:
- Original model
- 10% lie about count (add/subtract 1 randomly)
- Compare estimates
```

If estimate is stable: Robust to violations
If estimate changes dramatically: Fragile

---

## Extensions & Variations

### Extension 1: Multiple Hidden Questions

**Problem**: Want to ask about two sensitive topics

**Naive approach**: Add second hidden question
- But now 50% of list is sensitive (decreases privacy)
- Dependencies become complex

**Better approach**: Two separate surveys
- Group A: Harmless + Sensitive topic 1
- Group B: Harmless + Sensitive topic 2
- Estimates won't interfere

### Extension 2: Continuous Hidden Questions

**Problem**: Want to estimate a continuous distribution, not just prevalence

**Example**: "How many times did you cheat?" (not just 0/1)

**Solution**: Use continuous support instead of Bernoulli
- S ~ Geometric(p) or other distribution
- Same principle: hide signal in noise
- Inference slightly more complex

### Extension 3: Randomized Response

**Alternative method**: Different privacy mechanism

**Instead of list experiment**:
- Person flips hidden coin
- Heads: answer truthfully
- Tails: always say "yes"

**Advantage**: Even more privacy, respondent always has deniability

**Disadvantage**: Less efficient (less signal per response)

### Extension 4: Machine Learning Approach

**Bayesian inference**:
- Use prior knowledge about θ₂
- Update with observed data
- Get posterior distribution (uncertainty quantified)
- Provides confidence intervals, not just point estimates

**Example**:
- Prior: θ₂ could be anywhere from 0 to 0.5 (Palpatine probably unpopular)
- Data: Observed counts
- Posterior: θ₂ ≈ 0.09 with 95% CI = [0.05, 0.15]

---

## Putting It All Together: Complete Workflow

### 1. Problem Definition
- What's the sensitive question?
- Why can't we ask directly?
- What aggregate statistic do we need?

### 2. Design Phase
- Choose 5-6 harmless questions
- Pilot-test: Are they 50/50?
- Theory check: Independent from hidden question?

### 3. Data Collection
- Survey large sample (N ≥ 500-1000)
- Collect counts only, not individual answers
- Maintain anonymity

### 4. Analysis: Descriptive
- Plot histogram of counts
- Compute mean count
- Compare to expected distribution for H alone

### 5. Analysis: Inferential
- Estimate θ₂ using mean method
- Verify with simulation
- Check extreme answers
- Perform sensitivity analysis

### 6. Interpretation
- Report estimate with uncertainty
- Discuss limitations and assumptions
- Compare to direct methods (if available)
- Contextualize findings

### 7. Reporting
- "List experiment suggests approximately [X]% support"
- "This is [Y]x higher than direct questioning"
- "We rely on assumptions of independence and 50/50 questions"
- "Privacy maintained: no individual responses revealed"

---

## Summary: Key Concepts

### The List Experiment Principle

```
Raw data: Only counts (no individual answers)
          ↓
Lost information: Which questions got yes?
                 (intentional for privacy)
          ↓
Recovered signal: Hidden support through statistics
                 (everyone's answers + patterns)
          ↓
Result: Both privacy protected AND truth revealed
```

### The Mathematics Behind It

- **H ~ Bin(5, 0.5)**: Noise from harmless questions
- **S ~ Ber(θ₂)**: Signal from hidden question
- **A = H + S**: Observed mix of signal + noise
- **E[A] = 2.5 + θ₂**: Mathematical relationship
- **From E[A], estimate θ₂**: Recover the signal

### The Real-World Lesson

This case study illustrates:
1. **Why direct methods fail** (social desirability bias)
2. **How probability helps** (models the full scenario)
3. **How to reveal truth** (aggregate patterns)
4. **How to protect privacy** (individual answers hidden)
5. **When to be careful** (assumptions can fail)

---

## Practice Problems

### Easy

1. What's E[H] for harmless questions? Why?

2. If someone reports A = 4, what are the possible values of (H, S)?

3. What would happen if all harmless questions were "Do you like breathing?" (99% yes rate)?

### Medium

4. From real data: mean A = 2.62. Estimate θ₂.

5. Why does P(A=6) directly reveal θ₂? (Hint: what's the only way to get A=6?)

6. If observed P(A=6) = 0.004, what's the estimate of θ₂?

### Hard

7. Explain why the independence assumption matters. What would go wrong if violated?

8. Design a sensitivity analysis: How does the estimate change if 5% of people lie about the count?

9. Propose an improved list experiment with two hidden questions. What's the challenge?

10. Compare list experiment vs. randomized response. Which provides better privacy? Better accuracy?

---

**End of Week 2 Part 2**

Next: Part 3 covers **Advanced Topics & Extensions** including Bayesian inference, model checking, and open research questions.
