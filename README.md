# ai201-project3-takemeter

## TakeMeter: Text Classifer

## Community: NBA Reddit 

I chose r/nba because sports discourse on a massive public forum serves as a perfect microcosm of internet culture. The community sits at a unique intersection of heavy data-driven analysis, traditional journalism, corporate entertainment, and raw fan tribalism. As a result, it constantly generates massive volumes of text that vary wildly in tone, intent, and substance on a daily basis.

## Label Taxonomy

1. Analytical / Insight-Driven: Posts or comments focused on statistical breakdowns, film/schematic analysis, salary cap logistics, or historical context. 

Label 1 Examples:

"[Stat] In the 2026 NBA playoffs, opponents shot 52.6% on 16.5 FGA from within 5 feet of the rim when guarded by Victor Wembanyama"

"3 Players in NBA History have averaged 2 Blocks & 2 Steals per Game for an entire Season: Hakeem Olajuwon, David Robinson, and? Gerald Wallace."

2. Narrative / Fan Conjecture: Speculation about NBA team, player legacies, locker room drama, trade rumors, or hypothetical "who is better" matchups. It's coherent discourse, but driven by storylines rather than hard evidence.

Label 2 Examples:

"Wemby Doesn’t Need To Gain Weight. That Defeats The Entire Purpose Of Wemby
What makes him special isn’t strength it’s that he’s a 7’5” player who moves like a wing, covers half the court on defense, and can score from anywhere. The more mass he adds, the greater the risk of losing some of the mobility, fluidity, and defensive range that make him unique in the first place. There is a real chance it’s hurt the very skills that make him a unicorn.He isn’t Giannis or Shaq or Jokic, and he doesn’t need to be."

"Gilbert arenas says to all the people that are saying the San Antonio spurs coach should have benched De'Aaron Fox for Dylan harper in the finals against the Knicks don't know basketball. Fox was their main guy the whole season you bench him in that moment you lose him mentally"

3. Low-Effort / Reactionary: memes, ragebaiting, making fun of, disrespecting, shitposting, circlejerking, "copypasta," or knee-jerk, emotional reactions immediately following a regular season game, playoff game or series. 

Label 3 Examples:

"Michael Jordan 1987 Anti-Drug Public Service Announcement Sponsored By McDonalds."

"Giannis Antetokounmpo Gives Inspirational Speech After Losing 2023 Playoffs: “There is no failure in sports.”

4. News, Media & Fluff: Official team announcements, NBA transactions coming from sources (ESPN insiders), injury reports, and wholesome community/charity events where NBA players, owners, or employees attend it, can be interacting with the fans.

Label 4 Examples:

"Wemby and Champagnie dropping in for a surprise visit at a San Antonio Children's Hospital today."

"[FOS] Madison Square Garden hit with class action lawsuit over apparent data breach after hackers allegedly accessed sensitive visitor data from up to 26 million people collected through James Dolan's controversial surveillance and facial-recognition system used at the Knicks home arena."

## Annotated Dataset

### Data Source
https://www.reddit.com/r/nba/ 

### Labeling Process
I manually entered 200 nba reddit posts into the CSV file, I annotated most of the text through my own judgement and some of the text through AI Assistance. I used Google Gemini and tracked the examples that were pre-labeled by having a note column in the CSV file, I entered "AI Assisted Annotation", indicating that I used a LLM to label this text.

### Data Distribution
| Label | # of Examples | % of Dataset |
| -------- | -------- | -------- |
| Analytical / Insight-Driven  | 31  | 15.5%  |
| Narrative / Fan Conjecture  | 71  | 35.5%  |
| Low Effort / Reactionary  | 24  | 12% |
| News, Media & Fluff | 74 | 37%  |

### 3 Difficult Labeled Examples

```
1. Number of NBA Primetime Games per team
East

Pistons: 24, Celtics: 34, Knicks: 42, Cavaliers: 34, Raptors: 6, Hawks: 16, 76ers: 23, Magic: 22, Hornets: 10, Heat: 11, Bucks: 21, Bulls: 7, Nets: 1, Pacers:4, Wizards: 3

West

Thunder: 38, Spurs: 36, Nuggets: 31, Lakers: 42, Rockets: 33, Timberwolves: 34, Suns: 17, Trail Blazers: 13, Clippers: 28, Warriors: 40, Pelicans: 2, Mavericks: 27, Grizzlies: 10, Kings: 7, Jazz: 3

The Raptors got screwed. How did they get less prime time games than horrible teams like the Bulls and Kings.

How do you guys feel about it?
```
Even though the user includes a data breakdown of primetime schedule numbers across the league, the entire structural intent shifts completely in the second half of the post. Its reactive over analytical: while the text contains numbers, the numbers are just a schedule list used as a visual shield to vent about a perceived injustice against a specific franchise. So I decided this post to be low effort / reactionary instead of analytical / insight-driven.


