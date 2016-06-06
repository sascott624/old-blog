---
layout: post
title:  "Scotty builds a ruby cli gem"
date:   2016-06-06 19:37:00 +0000
---

When I first read through this lab, I was intimated. It's one thing to be walked through a process, or to be told what the end result should look like if you've done it correctly. But building something new entirely from scratch is a different animal. Here are some tips and tricks that helped me through the process:

**1. Prep**
Before writing a single line of code, get your thoughts in order! I found it incredibly helpful to watch [Avi's video walkthrough](https://www.youtube.com/watch?v=_lDExWIhYKI) first, and then read through [the final code](https://github.com/learn-co-curriculum/daily_deal). Then, I would more or less follow these steps:

**2. Brainstorm** - *What are some things that interest you? In a perfect world, what would you want to build? How do you think you'd go about doing that?*

My brainstorm produced a few ideas, but at the end of the day, I thought I really only had one that met all of the requirements of the lab. I decided to build a Deities Generator that would scrape a webpage to produce a list of Greek deities, and then provide more information on each.
 
**3. Plan** - *What does the final version of this project look like? What about the simplest version? What are the major stepping stones between the two?*

I knew that I wanted the final version of my project to instantiate deity objects with attributes such as their name, domain, symbols, etc. All of that information would have to be scraped from a website (in my case, multiple websites). So I knew I'd want a CLI module, a Deities module to instantiate Deity objects, and a Scraper module to scrape the websites, and they would all have to communicate with each other. In order to get there, it was definitely crucial to take baby steps - build something simple, and elaborate. Which led me to....

**4. Branch** - *Based on your planning, what might your tree look like? What story will your commits tell?*

I started by building the basic skeleton of what my code would look like. What files/directories did I need, where did they live, what did my environment require, etc. I knew I'd need pry and nokogiri, so I went ahead and added those to my environment.rb file. I also set up my notes.md, which was a very rough guideline, but helped me keep my thoughts in order.

**5. Build** - *Again, start with the simplest version of your code, then flesh it out. Gradually increase in complexity, until you're satisfied with the end result*

With the foundations I had established in the "Branch" phase, I started simple - I built only the CLI methods. My CLI didn't call on objects or scrape any html, but it did greet the user, print a menu, and "respond" to a user menu selection with a corresponding hard-coded string. Once Deities::CLI was underway, I built Deities::Gods. Again, I didn't actually create objects or scrape - I just wanted to make sure that Deity::CLI could talk to Deity::Gods and spit out the strings I wanted. That led to some initial scrapes to get some of the simplest information from the html - the deity names. Once I was comfortable with Deities::CLI, Deities::Gods, and Deities::Scraper, and their necessary communication, I decided it was time to start creating deity objects, and giving them some attributes.

Once I had all of the information I wanted stored within each of the Deity objects, all that really remained was to tweak some of the loops in my initial menu to make the CLI more user friendly. And now we have a new gem! As intimidating as it was in the beginning, it was incredibly gratifying to utilize the skills I've been learning and actually create something on my own. It was more encouraging and reaffirming than I would have guessed, and made me more comfortable examining and questioning other codes. It also proved the necessity of taking baby steps! Check your code before moving on - it's easier to fix a problem the first time it pops up, than to backtrack and retrace your steps to identify the root cause.
