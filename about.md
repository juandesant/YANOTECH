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

{% assign the_issues = site.data.issues %}

<ul>
{% for issue in the_issues %}
  <li><a href="{{issue.url}}">{{ issue.title }}</a>: {{issue.body}}</li>
{% endfor %}
</ul>