---
title: 記事一覧
short_title: 記事一覧
layout: default
lead: サイト内の記事を一覧表示します。
permalink: /test/
nav_order: 999
sidebar_title: 関連記事
---

## 記事一覧

{% assign all_pages = site.pages | sort: "nav_order" %}

<ul>
  {% for p in all_pages %}
    {% if p.title and p.url != page.url %}
      {% if p.url contains '/test/' %}
        {% unless p.url == '/test/' or p.url == '/test/index.html' %}
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