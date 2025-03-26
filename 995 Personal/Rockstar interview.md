
## Tell me about yourself

“I’m Kartikeya Sharma. I was born in India, and I grew up playing Rockstar games—immersing myself in open worlds like GTA that felt alive, unpredictable, and filled with emergent possibilities. Later, I moved to Bosnia and Herzegovina for high school, where I was exposed to a truly international environment that shaped the way I think about systems, interactions, and the **data-driven nature of human behavior**. Now, I’m studying Data Science at UC Berkeley with a focus on Applied Mathematics and Modeling, and what fascinates me most is how **data transforms interactive experiences**.

Over the past few years, I’ve worked on a range of projects and internships—from designing **dynamic pricing models** to developing **machine learning-powered recommendation engines for games**. At **Seva Foundation**, I built and optimized **data pipelines across five continents**, and at **BLCK UNICRN**, I applied statistical modeling to segment and optimize subscription tiers. But what excites me the most is using data to **understand and shape how people engage with digital worlds**—which is why I was drawn to Rockstar’s approach to open-world multiplayer experiences.”


## Tell Me More About Your Experience in Specific Technologies

  

_“Across my work, I’ve developed a strong foundation in_ **_Python, SQL, machine learning, and backend development_**_—skills I’ve applied to projects ranging from_ **_real-time AI-powered motion tracking to predictive modeling for engagement and retention._**_”_

Massimo Fitness Tracker (Deep Learning, Pose Analysis, Flask, SQLAlchemy, Deployment)

  Massimo Fitness Tracker is a  real-time AI-powered gym application that analyzes workout posture using pose estimation and movement tracking. This was a particularly exciting project because it involved real-time interaction analysis, 

• **Situation:** Most fitness apps give generic instructions but don’t provide real-time feedback on posture, which is crucial for avoiding injuries and improving performance.

• **Task:** I wanted to build a system that could track user movements, detect improper form, and offer corrective feedback using AI-powered motion tracking.

• **Action:**

• Implemented **OpenPose and MediaPipe** for **pose estimation** to analyze exercise movements frame-by-frame.

• Built a **Flask API** to process workout data, delivering real-time insights to users.

• Used **SQLAlchemy** to design a **relational database** that tracks user progress over time.

• Deployed the model using **Docker and Heroku**, ensuring **scalability and accessibility**.

• **Impact & Result:**

• Provided **instant feedback** on posture deviations, helping users improve form dynamically.

• Designed a **data-driven recommendation engine** that adapts workouts based on long-term user performance trends.

• _Future Potential:_ The same **real-time motion tracking** concept could be applied in **NPC behavior analysis** or **enhancing interactive multiplayer animations**—something relevant to **Rockstar’s AI-driven character interactions.**

**🟡 Steam-lit (NLP, BERT, Transformers, Flask, Scikit-Learn)**

_“Steam-lit is a_ **_machine learning-powered game recommendation system_** _I built that analyzes_ **_Steam reviews and game metadata_** _to generate personalized suggestions. It was an exciting project because it_ **_used unstructured text data to understand player preferences_**_, similar to how_ **_player sentiment analysis can be applied in live-service games to track engagement trends._**_”_

• **Situation:** _Existing game recommendation engines rely on broad genres, but players often connect with games based on_ **_themes, storytelling, and gameplay depth_**_, which aren’t well captured by traditional recommendation models._

• **Task:** _I wanted to build an_ **_NLP-driven system_** _that recommends games based on_ **_text analysis of player reviews, themes, and mechanics_** _rather than just genre tags._

• **Action:**

• Used **BERT embeddings and LDA topic modeling** to extract thematic insights from thousands of Steam reviews.

• Trained **classification models** to cluster games based on player sentiment and key gameplay elements.

• Built a **Flask API** to serve real-time recommendations, making the system scalable.

• **Impact & Result:**

• **Achieved a 35% improvement** in recommendation relevance compared to genre-based models.

• Demonstrated how **natural language processing can be leveraged to capture nuanced player preferences**, a concept that could be applied to **tracking sentiment and engagement trends in Rockstar’s multiplayer games.**

**🔵 BLCK UNICRN (Predictive Modeling, SQL, A/B Testing, Business Intelligence Analytics)**

  

_“At_ **_BLCK UNICRN_**_, I worked on_ **_predictive modeling for dynamic pricing strategies_**_, helping optimize_ **_subscription tiers based on customer engagement and retention patterns._** _My work directly involved_ **_A/B testing and segmentation analysis_**_, which is essential when experimenting with in-game economy adjustments, such as balancing in-game transactions in a_ **_live-service environment like GTA Online_**_.”_

