# Recommendation Memo

## 1. Executive Summary

The treatment increased paid conversion from 3.2% to 7.0%, an absolute lift of 3.8% and a relative lift of 120.3%. The one-tailed two-proportion z-test returned p = 0.0006, which is statistically significant at the 5% level.

However, three guardrail metrics raise concerns: support ticket rate increased by 68.2%, average revenue per converted user dropped by 52.7%, and refund rate increased from 0.0% to 0.4%.

**Final Recommendation: Launch the treatment in a phased rollout with close guardrail monitoring.**

---

## Business Problem

Leadership needs to decide whether the new onboarding and activation campaign should be launched to all users, rejected, tested further, or launched only for selected segments. The decision impacts new users, product onboarding, marketing, customer support and revenue teams.

The main metric that should improve is paid conversion rate. The risks that must be monitored are refund rate, support ticket rate, engagement score, days to convert, revenue quality, and segment-level decline.

Before making a recommendation, the company needs evidence that the treatment improves paid conversion rate and does not create unacceptable negative impact on guardrail metrics.

---

## 2. North Star Metric

The North Star metric is paid conversion rate.

Paid conversion rate was selected because the objective of the campaign is to improve user conversion and early engagement in a way that creates more paying customers.

Supporting metrics such as landing page visit rate, trial start rate, onboarding completion rate, revenue per user, engagement score, refund rate, and support ticket rate explain the result but are not the main success metric. They can improve without producing sustainable paid customers.

Optimizing paid conversion blindly could create low-quality conversions, higher refund rates, increased support demand, or poor revenue per converted user. This is why guardrail metrics must be evaluated before making a launch decision.

---

## 3. KPI Tree Explanation

The KPI tree connects paid conversion rate to three primary drivers: activation depth, funnel progression, and revenue quality.

Activation depth includes landing page visit rate, trial start rate, and onboarding completion rate. These show how far users move through the early product experience.

Funnel progression includes device experience, traffic source quality, and plan type fit. These explain whether the campaign reaches the right users through the right channels on the right devices.

Revenue quality includes average revenue per user, average revenue per converted user, and days to convert. These show whether conversions are financially meaningful and efficient.

Guardrail metrics include refund rate, support ticket rate, average engagement score, and segment-level decline. These protect against conversion gains that come at the cost of customer quality or operational health.

The KPI tree image is saved as `outputs/kpi_tree.png`.

---

## Data Preparation Summary

The dataset was checked for missing values, group counts, duplicate user IDs, invalid binary values, revenue outliers, and segment balance.

8 duplicate user IDs were identified and flagged for deduplication before analysis. No invalid binary values were found in any funnel or outcome column.

Missing device type values (18 rows) were mapped to Unknown in a cleaned field called `device_type_clean`. Missing traffic source values (24 rows) were mapped to Unknown in `traffic_source_clean`. Missing engagement score values (14 rows) were replaced with the median engagement score in `engagement_score_clean` for aggregate analysis. Missing days to convert (1,336 rows) were expected for non-converters and excluded from average days-to-convert calculations.

Support ticket count was converted into a binary field called `support_ticket_user`, where users with one or more tickets were marked as 1. Revenue outliers were flagged using the 1.5x IQR rule and reviewed rather than removed.

---

## 4. Experiment Result Summary

The experiment summary compares Control and Treatment across all required metrics. Results are calculated using formulas in `outputs/experiment_summary.xlsx` on the `Control_vs_Treatment` sheet.

| Metric | Control | Treatment |
| --- | --- | --- |
| User count | 693 | 715 |
| Landing page visit rate | 63.6% | 72.6% |
| Trial start rate | 25.1% | 29.1% |
| Onboarding completion rate | 15.6% | 21.3% |
| Paid conversion rate | 3.2% | 7.0% |
| Average revenue per user | $51.75 | $53.88 |
| Average revenue per converted user | $1,630.10 | $770.41 |
| Refund rate | 0.0% | 0.4% |
| Support ticket rate | 14.7% | 24.8% |
| Average engagement score | 57.05 | 62.90 |
| Average days to convert | 8.86 | 6.40 |

Segment-level analysis was completed for region, device type, traffic source, and plan type in the `Segment_Analysis` sheet.

---

## Hypothesis Setup

**Null hypothesis:** Treatment paid conversion rate is less than or equal to Control paid conversion rate.
H0: Treatment paid conversion rate ≤ Control paid conversion rate

**Alternative hypothesis:** Treatment paid conversion rate is greater than Control paid conversion rate.
H1: Treatment paid conversion rate > Control paid conversion rate

The test is one-tailed because the business question is specifically whether the treatment improves paid conversion, not whether it differs in either direction.

The significance level is 5% (alpha = 0.05).

---

## 5. Hypothesis Test Interpretation

