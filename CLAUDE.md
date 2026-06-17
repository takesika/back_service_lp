# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

> やりとり・コメント・ドキュメントはすべて日本語で記述する。

## プロジェクト概要

「Back Service」（中小企業・小規模事業者向けの IT/AI 相談・実装支援サービス）の検証用ランディングページ。Google広告で少額（月3,000円程度）出稿し、訴求・クリック・相談ボタン押下の反応を見るための**ドラフトLP**であり、本番プロダクトではない。

ビルド・依存関係・テストフレームワークは一切なし。素のHTML/CSS/JSのみ。

## ファイル構成

- `index.html` — LP本体。単一ファイルに全CSS（`<style>`）と全JS（インライン`<script>`）を内包する自己完結型。セクション構成: hero → service → price(`#price`) → flow(`#flow`) → policy(`#policy`) → contact(`#contact`)
- `thanks.html` — 問い合わせ完了ページ（`noindex`）
- `README_SETUP.md` — 公開（Netlify Drop / Cloudflare Pages）・問い合わせ導線・GA4・Google広告のセットアップ手順
- `google_ads_test_plan.md` — 広告テストプラン（キーワード候補・広告文案・予算・判断基準）
- `lp_revision_notes.md` — LP訴求軸の変更履歴と未確定の検討事項

## 開発・確認

ローカル確認はファイルを直接ブラウザで開く、または任意の静的サーバ:

```bash
python3 -m http.server 8000   # http://localhost:8000/index.html
```

公開は手順書（`README_SETUP.md`）どおり Netlify Drop へフォルダごとドラッグ&ドロップが最短。

## 編集時の重要な前提

- **GA4は導入済み**: 測定ID `G-S9QLLD91KH` が `index.html` 冒頭に有効な状態で埋め込み済み。同ファイル内に `G-XXXXXXXXXX` のプレースホルダ版とコンバージョン計測スニペット（`gtag_report_conversion`）がコメントアウトで残っている。本番コンバージョンIDを入れる際はこちらを使う。`thanks.html` にも同じGoogle tagを必要に応じて貼る。
- **相談ボタンの計測**: `#contactButton` のクリックで GA4イベント `contact_click`（category: engagement / label: contact_form_button）を送る仕込みがファイル末尾の`<script>`にある。問い合わせ導線の主要KPI。
- **問い合わせ先**: `#contactButton` の `href` がGoogleフォーム（現状 `https://forms.gle/...`）。フォーム差し替えはここを編集する。

## 内容（コピー）を編集するときの方針

`lp_revision_notes.md` に訴求軸の決定事項がある。守るべき点:

- 軸は「業務整理」ではなく **「人の手作業（請求・確認・集計・広告作成）をIT/AIで代替・省力化・自動化」**。整理はその前段階という位置づけ。
- 開発自体にもAIを活用し試作・改善を高速化する、という点を含める。
- **具体例は推測で創作しない**（v4でこの方針が明確化された）。掲載中の実例は「ヨガスタジオの請求処理自動化・SNS広告戦略のAI化・SNS広告のAI生成」。知らない事実・数値・事例を追加しない。
- 料金は初月・月額とも10万円という前提でコピーが書かれている。
