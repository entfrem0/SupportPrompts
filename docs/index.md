---
title: サポートガイド集
short_title: トップ
lead: Questetra ワークフローのデータ更新工程の設定例や EL 式の作り方を、カテゴリごとにまとめています。
layout: default
nav_order: 0
sidebar_title: 関連記事
---

## はじめに

このサポートガイド集では、データ更新工程の設定例や EL 式の作り方を、実際の問い合わせに沿って紹介します。カテゴリごとに関連記事をまとめ、Zendesk のヘルプセンターに近い読みやすさを目指しています。

必要に応じて左側のナビゲーションから関連ページを参照してください。

## カテゴリから探す

<div class="kb-cards">
  {% assign all_pages = site.pages | sort: "nav_order" %}
  {% assign section_keys = all_pages | map: "section" | uniq %}

  {% for sec in section_keys %}
    {% if sec %}
      {% assign section_pages = all_pages | where: "section", sec | sort: "nav_order" %}
      {% assign section_home = section_pages | first %}
      {% assign title = site.sections[sec].title | default: sec %}
      {% assign desc = site.sections[sec].description %}

      {% if section_home %}
      <section class="kb-card">
        <header class="kb-card__header">
          <h2 class="kb-card__title">
            <a href="{{ section_home.url | relative_url }}">{{ title }}</a>
          </h2>
          {% if desc %}
            <p class="kb-card__desc">{{ desc }}</p>
          {% endif %}
        </header>

        <ul class="kb-card__list">
          {% for p in section_pages limit:3 %}
            {% if p.title %}
            <li class="kb-card__item">
              <a class="kb-card__link" href="{{ p.url | relative_url }}">{{ p.title }}</a>
              {% if p.lead %}
                <div class="kb-card__meta">{{ p.lead }}</div>
              {% endif %}
            </li>
            {% endif %}
          {% endfor %}
        </ul>

        <div class="kb-card__footer">
          <a class="kb-card__more" href="{{ section_home.url | relative_url }}">すべて見る →</a>
        </div>
      </section>
      {% endif %}
    {% endif %}
  {% endfor %}
</div>