---
layout: post
title:      "Multivariate LSTM Wrap-up"
date:       2021-04-04 22:21:39 +0000
permalink:  multivariate_lstm_wrap-up
---


Here we are folks! The completion of my first project outside of Flatiron School. So, for this project, I decided to take my capstone one step further. In case you haven't read about it yet, I'll fill you in. I found a dataset with information about dog licenses dispensed in Allegheny county. I was able to produce a univariate LSTM neural network, and then write a forecasting function to be able to predict how busy the office would be on a certain day.  

For this project, I continued on with my future work plans, and decided to create a multivariate LSTM to see if it would yield more accurate predictions of daily totals- that way a manager could better be able to staff the agency if there was a spike in licenses on say, National Labrador Retriever Day on January 8.  

Because of the presence of "national dog days", I decided to start my multivariate exploration with that as my second variable. Part of me was just curious as well. To start this out, I ran a count of how many unique breeds were in the dataset and found 340. This was just a little too many to run my experiment, so I decided to narrow it down to the top 10 most popular breeds. I found that one of the top breeds was "Tag". I didn't recognize that breed, so I googled it. What I found, upon researching my data a little more, was that Tag is not a breed of dog, but rather a placeholder for dogs that have previously been licensed and are just getting a yearly re-license. So I removed that column. I was also cognizant of the fact that 10 in 340 breeds isn't much. I considered using an 'Other' column, but I found that if I included Other, it would represent 54% of the total data. I decided that if the experiment was successful, I could start going back and adding in more breeds or classes of breeds.  

Once I had my dataframe, I used a ```pd.get_dummies()``` to give each breed a unique column and help generate daily totals. It seems I can't post an image here, but please check out the repo for a line chart of each breed's daily totals. I added all of these totals to create a column "Total" that would be our target, just like in the last experiment.  

Creating the neural net was very similar to doing it with the univariate model. I ran into some kinks regarding scaling the data and creating lags. I would once again like to thank Jason Brownlee in this [article](https://machinelearningmastery.com/multivariate-time-series-forecasting-lstms-keras/) for the walkthrough and also the ```scaled_to_supervise()``` function. To keep the experiment consistent, I opted to use the same neural net as in the univariate model, just adjusted to multiple variables. This also meant using 5 lags on the data, which was a lot more of a mind bender with 10 extra variables.  

I was delighted to find that my RMSE was only 68.17! However, as I considered the data, I realized that if I was going to make the call that my multivariate model was truly more accurate, I would have to run the univariate model on the same Top 10 breeds dataframe. So while I want to think my multivariate model is considerably more accurate, more research is needed to make that call.  

The next step was to reprise my prediction function. This is where the whole experiment hits a snag. I created a new notebook just for fiddling around with this function and trying to rewrite it- it's in the repo as Multivariate Prediction Function. I spent countless hours tweaking, researching, and (let's be honest) yelling at the monitor. In the end, I'm not sure that I have the resources to rewrite this function to account for the extra variables. It is disappointing because the prediction is the real selling point of this project- it is what creates a tangible value for a business owner.  

The next steps are of course to keep researching how to make that prediction function work. I'm sure the answer is out there, it's just not available to me yet. I really believe that looking at this data from  a multiple variable standpoint is the way to glean extra insights- if the data is there, we should be using it! I would also like to see some of these visualizations and insights in a Tableau dashboard. I think the graphs would really benefit from something a little more interactive, and it would help analysts to have the pertinent data at a glance.  

This project has been an excellent learning opportunity. I feel like I took the parts of my capstone that I was a little shaky on and really firmed those areas up. It has been rewarding to complete my first project out of school and know that the learning is going to continue, and that I can make cool things on my own. I'm excited to explore and come up with my next idea. 
