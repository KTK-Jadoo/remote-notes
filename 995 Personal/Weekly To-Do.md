

- [8] Rockstar Interview
- [ ] Data 8 review
- [ ] Data 100 review
- [ ] Take Home Assignment review


- [9] COMPSCI 170
- [ ] Final Prep


- [1] DATA 101
- [ ] Final Project
- [ ] Project 3
- [ ] Final Prep


- [5] Leetcode
- [ ] 4 problems everyday



__Intro:__

I’m Kartikeya Sharma,  I’m originally from Agra, India, and I had the unique experience of attending high school in Bosnia and Herzegovina, where I really began to explore my interests in physics and mathematics. Currently, I'm  a data science major at UC Berkeley, where I’ve focused on applying data to real-world problems through projects in machine learning and data engineering.  I’ve had the chance to work on projects ranging from building dynamic pricing models to developing a personalized game recommendation system using NLP, which is something I’m particularly passionate about. 

Professionally, I’ve also had the chance to apply these skills in real-world settings. As a Data Science Intern at BLCK UNICRN, I designed a dynamic pricing model based on user behavior analysis, and as a Data Engineer Intern at Seva Foundation, I developed a PostgreSQL database and automated data pipelines to streamline data processing and several internal tools. These roles deepened my understanding of building scalable solutions and using data to enhance user experience.

I’d describe myself as a curious and driven problem-solver who loves combining creativity with technical skills. I’m always looking for new ways to use data to tell better stories or solve challenging problems. Outside of work, I’m an outgoing geek who loves gaming, which is why I’m particularly excited about this opportunity. 

Contribute to good stories being told.

Not just use the data, but get the data.

**Your Answer Summary:** You noted that a p-value of 0.04 suggests statistical significance (typically, a p-value < 0.05 indicates a low likelihood that the observed result is due to random chance). However, you advised gathering additional information, such as the effect size, sample size, and baseline engagement, before deciding.

  

**Explanation & Theory:**

1. **Understanding the p-value:** A p-value quantifies the probability that the observed data (or something more extreme) would occur under the null hypothesis, which in this case might assume “no effect of the new vehicle on engagement.” A p-value of 0.04 indicates a 4% probability of the result being due to chance, providing evidence against the null hypothesis.

2. **Statistical Significance vs. Practical Significance:** While the p-value tells us the result is statistically significant, it doesn’t tell us the size or impact of the effect. Effect size measures how much the new vehicle influences engagement, while statistical significance only tells us that the effect likely isn’t due to random chance. If the effect size is small, even a statistically significant result might not justify a significant investment.

3. **Sample Size Considerations:** Larger samples can detect smaller effects, so understanding the sample size is essential. With a large sample, even minor increases in engagement could yield statistically significant results. Knowing the sample size helps gauge if the result represents a substantial enough engagement boost.

4. **Confidence Intervals (CIs):** Asking for confidence intervals gives a range for the true engagement increase, providing more context than the p-value alone. A narrow CI suggests more precise estimates, while a wide CI might indicate variability, suggesting caution before investing further.

5. **Baseline Comparison:** Comparing engagement levels before and after the vehicle’s introduction can contextualize the engagement increase. For instance, if engagement was already high, the increase might not be as impactful as if engagement were initially low.

  

**Question 2a**
**Question Prompt:** A stakeholder in marketing is working on a campaign with low-cost ads and aims to reach as many potential converters as possible, prioritizing recall over precision. Two models are available:

• Model A: Precision = 0.45, Recall = 0.95
• Model B: Precision = 0.95, Recall = 0.45

  

**Your Answer Summary:** You recommended Model A because it has high recall (0.95), which aligns with the goal of targeting as many potential converters as possible, even if some non-converters are also targeted.

  

**Explanation & Theory:**

1. **Precision vs. Recall:** Precision measures the accuracy of positive predictions, answering “Of the players targeted as potential converters, how many are actual converters?” Recall measures the coverage of positive instances, asking “Of all potential converters, how many did the model identify?” Here, recall is prioritized due to the low ad cost, meaning it’s acceptable to cast a wide net.

2. **Cost-Benefit of High Recall in Low-Cost Campaigns:** In campaigns where the cost per ad is low, capturing all potential converters is often more important than minimizing false positives. High recall means almost all true converters are identified, aligning with the marketing goal, even though some non-converters are also targeted.

