---
title: Introduction to Machine Learning and Machine Learning Systems
author: Raffi Khatchadourian (based on material from Christian Kaestner and Eunsuk Kang)
date: November 26, 2025
semester: Fall 2025
lang: en
footer: Based on "Machine Learning in Production/AI Engineering" by Christian Kaestner and Eunsuk Kang, Carnegie Mellon University
license: Creative Commons Attribution-ShareAlike 4.0 International (CC BY-SA 4.0)
---

# Introduction to Machine Learning and Machine Learning Systems

## Disclaimer

New part of the course.

## What is Machine Learning (ML)?

:::::::::::::: {.columns}
::: {.column width="50%"}

![AI vs. ML](graphics/AIvsML.jpg){width=90% title="Courtesy Eunsuk Kang."}

:::
::: {.column width="50%"}

- ML is a subfield of Artificial Intelligence (AI).
- ML is concerned with the design and development of algorithms that allow computers to learn from, make predictions or decisions, or generate "new" data based on ("other") data.[^1]
- This is different than traditional programming, where "hard-and-fast" rules are explicitly coded by programmers.
  - Conditional statements, loops, functions, etc.
- In ML, the system *learns* patterns from data and uses these patterns to make predictions or decisions on new, unseen data or generate "new" data.

[^1]: Whether "new" data is actually generated or illegally copied (sometimes verbatim) is currently a controversial topic in the AI/ML community. The problem lies in the "explainability" of ML models, especially large language models (LLMs) and generative AI models.

:::
::::::::::::::

## Foundation Models

:::::::::::::: {.columns}
::: {.column width="50%"}

![AI vs. ML](graphics/AIvsML.jpg){width=90% title="Courtesy Eunsuk Kang."}

:::
::: {.column width="50%"}

- Foundation models are large-scale machine learning models trained on vast amounts of data.
- They are contained within "Deep Learning" in the Venn diagram above.
- They are also referred to as "generative AI" models and include large language models (LLMs) like GPT-4, PaLM, and LLaMA.
- Foundation models can perform a wide range of tasks, such as text generation, image generation, and more, often with minimal fine-tuning for specific applications.

:::
::::::::::::::

## Types of Machine Learning (I)

- **Supervised Learning**: The model is trained on labeled data, where the input data is paired with the correct output. The goal is to learn a mapping from inputs to outputs.
- **Unsupervised Learning**: The model is trained on unlabeled data and must find patterns or structures in the data without explicit guidance.
- **Reinforcement Learning**: The model learns to make decisions by taking actions in an environment to maximize some notion of cumulative reward.
- **Semi-supervised Learning**: Combines both labeled and unlabeled data for training, often used when acquiring labeled data is expensive or time-consuming.
- **Self-supervised Learning**: The model generates its own labels from the input data, often used in natural language processing and computer vision tasks.
- **Deep Learning**: A subset of ML that uses neural networks with many layers (deep architectures) to model complex patterns in data.
- **Transfer Learning**: The model leverages knowledge gained from one task to improve performance on a related but different task.

## Types of Machine Learning (II)

- **Online Learning**: The model learns incrementally from a stream of data, updating its knowledge as new data arrives.
- **Federated Learning**: The model is trained across multiple decentralized devices or servers while keeping the data localized, enhancing privacy and security.
- **Active Learning**: The model actively selects the most informative data points to label, reducing the amount of labeled data needed for training.
- **Ensemble Learning**: Combines multiple models to improve overall performance, often by averaging predictions or using voting mechanisms.
- **Generative Learning**: The model learns to generate new data samples that resemble the training data, often used in applications like image synthesis and text generation.

## Applications of Machine Learning

- **Natural Language Processing (NLP)**: Language translation, sentiment analysis, chatbots.
- **Computer Vision**: Image recognition, object detection, facial recognition.
- **Recommendation Systems**: Product recommendations, content suggestions.
- **Healthcare**: Disease diagnosis, personalized treatment plans.
- **Finance**: Fraud detection, algorithmic trading.
- **Autonomous Vehicles**: Self-driving cars, traffic prediction.
- **Robotics**: Robot navigation, manipulation tasks.
- **Gaming**: Game AI, player behavior prediction.
- **Marketing**: Customer segmentation, targeted advertising.
- **Cybersecurity**: Threat detection, anomaly detection.
- **Speech Recognition**: Voice assistants, transcription services.
- **Software Development**: Code completion, bug detection.

## Case Study: Food Delivery Service

![DoorDash food delivery app](graphics/doordash.png){width=60% title="Courtesy DoorDash."}

## Predicting Delivery Time

* What are its objective? How do we measure success?
* How do we present intelligence & receive feedback?
* How do we build the intelligence?
  * What factors does it depend on?
  * What can be used for learning & prediction?

