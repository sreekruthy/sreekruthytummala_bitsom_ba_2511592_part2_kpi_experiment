# Task 6: Hypothesis Test Notes

## Metric Being Tested

The primary metric being tested is paid conversion rate.

Paid conversion rate = Users converted to paid / Total users

This metric was selected because the business decision is whether the new onboarding and activation campaign should be launched. A successful campaign should increase the percentage of users who become paying customers.

## Null Hypothesis

The treatment paid conversion rate is less than or equal to the control paid conversion rate.

H0: Treatment paid conversion rate <= Control paid conversion rate

## Alternative Hypothesis

The treatment paid conversion rate is greater than the control paid conversion rate.

H1: Treatment paid conversion rate > Control paid conversion rate

## Test Direction

This is a one-tailed test because the business question is whether the treatment improves paid conversion compared with control.

## Significance Level

The significance level used is 5%.

Alpha = 0.05

## Interpretation Logic

If the p-value is less than 0.05, reject the null hypothesis and conclude that the treatment shows statistically significant improvement in paid conversion rate.

If the p-value is greater than or equal to 0.05, fail to reject the null hypothesis and conclude that there is not enough statistical evidence to launch the treatment based on conversion improvement.

The final business decision should also consider guardrail metrics such as refund rate, support ticket rate, engagement score, days to convert, revenue quality, and segment-level performance.



## Task 7: Hypothesis Test Output

The test used is a one-tailed two-proportion z-test.

The test compares the paid conversion rate of the Control group against the paid conversion rate of the Treatment group.

The p-value from the Excel calculation is entered in the hypothesis test sheet. If the p-value is below 0.05, the null hypothesis is rejected.

Based on the calculated test result, the business interpretation is that the treatment should only be recommended if it improves paid conversion significantly and guardrail metrics remain acceptable.

## Test Inputs
- Control converted users: 22 out of 693 (3.2%)
- Treatment converted users: 50 out of 715 (7.0%)
- Absolute lift: 3.8%
- Relative lift: 120.3%

## Test Output
- Test used: two-proportion z-test
- Z-statistic: 3.252
- One-tailed p-value: 0.0006
- Two-tailed p-value: 0.0011

## Decision Rule
If the one-tailed p-value is below 0.05, reject the null hypothesis and treat the conversion lift as statistically significant evidence in favor of the campaign.

## Business Interpretation
The p-value is below 0.05, so the experiment provides statistical evidence that the treatment improves paid conversion. This result should be interpreted together with refund, support, engagement, days-to-convert, and segment results before making a launch decision.
