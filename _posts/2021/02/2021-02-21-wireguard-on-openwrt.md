---
title: Wireguard on OpenWRT
---

After playing with Wiregaurd on AWS instances, I tried to step up the game by
using my OpenWRT router as a client. Again, Wireguard is not built on
server-client architecture but still.

Gladly, I didn’t need to compile the OpenWRT image myself just to use
Wireguard. I was able to simply install it using `opkg`.

The guide in [OpenWRT’s Wiki on installing and configuring Wireguard](https://openwrt.org/docs/guide-user/services/vpn/wireguard/start)
was very helpful. I was able to install and configure Wireguard effortlessly
even though I don’t understand what those `uci` commands do.

I only faced one hurdle today, not being able to use the internet through
the Wireguard’s VPN tunnel. Later I realized I did not enable IP Forwarding
on AWS instance. After enabling it, I was able to browse the internet using t
he Wireguard tunnel created via the OpenWRT router.

-----------------

### In other news

Engaged in rubber duck debugging exercise with a friend and tried to
understand the working of [ElasticSearch Go Client](https://github.com/elastic/go-elasticsearch).
I think that it will help work on Kyverno.
