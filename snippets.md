---
layout: home
---

{% for s in site.snippets %}
## [{{s.title}}]({{s.url | prepend: site.baseurl }})
{% endfor %}