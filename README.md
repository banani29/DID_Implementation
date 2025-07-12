# DID_Implementation

Causal Impact of Free Shipping on Revenue: A DiD Case Study

This project explores the causal impact of offering free shipping on user revenue using Difference-in-Differences (DiD) methodology. Building upon earlier analyses using Propensity Score Matching (PSM) and Inverse Propensity Weighting (IPW), we now assess whether the free shipping feature led to sustained revenue uplift—not just increased membership conversions.

Business Problem

Did offering free shipping actually grow revenue from memberships, or just shift fulfillment preference?

A company rolled out free shipping as a perk for paid members. While early analysis showed more users converting, leadership wants to know: Did this feature cause more revenue over time?

Methodology Overview

1. Framing & Context
	•	Treatment: Users who engaged with free shipping after subscribing.
	•	Outcome: Weekly revenue per user.
	•	Objective: Estimate Average Treatment Effect on the Treated (ATT).

2. Data Design
	•	Created a balanced panel of user-week observations (16 weeks: 8 pre, 8 post).
	•	Defined a binary treatment indicator activated post-week-9.
	•	Built a control group using Propensity Score Matching (PSM).

3. Validation of Parallel Trends
	•	Visual inspection: Pre-treatment trends aligned across groups.
	•	Event study regression: Estimated week-by-week treatment effects using fixed effects and time-relative dummies.

4. Model Estimation
	•	Two-Way Fixed Effects (TWFE) DiD regression:
	•	User + Week Fixed Effects
	•	Clustered standard errors by user
	•	Log-transformed revenue to handle skewness.
	•	Treatment effect interpreted multiplicatively.

Result: Estimated DiD coefficient = 0.5686
⇒ Treated users spent ~76.5% more on average post-intervention.

Robustness Checks

✅ Exclude Outliers

Treatment effect held at ~74% after removing top 1% spenders.

✅ Placebo Tests

Injected a fake treatment before the real one — significant effect observed, indicating some sensitivity. Reinforces the need for careful interpretation.

✅ Alternative Controls

Re-ran DiD using users with even IDs as new controls. Coefficient (0.5765) consistent with original → high robustness.

✅ Vary Pre/Post Window

Tested 2-week and 4-week windows. Coefficients (~0.603) were stable → effect not driven by time window choice.

✅ Covariate Sensitivity

Adding session_activity and annual_purchase_value did not change the treatment coefficient. These variables were absorbed by fixed effects → model specification is stable.

Model Diagnostics
	•	Residual Plots: No patterns, indicating a good fit.
	•	Breusch-Pagan Test: Detected heteroskedasticity → justifies clustered errors.
	•	Durbin-Watson Statistic: 2.12 → no significant autocorrelation.

