---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: default
title: "YANOTECH: Yet ANOther TECHnical blog"
---

{% for post in site.posts %}
<article class="unit-article layout-post">
    <div class="unit-inner unit-article-inner">
        <div class="content">
            <div class="bd">
                <div class="entry-content">
                    {{ post.content }}
                </div><!-- entry-content -->
            </div><!-- bd -->
        </div><!-- content -->
    </div><!-- unit-inner -->
</article>
{% endfor %}