SadedeGel prebuilt models are built to extend capabilities of sadedegel library 
on common NLP tasks we encounter every day. Such as sentiment analysis, profanity detection.

Open source prebuilt models are not designed to achieve state of the art accuracies. They rather provide a good starting 
point by training sklearn based limited memory (`partial_fit` using micro batches) models with a single pass over training data.

If you need access for our state of the art models, please reach us at info@sadedegel.ai

### Maintainers
* [@husnusensoy](https://github.com/husnusensoy) contributes **Turkish News Text Classification**
* [@dafajon](https://github.com/dafajon) contributes **Telco Sentiment Classification**, **Tweet Sentiment Classification**
* [@askarbozcan](https://github.com/askarbozcan) contributes **Tweet Profanity Classification**
* [@ertugruldemir](https://github.com/ertugrul-dmr) contributes **Turkish Movie Review Sentiment Classification**, **Turkish Customer Reviews Classification**
* [@irmakyucel](https://github.com/irmakyucel) contributes **Product Sentiment Classification**

### Turkish News Text Classification

Classifier assigns each Turkish text into one of 12 categories (`sadedegel.dataset.tscorpus.CATEGORIES`)
by using a sadedegel including pipeline

#### Loading model

```python
from sadedegel.prebuilt import news_classification

model = news_classification.load()

y_pred = model.predict([''])
```

To convert class ids to class labels use

```python
from sadedegel.dataset.tscorpus import CATEGORIES

y_pred_label = [CATEGORIES.index(_y_pred) for _y_pred in y_pred]
```

#### Accuracy

Current prebuilt model has an average class prediction cv-3 accuracy of `0.812`

### Turkish Tweets Profanity Classification

This classifier assigns Turkish tweets to one of `OFF`, `NOT` classes based on whether a tweet contains a profane language or not, by using a `sadedegel`pipeline.

#### Load Model
```python
from sadedegel.prebuilt import tweet_profanity

model = tweet_profanity.load()  # Load latest version

y_pred = model.predict(['bir takım ağza alınmayacak sözcükler.'])
```
To convert predictions to profanity label by class mapping:

```python
from sadedegel.prebuilt.tweet_profanity import load, CLASS_VALUES
model = load()

y_pred = model.predict(['bir takım ağza alınmayacak sözcükler.'])

y_pred_value = [CLASS_VALUES[_y_pred] for _y_pred in y_pred]
```

#### Accuracy

Current prebuilt tweet profanity model has an **macro-F1** score of ` 0.7535` on test set.
> Best model in [SemEval-2020 Task 12](https://arxiv.org/pdf/2006.07235.pdf) has `0.8258` accuracy

### Turkish Tweet Sentiment Classification
Classifier assigns each Turkish tweet texts into two classes ('POSITIVE', 'NEGATIVE') by using sadedegel built-in pipeline.

#### Loading and Predicting with the Model:
```python
from sadedegel.prebuilt import tweet_sentiment
# We load our prebuilt model:
model = tweet_sentiment.load()

# Here we enter our text to get sentiment predictions.
y_pred = model.predict([])
```
#### Accuracy

Current prebuilt model has 
* 3-fold cross validation F1 macro score of `mean 0.8587, std 0.0066)`.
* 5-fold cross validation F1 macro score of `mean 0.8613, std 0.0035)` 

### Turkish Movie Review Sentiment Classification

Classifier assigns each Turkish movie review text into two classes ('NEGATIVE', POSITIVE') by using sadedegel built-in pipeline.

#### Loading and Predicting with the Model:

```python
from sadedegel.prebuilt import movie_reviews
# We load our prebuilt model:
model = movie_reviews.load()

# Here we feed our text to get predictions:
y_pred = model.predict(['süper aksiyon, tavsiye ederim'])

# You can check original test results on holdout set:
movie_reviews.evaluate()
```
#### Accuracy

Current prebuilt movie review model has a **macro-F1** score of `0.8258` on holdout test set model never seen before.

### Telco Brand Tweet Sentiment Classification

Classifier assigns each tweet mentioning the telecom brand into three classes ('olumlu', olumsuz', 'notr') by using sadedegel built-in pipeline.

#### Loading and Predicting with the Model:

```python
from sadedegel.prebuilt import telco_sentiment
# We load our prebuilt model:
model = telco_sentiment.load()

# Here we feed our text to get predictions:
y_pred = model.predict(['Magma tabakasından bile çekiyor helal olsun valla.'])

# You can check original test results on holdout set:
telco_sentiment.evaluate()
```

#### Accuracy

Current prebuilt open source telco sentiment model has a **accuracy** score of `0.6925` (**macro-F1** score of `0.6871`) on test set.

Comparable [benchmark](https://ieeexplore.ieee.org/document/8554037/) models has  
* `0.6925` **accuracy** score (convolutional neural networks fed with char ngrams)
* `0.66` **accuracy** score (classical ML approach fed with bag-of-words)
on the hold-out set.


### Turkish Customer Reviews Classification

Classifier assigns each Turkish customer review text into 32 classes by using sadedegel built-in pipeline.

#### Loading and Predicting with the Model:

```python
from sadedegel.prebuilt import customer_reviews_classification

# We load our prebuilt model:
model = customer_reviews_classification.load()

# Here we feed our text to get predictions:
y_pred = model.predict(['odalar çok kirliydi'])

# You can also get probabilities with:
y_probs = model.predict_proba(['odalar çok kirliydi'])

# You can check original test results on holdout set:
customer_reviews_classification.evaluate()

# You convert class id's back to labels by importing:
from sadedegel.dataset.customer_review import CLASS_VALUES

# And simply map them to get the converted string list:
y_pred_label = [CLASS_VALUES[idx] for idx in y_pred]
```

#### Accuracy
Current prebuilt customer review classification model has a macro-F1 score of `0.851` on holdout test set model never seen before.

If you want to compare benchmark results:
> The model on [Kaggle](https://www.kaggle.com/savasy/multiclass-classification-data-for-turkish-tc32) where we got dataset from has F1 score of `0.84`.

###  Hotel Sentiment Classification

Using sadedegel built-in pipeline, the prebuilt model for hotel review sentiment classification assigns text into two
classes, `0` and `1`, for `NEGATIVE` and `POSITIVE` sentiments consecutively.

#### Loading and Predicting with the Model:

```python
from sadedegel.prebuilt import hotel_sentiment

# We load our prebuilt model:
model = hotel_sentiment.load()

# Here we feed our text to get predictions:
y_pred = model.predict(['otel çok temiz, çalışanlar güler yüzlü, yemekler fena değil'])

# You can also get probabilities with:
y_probs = model.predict_proba(['otel çok temiz, çalışanlar güler yüzlü, yemekler fena değil'])

# You can check original test results on holdout set:
hotel_sentiment.evaluate()

# You convert class id's back to labels by importing:
from sadedegel.dataset.hotel_sentiment import CLASS_VALUES

# And simply map them to get the converted string list:
y_pred_label = [CLASS_VALUES[idx] for idx in y_pred]
```

#### Accuracy
Current prebuilt hotel sentiment classification model has an accuracy of `0.863` on holdout test set. Comparable
benchmark results found [here](https://journals.tubitak.gov.tr/elektrik/issues/elk-19-27-3/elk-27-3-16-1808-189.pdf) 
where their results with different classifiers are given below.

| Classifier|Method| Accuracy |
|---------|--------|--------|
| NB      | ML     | 83.80% |
|         | Hybrid | 89.98% |
| SVM     | ML     | 91.14% |
|         | Hybrid | 91.96% |
| J48     | ML     | 86.10% |
|         | Hybrid | 88.96% |
| Lexicon |        | 78.88% |


#### Relevant Links
* [SentiWordNet for New Language: Automatic Translation Approach](https://ieeexplore.ieee.org/document/7907484)
* [Turkish Sentiment Analysis Dataset](http://humirapps.cs.hacettepe.edu.tr/tsad.aspx)
* [A hybrid sentiment analysis method for Turkish](https://journals.tubitak.gov.tr/elektrik/issues/elk-19-27-3/elk-27-3-16-1808-189.pdf)

### Online Food Delivery Review Sentiment Classification
Classifier assigns each Turkish review texts into two classes ('NEGATIVE', 'POSITIVE') by using sadedegel buil-in pipeline.

#### Loading and Predicting with the Model:
```python
from sadedegel.prebuilt import food_reviews
# We load our prebuilt model:
model = food_reviews.load()

# Here we enter our text to get sentiment predictions.
y_pred = model.predict(['sıradan bir yemek yorumu'])

# You can also get probabilities with:
y_probs = model.predict_proba(['sıradan bir yemek yorumu'])

# You can check original test results on holdout set:
food_reviews.evaluate()

# You can conver class id's back to labels by importing:
from sadedegel.dataset.food_review import CLASS_VALUES

# And simply map them to get converted string list:
y_pred_label = [CLASS_VALUES[idx] for idx in y_pred]
```

#### Accuracy
Current prebuilt food review classification model has a macro-F1 score of `0.896` on holdout test set model never seen before.


### Online Food Delivery Review Sentiment Classification (Multi Output)
If you want to get separate sentiment per category (['speed', 'service', 'flavour']), you can use `multi output` version of our model instead:

```python
from sadedegel.prebuilt import food_reviews_multioutput
# We load our prebuilt model:
model = food_reviews_multioutput.load()

# Here we enter our text to get sentiment predictions.
y_pred = model.predict(['sıradan bir yemek yorumu'])

# Code above will return Mxn array where M is n_samples,
# n is n_outputs, ['speed', 'service', 'flavour'] in our case.

# You can also get probabilities with:
y_probs = model.predict_proba(['sıradan bir yemek yorumu'])

# Code above will return list of arrays;
# where the length of list is n_outputs;
# and each array is (M, n_classes) for that particular output.

# You can check original test results on holdout set:
food_reviews_multioutput.evaluate()
```
#### Accuracy
Current prebuilt multi output food review classification model has a macro-F1 score of `0.865` on holdout test set model never seen before.


