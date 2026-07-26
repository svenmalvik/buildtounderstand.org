---
layout: default
title: Explorations
permalink: /explorations/
---

[Home]({{ "/" | relative_url }}) ·
[Systems]({{ "/systems/" | relative_url }})

# Explorations

Long-form arguments and reflections on engineering freedom.

{% assign explorations = site.explorations | sort: "date" | reverse %}
{% for exploration in explorations %}
## [{{ exploration.title }}]({{ exploration.url | relative_url }})

{% if exploration.date %}{{ exploration.date | date: "%-d %B %Y" }}{% endif %}

{{ exploration.summary | default: exploration.excerpt }}
{% else %}
No explorations have been published yet.
{% endfor %}
