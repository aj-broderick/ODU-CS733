<div align="center">
  
<img src="https://www.odu.edu/sites/default/files/logos/univ/png-72dpi/odu-sig-noidea-fullcolor.png" style="width:225px;">

</div>

# CS 733 - Natrual Language Processing Assignment 1

## N-Grams
&emsp; This project was developed for Old Dominion Univeristy (ODU) CS 733 Natural Language Processing in Fall 2024. The code was developed to read through a list of financial new headlines, generate the n-grams, and then train various models to determine which model performed the best at generalizing unseen data. 

## Getting Started
&emsp; A majority of the packages that were used are common packages (i.e pandas, mayplotlib), however there are a few things to nore before using the code

### Prerequisites
&emsp; To process the text data to be run through the models, it needs to be cleaned and To acoomplish this, two modules from nltk need to be downloaded. These include `punkt` and `stopwords`. Thse modules are critical to the overall program, and without them the tokenization of text data cannot be done, and the program will fail.\
```
from nltk import word_tokenize 
nltk.download('punkt') 
from nltk.corpus import stopwords 
nltk.download('stopwords') 
```

## Usage

### Corpus Input
&emsp; As mentioned, the code was developed utilizing a set of financial news headlines from the perpective of a retail investor. This dataset can be found on [Kaggle](https://www.kaggle.com/datasets/ankurzing/sentiment-analysis-for-financial-news/data) if the data needs to be inspected if trying to replicate initial pass of the model. Because of this the model makes specific reference to this one dataset and alterations would need to be made to apply to a different corpus set.\
&emsp; An example of needed alterations include any time that `data['sentiment']` or `data['newsheadline']` are called:
```
#Create training and testing datasets
X_train, X_test = train_test_split(data['newsheadline'], test_size=0.2, random_state=42, stratify=data['sentiment'])
```

### Perplexity
&emsp; The primary output of the code includes the ***perplexity*** of the different models, when applied to the unseen data from the training data. When interpreting the output of the perplexity, the lower the perplexity of the model, the better the model was at understanding the unseen data. Perplexity was calculated using the following equation:

<div align="center">

$$ perplexity(W) = \sqrt[N]{\prod_{i=1}^{N}\frac{1}{P(w_{i}|w_{1},\dots,w_{i-1})}}$$

</div>

### Outputs
&emsp; Once the code is run, it gerenates a handful of outputs and if running without any changes to the corpus. These outputs include:
* Barchart of Top 10 unigram, bigram & trigrams from the input corpus
* Perplexity for the models:
    * N-Gram Model
    * Laplace Smoothed N-Gram Model
    * Linear Interpolated N-Gram Model



