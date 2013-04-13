---
layout: post
category : coding
tagline: "interview"
published: false
tags : [kata, interviews]
---
{% include JB/setup %}

#Interviewing and recruiting 

Over the past three or four years I have both interviewed prospective employees for companies I have worked for and been an interviewee on numerous occasions. Recent changes in both my current circumstances and movement at my employer has given thought to the different approaches to identifying suitable candidates. Most companies seem to employ a combination of the following:

* Telephone interview
* Technical interview
* Advanced code test
* On the day code test
* General interview

The goal is to identify good developers who will fit into the organisation. I think all of the approaches above have their strengths and weaknesses, but I want to focus on code tests for this particular blog post, and in particular, the use of code katas for technical tests. If you are not familiar with the concept, here is what Wikipedia has to say: 

> A kata is an exercise in karate where you repeat a form many, many times, making little improvements in each. The intent behind code kata is similar. Each is a short exercise (perhaps 30 minutes to an hour long). Some involve programming, and can be coded in many different ways. Some are open ended, and involve thinking about the issues behind programming. These are unlikely to have a single correct answer. You need to try it as many times as it takes, and be comfortable making mistakes. You need to look for feedback each time so you can work to improve. There needs to be no pressure: this is why it is hard to practice in a project environment. it helps to keep it fun: make small steps forward when you can. Finally, you’ll recognize a good practice session because you’ll came out of it knowing more than when you went in. Remember that the point of the kata is not arriving at a correct answer. The point is the stuff you learn along the way. [[reference](http://codekata.pragprog.com/2007/01/code_kata_backg.html#more)]

The code kata involves a task to complete, often with a paired programmer and an observer to watch how you perform. Some examples of katas can be found [here](http://codekata.pragprog.com/).

##Initial thoughts 

My initial thought when I heard about these being used in interviews was that the whole ethos of a kata seems at odds with the typical interview environment. According to the above description, you need to feel comfortable making mistakes in a pressure-free environment. So.... lets do them in an interview! :) I think most companies are just looking for a way to try and get a feel for how developers approach a problem and as a way of actually seeing someone code. They offer a way of seeing how a developer performs a given task under pressure. I'd personally like them not to be *called* katas when done in interviews - lets just call them code tests.  

##Context

From my own experience of code katas in interviews, I have learnt that I perform best when I am familiar with the domain at hand. For me, context is king. If I already understand a domain, or have time to learn it I perform well. If the domain is new to me I tend to struggle. 

One kata I performed successfully (and I am judging success on whether I was offered the job!!) is the [Bowling Kata](http://codingdojo.org/cgi-bin/wiki.pl?KataBowling). In this kata, you have to 
> Create a program, which, given a valid sequence of rolls for one line of American Ten-Pin Bowling, produces the total score for the game 

I am immediately familiar with the problem domain. I've been bowling many times. I've even hit a few strikes. I've seen Kingpin more than once. I knew what was expected of me and could settle into the actual coding exercise. 

Another example is the [Roman Numeral Kata](http://codingdojo.org/cgi-bin/wiki.pl?KataRomanNumerals):

> Write a function to convert from normal numbers to Roman Numerals: eg

     1 --> I
     10 --> X
     7 --> VII

Again, I am familiar with this concept. I know what Roman Numerals are. I've experimented with list styles in Word. I watch Spartacus. I already understand the task well. 

For both these katas, I am familiar with the concepts and the problems involved. This makes it much easier to perform a coding task under the pressure of an interview situation. I don't have to think about the concepts, only how to write some code to solve the task at hand. 

Contrast this to a kata where the context <del>[is](http://tom.liversidge.me/coding/2013/04/07/Game-Of-Life/)</del> was unfamiliar, such as the <del>[Game Of Life](http://en.wikipedia.org/wiki/Game_of_life)</del> [Game Of Life](http://en.wikipedia.org/wiki/Conway's_Game_of_Life) (in my case anyway - some people I've spoken to were familiar with this). I didn't know who Conway was. What is this infinite grid? Why are all the examples 3 by 3 rows if it is an infinite grid? What is the initial state of the game? The pressure is on! You need to start coding... *now*.

The question is, which makes for the better test? Should we strive to test developers in domains they are familiar with, or domains they are unfamiliar with? What is a better indicator of how they will perform in the job? 

##Advanced tests vs in-interview tests

One of the application processes I was involved with asked for code submitted in advance of the interview process. This is useful for weeding out the serious applicants from the larger pool, but I'd expect even the most inexperienced developer to know how to Google a code kata and *apapt* it to their own submission, so I'd question how useful well-known katas are as an advanced exercise.

A better alternative is to not use a code kata at all. The best example of a technical test I have come across was for an insurance company, who gave details in advance of the problem that I would have to solve in the technical test. I wasn't allowed to submit code in advance, but I was able to think about the problem and how I would approach it in advance of the interview. As it was a problem specific to the insurance company, there was no answer to search for online. The domain was familiar, and appropriate to the job role I was applying for. The task given had a good balance between simplicity and complexity, and was achievable in different ways.

When it came time to do the technical test, I was confident I had considered the problem at hand to a sufficient level that it reflected the way I would work in a real life situation. I had thought about the architecture, I had considered design patterns, I had reflected on different approaches. Once I had completed the task, we all had something to discuss. I was able to talk confidently about the decisions I had made, the patterns I had used and why I had chosen them. Having seen the test completed multiple times, the interviewers were able to discuss other approaches people had taken, which provided an excellent context for discussion.
 
I really liked this approach as it felt like a more natural reflection of what happens in a real life scenario. In a real life situation, do you start coding immediately after reading a specification? I wouldn't even start coding until I understood the domain to a decent level. Yet with a code kata this is what you are expected to do. 

## What have I learnt?

The most interesting thing I have learnt from these experiences is an understanding of how my own thought processes work. My best insights into problems come when I am not actively thinking about them. Looking back at a particular technical test that I performed without great merit, it was only hours later that I understood some of the errors I had made, and realized how a different approach would have been better. By the following day, my mind had internalized the problem and come up with multiple solutions. I began thinking about how I work on a day-to-day basis and realized that this is often the case too. My best insights come when I take time out from actually sitting at the desk coding - walking to the local coffee shop at lunch, taking a break etc. 

I'm going to go and watch Kingpin...

