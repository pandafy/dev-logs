---
title: Hiding elements from print
---


Took up two related issues on Kiwi TCMS which dealt with hiding certain HTML
elements(e.g. add/remove icons) while printing the webpage.

Implementing this introduced me to the `print` media query of CSS.
Creating a patch for these issues was simple, I just had to do the following
for respective elements.

```css
@media print {
    .element-selector {
        display: none;
    }
}
```

-----------------

### In other news

My end-semester exams got completed today. Just one more semester left for completed my bachelor's degree.
