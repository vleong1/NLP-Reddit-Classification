# Project 3: Classifying Subreddits with NLP by Veronica Leong

### OVERVIEW

### Table of Contents:
- Executive Summary
- Problem Statement
- Data Sources
- Data Dictionary
- Conclusion
- Recommendations
- Future Project Refinements

### Executive Summary

Are you looking for ways to improve your diet or thinking about trying the hot ketogenic diet millenials are obsessing over? **r/Nutrition** and **r/Keto** are two popular subreddits, with over 1.5 million members each. r/Nutrition focuses more on nutrition science, macro/micro nutrients, health supplements, and overall diets, whereas r/Keto is specific to the ketogenic diet - thoughts, experiences, and keto lifestyle advice.

Using Pushshift's API and NLP, we gathered subreddit data to build different classification models to determine which model would be the best at classifying the origin subreddit of the submissions text.

### Problem Statement

How can we determine the subreddit of a new post based on the text of its Submission, using classification modeling?

### Data Sources
- [Keto Subreddit](https://www.reddit.com/r/keto/)
- [Nutrition Subreddit](https://www.reddit.com/r/nutrition/)
- [Pushshift API](https://github.com/pushshift/api)

### Data Dictionary
|Feature|Data Type|Dataset|Description|
|---|---|---|---|
|**subreddit**|*object*|nutrition_subs / keto_subs CSV|Specific group of posts dedicated to a specific topic| 
|**selftext**|*object*|nutrition_subs / keto_subs CSV|Text of subreddit submission post| 
|**title**|*object*|nutrition_subs / keto_subs CSV|Title of subreddit submission post|

### Conclusion
The best performing model was **Logistic Regression, used with CountVectorizer**. This model can classify the subreddit of Submission posts with 91% accuracy, exceeding our baseline accuracy score of 55%. The parameters that performed best for this model included English stop_words, with additional irrelevant custom stop words (e.g. "'ve", "really", "just"), max_features of 1000, and an ngram_range of (1,2). Compared to the other models that were tested, this model had the highest True Negatives and the lowest False positives. Additionally, the lowest False positives led to the highest precision scores amongst the models tested. This model also had the highest f1-score.

The top 5 words within a selftext that best distinguished r/Nutrition submission posts included 'eat', 'food', 'protein', 'fat', 'calorie'. The top 5 words within a selftext that best distinguised r/Keto Submission posts include 'keto', 'eat', 'weight', 'carb', 'start'. Despite 'eat' and 'diet' being present in both subreddits, majority of the top words from the combined datafram of r/Nutrition and r/Keto derived from r/Keto, as that subreddit had almost twice as many top 10 common words, compared to r/Nutrition.

When comparing each model's accuracy score against one another, the Multinomial Naive Bayes models scored the lowest, followed by Random Forest Classifier, and finally, the Logistic Regression models performed the best. Additionally, comparing each models' confusion matrices, both Naive Bayes CountVectorizer + TfidfVectorizer models predicted the lowest number of True Positives and almost twice as many False Negatives, resulting in the lowest precision, recall, and f1-score scores of the models tested.

### Recommendations
- Lemmatize words prior to analyzation so that the model doesn't count instances of the root word ('eat', 'eats', 'eating') separately. Lemmatizing would also optimize the model in terms of finding different patterns of words.
- Look at different ngram_ranges to see what patterns of words occur the most frequent so that the model can train on those patterns.

### Future Project Refinements
- Look at other features, such as 'comments', or 'title'
- Look at a combination of features for analyzation
- Build and evaluate additional models (KNearestNeighbors, DecisionTree)
