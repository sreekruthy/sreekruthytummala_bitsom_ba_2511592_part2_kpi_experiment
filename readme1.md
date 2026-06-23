# Part 2: KPI Framework, Business Experiment Analysis, and Decision Recommendation

## Business Context

A subscription-based digital product company tested a new onboarding and activation campaign against the existing onboarding experience. Users were split into Control and Treatment groups.

The dataset is stored in `data/campaign_experiment_data.xlsx`. It contains 1,408 user-level records with experiment group, segment fields, funnel actions, revenue, support tickets, refund requests, days to convert, and engagement score.

## Task 1: Business Problem Statement

Leadership needs to decide whether the new onboarding and activation campaign should be launched to all users, rejected, tested further, or launched only for selected user segments.

This decision impacts new users, the product onboarding team, marketing, customer support, revenue teams, and leadership.

The main metric that should improve is paid conversion rate, calculated as users converted to paid divided by total users.

The risks that must be monitored are refund rate, support ticket rate, engagement score, days to convert, revenue quality, and segment-level declines.

Before making a recommendation, the company needs evidence that the treatment improves paid conversion rate and does not create unacceptable negative impact on guardrail metrics.

## Task 2: North Star Metric

The North Star metric is paid conversion rate.

Paid conversion rate = Users converted to paid / Total users

This metric is the main success metric because the campaign objective is to increase the share of users who become paying customers. A higher paid conversion rate directly supports subscription revenue growth.

Other metrics are supporting metrics. Landing page visit rate, trial start rate, and onboarding completion rate explain funnel movement. Revenue metrics explain conversion quality. Engagement score shows whether users are active. Refund rate and support ticket rate show whether the campaign created customer experience or operational issues.

Optimizing paid conversion blindly could be risky because the campaign may increase low-quality conversions, refunds, support burden, or weaker revenue per converted user. Therefore, guardrails must be evaluated before the final recommendation.

## Task 3: KPI Tree

The KPI tree uses paid conversion rate as the North Star metric.

The primary KPI drivers are activation depth, funnel progression, and revenue quality.

Activation depth includes landing page visit rate, trial start rate, and onboarding completion rate.

Funnel progression includes device experience, traffic source quality, and plan type fit.

Revenue quality includes average revenue per user, average revenue per converted user, and days to convert.

Guardrail metrics include refund rate, support ticket rate, average engagement score, and segment-level decline.

The KPI tree image is saved as `outputs/kpi_tree.png`.

## Task 4: Data Cleaning And Preparation

The dataset was checked for missing values, group counts, duplicate user IDs, invalid binary values, revenue outliers, and segment distribution across experiment groups.

Missing device type values were handled using `device_type_clean`, where blanks were mapped to `Unknown`.

Missing traffic source values were handled using `traffic_source_clean`, where blanks were mapped to `Unknown`.

Missing engagement score values were handled using `engagement_score_clean`, where blanks were replaced with the median engagement score.

Missing days to convert values were expected for users who did not convert to paid, so they were excluded from average days-to-convert calculations.

Support ticket count was converted into `support_ticket_user`, where users with one or more support tickets were marked as 1 and users with no support tickets were marked as 0.

Revenue outliers were flagged using the 1.5x IQR rule and reviewed instead of being removed.

## Task 5: Experiment Summary

The experiment summary compares Control and Treatment across user count, landing page visit rate, trial start rate, onboarding completion rate, paid conversion rate, average revenue per user, average revenue per converted user, refund rate, support ticket rate, average engagement score, and average days to convert.

The summary workbook uses formulas in `outputs/experiment_summary.xlsx`.

Segment-level analysis was completed for region, device type, traffic source, and plan type. For binary metrics such as conversion, refund, support ticket user, trial start, and onboarding completion, the average of the 0/1 field was used as the rate.

## Task 6: Hypothesis Framing

The primary metric tested is paid conversion rate.

Null hypothesis: Treatment paid conversion rate is less than or equal to Control paid conversion rate.

Alternative hypothesis: Treatment paid conversion rate is greater than Control paid conversion rate.

The test is one-tailed because the business question is whether the treatment improves paid conversion.

The significance level is 5%.

## Task 7: Hypothesis Test Analysis

A one-tailed two-proportion z-test was used to compare Control and Treatment paid conversion rates.

The Excel sheet calculates converted users, total users, conversion rates, pooled conversion rate, standard error, z-statistic, one-tailed p-value, two-tailed p-value, and decision rule.

The treatment conversion rate is higher than the control conversion rate, and the p-value is below 0.05. This means the treatment shows statistically significant improvement in paid conversion rate.

## Task 8: Guardrail Evaluation

The recommendation was not based only on paid conversion rate.

Guardrails reviewed include refund rate, support ticket rate, average engagement score, average days to convert, average revenue per user, average revenue per converted user, and segment-level performance.

The treatment improves conversion and engagement, and users convert faster. However, support ticket rate increases, refund rate increases slightly, and average revenue per converted user decreases. These guardrails create rollout risk and should be monitored carefully.

## Task 9: Final Recommendation

Final recommendation: Launch the treatment in a phased rollout with guardrail monitoring.

The treatment should not be ignored because the paid conversion lift is statistically significant. However, a full unmonitored launch is risky because support ticket rate increased and revenue per converted user decreased.

A phased launch allows the business to capture conversion gains while monitoring support demand, refunds, revenue quality, and segment-level performance.

Priority should be given to stronger-performing segments, especially traffic sources and user segments with higher conversion lift and acceptable guardrail behavior.

## Assumptions And Limitations

The dataset is treated as the source of truth.

The experiment assignment is assumed to be random and mutually exclusive.

The analysis uses 30-day outcomes only.

Long-term retention, churn, and lifetime value are not included.

Days to convert is only available for users who converted to paid.

Segment-level results may have smaller sample sizes than the overall experiment.

## Screenshots Included

The screenshots folder includes:

- `summary_metrics.png`
- `hypothesis_test_output.png`
- `kpi_tree_preview.png`