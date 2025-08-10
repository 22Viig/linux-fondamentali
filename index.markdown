---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: home
---

<ul>
  {% for pagina in site.pagine %}
    <li><a href="{{site.baseurl}}{{pagina.url }}">{{ pagina.title }}</a></li>
  {% endfor %}
</ul>