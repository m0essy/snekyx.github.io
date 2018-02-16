---
layout: post
title: "Odd Scala behaviour"
categories: blog
excerpt:
tags: [Scala, akka]
image:
  feature:
date: 2018-02-12T01:01:00-00:00
modified: 2018-02-12T01:00:01-00:00
---

# Odd scala behaviour

While developing an application using Scala and akka I encountered a very odd behaviour in my application. I received a timeout in my sender of a message.

I wrote a test, and started to debug. The code in question looked something like this:

{% gist 4346e710924ad5d67c104acec7ecde90 %}

In Scala I am used to have some If expressions. so my thought was to just have an If/else where every block returns a future of Int.
So the pipeTo should send this back to the sender.
My expectation was that When I do:
actor ? IncreaseBy1(-1) I get 0 and when I call actor ? IncreaseBy1(1) I'll receive 2.

What could possible go wrong...?

Well whenever I asked the actor with a Value of -1 I received a timeout.

When I decompiled the FaultyPipeToActor to java code, everything was clear... except WTF?
