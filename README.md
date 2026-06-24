# Part 2: KPI Framework, Business Experiment Analysis, and Decision Recommendation

## Business Context

A subscription-based digital product company tested a new onboarding and activation campaign against its existing onboarding experience. Users were split into two groups:

- **Control group:** Existing onboarding experience (693 users)
- **Treatment group:** New campaign experience (715 users)

Leadership needs to decide whether the treatment should be launched to all users, rejected, tested further, or launched only for selected segments.

---

## Dataset Description

The dataset is stored in `data/campaign_experiment_data.xlsx`. It contains 1,408 user-level experiment records with the following fields:

- Experiment group assignment (Control / Treatment)
- Segment fields: region, device type, traffic source, plan type
- Funnel actions: visited landing page, started trial, completed onboarding, converted to paid
- Outcome fields: revenue (30-day), support tickets (30-day), refund requested
- Engagement fields: engagement score, days to convert

Dataset link: https://drive.google.com/drive/folders/1AONQ3QSPVvn-A2bWANT0bFtljK1_PSTS


---

## Task 1: Business Problem 

The decision that needs to be made is whether the new onboarding and activation campaign should be launched to all users, rejected, tested further, or launched only for selected user segments.

This decision impacts new users, the product onboarding team, marketing, customer support, revenue teams, and leadership. If the campaign works, more users should move from signup to paid subscription. If it does not work well, it may increase support issues, refunds, or low-quality conversions.

The main metric that should improve is paid conversion rate, calculated as users converted to paid divided by total users.

The risks that must be monitored are refund rate, support ticket rate, engagement score, days to convert, revenue quality, and segment-level declines.

Before making a recommendation, the company needs evidence that the treatment improves paid conversion rate and does not create unacceptable negative impact on guardrail metrics.

---

## Task 2: North Star Metric Selected

**North Star Metric: Paid Conversion Rate**

Paid conversion rate = Users converted to paid / Total users

This is the main success metric because the purpose of the onboarding and activation campaign is to increase the number of users who become paying customers. A higher paid conversion rate directly supports subscription revenue growth.

Other metrics are supporting metrics because they explain the journey toward conversion but do not alone prove business success. Landing page visit rate shows whether users entered the campaign flow. Trial start rate shows whether users showed initial product interest. Onboarding completion rate shows whether users completed activation steps. All these explain funnel movement but do not alone prove business success. Revenue metrics show whether conversions are financially meaningful. Engagement score shows whether users are active. Refund and support ticket rates show whether the campaign created customer experience or operational issues.

Paid conversion rate connects to business growth because more paying users increase subscription revenue and create a larger active customer base.

However, optimizing this metric blindly could be risky. The campaign could increase conversions from users who later refund, need more support, generate lower revenue, or have poor engagement. Therefore, guardrail metrics must be evaluated before recommending a launch.

---

## Task 3: KPI Tree Summary

The KPI tree uses paid conversion rate as the North Star metric and breaks it into three primary drivers:

**1. Activation Depth**
- Landing page visit rate
- Trial start rate
- Onboarding completion rate

**2. Funnel Progression**
- Device experience
- Traffic source quality
- Plan type fit

**3. Revenue Quality**
- Average revenue per user
- Average revenue per converted user
- Days to convert

**Guardrail Metrics**
- Refund rate
- Support ticket rate
- Average engagement score
- Segment-level decline

The KPI tree image is saved as `outputs/kpi_tree.png`. A preview screenshot is at `screenshots/kpi_tree_preview.png`.

---

## Task 4: Data Cleaning and Preparation 

The dataset was checked for the following issues, documented in `analysis/experiment_analysis.xlsx` on the `Quality checks` sheet:

| Check | Result | Handling |
| --- | --- | --- |
| Total rows | 1,408 | Used as analysis base |
| Duplicate user IDs | 8 | Flagged for deduplication before analysis |
| Group count: Control | 693 | Used in balance review |
| Group count: Treatment | 715 | Used in balance review |
| Missing values: device_type | 18 | Mapped to Unknown in `device_type_clean` |
| Missing values: traffic_source | 24 | Mapped to Unknown in `traffic_source_clean` |
| Missing values: engagement_score | 14 | Median imputed in `engagement_score_clean` |
| Missing values: days_to_convert | 1,336 | Expected for non-converters; excluded from averages |
| Invalid binary values | 0 | No action needed across all binary columns |
| Revenue outliers | Flagged via 1.5x IQR | Reviewed, not removed |


Segment distribution across groups was reviewed for region, device type, traffic source, and plan type. Minor imbalances were noted in North and West regions and Email traffic source. These were noted but not corrected, as they are small enough not to invalidate the overall experiment results.

Missing device type values were handled by creating a cleaned field called `device_type_clean`, where blanks were mapped to `Unknown`.

Missing traffic source values were handled by creating `traffic_source_clean`, where blanks were mapped to `Unknown`.

Missing engagement score values were handled by creating `engagement_score_clean`, where blanks were replaced with the median engagement score.

