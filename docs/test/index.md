---
title: 記事一覧
short_title: 記事一覧
layout: default
lead: サイト内の記事を一覧表示します。
permalink: /test/
nav_order: 999
sidebar_title: 関連記事
---

## すべての記事

{% assign all_pages = site.pages | sort: "nav_order" %}

<ul>
  {% for p in all_pages %}
    {% if p.title and p.url != page.url and p.layout %}
      <li>
        <a href="{{ p.url | relative_url }}">{{ p.title }}</a>
        {% if p.lead %}
          <div style="color: var(--kb-muted); font-size: 13px; margin-top: 4px;">
            {{ p.lead }}
          </div>
        {% endif %}
      </li>
    {% endif %}
  {% endfor %}
</ul>