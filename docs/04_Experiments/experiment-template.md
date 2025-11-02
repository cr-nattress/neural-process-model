---
title: Experiment Design Template
type: experiment
cognitive_function: meta
ai_mapping: experimental_methodology
last_update: 2025-11-01
tags: [experiment, template, methodology, testing]
---

# 🧪 Experiment Design Template

Use this template for all CSAL experiments. Copy this file and fill in each section.

---

## Experiment Metadata

**Experiment ID:** `EXP-YYYY-MM-NNN` (e.g., EXP-2025-11-001)

**Title:** [Descriptive title of experiment]

**Principal Investigator:** [Name]

**Date Created:** YYYY-MM-DD

**Status:** ☐ Designed | ☐ Running | ☐ Completed | ☐ Failed

**Cognitive Function Tested:** [Executive | Memory | Creativity | Emotion | Learning | Attention | Perception | Social | Metacognition]

**Module(s) Under Test:** [Which cognitive modules are being evaluated]

---

## 1. Background & Motivation

### Research Context
[Describe the broader research question this experiment addresses]

### Neuroscience Basis
[Explain the biological cognitive function or brain region that inspired this]

[Include relevant citations to neuroscience literature]

### Prior Work
[Reference related experiments, either from this project or external research]

---

## 2. Hypothesis

### Primary Hypothesis
[State your main hypothesis clearly and testably]

**Format:** "We hypothesize that [specific condition] will result in [specific observable outcome] because [theoretical reasoning]."

**Example:** "We hypothesize that increasing the capacity of working memory from 7 to 12 items will improve performance on multi-step reasoning tasks by 20% because it reduces the need for memory consolidation during problem-solving."

### Secondary Hypotheses (if any)
[Additional hypotheses to be tested]

---

## 3. Experimental Design

### Independent Variables
[What are you manipulating?]

**Variable 1:** [Name and description]
- Levels: [e.g., Low, Medium, High]
- Values: [Specific values to test]

**Variable 2:** [If applicable]

### Dependent Variables
[What are you measuring?]

**Metric 1:** [Name and description]
- Measurement method: [How will you quantify this?]
- Unit: [Seconds, accuracy %, score, etc.]

**Metric 2:** [If applicable]

### Control Variables
[What are you holding constant?]
- [Variable 1]: [Value]
- [Variable 2]: [Value]

### Experimental Conditions
[Describe each condition to be tested]

