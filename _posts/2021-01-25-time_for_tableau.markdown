---
layout: post
title:      "Time for Tableau"
date:       2021-01-25 06:45:25 +0000
permalink:  time_for_tableau
---


In keeping with my theme of waiting for signs on what to learn next, I've taken on Tableau. I keep seeing it everywhere; which is a little daunting, but also increases the urge to learn. So I took advantage of the New Year's sales on Udemy and bought a course. And why, oh why, did I not start learning this sooner? I love it. I firmly believe that part of being a great data scientist is making great visualizations, and Tableau is amazing at that.   
I'm still less than halfway through my course, but I'm in love. It's taught by Kirill Eremenko through SuperDataScience, and I would highly recommend to anyone who has seen Tableau but isn't familiar with it. In my opinion so far, it's as easy to use as Excel or Microsoft Word. Kirill starts the course off with a bang by showing that with a simple drag and drop, Tableau can use data to create an informative map. And even in the simpler lessons such as making bar charts, the instruction goes deep enough to keep you interested and teach you the magic to make your visualizations that much more engaging.  
As a scientist, of course I had to deviate from the course. So while I was working on a personal project (which I'm so excited to share with you all when the time comes) I decided I wasn't satisfied with a simple .plot(). I've included a snapshot of the dataframe head. (Sidenote: I just learned ALL about how to export a dataframe to an image - I'll include a code snippet at the end of the post!)
![Click here for image](/https://docs.google.com/presentation/d/1opr57anRJta5ILo57a4QF3Hb3IXqaElyphUvpbz3_eE/edit?usp=sharing)  
If you didn't click the link- here's a summary. I took the top ten most popular dog breeds, and summed how many licenses were dispensed for each breed each day. While visions of colorful line charts danced in my head, I exported my csv and dragged it into Tableau and waited for the magic to happen... and it didn't. I'm definitely still troubleshooting, but I don't think Tableau agrees with my Datetime Index. I will keep you all posted with the resulting beautiful line chart.  
I guess I still have a way to go with Tableau. It's honestly actually a lot of fun, and very satisfying to produce gorgeous visualizations, so I don't think continuing my learning will be too hard.  
As promised, I present my code snippet for exporting a dataframe to an image. This actually turned out to be the real learning experience of this blog- I don't mind the detour. As always, feel free to reach out with any comments, constructive criticism, questions, anything at all!  
*Make sure to install dataframe_image first!* 
```
image_df = breed.head()  
image_df = image_df.style.background_gradient()
dfi.export(image_df, 'data/blog_image.png')
```  
In this case, my original dataframe was named "breed", but I adjusted it to only show the top 5 and added a gradient background because I thought it looked nice. 
