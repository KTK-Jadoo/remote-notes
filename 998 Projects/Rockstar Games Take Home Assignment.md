# Rockstar Games Take Home Assignment
**Author**: Kartikeya Sharma  
**Date**: 31st October

## Question 1

Adriana is interested in whether our new vehicle is leading to more engagement from our players. If so, she's going to invest more development resources in vehicles for the next update. Your colleague says they performed hypothesis testing on a sample dataset and got a p-value of 0.04. Will you recommend to Adriana that her team invest the additional resources? Is there any additional information you would like before making a decision? 

## Answer
The p-value of 0.04 tells us that there’s a low probability (4%) that the observed engagement increase happened by chance, so it's statistically significant. This is a promising sign. However, before making a final call on allocating more resources, here are a few questions that would help ensure this is the best decision:

1. **How big is the impact?**  
   If we know the effect size, we can see whether this engagement boost is meaningful or just barely noticeable to players. Seeing a change in user numbers: a jump from 5,000 to 10,000 players is huge, but an increase from 5,000 to 5,100 might be less so, even if both were statistically significant.

2. **How much data was this based on?**  
   If this test used many players, even a tiny change might look significant. Knowing the sample size helps us gauge if this change is strong enough to be worth further investment.

3. **How certain is the effect range?**  
   A confidence interval would show us a range where we think the true engagement change lies, giving us a clearer picture of the potential upside. If it’s a small range, we can feel more certain about the benefit to players.

4. **What was engagement like before?**  
   If engagement was already high, a statistically significant bump might not be as impressive as it seems. Having a sense of baseline engagement helps put the change in context.

5. **Cost versus Benefit:**  
   Finally, does the cost of further vehicle development align with the engagement boost we’re seeing? If the change is strong and cost-effective, that would support investing more resources in vehicles.

In summary, while the p-value suggests the new vehicle may indeed be increasing engagement, gathering answers to these questions will ensure that any further development is both statistically and practically meaningful for our players.

---
<div style="page-break-after: always;"></div>
<div style="page-break-after: always;"></div>
<div style="page-break-after: always;"></div>
<div style="page-break-after: always;"></div>
<div style="page-break-after: always;"></div>
<div style="page-break-after: always;"></div>
<div style="page-break-after: always;"></div>
<div style="page-break-after: always;"></div>
<div style="page-break-after: always;"></div>
<div style="page-break-after: always;"></div>
<div style="page-break-after: always;"></div>
<div style="page-break-after: always;"></div>
<div style="page-break-after: always;"></div>
V\
## Question 2a
A stakeholder in the marketing department is building a campaign where the cost per targeted ad is very cheap. They are working on optimizing their spend to capture as many potential converters as possible while not worrying too much about those unlikely to convert when targeted. There are two models to choose from for predicting conversion. Which would you suggest and why? 

- **Model A**: Precision = 0.45, Recall = 0.95  
- **Model B**: Precision = 0.95, Recall = 0.45  

## Answer
In this campaign:

1. **Model A** has:
    - **Precision = 0.45**: Out of all players the model identifies as potential converters, only 45% are truly converters.
    - **Recall = 0.95**: The model captures 95% of all actual converters in the data, maximizing reach to potential converters.

2. **Model B** has:
    - **Precision = 0.95**: Here, 95% of those targeted by the model are actual converters, making it highly accurate in predicting converters.
    - **Recall = 0.45**: However, it only captures 45% of the true converters, missing out on a large portion of potential conversions.

### Recommendation
Given that the marketing department aims to reach as many potential converters as possible and is less concerned about mistakenly targeting non-converters (thanks to the low ad cost), **Model A is the better choice**.

The high recall of Model A (0.95) ensures that nearly all potential converters will be targeted, aligning well with the campaign goal of maximizing reach. Even though Model A has lower precision, meaning it will also target some non-converters, the low cost per ad makes this an acceptable trade-off.

---

