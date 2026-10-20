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

## 1. Overall accuracy is at least 0.60.

<!-- Your criterion. It must name a number. -->

**Why this target:**
Since there are 2 labels, a random coin flip at best would return 50% accuracy due to chance. If the model is worth using, it has to be at least marginally better than randomly flipping a coin.

---

## 2. Label imbalance can only be up to 0.7.

**Why this target:**
No label above 70% of your data. If one label dominates, the model learns to guess it and nothing else. Since there are only 2 classes, the model could be sensitive to class imbalance. 



---

## 3. Both labels have recall of at least 0.65 on the held-out set, on every seed.

**Why this target:**
The test split is about 23 posts (11 recommendation, 12 advice), so one post moves recall by roughly 9 points. 0.65 means at least 8 of 11 and 8 of 12 correct, which is clearly above the coin-flip lines of 6/11 and 7/12 but still survives a one-post swing between seeds. Recall per label (not overall accuracy) catches the failure where the model dumps everything into one label. My classes are perfectly balanced (76/76), so there is no majority class to hide behind, and the advice/recommendation boundary is fuzzy (e.g. "Need birthday song recommendations... I'm looking for mellow songs" asks for a recommendation but reads like advice-seeking).

---

## 4. For each label, precision and recall differ by no more than 0.15.

**Why this target:**
With balanced data, a healthy model should not systematically over-predict one label. A big precision/recall gap on one label means the other label is being absorbed into it (e.g. high recall but low precision on recommendation means advice posts are being called recommendations). 0.15 is about 2 posts out of the 11-12 per label: tight enough to expose lopsided behavior, loose enough that a single-post swing does not fail it.

---

## 5. Every label has an F1 of at least 0.60 on the held-out set.

**Why this target:**
If the data set is imbalanced, then the accuracy metric may be misleading. The F1 score effectively captures the trade-off between precision and recall, offering a comprehensive evaluation of model performance.


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
