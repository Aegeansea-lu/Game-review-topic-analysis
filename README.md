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

![Image of html](/pic/html.png)

Html tags are used to mark page elements, and similar elements are usually contained within the same tags. Carefully locate every tag and save the data we want

```python3
#look for review_content tags since every user review has this tag
for review in soup.find_all('div', class_='review_content'): 
#within review_content tag, look for the presence of longer reviews
    if review.find('span', class_='blurb blurb_expanded'): 
        review_dict['review'].append(review.find('span', class_=’blurb blurb_expanded').text)
 
    else: 
        review_dict[‘review’].append(review.find('div',class_='review_body').find('span').text)
```

We use find all to get all review_content tags within the page. This is the same as finding all reviews on the page because each review is enclosed by this div class.
The if-else statement ensures that the text is pulled from the right tag, depending on whether the review is long or not.
Let’s look at the ‘else ’condition first. For each review_content tag, we look for a div class that is close to the span tag containing the text review. In this case, I’ve used review_body div class. Since there is only one span tag within this class, we can use find to look for the first span tag.
On to the ‘if’ condition. Longer reviews (that require users to click on ‘Expand’ to see the full text) are within a blurb blurb_expanded span class. Shorter reviews do not have this class. Since blurb blurb_expanded only appears for longer reviews, we can find it directly.
Since all reviews on Metacritic have the same elements, we can just append the desired info to lists, and they will be in-order.


## Model
Typically, there are two ways to complete the topic identification task. We can either resort to hierarchical Bayesian models, like latent Dirichlet allocation (LDA), or we can embed our target documents into some vector space and identify their similarity structure in the vector space by clustering methods. LDA has a hard time handling short texts when there is not much text to model, so the performance would be far from satisfaction. Let's combine both methods and see what we can get

![Image of html](/pic/model.png)

## Result
Visualizations (2D UMAP) of clustering results with different vectorization methods with n_topic=10:


**TF-IDF:**

<img src="/pic/2D_vis_TFIDF.png" alt="alt text" width="500" height="500">

**BERT:**

<img src="/pic/2D_vis_BERT.png" alt="alt text" width="500" height="500">

**LDA-BERT:**

<img src="/pic/2D_vis_LDABERT.png" alt="alt text" width="450" height="450">

**Word Clouds:**

**Topic 1: Negative critics**

<img src="/pic/t0.png" alt="alt text" width="450" height="450">

**Topic 2: Positive compliments**

<img src="/pic/t1.png" alt="alt text" width="450" height="450">

**Topic 3: Cheating behaviors**

<img src="/pic/t2.png" alt="alt text" width="450" height="450">

**Topic 4: Good graphics**

<img src="/pic/t3.png" alt="alt text" width="450" height="450">

**Topic 5: Bugs**

<img src="/pic/t4.png" alt="alt text" width="450" height="450">

**Topic 6: Play with Friends**

<img src="/pic/t5.png" alt="alt text" width="450" height="450">

**Topic 7: Game mods**

<img src="/pic/t6.png" alt="alt text" width="450" height="450">

**Topic 8: Spend lots of time**

<img src="/pic/t7.png" alt="alt text" width="450" height="450">

**Topic 9: Spend time with friends**

<img src="/pic/t8.png" alt="alt text" width="450" height="450">

**Topic 10: I believe to be soccer and the game : Rocket League**

<img src="/pic/t9.png" alt="alt text" width="450" height="450">
