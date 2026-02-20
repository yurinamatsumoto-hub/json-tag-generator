# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## 概要

SmartNews クイズ/キャンペーン向けの `completion` JSONタグを生成するブラウザツール。
`correctnessNum`・`missionId`・`ctaUrl` を入力すると、コピペ用のJSONスニペットをリアルタイム生成する。

## ファイル構成

- `index.html` — ツール本体（ビルド不要の単一ファイル。フレームワーク・依存パッケージなし）

## 開発・確認方法

ビルド不要。ブラウザで直接開くか、ローカルサーバー経由で確認する。

```bash
# macOS 内蔵 Apache で配信（社内ネットワーク共有時）
sudo cp index.html /Library/WebServer/Documents/json-tag-generator/index.html
sudo apachectl start
# → http://localhost/json-tag-generator/ でアクセス

# 簡易サーバー（手元確認用）
python3 -m http.server 8080
# → http://localhost:8080/
```

## 出力するJSONの構造

```json
,"completion": {
    "correctnessNum": <入力値（整数）>,
    "reward": {
      "type": "mission",
      "missionId": "<入力値>",
      "openAction": "close",
      "ctaText": "ミッションに戻る",
      "ctaUrl": "<入力値>"
    }
  }}
```

固定フィールド（`type`・`openAction`・`ctaText`）を変更する場合は `index.html` 内の `generate()` 関数のテンプレートリテラルを編集する。
