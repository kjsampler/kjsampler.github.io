---
layout: post
title:      "The Wildfire Data Set Introduction"
date:       2021-05-03 04:40:25 +0000
permalink:  the_wildfire_data_set_introduction
---

So after completing my most recent project [Using AI to Predict Dog Licenses](http://https://github.com/kjsampler/Using-AI-to-Predict-Dog-Licenses), I found myself looking for inspiration for my next project. As my husband was hard at work burning our yard rubbish, I sat and "supervised", (read: stressed over the fact that he was burning so close to our house.) I told him that I was lacking inspiration, and he sarcastically replied "Maybe you should look up data about out of control burns." I scoffed, but when I got on Kaggle and found [this dataset about wildfires](http://https://www.kaggle.com/rtatman/188-million-us-wildfires), it seemed like fate. As a native Coloradan, wildfire prevention is an issue that is near and dear to my heart, and after the Pine Gulch Fire last year, which was less than 10 miles from my home, wildfire knowledge and prevention becomes more and more personal to me. To be sure, I'm not sure what I'm going to do with this data yet. But I'm excited to work on a personal project that is so important to me.  

The data is stored as a .sql file, which was very exciting to me. I am eager to improve my SQL skills, and working with this data seemed to be a good opportunity. When I downloaded the file from Kaggle, I noticed that it took a minute but wasn't paying attention to the size. It wasn't until I tried to do an initial commit on GitHub that I noticed the file is 759MB, and that was only because it turns out that GitHub puts a limit on anything more than 100MB. The next question became: how am I going to use this large data source?  

If you follow this blog and Git, you already know the answer. I went to a Google Colab- my weapon of choice. In this way, I was able to download the file to my Google drive, mount my drive to the Colab notebook, and push to Github that way. I was delighted to realize that I could use the same flavor of SQL that I was already familiar with; MySQL.  

Once I was able to work in a Colab notebook, I wanted to find out if there was a way that I could break the data into small (preferably <100MB) datasets that I could then push to GitHub so that others could follow along. I decided that the first step was to keep analyzing the data. I think it is a lot harder to ask a question and then find data than supports it than it is to explore the data and listen to what it is telling you. Especially where a personal project is concerned. So I decided that my first step was to analyze the schema. So far, using the following code, I've been able to determine the tables in the dataset, and I'm about halfway through determining the columns in each table: 
```
c.execute("""SELECT name FROM sqlite_master WHERE type = 'table';""")
table_names = c.fetchall()

table_name = c.execute("""SELECT sql FROM sqlite_master WHERE type = 'table' AND name = 'table_name';""").fetchone()
```  
This week I hope to finish finding all of the column names. If anyone has suggestions for the most efficient way to diagram the schema, I'd love to hear it! Using a trusty pen and paper, I'm going to draw out the schema, including the primary keys. Once I understand the diagram on paper, I'm going to make a digital diagram and include it in my GitHub repo.  

I'm not sure what this data is telling me yet. I think once I complete my initial exploration, I want to review what others have done with the same dataset. With such a large file, there's sure to be countless questions to explore. While it's just exploration for now, I'm excited to share with everyone what this data has in store. Stay tuned! 
