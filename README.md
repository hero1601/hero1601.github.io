## My Projects

{% for project in site.projects %}
- [{{ project.title }}]({{ project.url }}) - {{ project.description }}
{% endfor %}
