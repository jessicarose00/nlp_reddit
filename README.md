# Web APIs & Classification

### Problem Statement
Will technology save the world? To what extent can technological innovation support long-term environmental sustainability? The objective of this research is to see whether classification models can accurately predict the origin of text posts from the environment and technology subreddit groups. We seek to understand whether conversations about technology are incorporating environmental threats and solutions.

## Executive Summary
This study involves data acquisition, natural language processing, and classification models to understand the degree to which public discourse on technology touches on topics related to the environment. Websites such as Reddit, a social news aggregation and discussion forum, are excellent sources of data where natural language processing and machine learning tecniques can be applied to better understand these phenomena.

### [Data Wrangling and Acquisition]()
The [pushshift.io](https://pushshift.io/) API was used to scrape public posts from the [r/environment](https://www.reddit.com/r/environment/) and [r/technology](https://www.reddit.com/r/technology/) subreddit groups. Roughly 5,455 posts were included. The data was cleaned to remove HTML code, punctuation, null values, duplicates and any text that was not composed of letters. The two subreddits were not assessed for cross posting (identical posts on both subreddits) due to the distinct nature of the topics under investigation. An initial exploratory analysis indicated a much higher character count on the posts from r/environment.

### [Natural Language Processing]()
After the text data was cleaned, natural language processing techniques including tokenization and stemming were used to break the text data into words. Stemming is a form of shortening words so we can combine similar forms of the same word.

### [Classification Modeling]()
NLP techniques combined with machine learning allow us to derive meaning from the text. Three classification models were used in this analysis: 
- Logistic Regression
- Multinomial Naive Bayes 
- Random Forest 
These models were used in combination with two of Sklearn's feature extraction transformers, Countvectorizer and Tfidfvectorizer. Countvectorizer is valuable because it provides a numeric representation of how often certain words appear, while Tfidfvectorizer is useful for understanding a word's value proportional to its frequency. All three models outperformed the baseline (52.3%) in terms of accuracy.

#### [Data Files]()
posts_raw.csv - original scraped posts from Reddit
posts_clean.csv - cleaned data for modeling

### Conclusions
The baseline accuracy was 52.2%. If we saw accuracy scores lower than the baseline accuracy it would indicate the models perform worse than randomly guessing 52.2% of the posts are coming from the technology subreddit.  

The model with the strongest performance in this analysis was a Logistic Regression model with TfidfVectorizer. The model achieved a training score of 92.9% and a testing score of 92.5%. We started with the Logistic Regression model because it is easy to interpret and can indicate which variables are considered. However, when looking at the accuracy scores, it turns out this actually was the best classifier. Given 92% of the model's predictions were correct, there doesn't appear to be a significant overlap in discourse between the environment and technology subreddits. 

It is also valuable to take into account the sensitivity and specificity measures. In this scenario, sensitivity (true positive rate) measures the proportion of technology posts that are correctly identified by the model, since technology is the positive class. Specificity (true negative rate) measures the proportion of environmental posts that are correctly identified by the model, since environment is the negative class. 

Returning to our models, the Logistic Regression model with Countvectorizer acheived the highest sensitivity score. It was strongest at predicting the positive class and of all the models, had the fewest false negative results.

### Future Analysis
The next stage of analysis will focus on a few items:
**Stopwords**: The models indicated that nltk's stopword list was a better parameter than Sklearn's stopword list. Future work could focus on expanding this list to include additional words that aren't particularly insightful to the analysis.
**Sentiment Analysis**: Deeper analysis here might yield notable results. The ability to classify text as either having positive or negative sentiment could be interesting in the context of discourse on technology.
**Hyperparameter Tuning**: Additional tuning would improve model performance. This is particularly apparent with the Random Forest model where we saw a training score of 99.7% with a lower test score and some of the best hyperparameters were indicative of overfitting.
