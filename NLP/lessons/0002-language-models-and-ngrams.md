# Lesson 0002: Language Modeling & N-grams

**⏱️ Duration:** 25 mins | **📖 Unit:** 2 (Language Modeling & POS Tagging) | **🎯 GTU Weightage:** 28% (Unit 2 — Highest!)

---

> [!NOTE]
> ### 🎣 The Hook
> How does your phone's autocomplete know that after *"I am going to the"* you probably want to type *"store"* or *"gym"* — not *"elephant"*? 
> It uses **Language Models** — systems that calculate the probability that a sequence of words is likely to appear in a real human sentence. The simplest and most powerful approach? **N-grams**: counting how often word sequences appear together in a training corpus (a large collection of text).

---

## 🗺️ The Big Picture

```mermaid
graph TD
    L1["Lesson 1: Introduction & Pipeline (Done)"] ──> L2["Lesson 2: Language Modeling & N-grams (Current)"]
    L2 ──> L3["Lesson 3: POS Tagging, Morphology & NER (Next)"]

    style L1 fill:#d3f9d8,stroke:#2f9e44,stroke-width:1px
    style L2 fill:#e7f5ff,stroke:#1971c2,stroke-width:2px
    style L3 fill:#f8fafc,stroke:#868e96,stroke-width:1px
```

---

## 1. What is a Language Model?
A **Language Model** is a probability distribution over sequences of words. Simply put: given some words, what is the most likely next word?

$$P(\text{"I am going to the store"}) > P(\text{"I am going to the elephant"})$$

The model assigns higher probability to realistic word sequences and lower probability to strange or rare ones.

---

## 2. N-gram Models
An **N-gram** is a contiguous sequence of **N** words from a text. N-gram models estimate the probability of a word based on the (N-1) words that came before it.

> [!TIP]
> **The "Markov Assumption":** We do NOT look at the entire sentence history. We only look at the **last N-1 words**. This is the core simplification that makes N-grams computationally practical.

### 📖 Example Sentence: *"This is a sentence"*

**Unigram (N=1):** Individual words — no context used.

| Token | P(word) |
|-------|---------|
| This | 1/4 = 0.25 |
| is | 1/4 = 0.25 |
| a | 1/4 = 0.25 |
| sentence | 1/4 = 0.25 |

*Formula:* $P(w_1, w_2, \ldots, w_n) = \prod_{i=1}^{n} P(w_i)$

---

**Bigram (N=2):** Pairs of consecutive words. Probability of a word given the **1 previous word**.

| Bigram | Count |
|--------|-------|
| \<START\> This | 1 |
| This is | 1 |
| is a | 1 |
| a sentence | 1 |

*Formula:* $P(w_i | w_{i-1}) = \frac{C(w_{i-1}, w_i)}{C(w_{i-1})}$

where $C$ = count of how many times the sequence appeared in training data.

---

**Trigram (N=3):** Triples of consecutive words. Probability of a word given the **2 previous words**.

| Trigram |
|---------|
| \<START\> This is |
| This is a |
| is a sentence |

*Formula:* $P(w_i | w_{i-2}, w_{i-1}) = \frac{C(w_{i-2}, w_{i-1}, w_i)}{C(w_{i-2}, w_{i-1})}$

### 🔑 The Trade-off:
*   **Higher N** (4-gram, 5-gram) = **More context, better accuracy**, but the model needs **much more training data** to have seen those sequences.
*   **Lower N** (unigram, bigram) = **Less context, less accurate**, but works well even with a small training corpus.

---

## 3. The Zero-Probability Problem
What happens when the model encounters a word sequence it has **never seen** in training?

*   **Example:** If our training corpus never contained the phrase *"the aardvark sings"*, then $C(\text{"aardvark sings"}) = 0$, so $P(\text{"sings"} | \text{"aardvark"}) = \frac{0}{C(\text{"aardvark"})} = 0$.
*   **Problem:** If ANY single probability in a sentence chain equals 0, the total probability of the entire sentence collapses to **0**. A probability of 0 means the model thinks this sentence is *impossible* — even if it's valid English!
*   **Solution:** **Smoothing**!

