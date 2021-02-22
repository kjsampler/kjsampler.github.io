---
layout: post
title:      "This Week's Update!"
date:       2021-02-22 05:40:21 +0000
permalink:  this_weeks_update
---


Sunday again friends! I am of course, still working on the Multivariate LSTM Dog License forecasting project. I haven't made much progress, at least on screen. There hasn't been a lot of code, but there has definitely been a lot of puzzling, for what that's worth. I've been working a lot on the problem of how to shape the data to run with my forecasting function. I made a definite breakthrough when I realized that I was attempting to force my x5_train dataset into the function. The problem with this dataset is that it accounts for 5 lags AND 10 features, plus a target. In the previous univariate model, I only used the train data with one lag, because the forecast doesn't rely on lags, just on the training data.  
After realizing this, it was simple enough to create a dataframe of the multivariate training data with only one lag. I pulled the last five target values, thinking that those would be sufficient to make predictions using the model_5 LSTM that I created for the multivariate model.  
There is however, a disconnect here. After throwing an error due to an unexpected shape, I began taking the function apart line by line. The first part, where I change the training values into an array was fine. The issue comes when I call
```
model_5.predict(x_array)
```
Because model_5 expects a 3D array, I attempted to reshape my 5 training data points into shape (1, 5, 1). While this satisfies the requirement of being 3D, I noticed that the error says the model expects shape (none, none, 11). I'm not sure that the "nones" make sense, but the 11 got me thinking- model_5 was trained on 11 features (10 variables and a target). So now, the challenge stands to find a way to append the target values to my prediction array, while taking in the other ten variables, but without using those variables as predictions.  
My initial thought is to create a list of arrays (10, 1) that can function as an input for the model, but be "discarded" once that step is done. It is satisfying in a way to know that the multiple variables are going to provide more data (and hopefully improved accuracy) in my prediction function, ultimately making it smarter.  
This does bring up a potential for making the function more usable in other cases. While I don't know if I'll be able to amend the function in this round, it is a definite idea for future work to put this steps inside the function. The dream function would really only need a pre-trained model and a dataset. Maybe someday we will get there, but for now I'm just taking this one error code at a time. 
