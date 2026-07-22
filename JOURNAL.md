## Week 7 — Issue selection

**Issue link:** https://github.com/ascherj/pathreview/issues/151

**Issue title:** Bias detector patterns are too narrow to match common phrasings
 #151

**Tier:** [x] Tier 1

**Problem summary:**
The regex patterns in bias_detector.py is based on deterministic word-by-word matching (such as using self-taught|online\s+course) to detect if the feedback dismisses the porfolio because online courses are unqualify. Other factors include college background, internship experience, project maturity, age, demographics.


**Branch name:** fix/151-fix-bias-detection

**Setup confirmation:** App runs locally at localhost:5173

**Cohort ledger:** Issue added to cohort ledger