---
layout: default
title: Systems
permalink: /systems/
---

{% assign systems = site.systems | sort: "date" | reverse %}
{% for system in systems %}
## [{{ system.title }}]({{ system.url | relative_url }})

{% if system.date %}{{ system.date | date: "%-d %B %Y" }}{% endif %}

{{ system.summary | default: system.excerpt }}
{% else %}
No systems have been published yet.
{% endfor %}