3. **Choosing Model A for High Recall:** By selecting Model A, you ensure that nearly all potential converters are targeted (recall = 0.95), maximizing reach. This choice reflects an understanding of the campaign’s objective to reach a broad audience of potential converters at minimal cost.

  

**Question 2b**
**Question Prompt:** A third model (Model C) has a precision of 0.95 and recall of 0.99. What is your initial reaction?

**Your Answer Summary:** You expressed a positive reaction, noting that the high precision and recall make Model C very effective for the campaign goals.

**Explanation & Theory:**

1. **Balanced Precision and Recall:** Model C’s high scores in both precision (0.95) and recall (0.99) indicate strong performance in accurately identifying converters while minimizing non-converters. This is often ideal in targeted campaigns where each conversion is valuable, as it minimizes wasted effort on non-converters while covering nearly all actual converters.

2. **Model Evaluation Metrics:** Precision and recall balance is often measured by the F1 score, which combines both metrics to provide an overall measure of accuracy. While this wasn’t directly calculated here, high precision and recall would yield an impressive F1 score, indicating Model C’s robust performance.

3. **Best of Both Worlds in Model C:** With high precision and recall, Model C can be deployed effectively in campaigns where both broad coverage and minimal wasted targeting are essential. This model would likely be the optimal choice for a campaign seeking high conversion accuracy without compromising reach.---


**1. Propensity Score Matching (PSM)**

**Definition:** Propensity Score Matching is a statistical technique used in observational studies to create a comparison group that is similar to the treatment group on observed covariates. This approach helps reduce selection bias by matching individuals based on their probability (or “propensity score”) of receiving the treatment, given their characteristics.

  

**Formula for Propensity Score (p):**

For a binary treatment  (e.g., 1 = purchased the property, 0 = did not purchase), the propensity score is calculated as the probability of treatment given a set of covariates :
where  represents characteristics like player experience level, in-game wealth, and playstyle.

Once propensity scores are calculated (often through logistic regression), players in the treatment group (property buyers) are matched with players in the control group (non-buyers) who have similar scores.

  

**Application Example in Rockstar Context:**

If Dylan wants to compare the behaviors of players who bought the new property with those who didn’t, PSM can help ensure that any observed differences in behavior are not due to underlying player characteristics. For example, more experienced players might buy properties at a higher rate, which could skew results unless controlled through matching.
  

**2. Pre- and Post-Purchase Comparative Analysis**

**Definition:** This technique involves comparing specific metrics before and after a treatment (e.g., property purchase) to observe changes in behavior. It works by defining clear “before” and “after” periods and measuring metrics of interest during each.

  

**Formula for Percentage Change in Behavior (Metric):**
For a metric  (e.g., session duration), the percentage change from pre- to post-purchase is calculated as: where  and  are the average values of the metric before and after the purchase.

  

**Application Example in Rockstar Context:**

Dylan could compare **session frequency** before and after purchasing the property to see if engagement increases post-purchase. For instance, if players who bought the property show a significant increase in session frequency or spending on in-game items, this might indicate that the property enhances player engagement.

  

**3. Statistical Testing (e.g., t-tests, ANOVA)**

**Definition:** Statistical tests, like t-tests and ANOVA, help determine whether observed differences between groups are statistically significant. They assess if the means of two or more groups are different enough to conclude that the treatment (e.g., property purchase) likely caused the difference, rather than random chance.

• **t-Test Formula for Two Independent Groups:**

For two groups with means  and , and variances  and , the t-statistic is: where  and  are the sample sizes of the two groups.

• **ANOVA Formula for Multiple Groups:**

ANOVA compares the variances among groups. The F-statistic for ANOVA is:
  

**Application Example in Rockstar Context:**

Dylan can use a t-test to compare the average **in-game spending** of property buyers versus non-buyers. If the t-test shows a significant difference, it suggests that the property purchase correlates with changes in spending behavior. ANOVA could be used if there are multiple groups, such as comparing engagement levels across players with different levels of experience.

  

**4. Time-Series Analysis and Visualization**

**Definition:** Time-series analysis involves examining how data points change over time, often focusing on trends, seasonality, and other patterns. This method is particularly useful in assessing how a treatment affects behavior over both the short and long term.


**Formula for Moving Average (Smoothing):**

