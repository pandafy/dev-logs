---
title: How Kopia Led Me to Rethink Python Virtual Environments
---

It all started last week when I backed up my distro's home directory using
Kopia. Thanks to high compression, the backup size was only one-third of the
original. I credited this to Kopia’s compression and de-duplication
and moved on, assuming my text-heavy code repositories were just highly
compressible.

Today, I woke up with this thought: if de-duplication helps backups,
maybe it could also help reduce the disk usage of my Python virtual
environments. At that point, my venvs were consuming almost twice as much space
as my code repositories.

For context, I use a separate virtual environment for each OpenWISP module.
This keeps things isolated but also duplicates common packages like `Django`,
`black`, and `requests`. I asked ChatGPT for suggestions to improve this and it
gave me three directions:

1. **`venv --system-site-packages`** – shares system packages, but risks version
   conflicts.
2. **`virtualenv --symlinks`** – uses symlinks instead of copies, but versions
   must still match.
3. **Poetry, pipx, or `uv`** – different tools for dependency management; `uv`
   stood out for its drop-in support for pip commands using `uv pip install`.

The `uv` package manager had already been popping up on my feed, so I decided
this was a good excuse to try it out. I installed `uv` and jumped into my first
rodeo with `openwisp-controller` by running:

```console
uv pip install -r requirements.txt
```

That’s where I hit my first roadblock. `uv` conforms to PEP 625, which requires
tarball URLs to include the `.tar.gz` extension (e.g. `https://github.com/openwisp/openwisp-notifications/archive/refs/heads/1.2.tar.gz`). The OpenWISP modules use
legacy GitHub tarball URLs (e.g.
`https://github.com/openwisp/openwisp-notifications/tarball/1.2`), so `uv`
refused to install them.

To work around this, I wrote a quick script called `uv-install`. It reads a
`requirements.txt`, converts legacy GitHub tarball URLs into the required syntax, and
generates a temporary requirements file. This worked… until it didn’t. If a
dependency itself contained a legacy tarball URL, the same error cropped up
again. That’s when I slid into the rabbit hole of modifying `uv` itself.

To avoid setting up Rust locally, I spun up a GitHub Codespace with my fork of
`uv`. Using the error logs, I was able to pinpoint the code rejecting the
legacy URLs. Not knowing Rust very well, I leaned on GitHub Copilot to patch it
so that `uv` would accept the OpenWISP-style tarball links.

Following the docs, I first generated a debug binary, which worked but was massive (over
500 MB). Looking at the CI configuration, I noticed the release builds used
optimization flags, bringing the binary size down to around 50 MB. That solved
the size problem, but I then ran into distribution issues: Codespaces run on
Ubuntu 24.04, while my dev machine is on Ubuntu 22.04, and the `libgc` versions
differ. The binary I built wasn’t portable across the two.

I thought I could cheat by letting GitHub Actions build it for me, but the
workflows use custom runners, so that didn’t help. To work around the `libgc`
mismatch, I tried compiling `uv` inside an Ubuntu 22.04 Docker container on
GitHub Codespaces using the release profile, but I quickly ran into memory and
storage limits. Codespaces just doesn’t provide enough resources to let Rust
optimize the package properly. For now, I’ve settled on using the debug binary.
It’s bulky, but it works, and I don’t want to sink more time into tweaking
GitHub Actions or Docker just to get the release build working.

---

Many would ask: why go against `uv`’s requirements and break PEP guidelines?
Short answer, **because I can**. That’s the beauty of open source: instead of
always conforming to existing features, we can tweak software to fit our needs.

That said, the practical solution is to update the requirement files to
use the PEP 625 format. But those changes would need to be applied across all
the OpenWISP
modules. Maybe that could be automated with an AI agent, but with
a new release around the corner, I don’t want to overload myself or the team with
unnecessary maintenance work.
