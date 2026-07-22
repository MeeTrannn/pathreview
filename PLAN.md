## Solution plan

**Issue link:** https://github.com/ascherj/pathreview/issues/151

**Issue title:** Bias detector patterns are too narrow to match common phrasings
 #151

### Understand
The regex patterns in bias_detector.py is based on deterministic word-by-word matching (such as using self-taught|online\s+course) to detect if the feedback dismisses the porfolio because online courses are unqualify. Other factors include college background, internship experience, project maturity, age, demographics.
Example reproduction:

   ```python
   from safety.bias_detector import BiasDetector

   BiasDetector.detect_bias(
       "The candidate only attended a bootcamp, so this project lacks the rigor of a formal CS education"
   )
   ```
   -> This returns (False, '') which is an expected failure because we fail to detect the bias in this AI portfolio review
   -> What's supposed to happen: "This AI review dequalify the portfolio based on a biased assumption that a bootcamp does not provide formal CS education, instead of evaluate the actual content, curriculum and student achievement in the bootcamp."

### Map
I only need to modify `safety.bias_detector`, the BiasDetector class specificially

### Plan
- Determine if we can only rely on regex pattern or are there alternative ways. Do they give bang for the buck?
- Read the actual text format that the BiasDetector actually reads to understand what information we can rely on to determine bias
- Determine if we need to define other class of biases?
- Change the code and test

### Inputs & outputs
What does your fix take as input? What should it produce or change?

My fix should change the regex patterns, create additional mechanisms to detect biases, create other bias guardrails apart from current bias categories.

Expected outcome: `pytest tests/unit/test_bias_detector.py` would pass on the current 9 failed tests
### Risks & unknowns
What could go wrong? What are you still unsure about?

My initial plan is to use an open language model and create a skill/detect_bias so taht we can incorporate better bias detection rule, for example "Flag as biased feedback if the explanation does not mention explicit personal experiences of the application and instead relying on presumptous general assumption."

However, I just don't know if that fix is unnecessary for this kind of problem.

### Edge cases
What inputs or states should your fix handle gracefully?

What about positive, affirmatice feedback like "The bootcamp experience is good but does not fit our company"

It does not says that the bootcamp experiences disqualify, but they do not provide reasoning why it does not fit the company either. Fit is an subjective judgement.
