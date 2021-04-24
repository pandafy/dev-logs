---
title: `wg-quick` and `wg`
---

In order to simplify the scripts deployed on Wireguard VPN Server, I planned to
add the `Address` field in the VPN server configuration in OpenWISP Controller.

Making this change in the server configuration made me struggle a little in the
beginning. I started debugging from the wrong place. I looked into “Preview
Configuration View” while my answers were hidden in “Download Configuration
View”. Though these two views mostly share the same code, the “Preview
Configuration View” works with a temporary instance, i.e. automatically
generated attributes are not available to it.

After successfully modifying OpenWISP Controller and NetJSONConfig, I started
testing these changes by spinning up an instance on AWS.

The updater script on the VPN server used `wg-quick` for creating a new
interface and `wg syncconf` for hot-loading configuration of an existing
interface.

Little did I know the configuration formats for `wg-quick` and `wg` are
different. `wg-quick` allows providing additional properties that are used
for making changes using the `ip` command. It was only clear to me after
reading manpages for [wg-quick(8)](https://git.zx2c4.com/wireguard-tools/about/src/man/wg-quick.8)
and [wg(8)](https://gitquick.zx2c4.com/wireguard-tools/about/src/man/wg.8).

Luckily, the manpage of `wg-quick(8)` contains an example that allows passing
`wg-quick` configuration to `wg syncconf`.

```
 wg syncconf wgnet0 <(wg-quick strip wgnet0)
```
