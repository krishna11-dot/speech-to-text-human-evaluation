# Speech to Text with Google and Microsoft: A Human Evaluation

**CS5063: Evaluation of AI Systems**
University of Aberdeen
Instructor: Prof. E. Reiter

**Authors**: Rotariu A., Milne C., Bucci V., Nair K.

### Team Contributions (from PDF Section 2.2.1)

Each researcher recruited 5 participants of their own nationality:

| Researcher | Nationality | Contribution |
|------------|-------------|--------------|
| Rotariu A. | Romanian | Data collection (5 Romanian participants) |
| Milne C. | British | Data collection (5 British participants) | Report Writing |
| Bucci V. | Italian | Data collection (5 Italian participants) |  Statistical analysis +  Report writing |
| **Nair K.** | **Indian** | **Data collection (5 Indian participants) + Statistical analysis code (`analysis.ipynb`) + Report writing** |

**Note**: The Indian participant data showed the **strongest statistical significance** (p = 0.006) - the largest performance gap between systems.

---

## Project Summary

**Type**: Empirical Study (original data collection + analysis, NOT a review paper)

A human evaluation comparing two speech-to-text systems (Google and Microsoft) to determine:
1. User preference between systems
2. Ease of use differences
3. Accuracy across sentence difficulty levels
4. Effect of user nationality on system accuracy

---

## Study Architecture

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                           RESEARCH QUESTIONS                                │
│  1. User preference?  2. Ease of use?  3. Accuracy?  4. Nationality effect? │
└─────────────────────────────────────────────────────────────────────────────┘
                                      │
                                      ▼
┌─────────────────────────────────────────────────────────────────────────────┐
│                           STUDY DESIGN                                      │
│                                                                             │
│   Participants: 20 (5 British, 5 Romanian, 5 Italian, 5 Indian)            │
│   Design: Within-subjects (each person tests BOTH systems)                  │
│   Why: Controls for individual differences (accent, speed, clarity)         │
└─────────────────────────────────────────────────────────────────────────────┘
                                      │
                                      ▼
┌─────────────────────────────────────────────────────────────────────────────┐
│                           TEST SENTENCES                                    │
│                                                                             │
│   EASY (2)      →  Phonetically balanced, common words                      │
│   MEDIUM (2)    →  Homophones, similar sounds (reed/read, ball/bowl)        │
│   HARD (2)      →  Rare words, unusual grammar (-ough variations)           │
│                                                                             │
│   Why this structure: Isolates WHERE systems fail, not just IF they fail    │
└─────────────────────────────────────────────────────────────────────────────┘
                                      │
                                      ▼
┌─────────────────────────────────────────────────────────────────────────────┐
│                           DATA COLLECTION                                   │
│                                                                             │
│   For each sentence: "System understood me quickly and accurately" (1-7)    │
│   After each system: "System was easy to use" (1-7)                         │
│   At the end: "Which system do you prefer?" (Google/Microsoft)              │
│   Open feedback: Free-text comments                                         │
└─────────────────────────────────────────────────────────────────────────────┘
                                      │
                                      ▼
┌─────────────────────────────────────────────────────────────────────────────┐
│                           ANALYSIS PIPELINE                                 │
│                                                                             │
│   1. Visualize distributions (histograms by nationality)                    │
│   2. Check normality (Shapiro-Wilkes) → Not normal                          │
│   3. Select appropriate tests:                                              │
│      • Preference → Binomial (binary outcome)                               │
│      • Likert ratings → Mann-Whitney U (ordinal data)                       │
│   4. Segment by conditions (difficulty, nationality)                        │
│   5. Analyze qualitative feedback (WHY patterns)                            │
└─────────────────────────────────────────────────────────────────────────────┘
                                      │
                                      ▼
