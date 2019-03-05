---
layout: default
title: About YANOTECH
permalink: /issues/
---

## Blog issues
{% assign the_issues = site.data.issues %}

<blockquote>
	{{ the_issues }}
</blockquote>

<hr/>

<blockquote>
	{{ the_issues | inspect }}
</blockquote>

{% if the_issues.length > 0 %} <!-- We only show the Blog issues section if the JSON file has at least one entry -->

This is a list of the known issues with YANOTECH. Feel free to report issues on [Github][yanotech-issues].

[yanotech-issues]: https://github.com/juandesant/YANOTECH/issues "Issues on YANOTECH repository."

<ul>

	{% for issue in the_issues %}
		<li><a href="{{issue.url}}">{{ issue.title }}</a>: {{issue.body}}</li>
	{% endfor %}

</ul>

{% else %}

Yay! No issues found!

{% endif %} <!-- if the_issues.length > 0 -->