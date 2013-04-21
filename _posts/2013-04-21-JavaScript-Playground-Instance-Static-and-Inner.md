---
layout: post
category : JavaScript
tagline: ""
published: true
tags : [JavaScript]
---
{% include JB/setup %}

#Instance, Static and Private functions

As part of my goal of "levelling up" in JavaScript I'm going to be writing a series of posts covering some basic concepts that are important to understand when trying to master the language. There is nothing new here - just a way of me recording my own understanding of the concepts. This first post is going to look at the different accessors for JavaScript functions.

##Instance functions

	var Robot = function() {
	    this.hello = function() {
	        return "Hello from Instance";
	    };
	};

In the above code, Robot is a constructor function that has an instance function called "hello" that would be called with the following code: 

	var robot = new Robot();
	robot.hello(); // "Hello from Instance"

##Static functions

We can add the equivalent of a static function to the above example by doing the following:

	Robot.hello = function () {
	    return "Hello from Static";
	};

Now we can call this directly from the Robot object without creating an instance of Robot:
	
	Robot.hello(); // "Hello from Static"

Note that we can still use the instance hello function as before:

	var robot = new Robot();
	robot.hello(); // "Hello from Instance"
	Robot.hello(); // "Hello from Static"

##Private functions

We can also add private functions to our Robot

	var Robot = function() {
	    this.hello = function() {
	        return "Hello from Instance";
	    };
		// private
	    function hello() {
	        return "Hello from private inner function";
	    }
	};

In this example, the private hello function will not be called by either of our previous usages:

  	var robot = new Robot();
	robot.hello(); // "Hello from Instance"
	Robot.hello(); // "Hello from Static"

###Exposing private functions
If we did want it to called, we would have to expose it

	var Robot = function() {
	    this.hello = function() {
	        return "Hello from Instance";
	    };
	
	    function hello() {
	        return "Hello from private inner function";
	    }
	
	    this.helloFromInner = function() {
	        return hello();
	    };
	};

Which results in:

	var robot = new Robot();
	robot.hello(); // "Hello from Instance"
	Robot.hello(); // "Hello from Static"
	robot.helloFromInner(); // "Hello from private inner function"

You might be wondering what the point is of exposing the private function like this, but this private function could be doing a lot more than what this example shows, maybe using other private functions and variables or a complicated calculation. Exposing private functions is a way of exposing a public API on your object whilst encapsulating private functionality.

##Prototype

What happens when we add a hello method to the prototype?

	Robot.prototype.hello = function() {
	    return "Hello from prototype";
	};
	var robot = new Robot();
	robot.hello(); // "Hello from Instance"
	Robot.hello(); // "Hello from Static"

The instance-level method takes priority on the robot.hello() call and the static Robot.hello() call ignores the prototype. If we remove the instance-level hello() function

	var Robot = function() {
	    // instance function removed

	    function hello() {
	        return "Hello from private inner function";
	    }
	
	    this.helloFromInner = function() {
	        return hello();
	    };
	};
	
	Robot.hello = function () {
	    return "Hello from Static";
	};
	
	Robot.prototype.hello = function() {
	    return "Hello from prototype";
	};

then the hello() call on the instance of a Robot will use the method on the prototype:

	var robot = new Robot();
	robot.hello(); // "Hello from prototype"

#Summary

This has been a really simple introduction to the different access modifiers in JavaScript. In a future blog post I'll be expanding on these basic concepts and having a look at more advanced usage scenarios. 