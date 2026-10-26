# Acceptance criteria — TakeMeter

Five criteria that say what "working" means for this classifier, written in
unit 5 **before** anything was trained.

**All five are yours this time.** None are given. You've had two projects of
practice.

An acceptance criterion names a number. *"The model is accurate"* is an
opinion. *"Every label has an F1 of at least 0.60 on the held-out set"* is a
criterion.

Under each, write a sentence or two on **why that number**. A reason that says
something about your data or your taxonomy earns credit — *"I picked 0.60 F1
for `reaction` because it's my smallest label and I only have about 50
examples of it"*. A reason that could be attached to any project does not.

> Missing your own targets next unit costs you nothing. Setting a target so
> easy you can't miss it does.

---

## Pick numbers you can defend

Not numbers that sound impressive. Three labels means a coin-flip guesser gets
about 33%, so a target of 0.40 is barely a target. Your number should sit
somewhere you'd honestly call useful.

**Cover at least three of these five areas.** They're here as prompts, not as a
form to fill in — a criterion that fits none of them is fine if it names a
number.

| Area | A question it could answer |
|---|---|
| Overall accuracy | How often does it need to be right to be worth using? |
| Per-label performance | Is one label allowed to be much worse than the others? |
| Balance | How lopsided can your label counts get before it's a problem? |
| Consistency | If someone else labelled the same posts, how often should you agree? |
| Confidence | Should a confident prediction be right more often than an unsure one? |

Two things worth knowing before you pick numbers, because both will affect
whether you hit them:

- **Your smallest label will have the jumpiest score.** If a label has 50
  examples, about 8 land in the test split. An F1 computed on 8 examples moves
  a lot between seeds. A target for that label should be looser than one for
  your biggest label, and saying so is a good reason.
- **Unit 6 tests across three seeds, and the target has to hold across all
  three.** A target of 0.65 against results of 0.71, 0.62, 0.68 is a **miss**.
  Pick with that in mind — it is stricter than it first sounds.

---

## 1. Overall accuracy is at least 0.70.

**Why this target:**
My test set is about 23 posts, so 0.70 means at least 17 correct. A coin flip gets about 11-12, and I only have two labels, so I want a clear gap above that. Anything lower would be hard to tell apart from luck on 23 posts.

---

## 2. No label makes up more than 60% of the data.

**Why this target:**
I have 152 posts split 76/76. r/kpophelp gets more recommendation requests than advice questions, so more scraping will likely skew it. At 60/40, always guessing the top label scores 0.60, still under criterion 1's 0.70. At a 70/30 skew it would score 0.70 and pass without learning anything.

## 2. New Revision: Overall F1 macro is at least 0.75

**Why this target:**
Overall F1 macro is at least 0.75. Macro F1 computes an F1 score for each class one-versus-rest and averages them with equal weight. Since this is a binary classification problem without class imbalance, the F1 macro score can measure a global "pulse" of how well the model is balancing precision and recall overall. In the k-pop data set, there are a balanced number of `advice` and `recommendation` posts, so I have higher performance expectations for the overall system.

---

## 3. Both labels have recall of at least 0.65 on the held-out set, on every seed.

**Why this target:**
The test set has 11 recommendation and 12 advice posts, so 0.65 means at least 8 of 11 and 8 of 12 correct. That beats the coin-flip lines (6/11, 7/12) but allows a miss or two. Checking recall per label catches a model that dumps everything into one label, which overall accuracy can hide. The advice/recommendation line is also fuzzy: "Need birthday song recommendations... I'm looking for mellow songs" reads like both.

---

## 4. For each label, precision and recall differ by no more than 0.15.

**Why this target:**
My data is balanced, so the model shouldn't favor one label. A big gap means one label is swallowing the other, for example high recall but low precision on recommendation means advice posts are being called recommendations. 0.15 is about 2 posts out of 11-12, so one stray post won't fail it.

---

## 5. Every label has an F1 of at least 0.60 on the held-out set.

**Why this target:**
Each label has only 11-12 test posts, so F1 will jump between seeds and I set the bar lower than overall accuracy. 0.60 is a floor for each label separately: criteria 3 and 4 can pass while precision is poor, and F1 catches that.

---

<!-- ─────────────────────────────────────────────────────────────────────────
     UNIT 6 — read this before you change anything above.

     If a criterion turns out to be BROKEN rather than merely unmet, you can
     revise it, and that earns credit. But never delete or edit the original
     line. Add the revision underneath, like this:

         ## 2. Every label performs acceptably

         The model performs well on all labels.

         **Why this target:** ...

         > **Revised in unit 6:** Every label has an F1 of at least 0.60 on
         > the held-out set.
         >
         > **Why revised:** "performs well" gave me nothing to check. I
         > couldn't produce a verdict from it at all.

     That's a revision because the criterion couldn't be MEASURED.

     Lowering a target because you missed it is not a revision, and it costs
     you the point:

         ✗ "Overall accuracy of at least 0.65" → "at least 0.55", because
            0.65 turned out to be optimistic for 200 examples.

     A number you missed stays where it is, gets diagnosed, and gets a fix
     attempted. That's where the points are.
     ───────────────────────────────────────────────────────────────────────── -->