• **Situation:** _BLCK UNICRN wanted to refine its pricing model by identifying which subscription tiers retained users the longest and which were underperforming._

• **Task:** _I was responsible for building a_ **_data-driven pricing optimization model_** _using historical transaction and engagement data._

• **Action:**

• Conducted **A/B tests** to evaluate different pricing structures and their impact on user churn.

• Built **predictive models using regression and clustering** to segment users based on **retention probability and spending behavior.**

• Queried and analyzed large datasets using **SQL and Snowflake** to generate actionable insights.

• **Impact & Result:**

• **Optimized pricing adjustments** led to a **7% increase in conversion rates and a 12% reduction in churn** across key customer segments.

• Developed a framework for **dynamic pricing experiments**, which could translate well to **in-game economy balancing** in persistent online worlds.

**🟠 Seva Foundation (Data Engineering, SQL, AWS, ETL Pipelines, Large-Scale Analytics)**

  

_“At_ **_Seva Foundation_**_, I worked on_ **_data pipelines that spanned five continents_**_, handling_ **_real-time streaming data_** _for a global training program. This experience gave me a strong foundation in_ **_data architecture and scalable analytics_**_, which is critical when working with_ **_massive multiplayer data in live-service games._**_”_

• **Situation:** _Seva needed a_ **_highly scalable ETL pipeline_** _to process multilingual training data across different regions in real time._

• **Task:** _I was tasked with building a_ **_cloud-based data infrastructure_** _that could efficiently process and store multilingual training datasets._

• **Action:**

• Designed **AWS-based ETL workflows** using **Lambda and Redshift** to automate data processing.

• Implemented **SQL-based query optimization** to improve report generation speed for global training insights.

• Worked on **data quality validation pipelines**, ensuring robust error handling and logging mechanisms.

• **Impact & Result:**

• Reduced **data processing time by 40%**, allowing Seva to scale its global training programs.

• Provided key experience in **large-scale real-time data processing**, applicable to **tracking in-game events and player behaviors in multiplayer environments.**

**Final Thought: How This Helps in the Interview**
## How would you conduct the following data experiment?

  

**Scenario:** _Measuring the impact of a new in-game property feature in GTA Online on player engagement._

**1. Situation & Goal:**
  
_“The goal is to determine whether introducing a new type of in-game property affects player engagement. Specifically, I’d analyze whether_ **_buying a property leads to increased session duration, daily active users (DAU), and in-game spending_**_.”_

**2. Experimental Setup & Data Collection:**

• _“Ideally, we’d conduct an_ **_A/B test_**_, randomly assigning players to a control group (no access to the feature) and a treatment group (with access).”_

• _“If an A/B test isn’t feasible due to player-driven purchases, I’d use an_ **_observational study_**_—analyzing historical engagement trends and controlling for external factors.”_

• _“I’d collect player activity data over a period before and after the feature’s release, ensuring granularity by segmenting data based on experience level (e.g., new players vs. veterans).”_

  

**3. Analysis & Statistical Methods:**

• _“To isolate the feature’s impact, I’d use_ **_propensity score matching_** _to ensure comparable player groups.”_

• _“For validation, I’d apply_ **_hypothesis testing (t-tests, ANOVA)_** _and_ **_regression modeling_** _to quantify the feature’s effect on engagement.”_

  

**4. Impact & Business Decision:**

_“If the feature leads to a significant increase in engagement, it suggests that adding similar high-value properties could be a viable strategy for_ **_sustaining long-term player investment_**_. However, if engagement remains unchanged, we might need to adjust pricing, property perks, or social incentives.”_


• **Confounding Variables:** 
“When analyzing player engagement in multiplayer games, confounding variables can distort relationships between game features and player behavior. To isolate the true impact of a change—whether it’s a new in-game property in GTA Online or an update to an in-game economy—it’s crucial to control for these variables. Here’s how I’d approach it:”

_First, I’d ask:_ **_What external factors could be influencing the results?_**

• Example: _If we’re measuring whether a new property purchase increases playtime, confounders could include:_

• **Player tenure:** Long-time players naturally engage more than new ones.

• **Spending behavior:** Players who buy properties might already be more engaged.

• **Event overlaps:** If a new seasonal event launched around the same time, it could drive up engagement independently of the property feature.

• **Selection Bias:** _“The decision to purchase isn’t random—high-level players may be more likely to buy. I’d use_ **_propensity score matching_** _to ensure we compare similar player cohorts.”_

