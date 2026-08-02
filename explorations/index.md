---
layout: default
title: Explorations
permalink: /explorations/
---

{% assign explorations = site.explorations | sort: "date" | reverse %}
{% for exploration in explorations %}
## [{{ exploration.title }}]({{ exploration.url | relative_url }})

{{ exploration.summary | default: exploration.excerpt }}{% if exploration.date %} <span class="exploration-date">({{ exploration.date | date: "%B %Y" }})</span>{% endif %}
{% else %}
No explorations have been published yet.
{% endfor %}
