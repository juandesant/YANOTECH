---
layout: default
title: About YANOTECH
permalink: /issues/
---

## Blog issues
{% assign issues_json = site.data.issues %}

This is a list of the known issues —including closed ones— with YANOTECH. Feel free to report issues on [Github][yanotech-issues].

[yanotech-issues]: https://github.com/juandesant/YANOTECH/issues "Issues on YANOTECH repository."

{% if issues_json.size > 0 %} <!-- We only show the Blog issues section if the JSON file has at least one entry -->

<ul>

	{% for issue in issues_json %}
		<li><strong>[{{issue.state}}]</strong><a href="{{issue.html_url}}">{{ issue.title }}</a>: {{issue.body}}</li>
	{% endfor %}

</ul>

{% else %}

Yay! No issues found!

{% endif %} <!-- if issues_json.size > 0 -->