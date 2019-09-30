---
layout: post
title:      "Module 3 Project "
date:       2019-09-30 23:12:21 +0000
permalink:  module_3_project
---

## My journey through SQL Queries

I'll be honest. Before this project I thought I understood SQL Queries pretty well. They imitate English, I have a list of what order your statements should go in, everything seemed pretty simple. What I didn't know was that I had a lot to learn about SQL Queries in my exploration of the fictitious Northwind Database. I've included a picture of the ERD below, but as I was about to learn, you can't always trust the ERD. 
![](http:/https://raw.githubusercontent.com/learn-co-curriculum/dsc-mod-3-project/master/Northwind_ERD_updated.png/)


The first lesson I learned was what happens when you have the word "Order" in your schema. I tried to run a basic query: 
```
c.execute("""Select * FROM Order;""")
c.fetchall()
```

But no matter how many times I ran it, I kept getting a syntax error. I tried several strategies (read: grasping at straws) like changing the c.fetchall() command, checking my cursor, and finally assuming that I wasn't connected to the database correctly. After troubleshooting my connection by selecting all from a different table, I realized that something had to be wrong with the "Order" table. I found out that because ORDER BY is a command in SQL, I needed to put apostrophes around the table name. SQLite was expecting me to order my table, not that I was asking it to fetch from a table named order. 

The lesson here is to be careful of your table names when creating a database, and to be careful when querying that you are very explicit in telling SQLite exactly what you want. 

My next surprise was join statements. As foreshadowed above, I started out just looking at the ERD to tell which column names I could join on. This led to a very simple query that actually ran and looked good at first. 
```
sql_query_1 = c.execute("""SELECT ProductName, Quantity, Discount FROM OrderDetail JOIN Product ON ProductId """)
``` 
Just looking at the ERD, this simple code should have worked. It ran without error in my notebook, I had the proper column name selected and the Pandas DataFrame I put it into looked fine. However, as I started using .loc statements to get specific pieces of data, I realized I had a problem. The tip off came from one of my hypothesis tests. I was testing to see what level of discount was most effective for the company to use, so I had come up with variables tied to the various levels of discount. 
```
test_0 = hyp_1_df.loc[hyp_1_df["Discount"] == 0.00]
test_5 = hyp_1_df.loc[hyp_1_df["Discount"] == 0.05]
```
I then ran a Welch's T-Test against the levels of discount versus no discount. 
```
stats.ttest_ind(zero, five, equal_var = False)
```
When some of my p-values started returning exactly the same for different levels of discount, I realized I had a problem with my data. 

To troubleshoot this, first I started by aliasing my table names and setting the columns equal to each other, ie:
```
sql_query_1 = c.execute("""SELECT ProductName, Quantity, Discount FROM OrderDetail od JOIN Product p ON od.ProductId = p.ProductId """)
```
But this returned an error. This was a tip off to me that my join statements were not in line. My next step was to query all of the columns within each table. I learned that especially for the column "Product ID", "Order ID", etc... the column was simply named "ID". After comparing the tables my final query looked more complicated, but also returned the proper data. 
```
sql_query_1 = c.execute("""SELECT ProductName, Quantity, Discount FROM OrderDetail o JOIN Product p ON o.ProductId = p.Id""")
```
I'm not going to say NEVER trust the ERD, but definitely don't put all your faith in it. It's a good idea to check your column names, especially when doing Join statements to make sure you get accurate data. 

The last advice I have is to keep it simple. At one point, I was trying to Join between 7 tables, when a simpler solution existed. It comes down to minimizing errors and making sure that your code is easy to read. It makes for simpler debugging and less mess when things don't work out. I'm learning that if there is a simpler way to do something- do it. 

I hope you have enjoyed reading my advice, hard learned through my own SQL errors. Though there are more errors to be had, it's all part of the process of learning. It's all part of this process of becoming a data scientist! 
