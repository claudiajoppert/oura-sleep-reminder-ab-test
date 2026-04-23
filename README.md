# Oura Sleep Reminder A/B Test

> **A portfolio analysis testing whether a nightly bedtime reminder increases Oura app engagement.** Built in R, written for a business audience.

## The question in one line

Does sending a nightly push notification reminding users to wind down get them to open the app more often in the following week?

## The answer

Yes. Users who received the reminder opened the app about 7% more over the test week. The lift is small but consistent, and the evidence is statistically reliable. Full write-up in the notebook.

**Recommendation:** Roll out to all users, with a longer holdout to confirm the lift is durable.

## What makes this project different

Most A/B test portfolio examples stop at a t-test and a p-value. This one goes further:

- **Power analysis before the test**, not after. Sample size is justified up front, the way it would be in a real experimentation platform.
- **CUPED variance reduction** applied as a secondary analysis. Shows fluency with modern experimentation tooling used at companies like Microsoft, Netflix, and Airbnb.
- **Business-first writing.** The report opens with the recommendation, not the methods. Statistical terms are translated into plain English for non-technical stakeholders.
- **Honest caveats.** The recommendation section lists specific follow-ups (notification fatigue, segment analysis, downstream sleep metrics) rather than declaring victory.

## What's in this repo

| File | What it is |
|---|---|
| `oura_sleep_reminder_ab_test.Rmd` | The analysis notebook, written in R Markdown |
| `oura_sleep_reminder_ab_test.html` | The rendered report. Open this in a browser to read |
| `oura_ab_test_data.csv` | The dataset, 10,000 users across two groups |

## Methods

Randomized A/B test design:

- 5,000 users per arm (control and treatment)
- Primary outcome: app opens in the 7 days following enrollment
- Sample size chosen before the test using a power analysis targeting a 5% minimum detectable lift at 80% power and a 0.05 significance level
- Primary analysis: Welch's two-sample t-test
- Secondary analysis: CUPED variance reduction using pre-period app opens as the covariate
- Balance check on pre-period means to validate random assignment

## Tools

R, tidyverse, broom, pwr, rmarkdown, knitr. Rendered output is self-contained HTML.

## How to reproduce

Clone the repo, open the project folder in RStudio, install packages:

```r
install.packages(c("tidyverse", "broom", "pwr", "scales", "knitr", "rmarkdown"))
```

Then open `oura_sleep_reminder_ab_test.Rmd` and click Knit.

## A note on the data

The dataset is simulated for portfolio purposes. It is calibrated to match realistic engagement patterns: user-level heterogeneity in baseline app usage, a correlation between pre-period and post-period behavior, and a treatment effect that varies across users rather than applying uniformly. The analysis pipeline is identical to what would run on real experiment data.

## Limitations

Worth naming up front:

- **Synthetic data.** Real production data would have missing values, attrition, and metric definitions that require cleaning decisions.
- **Single outcome.** A real rollout would track guardrail metrics (uninstalls, notification opt-outs) alongside the primary metric.
- **Short window.** Seven days is too short to observe notification fatigue or churn.
- **No heterogeneous effect analysis.** The average lift hides variation across user segments. A follow-up using causal forests or pre-registered segment cuts would sharpen the rollout plan.

## Author

**Claudia Joppert**

Data analytics portfolio project, 2026.
