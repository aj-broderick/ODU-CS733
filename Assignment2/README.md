<div align="center">
  
<img src="https://www.odu.edu/sites/default/files/logos/univ/png-72dpi/odu-sig-noidea-fullcolor.png" style="width:225px;">

</div>

# CS 733 - Natrual Language Processing Assignment 2

## Multi-class Sentiment Analysis (SA)
&emsp; This project was developed for Old Dominion Univeristy (ODU) CS 733 Natural Language Processing in Fall 2024. The code was developed to read through a compilation of 1.6million tweets, from Kaggle dataset [Sentiment140 dataset with 1.6 million tweets](https://www.kaggle.com/datasets/kazanova/sentiment140), create various language models and attempt to predict if the tweet had a positive or negative sentiment.

## Getting Started
&emsp; A majority of the packages that were used are common packages (i.e pandas, mayplotlib), however there are a few things to nore before using the code

### Prerequisites

#### General Natural Language Processing
&emsp; To process the text data to be run through the models, it needs to be cleaned and To acoomplish this, two modules from nltk need to be downloaded. These include `punkt` , `stopwords` and `wordnet`. These modules are critical to the overall program, and without them the tokenization of text data cannot be done, and the program will fail.
```
from nltk import word_tokenize 
nltk.download('punkt') 
from nltk.corpus import stopwords 
nltk.download('stopwords')
from nltk.stem import WordNetLemmatizer
wnl = WordNetLemmatizer()
nltk.download('wordnet')
```
#### Handling Twitter Handles 
&emsp; Since the primary dataset worked with tweets, an additional library was also called that handled the handles that were present in the tweets themselves. To remove the handles, which removes a lot of the noise from the overall dictionary of words to analyze, the `TweetTokenizer` from the `nltk.tokenize` is used. 
```
from nltk.tokenize import TweetTokenizer
tokenizer = TweetTokenizer(strip_handles=True)
```

&emsp; Below are some examples highlighting how anytime there is the @, which denotes the twitter handle, it is ignored and removed from the final tokenized list of words.
| *id*    | *text*    | *tokenized text* |
| -------- | ------- | ------- |
| 1467810917  | @Kenichan I dived many times for the ball. Managed to save 50% The rest go out of bounds  | 	[I, dived, many, times, for, the, ball ,. , Managed, to, save, 50, %, The, rest, go, out, of, bounds]| 
| 1467811193  | @nationwideclass no, it's not behaving at all. i'm mad. why am i here? because I can't see you all over there.  | 	[no, , , it's, not, behaving, at, all, ., i'm, mad, ., why, am, i, here, ?, because, I, can't ,see, you, all, over, there, .]| 


#### Vector Creation

```
from sklearn.feature_extraction.text import TfidfVectorizer
```

#### Model Evaluation

```
from sklearn.metrics import classification_report
from sklearn.metrics import confusion_matrix
```

## Usage

### Corpus Input
&emsp; As mentioned, the code was developed utilizing a large set of tweets f. This dataset can be found on [Kaggle](https://www.kaggle.com/datasets/ankurzing/sentiment-analysis-for-financial-news/data) if the data needs to be inspected if trying to replicate initial pass of the model. Because of this the model makes specific reference to this one dataset and alterations would need to be made to apply to a different corpus set.\
&emsp; An example of needed alterations include any time that `data['sentiment']` or `data['newsheadline']` are called:
```
#Create training and testing datasets
X_train, X_test = train_test_split(data['newsheadline'], test_size=0.2, random_state=42, stratify=data['sentiment'])
```

### Outputs
&emsp; Once the code is run, it creates, trains and evaluated A Naives Bayes and Logisitic Regression model and gerenates a two main pieces of information for each mnodel be analyzed. These include:
* Perfomance Metrics 
* Confusion Matrix


