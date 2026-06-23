# Hypothesis Test Notes

## Task 6: Hypothesis Framing

### Metric Being Tested

The primary metric being tested is paid conversion rate.

Paid conversion rate = Users converted to paid / Total users

This metric was selected because the business decision is whether the new onboarding and activation campaign should be launched. A successful campaign should increase the percentage of users who become paying customers.

### Null Hypothesis

The treatment paid conversion rate is less than or equal to the control paid conversion rate.

H0: Treatment paid conversion rate <= Control paid conversion rate

### Alternative Hypothesis

The treatment paid conversion rate is greater than the control paid conversion rate.

H1: Treatment paid conversion rate > Control paid conversion rate

### Test Direction

This is a one-tailed test because the business question is whether the treatment improves paid conversion compared with control.

### Significance Level

The significance level used is 5%.

Alpha = 0.05

### Interpretation Logic

If the p-value is less than 0.05, reject the null hypothesis and conclude that the treatment shows statistically significant improvement in paid conversion rate.

If the p-value is greater than or equal to 0.05, fail to reject the null hypothesis and conclude that there is not enough statistical evidence to launch the treatment based on conversion improvement.

The final business decision should also consider guardrail metrics such as refund rate, support ticket rate, engagement score, days to convert, revenue quality, and segment-level performance.

## Task 7: Hypothesis Test Analysis

The test used is a one-tailed two-proportion z-test.

The test compares the paid conversion rate of the Control group against the paid conversion rate of the Treatment group.

The Excel calculation includes:

- Control converted users
- Control total users
- Control paid conversion rate
- Treatment converted users
- Treatment total users
- Treatment paid conversion rate
- Absolute lift
- Relative lift
- Pooled conversion rate
- Standard error
- Z-statistic
- One-tailed p-value
- Two-tailed p-value
- Decision rule

The p-value from the Excel calculation is compared with alpha = 0.05.

If the p-value is below 0.05, the null hypothesis is rejected.

If the p-value is greater than or equal to 0.05, the null hypothesis is not rejected.

Based on the calculated result, the treatment shows statistically significant improvement in paid conversion rate. The business decision should still consider guardrail metrics before full rollout.