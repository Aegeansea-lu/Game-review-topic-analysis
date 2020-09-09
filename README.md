# Game-review-topic-analysis
This repository includes scraping raw data from Matacritic and Steam, NLP, topic modeling etc. Contextual topic identification model is implemented. The model is a combination of LDA probabilistic topic assignment and pre-trained sentence embeddings from BERT/RoBERTa.
## Motivation
User reviews play a vital role in product's future improvement and user performance analysis. Large online review websits like Metacritic and Steam have developed well-performed ecosystem of user/player semantic rating, yet there barely exits a satisfying categorization system for the reviews. Despit we can get information as positive or negative regarding to the product, it is meaningful to have a brief view of main topics people paying attention to. I'v been a gamer since childhood and would like to take the chance to practice what I'v learned recently. Hope we can gain some insight of what's going on among the players.

## Packages set up

* matplotlib
* numpy>=1.18.1
* pandas
* stop_words
* language_detector
* sklearn
* symspellpy==6.5.2
* gensim==3.8.1
* wordcloud==1.6.0
* tensorflow==1.14.0
* keras==2.3.1
* sentence-transformers==0.2.5
* umap-learn==0.3.10
* nltk==3.4.5
* bf4

## Web Scraping using Beautiful Soup 
Use Metacritic as example
