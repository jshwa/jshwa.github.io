---
layout: post
title:      "Disney Rides - CLI Data Gem"
date:       2017-11-25 00:49:31 +0000
permalink:  disney_rides_-_cli_data_gem
---

Let me start off by saying I’m not the biggest fan of Disney, and I’m even less a fan of their parks. There are definitely franchises that I like, Indiana Jones, TRON, and now Star Wars. But do I want to wait in line for literally hours for a couple minutes on a themed ride? Definitely not. My fiancée, on the other hand, has a much more diverse appreciation for Disney, and when I told her about the project she immediately suggested Disney rides. I wasn’t thrilled, but when I quickly looked over the Disney site it actually seemed like a good candidate. 

Peter Bell gave a lot of great advice in the orientation, and one of the things he said was when it comes to the first project just start working. I’m really glad he said that, too, because I’m someone who will take forever to make a decision on stuff like this because I want it to be amazing and groundbreaking and perfect. 
> 
> Tips/Aside - Building the Gem
> 
> I just used bundler to build the gem. The [bundler site](http://https://bundler.io/v1.12/guides/creating_gem.html) is great for getting started, just stop reading before “Testing a command line interface” because that is not the kind of CLI you want for this project. I spent some time messing with Thor, and that’s a whole different rabbit hole.

So, I built a program that would scrape the Disney site for all of the rides, sort them by various qualities depending on what the user wanted. The rides had attributes like whether Fastpass was available (where you can go to the ride early and get a ticket for later so you show up at an appointed time and wait in a shorter line), and “thrill level” and “height” and “park.” Which was where I ran into my first issue. Despite having been to 2 of them, I did not understand how Disney Resorts work.

Originally, I was just scraping the Disney World site. It had 160 rides and different parks, so I thought that was the whole world. No, it turns out each resort has multiple parks; Disney World is Disney World, not Disneyland (which I guess I always knew were different), nor Disney Shanghai, Hong Kong, Paris, Hawai’i or Tokyo. 

Once I realized this, I looked around and most of the other resorts’ sites were built the same so I figured if one worked, they’d all work. I kept going on the Disney World site. I thought through and built out a bunch of the classes for the attributes to each ride. They were pretty straightforward using similar methods from the labs, so on to the scraping. Next issue: 

AJAX

Disney, of COURSE, doesn’t just load some HTML and CSS and call it a day. They load their ride list with AJAX, I guess because it has options for filtering and sorting the rides on the page. It was really confusing when Nokogiri is telling me the css I want doesn't exist and I’m looking at it in the developer window in chrome.

![](https://media.giphy.com/media/EouEzI5bBR8uk/giphy.gif)

Since open-uri isn’t a browser it can’t load javascript. And since the ride info only loads with javascript nokogiri doesn’t get the stuff I’m seeing. So that sucks. 

After consulting the interwebs for a bit it seemed like Watir was my best bet. It’s a gem that loads a browser so the javascript loads, then you can pull the HTML and pass it to nokogiri. I think there are other options (I hope there are, because this one isn’t great), but all the people who seemed to know about them were either bluffing or trying to Miyagi the OP because giving useful advice they were not. 

Anyway, that’s it. A couple big issues. I had to do some thinking about how the classes were interacting, but it all worked out. If you want to check out the gem you can find it here.

At least now I don’t have to see the Disney site anymore when I want to look for a ride. Ha, jk, Watir pulls it up every time I run the program.

