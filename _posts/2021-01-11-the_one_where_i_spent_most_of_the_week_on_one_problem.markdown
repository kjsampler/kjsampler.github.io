---
layout: post
title:      "The One Where I Spent Most of the Week on One Problem"
date:       2021-01-11 06:15:13 +0000
permalink:  the_one_where_i_spent_most_of_the_week_on_one_problem
---


It's Sunday, and that means that it's time to update everyone on my data science journey! I've been taking a Tableau course through Udemy, and I'm SO impressed- why did I not start playing with this sooner? It's gorgeous. 

Another thing that I tried to focus on this week was making myself go to networking events. It's hard to break through the normal anxiety of meeting with others in your new profession, but I saw a MeetUp from Let's Brew Code that I knew I had to attend - Interview Coding Practice Lab. It was just too perfect. I'm so glad I went. Himanshu is a really incredible host. We didn't just jump straight into practice problems- he actually took the first few minutes to talk about what interviewers expect to see, and how to really tackle these problems in a productive way. 
1. Understand the problem
2. Work through an example, specifically the edge cases
3. Come up with a solution – brute force first, then optimize based on time constraints
4. Start a walk through
5. Code-  make it clean, modular (no duplicates)
6. Run tests

It's important to note that steps 1-4 should all be done before you even start to code. I've heard this before- you should really go into your code with a game plan, rather than making scrappy notes all over the place. You need to stay organized, and really illustrate your train of thought. 

With the steps learned, we were presented with the first problem- "Given a number between 0 and 1,000,000,000,000, spell the number in English." He pointed out, accurately, that the problem doesn't seem too hard at first, but there's edge cases to worry about. With that in mind, I started working through the solution. And working. And working. I've been giving a little bit of time to it each day, but I've definitely spent more time than I'm willing to admit to the internet. 

The way I started was to start making dictionaries in order to spell out the numbers. Obviously 1 through 9, the place dictionary (hundreds, thousands, millions, etc), the "tens" dictionary (twenty, thirty, forty) and my edge cases- the teens. It may be bulky, but I could think of no other way than to give the teens their own dictionary. 
```
my_dict = {0:'zero', 1:'one', 2:'two',
          3:'three', 4:'four', 5:'five',
          6:'six', 7:'seven', 8:'eight',
          9:'nine', 10:'ten'}
place_dict = {1:'trillion', 2:'billion', 3:'million', 4:'thousand', 5:'hundred'}

tens_dict = {2:'twenty', 3:'thirty', 4:'forty',
            5:'fifty', 6:'sixty', 7:'seventy',
            8:'eighty', 9:'ninety'}
teens_dict = {11:'eleven', 12:'twelve', 13:'thirteen',
             14:'fourteen', 15:'fifteen', 16:'sixteen', 17:'seventeen',
             18:'eighteen', 19:'nineteen'}
```

Armed with my dictionaries, I sought to answer the next question - how am I going to account for a trillion numbers? I realized that a trillion is really just four groups of three though. If I could figure out how to account for 0-999, I could just add the word "billion" after it, and move on to the next group of three. So my next question was actually "how am I going to convert an input number into groups of three, keeping in mind that the group of three may start with a zero?"

If you've been reading my blog, you know I love a good function. I wrote one that would first take in the input number, and become a list. Because the zero can only occur in the first two places, I provided that if the number was not divisible by 3, it would add one (or two) zeroes to the beginning. 
```
def divisible_list(list_):
    ''' A function to take in a list and return 
    a list that is divisible by three'''

    if len(list_) % 3 == 2:
        list_.insert(0, 0)
    if len(list_) % 3 == 1:
        list_.insert(0, 0)
        list_.insert(0, 0)
    return list_
		```  
		
So now I have a list that's divisible by three. Next, I wanted to create a list of tuples; each one containing the three values of my 0-999 number. Using a floor division to determine how many tuples to make, and a .pop() function to remove values that have already been accounted for, I was able to create my list of tuples.  

```
def tuple_generator(list_):
    '''A function to take in a list and split 
    the list into tuples in sets of 3'''
    tuples = []
    n = len(list_) // 3
    num_list = []
    for i in range(len(list_)):
        num_list.append(list_[i])
    for t in range(n):
        tuples.append([num_list[t], num_list[t+1], num_list[t+2]])
        num_list.pop(0)
        num_list.pop(0)
    return tuples 
		``` 
		
Himanshu was right - this problem is a lot more complicated than it seems at first blush. My next step is to write the master function - print_english() will take in an integer input, make it divisible by 3, split into tuples and then name each tuple. For the place in the tuple, it needs to also include the place value (hundreds, thousands), and account for the odd men out. I'm thinking of putting individual statements in for the numbers 1 trillion and zero. Again, it's a little bulky, but it does work.  
I've really loved doing these kind of practice problems. I really think they keep your skills sharp, and make you turn to things you may have forgotten- I completely forgot that .pop() exists, and it was one of the very first things I learned. Getting the opportunity to attend a networking event and work with other programmers was really incredible. The event was not limited to Python, so seeing the way other attendees solved the problem in their own language was really awesome. Seeing the way that everyone was willing to help and contribute to solving the problem, regardless of skill level, made me really proud to be a part of this community. 
	
		