• **Effect Size vs. Statistical Significance:** _“A statistically significant increase in engagement might not be_ **_meaningfully large_** _enough to justify continued investment in similar features.”_

• **External Factors:** _“Did the feature launch alongside a major update or seasonal event? If so, we need to isolate its true impact by controlling for external variables.”_

**Controlling for Confounders in Experimental Design**

• _The best way to deal with confounding variables is through_ **_proper experiment design._** _Ideally, I’d run an_ **_A/B test_**_, where players are randomly assigned to treatment and control groups. Randomization ensures that confounders are evenly distributed, making the groups statistically comparable._

• _If randomization isn’t possible (e.g., when analyzing naturally occurring player purchases), I’d use statistical techniques to control for confounding factors._

**Statistical Methods to Address Confounding**

**Propensity Score Matching (PSM):** _If randomization isn’t feasible, I’d use PSM to match players with similar behaviors (e.g., engagement history, in-game purchases) across treatment and control groups, ensuring that we compare like-for-like._

Multivariate Regression Models: _By including confounding factors as control variables in a regression model, I can isolate the effect of the feature while adjusting for external influences._


 **Difference-in-Differences (DiD):** _If we have pre-update and post-update data, I’d compare engagement trends in similar player cohorts before and after the feature launch. This helps eliminate time-based confounding factors._

  

Instrumental Variables (IV): if a confounder is affecting both the independent and dependent variable, I’d seek an instrumental variable—a factor related to the treatment but not directly to engagement (e.g., using time-zone variations in player activity as a natural experiment).

Dealing with confounding variables is about carefully structuring analysis to separate correlation from causation. Whether through experimental design, statistical controls, or segmentation techniques, the goal is to_ **_ensure that conclusions drawn from player data reflect real behavioral trends rather than external noise.

## Precision and Recall

• **Precision:** _Measures how many of the positive predictions were actually correct._

• Example: _If we build a model to detect cheating in_ **_GTA Online_**_, precision tells us how many flagged accounts were actually cheaters._

• **Recall:** _Measures how many actual positives were correctly identified._

• Example: _In the same cheating detection system, recall tells us how many total cheaters we successfully caught out of all cheaters present in the game._

  

**High Precision, Low Recall?** We catch fewer cheaters, but every flagged case is **highly accurate** (fewer false bans).

**High Recall, Low Precision?** We flag most cheaters, but risk more **false bans** (potentially harming the player community).

**For Fraud / Cheating Detection:**

_“In cases where false positives have high costs (e.g., banning innocent players), we prioritize_ **_precision_**_—making sure every flagged player is truly a cheater. This means setting stricter thresholds, favoring fewer bans over potential errors.”_


For Player Churn Prediction:

_“If we’re predicting which players might leave the game,_ **_recall_** _is more important—we want to catch as many at-risk players as possible to re-engage them before they churn. Missing a disengaged player means losing revenue and community size.”_

  

✅ **For Game Content Recommendations (e.g., suggesting missions, in-game purchases):**

_“In a recommendation system for_ **_GTA Online_**_, we’d optimize for a balance—favoring_ **_higher recall_** _to ensure players receive diverse suggestions, but tuning for_ **_precision_** _when monetization is involved (so players aren’t spammed with irrelevant offers).”_

**Techniques to Adjust Precision & Recall**

• **Threshold Tuning:** Adjust model confidence scores to trade off between precision and recall depending on the use case.

• **F1 Score Optimization:** Finding the best balance when both metrics matter.

• **Cost-Sensitive Learning:** Assigning penalties to false positives/negatives based on business impact.

• **Human-in-the-Loop Adjustments:** Using **A/B testing** or **player feedback** to refine decisions, especially for flagging systems.


  
## The Allure of Permanence and the “Forever Game"

  

**Introduction: What Makes Games Last?**
If there’s one question that fascinates me in game design, it’s this: _What makes a game last?_ Not just in the sense of how long it takes to beat, but what makes players keep coming back—days, months, even years after release?

  

I’ve always been drawn to the **philosophy behind game design**, how abstract ideas—like permanence, agency, and social dynamics—can be translated into concrete mechanics. Multiplayer games, in particular, intrigue me because they aren’t just systems created by developers; they evolve through the **players themselves**. In an industry where many technical skills are becoming standard, I see my unique strength in **how I think about games**—not just as software, but as **living experiences shaped by data, design, and community.**

  

