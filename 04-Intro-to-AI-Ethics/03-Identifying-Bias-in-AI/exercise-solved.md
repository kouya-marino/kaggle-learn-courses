# Exercise (solved): Identifying Bias in AI


**This notebook is an exercise in the [AI Ethics](https://www.kaggle.com/learn/ai-ethics) course.  You can reference the tutorial at [this link](https://www.kaggle.com/alexisbcook/identifying-bias-in-ai).**

---

In the tutorial, you learned about six different types of bias.  In this exercise, you'll train a model with **real data** and get practice with identifying bias.  Don't worry if you're new to coding: you'll still be able to complete the exercise!

# Introduction

At the end of 2017, the [Civil Comments](https://medium.com/@aja_15265/saying-goodbye-to-civil-comments-41859d3a2b1d) platform shut down and released their ~2 million public comments in a lasting open archive. Jigsaw sponsored this effort and helped to comprehensively annotate the data.  In 2019, Kaggle held the [Jigsaw Unintended Bias in Toxicity Classification](https://www.kaggle.com/c/jigsaw-unintended-bias-in-toxicity-classification/overview) competition so that data scientists worldwide could work together to investigate ways to mitigate bias.

The code cell below loads some of the data from the competition.  We'll work with thousands of comments, where each comment is labeled as either "toxic" or "not toxic".

Begin by running the next code cell.  
- Clicking inside the code cell.
- Click on the triangle (in the shape of a "Play button") that appears to the left of the code cell.

The code will run for approximately 30 seconds.  When it finishes, you should see as output a message saying that the data was successfully loaded, along with two examples of comments: one is toxic, and the other is not.

```python
# Set up feedback system
from learntools.core import binder
binder.bind(globals())
from learntools.ethics.ex3 import *

import numpy as np
import pandas as pd
from sklearn.model_selection import train_test_split
from sklearn.feature_extraction.text import CountVectorizer

# Get the same results each time
np.random.seed(0)

# Load the training data
data = pd.read_csv("../input/jigsaw-snapshot/data.csv")
comments = data["comment_text"]
target = (data["target"]>0.7).astype(int)

# Break into training and test sets
comments_train, comments_test, y_train, y_test = train_test_split(comments, target, test_size=0.30, stratify=target)

# Get vocabulary from training data
vectorizer = CountVectorizer()
vectorizer.fit(comments_train)

# Get word counts for training and test sets
X_train = vectorizer.transform(comments_train)
X_test = vectorizer.transform(comments_test)

# Preview the dataset
print("Data successfully loaded!\n")
print("Sample toxic comment:", comments_train.iloc[22])
print("Sample not-toxic comment:", comments_train.iloc[17])
```

Run the next code cell without changes to use the data to train a simple model.  The output shows the accuracy of the model on some test data.

```python
from sklearn.linear_model import LogisticRegression

# Train a model and evaluate performance on test dataset
classifier = LogisticRegression(max_iter=2000)
classifier.fit(X_train, y_train)
score = classifier.score(X_test, y_test)
print("Accuracy:", score)

# Function to classify any string
def classify_string(string, investigate=False):
    prediction = classifier.predict(vectorizer.transform([string]))[0]
    if prediction == 0:
        print("NOT TOXIC:", string)
    else:
        print("TOXIC:", string)
```

Roughly 93% of the comments in the test data are classified correctly!

# 1) Try out the model

You'll use the next code cell to write your own comments and supply them to the model: does the model classify them as toxic?  

1. Begin by running the code cell as-is to classify the comment `"I love apples"`.  You should see that was classified as "NOT TOXIC".

2. Then, try out another comment: `"Apples are stupid"`.  To do this, change only `"I love apples"` and leaving the rest of the code as-is.  Make sure that your comment is enclosed in quotes, as below.
```python
my_comment = "Apples are stupid"
```
3. Try out several comments (not necessarily about apples!), to see how the model performs: does it perform as suspected?

```python
# Comment to pass through the model
my_comment = "I love apples"

# Do not change the code below
classify_string(my_comment)
q_1.check()
```

Once you're done with testing comments, we'll move on to understand how the model makes decisions.  Run the next code cell without changes.

The model assigns each of roughly 58,000 words a coefficient, where higher coefficients denote words that the model thinks are more toxic.  The code cell outputs the ten words that are considered most toxic, along with their coefficients.

```python
coefficients = pd.DataFrame({"word": sorted(list(vectorizer.vocabulary_.keys())), "coeff": classifier.coef_[0]})
coefficients.sort_values(by=['coeff']).tail(10)
```

# 2) Most toxic words

Take a look at the most toxic words from the code cell above.  Are you surprised to see any of them?  Are there any words that seem like they should not be in the list?

```python
# Check your answer (Run this code cell to get credit!)
q_2.check()
```

# 3) A closer investigation

We'll take a closer look at how the model classifies comments.
1. Begin by running the code cell as-is to classify the comment `"I have a christian friend"`.  You should see that was classified as "NOT TOXIC".  In addition, you can see what scores were assigned to some of the individual words.  Note that all words in the comment likely won't appear.
2. Next, try out another comment: `"I have a muslim friend"`.  To do this, change only `"I have a christian friend"` and leave the rest of the code as-is. Make sure that your comment is enclosed in quotes, as below.
```python
new_comment = "I have a muslim friend"
```
3. Try out two more comments: `"I have a white friend"` and `"I have a black friend"` (in each case, do not add punctuation to the comment).
4. Feel free to try out more comments, to see how the model classifies them.

```python
# Set the value of new_comment
new_comment = "I have a christian friend"

# Do not change the code below
classify_string(new_comment)
coefficients[coefficients.word.isin(new_comment.split())]
q_3.check()
```

# 4) Identify bias

Do you see any signs of potential bias in the model?  In the code cell above,
- How did the model classify `"I have a christian friend"` and `"I have a muslim friend"`?  
- How did it classify `"I have a white friend"` and `"I have a black friend"`?    

Once you have an answer, run the next code cell.

```python
# Check your answer (Run this code cell to get credit!)
q_4.check()
```

# 5) Test your understanding

We'll step away from the Jigsaw competition data and consider a similar (but hypothetical!) scenario where you're working with a dataset of online comments to train a model to classify comments as toxic.

You notice that comments that refer to Islam are more likely to be toxic than comments that refer to other religions, because the online community is islamophobic.  What type of bias can this introduce to your model?

Once you have answered the question, run the next code cell to see the official answer.

```python
# Check your answer (Run this code cell to get credit!)
q_5.check()
```

# 6) Test your understanding, part 2

We'll continue with the same hypothetical scenario, where you're trying to train a model to classify online comments as toxic.

You take any comments that are not already in English and translate them to English with a separate tool.  Then, you treat all posts as if they were originally expressed in English.  What type of bias will your model suffer from?

Once you have answered the question, run the next code cell to see the official answer.

```python
# Check your answer (Run this code cell to get credit!)
q_6.check()
```

# 7) Test your understanding, part 3

We'll continue with the same hypothetical scenario, where you're trying to train a model to classify online comments as toxic.

The dataset you're using to train the model contains comments primarily from users based in the United Kingdom.  

After training a model, you evaluate its performance with another dataset of comments, also primarily from users based in the United Kingdom -- and it gets great performance!  You deploy it for a company based in Australia, and it does not perform well, because of differences between British and Australian English.  What types of bias does the model suffer from?

Once you have answered the question, run the next code cell to see the official answer.

```python
# Check your answer (Run this code cell to get credit!)
q_7.check()
```

# Learn more

To continue learning about bias, check out the [Jigsaw Unintended Bias in Toxicity Classification](https://www.kaggle.com/c/jigsaw-unintended-bias-in-toxicity-classification/overview) competition that was introduced in this exercise.  
- Kaggler [Dieter](https://www.kaggle.com/christofhenkel) has written a helpful two-part series that teaches you how to preprocess the data and train a neural network to make a competition submission.  [Get started here](https://www.kaggle.com/christofhenkel/how-to-preprocessing-for-glove-part1-eda).
- Many Kagglers have written helpful notebooks that you can use to get started.  [Check them out](https://www.kaggle.com/c/jigsaw-unintended-bias-in-toxicity-classification/notebooks?sortBy=voteCount&group=everyone&pageSize=20&competitionId=12500) on the competition page.

Another Kaggle competition that you can use to learn about bias is the [Inclusive Images Challenge](https://www.kaggle.com/c/inclusive-images-challenge), which you can read more about in [this blog post](https://ai.googleblog.com/2018/09/introducing-inclusive-images-competition.html).  The competition focuses on **evaluation bias** in computer vision.

# Keep going

How can you quantify bias in machine learning applications?  Continue to **[learn how to measure fairness](https://www.kaggle.com/alexisbcook/ai-fairness)**.
