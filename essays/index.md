---
layout: default
title: Essays
permalink: /essays/
---

[Home]({{ "/" | relative_url }}) ·
[Experiments]({{ "/experiments/" | relative_url }})

# Essays

Long-form arguments and reflections on engineering freedom.

{% assign essays = site.essays | sort: "date" | reverse %}
{% for essay in essays %}
## [{{ essay.title }}]({{ essay.url | relative_url }})

{% if essay.date %}{{ essay.date | date: "%-d %B %Y" }}{% endif %}

{{ essay.summary | default: essay.excerpt }}
{% else %}
No essays have been published yet.
{% endfor %}
