---
layout: post
category : phoenix
tagline: ""
published: true
tags : [elixir, phoenix]
---
{% include JB/setup %}

# Implementing Feature Folders in Phoenix

After years on the .net platform, I've recently started learning Elixir and Phoenix. One of the practices I want to bring over with me 
is the concept of Feature Folders in an MVC application.

## Default MVC Folders 

By default, Phoenix applications order code by type. For example, all _models_, _views_ and _controllers_ are kept together in their respective folders. Running

	mix phoenix.new my_app
	
results in a folder structure like this:

	/web/models/
	/web/views/
	/web/controllers/

The advantage of this folder structure is that it is a simple, easy to understand convention and is quite common across platforms. However,  [Christian Weiss](http://www.chwe.at/2014/04/introducing-the-asp.net-mvc-feature-folders-project-structure) asks a great question:

> Which of these requirements is more common?
> 
> * Change something in every view, controller or model of your project
> * Add a new field to your model X, show this field to the user, make it editable, the value must be validated against some fancy rules, …

In my experience, I can count on one hand the number of times in my career I've wanted to look at all _controllers_ together, or all _models_ together. This type-structure seems to be optimised for a use case that rarely exists. Instead, I want to see the code related to the feature I am working on. 

## Feature Folders

The concept of feature folders is simply that you organise your code by features, rather than by types. To use a real example, I'm going to use the application built in the excellent Programming Phoenix book. This app allows a user to register with the site, add videos to their account and view and annotate these videos in real time. 
Organising the project structure by features might look something like this:

	authentication/ #logging in, authenticating requests etc..
	membership/ #registering with the site, viewing account etc.
	video_viewer/ #the main app, viewing and annotating videos
		video_viewer_controller.ex
		video_viewer_view.ex
		video_channel.ex
		video_viewer.html.eex
		annotation_view.ex
	admin/videos/ #managing your videos

When working on, for example, the video viewer functionality, I have  all pieces of the puzzle together in the same folder. I'm not having to jump around between `contollers` and `views` and `models` folders just to find the pieces related to viewing videos. 

So how do you accomplish this in Phoenix? Well, it's very simple, thanks to the extensibility of the framework

# Setting up Phoenix for Feature Folders

The only change we're going to make is to tell Phoenix to locate the templates for views inside our feature folder. That's it. We're going to use the `video_viewer` feature from above for our example.

## Default Behaviour

How does Phoenix know where to look for our templates? When we generate a project using `mix phoenix.new` a number of helper files are created for us, one of which is `web.ex`. Inside this is a `view` function:

``` elixir
def view do
    quote do
      use Phoenix.View, root: "web/templates"

      # Import convenience functions from controllers
      import Phoenix.Controller, only: [get_csrf_token: 0, get_flash: 2, view_module: 1]

      # Use all HTML functionality (forms, tags, etc)
      use Phoenix.HTML

      import MyApp.Router.Helpers
      import MyApp.ErrorHelpers
      import MyApp.Gettext
    end
  end
```

Note the `use Phoenix.View, root: "web/templates"` line. This `view` function is, by default, used from our `*_view.ex` files:

``` elixir
defmodule MyApp.VideoViewerView do
  use MyApp.Web, :view
end
```
`use` requires the given module and then calls the `__using__/1` callback on it allowing the module to inject some code into the current context. `__using__/1` is defined in the generated `web.ex` file as:

``` elixir
  defmacro __using__(which) when is_atom(which) do
    apply(__MODULE__, which, [])
  end
```
As you can see, it takes an atom that defines the function to apply and passes an empty array as the last parameter to `apply/3`. So by having `use MyApp.Web, :view` in our `*_view.ex` files, we are saying "use the view function in web.ex, don't pass in any arguments and use "web/templates" as the root for templates."

## Implementing Feature Folders 

In order to have implement our desired behaviour we need to:

* accept some options in our `view` function in `web.ex` and pass them to `Phoenix.View`
* pass these options in from our `*_view.ex` files
* hook it together by way of `__apply__/1`

Let start by allowing some options to be passed into our `view` function:

``` elixir
def view(opts \\ [root: "web/templates"]) do
    quote do
      use Phoenix.View, unquote(opts)

      #....rest of code unchanged
    end
  end
```

Here we allow `opts` to be passed into the function, defaulting to "web/templates" if not used. This maintains backwards compatability with the existing convention. 

Next, we need to know what options to pass in from our `*_view.ex` files.  Our `opts` will get passed to `Phoenix.View` which accepts `:root`, `:path`, `:namespace` and `:pattern` options. The two we are interested in are `:root` and `:path`. The docs state:

* `:root` - the template root to find templates
* `:path` - the optional path to search for templates within the `:root`. Defaults to the underscored view module name. A blank string may be provided to use the `:root` path directly as the template lookup path.

Given our requirements of locating the template files in the feature folder, we need our `:root` to be the path to the folder and our `:path` to be an empty string in order to override the default:

``` elixir
defmodule MyApp.VideoViewerView do
  use MyApp.Web, {:view, %{root: "web/video_viewer", path: ""}}
end
```

We now need to hook this in via the `__using__/1` function in `web.ex`. We can take advantage of pattern matching and define a new definition as follows:

``` elixir
  # original
  defmacro __using__(which) when is_atom(which) do
    apply(__MODULE__, which, [])
  end
  # new
  defmacro __using__({which, opts}) do
    apply(__MODULE__, which, [opts])
  end
```
Again, we maintain backwards compatability by keeping the existing `__using__` definition and adding a new one that expects a tuple of `{which, opts}`. Notice that in our new definition we are passing the options in the final parameter to `apply/3` - these will then get passed to `Phoenix.View` by way of our `view` function above. 

With these changes we should now be able to move our code into feature folders! When creating new feature folders, the only thing we need to remember to do is set the `:root` and `:path` options in our view files `use MyApp.Web` call.


### Source code

I've made changes to the `rumbl` app from Programming Phoenix at https://github.com/tomliversidge/elixir-rumbl 