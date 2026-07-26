---
layout: default
title: Systems
permalink: /systems/
---

[Home]({{ "/" | relative_url }}) ·
[Explorations]({{ "/explorations/" | relative_url }})

# Systems

Working systems and the engineering choices behind them.

{% assign systems = site.systems | sort: "date" | reverse %}
{% for system in systems %}
## [{{ system.title }}]({{ system.url | relative_url }})

{% if system.date %}{{ system.date | date: "%-d %B %Y" }}{% endif %}

{{ system.summary | default: system.excerpt }}
{% else %}
No systems have been published yet.
{% endfor %}