```
2. Damian Lillard Stats in Game 7 of the 2019 Western Conference Semifinals
13 points on 3-17 shooting (17 % FG) in 45 minutes

This narrative that Lillard was a playoff killer who was only held back by his team just because of some First-Round gamewinners is revisionist history. The Knicks would not have won the championship this year if they swapped out Jalen Brunson for prime Dame 
```
I labeled this post as Low-Effort / Reactionary. At first glance, it looks like a statistical breakdown, but the underlying structure shifts entirely into a classic, emotionally driven hot take. The math is used as an emotional shield: While the post leads with an exact box score stat line (13 points on 3-17 shooting), it only pulls a single, highly isolated bad game from seven years ago to aggressively attack a player's entire career legacy.


```
3. James Dolan is the most insufferable owner in the NBA
```
I labeled this post as narrative / fan conjecture, even though it was a tough decision between that and low effort / reactionary. I decided narrative / fan conjecture because it is a subjective opinion on a team/league figure. If the post said "DOLAN IS A BUM FIRE HIM NOW!!!", that would be Low-Effort / Reactionary due to the emotional outburst formatting, punctuation spikes, and toxic slang.

## Fine Tuning Pipeline

### Model Name
distilbert-base-uncased 

### Training Platform
Google Colab (free T4 GPU)

### Key Training Decision
Key Training Hyperparameter Change
Epoch: how many times the model reads the training data 
I changed the Epoch from 3 to 4 to improve the accuracy. I went with the default parameters and got an low accuracy (49%), I believe the fine tuned model didn't capture the semantic meaning for low effort / reactionary posts. So I increased it and achieved a better accuracy by 11%. I don't want to increase it more to avoid overfitting.

## Baseline Comparision

### System Prompt
```
SYSTEM_PROMPT = """
Classify NBA Reddit posts.

Return exactly one label:

analytical / insight-driven
narrative / fan conjecture
low effort / reactionary
news, media & fluff

Definitions:

analytical / insight-driven:
stats, film analysis, cap analysis, historical context

narrative / fan conjecture:
trade rumors, GOAT debates, locker room stories,
hypotheticals, speculation

low effort / reactionary:
memes, ragebait, insults, reaction posts

news, media & fluff:
injuries, transactions, official announcements,
community appearances

Return ONLY the label."""
```

