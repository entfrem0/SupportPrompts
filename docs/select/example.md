---
title: 選択型データ項目を更新するサンプル
section: select
layout: default
date: 2026-04-03
lead: よくある質問をベースに、選択型データ項目の更新手順と EL 式サンプルをまとめました。
nav_order: 2
---

> ## 実例を確認したい場合
> 
> このページでは、選択型データ項目の更新手順や EL 式の具体例をまとめたサンプルを紹介しています。
>
> サポートページ 「Rxxxx: yyy」は[こちら](www.yahoo.co.jp)

# 選択型の例

ここでは前提と実現したい処理内容とEL式の記述例を掲載します。

## 1. 問い合わせ対応ステータスの自動更新

```
### 質問
ワークフローアプリには、以下のデータ項目があります。
- 顧客問い合わせ内容 - 文字型 - フィールド名 q_inquiry
- 問い合わせ対応ステータス - 選択型 - フィールド名 q_status

問い合わせ対応ステータスを自動更新したいです。
```

### 回答

```
提案1：
- EL式：£{#q_inquiry?.contains('至急') ? {'urgent'} : {'pending'}}
- #q_inquiry（文字型）
- 設定対象のデータ項目: q_status（選択型）
```

理由：問い合わせ内容に「至急」が含まれる場合は「urgent」、そうでない場合は「pending」に自動設定します。

## 2. 研修参加可否の部署に基づく設定

### 質問

```
ワークフローアプリには、以下のデータ項目があります。
- 研修参加者 - ユーザー型 - フィールド名 q_participant
- 研修参加可否 - 選択型 - フィールド名 q_attendance

研修参加可否を参加者の部署に基づいて設定したいです。
```

### 回答

```
提案1：
- EL式：£{#q_participant?.getName()?.contains('営業') ? {'approved'} : {'rejected'}}
- #q_participant（ユーザー型）
- 設定対象のデータ項目: q_attendance（選択型）
```

理由：参加者の名前に「営業」が含まれる場合は「approved」、そうでない場合は「rejected」に設定します。


## 3. 商品カテゴリに応じた割引適用

### 質問

```
ワークフローアプリには、以下のデータ項目があります。
- 商品カテゴリ - 選択型 - フィールド名 q_product_category
- 割引適用 - 選択型 - フィールド名 q_discount_type

商品カテゴリに応じて割引適用を自動設定したいです。
```

### 回答

```
提案1：
- EL式：£{#q_product_category?.get(0)?.getValue() == 'electronics' ? {'10percent'} : {'no_discount'}}
- #q_product_category（選択型）
- 設定対象のデータ項目: q_discount_type（選択型）
```

理由：商品カテゴリが「electronics」の場合は10%割引、それ以外は割引なしに設定します。


## 4. ファイルサイズに基づく契約審査結果

### 質問

```
ワークフローアプリには、以下のデータ項目があります。
- 契約申請書類 - ファイル型 - フィールド名 q_contract_file
- 契約審査結果 - 選択型 - フィールド名 q_review_status

契約審査結果をファイルサイズに基づいて自動判定したいです。
```

### 回答

```
提案1：
- EL式：£{#q_contract_file != null && #q_contract_file[0] != null && #q_contract_file[0]?.getLength() > 1000000 ? {'detailed_review'} : {'quick_review'}}
- #q_contract_file（ファイル型）
- 設定対象のデータ項目: q_review_status（選択型）
```

理由：契約申請書類のファイルサイズが1MB（1,000,000バイト）を超える場合は「detailed_review」、そうでない場合は「quick_review」に設定します。


## 5. 緊急度に応じたメール送信状況の更新

### 質問

```
ワークフローアプリには、以下のデータ項目があります。
- 緊急度 - 選択型 - フィールド名 q_urgency
- メール送信状況 - 選択型 - フィールド名 q_mail_status

緊急度に応じてメール送信状況を更新したいです。
```

### 回答

```
提案1：
- EL式：£{#q_urgency?.get(0)?.getValue() == 'high' ? {'immediate'} : {'standard'}}
- #q_urgency（選択型）
- 設定対象のデータ項目: q_mail_status（選択型）
```

理由：緊急度が「high」の場合は「immediate」、そうでない場合は「standard」に設定します。

