---
layout: default
title: About YANOTECH
permalink: /issues/
---

## Blog issues
{% assign issues_json = site.data.issues %}

**Issues**: {{ issues_json.length }}
**First issue**: {{ issues_json[0] }}

{{ issues_json[0].title }}

{% if issues_json.length > 0 %} <!-- We only show the Blog issues section if the JSON file has at least one entry -->

This is a list of the known issues with YANOTECH. Feel free to report issues on [Github][yanotech-issues].

[yanotech-issues]: https://github.com/juandesant/YANOTECH/issues "Issues on YANOTECH repository."

<ul>

	{% for issue in issues_json %}
		<li><a href="{{issue.url}}">{{ issue.title }}</a>: {{issue.body}}</li>
	{% endfor %}

</ul>

{% else %}

Yay! No issues found!

{% endif %} <!-- if issues_json.length > 0 -->