## How Does ML Work?

- ML algorithms build models based on sample data, known as "training data," to make predictions or decisions without being explicitly programmed to perform the task.
- The process typically involves:
  1. Collecting and preparing data.
  2. Choosing a suitable ML algorithm.
  3. Training the model on the training data.
  4. Evaluating the model's performance on unseen data (test data).
  5. Tuning the model to improve performance.

## Typical Machine Learning Pipeline

![ML Pipeline](graphics/ML-pipeline.png){width=60% title="Courtesy Semi Koen."}

## ML Tasks by Phase

### Before Deployment

1. Obtain labeled data.
1. Identify and extract features.
1. Split data into training and evaluation set.
1. Learn model from training data.
1. Evaluate model on evaluation data.
1. Repeat, revising features.

### After Deployment

1. Evaluate model on production data; monitor.
1. Select production data for retraining.
1. Update model regularly.

## Design Decisions in ML-based Systems

* Data collection and preparation.
  * Training vs test sets, sizes.
* Feature engineering.
* Model selection & configuration.
  * Structure: Number of layers, decision tree depth, etc., depending on model type.
  * Hyperparameters: Learning rate, regularization parameters, etc.
  * Search algorithms.
* (More ...)

## Example Data

| RestaurantID | Order| OrderTime|ReadyTime|PickupTime|
|-|-|-|-|-|
| 5 |5A;3;10;11C;C:No onion| 18:11|18:23|18:31|
|...|
|...|
|...|

## Data Processing

### Data Cleaning

* Remove outliers.
* Normalize data.
* Fill in missing values.
* Remove misleading/useless items.

### Feature Engineering

* Identify parameters of interest that a model can learn on.
* Convert initial data into feature set.
* Select relevant subset of features.

> QUESTION: What features would you use for delivery prediction?

## Features

![DoorDash food delivery app](graphics/doordash.png){width=60% title="Courtesy DoorDash."}

## Possible Features for Delivery Prediction

1. Order time, day of week.
1. Average number of orders in that hour.
1. Order size.
1. Special requests.
1. Order items.
1. Preparation time.

## Learning

Build a predictor that best describes an outcome for the observed features.

| RestaurantID | Order3 | SpecialRequest | DayOfWeek | PreparationTime |
|-|-|-|-|-|
|5|yes| yes|2|12|
|...|
|...|
|...|

## Evaluation

* Evaluate model accuracy on *learned* data vs. previously *unseen* data.
  * Separate learning set, not used for training.

![Dataset partitioning.](graphics/data-sets.png){width=50% title="Courtesy Eunsuk Kang."}

## Evaluation Methods

* Binary predictors.
    * Is a data point in class A or not?
    * False positives vs. false negatives, recall, precision.
    * This is called a confusion matrix.
    * Commonly used for several tasks, including:
        1. Classification tasks
        1. Information retrieval.
* Numeric predictors.
    * Output is a number.
    * Average (relative) distance between real & predicted values.
    * Mean squared error, mean absolute error.
* Ranking predictors.
    * Top-K algorithms, etc.
    * Evaluate quality of ranking against some "ground" truth.
* (More ...)

## Evaluation Methods

![DoorDash food delivery app](graphics/doordash.png){width=60% title="Courtesy DoorDash."}

## Precision and Recall

![Precision and recall.](graphics/recallprecision.png){width=25% title="Courtesy Eunsuk Kang."}

## Underfitting vs. Overfitting

* Overfitting.
    * Model learns exactly the input data.
    * Does not *generalize* to unseen data.
* Underfitting.
    * Model makes very general observations.
    * Poorly fits to data.

### Balancing Underfitting and Overfitting

* Adjust degrees of freedom in the model to balance between overfitting and underfitting.
    * Challenging to get right in practice!

## Underfitting Example

::: columns

:::: column
|Text|Genre|
|-|-|
|When the earth stood ... |Science fiction|
|Two households, both alike...|Romance|
|To Sherlock Holmes she...|Adventure|
::::

:::: column
![Underfitting: an overly simple model that fits the data loosely](graphics/underfitting.png)
::::

:::

## Overfitting Example

::: columns

:::: column
|Text|Genre|
|-|-|
|When the earth stood ... |Science fiction|
|Two households, both alike...|Romance|
|To Sherlock Holmes she...|Adventure|
::::

:::: column
![Overfitting: an overly complex model that fits the training data too tightly](graphics/overfitting.png)
::::

:::

## Learning and Evaluating in Production

* Beyond static data sets, build telemetry.
* Use sample of live data for evaluation.
* Retrain models with sampled live data regularly.
* Monitor objectives and intervene if necessary.
