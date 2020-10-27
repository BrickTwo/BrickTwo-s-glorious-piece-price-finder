---
layout: page
title: pages.faq

namespace: faq
permalink: /frequent-questions/
permalink_de: /haeufige-fragen/
---

{% for question in site.faq %}
<div>
    <h4>{% t {{ question.title  }} %}</h4>
    {{ question.content }}
</div>
{% endfor %}