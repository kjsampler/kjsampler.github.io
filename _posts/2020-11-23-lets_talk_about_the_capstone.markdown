---
layout: post
title:      "Let's talk about the Capstone"
date:       2020-11-24 00:50:02 +0000
permalink:  lets_talk_about_the_capstone
---


It's finally that time - I've  completed my capstone project for Flatiron School. I'm absolutely buzzing with emotion, so we'll keep this technical.  
The requirements of this project were wide open, which I quickly found was both a blessing and a curse. I could do anything I wanted- any dataset (that wasn't ready to go, out of the box), any data science question. Plus the pressure of trying to wrap up my entire experience at Flatiron School into one project. One of the hardest parts of this project legitimately was trying to decide where to start. After a few ideas took off and then sadly, crashed back to Earth, I found a dataset on data.gov about dog licenses dispensed in Allegheny County. I'm pretty sure a rainbow came out of my computer screen. It was a treasure trove of information, and subjects that I'm familiar with- puppies and government work.  
The first step was to decide just what question I was trying to answer. The fact that the licenses were input with a "Valid Date" made me think back to one of my favorite units- Time Series. I decided to do a time series analysis to predict the number of licenses dispensed in a day. I was worried the project was too simple (I was wrong), so I looked around at how I could use a neural net, and learned you can use LSTM for time series analysis. I was set.  
Before I could do any of these steps, I had to clean the data. Just because data is already in a csv does not mean it's easy to use, and I found out the hard way. I used three years of data to train because I didn't want to overwhelm my computer. The length of those three datasets was 227,000. It would definitely be an interesting extension of this project to train on more data, which is readily available. Within those three years, there weren't many null values, but I noticed that there were a lot of "hidden" nulls- values that were put in as null placeholders, but not actually null. I ran a ```.value_count()``` on each column. I was so fortunate as to browse through the entire list of dog names, searching for hidden nulls. Not judging, but people name their dogs pretty unfortunate names. Looking at you Taco Belle.  
Once the nulls were taken care of, I created a univariate dataframe that contained only a pandas timestamp index, and a column "Sum" that represented the total number of licenses dispensed in a given day. Looking over the data, I realized that the offices must not be open on weekends on holidays, because the Sum was always zero. I took weekends and holidays out.  
With my clean dataframe ready to go, I moved on to the ARMA model. As an initial exploration, I decided to plot my dataframe, just to see what it looked like.  
It was incredibly seasonal. For some reason, there's huge spikes in December and January. I would be curious to do more research and see if those are true spikes, like people who procrastinate licensing their dog until December, or if they are another imputing error. For example, if the Valid Date is unavailable, maybe a technician is imputing January 1 as a go-to.  
Whatever the reason, I was left with some very seasonal data, and when you're working with ARMA, that just won't do. I attempted several methods of regularizing the data, and some methods helped, but nothing took the seasonality out. I decided to go with a SARIMA model. The first thing I wanted to do was find the best values for p, d, and q. I could tell that I wanted my s to be one year because the spikes were happening yearly. I ran a grid search and chose the best p, d, q based on AIC. But that block of code ran for hours. I was confident that unless my forecast was extremely accurate, this SARIMA model would not be the way to go, just because of the long parameter search time.  
I went ahead and ran a forecast for the upcoming year using my SARIMA model. I was fortunate to be "forecasting" 2018, so I took the observed data in 2018 and compared it to my forecast. I came up with a MSE of 145,107. It seems really high, but when you look at the fact that we are predicting over a year, and the county typically dispenses dozens of licenses per day, it's not awful. What concerned me however, was the confidence intervals on the forecast. On the graph, the confidence interval is green, and the last third of my graph is completely green. I wondered if we could do better.  
So I moved on to LSTM. With a lot of help from Jason Brownlee's post in Machine Learning Mastery, I picked my way along manipulating my data into a form that could be fed into a neural network. I first made a very basic LSTM model, and then made several tweaks and tunes until I got an MSE that was close to what I was getting with the SARIMA model. I firmly believe that given more tweaks and maybe more data, the base model could achieve a lower MSE than the SARIMA model. I saved this as my model.  
LSTM doesn't come with an out-of-the-box forecast function, so I was tasked with writing my own. It was definitely overwhelming at first, because I was looking at a fairly complex function. But, and don't tell anyone, I really enjoy writing functions. I start with my basic steps that I want it to do, and then I write individual lines outside of the function so that I know those lines work. Once I have those steps down, it's not too difficult to adapt the code to take in whatever input the user wants to put in. Which is not to diminish the work I put in on this function, I just didn't find it nearly as scary as I thought I would.  
```
def predict_values(training_data, output):
  ''' A function that takes in training data and uses a tuned LSTM neural 
  network to recursively predict data for a given number of steps.

  Inputs: training_data: The last 5 points of the models training set
    output: user provided dataframe formatted with a desired time period to be predicted
    as a pd.TimeStamp 
  Returns: The output parameter with a scaled prediction and unscaled prediction column 
  appended'''

  predictions = []
  predictions.append(training_data)
  x_array = np.array(predictions)
  x_array = x_array.reshape(1, 5, 1)
#Generate predictions
  model = load_model('final_model')
  for n in range(len(output)):
    pred = model.predict(x_array)
    x_array = np.append(x_array, pred)
    predictions.append(pred)

    x_array = x_array[-5:].reshape(1, 5, 1)

#Add predictions to output df, unlist the values
  predictions = predictions[1:]
  pred_list = []
  for n in range(len(output)):
    pred_list.append(predictions[n].tolist())

  unlisted = []
  for n in range(len(pred_list)):
    var = pred_list[n]
    var = var[0]
    unlisted.append(var)

  output['Scaled Prediction'] = unlisted

#Unscale predicted value
  unlisted_array = np.array(unlisted)
  unlisted_array = unlisted_array.reshape(-1, 1)
  output['Predicted Value'] = scaler.inverse_transform(unlisted_array)

  return output```  
	You'll notice that this function requires the user to input their own dataframe, and in the future, I think it could be further developed to create that dataframe given a start and end date. But that's a story for another day.  
	Armed with my function, I made another year of forecasts, this time using my LSTM model. And somehow, this model performed better than the SARIMA. It yielded an MSE of 115,307. What interested me about this though, was the fact that because it is recursive, the model eventually starts to converge on itself. This one converged before 60 steps, so 251 seems a little inappropriate for it.  
The conclusion that I came to was the the LSTM model was absolutely the way to go. Even training the neural network took only 5 seconds, compared to the hours it took to generate the p, d, q for the SARIMA model. However, because of those seasonal spikes, even the LSTM should be taken with a grain of salt. And it shouldn't be used for long term forecasts. With this data, I would say no more than 60 steps should be predicted. 
There are some things that I'd love to work on in the future. Namely, I'd like to implement the categorical variables into the LSTM model. I think running a multivariate model would probably yield some unexpected insights. Another thing that I personally would like to do is reframe the data into a SQL database. Data manipulations would definitely be easier, and it would be simpler to see links between variables.  
This project has definitely flexed all of my data science muscles. I'm very proud of all the work that went in, and I'm excited to see where data science is taking me next. 
