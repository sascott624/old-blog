---
layout: post
title:  "Scotty Builds an Angular SPA with a Rails API backend"
date:   2016-09-07 14:59:53 -0400
---

It's crazy to think that a couple of months ago, the title of this blog would have been absolute jibberish. Angular? SPA? API? Yet here we are. 

This assignment wasn't without its ups and downs. I was excited at the beginning, because I really enjoy coding in Angular - for whatever reason, this language just clicked for me, and I caught on to the ebb and flow of modules, controllers, services etc. fairly quickly. This understanding, coupled with the anticipated magic of watching every piece of the puzzle come together, made me eager to dive in and start coding.

My excitement, however, caused a bit of trouble down the road. When you're programming, it's easy to let your mind wander a little too far, generating ideas faster than you can actually code them. It's all too tempting to run before you walk, even before you crawl. But a solid foundation is a necessary component to any application; without it, you're opening yourself up to frustration down the line.

Enter my final project.

I got so carried away with the angular possibilities (this directive! That filter! Let's add an event here! And we'd use an ng-repeat there!), that I rushed through the rails backend. I had my serializers set up, my routes were RESTful, and my json rendering controllers had the necessary CRUD operations to be functional - or, so I thought.

You can imagine my irritation when my ```$http.patch()``` request wasn't going through. I double, triple checked the Angular documentation on ```$http``` - was it my url? My data? I reconfigured the data I was passing along, checked my controller, my ```$scope```, the ```ng-model```. None of it raised any red flags. I drove myself crazy looking for the root of my problem in all the wrong places.

It wasn't until I decided to walk through the creation of my app from the very beginning that I realized my error. In my recipe controller's update method, I had neglected to locate the specific ```@recipe``` instance I was trying to update. Instead, I had jumped right into ```@recipe.update(recipe_params)``` - rails, of course, could not update something that had yet to be defined, ergo my patch was unsuccessful by default. Once I defined ```@recipe```, everything worked, and my ```$http.patch()``` succeeded.

Like I said, it's easy to get carried away, especially if (like me) you're excited about all of the cool tricks Angular has to offer. But if you don't take the time to crawl before you walk, when it comes time to run, you'll end up tripping.

With this in mind, I'm really looking forward to my next Angular SPA with a RoR backend - and this time, I'll take my time with my controllers ;)
