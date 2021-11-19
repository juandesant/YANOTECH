---
layout: page
title: About YANOTECH
permalink: /about/
---

# About YANOTECH
{% include_relative README.md %} <!-- Include relative so that we can use README.md as a base, and keep the styling -->

{% assign the_issues = site.data.issues | where_exp:"item", "item.state != 'closed'" %}
## Blog issues

<!-- {% assign issues_url = "/issues" | absolute_url %} -->
{% assign issues_url = "/issues" | relative_url %}

This is a list of the known open issues with YANOTECH. Feel free to report issues on [Github][yanotech-issues]. You can see a (not necessarily up-to-date) list of all issues <a href="{{ issues_url }}">here</a>.

[yanotech-issues]: https://github.com/juandesant/YANOTECH/issues "Issues on YANOTECH repository."

{% if the_issues.size > 0 %} <!-- We only show the Blog issues section if the JSON file has at least one entry -->
<ul>
{% for issue in the_issues %}
<li><strong>[{{issue.state}}]</strong> <a href="{{issue.html_url}}">{{ issue.title }}</a>: {{issue.body}}</li>
{% endfor %}
</ul>
{% else %}
There are currently no open issues. 
{% endif %} <!-- if the_issues.size > 0 -->