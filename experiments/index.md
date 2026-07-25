---
layout: default
title: Experiments
permalink: /experiments/
---

[Home]({{ "/" | relative_url }}) ·
[Essays]({{ "/essays/" | relative_url }})

# Experiments

Practical trials and the lessons that survived contact with reality.

{% assign experiments = site.experiments | sort: "date" | reverse %}
{% for experiment in experiments %}
## [{{ experiment.title }}]({{ experiment.url | relative_url }})

{% if experiment.date %}{{ experiment.date | date: "%-d %B %Y" }}{% endif %}

{{ experiment.summary | default: experiment.excerpt }}
{% else %}
No experiments have been published yet.
{% endfor %}
