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
- *What came back:*
- *What I changed:*

**Pre-labelling disclosure:**

<!-- ═══════════════════════ UNIT 6 — THE TEST ═══════════════════════

     Don't fill these in during unit 5.
     ═══════════════════════════════════════════════════════════════════ -->

---

## Baseline vs. Trained

<!-- Both models on the same posts. `python baseline.py --trained results.json`
     prints this table for you. -->

| Measure | Baseline | Trained | Difference |
|---|---|---|---|
| Overall accuracy |  |  |  |
| Macro F1 |  |  |  |
| F1 — `label_one` |  |  |  |
| F1 — `label_two` |  |  |  |

**What I predicted before I looked:**
<!-- Milestone 1 asks you to write this BEFORE seeing the trained numbers. A
     prediction made afterwards isn't one. -->

**What the gap actually means:**
<!-- If the baseline matched your trained model, your fine-tuning added
     nothing — and that is a real finding, not a failure. Say it plainly. -->



---

## Run Log — Before

<!-- Five criteria across three seeds. The notebook's section 6 prints the
     spread table; the Target and Verdict columns are yours. -->

| Criterion | Target | Seed 42 | Seed 7 | Seed 2024 | Verdict |
|---|---|---|---|---|---|
| 1.  |  |  |  |  |  |
| 2.  |  |  |  |  |  |
| 3.  |  |  |  |  |  |
| 4.  |  |  |  |  |  |
| 5.  |  |  |  |  |  |

### Confusion matrix

<!-- ⚠️ TYPED AS A MARKDOWN TABLE. The notebook prints one ready to paste.
     An image of a matrix earns nothing. -->

| true \ predicted |  |  |  |
|---|---|---|---|
| **** |  |  |  |
| **** |  |  |  |
| **** |  |  |  |

**My biggest off-diagonal number, and what it means:**
<!-- Not "the model made mistakes" — WHICH boundary it didn't learn, and which
     direction. "7 real analysis posts were called hot_take and only 3 went the
     other way" is a direction, not just an error rate. -->



---

## Verdicts and Diagnoses

<!-- MET or MISSED against LAST UNIT's target. The target has to hold across
     all three seeds, not turn up sometimes. -->

| # | Criterion | Target | Verdict | How I decided |
|---|---|---|---|---|
| 1 |  |  |  |  |
| 2 |  |  |  |  |
| 3 |  |  |  |  |
| 4 |  |  |  |  |
| 5 |  |  |  |  |

**Diagnoses**

<!-- For each miss: the cause, and how you know. The four common causes are:
     too few examples for a label, a boundary you applied inconsistently, a
     genuinely hard label pair, and a task the model can't reach from this
     much data.

     ⚠️ Use your agreement report as evidence. It is the only instrument you
     have that can tell a LABELLING problem from a MODEL problem, and this
     section is graded on whether you used it that way. -->



---

## Agreement Report

<!-- Your rate against the staff set, and every disagreement adjudicated.

     Remember you labelled these 30 under the STAFF taxonomy in
     data/staff_taxonomy.md, not your own — so every argument below is made
     from those definitions and those decision rules. -->

**Agreement rate:** ___ / 30 = ___%

<!-- Nobody grades this number. A 60% who argues every disagreement from the
     stated rules beats a 95% who wrote "staff was right" nine times. Several
     of the 30 were chosen because they're genuinely ambiguous — you should be
     winning some of these. -->

**Disagreements**

<!-- Three lines each: the post, both labels, and who you think is right and
     why — grounded in the staff definitions you were both applying.

     Then sort each into one of three piles:
       (a) the rule covered it and I applied it loosely → a consistency problem
       (b) the rule genuinely doesn't say               → a gap in the definitions
       (c) the rule is ambiguous here and my reading is defensible → argue it.
           This is a legitimate win.

     Pile (a) is the one that matters most for your diagnosis: if you applied a
     written rule two different ways on 30 posts, that is direct evidence about
     what you did across your own 200. -->

**1.**
> *The post:*
>
> *Staff said / I said:*
>
> *My call, and why:*
>
> *Which pile:*

**2.**
> *The post:*
>
> *Staff said / I said:*
>
> *My call, and why:*
>
> *Which pile:*

**What the pattern in my disagreements tells me:**



---

## The Improvement

**What I changed:**

**Which diagnosis pointed at it:**

### Run Log — After

| Criterion | Target | Seed 42 | Seed 7 | Seed 2024 | Verdict |
|---|---|---|---|---|---|
| 1.  |  |  |  |  |  |
| 2.  |  |  |  |  |  |
| 3.  |  |  |  |  |  |
| 4.  |  |  |  |  |  |
| 5.  |  |  |  |  |  |

**Did it help, and how do I know:**

<!-- If it didn't, say so. Relabelling that didn't help is a genuinely
     interesting result and earns full credit. -->



---

## What's Still Broken

<!-- For each criterion still missed: what you'd do, and why you stopped. -->



**The gap between what I meant my labels to capture and what the model
learned:**
<!-- Two sentences. Your confusion matrix is the evidence. -->



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