This is why I want to talk about **forever games**—games designed to **never truly end**. These games capture permanence, offering players a sense of lasting impact while continuously evolving. But how do you design a world that people never want to leave?

**Permanence in Video Games**

  

Permanence is what makes actions feel meaningful. If a decision in a game has **lasting consequences**, it makes players think before they act. In multiplayer spaces, permanence manifests in persistent **player progress** (like leveling up, acquiring in-game wealth) and **shared worlds** where community-driven changes feel real.

  

Take **GTA Online**, for example. When a player builds a criminal empire, **buys a business, invests in property, or customizes a car**, that progress is permanent. The next time they log in, it’s still there. This permanence fuels attachment, making actions feel **worth the time investment**. But games can’t be fully permanent. If every enemy you killed stayed dead, every puzzle you solved stayed solved, the game would eventually run out of things to do. **Designers balance permanence with renewal**—keeping some progress intact while resetting challenges to maintain engagement.

**Game Length: A Confounding Variable**

  

A common misconception in game design is that **longer games are better games**. We often judge a game’s success by its playtime—how many hours it takes to finish or how much content it offers. But in reality, **length can be misleading**. A 100-hour game isn’t necessarily engaging for all 100 hours, and a short, well-crafted experience can be unforgettable.

  

In the context of **forever games**, traditional notions of game length don’t apply. There is no “ending.” The goal isn’t just to fill time but to create systems that **sustain engagement** over months or years. A well-designed forever game doesn’t just add content—it **reconfigures itself**, offering players new reasons to return.

**Designing the “Forever Game”**

  

So, what actually keeps a game alive? I’d argue there are four major factors:

• **Persistent Progress:** Players need to feel like their time investment matters. In **GTA Online**, players build up assets—businesses, vehicles, reputations. This lasting growth keeps them invested.

• **Evolving Content:** The game world **must change over time**. Rockstar has consistently expanded GTA Online with **new heists, vehicles, and properties**—giving players something new to chase even years after launch.

• **Player Impact & Community Influence:** In persistent online spaces, players shape their own stories. GTA Online’s **crew system**, where players build alliances and territories, is an example of how **social structures drive long-term engagement**.

• **Flexible Play Sessions:** A forever game needs to **fit into different lifestyles**. Whether someone has 20 minutes or five hours, they should be able to log in and feel rewarded.

**A Natural Balance (Conclusion)**

  

The key to designing a game that lasts is **balance**. Players need **consequences** for their actions, but they also need **renewal**—something new to strive for. This balance is what keeps forever games alive.

  

At the heart of it, video games tap into something deeply human: the **desire to create, to build, to leave a legacy.** Permanence in games scratches that itch. But at the same time, we crave **freedom to reset, to explore, to keep the adventure going.**

  

The best forever games master this paradox. They let players **make meaningful progress while ensuring there’s always something new ahead.** And as an aspiring game designer and data-driven thinker, that’s what excites me—**figuring out how to craft experiences that players want to return to, not just because they have more content, but because the world itself keeps evolving around them.**

  

As an intern at Rockstar (fingers crossed!), I’d carry these insights forward: always ask why a player would stay with our game, and craft each feature or story beat to earn that precious long-term devotion.



_“I’m fascinated by how_ **_data can shape interactive experiences_**_, particularly in_ **_multiplayer and open-world games_**_. Unlike static software, games are_ **_dynamic ecosystems_**_, where millions of players create_ **_emergent behaviors_**_—and data science allows us to_ **_understand, predict, and enhance those interactions._**_”_


_“For example, in my project_ **_Steam-lit_**_, I built an_ **_NLP-driven game recommendation system_** _by analyzing_ **_Steam user reviews and game metadata_**_. This experience made me realize how_ **_data reveals hidden patterns in player preferences_**_—helping create_ **_personalized, engaging experiences_**_. Similarly, in my work on_ **_dynamic pricing at BLCK UNICRN_**_, I optimized pricing models based on behavioral segmentation—something that directly applies to balancing in-game economies.”_

## Questions

**What are some of the biggest challenges your team is currently working on when it comes to player engagement and retention in Rockstar’s online experiences**

**What do you personally enjoy most about working at Rockstar?**

**Based on our conversation today, is there anything you think I should further develop or focus on to be a strong candidate for this role?**

**Rockstar’s online games thrive on emergent gameplay—players creating their own stories within structured systems. How does the analytics team measure and analyze these unpredictable interactions?**

**What do you think makes someone excel in this role, and what do you personally look for in a great addition to your team?**