---

## 4. Smoothing Techniques
Smoothing adds a small fraction to the counts of zero-probability word sequences so that no sequence ever truly has probability 0.

### 🔹 Add-One Smoothing (Laplace Smoothing) — GTU Favorite!
The simplest method: **add 1 to every count**, including unseen sequences.

$$P_{Laplace}(w_i | w_{i-1}) = \frac{C(w_{i-1}, w_i) + 1}{C(w_{i-1}) + V}$$

where $V$ = the vocabulary size (total number of unique words).

> [!TIP]
> **Example:** Training corpus = *"This is a sentence"* (V = 4 unique words)
> - $C(\text{"is a"}) = 1$, $C(\text{"is"}) = 1$
> - **Without smoothing:** $P(\text{"a"} | \text{"is"}) = \frac{1}{1} = 1.0$
> - **With Laplace:** $P(\text{"a"} | \text{"is"}) = \frac{1 + 1}{1 + 4} = \frac{2}{5} = 0.4$
> - Any **unseen** bigram: $P(\text{unseen}) = \frac{0 + 1}{1 + 4} = \frac{1}{5} = 0.2$ (instead of 0!)

### 🔹 Good-Turing Smoothing
A smarter method. Instead of adding a fixed 1, it estimates the count of unseen things based on how often "things we've seen exactly once" appeared.
*   Intuition: *"If we saw 'aardvark eats' once, there are probably other similar rare pairs we haven't seen yet."*
*   Redistributes some probability mass from frequently seen events to unseen events.

---

## 5. Applications of Language Modeling
Language models are the **engine** behind many modern AI applications:

1.  📱 **Autocomplete & Predictive Text:** Phone keyboards suggesting the next word.
2.  🔍 **Search Engines:** Google ranking pages by how likely a query matches a document.
3.  🌐 **Machine Translation:** Ensuring translated sentences are grammatically fluent.
4.  🤖 **Chatbots & LLMs:** GPT-4, Gemini, and other models are essentially very sophisticated language models.
5.  📝 **Spell/Grammar Checkers:** Detecting unusual word sequences that signal errors.

---

> [!CAUTION]
> ### 🎯 GTU Exam Corner
>
> **Q1. Explain Unigram Language Model. (3 Marks)**
> *   A unigram model treats each word as **independent** — the probability of a sentence is simply the product of individual word probabilities. No context is used.
>
> **Q2. Explain Unigram, Bi-gram and Tri-gram concepts using the sentence: "This is a sentence". (7 Marks)**
> *   Define N-gram, then list all Unigrams, Bigrams, and Trigrams from the example sentence. Write the formula for each with the Markov Assumption. Use the tables in Section 2 above directly.
>
> **Q3. Explain Add-One (Laplace) Smoothing with an example. (3–4 Marks)**
> *   State the problem: zero-probability. State the solution: add 1 to all counts. Write the formula. Apply the formula to a small example from Section 4 above.
>
> **Q4. Explain various smoothing techniques with example. (7 Marks)**
> *   Cover **Add-One Smoothing** (with formula and example) and **Good-Turing Smoothing** (with intuition). Explain WHY smoothing is needed first.

---

## 🧠 Prof. Nova's Active Recall Challenge
*Don't scroll up! Close your eyes and test yourself:*
1. In a bigram model, to estimate $P(\text{"store"} | \text{"the"})$, what 2 counts do you need?
2. Why does a zero-probability N-gram collapse the probability of an entire sentence to zero?
3. In Laplace smoothing, what does the $V$ in the denominator stand for?

---
*Next Lesson: 0003 — POS Tagging, Morphology & Named Entity Recognition*
