---
title: 記事一覧
short_title: 記事一覧
layout: default
lead: 記事一覧です。
permalink: /test2/
section: test2
nav_order: 999
sidebar_title: 関連記事
is_category_top: true
---

## 記事一覧

{% assign all_pages = site.pages | sort: "nav_order" %}

{% assign section = page.section %}

<ul>
  {% for p in all_pages %}
    {% if p.title and p.url != page.url %}

      {% if p.section == section %}
        {% unless p.url == section_meta.url or p.url == section_meta.url | append: 'index.html' %}
          <li>
            <a href="{{ p.url | relative_url }}">{{ p.title }}</a>

            {% if p.lead %}
              <div style="color: var(--kb-muted); font-size: 13px; margin-top: 4px;">
                {{ p.lead }}
              </div>
            {% endif %}
          </li>
        {% endunless %}
      {% endif %}

    {% endif %}
  {% endfor %}
</ul>