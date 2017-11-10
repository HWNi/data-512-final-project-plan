# data-512-final-project-plan

## Motivation of the Study
There are 2 major motivations:
* Experience as a Yelp user

As a foodie, using Yelp to check out new or popular restaurants is a part of my life, and I believe there are a large number of customers who make their decisions on new restaurants based on the Yelp’s rating system and reviews. When people search restaurants near some specific location, Yelp allows users to sort the search results by three options: best match, highest rated, and most reviewed. Personally, I usually sort my search results by highest rated, but sometimes I feel disappointed about the rating because the Yelp rating was overestimated in my opinion. Even though such experience may not occur very often, these special cases still motivate me to conduct a study on the accuracy and efficacy of Yelp rating system in general. 

* Plenty of human-centered aspects involved: bias, algorithm transparency, …

Yelp has already initiated a project named [Yelp Dataset Challenge](https://www.yelp.com/dataset/challenge) which encourages students to dig interesting insights of their business dataset. There have been 9 rounds of challenges finished and hundreds of academic papers written using the dataset, which provides me a large amount of inspiration and guidance for my own research. When I was reading those papers, I realized that my project will involve plenty of human-centered aspects that have been discussed in data512 lectures. For example, there is a paper which points out the warm-start bias existed in the Yelp rating. This paper immediately resonates my exploration to the bias in Wikipedia data and makes me think about other potential bias and shortages that may exist in the current Yelp rating system. In addition, current research about hidden factors and topics in the review text motivated me to think about the mechanism of Yelp rating and its transparency and trustworthiness. 

## Research Questions
**Note that I will narrow down the scope of my investigation subject to restaurants in [Greater Seattle area](http://greaterseattle.us).**

**Main Topic: Are Yelp ratings and reviews trustworthy overall?**

Looking for a scientific way to evaluate the efficacy of Yelp rating and review system will be the major goal of my research. During the Yelp recommendation system background research, I was informed that Yelp has an automated recommendation software which is running constantly to examine the quality of user-generated ratings and reviews. This means ratings on Yelp are not only determined by users’ ratings but also filtered by some rules implemented by Yelp recommendation software. The subtlety of the Yelp rating mechanism could lead to a plenty of research questions that would be interesting to explore. In order to be more definitive on my research topic, I intend to divide my research into 2 types: a) Studying the Yelp rating system without considering the review system and b) integrative study on the Yelp rating and review. The following questions will be focused in my project:

*RQ1: What are the correlations between business overall rating and various non-review-related characteristics of the business such as price, location, number of photos uploaded etc. look like?*

  1. What are the factors that have larger correlations to rating?
  2. How reasonable is associating rating with restaurant’s success?
  3. Are there any correlations among those non-review-related characteristics themselves? For example, is there any correlation between price and location of restaurant.

*RQ2: How consistent are reviews to rating?*

  1. What is the proportion of reviews with sentiments that match the rating?
  2. What are the characteristics of recommended reviews/suspicious reviews that are determined by Yelp recommendation software?
  3. Are there any correlations between those characteristics of recommended reviews and corresponding rating or restaurant overall rating.

## Hypotheses
*Hypotheses to RQ1*

  1. Some aspects of restaurant are more likely to determine the rating of restaurant than others. 

One possible aspect is the price range of the restaurant. The more expensive the restaurant, the higher the rating in average because the restaurant probably invests more in hiring excellent chef and decorating the environment. It’s also possible that cheap restaurants will have higher ratings because their food are more affordable and not bad as well.
  
  2. Yelp rating is trustworthy in general, but it does have some bias that requires extra attention when customer interprets the rating.

