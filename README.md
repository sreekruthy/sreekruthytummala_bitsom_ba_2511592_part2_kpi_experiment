# Part 2: KPI Framework, Experiment Analysis, and Recommendation

## Business Context
A subscription-based digital product company tested a new onboarding and activation campaign against the existing onboarding experience. Users were split into Control and Treatment groups.

## Task 1: Business Problem Statement

The company is a subscription-based digital product company that tested a new onboarding and activation campaign against the existing onboarding experience.

The decision that needs to be made is whether the treatment experience should be launched to all users, rejected, tested further, or launched only for selected user segments.

This decision impacts new users, the product onboarding team, marketing, customer support, revenue teams, and leadership. If the campaign works, more users should move from signup to paid subscription. If it does not work well, it may increase support issues, refunds, or low-quality conversions.

The main metric that should improve is paid conversion rate, calculated as users converted to paid divided by total users.

The risks that must be monitored are refund rate, support ticket rate, engagement score, days to convert, revenue quality, and segment-level declines.

Before making a recommendation, the company needs evidence that the treatment improves paid conversion rate and does not create unacceptable negative impact on guardrail metrics.


### Dataset Description
The dataset is stored in `data/campaign_experiment_data.xlsx`. It contains 1,408 user-level experiment records with group assignment, segment fields, funnel actions, revenue, support, refund, days-to-convert, and engagement score.

## Task 2: North Star Metric

The North Star metric for this experiment is paid conversion rate.

Paid conversion rate is calculated as:

Paid conversion rate = Users converted to paid / Total users

This is the main success metric because the purpose of the onboarding and activation campaign is to increase the number of users who become paying customers. A higher paid conversion rate directly supports subscription revenue growth.

Other metrics are supporting metrics because they explain the journey toward conversion but do not alone prove business success. Landing page visit rate shows whether users entered the campaign flow. Trial start rate shows whether users showed initial product interest. Onboarding completion rate shows whether users completed activation steps. Revenue metrics show whether conversions are financially meaningful. Engagement score shows whether users are active. Refund and support ticket rates show whether the campaign created quality or experience problems.

Paid conversion rate connects to business growth because more paying users increase subscription revenue and create a larger active customer base.

However, optimizing this metric blindly could be risky. The campaign could increase conversions from users who later refund, need more support, generate lower revenue, or have poor engagement. Therefore, guardrail metrics must be evaluated before recommending a launch.


## Task 3: KPI Tree

The KPI tree starts with paid conversion rate as the North Star metric. It is broken into three primary drivers: activation depth, funnel progression, and revenue quality.

Activation depth includes landing page visit rate, trial start rate, and onboarding completion rate. Funnel progression includes device experience, traffic source quality, and plan type fit. Revenue quality includes average revenue per user, average revenue per converted user, and days to convert.

Guardrail metrics include refund rate, support ticket rate, average engagement score, and segment-level decline.



## Task 4: Data Cleaning And Preparation

The dataset was checked for missing values, group counts, duplicate user IDs, invalid binary values, revenue outliers, and segment distribution across experiment groups.

Missing device type values were handled by creating a cleaned field called `device_type_clean`, where blanks were mapped to `Unknown`.

Missing traffic source values were handled by creating `traffic_source_clean`, where blanks were mapped to `Unknown`.

Missing engagement score values were handled by creating `engagement_score_clean`, where blanks were replaced with the median engagement score.

Missing days to convert values were expected for users who did not convert to paid, so they were excluded from average days-to-convert calculations.

Support ticket count was converted into a binary field called `support_ticket_user`, where users with one or more tickets were marked as 1 and users with no tickets were marked as 0.

Revenue outliers were flagged using the 1.5x IQR rule and reviewed instead of being removed.

Duplicate user IDs and invalid binary values were checked explicitly.


## Task 5: Experiment Summary

The experiment summary compares Control and Treatment users across user count, landing page visit rate, trial start rate, onboarding completion rate, paid conversion rate, average revenue per user, average revenue per converted user, refund rate, support ticket rate, average engagement score, and average days to convert.

Segment-level analysis was also completed for region, device type, traffic source, and plan type. For binary metrics such as conversion, refund, trial start, and onboarding completion, the average of the 0/1 field was used as the rate.



## Hypothesis Test Summary
The primary hypothesis test compared Control vs Treatment paid conversion rate using a one-tailed two-proportion z-test at a 5% significance level. The treatment conversion rate was 7.0% vs control at 3.2%, with p = 0.0006.

## Task 8: Guardrail Metric Evaluation

The recommendation was not based only on paid conversion rate. Guardrail metrics were evaluated to check whether the treatment created business or customer experience risks.

Refund rate was reviewed to check whether the treatment created poor-quality conversions.

Support ticket rate was reviewed to check whether the treatment increased customer support burden.

Average engagement score was reviewed to check whether users exposed to the treatment were meaningfully engaged.

Average days to convert was reviewed to check whether the treatment helped users convert faster or slower.

Revenue metrics were reviewed to check whether conversion gains were supported by healthy revenue quality.

Segment-level performance was reviewed to identify whether any user segment performed worse under treatment.

## Final Recommendation
Continue testing before a full launch. The decision is supported by statistically significant paid conversion lift and no major guardrail breach in the summarized metrics.

## Assumptions and Limitations
- The assignment dataset is treated as the source of truth.
- The experiment assignment is assumed random and mutually exclusive.
- The analysis uses 30-day outcomes only.
- Long-term retention, churn, and lifetime value are outside the available dataset.

## Screenshots Included
The `screenshots/` folder contains generated preview images for summary metrics, hypothesis output, and the KPI tree. You can replace them with your own screenshots if required by your submission workflow.
