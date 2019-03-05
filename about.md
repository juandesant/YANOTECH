---
layout: default
title: About YANOTECH
permalink: /about/
---

# About YANOTECH
{% include_relative README.md %} <!-- Include relative so that we can use README.md as a base, and keep the styling -->

{% assign the_issues = site.data.issues %}
{% if the_issues.length > 0%} <!-- We only show the Blog issues section if the JSON file has at least one entry -->
## Blog issues

This is a list of the known issues with YANOTECH. Feel free to report issues on [Github][yanotech-issues].

[yanotech-issues]: https://github.com/juandesant/YANOTECH/issues "Issues on YANOTECH repository."

<ul>
{% for issue in the_issues %}
<li><a href="{{issue.url}}">{{ issue.title }}</a>: {{issue.body}}</li>
{% endfor %}
</ul>

{%endif} <!-- if the_issues.length > 0 -->