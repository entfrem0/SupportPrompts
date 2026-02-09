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

  {% for sec in site.sections %}
    {% assign sec_key = sec[0] %}
    {% assign sec_meta = sec[1] %}

    {% assign section_pages = all_pages | where: "section", sec_key | sort: "nav_order" %}

    {% if section_pages and section_pages.size > 0 %}
      <section class="kb-card">
        <header class="kb-card__header">
          <h2 class="kb-card__title">
            <a href="{{ sec_meta.url | relative_url }}">{{ sec_meta.title | default: sec_key }}</a>
          </h2>

          {% if sec_meta.description %}
            <p class="kb-card__desc">{{ sec_meta.description }}</p>
          {% endif %}
        </header>

        <ul class="kb-card__list">
          {% for p in section_pages limit: 3 %}
            {% if p.title and p.url != sec_meta.url %}
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
          <a class="kb-card__more" href="{{ sec_meta.url | relative_url }}">すべて見る →</a>
        </div>
      </section>
    {% endif %}
  {% endfor %}
</div>