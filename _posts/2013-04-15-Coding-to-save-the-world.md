---
layout: post
category : misc
tagline: "quickly"
published: true
tags : [stargate, writers]
---
{% include JB/setup %}

#How coding is done in totally awesome high stake scenarios

I have someone new to blame for my latest crazy deadline. This time it is Hollywood writers. They have poluted the minds of the common consciousness. This occurred to me watching an episode of Stargate SG1. In this particular episode, Earth was under attack from the Goa'uld Anubis. To cut a long story short, SG1 had to fly the Stargate out into space. There was however, a serious problem. They needed to activate the hyperdrive in-atmosphere, something the sub routine wasn't designed to do. BUT THAT DOESNT MATTER - "we can write and upload a new sub-routine" Colonol Carter enthused. "It will be ready in a couple of minutes". 

Thank you and all the other films and TV shows that spread this meme.

There are a number of things that Colonol Carter forgot about when promising this:

1. We are on a fixed-price contract here, so this needs to be considered as a change request. Using the hyperdrive in the upper atmosphere with an unstable stargate was NOT in the original spec.  We are going to need the new feature to be fully signed off before we begin to implement the functionality.
2. This needs to be properly specified and added to the backlog of tasks. Now granted that it is of high importance, as the Earth will be destroyed in around 5 minutes, but lets not abandon our discipline just because we have a tight deadline. 
3. We are probably going to have to refactor the code base as we YAGNI-ed the hell out of the sub-module replacement suggestion.
4. Has anyone mentioned this to the test team? 
5. The build server is a bit busy right now building the coffee-cam app. It's running on the master node as coffee takes priority. 
6. Do we have any resource for this?

I'm going to write the sub-module now. 

	CanFlyInAtmosphere = true;

WHOO HOO!!! GO SG1! :)
