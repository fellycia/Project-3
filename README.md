# Project-3
Web APIs and Classification

## Problem Statement
Previously, Reddit had a subreddit called r/SingaporeAndJapan that welcomed discussion on both Singapore and Japan topics. Due to a disagreement between moderators, the subreddit was decided to be split in r/Singapore and r/Japan. The respective moderators of the new subreddits are still keen to migrate the old posts from the combined subreddit into the new individual subreddits for archiving purposes. Hence, they have engaged our services to archive the old posts into the appropriate new subreddits.

We aim to create a model that can accurately predict which of the two subreddits a given post originated from using new posts scraped from the two subreddits. Accuracy score is used to compare between models.

## Executive Summary

### Data Collection:
A total of 1801 distinct posts were collected from both subreddits using Reddit's API.
The distribution betweeen the 2 subreddits was balanced. 54% belonged to Singapore, while 46% belonged to Japan.
Data Cleaning:

### Removal of duplicated post
Combined selftext and title into a new column
Removal of unwanted symbols and signs
Removal of non-alpha text
Switching to lower case
Tokenization
Lemmatization
Removal of stopwords
Removal of top common words from both subreddits and misclassified words

### Modeling:
Logistic Regression, Multinomial Naive Bayes, Support Vector Machine and Random Forest were used in this report to build a binary predictor.
For each model, both Count Vectorizer and TF-IDF Vectorizer were tried out to determine which suited the estimator better.
Grid searching was used for each pipe to find the optimal hyperparameters.
Using the best cross-validated model, its performance was determined by scoring it on the train and test dataset.
Multinomial Naive Bayes was the best.

### Conclusions:
All models beat the baseline accuracy of 54%, hence they served as a better option compared to no model. However, they can be further improvements made, like exploring other columns apart from selftext and title of the subreddits, using more complex POS tagging with lemmatization and analyse misclassification words from other models. Multinomial Naive Bayes prove to serve as the best model to best accurately archive the old posts into the new subreddits of Singapore and Japan.

## Data Dictionary
|Feature|Type|Dataset|Description|
|---|---|---|---|
|**ylabel**|*integer*|train/test|Binary classification of subreddit. 1 for singapore and 0 for japan| 
|**selftext**|*object*|train/test|Content in the body of individual post|
|**title**|*object*|train/test|Title of each post| 
|**combined**|*object*|train/test|Combination of the selftext and title| 
|**pos_lem**|*object*|train/test|List of tokenized words after lemmatizing| 
|**col_final**|*object*|train/test|Cleaned post, removal of stopwords, used to fit into the model| 

## Evaluations:
There is a close fight between Multinomial Naive Bayes (NB)(Pipe3) and Support Vector Classifier (SVC)(Pipe 6). NB had a slightly higher cross-validated best score, which was the model's ability to generalize on unseen data. Both Pipe 3 and Pipe 6 had the least overfitting on train dataset compared to the test dataset. They also chose not to include the vectorizer 'english' stopwords as a hyperparameter. For pipe 4, although it has the best cross-validation score on unseen data, the train and test score showed that the model was more overfitted on the train dataset.
All models beat the baseline accuracy of 0.54. Hence, they are all still better than average.

Another discovery was that for pipes using Count Vectorizer, if they do not include the vectorizer's 'english' stopwords as their hyperparameters, they would produce more generic words as predictive features, while TF-IDF does not seem to be affected by it. TF-IDF has the abilty to reduce the importance of the common generic words but not count vectorizer.

The Multinomial Naive Bayes model was the most outstanding and should be used to archive the old posts into the appropriate new subreddits. Compared to the rest, it handled unseen data well and balanced the tradeoff between bias/variance the best among the eight pipes. It is possible to use only raw text as input for making predictions. However if given more time, exploring new features apart from selftext and title could help. Also, more exploration on complex POS tagging and misclassified words from other models could be ventured into.