┌─────────────────────────────────────────────────────────────────────────────┐
│                           KEY FINDINGS                                      │
│                                                                             │
│   WHAT: Microsoft outperforms Google (95% preference, higher accuracy)      │
│   WHY:  Google's timing cuts off speakers too early (endpoint detection)    │
│   WHEN: Gap largest for non-native speakers + complex sentences             │
└─────────────────────────────────────────────────────────────────────────────┘
```

---

## The Three Questions Framework

> "Strong empirical validation answers three questions: Does it work? Why does it work? When does it work?"

| Question | How This Study Answers It |
|----------|---------------------------|
| **Does it work?** | Microsoft wins on preference (95%), ease of use (median 7 vs 6), and accuracy (all difficulty levels) |
| **Why does it work?** | User feedback reveals Google's timing problem - cuts off before sentence ends. This is endpoint detection, not recognition. |
| **When does it work?** | Gap is largest for: (1) Non-native speakers (Romanian p=0.018, Indian p=0.006), (2) Complex sentences (Hard: median 3 vs 6.5) |

---

## Study Design

### Participants
- **20 participants** total
- **5 per nationality**: British, Romanian, Italian, Indian
- Recruited from family/friends of researchers (convenience sampling due to time constraints)

### Within-Subjects Design
Each participant tests **both systems** on the **same sentences**.

**Why this matters**: Controls for individual speech patterns, accent strength, and speaking speed. Any difference observed must be due to the system, not the person.

### Test Sentences (6 total)

| Difficulty | Sentence | Purpose |
|------------|----------|---------|
| **Easy (E1)** | "The quick brown fox jumps over the lazy dog" | Phonetically balanced, easy pronunciation |
| **Easy (E2)** | "The boy was there when the sun rose" | Baseline - both systems should handle these |
| **Medium (M1)** | "Joe Reed read the redacted red book about reeds" | Similar pronunciation words (ambiguity test) |
| **Medium (M2)** | "Bob bought a bowl of balls in a ball at the mall" | Homophones and similar sounds |
| **Hard (H1)** | "A rough-coated dough-faced, thoughtful ploughman strode through the streets of Scarborough; after falling into a slough, he coughed and hiccoughed" | Rare word combinations, pronunciation ambiguity |
| **Hard (H2)** | "All the faith he had had had had no effect on the outcome of his life" | Convoluted grammar, repeated words |

**Why these sentences?** Each difficulty level isolates a specific phenomenon:
- Easy: Can the system handle standard speech?
- Medium: Can it disambiguate similar-sounding words?
- Hard: Can it handle unusual patterns and length?

### Measurements
- **Accuracy**: 7-point Likert scale ("The system understood me quickly and accurately")
- **Ease of Use**: 7-point Likert scale after all 6 sentences
- **Preference**: Binary choice at the end (Google or Microsoft)
- **Open Feedback**: Free-text comments

---

## Formal Hypotheses

| # | Null Hypothesis | Alternative |
|---|-----------------|-------------|
| H1 | No difference in user preference | Users prefer one system |
| H2 | No difference in ease of use | One system easier to use |
| H3 | No difference in accuracy | One system more accurate |
| H4 | Nationality has no effect on accuracy | Accuracy varies by nationality |

---

## Statistical Analysis: Why These Tests?

### Binomial Test (for Preference)
- **Data**: 19 chose Microsoft, 1 chose Google
- **Why binomial?** Binary outcome, independent choices
- **Result**: p < 0.001 (highly significant)

### Mann-Whitney U (for Likert Scales)
- **Why not t-test?** Likert data is ordinal (ordered categories), not interval (equal spacing)
- **What it tests**: Whether one group tends to rank higher than another
- **Why it's appropriate**: Compares ranks, not means - correct for ordinal data

### Shapiro-Wilkes (for Normality Check)
- **Purpose**: Determine if data is normally distributed
- **Finding**: Distributions were not normal → use non-parametric tests

---

## Results

### Overall Preference
| System | Votes | Percentage |
|--------|-------|------------|
| Microsoft | 19 | 95% |
| Google | 1 | 5% |

**Statistical test**: Binomial, p < 0.001

### Ease of Use
| System | Median |
|--------|--------|
| Google | 6 |
| Microsoft | 7 |

**Statistical test**: Mann-Whitney U, p = 0.012

### Accuracy by Difficulty
| Difficulty | Google Median | Microsoft Median | p-value |
|------------|---------------|------------------|---------|
| Easy | 7 | 7 | < 0.001 |
| Medium | 3 | 5 | < 0.01 |
| Hard | 3 | 6.5 | < 0.01 |

**Key insight**: Gap widens as difficulty increases. Google collapses on medium/hard; Microsoft degrades gracefully.

### Accuracy by Nationality
| Nationality | Google Median | Microsoft Median | p-value | Significant? |
|-------------|---------------|------------------|---------|--------------|
| British | 6 | 7 | 0.073 | No |
| Romanian | 5.5 | 7 | 0.018 | Yes |
| Italian | 5 | 5.5 | > 0.05 | No |
| Indian | 4 | 6 | 0.006 | Yes |

**Key insight**: For native English speakers (British), both systems perform similarly. The gap emerges for non-native speakers, especially Romanian and Indian.

---

## Qualitative Findings (User Feedback)

### Google's Problems (Timing)
- "Stops listening before the end of the sentence"
- "It didn't wait long enough for me to speak"
- "Not good with stuttering in long phrases"

### Microsoft's Advantage
- "Takes into account the speed of my speech"
- "Doesn't deliver results prematurely"
- "Little to no frustration compared to Google"

### Shared Weakness (Both Systems)
- "Can't distinguish between similar sounding words (e.g., reed and read)"

**What this reveals**: Google's core issue is **timing/patience** - it cuts off speakers too early. This is an endpoint detection problem, not a recognition problem.

---

## Limitations Acknowledged

| Limitation | Impact | Suggested Fix |
|------------|--------|---------------|
| Test sentences not representative | May not reflect real STT usage (search queries, voice commands) | Use naturalistic sentences |
| Limited nationality diversity | Only 4 nationalities, no American/Australian | Broader recruitment |
| Sample size per group | Only 5 per nationality | Larger sample for nationality conclusions |
| No demographic controls | Age, gender, race not analyzed | Include in future studies |
| Only 2 systems | Google and Microsoft only | Add Amazon, open-source options |

---

## Alignment with Research Methodology Principles

### The 5-Layer Evaluation Framework

| Layer | Expected | Present in Study |
|-------|----------|------------------|
| **1. Standard Benchmarks** | Performance metrics, same protocol | ✓ Likert scales, standardized sentences |
| **2. Ablations (Why)** | Component analysis | ✓ Difficulty breakdown shows where systems differ |
| **3. Controlled Experiments** | Isolated phenomena | ✓ Within-subjects design, controlled sentences |
| **4. Generalization** | Different conditions | ✓ 4 nationalities, 3 difficulty levels |
| **5. Failure Modes** | Where does it break? | ✓ User feedback reveals timing issues |

### Answers the Three Key Questions

| Question | Answer from Study |
|----------|-------------------|
| **Does it work?** | Microsoft outperforms Google on all metrics |
| **Why does it work?** | Microsoft has better timing/patience with speakers |
| **When does it work?** | Gap largest for non-native speakers and complex sentences |

### Statistical Rigor

| Criterion | Met? |
|-----------|------|
| Appropriate tests for data type | ✓ Mann-Whitney for ordinal, binomial for binary |
| Multiple comparisons | ✓ Tested across conditions |
| Honest about non-significant results | ✓ British/Italian results not significant |
| Limitations documented | ✓ Section 4.2 |

---

## The Nuances: What This Study Demonstrates

### Understanding Why Things Break

> "If things break, can you figure out why it's breaking?"

This study doesn't just say "Google scored lower." It identifies:
- **The mechanism**: Timing/endpoint detection
- **The conditions**: Non-native speakers, complex sentences
- **The evidence**: Both quantitative (Likert) and qualitative (comments)

### Appropriate Complexity

> "If you create something very complicated, you will not understand how the parts work."

This study uses:
- Simple, interpretable statistical tests (Mann-Whitney, binomial)
- Clear experimental design (within-subjects, controlled sentences)
- Understandable visualizations (histograms by nationality)

No over-engineering. Each element serves a purpose.

### Intellectual Honesty

> "Being honest about limitations builds trust."

The study explicitly states:
- British and Italian results were not significant
- More data needed to draw nationality conclusions
- Test sentences may not represent real usage

---

## Repository Structure

```
├── analysis.ipynb          # Data analysis notebook
├── README.md               # This file
├── METHODOLOGY.md          # Detailed methodology explanation
├── ALIGNMENT_ANALYSIS.md   # Alignment with interview criteria
└── figures/                # Generated visualizations
    ├── preferencePieChart.pdf
    ├── easeOfUse.pdf
    ├── aggregatedScores.pdf
    └── testCase[1-6].pdf
