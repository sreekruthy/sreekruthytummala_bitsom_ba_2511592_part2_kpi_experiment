# Recommendation Memo


## Task 1: Business Problem

Leadership needs to decide whether the new onboarding and activation campaign should be launched to all users. The decision impacts new users, product onboarding, marketing, customer support, revenue teams, and leadership.

The main metric that should improve is paid conversion rate. The risks that must be monitored are refund rate, support ticket rate, engagement score, days to convert, revenue quality, and segment-level decline.

## Task 2: North Star Metric

The North Star metric is paid conversion rate.

Paid conversion rate was selected because the objective of the campaign is to improve user conversion and early engagement in a way that creates more paying customers.

Supporting metrics such as landing page visit rate, trial start rate, onboarding completion rate, revenue per user, engagement score, refund rate, and support ticket rate help explain the result but are not the main success metric.

## Task 3: KPI Tree Explanation

The KPI tree connects paid conversion rate to activation depth, funnel progression, and revenue quality.

Activation depth includes landing page visits, trial starts, and onboarding completions.

Funnel progression includes device experience, traffic source quality, and plan type fit.

Revenue quality includes average revenue per user, average revenue per converted user, and days to convert.

Guardrail metrics include refund rate, support ticket rate, engagement score, and segment-level decline.

## Task 4: Data Preparation Summary

The dataset was checked for missing values, group counts, duplicate user IDs, invalid binary values, revenue outliers, and segment balance.

Cleaned fields were created for device type, traffic source, engagement score, and support ticket users.

Missing device and traffic source values were mapped to Unknown. Missing engagement scores were replaced with the median engagement score for analysis. Missing days to convert values were treated as expected for users who did not convert.

## Task 5: Experiment Result Summary

The experiment summary compares Control and Treatment across user count, landing page visit rate, trial start rate, onboarding completion rate, paid conversion rate, average revenue per user, average revenue per converted user, refund rate, support ticket rate, average engagement score, and average days to convert.

The final values should be taken from the formula-based `Control_vs_Treatment` sheet in `outputs/experiment_summary.xlsx`.

## Task 6: Hypothesis Setup

Null hypothesis: Treatment paid conversion rate is less than or equal to Control paid conversion rate.

Alternative hypothesis: Treatment paid conversion rate is greater than Control paid conversion rate.

The test is one-tailed with a 5% significance level.

## Task 7: Hypothesis Test Interpretation

The hypothesis test uses a two-proportion z-test to compare Control and Treatment paid conversion rates.

If the p-value is less than 0.05, the treatment shows statistically significant improvement in paid conversion rate.

If the p-value is greater than or equal to 0.05, the treatment does not have enough statistical evidence for a full launch.

## Task 8: Guardrail Analysis

Guardrail metrics were reviewed before making the final recommendation. These included refund rate, support ticket rate, average engagement score, average days to convert, revenue quality, and segment-level performance.

If conversion improves but support tickets, refunds, or poor-quality revenue also increase significantly, the campaign should not be launched without further investigation.

## Task 9: Final Recommendation

Based on the formula-based experiment summary and hypothesis test output, the final recommendation should be one of the following:

- Launch
- Do not launch
- Launch only for selected segment
- Continue testing

The recommended decision should be supported by the paid conversion result, p-value, guardrail metrics, and segment-level insights.

Final recommendation: [Write your final recommendation here after reviewing your Excel results.]

## Risks And Limitations

The analysis is based on 30-day experiment data only. Long-term retention, churn, and lifetime value are not available in the dataset.

Missing values were handled through cleaned helper fields, but missingness may still affect interpretation.

Days to convert is only available for converted users, so it should be interpreted carefully.

Segment-level results may have smaller sample sizes than the overall experiment.

## Next Steps

Monitor guardrail metrics after launch.

Track retention and churn once longer-term data is available.

Review segment-level performance before scaling the campaign fully.

Continue testing if guardrail risks are high or if results are inconsistent across key segments.



## Business Problem

Leadership needs to decide whether to launch the new onboarding and activation campaign. The campaign should improve paid conversion rate, but the decision must also consider refund rate, support ticket rate, engagement score, days to convert, revenue quality, and segment-level performance.

## Executive Summary
The treatment increased paid conversion from 3.2% to 7.0%, an absolute lift of 3.8% and a relative lift of 120.3%. The one-tailed two-proportion z-test returned p = 0.0006, which is statistically significant at the 5% level.

Recommendation: **Continue testing before a full launch.**

## North Star Metric
The North Star metric is paid conversion rate. It directly connects onboarding effectiveness to subscription growth because it measures whether users become paying customers after exposure to the campaign.

Supporting metrics such as landing page visits, trial starts, onboarding completion, ARPU, engagement, refunds, and support tickets explain why conversion changed and whether the change is healthy. They are not the North Star because they can improve without producing sustainable paid customers.

Optimizing paid conversion blindly could create low-quality conversions, more refunds, higher support demand, or poor experiences in specific segments.

## KPI Tree Explanation
The KPI tree breaks paid conversion into activation depth, funnel progression, and revenue quality. Guardrails include refund rate, support ticket rate, and engagement score.

## Experiment Result Summary
- Control users: 693
- Treatment users: 715
- Control paid conversion: 3.2%
- Treatment paid conversion: 7.0%
- Control ARPU: $51.75
- Treatment ARPU: $53.88
- Control onboarding completion: 15.6%
- Treatment onboarding completion: 21.3%

## Hypothesis Test Interpretation
The one-tailed p-value of 0.0006 is below 0.05, so the conversion lift is unlikely to be random noise under the null hypothesis.

## Guardrail Analysis
| Metric | Control | Treatment | Absolute delta | Relative change | Risk assessment |
| --- | --- | --- | --- | --- | --- |
| Average revenue per user | $51.75 | $53.88 | $2.13 | 4.1% | Acceptable |
| Average revenue per converted user | $1,630.10 | $770.41 | $-859.69 | -52.7% | Watch |
| Refund rate | 0.0% | 0.4% | 0.4% |  | Watch |
| Support ticket rate | 14.7% | 24.8% | 10.0% | 68.2% | Watch |
| Average engagement score | 57.05 | 62.90 | 5.85 | 10.2% | Acceptable |
| Average days to convert | 8.86 | 6.40 | -2.46 | -27.8% | Acceptable |

## Segment-Level Insight
The strongest segment-level conversion lift was observed in Traffic Source = Referral, with an absolute paid conversion lift of 8.5%. This segment can be prioritized in rollout monitoring.

## Final Recommendation
Launch the treatment broadly, with weekly monitoring of refund rate, support ticket rate, engagement score, ARPU, and segment-level conversion. If operations capacity is constrained, prioritize the strongest positive segments first.

## Risks and Limitations
- Missing device, traffic source, and engagement values were handled with explicit unknown/imputed fields for analysis.
- Days to convert is only observed for converted users, so it is not comparable across all users.
- The dataset covers 30-day outcomes only; long-term retention and churn are not measured.
- Revenue quality should be monitored beyond the initial conversion window.

## Next Steps
- Prepare rollout dashboard for the same KPIs.
- Monitor guardrails by segment after launch.
- Run retention and churn analysis once longer-term data is available.
