---
title: "Adding version switcher to the OpenWISP Docs"
---

In From Modules to Manuals: Unifying OpenWISP Docs, I detailed the journey of
creating the new OpenWISP documentation. This process involved addressing
numerous challenges, one of which was adding a version switcher to the
documentation pages.

The [blog on multi-version documentation with Sphinx by Thomas
Sedlmair](https://www.codingwiththomas.com/blog/my-sphinx-best-practice-for-a-multiversion-documentation-in-different-languages)
provided a solid foundation for implementing a version switcher. By leveraging
Sphinx's templating capabilities, we successfully integrated the version
switcher element into the sidebar. However, this version switcher was statically
generated using the HTML context defined in Sphinx's configuration file
(`conf.py`). This meant that all pages included URLs to download the ePUB and
PDF versions of the documentation, as well as URLs to other versions of the
docs.

The devil lies in the details, and so does our challenge. Since OpenWISP is
continuously evolving, we regularly add documentation for new features. This
means that if we display all versions on all pages, the new pages in the latest
version of OpenWISP might not exist in older versions. Consequently, URLs for
these new pages would lead to 404 errors in the older versions, resulting in a
frustrating user experience. Therefore, our version switcher needed to be
version-aware and dynamically generated.

### Inside the Documentation Build Process

Before diving into the solution for the version switcher, it's important to
understand the build steps for generating the documentation. Without this
context, the solution might be difficult to grasp.

The build process starts by reading a configuration file that specifies the
versions to build and the modules to include in each version. The script then
pulls each module, checks out the specified version, and generates the
documentation in HTML, PDF, and ePUB formats using Sphinx. This procedure is repeated for
each version. Since the documentation is built separately for each version,
the documentation is not aware pages present in other versions.

### Creating a Version-Aware Switcher

The initial idea was to maintain a data structure that maps each page to the
versions in which it is present. This data structure would then be used
to show only relevant version on each page.

We settled on creating a custom Sphinx builder for this task. The builder goes
through all the pages of the documentation—just like any other Sphinx
builder—and creates a map of page names to their respective versions. This
process is repeated for each version, with the map being shared among all
runs. The result is a version map similar to the following:

```json

{
    "index": ["dev", "22.05"],
    "modules": ["dev"],
    "user/monitoring": ["22.05"],
}
```
