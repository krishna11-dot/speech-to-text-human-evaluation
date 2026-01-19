# Methodology: The Nuances Explained

> "If things break, can you figure out why it's breaking?"

This document explains the **conceptual reasoning** behind every methodological choice. The goal: understand the parts, not just the whole.

---

## Why Human Evaluation?

### The Problem with Automated Metrics

**Word Error Rate (WER)** measures: "Did the system output the exact words?"

But WER doesn't capture:
- How many **attempts** did it take?
- Did the user **give up** in frustration?
- Was it **easy to use** even if eventually correct?

**Human evaluation measures usability**, not just accuracy. This study focuses on perceived system performance from the user's perspective.

---

## Why Within-Subjects Design?

### The Alternative: Between-Subjects

**Between-subjects**: Person A tests Google, Person B tests Microsoft

**Problem**:
- Maybe Person A has a clearer accent
- Maybe Person B speaks faster
- You can't separate "system quality" from "person quality"

### Within-Subjects Solution

Each participant tests **both systems**:
- Same voice, same accent, same speed
- Any difference **must** be the system
- Higher statistical power (paired comparisons)

### Potential Issue: Order Effects

Did testing Google first affect Microsoft ratings?

**Mitigation**: The study could have counterbalanced (half test Google first, half test Microsoft first). The PDF doesn't mention this explicitly - a potential limitation.

---

## Why These Specific Test Sentences?

### The Design Logic

| Difficulty | Design Principle | What It Tests |
|------------|------------------|---------------|
| **Easy** | Phonetically balanced, common words | Baseline capability - can it work at all? |
| **Medium** | Homophones and similar sounds | Disambiguation ability |
| **Hard** | Rare words, unusual grammar | Robustness under stress |

### The Specific Sentences

**Easy - E1**: "The quick brown fox jumps over the lazy dog"
- Classic pangram (contains all letters)
- Every native English speaker knows it
- If a system fails this, something is fundamentally wrong

**Easy - E2**: "The boy was there when the sun rose"
- Simple grammar, common words
- No ambiguity
- Tests basic transcription

**Medium - M1**: "Joe Reed read the redacted red book about reeds"
- Multiple similar sounds: Reed/read/red/reeds
- Tests acoustic disambiguation
- Language model must choose correct spelling

**Medium - M2**: "Bob bought a bowl of balls in a ball at the mall"
- Repeated 'b' and 'all' sounds
- Tests phonetic precision
- "ball" vs "bowl" vs "balls" vs "mall"

**Hard - H1**: "A rough-coated dough-faced, thoughtful ploughman..."
- Multiple "-ough" pronunciations (rough, dough, through, slough, cough, hiccough)
- All pronounced differently in English
- Tests knowledge of irregular spelling-sound mappings

**Hard - H2**: "All the faith he had had had had no effect..."
- Repeated "had" is grammatically correct
- Tests language model's syntactic understanding
- Many speakers stumble themselves

### Why This Progression Matters

If a system fails on **easy** sentences → fundamental problem
If it fails only on **hard** sentences → graceful degradation
If it fails on **medium** but not **easy** → disambiguation weakness

This **isolates the failure mode**.

---

## Why These Statistical Tests?

### Binomial Test for Preference

**The data**: 19 chose Microsoft, 1 chose Google (binary choice)

**The question**: "Is 19/20 different from 50/50?"

**Why binomial?**
- Each choice is independent
- Two outcomes (Google or Microsoft)
- This IS a binomial experiment by definition

**The calculation**:
```
P(X >= 19 | p=0.5, n=20) ≈ 0.00002
Two-sided p-value ≈ 0.00004
```

**Interpretation**: If truly no preference exists, seeing 19/20 would happen 0.004% of the time. We reject the null hypothesis.

---

### Mann-Whitney U for Likert Scales

**Why not t-test?**

The t-test assumes:
1. Data is **interval** (equal spacing between values)
2. Data is **normally distributed**

Likert scales violate assumption 1:
- Is the difference between "Strongly Agree (7)" and "Agree (6)" the same as between "Neutral (4)" and "Disagree (3)"?
- We don't know. Likert is **ordinal** (ordered but not equally spaced)

**What Mann-Whitney does**:
1. Rank all values from both groups combined
2. Compare the sum of ranks between groups
3. If one group consistently ranks higher, U-statistic is low, p-value is low

**Example from this study**:
```
If Google ratings are: [6, 6, 5, 4, 2]
And Microsoft ratings: [7, 7, 7, 6, 6]

Mann-Whitney asks: "Do Microsoft values tend to be larger?"
Answer: Yes, systematically → significant difference
```

---

### Shapiro-Wilkes for Normality

**Purpose**: Check if we could use parametric tests

**Finding**: Distributions were not normal (as expected for Likert data)

**Decision**: Use non-parametric tests (Mann-Whitney U)

