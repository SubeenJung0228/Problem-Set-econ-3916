# Problem Set 5: Right 93% of the Time

ECON 3916 · Role: Analyst, Credit Risk

A vendor claims its loan-default model is 93% accurate. But 93% of applicants never default, so approving everyone is also 93% accurate. This notebook tests whether the claim means anything and finds the decline threshold that minimises the lender's expected cost.

## What's in the notebook
- **Phase 1:** simulated 6,000 loan applications (7% default rate, 5 real and 4 noise features) and a "predict no default" null model.
- **Phase 2:** logistic regression, LASSO and Ridge (penalty chosen by cross-validation), and a random forest with out-of-bag scoring and feature importance.
- **Phase 3:** precision, recall, ROC AUC and PR AUC, then an expected-cost curve to choose the decline threshold.
- **Phase 4:** AI-assisted checks: McNemar's test (forest vs. logistic) and a calibration review, with full transcripts.

## Recommendation to the Head of Risk

**Recommendation:** I would not accept the vendor's 93% accuracy figure as proof of performance. I would only use the model with a cost-based threshold and choose the penalised logistic model over the random forest.

**Why 93% is misleading.** Approving everyone gives 92.9% accuracy on our test set but catches no defaults. At the default 0.5 threshold, the model catches only 3 out of 106 defaults.

**What the model adds.** The model ranks risk well, with a PR-AUC of 0.23 compared with 0.07 for random flagging. With the right threshold, expected cost drops from \$807 to \$663 per applicant, an 18% reduction. The random forest is no better (lower AUC, McNemar p = 0.25), and the logistic model is easier to explain to regulators.

**Recommended threshold.** Decline applicants when their predicted default probability is above 13%, rather than 50%. This assumes a default loses 60% of principal and wrongly declining a good applicant costs the 8% interest margin plus \$500 in lost relationship value. The general rule is to decline above 1/(1+k), where k is the ratio of the two costs (about 5.6 here). The probabilities passed the calibration check, and thresholds between 0.13 and 0.16 give nearly the same cost.

**What would change my recommendation.** The 13% threshold depends on well-calibrated probabilities. If the default rate among live applicants differs from the 7% in our test data, it may no longer be appropriate, so I would check calibration on an out-of-time sample first.
