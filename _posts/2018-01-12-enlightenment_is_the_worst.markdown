---
layout: post
title:      "Enlightenment is the Worst"
date:       2018-01-13 01:02:23 +0000
permalink:  enlightenment_is_the_worst
---


> It is paradoxical, yet true, to say, that the more we know, the more ignorant we become in the absolute sense, for it is only through enlightenment that we become conscious of our limitations.  
> -Nikola Tesla

This was my rails project experience in a nutshell. Right now, I feel like a jack of *some* trades when it comes to rails. The further along I got in this project, the more I realized how much more there is to learn. It’s kind of like being in a car with foggy windows and thinking “wow, it feels like we’re really zipping along,” but then you wipe your hand on the window and take a look outside and realize you’re on the struggle bus. 

![](https://media.giphy.com/media/f6ek1KcvTWPmw/giphy.gif)

For example, unhappy with how much logic was in my views I started looking around for the right way to refactor them and stumbled upon decorators. A decorator class is a place to put presentation logic, and I had a lot of conditionals concerned with what to display in a view. Or so I thought. In the end, I was able to refactor a lot of it away without the need for a decorator class, which was good because decorators were surprisingly finicky to implement. But it made me a lot more aware of the single responsibility principle. This excellent [series of posts](http://www.thegreatcodeadventure.com/rails-refactoring-part-i-the-adapter-pattern/) by former Flatiron Instructor Sophie DeBenedetto really helped clarify these ideas. Definitely worth a read.

My rails project really solidified all of the topics that were in the lessons. There were definitely a lot of things in the lessons that I understood, but didn’t know or didn’t recognize the importance of. For example, namespacing resources. 

My app is a wishlist app that allows a user to add a gift that they want to their wishlist. If they if they receive that gift or don’t want it anymore they should be able to remove it. Originally, I put that functionality under the update and destroy actions in the gift controller. I wasn’t concerned about updating or deleting gifts because once they were created they could be added to other users wishlists. I didn’t want one user to be able to delete a gift across the whole site, plus I want lots of gifts in my database so users have to look outside the site less. But there is always future functionality to think about, like if I wanted admins to be able to delete a gift. 

So, the only recourse was to move the current functionality for adding or removing from a wishlist somewhere else. The controller for the wishlist wouldn’t work because it was already concerned with CRUD for the lists themselves. Taking to the google, it was [this article](http://jeromedalbert.com/how-dhh-organizes-his-rails-controllers/) that made all the pieces fall in place. Namespaced or scoped resources allow you to organize everything while emphasizing RESTful architecture. Rather than adding a random route name, I have a wishlists controller that handles how gifts are managed on a wishlist. I can delete a gift, I can delete a wishlist, and I can delete a gift from a wishlist.

```
  namespace :gifts do
    resources :wishlists, only: [:update, :destroy]
  end 
```

As Jerome Dalbert sums up: 

> A lot of people like REST because it is uniform and simple. Once you understand a (truly) RESTful API, it is easier to understand another one. In theory at least: authentication anyone? ;–). The business logic obviously differs between applications so you have to understand it, but how you consume that logic is the same: you create a charge in Stripe (i.e. you take someone’s money), you create an SMS in Twilio (i.e. you send it), you get a repository in Github, etc. You have to bend your mind a little at first to use REST nouns instead of actions: you don’t “pay”, you “create a payment”. You don’t “add funds to your balance”, you “create a fund in a balance”.

This project was a stretch for me and that would be my advice to anyone else starting their rails project: stretch, reach, make it hurt because rails is big and I feel myself becoming more ignorant by the second; but as the Tesla quote at the beginning of this post continues: 

> Precisely one of the most gratifying results of intellectual evolution is the continuous opening up of new and greater prospects.

