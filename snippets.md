<<<<<<< HEAD
---
layout: home
---

{% for s in site.snippets %}
## [{{s.title}}]({{s.url | prepend: site.baseurl }})
=======
---
layout: home
---

{% for s in site.snippets %}
## [{{s.title}}]({{s.url | prepend: site.baseurl }})
>>>>>>> 16412f9fb410fa94fc34b3c3851760354412cde0
{% endfor %}