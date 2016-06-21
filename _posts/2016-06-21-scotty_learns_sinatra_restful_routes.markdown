---
layout: post
title:  "Scotty learns Sinatra RESTful Routes"
date:   2016-06-21 13:06:07 +0000
---


Sometimes, reading and understanding are one and the same. Sometimes, I hit a wall and it feels like every sentence on a page is devoid of meaning, the repetition of a word abstracts it into jibberish, and I just hope that by the end of the passage I'll magically understand what just happened. The lab on RESTful routes was one such wall, and, unsurprisingly, I completed the reading with absolutely no idea what I had read. I definitely needed to break it down step by step, and untangle the jumble of words to give them back their meaning and comprehend the lab.

**But first. What are Sinatra RESTful Routes?**
Sinatra RESTful Routes map HTTP verbs (get, post, put, delete, patch) to corresponding controller CRUD actions (Create, Read, Update, Delete).

This provides us with the convention, or a generic flow chart, for handling URLs across the board - whether we're deleting a blog post, creating a recipe, updating a pet inventory, etc.

**My Basic Flow Chart**
I personally found it easiest to walk through the code provided in the [lab](https://learn.co/tracks/full-stack-web-development/sinatra/activerecord/sinatra-restful-routes) and put it into a flow chart. Obviously, this isn't the required order - in the real world, we might want to delete one blog post before editing another, or might edit a blog post before creating a new one.

**INDEX**
First off, let's take a look at all of the blog posts that I've written:

```
get '/posts' do
  @posts = Post.all
  erb :index
end
```

Here, the controller is responding to a HTTP GET request by
    1. establishing an instance variable @posts
    2. READing the 'index' view (which would iterate through and display all of the Post instances stored in our instance variable @posts)


**NEW**
Let's assume I want to CREATE a new post:

```
get '/posts/new' do
  erb :new
end
```

Here, our controller is responding to a HTTP GET request by READing the 'new' view. The 'new' view will contain a form with all of the input fields that allow me to write a blog post, and this form will send a 'post' request to '/posts':

```
#new.erb

<form action="/posts" method="post">
    <h2>Post Name: <input type="text" name="name"></h2><br>
    <h4>Post Content: <input type="text" name="content"></h4><br>
    <input type="submit" value="Submit Post">
</form>
```

Once I've filled out the form and submitted the blog post information, I'll need a controller method to handle the 'post' request:

```
post '/posts' do
  @post = Post.create(:title => params[:title], :content => params[:content])
  redirect to '/posts/#{@post.id}'
end
```

Here, the controller is:
    1. CREATE-ing a new Post based on the params, and saving it as an instance variable @post
    2. redirecting me to the view where I can see my new post in action


**SHOW**
When I CREATEd a new post, my controller redirected me to "/posts/#{@post.id}"... but I don't have a controller action for that HTTP GET request yet. So, I need to build one.

```
get '/posts/:id' do
  @post = Post.find_by_id(params[:id])
  erb :show
end
```

Our controller is responding to the HTTP GET request by, again, establishing an instance variable based on finding a Post with the given params (the id of the newly created post), and then READing the 'show' view:

```
#show.erb

 <h1><%= @post.title %></h1>
 <p><%= @post.content %></p>
```


**EDIT**
Let's say I want to edit a post. I might build a link on the bottom of the 'show' view, which directs me to '/posts/:id/edit'. Once again, I'll need to build a controller action for this route:

```
get '/posts/:id/edit' do
  @post = Post_find_by_id(params[:id])
  erb :edit
end
```

This will READ the 'edit' view, which will include a form with the appropriate post-related fields. Also, since we're editing a post that already exists, I'll go ahead and set the values of the form's inputs equal to the specific post's title, content, etc. 

```
#edit.erb

<form action="/posts/:id" method="post">
  <input id="hidden" type="hidden" name="_method" value="patch">
  
  <input type="text" name="title" value="<%= @post.title %>">
  <input type="text" name="content" value="<%= @post.content %>">
  <input type="submit" value="submit">
</form>
```

Here, I'm sending a patch request to '/posts/:id', which will require a corresponding controller action:

```
patch '/posts/:id' do
  @post = Post.find_by_id(params[:id])
  @post.title = params[:title]
  @post.content = params[:content]
  @post.save
  redirect to "/posts/#{@post.id}"
end
```

First, I'm finding the correct instance of a Post and setting it to my instance variable @post. The following lines UPDATE that specific instance based on the edits I've submitted in the 'edit' form, and then save this post. Lastly, I'm redirecting to that specific post's 'show' page, where I'll see my updated post.


**DELETE**
Lastly, I'll need a way to delete a post I no longer want. I would build a form on the bottom of the 'show' view, which requests the route '/posts/:id/delete':

```
#show.erb

<form action="/posts/:id/delete" method="post">
  <input id="hidden" type="hidden" name="_method" value="delete">
  
  <input type="text" name="title" value="<%= @post.title %>">
  <input type="text" name="content" value="<%= @post.content %>">
  <input type="submit" value="submit">
</form>
```

Once again, this from requires the hidden input field in order to work, and will require a corresponding controller action:

```
get '/posts/:id/delete' do
  @post = Post.find_by_id(params[:id])
  @post.delete
  redirect to '/posts'
end
```

Here, our controller is responding to the HTTP GET request and DELETE-ing the selected post. 

In this way, we've successfully correlated various HTTP verbs to a corresponding CRUD action! I definitely found it easiest to learn these relationships by building this flow chart and examining the conversation between the two actions, looking at it one step at a time. 


