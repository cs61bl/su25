---
layout: page
nav_order: 0
hide_right_toc: true
---

{%- assign instructors = site.staffers | where: 'role', 'Instructor' | map: "name" -%}
{%- assign instructor_msg = "Instructor" -%}
{%- if instructors.size != 1 -%}
{%- assign instructor_msg = "Instructors" -%}
{%- endif -%}

<img align="right" alt="161 lock logo" width="85px" src="{{ site.baseurl }}/assets/images/logo.png">

# {{ site.title }}

{% if instructors.size != 0 %}
<span style="white-space: nowrap;">
    <strong>{{instructor_msg}}</strong>: {{ instructors | join: ", " }}{%- if site.lecture.time != empty %} / {%- endif -%}
</span>
{% endif -%}
{%- if site.lecture.time != empty -%}
<span style="white-space: nowrap;">
    <strong>Lecture</strong>: {{ site.lecture.time }}
    {%- if site.lecture.location.name != empty and site.lecture.location.link != empty -%}
    , [{{site.lecture.location.name}}]({{site.lecture.location.link}})
    {%- elsif site.lecture.location.name != empty -%}
    , {{site.lecture.location.name}}
    {%- endif -%}
</span>
{% endif -%}
{%- if site.heading_links.size != 0 -%}
<span style="white-space: nowrap;">
    [
    {%- for link in site.heading_links -%}
    {%- unless forloop.first -%}, {% endunless -%}
    {%- if link.text != empty and link.url != empty -%}
    [{{link.text}}]({{link.url}})
    {%- elsif link.text != empty -%}
    {{link.text}}
    {%- endif -%}
    {%- endfor -%}
    ]
</span>
{% endif -%}

{%- if site.enable_announcements -%}
## Announcements

{{ site.announcements.last }}

[Past announcements](announcements){: .btn .btn-outline .fs-3 }
{%- endif %}

## Course Calendar

[Skip to current week](#week-{{ 'now' | date: '%U' }}){: .btn .btn-outline .fs-3 }

<div>
{%- include syllabus.html -%}
</div>
