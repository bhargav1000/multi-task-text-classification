Disaster Tweet Classification <!-- omit from toc -->
==============================

A BERT-based multi-task model to classify whether a Tweet is a Disaster or not and also to classify the Sentiment of the Tweet. 


- [Summary](#summary)
- [Data Sources](#data-sources)
- [Results](#results)
  - [Method 1](#method-1)
  - [Method 2](#method-2)
  - [Method 3](#method-3)
- [Team Members](#team-members)

Summary
------------
Developed and trained a BERT-based multi-task model to classify tweets whether they refer to a real disaster or not. The multi-task model leverages a separete tweet dataset with sentiment labels to help in the disaster classification task. This is achieved by utilizing a neural network architecture with two heads, one for disaster classification (Task 1) and one for sentiment classification (Task 2). A weighted loss (utilizes adversarial training), which weights and sums the losses of the two classification tasks is ultimately used during back propagation to incorporate sentiment information during training. The weights of the loss function are tuned using Bayesian Optimization which maximizes the F1 score of Task 1.

This repository also includes two alternative strategies in predicting disaster tweets but results are not reported.

Data Sources
------------
1. [Disaster Tweets Prediction Competition](https://www.kaggle.com/competitions/nlp-getting-started/overview)<br>
Labels: 1, if tweet is about a real disater, 0 otherwise
1. [Twitter Tweets Sentiment Dataset](https://www.kaggle.com/datasets/yasserh/twitter-tweets-sentiment-dataset)<br>
Labels: Negative, Neutral or Positive Sentiment


Results
------------
 ### Method 1 ###
 Minimizing separate loss functions for Task 1 and Task 2 during training.
| Task                        | F1 Score | Accuracy |
| :-------------------------- | -------: | -------: |
| 1. Disaster Classification  |   75.83% |   77.60% |
| 2. Sentiment Classification |   61.00% |   59.53% |

**Confusion Matrix for Task 1**

![t1_tm1](/notebooks/t1_tm1.png)

**Confusion Matrix for Task 2**

![t2_tm1](/notebooks/t2_tm1.png)


### Method 2 ###
Minimizing a combined weighted loss, $\lambda_1l_1 + \lambda_2l_2$  where $\lambda_1$ and  $\lambda_2$ are positive scalar weights, and $l_1$ and $l_2$ are the task-specific loss functions. Uses $\lambda_1=\lambda_2=0.5$

| Task                        | F1 Score | Accuracy |
| :-------------------------- | -------: | -------: |
| 1. Disaster Classification  |   70.94% |   79.77% |
| 2. Sentiment Classification |   62.00% |   62.90% |

**Confusion Matrix for Task 1**

![t1_tm2](/notebooks/t1_tm2.png)

**Confusion Matrix for Task 2**

![t2_tm2](/notebooks/t2_tm2.png)


### Method 3 ###
Same method as Method 2, but both lambdas tuned using Bayesian Optimization by optimizing the model's disaster classification F1 score (Task 1) which yielded $\lambda_1 = 0.6342942588575995$, $\lambda_2= 0.9743182933953305$. 

After tuning, inference was made on unlabeled test tweets and predictions were submitted to the [Disaster Tweets Prediction Competition](https://www.kaggle.com/competitions/nlp-getting-started/overview).

| Task                    | F1 Score      |
| :---------------------- | ------------: |
| Disaster Classification |        80.00% |

Team Members
------------
- Bhargav Sagiraju
- Xuan Wen
- Jiaqi Hu