A moving average helps smooth out short-term fluctuations in time-series data. For a simple moving average over  time periods:

where  represents the metric at time .


**Application Example in Rockstar Context:**

Dylan can plot the **session duration** of players over time, marking the purchase date to see if there’s a sustained increase in engagement post-purchase. A time-series plot can reveal trends like a sharp increase immediately after purchase or gradual engagement changes over weeks.

  

**5. Regression Analysis for Behavioral Impact Quantification**

**Definition:** Regression analysis models the relationship between a dependent variable (e.g., engagement or spending) and one or more independent variables (e.g., property purchase, player experience level) to quantify the effect of each variable on the outcome.

• **Linear Regression Formula:**

A simple linear regression equation for predicting  based on  is:

where:

• : Dependent variable (e.g., spending behavior post-purchase)

• : Independent variable (e.g., property purchase status)

• : Intercept

• : Coefficient for  (effect size of property purchase)

• : Error term

• **Multiple Regression Formula:**

When there are multiple variables, the model becomes:

  


  

**Application Example in Rockstar Context:**

Dylan can use regression to determine how much of the change in engagement or spending is attributable to property purchase after controlling for variables like **experience level** and **playstyle**. A significant positive coefficient for property ownership would indicate that buying the property positively impacts player engagement, even after adjusting for other factors.

  

**Summary of Techniques for the Analysis**

  

1. **Propensity Score Matching (PSM):** Balances comparison groups by matching based on covariates, reducing bias.

2. **Pre- and Post-Purchase Analysis:** Compares player behaviors before and after purchase, measuring changes in engagement and spending.

3. **Statistical Testing (t-tests, ANOVA):** Determines if differences between groups are statistically significant.

4. **Time-Series Analysis:** Tracks changes in behavior over time, identifying trends related to the property purchase.

5. **Regression Analysis:** Quantifies the impact of property purchase on behavior, controlling for other variables.

  

These techniques equip you to answer Dylan’s question comprehensively by isolating the effects of the property purchase on player behavior, ensuring that observed changes are both statistically and practically meaningful.

---



---


5. **Python (PyTorch, Scikit-Learn, Pandas, Flask, Streamlit):**

• “I’ve used Python extensively across many projects. In my most recent internship at BLCK UNICRN, I built dynamic pricing models using Python, leveraging **Pandas** for data manipulation and **Scikit-Learn** for predictive modeling. During my _Steam-lit_ project, I worked with **PyTorch** to implement BERT for NLP tasks, improving game recommendations by extracting nuanced insights from user reviews. I also built and deployed the final product using **Flask** and **Streamlit**, ensuring a smooth user experience.”



2. **SQL (PostgreSQL, SQLite, SQLAlchemy, Snowflake):**

• “In my internship with the Seva Foundation, I set up a **PostgreSQL** database from scratch, managing large datasets across different regions. I also used **SQLAlchemy** for managing database connections within a Flask web app and **Snowflake** for data warehousing during a project focused on integrating legacy Excel data. These experiences gave me a deep understanding of database design, querying, and optimization.”



3. **Machine Learning (NLP, BERT, LDA, Transformers, PySpark):**

• “My experience with **NLP** has been a key focus, particularly in projects like _Steam-lit_ where I used **BERT** for word embeddings and **LDA** to extract dominant topics from game reviews. I’ve also used **Transformers** to fine-tune models for generating creative content in my _Scribble AI_ project, which won an OpenAI hackathon. Additionally, I’ve explored distributed machine learning using **PySpark** to handle large datasets more efficiently.”



4. **Cloud Computing (AWS, Docker, Apache Kafka):**

• “At the Seva Foundation, I integrated cloud services using **AWS** to manage data pipelines and alert systems. I’ve also worked with **Docker** for containerizing applications, ensuring smooth deployment across environments, and have explored streaming data using **Apache Kafka** to handle real-time data flows.”




5. **Other:**

• “I’ve also worked with **C# in Unity** to explore game development, which helps me understand the technical side of Rockstar’s products better. My experience with **Git/GitHub** for version control is extensive, ensuring collaborative development processes are smooth and error-free.”

Rockstar’s ability to create compelling, open-world narratives that captivate players is something I deeply admire. I want to be part of a team that uses data to drive those experiences, pushing the boundaries of what’s possible in gaming. I see Rockstar as a company that values creativity as much as it values technical innovation, which aligns perfectly with my own aspirations to use data for storytelling.


