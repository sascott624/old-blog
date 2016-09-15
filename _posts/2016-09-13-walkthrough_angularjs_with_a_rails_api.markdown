---
layout: post
title:  "Walkthrough: AngularJS with a Rails API"
date:   2016-09-14 17:18:00 -0000
---

There are a lot of small, but necessary steps required to get a new app up and running. If - like me - you are excited to play around with Angular, it's easy to let your eagerness obstruct your apps foundations! So, I decided to write out a step by step guide to getting your app up and running and ready for front end functionality.

N.B. - I didn't set up any schema, migrations, or any of the back end data. This walkthrough is simply to get your Rails app up and running and ready to support an AngularJS front end!


# SETUP #

First and foremost, I like to set up my Rails API. I know some people prefer to work in the opposite manner (creating the front end first), but I like to build from the bottom up.

```cd``` into the directory where you'd like to save your app, and enter ```rails new <YOUR_APP_NAME>``` to create the default Rails file structure (don't forget to ```cd``` into your app's directory!)

# DEPENDENCIES #

Now, add the following gems to your Gemfile:

``` 
gem 'angular-rails-templates'
```

I also like to remove the ```coffee-rails``` and ```turbolinks``` at this point.

Then run ```bundle install```

You'll also need to include angular.js, angular-ui-router.js (if you're using ui-router), and angular-rails-templates.js either via ```<script>``` tags linking the CDNs, or by downloading and hosting the files locally.

I downloaded the files and stored under <em>your-app-name/app/assets/javascripts</em>, and included in my manifest:

<em># your-app-name/app/assets/javascripts/application.js</em>

```
//= require angular
//= require angular-ui-router
//= require angular-rails-templates
```

## BEGIN ANGULAR SETUP ##

I like to make a separate controller with just an index method in order to render all of our Angular routes/states:

<em># your-app-name/app/controllers/your-app-name_controller.rb</em>

```
class YourAppNameController < ApplicationController

  def index
  end
  
end
```

then, in our <em>config/routes.rb</em>, we identify the above page as our root:

```root to: 'your_app_name#index'```

finally, in <em>app/views/your-app-name/index.html.erb</em>, we add our angular view:

```<ui-view> </ui-view>```

(or ```<ng-view> </ng-view>``` if you're using ng-route)

Don't forget to include ```ng-app``` and remove turbolinks from the html in <em>your-app-name/app/views/layouts/application.html.erb</em>:

```
<!DOCTYPE html>
<html>
  <head>
    <title>TestApp</title>
    <%= csrf_meta_tags %>

    <%= stylesheet_link_tag    'application', media: 'all' %>
    <%= javascript_include_tag 'application'%>
  </head>

  <body ng-app='app'>
    <%= yield %>
  </body>
</html>
```

Now, let's define our ```app``` module in your-app-name/app/assets/javascripts/app.js:

```
angular
    .module('app', ['templates', 'ui.router'])
    .config(function($httpProvider, $authProvider) {

        // for CSRF errors
        $httpProvider.defaults.headers.common['X-CSRF-Token'] = $('meta[name=csrf-token]').attr('content');

        $httpProvider.defaults.headers.patch = {
          'Content-Type': 'application/json;charset=utf-8'
        };

    });
```

Time to set up a home state. I like to keep all of my angular routes/states organized in a separate file:

<em># your-app-name/app/assets/javascripts/routes.js</em>

```
angular
    .module('app')
    .config(function($urlRouterProvider, $stateProvider) {
      $stateProvider
        .state('home', {
          url: '/home',
          templateUrl: 'home/home.html',
          controller: 'HomeController as vm'
        })
    });
```

and we'll go ahead and create the ```home``` directory, which houses our ```home.controller.js``` and ```home.html``` files:

```
function HomeController() {
    var ctrl = this;
    ctrl.name = 'YOUR-NAME-HERE!';
}

angular
    .module('app')
    .controller('HomeController', HomeController)
```

Now, enter ```<h1>Hi {{vm.name}}!</h1>``` into ```home.html```, and run ```rails s```

If you browse to ```localhost:3000```, you should be greeted by name!

From here, you're all set to build on your app. I'll write a few follow up posts regarding setting up your database/schema/migrations, leveraging Active Model Serializers to render appropriate JSON, and authenticating with Angular and your Rails API, but for now, this is a solid foundation to build out an Angular UI!
