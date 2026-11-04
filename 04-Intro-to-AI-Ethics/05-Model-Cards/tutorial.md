# Model Cards


# Introduction
 
A **model card** is a short document that provides key information about a machine learning model.  Model cards increase transparency by communicating information about trained models to broad audiences.
 
In this tutorial, you will learn about which audiences to write a model card for and which sections a model card should contain.  Then, in the following **[exercise](https://www.kaggle.com/kernels/fork/15577440)**, you will apply what you have learned to a couple of real-world scenarios.

# Model cards
 
Though AI systems are playing increasingly important roles in every industry, few people understand how these systems work. AI researchers are exploring many ways to communicate key information about models to inform people who use AI systems, people who are affected by AI systems and others.

Model cards - introduced in a [2019 paper](https://arxiv.org/abs/1810.03993) - are one way for teams to communicate key information about their AI system to a broad audience. This information generally includes intended uses for the model, how the model works, and how the model performs in different situations.

You can think of model cards as similar to the nutritional labels that you find on packaged foods.

# Examples of model cards

Before we continue, it might be useful to briefly skim some examples of model cards. 
- [Salesforce's model cards](https://blog.einstein.ai/model-cards-for-ai-model-transparency/)
- [Open AI’s model card for GPT-3](https://github.com/openai/gpt-3/blob/master/model-card.md)
- [Google Cloud's example model cards](https://modelcards.withgoogle.com/face-detection)

# Who is the audience of your model card?

A model card should strike a balance between being easy-to-understand and communicating important technical information. When writing a model card, you should consider your audience: the groups of people who are most likely to read your model card. These groups will vary according to the AI system’s purpose. 

For example, a model card for an AI system that helps medical professionals interpret x-rays to better diagnose musculoskeletal injuries is likely to be read by medical professionals, scientists, patients, researchers, policymakers and developers of similar AI systems. The model card may therefore assume some knowledge of health care and of AI systems.

# What sections should a model card contain?

Per the original paper, a model card should have the following nine sections. Note that different organizations may add, subtract or rearrange model card sections according to their needs (and you may have noticed this in some of the examples above).

As you read about the different sections, you're encouraged to review the two example model cards from the original paper.  Before proceeding, open each of these model card examples in a new window:
- [Model Card - Smiling Detection in Images](https://github.com/Kaggle/learntools/blob/master/notebooks/ethics/pdfs/smiling_in_images_model_card.pdf)
- [Model Card - Toxicity in Text](https://github.com/Kaggle/learntools/blob/master/notebooks/ethics/pdfs/toxicity_in_text_model_card.pdf)

## 1. Model Details     
* Include background information, such as developer and model version.
 
## 2. Intended Use
- What use cases are in scope?
- Who are your intended users?
- What use cases are out of scope?
 
## 3. Factors
- What factors affect the impact of the model? For example, the smiling detection model's results vary by demographic factors like age, gender or ethnicity, environmental factors like lighting or rain and instrumentation like camera type.
 
## 4. Metrics
- What metrics are you using to measure the performance of the model? Why did you pick those metrics?
  - For **classification systems** – in which the output is a class label – potential error types include false positive rate, false negative rate, false discovery rate, and false omission rate. The relative importance of each of these depends on the use case.
  - For **score-based analyses** – in which the output is a score or price – consider reporting model performance across groups.

 
## 5. Evaluation Data
- Which datasets did you use to evaluate model performance?  Provide the datasets if you can.
- Why did you choose these datasets for evaluation?
- Are the datasets representative of typical use cases, anticipated test cases and/or challenging cases?
 
## 6. Training Data
- Which data was the model trained on?
 
## 7. Quantitative Analyses
- How did the model perform on the metrics you chose? Break down performance by important factors and their intersections. For example, in the smiling detection example, performance is broken down by age (eg, young, old), gender (eg, female, male), and then both (eg, old-female, old-male, young-female, young-male).
 
## 8. Ethical Considerations
- Describe ethical considerations related to the model, such as sensitive data used to train the model, whether the model has implications for human life, health, or safety, how risk was mitigated, and what harms may be present in model usage.
 
## 9. Caveats and Recommendations
- Add anything important that you have not covered elsewhere in the model card.

# How can you use model cards in your organization? 

The use of detailed model cards can often be challenging because an organization may not want to reveal its processes, proprietary data or trade secrets. In such cases, the developer team should think about how model cards can be useful and empowering, without including sensitive information.

Some teams use other formats - such as [FactSheets](https://aifs360.mybluemix.net/) - to collect and log ML model information.

# Your turn

Apply what you've learned to **[decide how to use model cards](https://www.kaggle.com/kernels/fork/15577440)** in real-world scenarios.

---




*Have questions or comments? Visit the [course discussion forum](https://www.kaggle.com/learn/ai-ethics/discussion) to chat with other learners.*