### How test results were collected
1. The Core Classification Function 
The Request: It sends the text to the llama-3.3-70b-versatile model via the Groq API, using a predefined SYSTEM_PROMPT and a low temperature=0 (to ensure the model's responses are as deterministic and consistent as possible).

The Parsing: It takes the raw string response, converts it to lowercase, and cleans up whitespace.

Substring Matching: To map the model's raw text back to your specific dataset labels (LABEL_MAP), it loops through your valid labels sorted by length in descending order. This is a clever safeguard: it ensures that longer, more specific labels (like "strong_recommendation") are checked before shorter substrings (like "recommendation"), preventing false matches.

Fallback: If the model outputs something unexpected that doesn't match any label, or if the API throws an error, it safely returns None.

2. The Collection Loop
The script iterates through your test dataset to gather the predictions:

Iteration: It loops through the test_df DataFrame using .iterrows(), pulling out the "text" column for each row.

Storage: It calls classify_with_groq(row["text"]) for each row and appends the resulting label (or None) directly into a Python list called baseline_preds.

Rate Limiting: It includes a time.sleep(0.1) delay after every single request. This 100ms pause is there to respect the rate limits of Groq's free tier.

Progress Tracking: Every 10 rows ((i + 1) % 10 == 0), it prints a quick status update to the console so you aren't left wondering if the script froze.

3. Final Aggregation and Quality Check
Once the loop finishes, the script performs a quick sanity check on the collected results

## Evaluation Report and Error Analysis

### Confusion Matrix

### Failure Analysis

Which labels are being confused? 
<!-- Look at the confusion matrix — is there one pair of labels (e.g., analysis → hot_take) that accounts for most of the errors? A directional pattern tells you exactly which boundary the model hasn't learned. -->

Why is that boundary hard? 
<!-- Is it ambiguous language, sarcasm, short posts, or posts where the topic signals one label but the structure signals another? -->

Is this a labeling problem or a prompt/data problem? 
<!-- If you labeled those examples consistently but the model still gets them wrong, the issue is in your training data distribution or the boundary itself. If you find you labeled similar posts differently, the issue is annotation inconsistency. -->

What would need to change to fix it? 
<!-- More examples for the confused class? A tighter label definition? More diverse examples that show the hard case explicitly? -->

### Sample Classifications
<!-- 
a markdown table or list of 3–5 example posts run through your fine-tuned model, each shown with the predicted label and its confidence score, and for at least one correctly-predicted example, a sentence explaining why the prediction is reasonable. Write these out as text (a markdown table or list) — not a screenshot — so they read cleanly in the README.
-->

### Reflection
<!-- 
what your model captured vs. what you intended it to capture. This is distinct from listing wrong predictions — it's a higher-level observation about the gap between your label definitions and what the model's decision boundary actually captures. What did the model overfit to? What did it miss? 
-->

## Spec Reflection
<!--Describe one way the spec helped guide your implementation and one way your implementation diverged from it and why.
-->
One way the spec helped me was in the label test stressing, I could determine the boundaries between a analytical / insight-driven and narrative / fan conjecture label. Analytical / insight-driven and narrative offers hard evidence, even if an opinion or question is asked, narrative / fan conjecture offers an opinion with no or little evidence (soft evidence). One way my implementation diverged from the spec is the dataset distribution, I initially wrote in the spec of having 50 examples for each 4 labels (25 % of total dataset for each label). But the reddit NBA community mostly consists of news, media & fluff and narrative / fan conjecture posts so I had to change my distribution plan. But I made sure that no label takes 70% or more of the total dataset.  

## AI Usage
<!-- 
Describe at least 2 specific instances: what you directed the AI tool to do, what it produced, and what you changed or overrode. If you used any AI assistance during annotation (e.g., asking an LLM to pre-label examples you then reviewed), disclose it here.
-->

**Instance 1** AI Assisted Annotations (Milestone 3)

- *What I gave the AI:*
The label definitions (gave it earlier in the prompt) & reddit posts
Input
```
Knicks fans are making De’Aaron Fox jerseys
```

- *What it produced:*
Told me what label to give the post and the reasoning behind it
Output
low effort / reactonary + reasoning 

- *What I changed or overrode:*
I didn't disagree with the LLM's decision after thinking about it, decided to go with that label.


**Instance 2** API rate errors handling (Milestone 4)

- *What I gave the AI:*
The Base Model in section 5 wasn't parsing
```
I am getting this error from an API call using GROQ, 
10/30 complete...
API error: Error code: 429 - {'error': {'message': 'Rate limit reached for model `llama-3.3-70b-versatile` in organization `org_01kt29mp8kfzar9vybe8mxrkz9` service tier `on_demand` on tokens per day (TPD): Limit 100000, Used 99675, Requested 640. Please try again in 4m32.16s. Need more tokens? Upgrade to Dev Tier today at https://console.groq.com/settings/billing', 'type': 'tokens', 'code': 'rate_limit_exceeded'}}
API error: Error code: 429 - {'error': {'message': 'Rate limit reached for model `llama-3.3-70b-versatile` in organization `org_01kt29mp8kfzar9vybe8mxrkz9` service tier `on_demand` on tokens per day (TPD): Limit 100000, Used 99675, Requested 631. Please try again in 4m24.383999999s. Need more tokens? Upgrade to Dev Tier today at https://console.groq.com/settings/billing', 'type': 'tokens', 'code': 'rate_limit_exceeded'}}
API error: Error code: 429 - {'error': {'message': 'Rate limit reached for model `llama-3.3-70b-versatile` in organization `org_01kt29mp8kfzar9vybe8mxrkz9` service tier `on_demand` on tokens per day (TPD): Limit 100000, Used 99675, Requested 592. Please try again in 3m50.688s. Need more tokens? Upgrade to Dev Tier today at https://console.groq.com/settings/billing', 'type': 'tokens', 'code': 'rate_limit_exceeded'}}
API error: Error code: 429 - {'error': {'message': 'Rate limit reached for model `llama-3.3-70b-versatile` in organization `org_01kt29mp8kfzar9vybe8mxrkz9` service tier `on_demand` on tokens per day (TPD): Limit 100000, Used 99675, Requested 640. Please try again in 4m32.16s. Need more tokens? Upgrade to Dev Tier today at https://console.groq.com/settings/billing', 'type': 'tokens', 'code': 'rate_limit_exceeded'}}
API error: Error code: 429 - {'error': {'message': 'Rate limit reached for model `llama-3.3-70b-versatile` in organization `org_01kt29mp8kfzar9vybe8mxrkz9` service tier `on_demand` on tokens per day (TPD): Limit 100000, Used 99674, Requested 661. Please try again in 4m49.44s. Need more tokens? Upgrade to Dev Tier today at https://console.groq.com/settings/billing', 'type': 'tokens', 'code': 'rate_limit_exceeded'}}
API error: Error code: 429 - {'error': {'message': 'Rate limit reached for model `llama-3.3-70b-versatile` in organization `org_01kt29mp8kfzar9vybe8mxrkz9` service tier `on_demand` on tokens per day (TPD): Limit 100000, Used 99674, Requested 578. Please try again in 3m37.728s. Need more tokens? Upgrade to Dev Tier today at https://console.groq.com/settings/billing', 'type': 'tokens', 'code': 'rate_limit_exceeded'}}
API error: Error code: 429 - {'error': {'message': 'Rate limit reached for model `llama-3.3-70b-versatile` in organization `org_01kt29mp8kfzar9vybe8mxrkz9` service tier `on_demand` on tokens per day (TPD): Limit 100000, Used 99674, Requested 572. Please try again in 3m32.543999999s. Need more tokens? Upgrade to Dev Tier today at https://console.groq.com/settings/billing', 'type': 'tokens', 'code': 'rate_limit_exceeded'}}
API error: Error code: 429 - {'error': {'message': 'Rate limit reached for model `llama-3.3-70b-versatile` in organization `org_01kt29mp8kfzar9vybe8mxrkz9` service tier `on_demand` on tokens per day (TPD): Limit 100000, Used 99674, Requested 589. Please try again in 3m47.232s. Need more tokens? Upgrade to Dev Tier today at https://console.groq.com/settings/billing', 'type': 'tokens', 'code': 'rate_limit_exceeded'}}
API error: Error code: 429 - {'error': {'message': 'Rate limit reached for model `llama-3.3-70b-versatile` in organization `org_01kt29mp8kfzar9vybe8mxrkz9` service tier `on_demand` on tokens per day (TPD): Limit 100000, Used 99674, Requested 619. Please try again in 4m13.152s. Need more tokens? Upgrade to Dev Tier today at https://console.groq.com/settings/billing', 'type': 'tokens', 'code': 'rate_limit_exceeded'}}
API error: Error code: 429 - {'error': {'message': 'Rate limit reached for model `llama-3.3-70b-versatile` in organization `org_01kt29mp8kfzar9vybe8mxrkz9` service tier `on_demand` on tokens per day (TPD): Limit 100000, Used 99673, Requested 608. Please try again in 4m2.784s. Need more tokens? Upgrade to Dev Tier today at https://console.groq.com/settings/billing', 'type': 'tokens', 'code': 'rate_limit_exceeded'}}
  20/30 complete...
API error: Error code: 429 - {'error': {'message': 'Rate limit reached for model `llama-3.3-70b-versatile` in organization `org_01kt29mp8kfzar9vybe8mxrkz9` service tier `on_demand` on tokens per day (TPD): Limit 100000, Used 99673, Requested 569. Please try again in 3m29.088s. Need more tokens? Upgrade to Dev Tier today at https://console.groq.com/settings/billing', 'type': 'tokens', 'code': 'rate_limit_exceeded'}}
API error: Error code: 429 - {'error': {'message': 'Rate limit reached for model `llama-3.3-70b-versatile` in organization `org_01kt29mp8kfzar9vybe8mxrkz9` service tier `on_demand` on tokens per day (TPD): Limit 100000, Used 99673, Requested 779. Please try again in 6m30.527999999s. Need more tokens? Upgrade to Dev Tier today at https://console.groq.com/settings/billing', 'type': 'tokens', 'code': 'rate_limit_exceeded'}}
API error: Error code: 429 - {'error': {'message': 'Rate limit reached for model `llama-3.3-70b-versatile` in organization `org_01kt29mp8kfzar9vybe8mxrkz9` service tier `on_demand` on tokens per day (TPD): Limit 100000, Used 99673, Requested 634. Please try again in 4m25.248s. Need more tokens? Upgrade to Dev Tier today at https://console.groq.com/settings/billing', 'type': 'tokens', 'code': 'rate_limit_exceeded'}}
API error: Error code: 429 - {'error': {'message': 'Rate limit reached for model `llama-3.3-70b-versatile` in organization `org_01kt29mp8kfzar9vybe8mxrkz9` service tier `on_demand` on tokens per day (TPD): Limit 100000, Used 99672, Requested 579. Please try again in 3m36.864s. Need more tokens? Upgrade to Dev Tier today at https://console.groq.com/settings/billing', 'type': 'tokens', 'code': 'rate_limit_exceeded'}}
API error: Error code: 429 - {'error': {'message': 'Rate limit reached for model `llama-3.3-70b-versatile` in organization `org_01kt29mp8kfzar9vybe8mxrkz9` service tier `on_demand` on tokens per day (TPD): Limit 100000, Used 99672, Requested 605. Please try again in 3m59.328s. Need more tokens? Upgrade to Dev Tier today at https://console.groq.com/settings/billing', 'type': 'tokens', 'code': 'rate_limit_exceeded'}}
API error: Error code: 429 - {'error': {'message': 'Rate limit reached for model `llama-3.3-70b-versatile` in organization `org_01kt29mp8kfzar9vybe8mxrkz9` service tier `on_demand` on tokens per day (TPD): Limit 100000, Used 99672, Requested 1082. Please try again in 10m51.456s. Need more tokens? Upgrade to Dev Tier today at https://console.groq.com/settings/billing', 'type': 'tokens', 'code': 'rate_limit_exceeded'}}
API error: Error code: 429 - {'error': {'message': 'Rate limit reached for model `llama-3.3-70b-versatile` in organization `org_01kt29mp8kfzar9vybe8mxrkz9` service tier `on_demand` on tokens per day (TPD): Limit 100000, Used 99672, Requested 579. Please try again in 3m36.864s. Need more tokens? Upgrade to Dev Tier today at https://console.groq.com/settings/billing', 'type': 'tokens', 'code': 'rate_limit_exceeded'}}
API error: Error code: 429 - {'error': {'message': 'Rate limit reached for model `llama-3.3-70b-versatile` in organization `org_01kt29mp8kfzar9vybe8mxrkz9` service tier `on_demand` on tokens per day (TPD): Limit 100000, Used 99672, Requested 650. Please try again in 4m38.208s. Need more tokens? Upgrade to Dev Tier today at https://console.groq.com/settings/billing', 'type': 'tokens', 'code': 'rate_limit_exceeded'}}
API error: Error code: 429 - {'error': {'message': 'Rate limit reached for model `llama-3.3-70b-versatile` in organization `org_01kt29mp8kfzar9vybe8mxrkz9` service tier `on_demand` on tokens per day (TPD): Limit 100000, Used 99671, Requested 696. Please try again in 5m17.088s. Need more tokens? Upgrade to Dev Tier today at https://console.groq.com/settings/billing', 'type': 'tokens', 'code': 'rate_limit_exceeded'}}
API error: Error code: 429 - {'error': {'message': 'Rate limit reached for model `llama-3.3-70b-versatile` in organization `org_01kt29mp8kfzar9vybe8mxrkz9` service tier `on_demand` on tokens per day (TPD): Limit 100000, Used 99671, Requested 566. Please try again in 3m24.768s. Need more tokens? Upgrade to Dev Tier today at https://console.groq.com/settings/billing', 'type': 'tokens', 'code': 'rate_limit_exceeded'}}
  30/30 complete...

⚠️  30 responses could not be parsed.
Review your prompt — the model may not be outputting clean label names.
```
- *What it produced:*
Told me to reduce my token usage by decreasing my token size (characters) in the system prompt. My system prompt was long initially (400-500 tokens).

- *What I changed or overrode:*
I decreased my system prompt character length by removing examples for each label and only providing the label definitions.