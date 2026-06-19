# Project 3: TakeMeter Specs

## Community: 
<!-- What community did you choose and why? Why is this community a good fit for a classification task — what makes the discourse varied enough to be interesting?]
-->
I chose r/nba (the NBA Reddit community). \

I selected this community because sports discourse on a massive public forum like Reddit serves as a perfect microscopic reflection of internet culture. It sits at a unique intersection of heavy data-driven analysis, journalistic reporting, corporate entertainment, and raw, emotionally charged fan tribalism. This means the community is constantly generating massive volumes of text that vary wildly in tone, intent, and substance on a daily basis.

## Labels: 
<!--What are your 2–4 labels? Define each in a complete sentence. Include 2 example posts per label.
-->
1. Analytical / Insight-Driven: Posts or comments focused on statistical breakdowns, film/schematic analysis, salary cap logistics, or historical context.
Some keywords/signals are: "Points Per Game", "True Shooting %," "PER," "pick-and-roll coverage," "cap space," linking to Basketball-Reference/cleaningtheglass.

Label 1 Examples:

"[Stat] In the 2026 NBA playoffs, opponents shot 52.6% on 16.5 FGA from within 5 feet of the rim when guarded by Victor Wembanyama"

"3 Players in NBA History have averaged 2 Blocks & 2 Steals per Game for an entire Season: Hakeem Olajuwon, David Robinson, and? Gerald Wallace."

2. Narrative / Fan Conjecture: Speculation about NBA team, player legacies, locker room drama, trade rumors, or hypothetical "who is better" matchups. It's coherent discourse, but driven by storylines rather than hard evidence.
Some keywords/signals are: "GOAT debate," "legacy points," "source says," "vibes," "prime vs prime."


Label 2 Examples:

"Wemby Doesn’t Need To Gain Weight. That Defeats The Entire Purpose Of Wemby
What makes him special isn’t strength it’s that he’s a 7’5” player who moves like a wing, covers half the court on defense, and can score from anywhere.

The more mass he adds, the greater the risk of losing some of the mobility, fluidity, and defensive range that make him unique in the first place. There is a real chance it’s hurt the very skills that make him a unicorn.

He isn’t Giannis or Shaq or Jokic, and he doesn’t need to be."

"Gilbert arenas says to all the people that are saying the San Antonio spurs coach should have benched De'Aaron Fox for Dylan harper in the finals against the Knicks don't know basketball. Fox was their main guy the whole season you bench him in that moment you lose him mentally"

3. Low-Effort / Reactionary: memes, ragebaiting, making fun of, disrespecting, shitposting, circlejerking, "copypasta," or knee-jerk emotional reactions immediately following a regular season game, playoff game or series. 
Some keywords/signals are: "Fraud," "washed," "carried," typing in all caps, short insults, or recycling memes, emojis.

Label 3 Examples:

"Michael Jordan 1987 Anti-Drug Public Service Announcement Sponsored By McDonalds."

"Giannis Antetokounmpo Gives Inspirational Speech After Losing 2023 Playoffs: “There is no failure in sports.”

4. News, Media & Fluff: Official team announcements, NBA transactions coming from sources (ESPN insiders), injury reports, and wholesome community/charity events where NBA players, owners, or employees attend it, can be interacting with the fans.

Label 4 Examples:

"Wemby and Champagnie dropping in for a surprise visit at a San Antonio Children's Hospital today."

"[FOS] Madison Square Garden hit with class action lawsuit over apparent data breach after hackers allegedly accessed sensitive visitor data from up to 26 million people collected through James Dolan's controversial surveillance and facial-recognition system used at the Knicks home arena."


## Hard edge cases: 
<!--What type of post will be genuinely ambiguous between two labels? How will you handle it when you encounter it during annotation?
-->
One post/comment can have an opinion and then give stats, it's a challenge to classify it as Narrative/Fan Conjecture or Analytical/Insight-Driven. For example, if one post states Lebron James is the GOAT and says this because he came back down 3-1 in the NBA 2016 FInals. I will handle this by defining a Narrative/Fan Conjecture as offering an opinion with the possibility of offering soft evidence or none at all. In this example, saying coming down 3-1 isn't hard evidence, you have to offer more (stats, advanced analytics) to prove your claim, so this would be labeled as Narrative/Fan Conjecture.

