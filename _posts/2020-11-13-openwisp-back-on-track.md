---
title: OpenWISP Back on Track
published: true
---

I started working on another
[issue on ansible-openwisp2](https://github.com/openwisp/ansible-openwisp2/issues/200).
This issue is to generate an SSH key pair on the remote machine and utilize
that keypair for the devices.

Being mostly unfamiliar Ansible, I had to do a fair bit of research for
generating SSH key on a remote machine using Ansible. The Ansible Community on
the IRC helped a lot. That has become my goto place whenever I have a doubt
which does not get resolved with a fair bit of searching.

Thanks to an Ansible module, I did not have to do much weight lifting myself
to generate SSH keypair. The next task was to create credential objects in
the database. I wrote a Python script for it and tested it locally in the
openwisp-controller. After adding a bit of error handling, I ported it for use
in Ansible.

The initial test runs looked promising. Later, I found out that the script was
missing out on corner cases. I had to tweak the script but doing that I broke
the earlier implementation. So, I had to go back to a state when the earlier
implementation was not broken and modify the code to cater to corner cases.

I hope I could complete this today and create an initial PR.

-------------

### In other news

My second [PR to Kiwi TCMS](https://github.com/kiwitcms/Kiwi/pull/2088)
got merged. The maintainer requested a few minor changes.
Basically, he asked me to remove the tests which were testing something that was
not the functionality of the Kiwi TCMS codebase.
