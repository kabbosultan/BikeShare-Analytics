
# Riding the Demand: Insights for a Bike-Share PM

This repository contains the analysis for the Module 4 Project, focusing on extracting stakeholder-ready insights from the UCI Bike Sharing dataset.

## Business Framing and Stakeholders

As a data analyst on the BikeShare Product team, my role is to analyze hourly bike usage data to provide actionable insights that inform pricing, promotions, staffing, and bike availability decisions. This analysis uses the `hour.csv` file from the UCI Bike Sharing dataset.

The key stakeholders for this project and their primary concerns are:

* **Product Manager (PM)**: Understand when and where demand is strong or fragile, identify user behavior patterns, and determine which hypotheses to prioritize next quarter.
* **Operations Lead**: Identify optimal windows for inventory rebalancing, plan for staffing during demand spikes, and find low-impact windows for fleet maintenance.
* **Marketing Lead**: Determine the best timing (day/hour/season) for promotions and identify user segments (e.g., casual vs. registered) that are most likely to respond.
* **Policy & Ethics Advisor**: Ensure equity of access, avoid decisions that could disadvantage specific user groups, and communicate findings with a responsible understanding of uncertainty.

## Methods Summary

The analysis was conducted in three main parts:

1.  **Exploratory Data Analysis (EDA)**: The `hour.csv` dataset was loaded, cleaned, and processed. Key features like temperature and humidity were de-normalized for better interpretability. Five key visuals were created to identify initial patterns related to hourly, weekly, and seasonal demand, as well as user behavior and weather impacts.

2.  **Hypothesis Testing**: Two formal hypothesis tests were conducted with a significance level of alpha = 0.05.
    * A **Welch's t-test** was used to compare the mean hourly ridership between working days and non-working days.
    * A **one-way ANOVA** was used to compare the mean hourly ridership across the four seasons.

3.  **Simulated A/B Test**: A pre/post analysis was conducted to evaluate a hypothetical feature launch on `2012-09-01` aimed at increasing evening commuter ridership. Data was filtered for the target demographic , and Pre/Post groups were balanced using stratified sampling by weekday and hour. A **Welch's t-test** was then used to compare the mean ridership before and after the launch.

## Top 3 Trends & Insights

1.  **Weekday Demand is Dominated by a Bimodal Commuter Rush**: Working days show two massive, predictable spikes in demand at 8 AM and 5-6 PM, driven almost entirely by registered users. This confirms that commuting is the primary use case for the service's core user base.
<p align="center">
<img width="920" height="705" alt="Screenshot 2025-09-28 at 10 55 16 PM" src="https://github.com/user-attachments/assets/0ff9213e-9354-4220-86e6-870258a8aec0" />
</p>
4.  **Environmental Conditions Dictate Ridership Viability**: Ridership is highest in Fall and Summer and drops significantly in Spring and Winter. Furthermore, adverse weather like rain or snow causes a dramatic decline in usage, making the service unreliable in poor conditions.
<p align="center">
 <img width="849" height="553" alt="Screenshot 2025-09-28 at 10 56 38 PM" src="https://github.com/user-attachments/assets/892e39b4-3da9-4cb2-92b1-6afca78dfaaf" />
</p>

<p align="center">
<img width="1010" height="627" alt="Screenshot 2025-09-28 at 10 57 07 PM" src="https://github.com/user-attachments/assets/dd3b1fe2-101a-4557-89ac-2b059c741f84" />
</p>

5.  **Casual vs. Registered Users are Two Distinct Personas**: Registered users are predictable commuters, while casual users are leisure riders who use the service primarily on afternoons and weekends. These two segments have fundamentally different needs and behaviors that require separate product and marketing strategies.

<p align="center">
<img width="1094" height="593" alt="Screenshot 2025-09-28 at 10 58 17 PM" src="https://github.com/user-attachments/assets/390995f8-2b0e-41e8-b58b-b2d0aafdec4f" />
</p>

<p align="center">
<img width="1004" height="552" alt="Screenshot 2025-09-28 at 10 59 48 PM" src="https://github.com/user-attachments/assets/6bffcd81-bc3e-49bf-a471-7548f5f92dd5" />
</p>

## Hypothesis Testing Results

### Q1: Working vs. Non-Working Day Ridership

* **Test**: Welch's t-test.
* **Result**: The test was statistically significant (p < 0.0001), leading us to reject the null hypothesis.
* **Practical Significance**: Working days averaged **193.21** rides/hour, while non-working days averaged **181.41** rides/hour. This difference of **11.80 rides/hour** is practically significant, as it surpasses a reasonable business threshold (e.g., 10 rides/hour) for altering operational plans. This validates treating these day types as distinct strategic units.

### Q2: Seasonal Ridership Comparison

* **Test**: One-way ANOVA.
* **Result**: The test was statistically significant (F-statistic = 409.18, p < 0.0001), leading us to reject the null hypothesis.
* **Conclusion**: There is strong evidence that mean hourly ridership is not the same across all four seasons.
* **Next Step**: To provide actionable insights, a **Tukey's HSD post-hoc test** is recommended to identify exactly which pairs of seasons (e.g., Summer vs. Fall) have statistically different ridership levels.

### Part C: Simulated A/B Test on App Feature

* **Test**: Welch's t-test.
* **Result**: The test was **not statistically significant** (p = 0.1206), so we fail to reject the null hypothesis. We cannot conclude the feature had a statistically significant impact.
* **Practical Significance**: Despite the statistical result, we observed a large positive increase of **+43.78 rides per hour** in the post-launch period (788.57 vs. 744.78). This is well above a practical threshold of +15 rides/hour.
* **Recommendation**: The result is **promising but inconclusive**, likely due to a small sample size. The recommendation is to **continue the experiment to collect more data**, as the strong positive trend justifies further testing.

## Presentation Slides

[![View Slides](https://img.shields.io/badge/Google-Slides-orange?style=for-the-badge&logo=googleslides&logoColor=white)](https://docs.google.com/presentation/d/1nclAYTitozg5Z0CRpzqnbQRxzXK4ON4zzQZ8AxnxCY0/edit?usp=sharing)

## Ethics & Limitations

* **Observational Data**: This analysis is based on historical, observational data. While we identified strong correlations, we cannot prove causation.
* **A/B Test Simulation**: The A/B test was a simulated pre/post analysis, not a true randomized controlled trial. This makes it susceptible to confounding variables like seasonality or weather.
* **Confounding Variables**: A key limitation in the A/B test was an imperfect balance in weather conditions; the post-launch period had a higher proportion of clear weather days (~89% vs. ~80%), which may have contributed to the observed increase in ridership.
* **Equity of Access**: The EDA revealed that the bike-share service's usability drops dramatically in adverse weather. This presents an ethical consideration regarding service reliability and equity for users who may depend on it for their commute.

## Repository Contents

* `README.md`: This summary file.
* `bike_share_analysis.ipynb`: The Jupyter Notebook containing all Python code for the analysis.
* `hour.csv`: The dataset used for this analysis.