```

## Requirements

```
pandas
scipy
matplotlib
seaborn
colorcet
numpy
```

## Data Format

CSV with columns:
- Timestamp, Nationality
- 6 Google accuracy ratings (Tests 1-6)
- Google ease of use, Google comments
- 6 Microsoft accuracy ratings (Tests 7-12)
- Microsoft ease of use, Microsoft comments
- Final preference

---

## Core Concepts Explained Simply

### Why Within-Subjects Design?

```
BETWEEN-SUBJECTS (Not used):          WITHIN-SUBJECTS (Used):
Person A → Google                     Person A → Google AND Microsoft
Person B → Microsoft                  Person B → Google AND Microsoft

Problem: Maybe Person A has           Advantage: Same voice tests both
clearer speech than Person B          systems. Any difference MUST be
                                      the system, not the person.
```

### Why Mann-Whitney U, Not T-Test?

```
Likert Scale: 1 ─── 2 ─── 3 ─── 4 ─── 5 ─── 6 ─── 7

T-test assumes: Distance 1→2 = Distance 6→7 (equal intervals)
Reality: We don't know if "Agree" to "Strongly Agree" = "Disagree" to "Neutral"

Mann-Whitney: Compares RANKS, not distances
             "Does one group tend to score higher?" ✓
```

### Why Segment by Difficulty?

```
If you only report overall accuracy:
  "Microsoft is better" → But when? Always? Sometimes?

