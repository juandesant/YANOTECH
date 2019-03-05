---
layout: default
title: About YANOTECH
permalink: /about/
---

# About YANOTECH
{% include_relative README.md %}
## Blog issues

This is a list of the known issues with YANOTECH. Feel free to report issues on [Github][yanotech-issues].

[yanotech-issues]: https://github.com/juandesant/YANOTECH/issues "Issues on YANOTECH repository."

{% externalJSON issues from url https://api.github.com/repos/juandesant/YANOTECH/issues %}
<ul>
{% for issue in issues %}
  <li><a href="{{issue.url}}">{{ issue.title }}</a>: {{issue.body}}</li>
{% endfor %}
</ul>