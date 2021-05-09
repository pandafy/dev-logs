---
title: Running a script on boot
---

`ansible-wireguard-openwisp` role needed to be updated to add this
functionality.

I modified the `update_wireguard.sh` script to introduce a new function for
bringing up interfaces. Then I modified the script to allow calling each
function from the terminal. Adding `”$@”` at the end of file does the trick.

Executing a command on boot was pretty easy on CentOS. All I had to do was add
the command in `/etc/rc.d/rc.local` and make that file executable. I thought my
job was done, but I was wrong. Such a file does not exist on Debian
derivatives. Instead of adding workarounds for different distributions,
I started from scratch and created my own service for bringing up WireGuard
interfaces that worked similar to rc.local. Adding a custom service helped
prevent bloating of `ansible-wireguard-openwisp` role.

I learnt many things today, since it was the first time I interacted with
system services except for restarting or enabling an existing service.
