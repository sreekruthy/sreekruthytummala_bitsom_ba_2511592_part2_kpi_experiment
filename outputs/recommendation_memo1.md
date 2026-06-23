# Recommendation Memo

## Task 1: Business Problem

Leadership needs to decide whether the new onboarding and activation campaign should be launched to all users, rejected, tested further, or launched only for selected segments.

The decision impacts new users, product onboarding, marketing, customer support, revenue teams, and leadership.

The main metric that should improve is paid conversion rate. The risks that must be monitored are refund rate, support ticket rate, engagement score, days to convert, revenue quality, and segment-level decline.

## Task 2: North Star Metric

The North Star metric is paid conversion rate.

Paid conversion rate was selected because the objective of the campaign is to improve user conversion and create more paying subscribers.

Supporting metrics such as landing page visit rate, trial start rate, onboarding completion rate, revenue per user, engagement score, refund rate, and support ticket rate explain the result but are not the main success metric.

## Task 3: KPI Tree Explanation

The KPI tree connects paid conversion rate to activation depth, funnel progression, and revenue quality.

Activation depth includes landing page visits, trial starts, and onboarding completions.

Funnel progression includes device experience, traffic source quality, and plan type fit.

Revenue quality includes average revenue per user, average revenue per converted user, and days to convert.

Guardrail metrics include refund rate, support ticket rate, engagement score, and segment-level decline.

## Task 4: Data Preparation Summary

The dataset was checked for missing values, group counts, duplicate user IDs, invalid binary values, revenue outliers, and segment balance.

Cleaned fields were created for device type, traffic source, engagement score, and support ticket users.

Missing device and traffic source values were mapped to Unknown. Missing engagement scores were replaced with the median engagement score. Missing days to convert values were treated as expected for users who did not convert.

## Task 5: Experiment Result Summary

The experiment summary compares Control and Treatment across user count, landing page visit rate, trial start rate, onboarding completion rate, paid conversion rate, average revenue per user, average revenue per converted user, refund rate, support ticket rate, average engagement score, and average days to convert.

The results are calculated using formulas in `outputs/experiment_summary.xlsx`.

Overall, Treatment improves paid conversion rate compared with Control. Treatment also improves onboarding completion, engagement score, and average days to convert.

## Task 6: Hypothesis Setup

Null hypothesis: Treatment paid conversion rate is less than or equal to Control paid conversion rate.

Alternative hypothesis: Treatment paid conversion rate is greater than Control paid conversion rate.

The test is one-tailed with a 5% significance level.

## Task 7: Hypothesis Test Interpretation

The hypothesis test uses a two-proportion z-test to compare Control and Treatment paid conversion rates.

The treatment paid conversion rate is higher than the control paid conversion rate. The one-tailed p-value is below 0.05, so the null hypothesis is rejected.

This means the treatment shows statistically significant improvement in paid conversion rate.

## Task 8: Guardrail Analysis

Guardrail metrics were reviewed before making the final recommendation.

Engagement score improves under Treatment, and average days to convert decreases, which are positive signs.

However, support ticket rate increases under Treatment. Refund rate also increases slightly, and average revenue per converted user decreases. These guardrails indicate that the campaign may be creating more conversions, but not all conversions may be equally high quality.

Because of these risks, the recommendation should not be a fully unmonitored launch.

## Task 9: Final Recommendation

Final recommendation: Launch the treatment in a phased rollout with guardrail monitoring.

The treatment should be launched carefully because the paid conversion improvement is statistically significant. However, support tickets, refunds, and revenue per converted user should be monitored closely.

A phased launch is better than a full immediate launch because it allows the company to capture conversion gains while controlling operational and revenue-quality risk.

The rollout should prioritize stronger-performing segments and continue monitoring weaker or riskier segments before scaling completely.

## Risks And Limitations

The analysis is based on 30-day experiment data only. Long-term retention, churn, and lifetime value are not available.

Missing values were handled through cleaned helper fields, but missingness may still affect interpretation.

Days to convert is only available for converted users, so it should be interpreted carefully.

Segment-level results may have smaller sample sizes than the overall experiment.

## Next Steps

Monitor support ticket rate, refund rate, engagement score, ARPU, revenue per converted user, and segment-level conversion after rollout.

Review customer support reasons for Treatment users.

Track longer-term retention and churn once additional data is available.

Continue testing or limit rollout if guardrail risks increase after launch.