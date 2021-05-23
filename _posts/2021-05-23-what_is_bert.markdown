---
layout: post
title:      "What is BERT?"
date:       2021-05-23 19:06:26 +0000
permalink:  what_is_bert
---


Today's blog is going to be a learning summary blog. Like I mentioned last week, I have started working on an NLP project with Omdena. Right now, we are still deciding on the road map of the project, and so many great ideas are being thrown out. Something that keeps coming up is BERT, and since I am not familiar, I decided to do some research and find out just what this is!  

This [article](https://towardsdatascience.com/bert-explained-state-of-the-art-language-model-for-nlp-f8b21a9b6270/) from Towards Data Science by Rani Horev was an indispensible resource for gaining new understanding of just what this new research is. First things first: what does BERT stand for? Bidirectional Encoder Representations for Transformers. BERT is actually a paper recently published. Where BERT excels is the ability to apply Transformer bidirectionally. Because BERT is an application of Transformer, please don't be surprised if next week's post is about Transformer- another new technology to me!  

One important feature of BERT is that before feeding in a sample of words, 15% are kept as a mask token, which to me sounds like keep a test or validation set, but also helps to make the BERT model more accurate. Another important aspect is that sentences are fed in such a way that 50% are paired with sentences that are connected (subsequent) and 50% are paired with a random sentence. The goal is that the random sentences will be predicted to be random.  

The part of BERT that I think will be most useful for the project will be the classification abilities. Horev talks about how sentiment analysis can be done similiarly to the Next Sentence classification. Because the project involves using social media to identify human rights violations, sentiment analysis is definitely going to be very important. It does seem like the drawback will be that the model converges slowly, and with the large amount of data, this could be a real consideration.  

I am not surprised to see that my colleagues are interested in using BERT. I think that this could be extremely beneficial to us. While this post is more of a high level overview, I am excited to delve into the technical aspects of this. NLP is a soft spot of mine! If anyone has anything to add/correct or questions to ask, I would welcome them! Thanks for reading, and stay tuned for next week's post! 
