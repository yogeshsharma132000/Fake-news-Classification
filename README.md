# Fake-news-Classification
using Multinomial Naive Bayes Classifier and TF-IDF Vectorizer

# ABSTRACT    
This Project comes up with the applications of NLP (Natural Language Processing) techniques for detecting the 'fake news' (misleading news stories that comes from the non-reputable sources).Only by building a model based on a (Term Frequency Inverse Document Frequency) tfidf  matrix, (word tallies relative to how often they’re used in other articles in your dataset) can only get you so far. But these models do not consider the important qualities like word ordering and context. 

This project includes assembling a dataset of both fake and real news and employ a Naive Bayes classifier in order to create a model to classify an article into fake or real based on its words and phrases.

# OBJECTIVE
The main objective is to detect the fake news, which is a text classification problem. It is needed to build a model that can differentiate between “Real” news and “Fake” news

## REQUIREMENTS
1. Python
2. Numpy
3. Pandas
4. newspaper 
5. json
6. NLTK
7. sklearn 

## Directories
1. data_cleaning 
    1.1 cleaning_helper.py
2. notebooks
    2.1 read_json_and_clean.ipynb
    2.2 train_test_model.ipynb
3. savedFiles
    3.1 cleaned_df.pkl
    3.2 dirty_df.pkl
4. scrapper
    4.1 NewsPapers.json
    4.2 scraped_articles.json
    4.3 scrapper.py
5. to extract fake news sites
    5.1 fakenewssites.csv
    5.2 forfakenews.ipynb
    
## Various Stages 
1. Data Collection
2. Data preprocessing 
3. Preprocessing the Text
4. Model selection
5. Classification
6. Model Evaluation
    
    
### First Step - DATA COLLECTION

First of all find the reliable news sources for 'Real News' and unreliable news sources to gather 'Fake News' .
Create a json file "NewsPapers.json" Put the links of all reliable sources first and then put links for fake news.
Build a web scrapper for scrapping news articles from the links given in "NewsPapers.json" and store the articles in "scraped_articles.json".

### Second Step - Data preprocessing

After storing the articles in "scraped_articles.json" we have to retrive data from it and build a dataframe out of it.
After building dataframe remove the unwanted columns and extract the wanted features . 
In this case wanted features are - "title" - title of article , "text" - content of the article , "link" - url of the article , "author" - author of the article.
Now we have to label the articles - for articles that are scrapped from real news sources are to be marked with label "0" i.e. "not fake" or real news.
and articles that are scrapped from fake news sources are to be marked with label "1" i.e. "fake news".
Now we have 5 features of the given dataset - title, text, link, author and label.

### Third Step - Preprocessing the Text (or cleaning the text)

In this step we use Data mining techniques or NLP (Natural Language Processing) .
With the help of "cleaning_helper.py" first we have to lowercase all the text and title.
After that we have to remove Stopword (a, and, but, the, or ... etc.) from our text data because stopwords does not provide much information about the text.
After that we need to remove punctuations ('!"$%&\'()*+,-./:;<#=>?@[\\]“”^_~’' etc) and digits also.
At this moment we have 7 features in the dataset - title, text, link, author, label, clean_title and clean_text.
Now save this dataset as "cleaned_df.pkl".

### Fourth Step - Model selection

First we will remove some columns('title','text','label','author','link', 'clean_title') from our dataset because we only need clean_text for our classification .
I created a column called 'fake' by copying the 'label' column.
Now we have only 2 columns in our dataset - 'clean_text' and 'fake'.

Now using train_test_split() method of model selection we have to split the given dataset into "Training Dataset" (80%) and "Test Dataset" (20%).
Now using pipelining we will create 4 models to check the performance and select the best Model.
#### Model 1 - Countvectorizer and MultinomialNB
Best score: 0.9128957473013113
Train score 0.9968895800933126
Test score 0.9440993788819876
#### Model 2 - tfidfvectorizer and MultinomialNB
Best score: 0.9175024224806201
Train score 0.9906687402799378
Test score 0.9440993788819876
#### Model 3 - tfidfvectorizer and logistic regression
Best score: 0.8242700862131421
Train score 0.9129082426127527
Test score 0.8385093167701864
#### Model 4 - countvectorizer and LogisticRegression
Best score: 0.919126276896327
Train score 1.0
Test score 0.9254658385093167

##### The best Model on the basis of Best score is tfidfvectorizer and MultinomialNB.

### Fifth Step - Classification

We have to create a TF-IDF vector and transform the clean_text data values into this vector.
Then import MultinomialNB(Naive Bayes Model) from sklearn and build a classifier (in this case named - "nb_body") 
Then fit the tf-idf vectorized data into the Naive Bayes Model(this is the training of classification Model).

### Sixth Step - Model Evaluation

Model evaluation step contains analysis of the trained model by calculating F1 score, Accuracy, precesion and recall value of the model.
I have shown most common spam words and most common ham words with their number of occurance

# Conclusion

The most model to optimize for accuracy in detecting fake news and absurd news uses TfidfVectorizer and MultinomialDB. The optimal parameters for this model are where ngram_range = (1,2) and alpha = 0.1.

Accuracy: 94.41 % Precision: 92.68 % Recall: 86.36 % F1 score: 89.41 %
