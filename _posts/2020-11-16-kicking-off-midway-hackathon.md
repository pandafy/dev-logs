---
title: Kicking Off Midway Hackathon
published: true
---

My hackathon team started by discussing the implementation of our project.
I am glad that I attended that meeting. After the meeting, I realized that my
understanding of the project idea was broken.

It was unanimously decided to use [SocketIO]()
for WebSocket implementation. It was also decided to write the backend in
GoLang since it would be a great learning opportunity for most of us.
While we were researching to get started, we found out that the
[GoLang library]()
for SocketIO does not support the latest version of SocketIO while the Python
counterpart supported many more features. It was a pragmatic choice to ditch
the idea of using GoLang and proceed with Python instead.

Using Python inherently meant using Flask. Being a complete noob in Flask,
I stood at a corner waiting for the pros to set up the project. Even in the
last hackathon, I got stuck while doing the initial setup of the project.
After the pros did the heavy lifting, I jumped in.

One of the teammates found [Flask-SocketIO](),
a flask package supporting SocketIO. We followed the documentation for creating
a simple SocketIO app just to check whether our project setup works or not.
As expected, we encountered various hurdles doing that. After a lot of web
searches and making logical decisions, we were able to make it work. We were
really glad that it was working because it meant that we can focus on
implementing the project idea now.

While exploring that simple demo implementation we noticed that it was using
HTTP protocol instead of WS. This meant it was using long polling and not web
sockets. We tried different solutions from the internet, but none of them
worked. It is still a mystery why it did not use WebSockets in the first place.
Maybe this is something which we will have to live with.

--------------------

### In other reviews

I updated the documentation for one of the PR on ansible-openwisp2.
I am waiting for reviews on my PR.

This week is going to be a busy one. Brace!
