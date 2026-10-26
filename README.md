# TakeMeter

## What This Does

<!-- Your community, and what your classifier sorts posts into. Three or four
     sentences. -->
The classifer classifies posts in the [K-pop Help Subreddit](https://www.reddit.com/r/kpophelp/), a forum for fans to ask questions about the k-pop music genre.

---

## Label Taxonomy

<!-- Each label: a one-sentence definition and two real examples from your
     reading. Then your decision rule for the hardest boundary.

     The decision rule is worth a point on its own and it's the thing most
     people leave out. Every taxonomy has a hardest boundary. Name yours. -->

### `recommendation`

**Definition:**
A question soliciting help for finding similar types of artists, subgenres, fashion, or songs. The request can be related to the music, performance, themes, or specific wardrobe styling.

**Example 1:**
> Songs like Indigo Promise and Teddy Bear by Kim Sejeong? I absolutely love these 2 songs but Sejeong rarely does these types. Songs that sound soft and sultry in the ears, with breathy vocals, kinda indie.

**Example 2:**
> Need birthday song recommendations. Its my birthday soon and i wanted a song to post myself to. Im looking for more mellow songs, so not too upbeat and super happy.

### `advice`

**Definition:**
Question or request for personal help. The fan is seeking personalized help for their situation as a fan, usually related to fan culture, ticketing, merchandising, and purchasing albums.

**Example 1:**
> Where to get Aespa tickets for free or really cheap. I really want to go to Aespas’ concert in London but I’m have no money like I have no allowance and my mum said she isn’t paying for a concert but I really want to go😭😭 I’m actually panicking at the thought that I won’t see them. I’d appreciate any seats. Thank you😭😭🥺

**Example 2:**
> Where to sell or Donate kpop albums? Hi yall! Where can I donate or sell my albums? I have a couple and most don’t have photocards. I think throwing them would be a waste and would want someone or people to have these albums instead.

### The hardest boundary
Questions asking for help on the poster's personal project or fan-fiction is considered advice. They are not asking for similar reccomendations for songs or artists that already exist. Instead, they're asking for help cultivating their own personal fan experience.

**Which two labels:**
> Could some K-pop fans help me test the difficulty of a song guessing game? I’ve been making a small K-pop song guessing game because I really like those “guess the song in 1 second” challenges and I was not able to find one for Kpop, but I’ve reached the point where I’ve heard the songs so many times that I genuinely can’t tell what is easy or difficult anymore 😭 Would anyone here be willing to try a few rounds and help me figure out: Are the songs too obvious or too difficult? Do the song choices feel representative of K-pop?


> Blackpink, Twice, Red Velvet, and Gfriend members as TripleS. I want to make a “how would Blackpink, twice, red velvet, and gfriend sing triples” video because these big 4 3rd gen groups add up to 24, but I don’t know what member to assign to sing



**The decision rule I used every time:**
<!-- e.g. "If the post names a specific checkable fact, it's `analysis`, even
     if the tone is heated." -->
If the post is asking for reccommendations relative to their own personal project use case, then it is seeking advice. If the request for help is related to fan-fiction or fandom imagination, then it is asking for advice -- not a recommendation for real songs they could actually listen to.

---

## The Dataset

<!-- Where you collected from, how you labelled, your counts, and three hard
     cases. -->

**Where the posts came from:**
K-pop Help Subreddit. (https://www.reddit.com/r/kpophelp/)

**How I labelled them:** <!-- Cold first? Pre-labelled with AI and corrected?
Say so plainly — the disclosure is required, not penalised. -->
Cold labelled

I'm stopping at 152 rows because that is all the data I can collect by hand given the deadline. I do not have accesss to the Reddit Developer API, which would make downloading and querying the data faster in the future.

**Counts per label:**

| Label | Count | Share |
|---|---|---|
| recommendation  | 76 | 50% |
| advice | 76 | 50% |
| **Total** | 152 | 100% |

**Three hard cases**

<!-- Any post that made you pause: what it was, which two labels it could have
     been, and what you chose. These are worth more than the easy 190. -->

**1.**
*The post:*
>help me make a kpop playlist for my heartbroken friend !!
Hi guys !! My friend recently got her heartbroken by a guy and she’s been saying that she can’t listen to most of the songs she used to listen to because she relates to much to the lyrics now.
I suggested that she listen to kpop songs cause she wouldn’t understand the lyrics but she’ll still be able to listen to music.
So I’m making a playlist for her with two parts :
hype songs (something like Attention by New Jeans , not something too hype i guess)
krnb (she likes these type of songs)
So if you guys have any song recommendations from any group or solo artists, please lemme know. Oh btw, she’s not a kpop stan so she has untrained ears haha just in case someone pulls out something diabolical

*Could have been:*
advice because they are asking for personal help for their friend

*I chose, because:*
I chose recommendation because the ask is still not about the poster's personal fan experience. The result is still songs with a similar taste profile.

**2.**
*The post:*
> Finding Unreleased tracks
Where do i find unreleased kpop tracks? The most I've found are some seventeen songs on soundcloud (I'm more of a gg stan), or fan made recreated tracks for illit and loona on youtube or soundcloud. I want full official leaks but I can't find anything!

*Could have been:*
recommendation because their request is seeking songs related to an artist.

*I chose, because:*
advice because it is technically related to the logistics of finding content as a fan -- not a recommendation for personalized songs with a similar taste.

**3.**
*The post:*
>Would you consider Likey by TWICE a summer type song or no?
I want to create a playlist with every twice summer song and I’m getting a little stuck with wondering if certain songs are a summer song or not. Likey is one of them, to me it sounds like a summer song but what do u think?

*Could have been:*
Recommendation because the poster needs help on assessing the musical genre or mood.

*I chose, because:*
Advice because it's more related to someone's personal opinion.

---

## The Training Run

<!-- Your starting model, your settings, and anything you changed and why. -->

**Base model:**
distilbert-base-uncased

**Settings:** 

- EPOCHS = 3
- LEARNING_RATE = 2e-5
- BATCH_SIZE = 16
- seed = 42

**Anything I changed from the defaults, and why:**
I didn't change anything from the defaults.

**Split sizes:** <!-- train / val / test, and per-label counts in the test
split. If a label had fewer than about 8 in test, say so — it explains a lot
of next unit's variance. -->

```markdown
train 106  ·  val 23  ·  test 23

                train  val  test
label                           
advice             53   11    12
recommendation     53   12    11
```


---

## How I Used AI

<!-- Two specific moments — what you asked, what came back, what you changed.

     ⚠️ Plus disclosure of any pre-labelling. If you had a model pre-label a
     batch and then read and corrected every one, say that. It's an allowed
     workflow and disclosing it costs you nothing. Not disclosing it is the
     problem. -->

**Moment 1**

- *What I asked for:*
  - Help writing a Python script to scrape 5 posts from the subreddit.
- *What came back:*
  - A suggested script using the .json endpoint.
- *What I changed:*
  - I did not end up using the draft scraping script because it is blocked by Reddit with a 403 error and this type of unathenticated access is blocked. 
 
**Moment 2**

- *What I asked for:*
  - I asked for help labelling the hardest boundary posts mentioned above.
- *What came back:*
  - Unhelpful suggestion to add another category.
- *What I changed:*
  - Nothing, ignored the suggestion because I need to stay in scope for the current project. 

**Pre-labelling disclosure:**
The K-pop subreddit has flairs or tags, such as "recommendation", "explain", and "advice". I used the flair as a rough proxy for posts that fit the label but verified that the definition stated for this project still applies.

<!-- ═══════════════════════ UNIT 6 — THE TEST ═══════════════════════

     Don't fill these in during unit 5.
     ═══════════════════════════════════════════════════════════════════ -->

---

## Baseline vs. Trained

<!-- Both models on the same posts. `python baseline.py --trained results.json`
     prints this table for you. -->

| Measure | Baseline | Trained | Difference |
|---|---|---|---|
| Overall accuracy | 0.696 | 0.783 | +0.087 |
| Macro F1 | 0.673 | 0.776 | +0.102 |
| F1 — `advice` | 0.588 | 0.737 | +0.149 |
| F1 — `recommendation` | 0.759 | 0.815 | +0.056 |

**What I predicted before I looked:**
<!-- Milestone 1 asks you to write this BEFORE seeing the trained numbers. A
     prediction made afterwards isn't one. -->
I think the trained model will beat the baseline because in general BERT is better at deep understanding of context and named entity recognition problems. That's closer to our objective here, which is classifying labels from text on the specific topic of K-pop fans. Meanwhile, the baseline BART is better at tasks that create output, like translation and summarizing.

**What the gap actually means:**
<!-- If the baseline matched your trained model, your fine-tuning added
     nothing — and that is a real finding, not a failure. Say it plainly. -->
It's possible the gap could stem from my poorly written definition of the class labels in `label_definitions.txt`.


---

## Run Log — Before

<!-- Five criteria across three seeds. The notebook's section 6 prints the
     spread table; the Target and Verdict columns are yours. -->
| Measure | Seed 42 | Seed 7 | Seed 2024 | Spread |
|---|---|---|---|---|
| Overall accuracy | 0.783 | 0.870 | 0.870 | 0.087 |
| Macro F1 | 0.776 | 0.865 | 0.869 | 0.093 |
| F1 — `advice` | 0.737 | 0.842 | 0.857 | 0.120 |
| F1 — `recommendation` | 0.815 | 0.889 | 0.880 | 0.074 |

| Criterion | Target | Seed 42 | Seed 7 | Seed 2024 | Verdict |
|---|---|---|---|---|---|
| 1. Overall accuracy | >=0.70 | 0.783 | 0.870 | 0.870 | MET |
| 2. Per label distribution | <=0.60 | no metric | no metric | no metric | MISSED |
| 3. Recall on held-out set | >=0.65 | `advice`: 0.583, `recommendation`:1.0 | `advice`:0.727, `recommendation`:1.0 | `advice`: 0.75, `recommendation`:1.0 | MISSED  |
| 4. Diff(precision - recall) per label| <=0.15 | `advice:`0.417, `recommendation`:0.313 | `advice:`0.272, `recommendation`:0.200 | `advice:`0.25, `recommendation`:0.214 | MISSED |
| 5. F1 on held-out set | >=0.60| `advice`:0.737, `recommendation:`0.815 | `advice`:0.842, `recommendation`:0.889 | `advice`:0.857, `recommnedation`:0.88 | MET |

### Confusion matrix

<!-- ⚠️ TYPED AS A MARKDOWN TABLE. The notebook prints one ready to paste.
     An image of a matrix earns nothing. -->

| true \ predicted | advice | recommendation |
|---|---|---|
| **advice** | 7 | 5 |
| **recommendation** | 0 | 11 |

**My biggest off-diagonal number, and what it means:**
<!-- Not "the model made mistakes" — WHICH boundary it didn't learn, and which
     direction. "7 real analysis posts were called hot_take and only 3 went the
     other way" is a direction, not just an error rate. -->
Biggest confusion: 5 real `advice` posts called `recommendation`.

The other direction: 0 real `recommendation` posts called `advice`.

That's lopsided — the model leans toward `recommendation` on this pair. A direction like that usually points at your labelling rather than the model.


---

## Verdicts and Diagnoses

<!-- MET or MISSED against LAST UNIT's target. The target has to hold across
     all three seeds, not turn up sometimes. -->

| # | Criterion | Target | Verdict | How I decided |
|---|---|---|---|---|
| 1 | Overall accuracy is at least 0.70. | 3/3 | MET | Check overall accuracy output |
| 2 | No label makes up more than 60% of the data.  | 0/3 | MISSED  | Criterion could not be measured. Unable to evaluate because we do not have per label count metric after each seed run.|
| 3 | Both labels have recall of at least 0.65 on the held-out set, on every seed. | 2/3 | MISSED | `recall`is not high enough in seed 42 run. |
| 4 | For each label, precision and recall differ by no more than 0.15. | 0/3 | MISSED | Calculated metric in Appendix section of `takemeter.ipynb` and differences were all greater than 0.15. |
| 5 | Every label has an F1 of at least 0.60 on the held-out set. | 3/3 | MET | Check labels `advice` and `recommendation` F1 scores.  |

**Diagnoses**

<!-- For each miss: the cause, and how you know. The four common causes are:
     too few examples for a label, a boundary you applied inconsistently, a
     genuinely hard label pair, and a task the model can't reach from this
     much data.

     ⚠️ Use your agreement report as evidence. It is the only instrument you
     have that can tell a LABELLING problem from a MODEL problem, and this
     section is graded on whether you used it that way. -->

*Missed Criteria 2*
I'm unable to meet second criteria because it can not be measured. I didn't save per label counts after each seed run. The data on the distribution of each label in the corpus is already lost after each seed run. In retrospect, it's not a good criteria for evaluating the performance of the model.

Instead, I changed criteria #2 to a metric that we have measured. Overall F1 macro is at least 0.75. Macro F1 computes an F1 score for each class one-versus-rest and averages them with equal weight. Since this is a binary classification problem without class imbalance, the F1 macro score can measure a global "pulse" of how well the model is balancing precision and recall overall.

*Missed Criteria 3*
The recall for advice was below the 0.65 criteria on seed 42 run. This may stem from my labeling, not the model — I applied the boundary two different ways in the training data.

*Missed Criteria 4*
Criteria 4 (For each label, precision and recall differ by no more than 0.15) was missed. The confusion matrix shows most misses going to `recommendation.` 5 real `advice` posts were labelled `recommendation` while 0 real `recommendation` posts predicted as `advice`. I think the miss may be attributed to several reasons. First, there may be disagreement among labelling and inconsistency with how I applied the boundary rules to the training data. This could stem from the label definition not being clear enough.



<!-- "reaction has an F1 of 0.41 across all three seeds. My matrix shows most misses going to hot_take. My agreement check found 4 of my 6 disagreements on exactly that pair. So this is my labeling, not the model — I applied the boundary two different ways in the training data." -->

---

## Agreement Report

<!-- Your rate against the staff set, and every disagreement adjudicated.

     Remember you labelled these 30 under the STAFF taxonomy in
     data/staff_taxonomy.md, not your own — so every argument below is made
     from those definitions and those decision rules. -->

**Agreement rate:** 30 / 30 = 100%

<!-- Nobody grades this number. A 60% who argues every disagreement from the
     stated rules beats a 95% who wrote "staff was right" nine times. Several
     of the 30 were chosen because they're genuinely ambiguous — you should be
     winning some of these. -->

**Disagreements**
There were no disagreements. The labels were easier to evaluate compared to my k-pop project data because the definition and boundary examples were very well written.

**What the pattern in my disagreements tells me:**
My lack of diasgreements tells me that I'm consistently following the rules while labelling. And the rules are clearly written.

---

## The Improvement

**What I changed:**
Add examples to the thinnest label. I added 20 posts to the `advice` label, which had the worst F1 score.

**Which diagnosis pointed at it:**

While 5 real advice posts were called recommendation, 0 real recommendation posts called advice. That's lopsided — the model leans toward recommendation on this pair. A direction like that usually points at my labelling rather than the model.

<!--152 labels overall is insufficient after the data is split. We get 12 `recommendation` posts and 11 `advice` in the validation set. The extra post could bias answers towards `reccomendation` also.-->


### Run Log — After
| Criterion | Target | Seed 42 | Seed 7 | Seed 2024 | Verdict |
|---|---|---|---|---|---|
| 1. Overall accuracy | >=0.70 | 0.885 | 0.769 | 0.769 | MET |
| 2. F1 macro | >=0.75 | 0.876 | 0.729 | 0.768 | MISSED |
| 3. Recall on held-out set | >=0.65 | `advice`: 1.0, `recommendation`:0.727 | `advice`:0.714, `recommendation`:0.455 | `advice`: 0.733, `recommendation`:0.818 | MISSED  |
| 4. Diff(precision - recall) per label| <=0.15 | `advice:`0.167, `recommendation`:0.273 | `advice:`0.286, `recommendation`:0.545 | `advice:`0.113, `recommendation`:0.126 | MISSED |
| 5. F1 on held-out set | >=0.60| `advice`:0.909, `recommendation:`0.842 | `advice`:0.833, `recommendation`:0.625 | `advice`:0.786, `recommnedation`:0.75 | MET |

**Did it help, and how do I know:**

<!-- If it didn't, say so. Relabelling that didn't help is a genuinely
     interesting result and earns full credit. -->
Adding additional advice labels did not help. I know this because 3 criterion failed in both the before and after runs.


---

## What's Still Broken

<!-- For each criterion still missed: what you'd do, and why you stopped. -->
For criterion 3, I would add additional `recommendation` labels to balance out the class imbalance I introduced in the "after" run. I stopped because I didn't have enough time.

For criterion 4 and 5, I would also add more labels overall. I think the 200 mark would be more sufficient information to split across train, evaluate, and test. I stopped because I didn't have enough time for the project deadline.


**The gap between what I meant my labels to capture and what the model
learned:**
<!-- Two sentences. Your confusion matrix is the evidence. -->
| true \ predicted | advice | recommendation |
|---|---|---|
| **advice** | 15 | 0 |
| **recommendation** | 3 | 8 |

Biggest confusion: 3 real `recommendation` posts called `advice`.
The other direction: 0 real `advice` posts called `recommendation`.

That's lopsided — the model leans toward `advice` on this pair. A direction like that usually points at my labelling rather than the model.

## Sources

- https://rushdishams.blogspot.com/2011/08/micro-and-macro-average-of-precision.html
- https://datascience.stackexchange.com/questions/15989/micro-average-vs-macro-average-performance-in-a-multiclass-classification-setting


<!-- ═════════════════════════════════════════════════════════════════════

     SUBMISSION CHECKLIST — unit 5

       [ ] criteria.md has five numbered criteria, each naming a NUMBER
       [ ] Each has a reason underneath tied to your data or taxonomy
       [ ] labels.csv: at least 150 rows, text/label/note, ONE file not split
       [ ] No label above 70%
       [ ] All five unit 5 sections have real content
       [ ] Label Taxonomy includes the decision rule for your hardest boundary
       [ ] The Dataset includes three hard cases
       [ ] results.json and test_split.csv committed (the notebook does this)
       [ ] At least four new commits
       [ ] Repository URL submitted — WRITE IT DOWN

     SUBMISSION CHECKLIST — unit 6

       [ ] Baseline vs. Trained table, with your prediction written beforehand
       [ ] Run Log — Before, five criteria across three seeds
       [ ] Confusion matrix TYPED AS A MARKDOWN TABLE
       [ ] A verdict on every criterion
       [ ] A diagnosis for every miss, using the agreement report as evidence
       [ ] Agreement Report with every disagreement adjudicated
       [ ] One improvement, with Run Log — After
       [ ] What's Still Broken
       [ ] results_three_seeds_before.json, results_three_seeds_after.json,
           baseline_results.json and
           agreement_results.json committed
       [ ] At least four new commits
       [ ] The SAME repository URL as last unit

     Do not delete and recreate this repository.
     ═════════════════════════════════════════════════════════════════════ -->

---

📖 **How to run this project: [RUNNING.md](RUNNING.md)**
