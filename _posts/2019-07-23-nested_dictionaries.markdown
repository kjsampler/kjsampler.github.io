---
layout: post
title:      "Nested Dictionaries "
date:       2019-07-23 06:47:37 -0400
permalink:  nested_dictionaries
---


For this post, I'll be talking a little bit about nested dictionaries and how to manipulate them. Of course, to make it fun, I wrote my own dictionary about... my pets! So, to start with, here is our original dictionary: 
```
my_pets = {'Natasha': {'species': 'cat', 'age': '4', 'color': 'brown'},
           'Lyla': {'species': 'cat', 'age': '7', 'color' : 'calico'},
           'Copper': {'species': 'dog', 'age': '1', 'color': 'brown'}}
```
So the first thing I want to do, both as part of a tutorial and as a sanity check- is pull information from my dictionary. 
```
my_pets['Natasha']
```
returns 
```
{'species': 'cat', 'age': '4', 'color': 'brown'}
```


```
my_pets['Lyla']['color']
```
returns
```
'calico'
```

So far, everything seems to be in working order. So the next thing I want to do is start experimenting with my dictionary, and seeing what uses it can be to me. To understand this, I'll tutorialize a couple questions that showcase the usefulness of nested dictionaries. 

Question 1: Suppose I got another dog; how would I had him into the dictionary? Delete when finished

```
my_pets['new_dog'] = {'species':'dog', 'age': '4', 'color':'black'}
```
So this question is actually not so hard. First we want to call the dictionary. To create a new entry in the dictionary, we use square brackets around the new entry; in this case ['new_dog']. After that, we want to set this new entry equal to our information, which should match the previous information in the dictionary. That explains our ={'species':'dog', 'age': '4', 'color':'black'}. 

In order to delete the new_dog, we will use .pop(). When nothing is specified in the .pop() parameters, it will delete the last item from the dictionary, in this case 'new_dog'. Because we know what we want to delete, I will be specifying which entry I want to delete. 
```
my_pets.pop('new_dog')
```
And just like that, the new_dog entry is deleted. 
``` 
my_pets
```
returns 
```
{'Natasha': {'species': 'cat', 'age': '4', 'color': 'brown'},
 'Lyla': {'species': 'cat', 'age': '7', 'color': 'calico'},
 'Copper': {'species': 'dog', 'age': '1', 'color': 'brown'}}
 ```


Question 2: What if I wanted to see all pets who were brown in color?

The first thing to know about this question is that it requires a for loop. We need to iterate over every entry to check for 'color':'brown'.  In other words, for each pet in my_pets, if 'color' is brown, we want to add the animal to a list. The code for that looks like this:
```
brown_pets = []

for pet in my_pets:
   if my_pets[pet]['color'] == 'brown':
        brown_pets.append([pet])
	```
	
	Which will return Natasha and Copper. 


Question 3: I want a list of tuples that lists each cat's names and their species- How would I do that? 

The answer is with another for loop! First we want to iterate and see if the animal is a cat, then we want to add each cat's name and species to a list of tuples. In order to make a list of tuples, we just enclose what we want in the tuple in square brackets. 

```
cats = []

for pet in my_pets:
    if my_pets[pet]['species'] == 'cat':
        cats.append([pet, my_pets[pet]['species']])
	```

When I print cats, this is the output:
```
[['Natasha', 'cat'], ['Lyla', 'cat']]
```

Question 4: Order the dictionary alphabetically. 

The easiest way to accomplish this is with the .sorted() method. It actually makes it quite simple- 
```
sorted(my_pets.items())
```

Depending on what you're trying to accomplish, it is important to include .items(). Without it, you just get an ordered list of the pets' names. With .items(), you get not only the names, but also the inner dictionary information. 

There you have it! I know it may seem like a simple topic, but nested dictionaries can actually get quite complex. It's better to have these foundations down pat than to only somewhat understand and try to move on. I quite enjoyed this look into nested dictionaries, and I hope you did too! 

