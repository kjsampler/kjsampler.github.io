---
layout: post
title:      "Throwing Shapes... errors"
date:       2021-02-15 06:54:02 +0000
permalink:  throwing_shapes_errors
---


It's Sunday, and that means it's time to update everyone on my data science meanderings. This week I've been having a really fun time working with my multivariate dog license model. Once I sorted out the Keras download error, I've been able to actually run the model. And I am SO impressed with the results. Where my univariate model was yielding a prediction MSE of 150148.29 with the best tuning I attempted; this multivariate model now has an MSE of 76.07.  
Just typing that makes me a little cautious. I think this upcoming week will definitely involve a lot more of analysis and trying to figure out why that number has improved so drastically. It seems too good to be true, and with data, that's usually not a great sign. My initial thought is that the MSE would improve even with the univariate model if I was testing on the smaller dataframe produced by only analyzing the top ten dog breeds like I am in the multivariate. But that's a topic I'll update you all on next week!  
Of course, my next step is to use my prediction function that I'm so proud of. Alas, I realized all too soon that it wouldn't be as simple as copying the function into the new notebook and running it on the data. I found myself again staring down the barrel of an error claiming that my data was not the right shape. 
```
ValueError: cannot reshape array of size 275 into shape (1,5,11)
```

It should be noted that initially I tried to reshape into (1, 5, 1) because I had only copied the function; it wasn't written to accomodate multivariate models. Once I get this issue resolved, the function will absolutely be updated in order to be more usable for a broad range of data.  
I'm realizing that this issue is not coming from the model, but rather the initial 5 data points that I'm using as the training data input. In a univariate model, it was simple enough to just pull the last 5 values of the X train set, because even with 5 lags, there was only one variable for X. I am having a hard time deciding which values to pull from the multivariate model. Because now I not only have to contend with the 5 lags for each data "point", but also the 10 variables (because of the dummies created to sort them into breeds.)  
My initial thought, as you see above, was to reshape into 1 variable, 5 lags, with 11 features. However, I am not sure this is correct. Obviously it errors, but beyond that, what I need is not the last 5 values. I need to figure out how to pull the last 5 X train values.  
My game plan is actually to put my X train into a pandas dataframe, and use the visual to assist in how I will decided which values to pull and how. With the lag of 5, there should be a clear "line" in which values start and stop repeating. It will be easier to visualize which value is the pertinent one, and from there it will (hopefully) be easier to decide how to pull these values; not just in the dataset I'm currently working with that has 5 lags and 10 features, but with any dataset that a user wanted to predict on.  
I have been attempting to visualize this just based on print statements and shapes of the datasets, but I truly think that making a dataframe is going to be the way to see patterns visually. Ultimately, even though this is really hard to wrap my head around right now, it's going to benefit my function. One of my goals for this project is to make this function usable even to those without a code background, and teaching it to handle multiple styles of data and even edge cases will assist with that. Until next week! 
