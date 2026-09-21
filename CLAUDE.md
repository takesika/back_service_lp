# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

> やりとり・コメント・ドキュメントはすべて日本語で記述する。

## プロジェクト概要

「Back Service」（作りたいアプリがあり開発費を抑えたい人向けの、Webアプリ・iPhoneアプリの受託開発サービス）の検証用ランディングページ。開発作業にAIを活用するので安く・早く作れる、というのが訴求。Google広告で少額（日予算100円／月3,000円程度）出稿し、訴求・クリック・見積もり依頼ボタン押下の反応を見るための**ドラフトLP**であり、本番プロダクトではない。

2026-09-21 に旧モデル（中小企業向けIT/AI相談・実装支援）から転換した。経緯は `lp_revision_notes.md` を参照。

ビルド・依存関係・テストフレームワークは一切なし。素のHTML/CSS/JSのみ。

## ファイル構成

- `index.html` — LP本体。単一ファイルに全CSS（`<style>`）と全JS（インライン`<script>`）を内包する自己完結型。セクション構成: hero → こんな方へ(`#target`) → 安く・早く作れる理由(`#reason`) → 対応できるもの(`#scope`) → 実績(`#works`) → 開発の流れ(`#flow`) → 中盤CTA(`.mid`) → よくある質問(`#faq`) → 見積もり依頼(`#contact`)。ほかにスマホ用固定CTA(`#stickyCta`)
- `thanks.html` — 見積もり依頼完了ページ（`noindex`）
- `privacy.html` — プライバシーポリシー・運営者情報（フッターからリンク）
- `README_SETUP.md` — 公開・問い合わせ導線・GA4・Google広告のセットアップ手順
- `google_ads_test_plan.md` — 広告テストプラン（キーワード候補・除外キーワード・広告文案・予算・判断基準）
- `lp_revision_notes.md` — LP訴求軸・ビジネスモデルの変更履歴と未確定の検討事項
- `*.bak` — 編集前のバックアップ。`.gitignore` で除外済み

## 開発・確認

ローカル確認はファイルを直接ブラウザで開く、または任意の静的サーバ:

```bash
python3 -m http.server 8000   # http://localhost:8000/index.html
```

公開先は **Render**（https://back-service-lp.onrender.com/ ）。GitHub `takesika/back_service_lp` の `main` ブランチから配信される。

## 編集時の重要な前提

- **GA4は導入済み**: 測定ID `G-S9QLLD91KH` が `index.html` 冒頭に有効な状態で埋め込み済み。同ファイル内に `G-XXXXXXXXXX` のプレースホルダ版とコンバージョン計測スニペット（`gtag_report_conversion`）がコメントアウトで残っている。本番コンバージョンIDを入れる際はこちらを使う。`thanks.html` / `privacy.html` にも同じGoogle tagを必要に応じて貼る。
- **見積もり依頼ボタンの計測**: CTAは4箇所（ヒーロー／中盤／最下部 `#contactButton`／スマホ固定 `#stickyCta`）。各ボタンの `data-cta` 属性（`hero` / `middle` / `bottom` / `sticky`）を使い、ファイル末尾の`<script>`がクリック時に GA4イベント `contact_click`（event_category: `engagement` / event_label: `data-cta` の値）を送る。見積もり依頼導線の主要KPI。CTAを追加する場合は `data-cta` を付ければ計測対象になる。
- **問い合わせ先**: 4つのCTAすべての `href` が見積もり依頼用Googleフォーム `https://forms.gle/2j4mxKfMmTqbw5Bs5`。フォーム差し替え時は4箇所とも編集する。

## 内容（コピー）を編集するときの方針

`lp_revision_notes.md` に訴求軸の決定事項がある。守るべき点:

- 対象は **「作りたいアプリがあり、開発費を抑えたい人」**。サービスはアプリの受託開発。
- 訴求の軸は **「開発作業にAIを活用 → 工数が減る → 安く・早く作れる」**。「AI活用」は開発の進め方のことで、AI機能を組み込んだアプリも開発可能（AI機能なしの一般的なアプリも対象）。
- 対応は **WebアプリとiPhoneアプリ（iOS）のみ**。Androidは非対応と明記する。「スマホが得意」とは書かない。
- **料金は見積もり制・見積もり無料**。金額・料金の目安・「通常の1/3」などの比較表示は根拠がないため一切書かない。公開後の保守・修正も見積もり。
- 返信期限（「◯営業日以内に返信」など）は書かない。
- 運営者の個人名・経歴は載せない。
- **事実・数値・事例は推測で創作しない**。掲載できる実績は「ヨガスタジオの請求処理業務の自動化・SNS広告戦略のAI化・SNS広告のAI生成」の3件のみ。知らない事実・数値・事例を追加しない。