A one-tailed two-proportion z-test was used to compare Control and Treatment paid conversion rates.

- Control: 22 converted out of 693 users (3.2%)
- Treatment: 50 converted out of 715 users (7.0%)
- Absolute lift: 3.8%
- Relative lift: 120.3%
- Z-statistic: 3.252
- One-tailed p-value: 0.0006

The p-value of 0.0006 is below alpha = 0.05, so the null hypothesis is rejected. The treatment shows statistically significant improvement in paid conversion rate. This result is unlikely to be explained by random variation alone.

---

## 6. Guardrail Analysis

The recommendation was not based only on paid conversion rate. Six guardrail metrics were evaluated before making the final decision.

| Metric | Control | Treatment | Absolute delta | Relative change | Risk assessment |
| --- | --- | --- | --- | --- | --- |
| Average revenue per user | $51.75 | $53.88 | +$2.13 | +4.1% | Acceptable |
| Average revenue per converted user | $1,630.10 | $770.41 | −$859.69 | −52.7% | Watch |
| Refund rate | 0.0% | 0.4% | +0.4pp | — | Watch |
| Support ticket rate | 14.7% | 24.8% | +10.1pp | +68.2% | Watch |
| Average engagement score | 57.05 | 62.90 | +5.85 | +10.2% | Acceptable |
| Average days to convert | 8.86 | 6.40 | −2.46 | −27.8% | Acceptable |

Three metrics are marked Watch. Support ticket rate increasing by 68.2% suggests the new onboarding experience may be creating more user confusion or friction post-conversion. Revenue per converted user dropping by 52.7% suggests the additional conversions brought in by the treatment are lower-value customers on average. Refund rate increasing from zero to 0.4% is a small absolute number but directionally negative and worth tracking.

Engagement score improving and days to convert decreasing are positive signs that users exposed to the treatment are more engaged and convert faster. Overall ARPU also improved slightly, which partially offsets the revenue-per-converted-user concern.

---


## 7. Segment-Level Insight

Segment analysis was completed across four dimensions: region, device type, traffic source, and plan type. Every segment showed conversion improvement under Treatment, but the size of the lift, guardrail behaviour, and revenue quality vary meaningfully across segments.

### Region

| Region | Control conversion | Treatment conversion | Lift | Control ARPU | Treatment ARPU | Support ticket rate (Treatment) |
|---|---|---|---|---|---|---|
| North | 3.4% | 8.9% | +5.5pp | $83.67 | $80.97 | 22.8% |
| South | 3.3% | 7.6% | +4.4pp | $76.03 | $47.00 | 22.3% |
| East | 2.5% | 6.4% | +3.8pp | $18.12 | $46.50 | 26.7% |
| West | 3.4% | 5.0% | +1.7pp | $13.68 | $40.78 | 27.4% |

North region shows the highest Treatment conversion rate at 8.9% and the strongest absolute lift at +5.5pp. ARPU remained relatively stable in the North ($83.67 vs $80.97), making it the most attractive region for early rollout. South shows a solid lift but a significant ARPU drop ($76 to $47), suggesting lower-value conversions. East improved both conversion and ARPU, which is a positive signal. West showed the weakest lift (+1.7pp) and the highest support ticket rate (27.4%), making it the lowest-priority region for rollout.


### Device Type

| Device | Control conversion | Treatment conversion | Lift | Control ARPU | Treatment ARPU | Support ticket rate (Treatment) |
|---|---|---|---|---|---|---|
| Desktop | 4.5% | 6.5% | +2.1pp | $84.94 | $40.96 | 23.8% |
| Mobile | 2.6% | 7.3% | +4.8pp | $41.85 | $58.83 | 25.2% |
| Tablet | 1.8% | 7.1% | +5.4pp | $7.31 | $73.33 | 21.4% |
| Unknown | 11.1% | 0.0% | −11.1pp | $61.49 | $0.00 | 44.4% |

Mobile is the standout device segment — it shows a strong conversion lift (+4.8pp) combined with ARPU increasing from $41.85 to $58.83. This is the only device segment where both conversion and ARPU improved simultaneously, making Mobile the highest-confidence segment for rollout. Tablet also shows strong conversion lift and ARPU improvement, but the sample size is small (56 users per group) so results should be interpreted cautiously. Desktop shows a conversion lift but ARPU dropped sharply ($84.94 to $40.96), suggesting lower-value conversions. The Unknown device type segment is a serious concern — Treatment users in this segment had zero conversions compared to 11.1% in Control. This is likely an attribution or data quality issue and must be investigated before any rollout to unidentified device users.


### Traffic Source