The result of “[The warm-start bias of Yelp ratings](https://arxiv.org/abs/1202.5713)” by Michalis Potamias, a researcher from Groupon suggest that there is a “signiﬁcant warm-start bias which may be attributed to the limited exposure of a business in its ﬁrst steps may mask analysis performed on ratings and reputational ramiﬁcations.” In addition, a Groupon deal may also lead to lower Yelp ratings because “when merchants put out an offer they get swamped with new customers and quality deteriorates--even though the goal of a daily deal is to get new potential customers who will become loyal.” (See [reference](http://www.businessinsider.com/how-does-groupon-affect-a-local-merchants-ratings-2011-9))

### Past study:
[Daily Deals: Prediction, Social Diffusion, and Reputational Ramiﬁcations](https://arxiv.org/abs/1109.1530)

[The Groupon Effect on Yelp Ratings: A Root Cause Analysis](https://arxiv.org/abs/1202.2369)

In my research, I wish I could replicate the results generated from these past works and figure out some new potential bias in the Yelp rating system. 

*Hypotheses to RQ2*

  1. The sentiments of reviews match the corresponding user’s rating and the restaurant overall rating in general.

One of my hypotheses to the Yelp rating mechanism is that the overall restaurant rating must be determined by each published review through some computations. Although there could be some discrepancy due to the Yelp recommendation system, it’s reasonable to deduce that user’s rating matches their comments to the restaurant. If this is true, then we should see the overall rating matches the overall sentiments of reviews.

  2. There are some patterns about recommended reviews, and those patterns have correlations to the overall rating.

According to the video which talks about Yelp recommendation software, every Yelp review is automatically evaluated by Yelp’s recommendation software based on quality, reliability, and user activity on Yelp. More often than not, those useful reviews come from active members of the Yelp community. The recommendation software is looking for reviews written by whose opinions, positive or negative, that Yelp feel are helpful and reliable to consumers. In my research, I want to validate this fact by digging some features of recommended reviews. Meanwhile, I would like to deduce the recommendation model and examine whether there are some flaws in the algorithm.

## Data Source Information and Usage

This project will use datasets from [Yelp Dataset Challenge](https://www.yelp.com/dataset/challenge). The datasets are available in both JSON and SQL files. (See the documentation from here). I will mainly use 3 datasets in JSON format for my project:

*Businesss.json*

The business dataset contains business data including location data, attributes, and categories.

_How to use it:_

This dataset will help me identify my research subjects and provide relevant information I need to answer my first research question. As I mentioned before, my project will focus on the restaurants in greater Seattle area, so I need to do some filtering on the categories. Note that the category data looks like:

// an array of strings of business categories
    "categories": [
        "Mexican",
        "Burgers",
        "Gastropubs"
    ],

which has a variety of tags. It’s impossible to get all restaurants in the data by simply searching “restaurant” for category. Thus, I will need to do some explorations to the category in business data and figure out the set of applicable categories to my research.

*Review.json*

The review dataset contains full review text data including the user_id that wrote the review and the business_id the review is written for.

_How to use it:_

This dataset will be the source of my text mining in reviews. Specifically, I will try to use some natural language processing techniques such as sentiment analysis and topic modelling. 

*User.json*  

The user dataset includes the user's friend mapping and all the metadata associated with the user.

_How to use it:_

I will use this dataset for investigating the pattern in the recommended reviews that are identified by Yelp recommendation software. I intend to use the features in this dataset to build a regression model that can predict whether the review will be considered as helpful by Yelp recommendation software. 

### License information:

Yelp provides a [guideline](https://s3-media2.fl.yelpcdn.com/assets/srv0/engineering_pages/e926cc12796d/assets/vendor/yelp-dataset-license.pdf) regarding the dataset license. 

## Analytical Methods

The analytical methods I will use for this project include statistical analysis, exploratory visualization, machine learning, and qualitative case study. 

*Correlation analysis*

A large portion of my study will involve calculating the correlations between two variables, so correlation analysis will dominate my research. Besides, since some of the independent variables are quantitative variables such as price range and number of reviews, plus the response variable like overall rating is ordinal, the correlation analysis will be the most appropriate statistical method to figure out the potential linear association between overall ratings and different quantitative aspects of restaurant.

*Data Visualization and exploratory analysis*

Some variables in this research such as location or type of food are categorical, which means it would be better to use visualization to show the relation between those categorical variables and overall rating of a restaurant. 

*Sentiment analysis*

Sentiment analysis will be very useful when we try to label a given review with either “positive” or “negative”. Advanced sentiment analysis even provides a sentiment score to indicate the strength of tone or emotion in the analyzed text. Since I will need to check whether the sentiment of a given review matches the corresponding rating of user or overall rating of the restaurant, I could use the sentiment label generated by sentiment analysis and even compare the sentiment score with the rating to seek some quantitative relations between them.

*Topic modelling*

One task of my research will look for the hidden patterns in the reviews that Yelp recommendation software considers as helpful, so I will use topic modelling to handle the text mining in those reviews. Also, the hidden factors extracted by topic modelling using LDA algorithm might reveal the reason accounting for minor difference between 3 stars rating and 4 stars.

*Qualitative case study*

The reason for conducting some qualitative studies is to evaluate the context of my research. This is important because rating and reviews are supposed to be completely subjective. I believe the overall rating might be implicitly determined by some demographical or economical factors. 

## Potential limitations

No matter what kind of research I will conduct to analyze the Yelp rating system, a big assumption I have to make is that each individual rating or review is independent to others. In other words, Yelp users’ ratings probably are mutually influenced, and my study will not be able to have a scientific way to evaluate this fact. 

Similar limitation could be the impact of actual fake rating or reviews that somehow get passed from Yelp recommendation software. Rating or reviews that were edited with specific advertising purpose will reduce the validity of most statistical analysis I will conduct in my research.  