### Hard edge case examples
```
Who do you think is better? Paolo, or Maxey?

Stats in this past regular season:

Paolo: 22/8/5 on 57 TS%

Maxey: 28/4/7 on 59 TS%

Stats in their best individual playoff series:

Paolo:

27/9/4 on 55 TS% vs Cavs (2024)

29/8/4 on 52 TS% vs Celtics (2025)

26/9/6 on 52 TS% vs Pistons (2026)

Maxey:

30/5/7 on 60 TS% vs Knicks (2024)

27/5/7 on 58 TS% vs Celtics (2026)

Who’s the better player? 
```
Narrative offers an opinion with the possibility of soft evidence or none at all. This post does the exact opposite—it offers zero opinion of its own and provides a high volume of structured, hard evidence (advanced analytics) to let the community decide. I intially thought it was Narrative / Fan Conjecture since it was asking for an opinion. 

``` 
Chris Bosh Reflects on Spurs Losing Finals: "Second place, it sucks, you know. You don't want to get all the way to the championship and lose, especially when everybody's watching, when the whole world's watching. It's embarrassing, it's deflating."
```

I knew it was between Narrative / Fan Conjecture & News, Media & Fluff, I couldn't intially decide. Chris Bosh is a former player, not a fan, so I thought it can be news since its coming from a former champion. But News, Media & Fluff is for sources like NBA, ESPN insiders who provide league info through trusted sources. Chris Bosh gave his opinion on a podcast and he is giving his speculation of a team so this a Narrative / Fan Conjecture. You've now looked at quotes from J.R. Smith, Chris Bosh, and Draymond Green. Whenever a post on r/nba consists of a raw, text-only quote from a player reflecting on a past emotional moment, locker room conflict, or career milestone, it will almost always fall into Narrative / Fan Conjecture. They are the "soap opera" elements of the NBA that fans use to debate legacies and team chemistry, completely separate from hard analytics or breaking news headlines.

``` 
 Knicks’ Victory Caps Most Watched NBA Finals Since 1998
https://www.hollywoodreporter.com/tv/tv-news/nba-finals-2026-tv-ratings-best-since-1998-1236622090/

Saturday’s deciding fifth game averaged 24.5 million viewers on ABC and ESPN, the third game in a row to draw more than 20 million. The last time the finals drew 20 million-plus viewers over three consecutive contests was in 2016, for the final three games of the Cleveland Cavaliers’ comeback victory over the Golden State Warriors. The telecast was also the most watched game five since the 1998 NBA Finals, which marked Michael Jordan’s last championship with the Chicago Bulls. 
```

This is a fantastic edge case because the post is packed with numbers (24.5 million, 20 million, 2016, 1998). However, these are business/broadcast metrics, not basketball metrics. They don't break down how a basketball game was played, a team's salary cap logistics, or player performance statistics.

## Data collection plan: 
<!--Where will you collect examples? How many per label? What will you do if a label is underrepresented after 200 examples?
-->
I will manually enter 200 samples from the reddit's NBA page and insert them into the CSV file (4 hours), each label will not represent 70% of the total dataset (diversity) so that a label isn't overrepresented.


| Label | # of Examples | % of Dataset |
| -------- | -------- | -------- |
| Analytical / Insight-Driven  | 31  | 15.5%  |
| Narrative / Fan Conjecture  | 70  | 35%  |
| Low Effort / Reactionary  | 25  | 12.5%  |
| News, Media & Fluff | 72 | 36%  |


## Evaluation metrics: 
<!--Which metrics will you use to evaluate your model and why are those the right ones for this specific task? (Accuracy alone is not enough — explain what else you need and why.)
-->
Rather than overall accuracy, I will consider per class accuracy, precision, recall, $F_1$-Score and confusion matrix. Per class accuracy is less flawed when compared to overall accurracy, especially when the dataset isn't diverse. Precision & Recall are when the model predicts the positive label class, how often is it right and out of all the actual positive label instances, how many did the model manage to find respectively. $F_1$-Score is a decimal value between 0 and 1, indicator of how good and complete are the predicted labels. A confusion matrix is used for classification models. It compares the model's predictions against the actual, true labels in a dataset, visually highlighting where the algorithm is getting "confused" and making mistakes