Missing days to convert values were expected for users who did not convert to paid, so they were excluded from average days-to-convert calculations.

Support ticket count was converted into a binary field called `support_ticket_user`, where users with one or more tickets were marked as 1 and users with no tickets were marked as 0.

Revenue outliers were flagged using the 1.5x IQR rule and reviewed instead of being removed.

Duplicate user IDs and invalid binary values were checked explicitly.



---

## Task 5: Experiment Analysis Approach

The experiment summary is in `outputs/experiment_summary.xlsx`. It compares Control and Treatment across all required metrics using Excel formulas on the `Control_vs_Treatment` sheet.

Metrics calculated: user count, landing page visit rate, trial start rate, onboarding completion rate, paid conversion rate, average revenue per user, average revenue per converted user, refund rate, support ticket rate, average engagement score, and average days to convert.

Segment-level analysis was completed for region, device type, traffic source, and plan type in the `Segment_Analysis` sheet. For binary metrics such as conversion, refund, trial start, and onboarding completion, the average of the 0/1 field was used as the rate.

---

## Task 6 & 7: Hypothesis Test Summary

**Metric tested:** Paid conversion rate

**Null hypothesis:** Treatment paid conversion rate ≤ Control paid conversion rate

**Alternative hypothesis:** Treatment paid conversion rate > Control paid conversion rate

**Test type:** One-tailed two-proportion z-test

**Significance level:** α = 0.05

**Results:**

| Input / Output | Value |
| --- | --- |
| Control converted users | 22 out of 693 (3.2%) |
| Treatment converted users | 50 out of 715 (7.0%) |
| Absolute lift | 3.8 percentage points |
| Relative lift | 120.3% |
| Z-statistic | 3.252 |
| One-tailed p-value | 0.0006 |
| Decision | Reject null hypothesis |

The p-value of 0.0006 is below alpha = 0.05. The treatment shows statistically significant improvement in paid conversion rate. Full test output is in `outputs/experiment_summary.xlsx` on the `Hypothesis Testing` sheet. Screenshot evidence is at `screenshots/hypothesis_test_output.png`.

Full hypothesis framing and interpretation are documented in `analysis/hypothesis_test_notes.md`.

---

## Task 8: Guardrail Metrics Considered

The final recommendation was not based only on paid conversion rate. Six guardrail metrics were evaluated:

| Metric | Control | Treatment | Risk |
| --- | --- | --- | --- |
| Average revenue per user | $51.75 | $53.88 | Acceptable |
| Average revenue per converted user | $1,630.10 | $770.41 | Watch |
| Refund rate | 0.0% | 0.4% | Watch |
| Support ticket rate | 14.7% | 24.8% | Watch |
| Average engagement score | 57.05 | 62.90 | Acceptable |
| Average days to convert | 8.86 days | 6.40 days | Acceptable |

Refund rate was reviewed to check whether the treatment created poor-quality conversions.

Support ticket rate was reviewed to check whether the treatment increased customer support burden.

Average engagement score was reviewed to check whether users exposed to the treatment were meaningfully engaged.

Average days to convert was reviewed to check whether the treatment helped users convert faster or slower.

Revenue metrics were reviewed to check whether conversion gains were supported by healthy revenue quality.


Three metrics are flagged Watch. Support ticket rate increased by 68.2%, revenue per converted user dropped by 52.7%, and refund rate moved from zero to 0.4%. These risks prevent a fully unmonitored broad launch.

---

## Final Recommendation

**Recommendation: Launch the treatment in a phased rollout with guardrail monitoring.**

The paid conversion lift is statistically significant (p = 0.0006) with a 120.3% relative improvement. However, three guardrail metrics — support ticket rate, revenue per converted user, and refund rate — indicate that the quality and cost profile of new conversions needs to be monitored before full scaling.

A phased launch allows the company to capture conversion gains while controlling operational and revenue-quality risk. Priority segments for the initial rollout include the Referral traffic source (highest conversion lift) and North region users (strongest absolute conversion rate under treatment).

Full recommendation details, segment-level insights, risks, and next steps are in `outputs/recommendation_memo.md`.

---

## Assumptions and Limitations

- The dataset is treated as the source of truth for experiment outcomes.
- The experiment assignment is assumed to be random and mutually exclusive.
- The analysis uses 30-day outcomes only. Long-term retention, churn, and lifetime value are not available.
- Missing values in device type, traffic source, and engagement score were handled via cleaned helper fields; missingness may still affect segment-level interpretation.
- Days to convert is only available for users who converted to paid and should not be compared across all users.
- Segment-level results have smaller sample sizes than the overall experiment and should be interpreted with caution.

---

## Screenshots Included

| File | Contents |
| --- | --- |
| `screenshots/summary_metrics.png` | Experiment summary metrics comparison |
| `screenshots/hypothesis_test_output.png` | Hypothesis test inputs, z-statistic, and p-value output |
| `screenshots/kpi_tree_preview.png` | KPI tree preview |
