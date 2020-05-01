# Web APIs & Classification

### Problem Statement
To what extent can technological innovation support long-term environmental sustainability? The objective of this research is to see whether classification models can accurately predict the origin of text posts from the environment and technology subreddit groups. I seek to understand whether conversations about technology are incorporating environmental threats and solutions.

## Executive Summary
This project uses APIs, natural language processing techniques, and classification models to understand the degree to which public discourse on technology touches on topics related to the environment. Websites such as Reddit, a social news aggregation and discussion forum, are excellent sources of data where natural language processing and machine learning tecniques can be applied to better understand these phenomena.

### [Data Wrangling and Acquisition](https://git.generalassemb.ly/jessicaertel/project_3/blob/master/code/01_Data_Gathering_EDA.ipynb)
The [pushshift.io](https://pushshift.io/) API was used to scrape public posts from the [r/environment](https://www.reddit.com/r/environment/) and [r/technology](https://www.reddit.com/r/technology/) subreddit groups. Roughly 5,455 posts were included. The data was cleaned to remove HTML code, punctuation, null values, duplicates and any text that was not composed of letters. The two subreddits were not assessed for cross posting (identical posts on both subreddits) due to the distinct nature of the topics under investigation. An initial exploratory analysis indicated a much higher character count on the posts from r/environment.

### [Natural Language Processing](https://git.generalassemb.ly/jessicaertel/project_3/blob/master/code/02_NLP._Modeling.ipynb)
After the text data was cleaned, natural language processing techniques including tokenization and stemming were used to break the text data into words. Stemming is a form of shortening words so we can combine similar forms of the same word.

### [Classification Modeling](https://git.generalassemb.ly/jessicaertel/project_3/blob/master/code/02_NLP._Modeling.ipynb)
NLP techniques combined with machine learning allow us to derive meaning from the text. Three classification models were used in this analysis: 
- Logistic Regression
- Multinomial Naive Bayes 
- Random Forest  

These models were used in combination with two of Scikit-Learn's feature extraction transformers, Countvectorizer and Tfidfvectorizer. Countvectorizer is valuable because it provides a numeric representation of how often certain words appear, while Tfidfvectorizer is useful for understanding a word's value proportional to its frequency. All three models outperformed the baseline (51.2%) and achieved >90% accuracy.

#### [Data Files](https://git.generalassemb.ly/jessicaertel/project_3/tree/master/data)
posts_raw.csv - original scraped posts from Reddit  
posts_clean.csv - cleaned data for modeling

### Conclusions
The r/environment and r/technology subreddits were both created in January 2018. At the time this project was completed, the technology subreddit had 8.5 million members compared to 648,000 in r/environment, and a higher number of posts. However, the average length of posts in the technology subreddit is significantly shorter and the most common words clearly have an environmental flavor.

All of the models I attempted indicated overfitting by the high train and lower test scores. The accuracy on test scores hovered just under 94% for almost all of the models. Weakening regularization (C parameter) achieved a higher test score but increased overfitting. Given the high accuracy of the classification predictions, there's no significant overlap in discourse between the environment and technology subreddits. 

It is also valuable to take into account the sensitivity and specificity measures. In this scenario, sensitivity (true positive rate) measures the proportion of technology posts that are correctly identified by the model, since technology is the positive class. Specificity (true negative rate) measures the proportion of environmental posts that are correctly identified by the model, since environment is the negative class. 

The Logistic Regression model with Countvectorizer acheived the highest sensitivity score. It was strongest at predicting the positive class and of all the models, had the fewest false negative results. Again, high sensitivity indicates clear division between the technology and environment posts so there would need to be deeper analysis to determine a relationship between the two topics.

### Future Analysis
The next stage of analysis will focus on a few items:  
**Analyze r/sustainability**: The r/environment and r/technology subreddits are understandably distinct and easily separable. Perhaps looking at a more applied environmental subreddit like r/sustainability could illustrate greater overlap with tech discourse.
**Sentiment Analysis**: Deeper analysis here might yield notable results. The ability to classify text as either having positive or negative sentiment could be interesting in the context of discourse on technology.  

