# Back Service LP 公開・計測セットアップ

## 1. 公開

最短は Netlify Drop。

1. このフォルダをダウンロードして展開する
2. `back_service_lp_public_v1` フォルダごと Netlify Drop にドラッグ&ドロップ
3. 発行されたURLを開いて表示確認
4. 必要なら独自ドメインを設定

Cloudflare Pagesでも公開可能。GitHubリポジトリ連携またはDirect Uploadを使う。

## 2. 問い合わせ導線

`index.html` の次の部分を差し替える。

```html
<a class="btn light" id="contactButton" href="https://forms.gle/REPLACE_WITH_YOUR_FORM" target="_blank" rel="noopener">相談フォームへ</a>
```

候補:

- GoogleフォームURL
- Formspree / Basin などのフォームサービス
- まずは `mailto:メールアドレス`

検証段階では Googleフォームで十分。

## 3. GA4設定

1. Google AnalyticsでGA4プロパティを作成
2. Webデータストリームを追加
3. 測定ID `G-XXXXXXXXXX` を取得
4. `index.html` のGoogle tagコメントアウトを解除
5. `G-XXXXXXXXXX` を実際の測定IDへ置換

## 4. Google広告設定

検証目的なので、検索広告・クリック重視・月3,000円程度から開始。

- 日予算: 100円
- 配信地域: まず日本、必要なら地域を絞る
- キーワード: 広すぎる語は避ける
- 除外キーワード: 求人、無料、テンプレート、資格、意味、とは など

## 5. 最低限見る指標

- 表示回数
- クリック数
- CTR
- 平均クリック単価
- LP滞在・スクロール
- 相談ボタンクリック
- 問い合わせ数

## 6. 検証の判断

1ヶ月または30クリック程度でいったん判断。
問い合わせがゼロでも、クリックされるキーワードやLP内の行動が取れていれば改善材料になる。