One of the most technically challenging projects I’ve worked on is _Steam-lit_, a personalized game recommendation system that combines the power of BERT embeddings with Latent Dirichlet Allocation (LDA) topic modeling. The goal was to recommend Steam games based on user input descriptions—basically, building a recommendation system from the ground up.

  

To break it down, I started with data extraction using the Steam Web API, where I retrieved metadata, game descriptions, and user reviews. Next came exploratory data analysis to get a clear picture of our dataset, filtering out non-game items like DLCs and analyzing the distribution of game tags, genres, and reviews.

  

Then, I dove into the NLP techniques: using BERT embeddings to capture the semantic meaning of game descriptions and LDA for topic modeling. This combination created a powerful feature set by capturing both the nuances of language and thematic insights. Finally, I used cosine similarity to match user input with game descriptions, giving accurate recommendations based on user preferences. This project taught me a lot about the synergy of modern NLP techniques and traditional topic modeling, and the system’s accuracy in recommending games has been really rewarding to see.


**How would you describe a project where your initial approach didn’t work, and how did you adapt?**

**Tell me about a time your initial approach didn’t work. How did you pivot?**


**Situation:** In my project “Steam-lit,” I was building a personalized game recommendation system—think of it as a mini-version of Steam’s recommendation engine but built from scratch! My first approach was to use basic word embeddings to analyze reviews and game descriptions, but the recommendations just weren’t hitting the mark. I’d hoped it would capture user preferences, but it was about as accurate as throwing darts blindfolded.

**Task:** My goal was to find a way to make the recommendations meaningful, so users wouldn’t just see “any game,” but the game that felt like it was picked for them.

**Action:** I rethought my whole approach and decided to go all-in on **BERT** embeddings for context-aware recommendations. It was like adding rocket fuel to my model—suddenly, the system was understanding language nuances. I also threw in topic modeling with LDA, so we could capture themes in user reviews. I geeked out hard on this because it felt like the system was finally “getting” what users wanted.

**Result:** The pivot was a game-changer. The model’s accuracy improved significantly, and it was deployed on Streamlit with far better results. I remember watching my system recommend “hidden gems” instead of generic hits and thinking, “Now we’re talking!” It taught me the beauty of iteration, especially in machine learning.


\\\\\ 

“Absolutely! _Steam-lit_ is a perfect example of this. For this project, I combined several technologies and approaches to create an effective game recommendation system. I used:

• **Streamlit** for the user interface, creating an interactive, accessible platform.

• **SQLite** to store and manage the game data retrieved from the Steam API.

• **BERT embeddings** from the Hugging Face Transformers library to capture the semantic meaning of game descriptions in dense vector form.

• **LDA** for topic modeling, which allowed us to extract dominant themes from user reviews and tag each game with these themes.

• Finally, **cosine similarity** served as the core algorithm to compare the user’s input to our comprehensive game embeddings.


Bringing these tools together required careful data processing and matrix combination to build a feature matrix that integrated both topic and semantic layers. This multi-tech approach allowed the recommendation system to capture rich, meaningful connections between user descriptions and game content, making the recommendations genuinely useful.”



**7. Tell me about a time you had a big influence on product strategy or vision.**

**Situation:** At BLCK UNICRN, our team was setting up subscription tiers for the Talent Marketplace, and the initial strategy was simply to mimic competitor pricing. I wanted to take it a step further and create a pricing strategy that actually responded to our users’ unique needs.

**Task:** I wanted to influence the strategy to be user-centric and data-driven, so it wasn’t just about matching competitors but about providing real value to our users.

**Action:** I led an analysis of our user data and found clear patterns in usage and preferences that weren’t reflected in the competitor-based model. I segmented users by behavior and proposed pricing tiers that aligned with the way they engaged with the platform. It felt like building a personalized solution, something I’m really passionate about.

**Result:** The data-driven approach led to a 15% increase in sign-ups and higher retention rates. The team saw the benefits of going beyond standard strategies, and it felt great knowing my input shaped how the product connected with users. It was like finding the sweet spot where data meets real human needs.