**Condition 1:** [Name]
- Description: [What's different in this condition]
- N (sample size): [Number of trials]

**Condition 2:** [Name]
...

---

## 4. Methodology

### Participants/Subjects
- [If human participants: N, demographics, recruitment method, consent process]
- [If AI agents: Which cognitive architecture version, configuration details]
- [If simulation: Environment description]

### Materials
- Datasets: [Which datasets will be used]
- Software: [Code version, dependencies]
- Hardware: [Computational resources]

### Procedure

**Step-by-step protocol:**

1. [Initialization/Setup]
   - [Specific actions]

2. [Stimulus Presentation / Task Administration]
   - [Details of what the system/participant will do]

3. [Data Collection]
   - [What data will be logged, at what frequency]

4. [Iteration]
   - [How many trials, randomization, counterbalancing]

5. [Completion Criteria]
   - [When does the experiment end]

### Task Description
[Detailed description of the cognitive task]

**Example:**
```
Task: N-Back Working Memory Test
- Present sequence of stimuli (letters)
- Participant must indicate if current stimulus matches
  the one from N steps back
- N = 2 (2-back condition)
- 50 trials per condition
- Response time and accuracy recorded
```

---

## 5. Biological Benchmark (if applicable)

### Human/Animal Performance
[What do we know about biological performance on this task?]

**Reference Study:** [Citation]
- Performance metric: [e.g., 75% accuracy, 500ms response time]
- Sample: [e.g., healthy adults, rats in maze]

### Target Performance
[What would constitute "biologically plausible" performance for the AI system?]

---

## 6. Success Criteria

### Primary Success Criterion
[What result would confirm your hypothesis?]

**Criterion:** [Specific, measurable threshold]

**Example:** "Accuracy > 80% on task AND statistically significant improvement over baseline (p < 0.05)"

### Secondary Success Criteria
[Additional metrics that would support your findings]

---

## 7. Data Collection Plan

### Data to be Logged
- [Data type 1]: [Format, storage location]
- [Data type 2]: [Format, storage location]

### Logging Mechanism
```python
# Example logging code structure
class ExperimentLogger:
    def log_trial(self, trial_data: TrialData):
        """Log data for each experimental trial"""
        ...

    def log_performance(self, metrics: PerformanceMetrics):
        """Log summary performance metrics"""
        ...
```

### Data Storage
- **Location:** `/data/results/EXP-YYYY-MM-NNN/`
- **Format:** [CSV, JSON, HDF5, etc.]
- **Metadata:** [What metadata will be included]

---

## 8. Analysis Plan

### Statistical Methods
[Which statistical tests will you use?]

**Example:**
- Paired t-test to compare conditions
- ANOVA for multi-condition comparison
- Linear regression for correlation analysis

### Visualization
[What plots/graphs will you create?]
- [Plot type 1]: [What it shows]
- [Plot type 2]: [What it shows]

### Software
- Analysis: [pandas, scipy, R, etc.]
- Visualization: [matplotlib, seaborn, ggplot]

---

## 9. Expected Outcomes

### Predicted Results
[What do you expect to find?]

[Include sketches of expected graphs if helpful]

### Alternative Outcomes
**If hypothesis is not supported:**
- Possible explanation 1: [...]
- Possible explanation 2: [...]
- Next steps: [...]

---

## 10. Risks & Limitations

### Potential Issues
[What could go wrong?]
- Risk 1: [Description and mitigation strategy]
- Risk 2: [Description and mitigation strategy]

### Limitations
[What are the constraints of this experiment?]
- [e.g., Limited sample size]
- [e.g., Simplified task environment]
- [e.g., Only tests one cognitive module in isolation]

---

## 11. Timeline

| Milestone | Target Date | Status |
|-----------|------------|--------|
| Experiment designed | YYYY-MM-DD | ☐ |
| Code implemented | YYYY-MM-DD | ☐ |
| Data collection started | YYYY-MM-DD | ☐ |
| Data collection completed | YYYY-MM-DD | ☐ |
| Analysis completed | YYYY-MM-DD | ☐ |
| Report written | YYYY-MM-DD | ☐ |

**Total Duration:** [X weeks/months]

---

## 12. Resources Required

### Computational
- CPU/GPU hours: [Estimate]
- Memory: [Estimate]
- Storage: [Estimate]

### Human
- Researcher time: [Hours/days]
- [Other personnel if applicable]

### Budgetary
- API costs (if using external LLMs): [Estimate]
- Cloud computing: [Estimate]
- Other: [...]

---

## 13. Ethical Considerations

### Human Subjects (if applicable)
- IRB approval: ☐ Required | ☐ Not Required
- Consent form: [Link to form]
- Data anonymization: [Method]

### AI Ethics
- Potential for harm: [Assessment]
- Bias concerns: [Mitigation strategy]
- Transparency: [How will results be shared]

---

## 14. Results (To be completed after experiment)

### Summary Statistics
[Fill in after data collection]

| Condition | Metric 1 | Metric 2 | N |
|-----------|----------|----------|---|
| Control | | | |
| Experimental | | | |

### Statistical Tests
[Report test results, p-values, effect sizes]

### Visualization
[Include key plots]

---

## 15. Discussion (To be completed after experiment)

### Interpretation
[What do the results mean?]

### Comparison to Biological Benchmarks
[How does AI performance compare to brain performance?]

### Hypothesis Evaluation
- Primary hypothesis: ☐ Supported | ☐ Not Supported | ☐ Inconclusive
- Secondary hypotheses: [...]

### Unexpected Findings
[Anything surprising?]

---

## 16. Conclusions & Next Steps

### Key Takeaways
[Main lessons learned]

### Implications for CSAL
[How does this inform the broader project?]

### Future Experiments
[What should be tested next?]

**Proposed Follow-Ups:**
1. [Experiment idea 1]
2. [Experiment idea 2]

---

## 17. References

[List all citations in APA format]

---

## Appendices

### Appendix A: Code
[Link to experiment code repository]

### Appendix B: Data
[Link to raw data files]

### Appendix C: Supplementary Figures
[Additional visualizations]

---

**Experiment Template Version:** 1.0
**Template Last Updated:** 2025-11-01

---

## Example Usage

See example experiments:
- `/docs/04_Experiments/examples/working-memory-capacity.md`
- `/docs/04_Experiments/examples/attention-filtering-accuracy.md`
- `/docs/04_Experiments/examples/creativity-dual-process.md`
