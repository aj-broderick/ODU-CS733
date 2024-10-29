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
&emsp; To process the text data to be run through the models, it needs to be cleaned and To accomplish this, two modules from nltk need to be downloaded. These include `punkt` , `stopwords` and `wordnet`. These modules are critical to the overall program, and without them the tokenization of text data cannot be done, and the program will fail.
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
&emsp; TF-DIF was chosen as the feature extraction method for the sentiment analysis. This was done over a bag of words approach since it's a little more nuanced in the way that each of the words is given a weight as opposed to simply counting the words. In a model of this size, the words that have the higher frequency will have a larger impact to the end output.

```
from sklearn.feature_extraction.text import TfidfVectorizer
```

## Usage

### Corpus Input
&emsp; As mentioned, the code was developed utilizing tweets from a preprocssed file, and has a set number and ordering of columns. Because of this the model makes specific reference to this one dataset and alterations would need to be made to apply to a different corpus set.\
&emsp; An example of needed alterations include any time that `df['text']` or `df['target']` are called:
```
#Create training and testing datasets
y = df['target']

vectorizer = TfidfVectorizer(max_features = 228117)
X_vector = vectorizer.fit_transform(df['text'])
```

### Outputs
&emsp; Once the code is run, it creates, trains and evaluated A Naives Bayes and Logisitic Regression model and gerenates a two main pieces of information for each mnodel be analyzed. These include:
* Perfomance Metrics 
* Confusion Matrix


