---
title: Banging head against WebRTC
published: true
---

We had some leftover tasks from yesterday to cover today. We wrote the backend
logic for rooms but it was not integrating well with the frontend.
While integrating we realized that I had made several mistakes in the code.
In my defense, I wrote the whole code presuming the working of SocketIO.
I am glad the logic of code held for most of the places.
Most of the bugs were due to typographic errors or my wrong assumption of the
schema of the data.

After fixing these bugs, we were relieved that the major part of the work has
been completed. But we were unaware that something more deadly was waiting for
us. We planned to add an audio group chat as well. I knew that WebRTC is used
for making audio and video calling applications. We chose to go ahead with
WebRTC unaware of what stands ahead of us.

All of us were clueless about WebRTC. We only had a faint idea of what it is
and how it is supposed to work. None of us used it in any of our projects.
To our disappointment, we found out that a WebRTC connection is established
between two users and we will have to manage connections between a group of
people ourselves.

We sensed that managing those connections will be a pain for us. We went back
to the web to search for a library that can do it for us. The day was not on
our side. We could not find a single library that even talks about using it
for multiple users, let apart managing group calls.

We stumbled across some good blog posts which boasted of using WebRTC with
SocketIO. Every time we found such a blog, we thought we found our treasure,
but they were only fools' gold.

We wandered on the internet. Read the code of every blog which seemed relevant,
checked out random project implementing WebRTC with SocketIO, but nothing turned
out to be fruitful.

Disappointed by blogs, we turned to video tutorials. We found a tutorial which
talked about [PeerJS](https://peerjs.com/), a JS library to handle WebRTC
connections. Yes, it was like every other library out there which only managed
connection to only one user at a time. But, it seemed easier to write code for
managing multiple users using this library since it took care of most of the
things itself.

I found out that the [PeerJS community has a Telegram channel](https://t.me/joinchat/ENhPuhTvhm8WlIxTjQf7Og).
At this moment every shot was worth taking. I took a shot, joined the channel
and asked whether a tutorial or a project already exists which we could look up
for reference. Finally, things turned around and someone from the community
shared a tutorial for it.

This is it. This is the tutorial we have been searching for. While it was a bit
tricky to port the learnings from the tutorial to our project but we did it in the
end. It was a jaw-dropping moment when the group video call worked. It was the
moment when we realized the day long headbanging was worth it.

-----------------

### In other news

Opened [PR in ansible-openwisp2 for minification of static files and browser cache invalidation](https://github.com/openwisp/ansible-openwisp2/pull/222).
The task was pretty straight forward, the configuration needed was already
provided in the issue. I had to just copy-paste and install the required
dependencies. I completed the task but I am not sure whether it works or not.
I am not sure what to test in the PR.