| Traffic source | Control conversion | Treatment conversion | Lift | Control ARPU | Treatment ARPU | Support ticket rate (Treatment) |
|---|---|---|---|---|---|---|
| Referral | 2.5% | 11.0% | +8.5pp | $33.31 | $103.00 | 28.6% |
| Paid Search | 1.3% | 6.3% | +5.0pp | $10.84 | $34.78 | 22.2% |
| Email | 2.7% | 7.1% | +4.4pp | $28.72 | $44.98 | 33.9% |
| Organic | 2.0% | 6.2% | +4.2pp | $42.51 | $50.71 | 22.8% |
| Social | 7.7% | 6.0% | −1.6pp | $136.09 | $51.55 | 27.1% |

Referral is the standout traffic source — the highest conversion lift (+8.5pp) combined with the highest Treatment ARPU ($103.00, more than tripling from $33.31). Despite a slightly elevated support ticket rate (28.6%), the revenue quality improvement makes Referral the strongest candidate for priority rollout. Paid Search also shows a meaningful lift with acceptable guardrail behaviour. Email shows solid conversion improvement but the highest support ticket rate among all traffic sources at 33.9%, which warrants investigation before scaling. Social is the only traffic source where Treatment underperformed Control in conversion rate (6.0% vs 7.7%), and ARPU dropped sharply from $136.09 to $51.55. Social users should be excluded from the initial rollout until the drop in conversion and revenue quality is understood.


### Plan Type

| Plan type | Control conversion | Treatment conversion | Lift | Control ARPU | Treatment ARPU | Support ticket rate (Treatment) |
|---|---|---|---|---|---|---|
| Free | 3.0% | 9.2% | +6.2pp | $22.67 | $50.90 | 24.2% |
| Premium | 2.8% | 6.3% | +3.5pp | $53.86 | $100.56 | 26.8% |
| Basic | 3.6% | 3.8% | +0.3pp | $97.80 | $36.29 | 24.7% |

Free plan users show the strongest conversion lift (+6.2pp) and ARPU more than doubled ($22.67 to $50.90). This suggests the new campaign is particularly effective at converting free users into paying customers, which is a core business goal. Premium plan users show both conversion improvement and strong ARPU ($100.56), making them a high-value segment for rollout. Basic plan users showed almost no conversion improvement (+0.3pp) and ARPU dropped significantly from $97.80 to $36.29. The campaign appears to have had little positive effect on Basic plan users and may have attracted lower-value conversions within that group.


### Summary of Priority Segments for Rollout

Based on the combination of conversion lift, ARPU improvement, and guardrail risk, the following priority tiers are recommended:

| Priority | Segment | Reason |
|---|---|---|
| High | Referral traffic, Mobile device, Free plan, North region | Strong lift + improving or stable ARPU + manageable guardrails |
| Medium | Paid Search, Organic traffic, Tablet device, Premium plan, South/East region | Solid lift but ARPU or support rate needs monitoring |
| Low / Hold | Social traffic, Basic plan, West region, Unknown device | Weak or negative lift, ARPU decline, or data quality concern |


---
## 8. Final Recommendation

**Recommendation: Launch the treatment in a phased rollout with guardrail monitoring.**

The paid conversion lift is statistically significant and meaningful in size. A 120.3% relative improvement in conversion directly supports the company's subscription growth objective. The p-value of 0.0006 provides strong statistical confidence in the result.

However, a fully unmonitored broad launch is not recommended because support ticket rate increased by 68.2%, revenue per converted user dropped by 52.7%, and refund rate increased. These signals suggest that while more users are converting, the quality and cost profile of those conversions needs to be understood before scaling fully.

A phased rollout allows the business to capture the conversion gains while closely monitoring support demand, refund behavior, and revenue quality. Priority should be given to segments showing stronger conversion lift with acceptable guardrail behavior. Based on the segment analysis, the Referral traffic source showed the strongest lift (+8.5 percentage points absolute) and is a strong candidate for priority rollout.

---

## 9. Risks and Limitations

- The analysis is based on 30-day experiment data only. Long-term retention, churn, and lifetime value are not available.
- Missing values in device type, traffic source, and engagement score were handled through cleaned helper fields, but missingness may still affect segment-level interpretation.
- Days to convert is only observed for users who converted to paid, so it cannot be compared across all users.
- Segment-level results have smaller sample sizes than the overall experiment and should be interpreted with caution.
- Revenue per converted user dropped significantly, which may reflect plan mix differences rather than true value differences, but this cannot be confirmed from the current dataset alone.

## 10. Next Steps

- Set up a rollout monitoring dashboard tracking refund rate, support ticket rate, ARPU, revenue per converted user, and segment-level conversion weekly.
- Review support ticket reasons for Treatment users to understand what is driving the increase.
- Prioritize Referral traffic and North region users in the initial rollout phase.
- Track longer-term retention and churn once additional data becomes available beyond the 30-day window.
- If guardrail metrics worsen after rollout, reduce rollout scope or pause until root cause is identified.


---

