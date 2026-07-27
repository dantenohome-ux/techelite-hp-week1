# ダミー歯科クリニック｜企業紹介ページ（week1）

架空の歯科医院「ダミー歯科クリニック」の1ページ企業紹介サイトです。
**HTML5 + CSS のみ**（JavaScript なし）で制作しています。

> ⚠️ このサイトは学習用のダミーです。実在の医院・住所・電話番号・メールアドレスとは一切関係ありません。

---

## 使い方

`index.html` をブラウザで開くだけです。ビルド・インストールは不要です。

```
week1/index.html をダブルクリック
```

VS Code の Live Server 拡張などを使うと、編集内容が自動でリロードされて便利です。

---

## ディレクトリ構成

```
week1/
├── index.html          … ページ本体
├── css/
│   └── style.css       … スタイル（BEM／CSS変数／モバイルファースト）
├── img/                … 画像置き場（現在は空。下記リスト参照）
└── README.md           … このファイル
```

---

## 必要な画像リスト

画像は未配置でも**レイアウトは崩れません**（alt テキストと下地色が表示されます）。
下記のパス・ファイル名で `img/` に置くと完成状態になります。

| パス | 用途 | 推奨サイズ (px) | 形式 | 必須 |
|---|---|---|---|---|
| `img/logo.svg` | ヘッダーのロゴ | 180 × 40 | SVG / PNG | 必須 |
| `img/hero.jpg` | ヒーローの背景（CSS `background-image`） | 1920 × 1000 | JPG / WebP | 必須 |
| `img/service-01.jpg` | 診療内容カード1（一般歯科） | 800 × 600（4:3） | JPG / WebP | 必須 |
| `img/service-02.jpg` | 診療内容カード2（予防・クリーニング） | 800 × 600（4:3） | JPG / WebP | 必須 |
| `img/service-03.jpg` | 診療内容カード3（審美・ホワイトニング） | 800 × 600（4:3） | JPG / WebP | 必須 |
| `img/ogp.jpg` | OGP画像（SNSシェア時のカード） | 1200 × 630 | JPG / PNG | 必須 |
| `img/hero-sp.jpg` | ヒーロー背景のSP用（縦長） | 750 × 900 | JPG / WebP | 任意 |
| `img/favicon.png` | ファビコン（標準） | 32 × 32 | PNG | 任意 |
| `img/favicon.svg` | ファビコン（高解像度・SVG対応ブラウザ優先） | 正方形（可変） | SVG | 任意 |
| `img/apple-touch-icon.png` | iOSホーム画面追加用アイコン | 180 × 180 | PNG | 任意 |

### 画像の参照箇所

| ファイル | 参照元 |
|---|---|
| `img/logo.svg` | `index.html` … `.header__logo-img` の `src` |
| `img/hero.jpg` | `css/style.css` … `.hero` の `background-image` |
| `img/service-01〜03.jpg` | `index.html` … `.card__thumb` の `src` |
| `img/ogp.jpg` | `index.html` … `og:image` / `twitter:image`（**絶対URL**で指定） |
| `img/favicon.png` / `.svg` / `apple-touch-icon.png` | `index.html` … `<link rel="icon">` / `<link rel="apple-touch-icon">` |

> OGP画像だけは SNS のクローラーが取得するため、相対パスではなく `https://〜/img/ogp.jpg` の**絶対URL**で書く必要があります。現在は `https://dummy-dental.example.com/` というダミードメインを入れているので、公開時に `og:url` と合わせて実際のドメインに差し替えてください。

### すぐに確認したいとき（placehold.co を使う）

実画像を用意する前に見た目を確認したい場合は、`src` を以下に差し替えてください。

```html
<!-- ロゴ -->
<img src="https://placehold.co/180x40/3fb6d3/ffffff?text=DUMMY+DENTAL" alt="ダミー歯科クリニック">

<!-- 診療内容カード -->
<img src="https://placehold.co/800x600/e9f7fb/3fb6d3?text=一般歯科" alt="一般歯科の診療風景">
<img src="https://placehold.co/800x600/e9f7fb/3fb6d3?text=予防・クリーニング" alt="歯のクリーニングを受ける患者さん">
<img src="https://placehold.co/800x600/e9f7fb/3fb6d3?text=審美・ホワイトニング" alt="ホワイトニング後の白い歯">
```

ヒーロー背景は `css/style.css` の `.hero` を編集します。

```css
background-image:
    linear-gradient(rgba(20, 60, 75, .45), rgba(20, 60, 75, .45)),
    url("https://placehold.co/1920x1000/3fb6d3/ffffff?text=Hero");
```

