---
layout: post
title:      "Azul, Java, and JVM, Oh My!"
date:       2021-03-29 05:52:35 +0000
permalink:  azul_java_and_jvm_oh_my
---


For tonight's post, I thought I would look into a technology new to me- Azul. However, upon trying to look what Azul is, I realized that my Java knowledge is seriously lacking. For each question I answered, I raised two more. So this is me trying to keep things straight. Anyone who is reading this who has more familiarity with Java and would like to correct me, offer feedback or good resources to learn about this is more than welcome to!  

First- what is Azul? It was introduced to me as a way to deploy machine learning algorithms as part of a SaaS. As I started researching Azul and how it is used, I learned that it is not a JVM itself, but it does produce and support JVMs. From my very brief and high level interest in Azul, this made sense with the deployment aspect. But I needed to understand better what a JVM actually is.  

So, what is a JVM? Java Virtual Machine. From my understanding, with help from this [article](http://https://www.infoworld.com/article/3272244/what-is-the-jvm-introducing-the-java-virtual-machine.html) from InfoWorld, the JVM basically seems to be what makes sure that an app plays nicely with any environment. This article states that when Java was released in 1995, programs were written to specific operating systems. As someone who went to coding bootcamp in 2020, this seems a little horrifying. I realize that I take ease of access for granted! I particularly enjoyed this quote- "So, all the JVM has to do is run Java programs correctly." It sounds so simple, but any programmer sees the humor in this statement.  

I'm going to make an assumption here, which I know is dangerous. But after reading this article, I believe that Azul (and it's several flavors) are implementations of JVMs. And what I'm learning is that Azul (especially Zing) has very large garbage collectors that ensure shorter pauses. Part of a JVM is "garbage collecting" which is essentially getting rid of unused programs. I really like the simplicity of the terminology there.  

This post may end up being more of a reference for myself, if not just a way for me to work through my new learning in my head. They say the best way to learn is to teach. What I would like to learn next regarding Azul is if it is a production environment like AWS, or if it just facilitates the deployment to multiple platforms and operating systems. I also know that my next step is to learn just how it works- there are several promising YouTube tutorials out there. For tonight, this is where I'll leave it. I'm excited to learn about new aspects of programming, including new technologies. Like I said, if anyone reads this and has any feedback, please reach out- I'd love to benefit from someone else's experience! Until next week! 
