---
layout: post
title:  "Link directly to a specific PDF page"
date:   2019-03-05 10:47:53 -0300
categories: tips
tags: pdf, url
---

Sometimes you want to link directly to a given PDF page. For instance, you want to point to a figure that appears on a given page, or to a slide in a PDF presentation.

It seems that Adobe makes it possible to link to PDF pages, as shown in their [help document][pdf-link].

If you have a URL link to a PDF, say `http://example.com/file.pdf`, you can link directly to a page by adding a `#page=n` fragement, were `n` is the page you want to link to. For instance, if you're interested in page 17 of the Enterprise Objects Framework (start of Part I), we can link to [https://tinuryl.com/EOFDevGuide#page=17](https://tinuryl.com/EOFDevGuide#page=17)[^EOFDevGuide].

And this also works for `file` URLs, i.e., `file:///Users/username/file.pdf#page=23` will open a web browser —if it can render PDFs— on page 23 of `file.pdf`.

[pdf-link]: https://helpx.adobe.com/acrobat/kb/link-html-pdf-page-acrobat.html

[^EOFDevGuide]: The TinyURL [https://tinyurl.com/EOFDevGuide](https://tinyurl.com/EOFDevGuide) points to  [https://developer.apple.com/ library/ archive/ documentation/ LegacyTechnologies/ WebObjects/ WebObjects_4.0/ System/ Documentation/ Developer/ EnterpriseObjects/ Guide/ EOFDevGuide.pdf](https://developer.apple.com/library/archive/documentation/LegacyTechnologies/WebObjects/WebObjects_4.0/System/Documentation/Developer/EnterpriseObjects/Guide/EOFDevGuide.pdf). See that you can add the fragment to a redirection!

## Linking to a named anchor

Adobe Acrobat allows authors to include named Destinations in the file. If you have a destination named `Glossary`, for instance, you can use the fragment to point to it, as in `http://example.com/file.pdf#Glossary`. Unfortunately, bookmarks created from the Table of Contents hierarchy don't seem to work. That is, [https://tinyurl.com/EOFDevGuide#Index](https://tinyurl.com/EOFDevGuide#Index) does not work, even when there is a bookmark —but not a named destination— with the name Index.