**Why this matters**: Using t-test on non-normal Likert data would violate assumptions and potentially give misleading p-values.

---

## Why Segment by Difficulty?

**The question**: "Does Microsoft's advantage hold across conditions?"

| Possibility | Interpretation |
|-------------|----------------|
| Microsoft better only on easy | Narrow advantage, may not generalize |
| Microsoft better on all levels | Fundamental quality difference |
| Gap widens on harder sentences | Systems degrade differently |

**What this study found**:

| Difficulty | Google Median | Microsoft Median |
|------------|---------------|------------------|
| Easy | 7 | 7 |
| Medium | 3 | 5 |
| Hard | 3 | 6.5 |

**The insight**: Google collapses on medium/hard sentences. Microsoft degrades gracefully. The gap **widens** as difficulty increases.

This tells a story: Google's problem isn't just "worse accuracy" - it's specifically unable to handle ambiguity and length.

---

## Why Segment by Nationality?

**The research question**: "Does accent affect the performance gap?"

### Possible Outcomes

| Outcome | What It Would Mean |
|---------|-------------------|
| Gap same for all nationalities | Both systems handle accents equally |
| Gap larger for non-native speakers | One system has better accent robustness |
| Gap varies unpredictably | Noise, need more data |

### What This Study Found

| Nationality | p-value | Significant? |
|-------------|---------|--------------|
| British (native) | 0.073 | No |
| Romanian | 0.018 | Yes |
| Italian | 0.132 | No |
| Indian | 0.006 | Yes |

**The insight**: For native English speakers (British), both systems perform similarly. The differentiation happens with certain non-native accents.

**Why might this be?**
- Training data composition (more native English?)
- Acoustic model tuning
- Endpoint detection calibration for different speech patterns

This points to **where to investigate further**, not just "Microsoft is better."

---

## Understanding the Visualizations

### Why Stacked Histograms?

**The goal**: Show distribution shape, not just averages

A mean of 5.5 could be:
- Everyone gave 5 or 6 (consensus)
- Half gave 2, half gave 7 (bimodal disagreement)

**Histograms reveal the shape**. This study's histograms showed:
- Google: More spread, more low ratings
- Microsoft: Concentrated at high ratings

### Why Stack by Nationality?

Shows whether all groups agree or if one group is pulling averages.

For example: If only Indian participants gave low ratings to Google, that's a different story than all nationalities giving low ratings.

---

## The Qualitative Data: What Numbers Can't Tell

### From User Feedback

**Google's failure mode identified**:
> "Stops listening before the end of the sentence"
> "It didn't wait long enough for me to speak"

**Microsoft's advantage explained**:
> "Takes into account the speed of my speech and doesn't deliver results prematurely"

### Why This Matters

The Likert scores tell you **THAT** Google performs worse.
The comments tell you **WHY** - it's a timing/endpoint detection issue.

**For practitioners**: This is actionable. The problem is specific (timing), not general (accuracy).

**For researchers**: This is a testable hypothesis for follow-up study.

---

## Limitations: Being Honest

### Sample Size
- 20 participants total (5 per nationality)
- Sufficient for overall comparisons
- Insufficient for confident nationality-specific conclusions

### Sentence Representativeness

The PDF acknowledges: Test sentences are not what users typically say to STT systems.

Real STT usage:
- Search queries: "weather tomorrow"
- Voice commands: "play music"
- Dictation: Natural conversational speech

The study's sentences are controlled but artificial.

### Order Effects (Potential)

If all participants tested Google first, Microsoft ratings might be inflated by:
- Learning effects
- Familiarity with the task
- Contrast effects

The study doesn't explicitly mention counterbalancing.

### Convenience Sampling

Participants were family/friends of researchers. This may introduce bias:
- Similar demographics
- Similar environments
- Similar speech patterns

---

## Connection to Research Methodology Principles

| Principle | How This Study Implements It |
|-----------|------------------------------|
| "Does it work?" | Preference, accuracy, ease-of-use metrics |
| "Why does it work?" | Qualitative feedback reveals timing issues |
| "When does it work?" | Difficulty and nationality breakdowns |
| Appropriate statistics | Non-parametric for ordinal data |
| Failure mode analysis | User comments document where Google fails |
| Honest limitations | Section 4.2 explicitly lists weaknesses |

---

## What to Remember

1. **Statistical tests must match data types** - Ordinal data needs non-parametric tests

2. **Within-subjects design controls confounds** - Same person testing both systems isolates the system effect

3. **Segmented analysis reveals conditions** - Overall average hides important variation

4. **Qualitative data explains mechanisms** - Numbers say "what," comments say "why"

5. **Limitations are features, not bugs** - Acknowledging them shows rigor

6. **Sentence design matters** - Each difficulty level isolates a different phenomenon

The goal isn't perfect methodology. The goal is **understanding what your analysis can and cannot claim**.
