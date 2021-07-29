# Sentiment Checker Analysis
Author: Albert Aldo - 12albertaldo@gmail.com | [LinkedIn](https://www.linkedin.com/in/albertaldo/) | [GitHub](https://github.com/AlbertAldo)

## Introduction
Sentiment is a computational process in identifying and categorizing opinions in the form of pieces of text, specifically to measure the intent of the creator of the piece of text to a certain topic, can be positive, negative, or neutral. Social media is a place that can be used to submit complaints and positive reviews from customers about the services provided by the company.

## Problems
In times like today, the development of social media is very rapidly and had an impact on an existing business. When word of mouth is carried out by netizens on a business product, it will have a good impact and a bad impact. If the good impact is received, it will make profits for the business company, but if the bad impact is carried out by certain individuals such as for example hate speech on the product, badmouthing the product, insulting the product it will harmful the business company, Therefore it is necessary to have a machine that can assist in filtering negative sentiments that entering our business products.

## Problems Impact
Customer's complaints about the Company Products, Hoax and False Information committed by certain people, and another which can make a bad perception for the public that affect for Company Reputational causing to inflict the business.

If the customer's complaints are relevant to your business products, so your company must have an improvement to give the best services to maintain your customers.

Therefore, The Companies must always be aware of conversations that occur on online platforms, so they can always map public perceptions/sentiments, especially customers, towards the company itself and should be anticipated as early as possible.

So my sentiment detector is useful for your Company, in mapping the sentiment of conversations, especially on social media.

## Goals
Can provide a solution to the problem above by making a machine that can predict a sentence that has a negative or positive connotation, to prevent negative sentences that have an impact on our product business.

# Workflow Project
![Workflow](https://i.imgur.com/u5yGZbV.jpg)

# 1. Data Information

I collected data from [Repo Telematika](https://repo.telematika.org/project/louisowen6_nlp_bahasa_resources/), [Kaggle - Ilhamfp31](https://www.kaggle.com/ilhamfp31/indonesian-abusive-and-hate-speech-twitter-text?select=data.csv), [Rizalespe](https://rizalespe.github.io/Dataset-Sentimen-Analisis-Bahasa-Indonesia/) and I would give an appreciation from this datasets because already has the result of sentiment from the text.

The datasets are combined all from the above source, and it is an Indonesian Text. They are labeled into 1 (Positive Sentiment) and -1 (Negative Sentiment). Assisted with another source such as StopWords Indonesian from nltk, Emoticon and Slang Words from [Repo Telematika](https://repo.telematika.org/project/louisowen6_nlp_bahasa_resources/). This dataset including from Tweets, Instagram Comment, Single Word of Positive and Negative Sentiment Dictionary from [Repo Telematika](https://repo.telematika.org/project/louisowen6_nlp_bahasa_resources/). Using Sastrawi Package for stemming text.

# 2. Data Pre-Processing

I only input the text and the results of the sentiment as the data used. Then I merged all the data and deleted the duplicate text data. The data is ready for processing.

There are a few steps for text processing:
1. Lowering all words from Text
2. Tokenize the sentence from Text
3. Removing all numbers from Text
4. Removing punctuation from Text
5. Removing like user, retweet, http, etc from Text
6. Removing Indonesian stopwords from Text
7. Converting Indonesian slang words from Text
8. Converting emoji into Meaning of the Emoji
9. Using Sastrawi for stemming process
10. Tokenize the stemmed text
11. Removing Indonesian stopwords after stemmed

For full further details Data Processing please refers to :
- [Data Processing - GitHub](https://github.com/AlbertAldo/Sentiment-Checker-Analysis/blob/main/1%20-%20Data%20Processing.ipynb)

I also do Exploratory Data Analysis, for full further details please refers to :
- [Exploratory Data Analysis - GitHub](https://github.com/AlbertAldo/Sentiment-Checker-Analysis/blob/main/2%20-%20Exploratory%20Data%20Analysis.ipynb)

# 3. Modelling & Feature Engineering

Before I enter the modeling stage, I used Pipeline in order to process CountVectorizer and TfidfVectorizer with each other using ngram_range=(1,2) for LogisticRegression, KNN, DecisionTreeClassifier, RandomForestClassifier algorithm.

```
- CountVectorizer:
Pipeline([
    ("prep", CountVectorizer(ngram_range=(1,2)))
])

_________________________________________________

- TfidfVectorizer:
Pipeline([
    ("prep", TfidfVectorizer(ngram_range=(1,2)))
])
```

<hr>

## - Classification

Classification problem is the target of Sentiment from the text. [ML Classification - GitHub](https://github.com/AlbertAldo/Sentiment-Checker-Analysis/blob/main/3%20-%20ML%20Classification.ipynb) 

I did several Algorithms such as :
- LogisticRegression, KNN, DecisionTreeClassifier, RandomForestClassifier as a Base Model.
- LogisticRegression, KNN, DecisionTreeClassifier, RandomForestClassifier with Hyper Parameter Tuning.
- KNN, RandomForestClassifier with Fine Tuning.

After do some development from the models then I choose **RandomForestClassifier with Fine Tuning** for the best algorithm that I found, as follows :

```
n_estimators = 201, max_depth = 21, max_features = 0.1, min_samples_leaf = 4, min_samples_split = 8, random_state=42
```

Which resulted in the following scores :

Data  | Accuracy | Recall | Precision  | F1-Score |
-----|------|------|------|------|
Training RandomForestClassifier Tuned | 0.733   |0.957 | 0.693 | 0.803
Test RandomForestClassifier Tuned | 0.722   | 0.947 | 0.686 | 0.803

# 4. Application

## Sentiment Checker

When a customer makes a comment via social media, there must be a positive or negative sentiment that he gives, if it is a negative sentiment that is given, and it is not a real case, then this sentiment checker will be very useful.

The following picture demonstrates how our Sentiment Checker Model application flows :

### **Positive Sentiment**
![PositiveSentiment](https://i.imgur.com/gKBJ8WM.jpg)

### **Negative Sentiment**
![NegativeSentiment](https://i.imgur.com/fqZPFpA.jpg)

# 5. Conclusion

## - Sentiment Checker
With this model, it can help companies to filter comments from customers who have negative sentiments, so that things can be minimized that affect other customers by looking at these comments. If the negative comments are true in accordance with the company's conditions and the average customer comments negatively too, it can be a warning for future developments.

From this model, it has been considered from the confusion matrix, and focuses on the **Evaluation Matrix Recall**, so that if there are negative sentiment comments the machine will minimize error in guessing it into positive sentiment (**Reducing False Positive**).

<hr>

**Thanks for reading my project! I hope my project useful and inspiring.**
