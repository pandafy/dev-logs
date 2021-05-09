---
title: "`host_vars` for Molecule Scenarios"
---

Been working on the enhancing `ansible-wireguard-openwisp`. I added support
for CentOS and RHEL 7 and 8 which was quite a chore. I have been using Debian
derivatives for all of my development work and it took time to get used to
workings of CentOS.

The names of some system packages are different, the configuration files live
in different places and then there are three ways to install WireGuard.
Managing all of this burned a lot of my time. Adding automated tests was
another hustle.

CentOS 7 requires `ansible_python_interpreter` to point to `python2` to be
able to run without need of any additional packages. While testing it on an
instance on AWS, I configured this setting in the inventory file, but for
automated tests using molecules, I was clueless.

After some searching on the web, I came across this [comment on an issue on molecule’s GitHub repository](https://github.com/ansible-community/molecule/issues/214#issuecomment-414730715)
which suggests to configure `host_vars` of the `provisioner`. After this,
the tests run smoothly for CentOS 7.

```yaml
provisioner:
  name: ansible
  lint:
    name: ansible-lint
  inventory:
    host_vars:
      my_instance:
        ansible_python_interpreter: "/home/core/bin/python"
```
