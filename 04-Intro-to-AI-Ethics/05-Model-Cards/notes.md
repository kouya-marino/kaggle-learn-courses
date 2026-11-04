# Model Cards

*Intro to AI Ethics — lesson 5* · [Tutorial on Kaggle](https://www.kaggle.com/code/var0101/model-cards) · [Exercise on Kaggle](https://www.kaggle.com/code/var0101/exercise-model-cards)

## Key ideas

- A model card documents intended use, training data, metrics, limitations and ethical considerations.
- Write it for the people who will use or be affected by the model.

## Exercise

### `q_1` — 1) Audience

**Discussion:** Model cards should be written for the groups that are most likely to read it. For *Simple Zoom*, such groups probably include people using the tool to record videos, organizations seeking to adopt the tool, IT and audio-visual teams and agencies, computer vision researchers, policymakers and developers of similar AI systems. Given how broad this group is, your team can only assume a basic knowledge of video recording terms throughout the model card.

### `q_2` — 2) Intended Use

**Discussion:** Since *Simple Zoom* is not suitable for presentations in which the presenter is partially or fully hidden at any time, it might not work well in a presentation in which the presenter uses a large object, because the object could partially or fully hide the presenter. There are many potential ways to address this issue. For example, your team could reach out to the *Simple Zoom* team to assess the potential risks and harms of using *Simple Zoom* with props. As another example, your team could eventually add a message in the Presenter Pro user interface explaining that the *Simple Zoom* feature should not be used in presentations that use props.

### `q_3` — 3) Factors, Evaluation Data, Metrics, and Quantitative Analyses

**Discussion:** There are many possible answers to this question. For example, you may want to check that the model’s equal performance across demographic groups (gender, skin tone and age) remains equal across different camera angles, distances from camera, camera types and lighting conditions. As another example, you may want to know how well the model performs from the specific camera angles that _Production Pro_ customers most commonly use.
