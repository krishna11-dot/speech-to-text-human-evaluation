# Alignment Analysis: Does This Study Demonstrate Research Competence?

> "The final project will never be the same but the internal nuances and concepts will be the same. That's what is more important to understand."

---

## The Core Question

Does this study (CS5063 Assignment 2) demonstrate understanding of **why research decisions matter**, not just what was done?

---

## Evaluation Against Interview Criteria

### Criterion 1: Evaluation Methodology (5-Layer Framework)

**Layer 1: Standard Benchmarks**

| Expected | Present? | Evidence |
|----------|----------|----------|
| Performance metrics | ✓ | 7-point Likert accuracy scores |
| Variance shown | ✓ | Histograms display full distributions |
| Same protocol for both | ✓ | Within-subjects design |
| Strong baselines | ✓ | Google vs Microsoft (industry leaders) |

**Layer 2: Ablation Studies (Why It Works)**

| Expected | Present? | Evidence |
|----------|----------|----------|
| Component breakdown | ✓ | Easy/Medium/Hard difficulty analysis |
| Interaction analysis | ✓ | Nationality × System comparison |
| Mechanism insight | ✓ | User comments reveal timing issues |

**Layer 3: Controlled Experiments**

| Expected | Present? | Evidence |
|----------|----------|----------|
| Isolated phenomena | ✓ | Each difficulty level tests specific capability |
| Controlled variables | ✓ | Same sentences, same participants for both systems |
| Clear IV/DV | ✓ | System = IV, ratings = DV |

**Layer 4: Generalization Testing**

| Expected | Present? | Evidence |
|----------|----------|----------|
| Different conditions | ✓ | 4 nationalities (accents) |
| Different difficulties | ✓ | 3 difficulty levels |
| Cross-condition consistency | ✓ | Microsoft wins across all difficulty levels |

**Layer 5: Failure Mode Analysis**

| Expected | Present? | Evidence |
|----------|----------|----------|
| Active failure search | ✓ | Open-ended feedback solicited |
| Systematic patterns | ✓ | Google's timing problem identified |
| Boundary conditions | ✓ | Native vs non-native gap documented |

**Assessment**: All 5 layers present. Strong alignment with evaluation methodology principles.

---

### Criterion 2: Statistical Rigor

**Does the study use appropriate statistics?**

| Decision | Rationale | Correct? |
|----------|-----------|----------|
| Binomial test for preference | Binary outcome (Google vs Microsoft), independent choices | ✓ |
| Mann-Whitney U for Likert | Ordinal data requires non-parametric test | ✓ |
| Shapiro-Wilkes for normality | Validates test choice | ✓ |
| Segmented analysis | Tests conditions, not just overall | ✓ |

