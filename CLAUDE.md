# tech-writing — Qiita記事執筆ガイド

このリポジトリはQiita CLI連携で技術ブログ記事を管理・執筆する場所。
Claude Codeは記事の執筆補助、構成レビュー、校正を担う。

---

## ディレクトリ構成

```
tech-writing/
├── CLAUDE.md
├── README.md
├── public/              # Qiita CLI管理下 (qiita pull/pushで同期)
│   └── <article-id>.md
├── wip/                 # 執筆中のローカル草稿 (Qiitaに上げる前)
│   └── <slug>.md
└── templates/
    └── article.md       # 新規記事のテンプレート
```

### ディレクトリの役割

| ディレクトリ | 役割 |
|---|---|
| `wip/` | 執筆中の草稿。アイデアレベルから書き始める場所 |
| `public/` | `qiita pull` で取得・`qiita publish` で投稿した記事 |
| `templates/` | 新規記事のひな型 |

---

## Qiita CLIのセットアップ

```bash
# 初回セットアップ
npm install --global @qiita/qiita-cli
qiita login

# 既存記事の取得
qiita pull

# 記事の投稿・更新
qiita publish <article-id>

# ローカルプレビュー
qiita preview
```

---

## 記事ファイルの形式

### フロントマター (public/ 配下)

```yaml
---
title: "タイトル"
tags:
  - tag1
  - tag2
private: false
updated_at: ""
id: null
organization_url_name: null
slide: false
ignorePublish: false
---
```

### wip/ のファイル命名規則

```
wip/YYYY-MM-DD_<slug>.md
例: wip/2026-03-04_docker-compose-tips.md
```

---

## 執筆ワークフロー

```
1. wip/ に草稿作成
       ↓
2. Claude Codeで構成・内容レビュー
       ↓
3. public/ に移動してフロントマター整備
       ↓
4. qiita preview でローカル確認
       ↓
5. qiita publish で投稿
```

---

## 執筆スタイルガイドライン

### 対象読者
- 実務エンジニア向け (初心者すぎる説明は不要)
- 動けばOKではなく、**なぜそうするか**を添える

### 文体
- 語尾は「です・ます」調
- 見出しは体言止め or 短い文
- コードブロックには言語名を明記

### 構成パターン (推奨)
1. **課題提示** — 何が問題か、なぜ書くか
2. **概要・前提** — 環境、バージョン
3. **手順 / 解説** — コード付きで具体的に
4. **まとめ** — 要点の箇条書きとリンク

### タグの付け方
- 3〜5個を目安
- 主なテーマ: `バックエンド` `フロントエンド` `インフラ` `DevOps`
- 技術固有タグ (例: `Docker` `Next.js` `Go`) を必ず含める

---

## Claude Codeへの指示テンプレート

記事作業をお願いする際は以下の形式を使う:

```
# 依頼種別
- [ ] 草稿執筆 (テーマ: _____)
- [ ] 構成レビュー
- [ ] 文章校正・リライト
- [ ] コードサンプル作成

# 対象ファイル
wip/_____.md

# 補足・要望
(自由記述)
```

---

## 注意事項

- `public/` のファイルはQiita CLIが管理するため、フロントマターのフォーマットを崩さない
- `id: null` の記事は未投稿。`qiita publish` 後に自動でIDが付与される
- 画像はQiitaのメディア機能にアップロードし、URLを記事に貼る (ローカル管理不要)
