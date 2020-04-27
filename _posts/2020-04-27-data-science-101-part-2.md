---
layout: single
classes: wide
title: Data Science 101 - Part 2
date: 2020-04-27
tags: [machine learning]
category: [blog, data science 101]
mathjax: true
---

This is the Part 2 of a series of posts that cover basic concepts of Data Science. In this post, I will focus on Machine Learning and define the main learning strategies that these methods use. I will also try to illustrate these strategies by giving examples of when each one is used. The main objective here is to give an overview of each learning strategy and not to go into details (yet).

Part 1 of this series covered the main areas within Data Science, a few commonly used terms and applications. Part 1 can be found [here](/blog/2020-04-14-data-science-101-part-1/).

---

# Machine Learning - Learning strategies

Machine learning's main goal is to develop algorithms that are capable of creating models that can make non-trivial decisions without explicit instructions. This is usually done by learning through past experience or by making assumptions as to how each decision should be made. Many different approaches can be used to achieve this. The most common approaches can be put into one of these four categories: Supervised Learning; Semi-Supervised Learning; Unsupervised Learning; and Reinforcement Learning.

## Supervised Learning

__Supervised Learning__ focuses on creating models when there is data available stating which decisions should have been made on past observations. That is, Supervised Learning methods require a dataset with __labelled examples__, where each labelled example consists of the information used to make the decision (commonly called _X_) and the label that indicates the decision that should be made (usually represented by _y_). This approach can be seen as a parallel to a person learning a certain topic by studying a set of questions and answers on that topic and then proceeding to answer never before seen questions on the same topic.

__Classification__ is a task usually addressed with Supervised Learning algorithms. In this task, the machine learning model (_classifier_) is given an example (also called observation) and is asked to place this example in one (or more) category (a.k.a. _class_). The set of possible categories is predefined and the dataset used to train the classifier needs to contain a representative sample of every class. Binary classification tasks focus on predicting a single binary output (e.g. Yes / No), while multi-class classification allows more than two categories. Another problem that is tackled by Supervised learning methods is __Regression__. This is similar to Classification, however the output of the model is continuous instead of categorical. For example, consider a supervised model that is trained on a dataset of dog images to make a decision, based on their appearance, which is each dog's breed. In this scenario: each image is used as the information that led to a decision (_X_); the decision itself is which is the dog's breed (_y_); the set of possible classes is defined by all the dog breeds included in the dataset used to train the model. Another example would be to train a supervised model to predict the price of a house given the house's characteristics, such as number of bedrooms, neighbourhood and size. In this case, the list of characteristics is used to make a decision (_X_); and the decision is how expensive is each house (_y_). These examples illustrate a classification and a regression task, respectively.

Another learning approach I consider to be part of Supervised Learning is __Collaborative Filtering__. Collaborative Filtering is used by many __Recommendation Systems__ as a way to predict a user's behaviour based on the behaviour of similar users and the user's behaviour towards similar objects. I will go into more details on how this works and other ways to train Recommendation systems on another post.

## Unsupervised Learning

While Supervised Learning uses labelled examples to learn from past experience, __Unsupervised Learning__ focuses on cases where labels are not available and finds patterns in the data based only on the information available for each observation. This is usually done by making assumptions about how the data is organised, such assuming certain characteristics about the statistical distribution the data is sampled from. Unsupervised learning algorithms are specially useful when labels are not available and/or hard to obtain, when doing exploratory analysis of datasets and to make changes to the dataset with the goal of simplifying or cleaning it.

The most common application of Unsupervised learning algorithms is __Clustering__, which creates groups (clusters) of examples based on similarity. That is, Clustering algorithms group examples in a way that examples in the same cluster are more similar than examples in different clusters, in other words, these methods maximise _intra-cluster_ similarity while minimising _inter-cluster_ similarity. __Anomaly Detection__ is also commonly addressed as an Unsupervised learning problem (even though it can be treated as a Supervised or Semisupervised problem too) where the algorithm tries to create a model that defines what _normal_ behaviour looks like and any examples that do not fit that model are considered to be _anomalous_. These anomalous examples are often called: anomalies, outliers, novelties or exceptions. Anomaly detection is frequently used for problems such as bank fraud, medical diagnosis and fault detection.

Lastly, most Machine Learning methods are not able to deal with the raw data directly, for example a text or an image. These methods need a numerical representation (commonly called _feature vector_) for each example which can be created in several different ways (which I will address in a future post). Creating these feature vectors generates a _feature space_ where all the examples in a dataset are projected. However, the created feature space might contain redundant information and/or noise. Unsupervised learning algorithms can be used to make changes to the feature space making it easier to understand or visualise (_dimensionality reduction_); or to remove unwanted characteristics or information contained in that space. A very well known unsupervised learning method that can be used for these purposes is __Principal Component Analysis__ (PCA), which finds dimensions in the feature space in way that the dimensions are sorted by how much data variability they capture. Again, I will go into more details on how this method works in a future post, when talking about _feature projection_.

## Semisupervised Learning

__Semisupervised Learning__ is a grey area between Supervised learning and Unsupervised learning where methods use weaker types of supervision (e.g. noisy or imprecise labels), a mix between labelled and unlabelled examples, or  information that is not part of the dataset as a proxy for labels (e.g. descriptions of each label). These methods are usually a good option when having access to a large quantity of unlabelled samples but only a small amount of labelled samples is available, specially when labelling is too expensive. Semisupervised learning algorithms usually tackle similar problems to Supervised learning, like __Classification__ and __Regression__. However, these methods can also be used in other tasks such as to extend the available labels to unlabelled examples automatically (for example, by using __Label Propagation__), which can then be used on a Supervised method.

## Reinforcement Learning

Finally, __Reinforcement Learning__ focuses on goal-centred algorithms that maximise the rewards obtained based on  policies over several steps. That is, one or more reward functions are predefined based on the task at hand and the model is trained to maximise the rewards gained. These algorithms are used for several different applications but got particularly famous for their applications in robotics ([like Deep Mind's model that learn to walk and overcome several obstacles](https://deepmind.com/blog/article/producing-flexible-behaviours-simulated-environments)) and gaming (e.g. [the AI trained to play Super Mario Bros](https://www.youtube.com/watch?v=qv6UVOQ0F44)).

There are different ways of designing Reinforcement Learning algorithms, the most common being __Temporal Difference__, which updates the rewards and evaluates the decision making at every _step_ (instead of evaluating entire _episodes_ - from start to end state). Within Temporal Difference, two types of learning take prominence: (1) __State-Action-Reward-State-Action__ (SARSA); (2) __Q-Learning__. SARSA is an _on-policy_ temporal difference approach where a policy is a state-action pair, that is, each state defines the action to be taken. Q-Learning is an _off-policy_ temporal difference approach, very similar to SARSA. However, Q-Learning methods do not follow a policy to define which is the next action to be taken, but instead chooses the next action using a greedy policy, by always taking the action that gives the best reward at that moment.

---

On this post I went over the four main learning approaches used in Machine Learning by giving a quick overview of each and giving simple examples of when they are used. On my next post I will go over other learning strategies that are commonly used in Machine Learning. These learning strategies are complementary to the ones described in this post and often define a subset of methods within these.