Precision = True Positive / True Positive + False Positive \
Recall = True Positive / True Positive + False Negative \
$F_1$-Score = 2 * (Precision * Recall / Precision + Recall)

## Definition of success: 
<!--What performance would make this classifier genuinely useful? What would you accept as "good enough" for deployment in a real community tool?
-->
Success for my LLM text classifier means accuracy, no overfitting on training dataset and efficiently assigning labels to where the boundaries are defined and distinguishable. The model needs to handle edge cases well as it relates to Narrative/Fan Conjecture vs Analytical/Insight-Driven (difficult part of project). For a real-world community deployment, I would accept $F_1$-score of 0.78 to 0.82 as "good enough." Internet slang changes fast and sports discourse is inherently messy, attempting for a perfect 0.95+ score on human-generated text is unrealistic.

## Evaluation Plan Review: 
<!-- are your success criteria specific enough that you could objectively determine at the end whether you hit them?
-->

The success criteria is specific enough that I can objectively determine at the end whether I hit them. I am aiming for an 0.8 or above Precision score, 0.7 or above for Recall score, and 0.78 or above for my $F_1$-Score. For per class accuracy for each label, not overall accuracy, I am hoping for 80% or above.

## AI Tool Plan:

### Label stress-testing: 
<!--Give the AI your label definitions and edge case description, and ask it to generate 5–10 posts that sit at the boundary between two labels. If it produces posts you can't classify cleanly, your definitions need tightening — do that now, before you annotate 200 examples.
-->

#### AI Input
[Label definitions pasted above from this file] \
[Edge Case Descriptions pasted above from this file] \
I have given you my labels, edge case to handle. Can you generate 5–10 posts that sit at the boundary between Narrative/Fan Conjecture & Analytical/Insight-Driven labels?

#### AI Output:
Here are 8 boundary posts that deliberately blur the line between Narrative / Fan Conjecture and Analytical / Insight-Driven.

To help you build a bulletproof annotation framework, I’ve included a Verdict and Annotation Logic for each, using your rule: Narrative allows for soft evidence/basic context, while Analytical requires hard data or technical/schematic breakdown to prove a claim.

Post 1: The "Clutch" Legacy Argument
Post Text: "People saying Luka Doncic isn't a clutch playoff performer are ignoring reality. In the 2026 Western Conference Semifinals alone, he shot 8-for-11 (72.7%) in 'clutch time' (final 5 minutes, game within 5 points). He single-handedly saved their season; his legacy as a big-game hunter is completely secure."

Verdict: Analytical / Insight-Driven

Boundary Logic: While the ultimate goal of the post is to defend a narrative ("his legacy is secure"), the user uses a highly specific, officially tracked advanced metric ("clutch time" parameters with exact shooting splits over a specific sample) to prove it. It crosses the line into hard evidence.

Post 2: The Historical Erasure Debate
Post Text: "We need to stop acting like the 2000s Spurs were just a boring defensive team. Go look at their offensive rating from 2003 to 2007—they were consistently top 7 in the league. Duncan's post gravity opened up everything for their shooters. They played beautiful, efficient inside-out basketball, not just slugfests."

Verdict: Narrative / Fan Conjecture

Boundary Logic: This is a classic trap. The post mentions "offensive rating" and "top 7," which feels like data. However, it is fundamentally a historical storyline correction ("they weren't boring, they were beautiful"). Citing a single broad team ranking across a 4-year span qualifies as soft evidence.

Post 3: The System Change vs. Player Drop-off
Post Text: "Tyrese Haliburton hasn't 'washed up' or lost his edge; his production dipped because the Pacers shifted from a 122-pace transition offense to a heavy half-court, spamming high horn sets that force him into isolation. When a passer-first guard loses his transition outlets, his assists drop by 3 per game naturally."

Verdict: Analytical / Insight-Driven

Boundary Logic: Even though there are no heavily cited shooting percentages, this post performs a schematic/film analysis of play types ("high horn sets", "half-court vs transition", "isolation volume"). It diagnoses why a stat changed using basketball mechanics, lifting it out of pure conjecture.

