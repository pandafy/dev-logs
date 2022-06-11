---
title: Adding WireGuard to Docker OpenWISP
---

Last summer, I worked on adding WireGuard support to OpenWISP.
And after a year of testing, improvements and production
deployments, I am containerizing that work for
[`docker-openwisp`](https://github.com/openwisp/docker-openwisp/).

The Ansible solution we developed to deploy this feature in
[`ansible-wireguard-openwisp`](https://github.com/openwisp/ansible-wireguard-openwisp)
bundles an updater application with the WireGuard server. Each
WireGuard VPN server has its updater application that listens
for configuration updates.

While designing this feature for docker-openwisp, we asked ourselves:
- How can we support multiple WireGuard VPN servers?
- How will VPN servers behave on replication (for high availability)?

The solution was to decouple the updater application
and the WireGuard VPN server. We created two Docker images:
one for running the WireGuard VPN server and the other for the configuration
updater application.

This architecture would work for both the scenarios I shared above. Also,
it had the added advantage to use the one updater application for
multiple VPN servers (even for the replicated containers).

The following illustrates the flow of control whenever a change is made
to VPN server's configuration:

![Flow of control whenever a change is made
to VPN server's configuration](https://i.imgur.com/4ztVU0B.png)
