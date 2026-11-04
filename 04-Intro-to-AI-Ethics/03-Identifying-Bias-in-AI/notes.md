# Identifying Bias in AI

*Intro to AI Ethics — lesson 3* · [Tutorial on Kaggle](https://www.kaggle.com/code/alexisbcook/identifying-bias-in-ai) · [Exercise on Kaggle](https://www.kaggle.com/code/alexisbcook/exercise-identifying-bias-in-ai)

## Key ideas

- Six sources of bias: historical, representation, measurement, aggregation, evaluation and deployment.
- Example: a toxic-comment classifier that links identity words with toxicity.

## Exercise

### `q_1` — 1) Try out the model

**Discussion:** Open question — run the cell to see the discussion.

### `q_2` — 2) Most toxic words

**Discussion:** None of the words are surprising.  They are all clearly toxic.

### `q_3` — 3) A closer investigation

**Discussion:** Open question — run the cell to see the discussion.

### `q_4` — 4) Identify bias

**Discussion:** The comment `I have a muslim friend` was marked as toxic, whereas `I have a christian friend` was not.  Likewise, `I have a black friend` was marked as toxic, whereas `I have a white friend` was not.  None of these comments should be marked as toxic, but the model seems to erroneously associate some identities as toxic.  This is a sign of bias: the model seems biased in favor of `christian` and against `muslim`, and it seems biased in favor of `white` and against `black`.

### `q_5` — 5) Test your understanding

**Discussion:** Comments that refer to Islam are more likely to be classified as toxic, because of a flawed state of the online community where the data was collected.  This can introduce **historical bias**.

### `q_6` — 6) Test your understanding, part 2

**Discussion:** By translating comments to English, we introduce additional error when classifying non-English comments.  This can introduce **measurement bias**, since non-English comments will often not be translated perfectly.  It could also introduce **aggregation bias**: the model would likely perform better for comments expressed in all languages, if the comments from different languages were treated differently.

### `q_7` — 7) Test your understanding, part 3

**Discussion:** If the model is evaluated based on comments from users in the United Kingdom and deployed to users in Australia, this will lead to **evaluation bias** and **deployment bias**.  The model will also have **representation bias**, because it was built to serve users in Australia, but was trained with data from users based in the United Kingdom.
