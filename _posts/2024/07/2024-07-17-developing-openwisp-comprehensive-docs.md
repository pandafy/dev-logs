---
title: "From Modules to Manuals: Unifying OpenWISP Docs"
---

OpenWISP draws inspiration from the Unix philosophy:
**Do one thing and do it well**. This modular approach has shaped OpenWISP’s
architecture, where separate modules handle specific functionalities such as the
controller, monitoring, firmware upgrades, etc. While this modularity offers
flexibility, it also presents a challenge — fragmented documentation.

"Let's have a separate repository to centralize the docs", some would
say, but at OpenWISP, we like to keep the docs alongside the code. This
called for developing a mechanism which pulls the documentation from all
the repositories and build them at one place.

### The Current State of Affairs

[![OpenWISP's old documentation](https://imgur.com/Wpngv8Z.png)](https://web.archive.org/web/20240717083915/https://openwisp.io/docs/index.html)

In the screenshot above, you can see [OpenWISP’s old
documentation](https://web.archive.org/web/20240717083915/https://openwisp.io/docs/index.html).
It was housed in a separate repository and primarily consisted of tutorials
(such as the quick start guide) and developer resources (including contribution
guidelines and GSoC project ideas). Overall, it contained non-code documentation
written in ReStructuredText and built with
[sphinx](https://www.sphinx-doc.org/en/master/).

For code oriented docs, the user had to hop over individual repositories on
GitHub and find the relevant section in huge README files. This was tedious and
hurt the user on-boarding. Moreover, GitHub encountered a bug in rendering the
ReStructuredText files once, which rendered URL references useless. Fortunately,
the GitHub bug was short-lived, but it served as a valuable lesson—anticipating
potential challenges in the future.

### Brainstorming the Comprehensive Docs

Similar to any well-designed software project, our journey toward comprehensive
documentation began with gathering requirements and brainstorming implementation
ideas. We delved into the documentation practices of other successful projects,
like Django, Kubernetes, ReadTheDocs, etc. seeking inspiration.

After thorough research, we distilled our vision into the following essential
requirements:

1. Eliminate the fragmentation by publishing all the docs at one place
2. Support hosting multiple versions of the docs
3. Generate PDF and ePUB for each doc version

### Developing the Comprehensive Docs

We started by refactoring the documentation in each module. Instead of having a
big README file, we split the documentation into several files based on their
target audience -- users and developers.

We developed a simple Python script in
[openwisp-docs](https://github.com/openwisp/openwisp-docs) to pull the
structured docs from each repository and consolidate them into a unified
resource. The result? HTML, PDF, and ePUB files—all in one place. Our YAML
configuration file specified which modules to include and which versions of the
documentation to generate, ensuring flexibility for future OpenWISP releases.

Thanks to the [blog on multi-version documentation with Sphinx by Thomas
Sedlmair](https://www.codingwiththomas.com/blog/my-sphinx-best-practice-for-a-multiversion-documentation-in-different-languages),
we discovered an elegant solution for implementing the version switcher
in the comprehensive docs.

### Future of the Comprehensive Docs

[![OpenWISP Comprehensive
Docs](https://i.imgur.com/AuJtOaD.png)](https://openwisp.io/docs/__new__/dev/)

In this document, I only touched the technical intricacies of creating
comprehensive documentation for OpenWISP. The comprehensive docs represent an
ongoing commitment to enhance user experience. We’ve invested significant
effort in simplifying the documentation, but the work doesn’t end here.
There is a need for more tutorials, clearer explanations, and many improvements
as we aim to create a holistic documentation for OpenWISP.
