---
layout: post
title: "Form Helpers"
date: 2015-07-15 08:11:08 -0400
comments: true
categories: 
---


So I am a week into Rails and I have little grasp on exactly what I can do with these forms. If Rails generates the HTML in our forms then we should be able to generate anything that you can write in HTML. Form Helpers are great for that. There are many different helpers that you can use to gather user input.

Well lets start with the obvious. Form Helpers help you make forms!!
form_for and form_tag are the two ways you can generate forms through Rails.






Below is a list of some useful helpers that allow you to specify the types of data you expect from the user.

password_field – Simple, makes your text box have the little password dots. 
``` ruby
<%= f.password_field :name%>
```
email_field – Lets you accept an email address where if a user types in www.google.com you will get http://www.google.com 
``` ruby
<%= f.email_field :website %>
```
number_field – This is really cool. It creates a number field where you can set minimum, maximum, and ranges.  Extremely useful if you want users to select a QTY in their cart but not to exceed a certain amount.
range_field


collection_select – create a drop down list to choose from.

``` ruby
<%= f.collection_select :tag_ids, Tag.all, :id, :name, include_blank: true %>
```
 

Those are only a few that I think I will be using a lot in the future.

Guess what.... I can now write some kick ass HTML without even knowing HTML!! 

<img src="http://www.quickmeme.com/img/2a/2a4ac1cee5f34a3bc2c4e501ea90810fdb90e39cb12b46b67a0d545c1058d6c3.jpg" alt="">

