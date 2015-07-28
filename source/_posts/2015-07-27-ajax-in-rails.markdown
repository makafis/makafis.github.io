---
layout: post
title: "Ajax in Rails"
date: 2015-07-27 22:37:57 -0400
comments: true
categories: 
---


Ajax is awesome. It lets you make cool things happen on your page without any need to reload your website. It increases the user experience and makes your app more interactive and appear magical. Luckily with Rails we do not have to exhaust ourselves with writing the same pattern of Ajax code over and over. Rails does it for us!

<img src="http://img.gawkerassets.com/img/17bya5m22xknejpg/original.jpg" alt="Clappy Cat">

<h3>Basic flow of Ajax</h3>
<ol>
    <li>A Trigger Fires (such as a button click or link click).</li>
    <li>The Browser calls the server by sending the data that belongs to the trigger that fired.</li>
    <li>Server processes the data and sends back an HTML string.</li>
    <li>Browser receives our response and updates the specified part of the HTML code.</li>
</ol>



In a Rails Form we can mark it with remote: true which automatically submits the form via Ajax rather than by the normal submit instructions. You can even add the remote: true to a link_to and button_to action.


Here is an example of a form_for in Rails:
``` ruby
<%= form_for(@person, remote: true) do |f| %>
  ...
<% end %>
```
Creates the following HTML code:
``` html
<form accept-charset="UTF-8" action="/articles" class="new_article" data-remote="true" id="new_article" method="post">
  ...
</form>
```


Here is an example of a link_to in Rails:
``` ruby
<%= link_to "a person", @person, remote: true %>
``` 
Creates the following HTML code:
``` ruby
<a href="/people/1" data-remote="true">a person</a>
```

With the data-remote="true" the form will now be submitted via Ajax.

<h3>Server Side</h3>

The only thing we really have to do is take care of the Ajax request on our server. To do this you add a respond_to block inside of your controller. You must then create a new .js.erb view to hold your javascript code. Using partials is extremely helpful since you will typically replace one <div> of HTML code with your response. Returning a partial lets construct your HTML code in Ruby rather than creating a long HTML string.

``` ruby
  respond_to do |format|
    # if the response fomat is HTML, redirect as usual. 
    #This is great for those people who disable JS......
    format.html { redirect_to root_path } 

    # if the response format is JS we will have specific
    # instructions on how to handle the response.
    format.js { }
  end
```


Thats really all you have to do. Quite amazing I know. 











Sources: https://github.com/rails/jquery-ujs/wiki/ajax
http://www.tutorialspoint.com/ruby-on-rails/rails-and-ajax.htm