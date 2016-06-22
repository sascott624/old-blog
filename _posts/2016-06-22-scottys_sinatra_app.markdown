---
layout: post
title:  "Scotty's Sinatra App"
date:   2016-06-22 14:03:43 +0000
---

Building my own sinatra mvc CRUD app was a lot more intuitive than I initially thought it would be. I think it was helpful to organize the flow of controller requests and views in a manner that made sense to me, as opposed to some of the previous labs where the routes were pre-determined. As a result, I'm really happy with what I built, and felt like my understanding of the correlation between HTTP verbs and CRUD actions was solidified.

First, when I had settled on building a "Routines and Tasks" tracker, I started with the basic table structure. I knew that I would need models for Users, Routines, and Tasks, and that routines would belong to a user, and routines and tasks would have a many to many relationship requiring a join table. What I didn't realize at the onset, though, was that I would also need to create a model for Days. In my app, a Routine has Days of the week on which it is done, as well as a list of associated tasks, but I incorrectly assumed it'd be just as well for me to make days as strings and push them into an empty Routine.days array. Unfortunately, about halfway through building my app (specifically when I was iterating over the days of the week and associating those days to a specific routine) I realized that it would be necessary to build Day models, and would therefor need a days table and its relationship to Users, Routines, and Tasks.

So, I started over, creating all of my previous tables/models, and adding a secondary many to many relatinoship between Routines and Days through a join table routine_days. In this way, when it came time to instantiate or edit a routine, I could associate it to any number of Days.

I more or less followed the flow chart I had elaborated on in my previous blog post, which provided a sensical order in which to view the catch-and-receive of various views, forms, and controller actions. 

With my models set up, it was really a question of fine-tuning my pages and controller actions, ensuring that I remembered to verify that a user was signed in before showing a page, and getting the correct routes within the correct controller, and keeping track of my commits! I ended up with four controllers with four distinct areas of responsibility: ApplicationController, UsersController, RoutinesController, and TasksController. A user could sign up or login, view an index of available tasks, create a new task, view his/her routines, edit these routines, delete these routines, and logout. I also added error messages advising that routines cannot be created without a name, and that users cannot signup without a username/email. 

I'm really happy with what I've built - I know it's only just scratched the surface of possibilities, but everything I've learned so far is starting to take shape in a real-world applicable way, and that's very exciting!

