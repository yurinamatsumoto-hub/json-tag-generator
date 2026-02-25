# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## 概要

SmartNews クイズ/キャンペーン向けの `completion` JSONタグを生成するブラウザツール。
`correctnessNum`・`missionId`・`ctaUrl` を入力すると、コピペ用のJSONスニペットをリアルタイム生成する。

Vercel でホスティングし、GitHub (`yurinamatsumoto-hub/json-tag-generator`) へ push すると自動デプロイされる。

## ファイル構成

- `index.html` — ツール本体（ビルド不要の単一ファイル。フレームワーク・依存パッケージなし）

## 開発・確認方法

ビルド不要。ブラウザで直接開くか、簡易サーバーで確認する。

```bash
# 手元確認
python3 -m http.server 8080
# → http://localhost:8080/

# 本番反映（push すると Vercel が自動デプロイ）
git add .
git commit -m "変更内容"
git push
```

## 出力するJSONの構造

```json
,"completion": {
    "correctnessNum": <整数>,
    "reward": {
      "type": "mission",
      "missionId": "<入力値>",
      "openAction": "close",
      "ctaText": "ミッションに戻る",
      "ctaUrl": "<入力値>"
    }
  }}
```

- **可変フィールド**：`correctnessNum`（整数）・`missionId`・`ctaUrl`
- **固定フィールド**：`type`・`openAction`・`ctaText` — 変更する場合は `index.html` の `generate()` 関数内のテンプレートリテラルを編集する

## 各フィールドの説明

| フィールド | 説明 |
|-----------|------|
| `correctnessNum` | ミッションをクリアするのに必要な正解数 |
| `missionId` | クイズのミッションID |
| `ctaUrl` | Mission の Deeplink（Mission Admin の [META] タブ → [Deeplink] → [GENERATE DEEPLINK] で発行。Referrer に `quiz` を入力） |
