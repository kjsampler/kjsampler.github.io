---
layout: post
title:      "On Downloading Libraries..."
date:       2021-02-01 05:24:29 +0000
permalink:  on_downloading_libraries
---


Tonight, we're going to talk about Windows 8.1 (I know...) and installing Keras and TensorFlow. I'll preface this by saying that I'm not a CS major, and if anyone reading this can see where I've gone wrong, please reach out! As frustrating as fighting with libraries is, I do feel like seeing what went wrong may be able to help troubleshoot the problem when I decide to sit down and try again.  
For reference, I spoke in my last post about my current project- I'm trying to build a multivariate model to predict the number of dog licenses dispensed; in this case specifically, I want to see if breed of dog has any impact on the total prediction. I've done some good work this week normalizing the data and creating lags (of 5 days to match my previous univariate model) to run the LSTM on. Let's acknowledge that the most frustrating part of this is that at one point, my version of TensorFlow was working- I've already run this model. But for whatever reason (probably self inflicted)... it's not running any more.  
My first mistake was trying to create my LSTM without even importing Keras. 
```
model_5 = Sequential()
```
Which of course returned "Sequential() is not defined". So I copied my import statements from the previous notebook and tried to run them, assuming that because the ran once, they would run again. Rookie move! 
```
from keras.models import Sequential, load_model
from keras.layers import Dense, LSTM, Dropout
```
However, this returned an error longer than the rest of my notebook. At the bottom, it stated that Keras requires TensorFlow 2.2 or higher. The obvious first step was to run 
```
pip install tensorflow
``` 
but that yielded an error that was vaguely familiar: "ImportError: DLL load failed: The specified module could not be found." In researching this error, I quickly found myself in a rabbit hole of unfamiliar territory. I have tried installing several versions of TensorFlow, including CPU and GPU, 2.0 and 2.2. I saw on Stack Overflow that you have to access your environments in Anaconda, check the appropriate TensorFlow box, and apply; but that did not change the outcome.  
Perhaps the most interesting note is that I have a "learn-env" and a Python 3 kernel option for Jupyter. I am afraid that I noticed this too late, and upon changing environments the errors do not change. I know this post is reading like an extended Stack Overflow question, but maybe getting it all out will help with clearing my mind and coming at it fresh next time. It also serves as a good record of all the things that haven't worked, if nothing else.  
Like I said, if anyone happens upon this and sees the error I would absolutely feedback. Ironically, I've never considered myself a computer person. But even these challenges are turning out to be challenging and fun surprises.  
If I can't find a solution in a timely manner, my go-to is to work in a Google Colab notebook. I think they're user friendly and very similar to Jupyter. But I definitely like the challenge aspect of this, and hope to get it solved soon. I'll keep you guys posted! 
