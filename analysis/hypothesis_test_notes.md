# Task 6: Hypothesis Test Notes


## Null Hypothesis

The treatment paid conversion rate is less than or equal to the control paid conversion rate.

H0: Treatment paid conversion rate <= Control paid conversion rate

---

## Alternative Hypothesis

The treatment paid conversion rate is greater than the control paid conversion rate.

H1: Treatment paid conversion rate > Control paid conversion rate

---

## Test Direction

This is a one-tailed test because the business question is whether the treatment improves paid conversion compared with control.

---

## Significance Level

The significance level used is 5%.

Alpha = 0.05

---

## Metric Being Tested

The primary metric being tested is paid conversion rate.

Paid conversion rate = Users converted to paid / Total users

---

## Reason for choosing that metric

This metric was selected because the business decision is whether the new onboarding and activation campaign should be launched. A successful campaign should increase the percentage of users who become paying customers.

--

## Interpretation Logic

If the p-value is less than 0.05, reject the null hypothesis and conclude that the treatment shows statistically significant improvement in paid conversion rate.

If the p-value is greater than or equal to 0.05, fail to reject the null hypothesis and conclude that there is not enough statistical evidence to launch the treatment based on conversion improvement.

The final business decision should also consider guardrail metrics such as refund rate, support ticket rate, engagement score, days to convert, revenue quality, and segment-level performance.


---

# Task 7: Hypothesis Test Output

The test used is a one-tailed two-proportion z-test. This test was chosen because
the experiment compares two independent groups (Control and Treatment) on a binary
outcome (converted to paid: yes or no), and both group sizes (693 and 715) are 
large enough to satisfy the normal approximation conditions for a z-test.

---

## Test Inputs
- Control converted users: 22 out of 693 (3.2%)
- Treatment converted users: 50 out of 715 (7.0%)
- Absolute lift: 3.8 percentage points
- Relative lift: 120.3%

---

## Test Output
- Test used: One-tailed two-proportion z-test
- Z-statistic: 3.252
- One-tailed p-value: 0.0006
- Two-tailed p-value: 0.0011
- 95% confidence interval for the lift: approximately [1.5pp, 6.2pp]

---

## Decision Rule
If the one-tailed p-value is below alpha = 0.05, we reject the null hypothesis and 
conclude that the treatment conversion lift is statistically significant.

---

## Business Interpretation
The one-tailed p-value is 0.0006, which is well below alpha = 0.05. The null 
hypothesis is rejected. The treatment group shows a statistically significant 
improvement in paid conversion rate: 7.0% versus 3.2% in Control, a lift of 3.8 
percentage points (120.3% relative improvement).

This result is unlikely to be due to random variation. The z-statistic of 3.252 
is more than 3 standard deviations above the null, and the 95% confidence interval 
for the lift does not include zero, confirming the finding is robust.

However, statistical significance alone does not justify a launch. Three guardrail 
metrics — support ticket rate (+68.2%), revenue per converted user (−52.7%), and 
refund rate (+0.4pp) — indicate the quality and cost profile of new conversions 
needs to be monitored. The final recommendation is a phased rollout with guardrail 
monitoring rather than an immediate full launch.

---
