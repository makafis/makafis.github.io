---
layout: post
title: "my first blog post ever and my horrible understanding of regex"
date: 2015-06-16 18:17:24 -0400
comments: true
categories: 
author: Vincent Alfieri
---
"Im going to tell you how I feel before I get into regex.

So far I am loving my time here at Flatiron. It is an amazing experience that I cannot get enough of. Its tough waking up at 5am to get here every morning but I know it is worth it. It is crazy how much material we have covered in only two weeks. I am excited to see what the next few weeks have in store.


Now onto my horrible knowledge of REGEX!

I hate regular expressions with a passion. It is some cryptic language that I have no desire to learn. Sadly, I should learn it soooooo here I am writing my first blog post about a topic I know nothing about. Rather than regurgitate every guide I read I will just share some things that caught my eye.

What is a regular expression? It is a pattern to match in a string.  Sounds simple. Its NOT! 

Here are some rules to follow.
Rule number 1.
We do not talk about Regular Expressions.

Rule number 2. 
We do NOT talk about Regular Expressions.

:)

REGEX is enclosed in //



anything inside of the // will be searched for in a string. For example
/x/ will match all x that appear in the string.
/aeiou/ matches all vowels.
/[^aeiou]/ matches all letters that are not vowels. 



The below statement takes a string of numbers and creates an array with each number having its own place in the array. You could have just called .split("") to get the same answer but regex looks cooler.
> numbers = "1234567"
 => "1234567" 
> numbers.scan(/\d/)
 => ["1", "2", "3", "4", "5", "6", "7"] 
 


 /^\d+/ matches any positive numbers

 /^-\d+/ matches any negative numbers

lets disect this.
^ means at the start of a line
- is a character indicating negative(subtract) character
\d means digits
+ match one or MORE occurances


/[\d]$/ will give you the last number of any digit. So if you type in 50493028 it will match 8.

/a[^aeiou]/ will match any "a" and any letter after it that is NOT a vowel.


a crazy one I found is:
/<script[^>]*>[\w|\t|\r|\W]*</script>/
This finds ALL lines within script inside of an HTML document.  
Sounds good for scraping?


SO BIG DEAL. Why do we need to know all of this random crap when .gsub can do all of this!?!?!?!?! technically you dont but stringing together tons of .gsub can get confusing plus it is an eyesore. I'll tell you.
1. In my previous life when I learned how to work with Oracle databases and PL-SQL I was always told to store a specific type of data in the same format throughout that table. For example. If I store a phone number like this 555-555-5555 that means anyone else who has a phone number in this table must have it stored in that format. It makes it easier so that when we retrieve the data we can easily manipulate it without having to worry about its format. 
2. Validating email addresses. This seems to be the most difficult thing ever for regex. Google knows all.




some awesome websites I have been using are:
http://regexlib.com/
http://www.tutorialspoint.com/ruby/ruby_regular_expressions.htm
http://rubylearning.com/satishtalim/ruby_regular_expressions.html