By segmenting:
  Easy:   Both good (median 7 vs 7)
  Medium: Gap appears (median 3 vs 5)
  Hard:   Gap widens (median 3 vs 6.5)

Insight: Google COLLAPSES on complex sentences. Microsoft DEGRADES GRACEFULLY.
```

### Why Collect Qualitative Feedback?

```
Quantitative: "Google scored lower"  → WHAT happened
Qualitative:  "It cut me off early"  → WHY it happened

The WHY is actionable:
- Not "Google needs better models"
- But "Google needs longer silence threshold"
```

---

## Key Takeaways

1. **Microsoft significantly outperforms Google** in user preference (95%), ease of use, and accuracy

2. **The gap is mechanism-specific**: Google's timing cuts off speakers too early (endpoint detection problem)

3. **The gap is condition-specific**: Larger for non-native speakers and complex sentences

4. **Statistical choices matter**: Mann-Whitney for ordinal data, not t-test

5. **Qualitative data explains quantitative findings**: Numbers show WHAT, comments show WHY

6. **Honest limitations strengthen credibility**: Acknowledging what the data can't support

---

## Quick Reference: Interview Alignment

| AI Researcher Criteria | Evidence in This Study |
|------------------------|------------------------|
| **Does it work?** | Preference, accuracy, ease-of-use all favor Microsoft |
| **Why does it work?** | Qualitative feedback → timing/endpoint detection |
| **When does it work?** | Difficulty + nationality segmentation |
| **Ablation studies** | Difficulty breakdown isolates the phenomenon |
| **Generalization testing** | 4 nationalities, 3 difficulty levels |
| **Failure mode analysis** | User comments document Google's failures |
| **Appropriate statistics** | Mann-Whitney for ordinal, binomial for binary |
| **Honest about limitations** | Section 4.2, non-significant results acknowledged |
| **Not over-engineered** | Simple tests, clear design, each part has a purpose |
