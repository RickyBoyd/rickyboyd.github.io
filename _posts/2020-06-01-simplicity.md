---
layout: post
title: Importance of Simplicity 
---

# Why Simplicity Matters And How To Achieve It

## Simplicity

The more software I write and read the more convinced I become that simplicity should be the number one goal
for any software engineer when creating software. This is not my own original idea by any means. It's mostly inspired by the talks and works of Rich Hickey which strike a note with my own experiences.

Do not mix up the concept of easy with the concept of simplicity. A software artifact may be created easily but still be incredibly complex. Also do not mix up the idea of cardinality
with the idea of simplicity. A software architecture may have a higher number of simpler parts than a complex system with less parts.

So what does simple mean? The definition given in dictionary.com is the following:

> easy to understand, deal with, use, etc.:

I would like to emphasise the word _understand_. It's not easy to do, easy to use, or easy to write. It's easy to _understand_. Unfortunately, simplicity can often be very hard to achieve.

Now the natural following question to this is, what makes software easy to understand? I don't believe this has very much to do with superficial ideas such as those you would find reading books such as 'Clean Code'. Don't get me wrong there are some ideas presented in that book which can certainly make code more readable but try to use these as a bedrock on which to form your own opinions.

The real enemy of simplicity is interactions with other pieces of software. When you are trying to understand one piece of software or one package or one class and you also need to know how another particular software/module/class works then you have a problem. We add more cognitive load and things to keep in our heads. Maybe this can work for a small set of software artifacts but the issue quickly compounds into a situation where a human cannot possibly understand what is really going on. This is known as _accidental complexity_. We want to avoid accidental complexity as much as possible. Therefore we advocate for simplicity where ever we can.

There is another form of complexity that is inherent to software development which is called _essential complexity_. This accounts for the operation requirements in which we work or the complexity of the domain for which the software is trying to model. Almost all software has to deal with this essential complexity. This is why we want to avoid the accidental complexity as much as possible, we already have enough complexity to deal with without adding on more.

## Simplicity Is Agility

Software ultimately needs to change over time due to changing requirements. This is a fact of life for almost all software. Therefore the agility of the company is linked closely to the ability to be able to change its software. The more simple the software is, the easier it is to change, and therefore true agility is gained. No amount of SCRUM ceremonies is going to change anything about this fact.

## Simplicity Is Reliability

What do you do when a problem is found in your software? How do you debug it? We have a myriad of tools today around tracing, metrics, and logging to increase observability in our systems. But the more the developers really truly have an understanding of the software they build and their interactions the drastically simpler it is to resolve problems. It's also much easier to avoid problems before they ever occur as unknown and unforeseen consequences of changes are far less likely. Therefore if we want to build reliable systems we should be aiming to build software as simple as possible.

## Sources of Accidental Complexity & Enemies of Simplicity

### Basic Coupling

Unnecessary coupling can easily appear at many levels of software development. Unnecessary coupling to a library, unnecessary coupling to other services, unnecessary coupling to certain technologies, and unnecessary coupling to other modules within our own program. I often see developers inadvertently coupling their software to other pieces of software in a way that could be avoided with a little more work. Techniques such as dependency injection are often the solution to these problems. A great advantage of decoupling is it often makes the individual components much easier to test and reason about on their own. We can then compose them together to get our desired behaviours.

### Object-Oriented Programming Overuse

We could instead use functions that accept pure data and return pure data. These functions will not be tied together in any way so can be moved. What is more, they can be composed in many different ways as we don't need to construct an object to use them. We also avoid the fact that as a user of an object we can't know for sure if the object is mutating its data from one method call to another. In short OOP ties together state and control when these are two things that should be dealt with independently from one another.

### Over Using Inter-Service RPC

When we use RPC we are introducing some accidental complexity. We are tieing together the what and the who because we need to know who to send the RPC to. This is fine up to a point. But when we have a service that needs to advertise some change or notify a set of services in some way the list of these services can grow. What is more, when we send the RPCs what do we do if one fails and others succeed? When do we give up? Do we now need to build knowledge into our service of which of these services we need to retry forever and which ones we don't? Our service also needs to know about the schemas for each of the other services RPCs. This is a problem which is solved by using out of process message broker systems where services can listen to changes. Then each service can have its own policy on how much they care about the data and can deal with their failure cases.

### Ordering

When we depend on order we introduce a form of complexity that may not be required. For example, positional arguments are a form of order which introduces complexity. These can easily lead to mistakes when there are too many. We can instead pass maps or data structures or named arguments across boundaries to avoid these easy to make mistakes. Tuples also share this same flaw. We need to consider the trade-offs of using such constructs when we use them. 

# Summary

I have attempted to lay out an argument for spending more time to think carefully about how we as developers could be introducing accidental complexity into our programs and explained some simpler solutions. This is only a small sample intended to force you to think more about how your software is designed and the potential consequences of these choices. Everything in software is a trade-off, but trade-offs can only be made when we are conscious of the benefits and the drawbacks of our designs.

##### References

[1] [Out Of The Tar Pit](http://curtclifton.net/papers/MoseleyMarks06a.pdf)

[2] [Simple Made Easy](https://www.youtube.com/watch?v=oytL881p-nQ)