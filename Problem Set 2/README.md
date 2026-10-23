# Problem Set 2 — The Survey That Wasn't Random

**ECON 3916 · Applied Data Analytics · Topics 5–8**

## Objective
A product manager wanted to report that satisfaction rose from 3.6 to 4.3 after an onboarding redesign. I tested whether an in-app survey, answered only by users who chose to respond, could support that claim.

## What I did
- Simulated 50,000 users before and after the redesign with a known true answer: mean satisfaction of 3.291 before and 3.391 after, a true improvement of 0.100 points.
- Added a response mechanism in which more satisfied users are more likely to answer, and reproduced the PM's numbers: the survey showed 3.592 before and 4.309 after, a gap of 0.717 points, while response rates fell from 27.5% to 15.3%.
- Bootstrapped the mean and median of the survey responses by hand and with scipy, comparing percentile and BCa intervals.
- Ran a 400-repetition coverage simulation to check how often the survey's 95% interval contains the true mean.
- Ran the PM's two-sample test, a power analysis, and a simulation of surveys of different sizes.
- Used AI to try inverse-probability weighting on engagement and support tickets, and checked the result against the known truth.

## Key findings
- **Nonresponse bias:** The 0.717-point gap is mostly created by who answers the survey, not by a real change in satisfaction. Because response depends on satisfaction itself, the missing data are MNAR.
- **Precise but wrong:** The bootstrap interval for the post-redesign mean was [4.294, 4.325], far above the true mean of 3.391. Across 400 repeated surveys, the 95% interval never contained the truth.
- **Significance is not the issue:** The PM's test is highly significant (t = 66.33, Cohen's d = 0.911), but it compares two biased samples.
- **More data does not help:** Larger surveys shrank the spread of the error from 0.110 to 0.014, but the bias stayed at about +0.92 points.
- **Weighting does not fix it:** Weighting on the covariates moved the estimate only from 4.309 to 4.137, because the covariates cannot capture a response decision driven by satisfaction itself.

## Recommendation
Survey a random sample of users and follow up with non-respondents, so that whether someone responds no longer depends on how satisfied they are.
