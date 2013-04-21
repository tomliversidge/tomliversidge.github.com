---
layout: post
category : JavaScript
tagline: ""
published: false
tags : [JavaScript]
---
{% include JB/setup %}

#What is this?

this.whatAmI? In JavaScript, 'this' is often a source of confusion. It is important to understand that 'this' is implicitly passed to a function. Because of this, when a function is invoked, 'this' provides the context of the function. However, what 'this' is actually depends on how the function is invoked.

The following code simply invokes a function that returns 'this':

	function getThis () { return this; }
	getThis(); // will be the global context, usually window

Assigning the function to a variable produces the same result:

	var assignedToVariable = getThis;
	assignedToVariable(); // will be the global context, usually window

##Method functions

Functions can be thought of as methods if they belong to an object. Take the following code, that assigns a method to an object property:

	var anObject = { getThis : getThis};
	anObject.getThis() === anObject; // true

In this case, 'this' refers to the object. Technically, this is exactly what we have seen previously, where both the getThis() function and the variable "assignedToVariable" are implicitly assigned to the global object. The same process applies to namespaced objects: 

	anObject.anotherObject = { getThis : getThis };
	anObject.anotherObject.getThis() === anObject.anotherObject; // true

The important point to take away from this is that the same function is used in all the examples, **but the value of 'this' changes depending on where the function is invoked**. 

##Assigning the function context

Every function has a call and apply method. These methods take a function as the first parameter and apply the context to the passed in function. 

	getThis.call(contextReceiver) === contextReceiver;
	getThis.apply(contextReceiver) === contextReceiver; 