---
title: ファイル型データ項目を更新する
layout: default
section: dfile
date: 2026-04-03
lead: ファイル型データを活用するための仕様と代表的な EL 式の使い方を整理しました。
updated: 2026-04-03
nav_order: 1
---

# ファイル型データに関する文法知識

業務プロセスで「ファイル型」データを扱う場合、  ファイルの情報取得や状態判定のために専用メソッドを使用します。  
以下では、ファイル型の基本概念と利用可能なメソッドを整理します。


## 1. ファイル型の基本概念

- ファイル型は、ワークフロー内で **複数のファイルを保存できるデータ型**です。
- 1つのデータ項目に **複数ファイルを格納できます**。
- ユーザーがアップロードしたファイルや、自動工程で取得したファイルを保存できます。
- 保存されたファイルは以下の用途で利用できます。
  - ダウンロード
  - プレビュー表示
  - メール添付
- 一度に複数ファイルを編集することはできません。

## 2. SpELの注意

- ファイル型は配列構造になっており、0番目のファイル型変数を表すときは
`#q_files[0]`
と記述します。
- ファイル型をEL式で扱うときは、`#q_files`と`#q_files[n]`がnullでないことを三項演算子で記述する必要があります。
例：
`#q_files != null && #q_files[0] != null ? #q_files[0]?.getId() : 0`

## 3. ファイル型のメソッド


### getId()

- **説明**：ファイルIDを取得します。
- **入力**：ファイル型
- **返り値の型**：Long
- **例**：

`#q_files != null && #q_files[0] != null ? #q_files[0]?.getId() : 0`

### getName()

- **説明**：ファイル名を取得します。
- **入力**：ファイル型
- **返り値の型**：文字型
- **例**：

`#q_files != null && #q_files[0] != null ? #q_files[0]?.getName() : ‘’`

### getLength()

- **説明**：ファイルサイズ（バイト）を取得します。
- **入力**：ファイル型
- **返り値の型**：Long
- **例**：

`#q_files != null && #q_files[0] != null ? #q_files[0]?.getLength() : 0`


### getLengthText()

- **説明**：ファイルサイズをテキスト形式で取得します。
- **入力**：ファイル型
- **返り値の型**：文字型
- **例**：

`#q_files != null && #q_files[0] != null ? #q_files[0]?.getLengthText() : ‘’`

### getContentType()

- **説明**：ファイルの Content-Type を取得します。
- **入力**：ファイル型
- **返り値の型**：文字型
- **例**：

`#q_files != null && #q_files[0] != null ? #q_files[0]?.getContentType() : ‘’`

### getCharset()

- **説明**：Content-Type の charset 情報のみを取得します。
- **入力**：ファイル型
- **返り値の型**：文字型
- **例**：

`#q_files != null && #q_files[0] != null ? #q_files[0]?.getCharset() : ‘’`


### getMalwareScanStatus()

- **説明**：ファイルのマルウェアチェック状態を取得します。
- **入力**：ファイル型
- **返り値の型**：文字型

**状態**

- `null`：マルウェアチェック有効化前のファイル  
- `SCANNING`：スキャン中  
- `NO_THREATS_FOUND`：脅威なし  
- `THREATS_FOUND`：マルウェア検出  
- `UNSUPPORTED`：チェックできないファイル  
- `TIMEOUT`：スキャンタイムアウト  

- **例**：

`#q_files != null && #q_files[0] != null ? #q_files[0]?.getMalwareScanStatus() : ‘’`


### getProcessDataInstanceId()

- **説明**：ファイルが格納されているデータインスタンスIDを取得します。
- **入力**：ファイル型
- **返り値の型**：Long
- **例**：

`#q_files != null && #q_files[0] != null ? #q_files[0]?.getProcessDataInstanceId() : 0`

### isImage()

- **説明**：ファイルが画像かどうかを判定します。
- **入力**：ファイル型
- **返り値の型**：Boolean
- **例**：

`#q_files != null && #q_files[0] != null && #q_files[0]?.isImage() == true ? ‘image’ : ‘’`


### isInline()

- **説明**：ファイルがブラウザでインライン表示可能か判定します。
- **入力**：ファイル型
- **返り値の型**：Boolean
- **例**：

`#q_files != null && #q_files[0] != null && #q_files[0]?.isInline() == true ? ‘inline’ : ‘’`
