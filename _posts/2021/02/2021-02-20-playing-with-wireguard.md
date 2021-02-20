---
title: Playing With Wireguard
---

I decided to experiment with Wireguard today. Since I am always concerned that
installing random things on my machine could break my regular development
environment, I settled on using my AWS Credits to play with Wireguard.

I spun up two `t2.micro` instances of Ubuntu 20.04 LTS. Though Wireguard is
based on the P2P model, I treated one machine as a client and the other as a
server just to keep everything sorted in my head.

Instead of starting my journey with the [quick start guide](https://www.wireguard.com/quickstart/),
I decided to watch some tutorials on Youtube to understand Wireguard well.
Honestly, the landing page of WireGuard explained better than most of the
Youtube videos. Most of them talked about setting up Wireguard and not how it
worked.

The creator of one of those videos documented the whole tutorial as a [blog](https://forums.lawrencesystems.com/t/getting-started-building-your-own-wireguard-vpn-server/7425)
and this blog served as the single source of truth to me. Later, I realized
that it was based on the quick start guide in Wireguard’s documentation.

My client machine got frozen every time I tried to enable the Wireguard network
interface on it. I double-checked whether I opened the necessary ports in AWS
Security Group but had no luck. To rule out limited system resources as a
cause, I tried upgraded the client instance to `t2.large` but got the same
result.

I had to setup Wireguard locally on my machine to test now. And, it worked on
my machine. I wonder why the client machine on AWS always froze on enabling
the Wireguard interface.
