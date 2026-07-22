## Week 7 — Issue selection

**Issue link:** https://github.com/ascherj/pathreview/issues/151

**Issue title:** Bias detector patterns are too narrow to match common phrasings
 #151

**Tier:** [x] Tier 1

**Problem summary:**
The regex patterns in bias_detector.py is based on deterministic word-by-word matching (such as using self-taught|online\s+course) to detect if the feedback dismisses the porfolio because online courses are unqualify. Other factors include college background, internship experience, project maturity, age, demographics.

Original logic:
```
    # Genuinely dismissive phrases about educational background
    DISMISSIVE_PATTERNS = [
        r"(?:bootcamp|self-taught|online\s+course)\s+(?:education|training)\s+is\s+(?:insufficient|inadequate|lacks)",
        r"(?:bootcamp|self-taught)\s+(?:graduates?|developers?)\s+(?:lack|missing)\s+(?:rigor|fundamentals|proper\s+training)",
        r"(?:bootcamp|coding\s+bootcamp)\s+(?:doesn't|does\s+not)\s+prepare\s+(?:you|developers?)",
        r"(?:self-taught|bootcamp)\s+is\s+(?:not|never)\s+(?:equal|comparable)\s+to\s+(?:university|traditional|formal)",
    ]

    # Demographic assumptions (about age, background, identity)
    DEMOGRAPHIC_PATTERNS = [
        r"(?:young|old|aged)\s+(?:person|developer|programmer)\s+(?:can't|cannot|won't|will\s+not)",
        r"(?:person\s+from|coming\s+from)\s+(?:poor|rich|working[\s-]?class)",
        r"(?:immigrant|international|foreign)\s+developers?.*(?:can't|cannot|won't|struggle)",
    ]
```

**Branch name:** fix/151-fix-bias-detection

**Setup confirmation:** App runs locally at localhost:5173

**Cohort ledger:** Issue added to cohort ledger

----------------------------------------------------------------------------------
## Week 8 — Reproduction & solution planning

**Reproduction commit link:** [link to commit documenting the reproduced issue]

**Reproduction summary:**
Reproduced issue #151 locally.

Steps:
1. Ran:
   pytest tests/unit/test_bias_detector.py

2. Observed:
   9 failed, 23 passed

3. Example reproduction:
   ```python
   from safety.bias_detector import BiasDetector

   BiasDetector.detect_bias(
       "The candidate only attended a bootcamp, so this project lacks the rigor of a formal CS education"
   )
   -> This returns (False, '') which is an expected failure because we fail to detect the bias in this AI portfolio review

**PLAN.md link:** https://github.com/MeeTrannn/pathreview/blob/fix/151-fix-bias-detection/PLAN.md

**Blockers or open questions:**
[Anything you're still uncertain about going into Week 9, or leave blank]