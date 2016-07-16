---
layout: post
title:  "Scotty Builds a Rails App!"
date:   2016-07-16 17:08:52 +0000
---


Rails has been equal parts exciting and frustrating. Every time I accelerate a level, I'm giddy to see everything I've learned transform from the logic to the "real thing." But as we all know, magic comes with a price. When you're not knee deep in the thicket of code, it's easy to lose track of the why and the how, and just focus on the what. This assessment was a good reminder for me to appreciate magic but respect it's roots.

I ended up using Devise to set up my User and allow for signup/login/logout and, to be honest, I'm on the fence about it. It's a great tool to simplify the sign in process, and provides a handful of useful helpers (where would I be without current_user?), but in some ways it's arguably *too* magical. When it came time to ensure that a user could only update their own profile, designs, etc., I hit a bit of a road block. I knew the logic I needed to incorporate, but either a) thought it had already been done for me through Devise (wrong!) or b) was unsure of where exactly I should implement the code. Whereas if I had built my User on my own, and set up my own authorization process, I would have been entrenched in the sign in flow. I think going back into my Devised user controller and adding these authorizations felt a bit patchy, and not quite as seamless. 

Am I against using Devise? No. I love writing code, even the monotonous sort, but if I'm gifted with a pre-packaged ready-to-use time-saving code, of course I'm going to check it out. That said, I don't think Devise should be relied on exclusively. Use the magic, appreciate the magic, but remember it's source.