**What would be wrong (and wasn't done)**:
- T-test on Likert data (assumes interval scale) - **avoided**
- Only reporting overall results without breakdown - **avoided**
- Claiming significance for non-significant results - **avoided** (British/Italian acknowledged as non-significant)

**Assessment**: Statistical choices are appropriate and defensible.

---

### Criterion 3: "If Things Break, Can You Figure Out Why?"

**The debugging mindset applied to research:**

| Observation | Investigation | Finding |
|-------------|---------------|---------|
| Microsoft scores higher overall | Is it consistent across difficulty? | Yes, at all levels |
| Microsoft scores higher overall | Is it consistent across nationalities? | No, varies (significant for Romanian/Indian, not for British/Italian) |
| Google scores lower | What do users say? | Timing issues - cuts off too early |
| Gap larger for some groups | Which ones? | Romanian and Indian speakers |

**The key test**: If someone asked "why does Google perform worse?", can you answer beyond "because the numbers are lower"?

**Answer from this study**: Yes - Google has an endpoint detection problem. It stops listening before speakers finish, especially problematic for non-native speakers who may speak more slowly or with pauses.

**Assessment**: Demonstrates diagnostic thinking. The study identifies **mechanisms**, not just results.

---

### Criterion 4: Understanding Nuances

**Nuances demonstrated in the study:**

1. **Why within-subjects design?**
   - Controls for individual speech patterns
   - Same person tests both → isolates system effect
   - Higher statistical power

2. **Why Mann-Whitney instead of t-test?**
   - Likert is ordinal, not interval
   - Can't assume equal spacing between scale points
   - Study explicitly checked normality first

3. **Why segment by difficulty?**
   - Overall average hides where systems differ
   - Allows "when does it work?" analysis
   - Reveals that gap widens with difficulty

4. **Why include qualitative feedback?**
   - Numbers show THAT Google is worse
   - Comments show WHY (timing)
   - Makes findings actionable

5. **Why segment by nationality?**
   - Tests generalization across accents
   - Reveals that native speakers see smaller gap
   - Points to potential bias in training data

**Assessment**: The study shows awareness of why each methodological choice matters.

---

### Criterion 5: Appropriate Complexity

> "If you create something very complicated, you will not understand how the parts work."

**Is this study appropriately scoped?**

| Element | Appropriate? | Reasoning |
|---------|--------------|-----------|
| Statistical tests | ✓ | Standard, interpretable (Mann-Whitney, binomial) |
| Visualizations | ✓ | Histograms show distributions, pie chart shows preference |
| Segmentation | ✓ | Meaningful groups (difficulty, nationality) |
| Sample size | ✓ | 20 participants, 5 per group - modest but sufficient for main questions |

**What would be over-engineering (and wasn't done)**:
- Bayesian hierarchical models for 20 participants
- Complex interaction models without theoretical justification
- Dozens of arbitrary subgroup analyses

**Assessment**: Complexity matches the problem. Each element serves a clear purpose.

---

### Criterion 6: Intellectual Honesty

> "Being honest about limitations builds trust."

**Limitations acknowledged in the study:**

| Limitation | Acknowledged? | Location |
|------------|---------------|----------|
| Test sentences not representative of real usage | ✓ | Section 4.2 |
| Limited nationality diversity | ✓ | Section 4.2 |
| Only 2 systems tested | ✓ | Section 4.2 |
| Non-significant results for British/Italian | ✓ | Section 4.1.4 |
| Small sample per nationality group | ✓ | Future work section |

**Key statement from the paper**:
> "For British and Italian nationals, the hypothesis that there was a difference could neither be rejected nor denied."

This is exactly what intellectual honesty looks like - not overclaiming when the data doesn't support it.

**Assessment**: Strong intellectual honesty demonstrated.

---

## Interview Question Alignment Summary

### Question 1: Evaluation Methodology

> "You've developed a new method that improves performance on standard benchmarks, but reviewers are skeptical it will generalize. How do you design experiments to convincingly demonstrate your method's value?"

**How this study aligns:**

| Principle from Answer | Present in Study |
|-----------------------|------------------|
| Report variance, not just best results | ✓ Full distributions shown |
| Use exact same protocol as comparison | ✓ Within-subjects design |
| Ablation studies | ✓ Difficulty breakdown |
| Controlled synthetic experiments | ✓ Designed sentences isolate phenomena |
| Out-of-distribution testing | ✓ Multiple nationalities |
| Failure mode analysis | ✓ User feedback analyzed |
| Honest about limitations | ✓ Section 4.2 |

---

### Question 2: Identifying Research Directions

> "How do you decide what research problem to work on?"

**How this study aligns:**

| Principle from Answer | Present in Study |
|-----------------------|------------------|
| **Importance**: Does solving this matter? | ✓ STT systems widely used; bias in AI is critical issue |
| **Tractability**: Can it be solved now? | ✓ Systems available, human evaluation feasible |
| **Fit**: Right team for this? | ✓ 4 researchers from 4 different nationalities |
| Gap between theory and practice | ✓ Automated metrics don't capture usability |
| Recurring pain points | ✓ Accent bias is known issue in STT |

---

### Question 3: Negative/Inconclusive Results

> "You spent months on a research direction that didn't pan out. How do you decide what to do with this work?"

**How this study handles inconclusive results:**

The British and Italian nationality analyses were not statistically significant.

**What the study did:**
1. **Reported honestly**: "could neither be rejected nor denied"
2. **Didn't overclaim**: No claim that nationality has no effect
3. **Identified next step**: "necessary to collect more data samples"
4. **Contextualized**: Other results (Romanian, Indian) were significant

This demonstrates the "Type 1" handling from the interview answer: "The hypothesis was wrong/inconclusive - this is valuable information."

---

### Question 4: Scaling Laws / Resource Allocation

Less directly applicable to this human evaluation study, but the study shows good resource judgment:
- Used convenience sampling due to time constraints (acknowledged)
- Appropriate scope for a course project
- Didn't over-design for available resources

---

## Gap Analysis: What Could Be Stronger?

**Present but could be enhanced:**

| Element | Current State | Enhancement |
|---------|---------------|-------------|
| Effect sizes | P-values reported | Add Cohen's d or rank-biserial correlation |
| Confidence intervals | Not present | Add 95% CIs for key comparisons |
| Order effects | Not addressed | Counterbalancing or analysis |
| Multiple comparisons | Not corrected | Bonferroni or FDR correction |

**These are enhancements, not fundamental flaws.** The core methodology is sound.

---

## Final Assessment

| Interview Criterion | Alignment Level |
|---------------------|-----------------|
| 5-layer evaluation methodology | Strong |
| Statistical appropriateness | Strong |
| Diagnostic thinking ("why it breaks") | Strong |
| Understanding nuances | Strong |
| Appropriate complexity | Strong |
| Intellectual honesty | Strong |

---

## The Meta-Point

> "The moment I see a project and talk to you, I will know that the intricacies are missing. The nuances are missing."

**What this study shows you understand:**

- Why Mann-Whitney instead of t-test (data type matters)
- Why within-subjects design (controls confounds)
- Why segment by difficulty (reveals conditions)
- Why segment by nationality (tests generalization)
- Why include qualitative feedback (explains mechanisms)
- Why acknowledge limitations (builds credibility)

**What would show lack of understanding:**

- "I used Mann-Whitney because scipy has it"
- "I got a significant p-value so it's proven"
- "I can't explain why the gap is larger for Indian speakers"
- "The limitations section is just something reviewers want"

This study demonstrates the former, not the latter.

---

## Conclusion

This CS5063 assignment demonstrates the research thinking patterns that matter:

1. **Multiple layers of evidence** - not just "Microsoft scored higher"
2. **Appropriate methodology** - tests match data types
3. **Mechanism understanding** - timing issues identified via qualitative data
4. **Condition breakdown** - when/where does each system work
5. **Manageable complexity** - each part is understandable
6. **Intellectual honesty** - limitations and non-significant results acknowledged

The work shows someone who understands **why** each analysis choice matters, which is exactly what the interview questions are testing for.
