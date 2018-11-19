---
title: Sleepless in Seattle,  A Data Story
categories:
- Data Science
excerpt: |
  Suppose you are planning a vacation to Seattle, most likely you will pull out the google map
  to see **which neighborhood to stay with**. And most likely you want to know which area is
  popular among fellow visitors. This is a good indicator of where you can get the most out
  of your stay in Seattle.
feature_text: |
  ## Undercover Seattle
  Through the lens of Big Data
feature_image: "/assets/seattle.jpg"
image: "/assets/seattle.jpg"
---

## Introduction

Suppose you are planning a vacation to Seattle, most likely you will pull out the google map
to see **which neighborhood to stay with**. And most likely you want to know which area is
popular among fellow visitors. This is a good indicator of where you can get the most out
of your stay in Seattle.

Now suppose you are a conference planner and assigned a task to organize an event in Seattle,
you definitely would like to find a time for this event so that it is easier and cheaper to
find accommodations for the event participants. In that sense, you'll want to stay away from
the **busiest time of Seattle tourism** business.

What is more, if you are running a bed&breakfast business in Seattle, at the beginning you
may want to find out at what price you should be hoping for. Location, number of beds,
free parking included? **Which factors are predominantly determining the price** of your BnB
service?

Of course, you might get suggestions from personal experiences, your friends, or professional
consultant. However these suggestions are either subjective, emotional, or derived from small
amount of samples. Fortunately, AirBnB provides dataset of its listings in Seattle area [here](
https://www.kaggle.com/airbnb/seattle). Through the lens of big data, we might give you objective
and illustrative answers to all the following three questions:

* Which neighborhoods in Seattle are most popular among AirBnB visitors?

* What is the busiest time of a year to visit Seattle?

* Which factors are most important in determining the pricing of AirBnB listings?


## Part One: The Most Popular Neighborhoods in Seattle

What defines the popularity of a neighborhood in terms of accommodating tourists? One intuitive
way is to look at the total **number of listing** in the dataset. The more listing there is, more
popular this neighborhood is. There is some merit to this argument. However, what if there is
oversupplying of AirBnB listings in this area? You will see a spike in the listing number but
that does not tell the whole story. Luckily, we could add a second metric, **vacancy rate**, to
tell us what percentage of these listings are vacant throughout a whole year. The lower the
vacancy rate, more popular the listing is. We could compute the median vacancy rate in all
listings of this neighborhoood, as a sound indicator to the popularity of neighborhood, in
addition to the metric of listing numbers.

{% include figure.html image="/assets/top_ten_listed.png" caption="Figure.1 Top Ten Most Listed Neighborhoods" width="500" height="500" %}

{% include figure.html image="/assets/top_ten_vacant.png" caption="Figure.2 Top Ten Least Vacant Neighborhoods" width="500" height="500" %}

We calculate the top ten most listed neighborhoods and the top ten least vacant neighborhoods.
There are two neighborhoods on both lists. And they are **Belltown** and **Lower Queen Anne**.
It turns out that both are located at the center of downtown Seattle and next to waterfronts.
No surprise!

## Part Two: The Busiest Time to Visit Seattle

What defines the term "busy" in Seattle's accommodation sector? It should indicate how hard it
is to find an accommodation in Seattle. Fortunately, in the dataset provided by AirBnB, the
availability of each listing on each day throughout year 2016 is recorded. We could do some
data wranglings to find out on any given day of year 2016 what the **vacant rate** of all listings
is. The time periods when vacant rate is low should be the days when visitors find it hard
to get accommodations. These should be the busy days! Moreover we could select only the popular
neighborhoods and see the vacant rate of these areas throughout the whole year. This might provide
a better metric for those conference planners planning for events mainly located in downtown Seattle!
From the dataset, the trends of vacant rates throughout year 2016 are calculated for all and
most popular neighborhoods found in the previous section.

{% include figure.html image="/assets/trend_vacant_rate.png" caption="Figure.3 Trend of Vacant Rate in Year 2016" width="500" height="500" %}

From the figure above, clearly the busiest time to visit Seattle will be the **first three weeks**
into the new year, when the vacant rates are lowest in both general and in popular neighborhoods.
Interestingly enough, the summer time, namely July, is also a busy time for popular areas, like in
**Belltown** and **Lower Queen Anne**.

## Part Three: What Factors Matter Most in Determining Price on AirBnB

It is quite easy to come up with a list of terms that seem important in determine the price of an
accommodation listed on AirBnB, for examples, locations, number of beds, etc. Yes, they are important
but how important exactly they are compared to other traits of a listing? We will use data to tell you.
To do this, a [**Random Forest Classifier**][random forest] is implemented and trained based on the dataset. The importance
of each feature is measured by **impurity** decreases it contributes to. The **importance** could be
a positive contribution or a negative one. For example, the location could both positively and
negatively impact pricing. The top ten most important features in determining price of a listing is
presented below.

{% include figure.html image="/assets/top_ten_feature.png" caption="Figure.4 List of Top Ten Most Important Features in Pricing" width="500" height="500" %}

Among these features, "accommodates", "beds", "bathrooms" and "bedrooms" are directly related with
how many visitors could be accommodated, which directly determines pricing in many cases.
"room_type_Private room" means the room is private and "room_type_Shared room" means the room is
shared. The former most likely contribute positively to the price and the latter does so negatively.
"longitude" and "latitude" are describing the locations of a listing, the impact of which on pricing
is obvious. "cleaning_fee" itself alreay contains the information of price. No surprise here.

What is interesting is the inclusion of "number_of_reviews" and "reviews_per_month". It turns out
that they are negatively contributing the price! Counter intuitive, isn't it? In fact, it make some
sense since customers are more likely to write a review on a AirBnB stay if they have a negative
experience of it. No wonder more reviews a listing has, more likely its price drops compared to
similar listings.

## Conclusion

Through the lens of AirBnB data in Seattle, we undercovers some aspects of accommodation business
in Seattle that are not easily perceived through human eyes. Firstly, a list of most popular
neighborhoods is presented by ranking the vacant rates and listing numbers of all neighborhoods.
Secondly, busiest time periods are found by calculating vacant rates throughout a whole year.
Thirdly, a machine learning method [**Random Forest Classifier**][random forest] is implemented to
discover the most
important features that dictate the pricing of a AirBnB listing. It is possible for people to give
out the same answers to these three questions based on their common sense. However, through data, we
could present our opinions in an objective and persuasive way.

This is the data story I have with Seattle. Thank you for reading. The technical details are available
[here](https://github.com/randomwalk10/udacity_ds_blog_project).

[random forest]: https://en.wikipedia.org/wiki/Random_forest
