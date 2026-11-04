# Exercise: Model Cards


**This notebook is an exercise in the [AI Ethics](https://www.kaggle.com/learn/ai-ethics) course.  You can reference the tutorial at [this link](https://www.kaggle.com/var0101/model-cards).**

---

In the tutorial, you learned how to use model cards.  In this exercise, you'll sharpen your understanding of model cards by engaging with them in a couple of scenarios.

# Introduction

Run the next code cell to get started.

```python
from learntools.core import binder
binder.bind(globals())
from learntools.ethics.ex5 import *
```

# Scenario A

You are the creator of the _Simple Zoom_ video editing tool, which uses AI to automatically zoom the video camera in on a presenter as they walk across a room during a presentation. You are launching the _Simple Zoom_ tool and releasing a model card along with the tool, in the interest of transparency.

# 1) Audience

Which audiences should you write the model card for? Once you have thought about your answer, check it against the solution below.

```python
# Check your answer (Run this code cell to receive credit!)
q_1.check()
```

# Scenario B

You are the product manager for _Presenter Pro_, a popular video and audio recording product for people delivering talks and presentations. As a new feature based on customer demand, your team has been planning to add the AI-powered ability for a single video camera to automatically track a presenter, focusing on them as they walk across the room or stage, zooming in and out automatically and continuously adjusting lighting and focus within the video frame. 

You are hoping to incorporate a different company’s AI tool (called _Simple Zoom_) into your product (_Presenter Pro_). To determine whether _Simple Zoom_ is a good fit for _Presenter Pro_, you are reviewing *Simple Zoom*’s model card.

# 2) Intended Use

The **Intended Use** section of the model card includes the following bullets:
* _Simple Zoom_ is intended to be used for automatic zoom, focus, and lighting adjustment in the real-time video recording of individual presenters by a single camera
* _Simple Zoom_ is not suitable for presentations in which there is more than one presenter or for presentations in which the presenter is partially or fully hidden at any time

As a member of the team evaluating _Simple Zoom_ for potential integration into _Presenter Pro_, you are aware that _Presenter Pro_ only supports one presenter per video.

However, you are also aware that in some _Presenter Pro_ customers use large props in their presentation videos. Given the information in the Intended Use section of the model card, what problem do you foresee for these customers if you integrate _Simple Zoom_ into _Presenter Pro_? What are some ways in which you could address this issue?

```python
# Run this code cell to receive a hint
q_2.hint()
```

```python
# Check your answer (Run this code cell to receive credit!)
q_2.check()
```

# 3) Factors, Evaluation Data, Metrics, and Quantitative Analyses

We'll continue with **Scenario B**, where you are the product manager for _Presenter Pro_.  Four more sections of the model card for _Simple Zoom_ are described below.

**Factors**: The model card lists the following factors as potentially relevant to model performance: 
* Group Factors
  * Self-reported gender
  * Skin tone
  * Self-reported age
* Other Factors
  * Camera angle
  * Presenter distance from camera
  * Camera type
  * Lighting

**Evaluation Data**: To generate the performance metrics reported in the **Quantitative Analysis** section (discussed below), the _Simple Zoom_ team used an evaluation data set of 500 presentation videos, each between two and five minutes long. The videos included both regular and unusual presentation and recording scenarios and included presenters from various demographic backgrounds.

**Metrics**: Since _Simple Zoom_ model performance is subjective (involving questions like whether a zoom is of appropriate speed or smoothness; or whether a lighting adjustment is well-executed), the _Simple Zoom_ team tested the tool’s performance by asking a diverse viewer group to view _Simple Zoom_’s output videos (using the evaluation dataset’s 500 videos as inputs). Each viewer was asked to rate the quality of video editing for each video on a scale of 1 to 10, and each video’s average rating was used as a proxy for _Simple Zoom_’s performance on that video.

**Quantitative Analyses**: The quantitative analyses section of the model card includes a brief summary of performance results. According to the summary, the model generally performs equally well across all the listed demographic groups (gender, skin tone and age).

The quantitative analyses section also includes interactive graphs, which allow you to view the performance of the _Simple Zoom_ tool by each factor and by intersections of ‘Group’ and ‘Other’ factors.

As a member of the team evaluating _Simple Zoom_ for potential integration into _Presenter Pro_, what are some questions you might be interested in answering and exploring via the interactive graphs?

```python
# Check your answer (Run this code cell to receive credit!)
q_3.check()
```

# Conclusion

Congratulations!  You have reached the end of the AI Ethics course.  Once you have viewed all of the tutorials and successfully answered the questions in the exercises, you will receive a completion certificate to celebrate your hard work.  

If you enjoyed the AI Ethics course, we recommend the [**Machine Learning Explainability**](https://www.kaggle.com/learn/machine-learning-explainability) course as a next step.  To prepare for the content in this course, you should have some background in python (which you can get from the [**Python**](https://www.kaggle.com/learn/python) course) and machine learning (which you can get from the [**Intro to Machine Learning**](https://www.kaggle.com/learn/intro-to-machine-learning) course).

---




*Have questions or comments? Visit the [course discussion forum](https://www.kaggle.com/learn/ai-ethics/discussion) to chat with other learners.*
