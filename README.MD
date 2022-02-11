# Overview

The purpose of Natural Language Processing project was to develop a model that could process the text of news articles and classify them into categories based on their content. 

A business case for this task is that an NLP model can make the classification of articles and more efficient than manually classifying them. 



# About the Data

The data consists of several thousand articles published by the news agency Reuters in 1987. Articles seem to be about commodities and related business topics. They were classified into 135 topics that in the data are represented by keywords such as *gold*, *linseed*, and *rubber*. 

Some articles have been assigned more than one topic, while some haven’t been assigned any topic. 

For this project, I focused on the topic *earn*, short hand for articles about earnings. 



# Process

## Data Preparation

- The data was provided as 22 files in the `sgm` format. Each file contained 1,000 text articles marked up with HTML tags.

- I used Beautiful Soup to assist with reading the files and extracting the article content and their assigned topics.
- Because for the purpose of this project, I was only interested in the *earn* topic, all topics were reassigned as either:
  - *earn* – meaning it was at least one of the assigned topics
  - *other* – meaning earn was not one of the assigned topics
  - *blank* – meaning no topic was assigned 

## Exploratory Data Analysis

There were 22,000 articles included in the dataset. Of the three topic categories:

- 18.3% - earn
- 34.2% - other
- 47.5% - blank

![image-20220211162403926](https://github.com/halpert3/reuters-nlp/blob/master/images/image-20220211162403926.png)



### Most common words in articles in the *earn* category

![image-20220211162509881](https://github.com/halpert3/reuters-nlp/blob/master/images/image-20220211162509881.png)



### Most common words in the *other* category

![image-20220211162644301](https://github.com/halpert3/reuters-nlp/blob/master/images/image-20220211162644301.png)

### Most common words in the *blank* category

![image-20220211162716309](https://github.com/halpert3/reuters-nlp/blob/master/images/image-20220211162716309.png)

## Data Preparation

- Tokenized the text – split articles into lists of lowercase words, removed numbers, stripped punctuation but reserved angle-bracketed company symbols (“&lt; CH >”)
- Removed stopwords like “the” and “if”
- Lemmatized words (“banks” → “bank”)
- Separated data into training set to train model and testing set to verify performance 
- Vectorized data – transformed words into their numerical frequencies



# Modeling

## Baseline Modeling

- Ran five different baseline models (Multinomial Naïve Bayes, Random Forest, Decision Tree, KNN, XGBoost)
- In scoring, ssed recall as the primary metric since the classes were imbalanced, and false positives weren’t concerning
- Looked for similar results between training and test results to minimize overfitting



## Model Refinement

- Built pipelines to experiment with various parameters for:
  - two vectorization techniques (Count Vectorizer and TF-IDF)
  - Decision Tree, which was the best baseline model
- Experimented with variations on the dataset’s topics:
  - *earn*, *other*, and *blank* (3 topics)
  - *earn* and *other*, merging *other* and *blank* together (2 topics)
  - *earn* and *other*, dropping all articles categorized as *blank* (2 topics)



## Favored Model

- The “winning” Decision Tree model, using the TF-IDF vectorizer, classified topics 100% correctly with minimal overfitting

- The *blank* topics were eliminated entirely for this model.

![image-20220211163637911](https://github.com/halpert3/reuters-nlp/blob/master/images/image-20220211163637911.png)



# Next Steps

### Develop More Robust Models

This project only classified articles into two topics, *earn* and *other*. Ideally, a model could classify articles into any topic. 

### Improve Data

The README included with the dataset had questions about why so many articles were unclassified, questions which I share. It seems many of these articles could have had topics, and assigning them topics would improve data quality and help with modeling. 