Post 4: The Defensively Biased Award Narrative
Post Text: "The Defensive Player of the Year award has a massive big-man bias. Bam Adebayo switches onto guards 45% of the time—the highest mark in the league—allowing just 0.88 points per possession on those switches. Voters just look at blocks, which favors drop-coverage centers, completely ignoring perimeter versatility."

Verdict: Analytical / Insight-Driven

Boundary Logic: This heavily attacks a storyline (voter bias). However, it uses highly precise tracking data (switching percentages and exact tracking metrics like points per possession) to build its case.

Post 5: The "Empty Calories" Accusation
Post Text: "Trae Young dropping 28 and 10 last night is the definition of empty stats. Atlanta was -14 when he was on the floor because his point-of-attack defense is non-existent. Teams just hunt him in the pick-and-roll until the game gets out of hand. He puts up massive numbers but doesn't impact winning."

Verdict: Narrative / Fan Conjecture

Boundary Logic: It uses box-score numbers (28 and 10, -14), but the fundamental argument is a subjective storyline: "he doesn't impact winning." Single-game plus-minus paired with general observations ("they hunt him") counts as soft evidence used to back up a fan narrative.

Post 6: The Secondary Star Longevity Argument
Post Text: "Khris Middleton is criminally underrated historically. He’s one of only six players in NBA history to average 20+ PPG on 40%+ from three over multiple championship runs. People act like Giannis carried a bunch of role players, but Middleton was an elite, historically efficient secondary closer."

Verdict: Analytical / Insight-Driven

Boundary Logic: This sits right on the knife's edge. It aims to elevate a player's legacy, but it establishes a highly specific historical statistical filter ("1 of only 6 players to average X on Y efficiency during Z runs"). Generating a hard historical threshold moves it into the analytical bucket.

Post 7: The "He Wants Out" Trade Rumor Speculation
Post Text: "Look at the body language and the tracking data. In the last 10 games, Shai Gilgeous-Alexander’s touches per game have dropped from 88 down to 62, and his average speed on offense is down to a crawl. He’s completely checked out of this offense and formatting his way out of Oklahoma City. A trade is coming this summer."

Verdict: Narrative / Fan Conjecture

Boundary Logic: The author throws in tracking data (touches and average speed) to look scientific, but the ultimate conclusion is pure psychological drama/locker room speculation ("body language", "checked out", "forcing his way out"). The hard data is being weaponized to serve a pure storyline.

Post 8: The Contract Valuation Analysis
Post Text: "Giving Jaylen Brown that supermax extension was a catastrophic mistake. He eats up 35% of the Celtics' total salary cap space. Under the new second-apron rules, that contract makes it mathematically impossible to retain their bench depth once the tax penalties hit next season. They ruined their window."

Verdict: Analytical / Insight-Driven

Boundary Logic: The conclusion ("catastrophic mistake", "ruined their window") sounds like an emotional fan take. However, the core of the post is explicitly focused on salary cap logistics and collective bargaining agreement (CBA) rules (35% cap hit, second-apron penalties). This is economic analysis.

Rule of Thumb for Your Annotation Guide:
If you are ever stuck on a post during your actual data labeling phase, ask yourself:

"If I stripped away the user's opinion words (like 'GOAT', 'fraud', 'ruined'), does the remaining text still tell me something concrete about basketball mechanics, finance, or deep history? Or does the text completely evaporate?"

### Annotation assistance: 
<!-- Decide whether you'll use an LLM to pre-label a batch of examples before reviewing them yourself. If yes, note which tool you'll use and how you'll track which examples were pre-labeled (for disclosure in your AI usage section).
-->
I won't use an LLM to pre-label, putting labeled examples directly in the prompt wouldn't make this a fine tuning model, but a few shot learning model (Week 3 lab).


### Failure analysis: 
<!--
Plan to give your list of wrong predictions to an AI tool and ask it to identify patterns before you write up your evaluation. Note what you'll look for and how you'll verify the patterns yourself.
-->
#### AI Input
[Will paste LLM model's wrong predictions] \
My LLM text classifier got these label predictions wrong for these posts/comments, can you identify patterns in thses mistakes, are these directional error patterns?

#### AI Output