## Question 2b
A third model was created and when assessed received the following scores. What is your initial reaction to this model? Why? 

- **Model C**: Precision = 0.95, Recall = 0.99  

### Answer
My initial reaction to Model C is highly positive. With both precision and recall scores being very high (Precision = 0.95, Recall = 0.99), this model appears to be exceptionally well-suited for the campaign’s goals, as it excels in both accuracy and coverage.

---

## Question 3

A new property was added to GTA Online and Dylan wants to know how a player’s buying it is impacting their behavior later, behavior such as their engagement with the game, how they spend their money in the game (guns, clothes, vehicles, other properties, etc.), which missions they play, etc. He can’t actually run an experiment at the moment so instead he has to rely on both older and more recent data already collected from players who bought it and players who didn’t. Assume Dylan has access to a wide variety of player data. What are some examples of player features that would be useful to Dylan? What’s an approach Dylan could use to tackle this question? Feel free to sketch a general method rather than a specific approach.  

## Answer
To investigate the impact of purchasing a new property in *GTA Online* on player behavior, we can utilize an observational analysis approach, given that an experiment cannot be conducted at this time. This study aims to explore how property ownership may affect player engagement, spending habits, and gameplay choices.

### Key Player Features to Analyze
We will examine features that reflect player engagement, in-game spending, and mission preferences. Below are some useful feature examples:

- **Engagement Metrics:**
    - *Session Frequency*: Average number of sessions per week, indicating overall activity.
    - *Session Duration*: Duration of each session, showing player investment.
    - *Daily Active Users (DAU)*: Frequency of activity in the game post-purchase.
    
- **Spending Behavior:**
    - *In-game Purchases*: Total spent on items such as weapons, clothing, vehicles, and properties.
    - *Currency Balance Trends*: Changes in in-game currency balance before and after the property purchase.
    - *Purchase Categories*: Breakdown of spending on utility versus luxury items.
    
- **Mission Preferences:**
    - *Mission Types*: Types of missions played (e.g., combat, heist, races) post-purchase.
    - *Difficulty Selection*: Selection of mission difficulty post-purchase.
    - *Team vs. Solo Play*: Participation in collaborative versus solo missions.
    
- **Ownership of Other Assets:**
    - *Previous Property Ownership*: Whether players previously owned similar assets.
    - *Asset Accumulation Rate*: Frequency of acquiring high-value items post-purchase.
    
- **Progression and Skill Development:**
    - *XP Accumulation Rates*: Rate of experience gain.
    - *Skill Usage Patterns*: Frequency of specific skill use post-purchase.

### Analytical Approach
Due to the observational nature of this study, we’ll adopt a structured analysis to control for potential confounders. Here is the general approach I'm thinking:

1. **Data Segmentation**
    - *Group Players*: Divide players into those who purchased the property and those who didn’t. To control for confounding variables, further segment by progression level or play style.
    - *Pre- and Post-Purchase Windows*: Define "before" and "after" periods for each player who purchased, allowing for comparison.
    
2. **Behavioral Comparison (Pre- vs. Post-Purchase)**
    - Analyze each feature (e.g., spending, mission type) to determine differences before and after purchase.
    - Calculate metrics like the percentage change in session duration or spending patterns to capture behavioral shifts.
    
3. **Matched Samples Analysis**
    - Use *propensity score matching* to create balanced samples of property buyers and non-buyers. This approach helps control for variables like player experience or wealth, making the comparison more reliable.
    
4. **Trend Visualization**
    - Plot time-series trends, particularly around the purchase date, for insights into post-purchase changes.
    
5. **Statistical Testing for Significance**
    - Use statistical tests (e.g., $t$-tests, ANOVA) to assess if behavioral differences between groups are significant.
    - Apply regression analysis to quantify the impact of property ownership on various behaviors, adjusting for confounders.

### Conclusion
This structured approach can help Dylan determine if owning this property correlates with meaningful changes in engagement, spending, and mission types. 