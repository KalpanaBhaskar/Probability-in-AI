# Large Language Models & Sampling
### From First Principles to the Math

---

## Table of Contents

1. [What is an LLM?](#1-what-is-an-llm)
2. [The Big Question](#2-the-big-question)
3. [How Does an LLM Pick the Next Word?](#3-how-does-an-llm-pick-the-next-word)
4. [Why Not Always Pick the Most Likely Word?](#4-why-not-always-pick-the-most-likely-word)
5. [How Are Probabilities Actually Calculated?](#5-how-are-probabilities-actually-calculated)
6. [The Softmax Function ](#6-the-softmax-function)
7. [Temperature — The Creativity Dial](#7-temperature--the-creativity-dial)
8. [Other Sampling Techniques](#8-other-sampling-techniques)
9. [Putting It All Together](#9-putting-it-all-together)
10. [Practice Problem — Step by Step](#10-practice-problem--step-by-step)

---

## 1. What is an LLM?

A **Large Language Model (LLM)** is an AI program trained to do one core thing:

> **Predict the most likely next word (or token) in a sequence.**

By repeating this prediction thousands of times, one word at a time, the model can write entire paragraphs, answer questions, summarise documents, and hold human-like conversations.

**The simplest mental model:**

```
"The cat sat on the ___"  →  [LLM thinks]  →  "mat"
"The cat sat on the mat and ___"  →  [LLM thinks]  →  "purred"
```

Think of it as an extraordinarily advanced **autocomplete** system — one that has read hundreds of millions of books, articles, and websites.

> **NOTE:** An LLM does not look up facts like a search engine. It *generates* text by predicting what word statistically fits best, given everything it has seen before.

---

## 2. The Big Question

> **"If I give a large language model the exact same prompt twice, should I expect the exact same answer? Is this a feature or a bug?"**

The short answer: **No — and this is an intentional feature, not a bug.**

Here is why. An LLM does not just spit out one answer. For every single word it writes, it calculates a **probability distribution** — a ranked list of *every possible next word* and the percentage chance of each one.

Then, instead of always picking the top word, it **samples** — it rolls a weighted die and picks according to those probabilities. Same prompt → same probability list → but a *different random draw* each time.

This controlled randomness is what makes LLMs feel alive, creative, and useful as brainstorming partners.

---

## 3. How Does an LLM Pick the Next Word?

The process is called **Sampling**. Here is the full picture:

```
Your Prompt
    ↓
LLM calculates probabilities for every possible next word
    ↓
A sampling method picks one word from those probabilities
    ↓
That word is added to the prompt, and the cycle repeats
```

### The Running Example

Throughout these notes we will use this sentence:

> **"The cat sat on the ___"**

Before picking the next word, the model calculates a probability for every word in its vocabulary. The top candidates look like this:

| Word    | Probability |
|---------|-------------|
| mat     | 60%         |
| rug     | 20%         |
| floor   | 15%         |
| pizza   | 4%          |
| moon    | 1%          |

>  **Remember:** These percentages must all add up to exactly **100%** across the entire vocabulary (which can be 50,000+ words). The ones not shown here share the remaining 0%.

---

## 4. Why Not Always Pick the Most Likely Word?

This approach — always picking the single highest probability word — is called **Greedy Decoding**. It sounds reasonable, but it causes two serious problems:

### Problem 1 — Repetitive Loops (might lead to infinite loop!)

If the model always picks the safest, most likely word, it can get mathematically trapped repeating itself:

```
"The site is a great place to find a great place to find a great place to find..."
```

Once "great place" generates a high probability for the words that follow it... those same words generate a high probability for "great place" again. The model is stuck.

### Problem 2 — Bland, Uncreative Output

If you ask an LLM to "write a story about a dragon" with greedy decoding, you get the *exact same story every single time* — the most average, most generic version possible. No variety. No creativity. No usefulness as a writing partner.

**Sampling fixes both problems** by introducing controlled randomness, so the model can:
- Break out of repetitive loops by occasionally choosing a less-obvious word
- Generate genuinely different, creative outputs on each run

---

## 5. How Are Probabilities Actually Calculated?

This is the most important conceptual section. The probability numbers do *not* come from a simple lookup table. They are the result of a multi-step mathematical pipeline:

### Step 1 — The Context Vector

As the LLM reads your prompt word by word, it compresses the *entire meaning* of the sentence so far into a single long list of numbers called a **context vector** (also called a hidden state).

```
"The cat sat on the..."  →  [0.23, -1.41, 0.87, 0.05, ..., 2.11]
                             ↑ This vector encodes meaning and grammar
```

Think of it as a mathematical snapshot of "what is being talked about and in what grammatical state."

### Step 2 — Matrix Multiplication (The Similarity Search)

The model holds an internal table called the **Output Embedding Matrix**. Every word in its vocabulary has its own vector in this table, representing that word's meaning.

The model takes the context vector and multiplies it against this matrix. This is essentially asking:

> *"Which word vectors are most similar (most aligned) with the current context vector?"*

This operation — multiplying vectors to measure similarity — is called a **dot product**. Words whose vectors align closely with the context get high scores. Words that do not align get low or negative scores.

The output of this step is a list of raw scores called **logits** — one score per word in the vocabulary.

```
mat   → logit z = 4.0   ← high score, good fit
rug   → logit z = 2.0   ← medium score
pizza → logit z = 0.5   ← low score, poor fit
moon  → logit z = -1.2  ← very poor fit
```

### Step 3 — Softmax (Turning Scores into Probabilities)

Raw logits are useful for ranking, but they are *not* probabilities. They can be any number — positive, negative, very large, very small. We need them to:

1. All be positive (between 0 and 1)
2. Sum to exactly 1.0 (100%)

This is done with the **Softmax function**, explained fully in the next section.

### The Full Pipeline

```
Prompt Text
    ↓
Context Vector  (meaning compressed into numbers)
    ↓
Dot Product with Embedding Matrix  (vector similarity → logits z)
    ↓
[Optional] Temperature Scaling  (divide logits by T)
    ↓
Softmax  (convert logits to probabilities)
    ↓
Sampling Method  (pick a word from those probabilities)
    ↓
Next Token Output
```

---

## 6. The Softmax Function 

### What It Does

Softmax takes a list of any numbers (logits) and squashes them into a valid probability distribution — all values between 0 and 1, summing to exactly 1.

### The Formula

For a word $x_i$ with logit score $z_i$, its probability is:

$$\boxed{P(x_i) = \frac{e^{z_i}}{\displaystyle\sum_{j} e^{z_j}}}$$

**Breaking this down:**

- $e$ is Euler's number ≈ 2.718 (the base of the natural logarithm)
- $e^{z_i}$ raises $e$ to the power of that word's logit — this ensures the result is always positive
- The denominator $\sum_j e^{z_j}$ sums up $e^z$ for *every* word in the vocabulary — this is what forces all probabilities to add up to 1

### Worked Example — Softmax at T = 1.0 (Default)

Let's use three words with these logits:

| Word  | Logit $z$ |
|-------|-----------|
| mat   | 4.0       |
| rug   | 2.0       |
| pizza | 0.5       |

**Step 1 — Exponentiate each logit:**

$$e^{4.0} \approx 54.60 \quad \text{(mat)}$$

$$e^{2.0} \approx 7.39 \quad \text{(rug)}$$

$$e^{0.5} \approx 1.65 \quad \text{(pizza)}$$

**Step 2 — Sum all exponentiated values:**

$$\text{Total} = 54.60 + 7.39 + 1.65 = 63.64$$

**Step 3 — Divide each by the total:**

$$P(\text{mat}) = \frac{54.60}{63.64} \approx \mathbf{85.8\%}$$

$$P(\text{rug}) = \frac{7.39}{63.64} \approx \mathbf{11.6\%}$$

$$P(\text{pizza}) = \frac{1.65}{63.64} \approx \mathbf{2.6\%}$$

**Verification:** $85.8\% + 11.6\% + 2.6\% = 100\%$  (Success!)

---

## 7. Temperature — The Creativity Dial

Temperature is a single number $T$ that controls how **sharp or flat** the probability distribution is — in other words, how confident or how random the model's choices are.

### Where Temperature Enters the Math

Temperature is injected by **dividing every logit by $T$** before applying Softmax:

$$\boxed{P(x_i) = \frac{e^{z_i / T}}{\displaystyle\sum_{j} e^{z_j / T}}}$$

That is the only change. Everything else stays the same. But this small change has dramatic effects.

### Intuition

| Temperature | Effect on logits | Effect on output |
|---|---|---|
| $T < 1$ (e.g. 0.5) | Dividing by a small number makes logits **bigger** → gaps amplified | More confident, safe, predictable |
| $T = 1$ | No change | Baseline behaviour |
| $T > 1$ (e.g. 2.0) | Dividing by a large number makes logits **smaller** → gaps compressed | More random, creative, unpredictable |

> **NOTE:** Temperature does not change *which* word has the highest probability — it changes *by how much* that word dominates over the others.

---

### Full Worked Example — Three Temperature Settings

Using the same logits as before:

| Word  | Logit $z$ |
|-------|-----------|
| mat   | 4.0       |
| rug   | 2.0       |
| pizza | 0.5       |

---

#### Case 1 — Low Temperature: $T = 0.5$ (Safe Mode)

Dividing by 0.5 is the same as multiplying by 2 — the logits get stretched apart.

**Step 1 — Scale logits by $T$:**

$$z_\text{mat} / T = 4.0 / 0.5 = 8.0$$

$$z_\text{rug} / T = 2.0 / 0.5 = 4.0$$

$$z_\text{pizza} / T = 0.5 / 0.5 = 1.0$$

**Step 2 — Exponentiate:**

$$e^{8.0} \approx 2981.0 \quad \text{(mat)}$$

$$e^{4.0} \approx 54.6 \quad \text{(rug)}$$

$$e^{1.0} \approx 2.7 \quad \text{(pizza)}$$

**Step 3 — Sum:**

$$\text{Total} = 2981.0 + 54.6 + 2.7 = 3038.3$$

**Step 4 — Probabilities:**

$$P(\text{mat}) = \frac{2981.0}{3038.3} \approx \mathbf{98.1\%}$$

$$P(\text{rug}) = \frac{54.6}{3038.3} \approx \mathbf{1.8\%}$$

$$P(\text{pizza}) = \frac{2.7}{3038.3} \approx \mathbf{0.1\%}$$

> **Result:** "mat" is almost certain. The model is highly predictable and safe.

---

#### Case 2 — Normal Temperature: $T = 1.0$ (Default)

No change to logits. We already calculated this above.

$$P(\text{mat}) \approx \mathbf{85.8\%}, \quad P(\text{rug}) \approx \mathbf{11.6\%}, \quad P(\text{pizza}) \approx \mathbf{2.6\%}$$

> **Result:** Balanced. The top choice wins clearly but alternatives have a real chance.

---

#### Case 3 — High Temperature: $T = 2.0$ (Creative Mode)

Dividing by 2.0 shrinks the logits — the gaps between them compress.

**Step 1 — Scale logits by $T$:**

$$z_\text{mat} / T = 4.0 / 2.0 = 2.0$$

$$z_\text{rug} / T = 2.0 / 2.0 = 1.0$$

$$z_\text{pizza} / T = 0.5 / 2.0 = 0.25$$

**Step 2 — Exponentiate:**

$$e^{2.0} \approx 7.39 \quad \text{(mat)}$$

$$e^{1.0} \approx 2.72 \quad \text{(rug)}$$

$$e^{0.25} \approx 1.28 \quad \text{(pizza)}$$

**Step 3 — Sum:**

$$\text{Total} = 7.39 + 2.72 + 1.28 = 11.39$$

**Step 4 — Probabilities:**

$$P(\text{mat}) = \frac{7.39}{11.39} \approx \mathbf{64.9\%}$$

$$P(\text{rug}) = \frac{2.72}{11.39} \approx \mathbf{23.9\%}$$

$$P(\text{pizza}) = \frac{1.28}{11.39} \approx \mathbf{11.2\%}$$

> **Result:** "mat" still leads but the gap has shrunk dramatically. "pizza" now has over a 1-in-10 chance. The model is creative and unpredictable.

---

### Complete Summary Table

| Setting | mat ($z=4.0$) → Prob | rug ($z=2.0$) → Prob | pizza ($z=0.5$) → Prob | Effect |
|---|---|---|---|---|
| Low ($T=0.5$) | $8.0$ → **98.1%** | $4.0$ → **1.8%** | $1.0$ → **0.1%** | Leader dominates; all others suppressed |
| Normal ($T=1.0$) | $4.0$ → **85.8%** | $2.0$ → **11.6%** | $0.5$ → **2.6%** | Balanced baseline |
| High ($T=2.0$) | $2.0$ → **64.9%** | $1.0$ → **23.9%** | $0.25$ → **11.2%** | Flattened — underdogs gain real chances |

### The Extremes

$$\lim_{T \to 0} \Rightarrow \text{Greedy Decoding: the top word wins 100\% of the time}$$

$$\lim_{T \to \infty} \Rightarrow \text{Pure chaos: every word gets an equal chance}$$

---

## 8. Other Sampling Techniques

Temperature is usually applied first to reshape the probability distribution. Then one of these techniques further filters which words are even in the running.

### Greedy Decoding (No Sampling)

Always pick the word with the highest probability. Completely deterministic — same prompt always gives the same output.

- Good for: factual Q&A, maths, structured tasks
- Bad for: creativity, variety, avoiding repetition

### Top-K Sampling

Keep only the top $K$ most likely words. Throw everything else away. Then sample from just those $K$ choices.

**Example with K = 3:**

From our list `{mat 60%, rug 20%, floor 15%, pizza 4%, moon 1%}`:

→ Keep top 3: `{mat, rug, floor}`  
→ Discard: `{pizza, moon}`  
→ Re-normalise: mat ≈ 63.2%, rug ≈ 21.1%, floor ≈ 15.8%  
→ Sample from these three

- Prevents wild, nonsensical word choices
- Fixed K can be too tight (when the model is uncertain) or too loose (when it is very confident)

### Top-P (Nucleus) Sampling

Instead of a fixed number of words, keep the smallest set of top words whose combined probability reaches a threshold $P$.

**Example with P = 0.80 (80%):**

- mat: 60% — running total: **60%**
- rug: 20% — running total: **80%** ← stop here, threshold reached
- floor: 15% — excluded
- pizza: 4% — excluded
- moon: 1% — excluded

→ Only `{mat, rug}` are in the nucleus. Sample from these.

**Why this is smarter than Top-K:**  
If the model is *very confident* (e.g. mat = 95%), the nucleus shrinks to just one word automatically.  
If the model is *very uncertain* (e.g. mat = 25%, rug = 20%, floor = 18%...), the nucleus grows to include more options.

Top-P adapts. Top-K does not.

### Min-P Sampling

Sets a dynamic floor based on the top token's own probability. Any word scoring less than $p_\text{min} \times p_\text{top}$ is discarded.

**Example with min-P = 0.1 (10%):**

If mat = 60%, then the floor is: $0.1 \times 60\% = 6\%$

→ pizza (4%) is discarded. moon (1%) is discarded. Everything at or above 6% survives.

This keeps the pool proportional to how confident the model is, rather than using an absolute cutoff.

### Combining Techniques

In practice, these are often chained together:

```
Raw Logits
    ↓ Temperature scaling  (reshapes the distribution)
    ↓ Top-K or Top-P filter  (removes the long tail)
    ↓ Sample one word  (random draw from what remains)
```

---

## 9. Putting It All Together

Let's summarise the full workflow from prompt to output in one clean picture:

```
User types:  "A sleepy robot dreams about"
                    ↓
      LLM reads the text token by token
                    ↓
      Context Vector is computed
      (entire sentence meaning → one vector)
                    ↓
      Dot product with Embedding Matrix
      (context vector × word vectors → Logits z)
                    ↓
      Temperature Scaling (divide z by T)
                    ↓
      Softmax: P(xᵢ) = e^(zᵢ/T) / Σ e^(zⱼ/T)
                    ↓
      Sampling filter (Top-K / Top-P / Min-P)
                    ↓
      Random draw → next token selected
                    ↓
      Token is appended to the prompt → repeat
```

Every single word in the output goes through this entire pipeline. That is why a 500-word essay involves thousands of individual probability calculations.

---

## 10. Practice Problem — Step by Step

> **Question:** A toy LLM is given the prompt "A sleepy robot dreams about". It can produce five complete outputs, each with a fixed probability. If you run this model **twice** with the same prompt, what is the probability it produces **two different outputs**?

### The Setup

| Output # | Output text        | Probability $p_i$ |
|----------|--------------------|-------------------|
| 1        | electric sheep     | 0.44              |
| 2        | counting stars     | 0.20              |
| 3        | sample spaces      | 0.14              |
| 4        | counting outcomes  | 0.13              |
| 5        | robot puppies      | 0.09              |

**Check point:** $0.44 + 0.20 + 0.14 + 0.13 + 0.09 = 1.00$ 

The two runs are **independent** — the result of the first run does not affect the second run at all.

---

### Step 1 — Define the Events

It is easier to first find the probability that both runs produce the **same** output (single combination only!), then subtract from 1.\
Mathematically, an event and its complement are mutually exclusive. \
Here, assessing multiple combinations for different outputs is harder than identifying when both of them will be the same.\
Let:
- $E$ = the event that **both runs produce the same output**
- $B_i$ = the event that both runs produce **output $i$** specifically
- $E^C$ = the complement = **the two runs produce different outputs** (this is what we want)

---

### Step 2 — Find P(Bᵢ) for Each Output

Since the two runs are independent, the probability that **both** produce output $i$ is simply:

$$P(B_i) = P(\text{run 1 gives output } i) \times P(\text{run 2 gives output } i) = p_i \times p_i = p_i^2$$

Calculate $p_i^2$ for each output:

$$P(B_1) = 0.44^2 = \mathbf{0.1936}$$

$$P(B_2) = 0.20^2 = \mathbf{0.0400}$$

$$P(B_3) = 0.14^2 = \mathbf{0.0196}$$

$$P(B_4) = 0.13^2 = \mathbf{0.0169}$$

$$P(B_5) = 0.09^2 = \mathbf{0.0081}$$

---

### Step 3 — Find P(E) Using the Addition Rule

The events $B_1, B_2, B_3, B_4, B_5$ are **mutually exclusive** (both runs can't simultaneously produce output 1 AND output 2 — it has to be one or the other). So we can simply add them:

$$P(E) = P(B_1) + P(B_2) + P(B_3) + P(B_4) + P(B_5) = \sum_{i=1}^{5} p_i^2$$

$$P(E) = 0.1936 + 0.0400 + 0.0196 + 0.0169 + 0.0081$$

$$\boxed{P(E) = 0.2782}$$

---

### Step 4 — Find P(E^C) Using the Complement Rule

The complement rule states:

$$P(E^C) = 1 - P(E)$$

$$P(E^C) = 1 - 0.2782$$

$$\boxed{P(E^C) \approx 0.72}$$

---

### Interpretation

There is a **72% chance** that running the same prompt twice produces two different outputs — even though the model and the prompt are completely identical.

Notice also: the probability of "same output" is dominated by $p_1^2 = 0.1936$, since "electric sheep" is the most likely output. Even so, there is only a 28% chance of matching. When probabilities are spread across many outputs, collisions become rare.

> **NOTE :** The formula $\sum p_i^2$ is known in statistics as the **sum of squared probabilities**, and its complement $1 - \sum p_i^2$ measures the diversity of a distribution. The more evenly spread the probabilities, the higher the diversity — and the more likely you are to get different outputs on each run.

---

## Try It Out!

> Suppose you run the same model **$n$ times** with the same prompt. What is the probability that **at least two runs** produce the same output? How does this probability change as $n$ increases?
>
> *Hint: Think about the Birthday Problem. For large n, even rare coincidences become almost certain.*

---

*End of notes. Happy learning!*
