# A/B testing for ux design

# Problem Statement:

In today's fast-paced digital landscape, businesses are constantly looking for ways to optimize their online presence, improve user engagement, and drive conversions. However, making data-driven decisions about website design, user experience, and marketing strategies can be challenging.

Many businesses struggle to determine which design elements, messaging, or calls-to-action (CTAs) resonate best with their target audience. Without a clear understanding of what drives user behavior, businesses risk making costly design and marketing decisions that may not yield the desired results.

A/B testing (also known as split testing) offers a solution to this problem. By randomly assigning users to different versions of a website, email, or app, businesses can compare the performance of different design elements, messaging, or CTAs. This enables data-driven decision-making, reduces the risk of costly mistakes, and helps businesses optimize their online presence for maximum impact.

## **Project Overview**  

This project demonstrates how to conduct an A/B test for UI design using a synthetic dataset. The goal is to determine which design variation leads to a higher **Click-Through Rate (CTR)**, helping businesses make data-driven UX decisions. In a real-world A/B test, we don't generate data immediately. Before running the test and collecting data, there are key preparatory steps to ensure the test is statistically valid and meaningful.

 **1. Define the Objective**  
Goal: Determine which UI design leads to a higher Click-Through Rate (CTR). 

**2. Select the Test Variable**  
UI Element: Call-to-Action (CTA) Button Design
Test Variants:
            Variant A (Control): Blue button with "Sign Up Now"
            Variant B (Test): Green button with "Get Started" 
    
**3. Identify the Target Audience**  
-User Segment: New visitors to a product landing page.
Traffic Source: Organic and paid traffic from search engines and social media.
Device Type: Mobile and desktop users.
User Assignment: Randomized 50/50 split:
                 50% of users see Variant A (Blue button, "Sign Up Now").
                 50% of users see Variant B (Green button, "Get Started").

**4. Determine Sample Size & Duration**  
Before running an A/B test, we need to know how many users should be included in each group (Variant A vs. Variant B) to get reliable results. If the sample size is too small, the results may be inaccurate. If it's too large, we may be wasting resources. To determine the right sample size, we consider four key factors:
1. Baseline Conversion Rate (CTR) – it tells us how things currently perform.This is the current Click-Through Rate (CTR) before making any changes. It tells us how many people, on average, click the button in the original design. For example, If 5 out of 100 people who visit the page click the button, the CTR is 5% (0.05). It gives us a starting point to compare the new design against. If we don’t know the baseline, we can estimate it based on past data or run a small test first.

2. Minimum Detectable Effect (MDE) – What change is worth noticing?. If our current CTR is 5%, and we want to detect at least a 1% increase, our MDE is 1% (0.01). So, we are testing to see if the new design gets 6% CTR or higher. If we set the MDE too small, we will need a very large sample size.

3. Significance Level (α) – How much error are we okay with. This is the chance of a false positive—seeing a difference when none exists.It is usually set at 5% (0.05). Meaning we are 95% confident that the results are real and not due to randomness. If α is too high, we might think the new design is better when it’s actually not. And if α is too low, we may miss real improvements.

4. Statistical Power (1 - β) – How confident are we in detecting a real difference?. statistial power is the ability to to detect a true difference if it exists. It is commonly set at 80% (0.8). This means if the new design actually performs better, there is an 80% chance we will detect it. If power is too low, we might miss improvements that actually exist. And increasing power requires more users in the test

To calculate the required sample size per group for an A/B test in Python, you can use the statsmodels library, which has a built-in function for power analysis.

from statsmodels.stats.power import NormalIndPower
from statsmodels.stats.proportion import proportion_effectsize

# Given parameters
baseline_ctr = 0.05  # 5% baseline conversion rate
mde = 0.01           # Minimum detectable effect (1% increase)
alpha = 0.05         # Significance level (5%)
power = 0.8          # Statistical power (80%)

# Compute effect size (Cohen's h)
effect_size = proportion_effectsize(baseline_ctr, baseline_ctr + mde)

# Calculate required sample size per group
sample_size = NormalIndPower().solve_power(effect_size, power=power, alpha=alpha, ratio=1)

print(f"Required sample size per group: {round(sample_size)}")
print(f"Total required sample size (both groups): {round(sample_size) * 2}")

**Output**
Required sample size per group: 3902
Total required sample size (both groups): 7804

**Determine Duration**
Once we have determined the sample size, the next step is to calculate how long the test should run. The test duration depends on: The number of users needed per variant (from sample size calculation), Average daily traffic (The number of visitors expected per day) and Traffic split that is the percentage of traffic assigned to each variant (e.g., 50/50 split). Given the sample size calculated sample size (7804), lets assume the daily traffic to be 2000, and the traffic split 50/50 using python the test duration is calculated thus:

# Given values
sample_size_per_group = 3902  # Sample size per group
total_sample_size = sample_size_per_group * 2  # Both groups (A & B)
daily_traffic = 2000  # Daily visitors
traffic_split = 0.5  # 50% traffic per variant

# Calculate test duration
test_duration = total_sample_size / (daily_traffic * traffic_split)
test_duration = round(test_duration)  # Round up to full days

print(f"Estimated test duration: {test_duration} days")

**output**
Estimated test duration: 8 days

## *5 Define the Hypothesis

## *6. Implement the Test*  
Deploy both versions (A and B) while ensuring proper tracking.  Monitor for technical issues or unintended biases during the test.  

Once these steps are completed, the experiment can run, and data can be collected for analysis.








