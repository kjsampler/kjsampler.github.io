---
layout: post
title:      "That's a Wrap!"
date:       2021-03-07 20:39:15 +0000
permalink:  thats_a_wrap
---


I feel like I'm throwing out a rubik's cube here. I've been puzzling over how to write a forecast function for my multivariate model, and I'm afraid that at this point, it's time to step away and wrap this particular page up. The frustrating part is that I can't escape the feeling that I'm one turn away from solving rubik's cube. Alas, let me share the journey I went on.  
I began by reviewing my predict_ values() function:  
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
  #ammend function to intake number of input variables
  x_array = x_array.reshape(1, 5, 1)
#Generate predictions
  model = model_5
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

  return output
```	
The first and most obvious issue is the training_data input. In a univariate model, this is just the last 5 data points in the training set. However, I could not use this for the multivariate, because the last 5 would have been made of 1 target value, and 4 variable values for the same row.  

I attempted to solve this by created a dataframe train_df, that contained a row for each data point: 1 target, and 10 variables. I created predict_array (which would later become training_data), by calling the last 5 rows of train_df.  
```
	predict_array = train_df[-5:].values
```

I realized that my data was still mismatched though- each row in train_df was still taking the 5 lags into account. The problem was becoming overwhelming in a hurry. I decided that in the interest of getting a working function, I would use a single lag and investigate the difference in MSE. With 5 lags, MSE was 67.19 and with one lag it went up to 94.68. This difference feels significant, but keep in mind that the MSE for the univariate models was in the hundreds. I decided to keep trying to write a forecast function.  

Once again, I used my predict_array, but reshaped it to be three dimensional, per the input shape of the multivariate model. My final shape used was (1, 5, 10). The target column was not needed, because the model.predict() function is predicting the target.  

Finally, I was able to generate a prediction! However, my final realization occured. The predict() function is only going to predict one value- the target. This is what I want, except that in order to make recursive predictions, I need the 10 variable values to go with that row, in order to use 10 variables to predict the next target, and so on.  

So this is where I'm calling it. I believe that it is technically possible- it would just involve reworking the data to make each variable the target value in turn. There comes a time when you have to wonder if you are doing something because it is worth it, or if you are doing it just to check a box and say you did. Maybe I will come back to it when I have more experience, time and resources. But for now, I think I have accomplished what I set out to do.  

Next week, expect a high level overview, along with a link to a YouTube video where I will present my findings. If anyone has advice or suggestions, I'd love to hear them! Even though I feel a little frustrated with the way this is ending, I've still enjoyed this further exploration, and I can't wait to hear feedback and hope that somebody may find this as exciting as I do. Until next Sunday! 
