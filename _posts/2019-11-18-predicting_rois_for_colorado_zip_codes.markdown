---
layout: post
title:      "Predicting ROI's for Colorado Zip Codes"
date:       2019-11-18 23:32:38 +0000
permalink:  predicting_rois_for_colorado_zip_codes
---


Let me start by saying - this was my favorite project that we've done so far. We were given close to 15,000 zip codes from across the United States and given a "simple" question- if our client asked us which were the best to invest in, which 5 would we choose?

For my fictitious client, I decided to look around Colorado. I was curious because I've noticed rising property values in Colorado through my own personal research. I wanted to know if there was a trend to these rising values, and if they were predicted to keep rising. I chose several zip codes from the Denver area, including Boulder, Denver Metro, and Aurora. I also included Colorado Springs. The rest of my zip codes were chosen from southwestern Colorado - the area that I personally have the most familiarity with. These areas included more rural areas like Durango, Montrose, and Cortez. The last few zip codes are clustered around the Grand Junction area- Fruita, Clifton, and Grand Junction. 

Now that I had chosen 14 zip codes, it was time to determine which 5 would be the best investment. The next question to answer was how I was going to determine "best." I decided to use a formula for return on investment- the difference in the last recorded value and the predicted value after three years, divided by the last recorded home value. This yields a percentage and tells us that for every dollar spent, you can expect the percentage in cents returned. I chose three years because it is more of a short term investment, but long enough to see a return on investment. 

The very first thing I did was modify the data to best suit my needs. This included shaping a new table called "Colorado" which only contained the zip codes I needed. Next I named each row as a variable to make them easier to manipulate individually. For time series analysis, I had to set the index of each row as a datetime. Lastly, I "melted" the data so that it would be in a long format (easier to use), rather than a wide format (easier to visualize). To get a whole picture of the data, I plotted the average home price of each zipcode between April 1996 and April 2018. 

This gave me a very interesting picture - almost every line dips leading into 2012, and then increases significantly. There is also very little line crossing, meaning that most areas were increasing at a similar rate. 

In order to make predictions, I wrote 3 functions. The first two worked together to calculate the best order for my p, d, and q values, based on the lowest mean squared order of the ARIMA model. 
```def arima(data, arima_order):
    '''
    Function to calculate mean squared error using ARIMA 
    
    args: 
        data: pandas dataframe 
        arima_order: values desired for p, d, q
    returns: 
        (int): Mean Squared Error using data and given p, d, q values
    '''
    train_size = int(len(data)*.66)
    train, test = data.values[0:train_size], data.values[train_size:]
    history = [x for x in train]
    predictions = []
    for x in range(len(test)):
        model = ARIMA(history, order = arima_order)
        model_fit = model.fit(disp = 0)
        yhat = model_fit.forecast()[0]
        predictions.append(yhat)
        history.append(test[x])
    error = mean_squared_error(test, predictions)
    return error```
		
```def arima_order(dataset, p_values, d_values, q_values):
    '''
    A function to determine optimal p, d, q values 
    
    args: 
        dataset: a Pandas dataframe
        p_values: a range of values for p
        d_values: a range of values for d
        q_values: a range of values for q
    returns:
        best_cfg: combination of p, d, q values with lowest mean squared error
        best_score: lowest mean squared error
    '''
    best_score, best_cfg = float('inf'), None
    for p in p_values:
        for d in d_values:
            for q in q_values:
                order = (p,d,q)
                try:
                    mse = arima(dataset, order)
                    if mse < best_score:
                        best_score, best_cfg = mse, order
                    print('ARIMA%s MSE=%.3f' % (order,mse))
                except: 
                    continue
        print('Best ARIMA%s MSE=%.3f' % (best_cfg, best_score)) ```
			
The third function is the same as the third, it just returns the predictions instead of the mean squared error. 
```def arima_predictions(data, arima_order):
    '''
    A function to make predictions on given data
    
    args:
        data: a given Pandas dataframe
        arima_order: desired values of p, d, and q
    returns:
        predictions: the predicted value based on data history
    '''
    train_size = int(len(data)*.66)
    train, test = data.values[0:train_size], data.values[train_size:]
    history = [x for x in train]
    predictions = []
    for x in range(len(test)):
        model = ARIMA(history, order = arima_order)
        model_fit = model.fit(disp = 0)
        yhat = model_fit.forecast()[0]
        predictions.append(yhat)
        history.append(test[x])
    error = mean_squared_error(test, predictions)
    return predictions ```
		
Using these functions, I followed these steps to calculate the ROI for each zip code in my subset. 
1. Use arima_order() to determine best p, d, q values. 
2. Split the data into train and test splits. 
3. Use arima_predictions() to predict the data. 
4. Append the predictions to the test dataframe to easily make comparisons.
5. Use ARIMA() to forecast 36 months into the future. 
6. Use the ROI formula to predict the percentage increase or decrease. 

Using these steps, I made the following observations:
The top 5 zipcodes to invest in were: 
*80011 Aurora at 35.8%
*80206 Denver Metro at 16.3%
*81507 Grand Junction at 14.0%
*80302 Boulder at 13.1%
*80303 Boulder at 11.2%

While the bottom 5 were: 
*81401 Montrose at -6.2%
*81520 Clifton at 3.4%
*81501 Grand Junction at 3.8%
*81321 Cortez at 4.3%
*81301 Durango at 6.5%

I thought this project was a true stretch of my abilities, but was very fulfilling and yielded some interesting observations, like Aurora having a huge return on investment. It was also intriguing to see that other than Montrose, none of these zip codes would be a decrease in investment. Overall, it looks like Colorado would be a good place to invest; it's just a matter of where you invest to yield the highest return on investment. 