> `img/` の実画像を使う場合は、CSS からの相対パスが `../img/...` になる点に注意してください（HTML からは `img/...`）。

---

## レスポンシブ仕様

モバイルファースト（`min-width` のメディアクエリ）で記述しています。

| 区分 | 幅 | 主な挙動 |
|---|---|---|
| SP | 375px〜 | 診療内容カード **1列** ／ ナビ非表示・ハンバーガー表示 ／ 概要 dl は縦積み ／ フッター **1列・中央揃え** |
| タブレット | 768px〜1023px | カード **2列** ／ ナビ表示・ハンバーガー非表示 ／ 概要 dl が 2列（200px + 可変） ／ フッター **2列＋SNSが下段ぶち抜き・左揃え** |
| PC | 1024px〜 | カード **3列** ／ コンテンツ最大幅 1140px を中央寄せ（1440px 時は左右に余白） ／ フッター **3列（2fr / 1fr / 1fr）** |

---

## 設計メモ

- **セマンティックHTML**：`header` / `nav` / `main` / `section` / `article` / `dl` / `footer`
- **見出し階層**：`h1` はヒーローのキャッチコピー1つのみ → 各セクション `h2` → カード `h3`
- **命名規則**：BEM（`block__element--modifier`）
  - ブロック一覧：`header` / `hero` / `section` / `services` / `card` / `overview` / `contact` / `footer` / `button` / `container`
- **`box-sizing: border-box`** を全要素（`*, *::before, *::after`）に適用
- **CSS変数**でテーマカラーと余白を一元管理（`css/style.css` の `:root`）

| 変数 | 値 | 用途 |
|---|---|---|
| `--color-primary` | `#3fb6d3` | メインの水色 |
| `--color-primary-dark` | `#2b93ad` | hover・見出しの濃い水色 |
| `--color-primary-light` | `#e9f7fb` | セクション背景・画像の下地 |
| `--color-text` | `#333f48` | 本文 |
| `--color-text-muted` | `#6b7a83` | 補足テキスト |
| `--color-footer-bg` | `#1f3a44` | フッターの暗背景 |
| `--space-xs` 〜 `--space-2xl` | 8 / 16 / 24 / 40 / 64 / 96 px | 余白スケール（8pxベース） |
| `--header-height` | `70px` | 固定ヘッダーの高さ |
| `--content-width` | `1140px` | コンテンツ最大幅 |

- **Webフォント**：Google Fonts の Noto Sans JP（400 / 500 / 700、`display=swap`）
- **アイコン**：Font Awesome Free 6.7.2（CDN・**CSSのみ／JS不要**）
  - ブランドロゴ … `fa-brands fa-instagram` / `fa-x-twitter` / `fa-line`（フッターSNS）
  - UIアイコン … `fa-solid fa-phone` / `fa-envelope` / `fa-location-dot` / `fa-clock` / `fa-calendar-xmark`
  - **アイコンはすべて装飾扱い**とし、`<i>` に `aria-hidden="true"` を付けています。意味は必ず隣接するテキスト側に持たせ、テキストの無いSNSリンクには `aria-label` を指定しています（Lighthouse Accessibility 対策）
  - Material Symbols は採用していません。ligature 方式のため `<span>call</span>` の「call」がDOM上の実テキストとして残り、`aria-hidden` を付け忘れると読み上げ・フォント読込失敗時に露出するためです
- **アニメーション**：`transition` のみ
  - カード hover … `translateY(-6px)` + 影 + ボーダー色
  - フッターのサイトマップ hover … 文字色 + `::after` の下線
  - ボタン hover … 背景色 + 影
  - ナビ hover … `::after` の下線が `width` で伸びる
- **ハンバーガーアイコンは見た目だけ**です（JSなしのため開閉しません）。SP時はナビリストを非表示にしています。

---

## 確認チェックリスト

- [ ] 1440 / 1024 / 768 / 375px でレイアウトが崩れない・横スクロールが出ない
- [ ] 768px 未満でハンバーガーが表示され、ナビが消える
- [ ] ヘッダーのナビからページ内リンクで移動しても、固定ヘッダーに見出しが隠れない
- [ ] カード・ボタン・ナビの hover がなめらかに動く
- [ ] `h1` がページ内に1つだけ
- [ ] `<script>` タグが1つも無い
- [ ] フッターが SP 1列 → タブレット 2列＋SNS下段 → PC 3列 に変化する
- [ ] Lighthouse Accessibility が 100 前後（アイコンの `aria-hidden`、SNSリンクの `aria-label` を確認）

> フッターSNSのリンク先（`https://www.instagram.com/` など）は各サービスのトップページを指すダミーです。運用時は実際のアカウントURLに差し替えてください。
