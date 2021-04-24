---
title: Ansible Role for Wireguard VPN Updater
---

For the last couple of days, I have been working on creating an Ansible role
to configure the Wireguard server instance. It includes deploying scripts to
automatically fetch configurations from OpenWISP Controller and update the
Wireguard and VXLAN configuration on the server.

The updater comprises a small Flask app that exposes a webhook to trigger the
update. The actual update scripts are written in bash for Wireguard and Python
for VXLAN.

Today, I improved the deployment script. I added more functionalities for
managing Wireguard interfaces. Now. the script can bring up or tear down
interfaces according to the configuration set in OpenWISP Controller while
respecting any manual changes done by the user.

Until today, the endpoints were running on Flask’s developer server. Today,
I added uWSGI for exposing webhook endpoints. I also added SSL support on top
of uWSGI, this is something that is not very well documented. I had it working
by trial and error. I would write about it in a separate blog soon.