**6. Tell me about a time you had to champion something and win people over to your side.**

  
**Situation:** As President of the India Policy and Entrepreneurship Forum (IPEF) at Berkeley, I pitched the idea of hosting a conference on US-India relations. It was a big dream, and understandably, some of the team members were hesitant about the scope and logistics.

**Task:** My job was to show them we could pull it off if we planned strategically and leveraged the right partnerships.

**Action:** I didn’t just push for the idea—I built the blueprint. I presented a detailed plan that included potential speakers, sponsors, and how we’d manage logistics. I even lined up a few big-name speakers to show them we had traction. I figured the best way to convince people was to show them it was doable, not just tell them.

**Result:** Once they saw the potential impact and the solid groundwork, the team got on board. The conference was a huge success, with great feedback from attendees and some serious networking opportunities. It reminded me how powerful it is to inspire confidence by being prepared and passionate.



**5. Tell me about a process improvement you implemented.**


**Situation:** At Seva Foundation, data validation was a daily struggle. We were dealing with mountains of inconsistent data from various sources, and it was all manually checked—a painfully slow and error-prone process.

**Task:** I needed to make data validation faster and more reliable to free up time for deeper analysis.

**Action:** I went into automation mode! I implemented **dbt** to handle data validation and clean up data inconsistencies automatically, and I even added Slack notifications to alert the team when errors popped up. It was like creating my own mini-quality control robot.

**Result:** We cut the validation time by 30%, and our error rates dropped noticeably. I was genuinely thrilled every time I got those Slack notifications because I knew it meant the team was working with clean, reliable data. It was one of those “small changes, big impact” moments.



 **Tell me about a time you had a conflict or disagreement with a coworker. How did you handle it?**

**Situation:** At Seva Foundation, I was working with another intern on a data visualization tool to track surgical metrics. We had different design philosophies—he wanted an all-inclusive tool, and I was pushing for a cleaner, simplified design that focused on key metrics. Think of it like a debate between “more is more” and “less is more.”

**Task:** My task was to find a way to work together so that our tool met user needs without overcomplicating things or alienating my teammate.

**Action:** I’m a big believer in “show, don’t tell,” so I suggested we prototype both versions. We mocked up each approach and presented them to our supervisor, gathering feedback directly from the users. This way, it wasn’t about who was “right” but about which design best served the project’s goals.

**Result:** Our supervisor loved the simplified design, and my coworker saw firsthand why it resonated better with users. He came around, and we moved forward with a unified approach. That experience taught me how important it is to use evidence and empathy to resolve conflicts—ultimately, we both wanted the same thing: a tool that worked.




**Describe a time you had to make an important decision with limited information and time.**


**Situation:** During my internship at Seva Foundation, I got one of those curveballs where they suddenly needed a new PostgreSQL database live in a week. We’re talking about huge datasets from five continents, and I had barely set up the structure, let alone refined it. My brain was in overdrive, and I knew I had to get creative fast.

**Task:** My job was to figure out how to make this database functional enough to launch within a tight deadline, even though we didn’t have all the data requirements.

**Action:** I went straight into what I like to call “core first mode”—focus on essentials, and add bells and whistles later. I built out the foundational structure and optimized workflows for high-priority data, getting buy-in from team members by focusing on what was absolutely necessary for day one. The more complex features had to wait, but I knew we could add them as we gathered more information.

**Result:** We launched the database on time, and I managed to keep it flexible enough for future additions. Seeing it work felt like scoring a win against the clock, and the foundation team was thrilled. The experience taught me that sometimes “done is better than perfect,” especially when you’re racing against the clock!



**Situation:** When I joined BLCK UNICRN, I had one of those “Wait, how do we even start this?” moments. The company’s Talent Marketplace platform was gearing up for a pricing overhaul, and my task was to design a dynamic pricing model that aligned with user preferences. We had tons of data but no clear direction—just “make it work and make it awesome.”

**Task:** My mission was to dig through user data, make sense of what they valued most, and create a pricing model that didn’t just look good on paper but genuinely met user needs.

**Action:** I love data exploration, so I dove deep, slicing and dicing data until I could see clear patterns. Using Python, I segmented users based on behavior and usage, creating a pricing strategy that reflected different user groups. It was like building a map to a place no one had been before, but I loved every minute of it.

**Result:** When the new pricing launched, we saw a 20% bump in retention from our key user segments. Watching those results come in felt like magic—seeing my analysis translate into real-world impact was just so satisfying!