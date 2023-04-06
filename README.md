## Misskey用カスタムCSSサンプル

## 更新履歴
<details><summary>クリックで展開できます</summary><div>
- 2023/04/01  
  GitHubにお引っ越し中  
  TLでパトロンバッジを非表示にする  
  ホバー時の絵文字を拡大  
  
- 2023/03/17  
  【Update】フォロー解除を押せなくするCSSを、プロフィールを開けば押せるように変更  

- 2023/03/13  
  【Update】絶対時間表記「のみ」にするよう変更  

- 2023/03/12  
  チカチカ絵文字対策にGitHub Pagesでホスティングしてあるものを追加

- 2023/03/08  
  【Update】デッキUIで特定カラムのRenote非表示（セレクタを修正しました）  

- 2023/03/06  
  【Update】自分のノートはリアクションできないようにする  
  特定の人がしたRenoteを非表示にする  

- 2023/03/04  
  スマホで通知受信時のポップアップ非表示  
 TLの画像サイズを変更（高さ）  

- 2023/03/03  
  特定リアクションをノートや通知一覧から非表示  
  フォロー解除ボタンを誤って押せないようにする  
  チャンネル投稿を非表示（HTLまたはリストTLを含むすべて）  
  HTL以外で画像サイズを変更（幅）  
  セレクタの記述を全体的に修正  

- 2023/02/27  
  指定したリアクションをノートや通知欄から消す例  
  スマホ向けカスタムCSSのリアクション選択時の絵文字サイズ調整  

- 2023/02/25  
  指定した絵文字ピッカーのカテゴリ非表示  
  FirefoxでカスタムCSSを使用する際の説明を概要欄に追記  

- 2023/02/20  
  ページ編集時の複製ボタンを無効化  
  特定の絵文字を含んでいるノートを非表示にする  

- 2023/02/12  
  リアクション選択のサイズ調整  

- 2023/02/08  
  チカチカ絵文字をおとなしくする  

- 2023/02/07  
  MFMの極端に大きなテキストを抑制  

- 2023/02/06  
  外部のリアクションをわかりやすくする  

- 2023/02/05  
  スマホ用デザイン調整（Android, iOS）  
  デフォルトUIウィジェットの編集リンク非表示  

- 2023/02/04  
  v13.3.4で確認  
  デッキUIで特定カラムのリアクションをすべて非表示にするCSSを追加  
  指定数よりリアクションが多いとき分かりやすいように文字でマークを付けるようにした  
  特定条件のときノート入力ポップアップ内の要素が表示しきれてなかったのでスクロールするように修正  

- 2023/02/04 初版  
  v13.2.6で確認  
</div></details>

## 説明
個人的に使用しているカスタムCSSをまとめました。  
かゆいところに手が届く…かもしれません。  
設定 → 全般 → カスタムCSSより設定することができます。  

Windows上のChrome(Vivaldi)およびFirefoxのデフォルト/デッキUI, Android 13のデフォルトUI, iPhone SE(iOS 16)のデフォルトUIにて最低限の確認をしています。  
ただし私自身がMisskeyで利用している機能が限られているため、確認していないページで不都合が生じる可能性があります。  
あくまで自己責任にてご使用くださいませ。

アップデートなどにより予告なく動作しなくなる、または表示が崩れることがあるかもしれません。  
その場合はカスタムCSSを一度リセットしてみてください。  
不具合報告はしゅいろさんや村上さんではなく [`@_kanade_`](https://misskey.io/@_kanade_) までお願いいたします。

さらに快適なMisskeyライフのお供になれれば幸いです。  

Stylusを使うとMisskeyの設定でいちいち変えなくても切り替えられるのでオススメです。  
- Chrome, Edgeなど  
https://chrome.google.com/webstore/detail/stylus/clngdbkpkpeebahjckkjfobafhncgmne?hl=ja  
- Firefox  
https://addons.mozilla.org/ja/firefox/addon/styl-us/  

---

### 投稿日時に絶対時間表記にする
```css
time {
    font-size: 0;
}
time:after {
    content: attr(title);
    font-size: 0.9rem;
}
```

---
### Renoteの非表示
#### すべてのスタイル（デフォルト、デッキ、クラシック）に適用する場合
```css
.xcSej.x3762:has(.xBwhh) {
    display: none;
}
```
#### デッキスタイルで特定のカラムのみ対象の場合
```css
/* この場合は左から数えて2番目と3番目のカラムにのみ適用 */
.left section:nth-child(2) .xcSej.x3762:has(.xBwhh),
.left section:nth-child(3) .xcSej.x3762:has(.xBwhh)
{
    display: none;
}
```
---
### デッキUI指定カラムのリアクション全非表示
リアクションしてなんぼのMisskeyですが、ときには見るのがつらいときもあるので、そういうとき心の平穏を保てるかもしれません。  
（自分のノートに全然リアクション付かないのに、あとから投稿されたノートにばかりリアクションが付いたりすると凹むときあるよね…）
```css
/* この場合は左から数えて3番目のカラムにのみ適用 */
div.left section:nth-child(3) .xlT1y
{
	display: none;
}
```

---
### デッキUI 編集サイドバーを非表示
```css
.left > .xECNb {
	display: none;
}
```

---
### デッキUIのポップアップ調整
```css
/* インラインCSSを上書きするために!importantを使っています */
/* そのためドラッグ操作でポップアップのリサイズができません */
.xpAOc:not(.xwAht) {
	width: 720px !important;
	height: 960px !important;
	top: calc(50% - 960px / 2);
    left: calc(50% - 720px / 2);
}
```

---
### ノート入力ポップアップ全般
#### ノート入力ポップアップ
```css
.xpDI4.xxtDg._popup {
	width: 720px;
	height: 960px;
	top: calc(50% - 960px / 2);
	max-width: initial;
	overflow: scroll;
}
```
#### ノート入力欄
```css
.xpDI4.xxtDg._popup .x8B0D {
	height: 400px;
}
```
#### ノートのプレビュー
```css
.xpDI4.xxtDg._popup .xoGjR {
	height: 400px;
    overflow: scroll;
}
```
#### ノート入力での絵文字ピッカー
```css
.xpAOc .omfetrab,
.xpAOc .emojis
{
	width: 720px;
	height: 880px;
}
```

---
### 自分のノートはリアクションできないようにする
```css
/* コード内の`@_kanade_`のところを自分のユーザー名にしてください */
/* 3箇所あります */
.x5yeR > a[href="/@_kanade_"] + .xDn7E .xhAPG > button:nth-last-child(2) {
	display: none;
}

.x5yeR > a[href="/@_kanade_"] + .xDn7E .xlT1y > button:hover {
	pointer-events: all;
	cursor: not-allowed;
}
.x5yeR > a[href="/@_kanade_"] + .xDn7E .xlT1y > button:active {
	pointer-events: none;
}
```

---
### ノートに添付されたGIFアニメをホバー時のみ表示（普段は隠す）
```css
.gqnyydlz.image:has(.gif) img {
	visibility: hidden;
}

.gqnyydlz.image:has(.gif):hover img {
	visibility: visible;
}
```

---
### 長いノートを指定行以降省略する
```css
.xDn7E .x7pHL {
	display: -webkit-box;
	-webkit-box-orient: vertical;
	-webkit-line-clamp: 10; /* この場合は10行まで表示 */
	overflow: hidden;
}

/* ノート全文をホバー（タップ）で表示 */
.xDn7E:hover .x7pHL {
	display: block;
	overflow: visible;
}
```
[プラグインを作成しました](https://misskey.io/@_kanade_/pages/1677390200412)

---
### 大量にリアクションが付いている場合に非表示
```css
/* この場合は11個以上リアクションが付いているとき、11個目以降を非表示にします */
/* n + 11 の 11 の数字を変更する */

/* 隠すだけだと分かりづらいので指定数以上リアクションがある場合は詳細ボタンをアクセントカラーにする（お好みで） */
.xDn7E:has(button:nth-child(11)) .ti-dots:before {
	color: var(--accent);
}

/* 隠すだけだと分かりづらいので指定数以上リアクションがある場合はマークを付ける（お好みで） */
.xDn7E:has(button:nth-child(11)) button:last-child:after {
	margin-left: 28px;
	content: "★";
}

/* 指定数以降のリアクションを省略 */
.xDn7E button:nth-child(n + 11) {
	display: none;
}

/* リアクションをホバー（タップ）で表示 */
.xDn7E:hover button:nth-child(n + 11) {
	display: inline-block;
}
```
疑似クラスの使い方はこちらをご参照ください。  
https://developer.mozilla.org/ja/docs/Web/CSS/:nth-child

---
### デフォルトUIウィジェットの編集リンク非表示
```css
.mk-widget-edit {
	display: none !important;
}
```

---
###外部のリアクションをわかりやすくする
```css
.xDRXD > .xeJ4G.x5kTm.x9Io4:not([src^="https://s3.arkjp.net/"]) {
	filter: grayscale(100%); /* グレースケール */
	pointer-events: none; /* カーソルイベントを無効 */
}
```

---
### MFMの極端に大きなテキストを抑制
```css
.mfm-x2, .mfm-x3, .mfm-x4 {
	font-size: 150%;
    --mfm-zoom-size: 150%;
}

.x7pHL span {
    transform: initial !important;
}
```

---
### チカチカ絵文字の視覚的刺激を軽減する
#### importバージョン
GitHub Pagesでホスティングしてみました。  
以下の記述だけで適用されます。  

ソースはこちら。  
https://github.com/kanade/misskey-css/blob/main/anti-blinking-emojis.css

全部の絵文字見てリストアップするのが一番大変だった…わりと厳しめに指定してあります。  
独断と偏見でサクッと選んだので、要望ありましたらMisskey内やGitHubのプルリクなどでどうぞ。  

```css
/* チカチカ絵文字を白黒にする */
@import url("https://kanade.github.io/misskey-css/anti-blinking-emojis.css");
```
#### 自分で個別に指定する場合
```css
/* [alt=":xxxxxxxx:"] に絵文字の名前を指定する */
.xeJ4G[alt=":emergency:"],
.xeJ4G[alt=":fastparrot:"],
.xeJ4G[alt=":ultrafastparrot:"],
.xeJ4G[alt=":ablobcathyper:"],
.xeJ4G[alt=":eyes_fidgeting:"],
.xeJ4G[alt=":twinsparrot:"]
{
	filter: grayscale(100%);
	opacity: .25;
}
```

---
### リアクション選択のサイズ調整
```css
/* 基本設定 → リアクション一覧の枠 */
.zoaiodol[data-v-543587d0] {
    padding: 6px;
}

/* 絵文字のサイズ */
.zoaiodol > button > img.xeJ4G.x5kTm,
.zoaiodol > button > img.xagin
{
    height: 2.25em;
}

/* 追加ボタンのポップアップサイズ */
.omfetrab.h2[data-v-c741f690] {
    width: 492px;
    height: 640px;
}

/* ==== リアクションシューティング用 ==== */
/* 絵文字選択 */
.omfetrab {
    width: 48em !important;
    height: 640px !important;
}
/* 絵文字のサイズ */
.omfetrab > .emojis section > .body > .item > .emoji {
    height: 2em !important;
}
.omfetrab > .emojis section > .body > .item {
    height: 80px !important;
    width: 80px !important;
}
```

---
### ページ編集時の複製ボタンを無効化
```css
._button.xbaFh.xfjt2:has(i.ti-copy) {
    pointer-events: none;
}
```

---
### 特定の絵文字を含んでいるノートを非表示にする
私の確認不足でしたがワードミュートで普通に対応できますね…  
ワードミュートに設定したあとにTLに流れたノートのみ対象となるようです。  

このカスタムCSSではハードミュート同様にTLから完全に消し去りますが、StylusなどでON/OFFしやすいというメリットがあるかもしれません。
```css
/* 絵文字の名前を指定する */
.xcSej.x3762:has(.x7pHL .xeJ4G[title=":yosano_akiko_is_always_watching_you:"]) {
    display: none;
}
```

---
### 指定した絵文字ピッカーのカテゴリ非表示
CSSだと使いづらかったのでUserScriptを書きました  

https://github.com/kanade/misskey-UserScript/blob/main/userscript-remove-emoji-categories.js

```css
/* この場合は左から数えて2番目と3番目のカラムにのみ適用 */
.emojis > .group[data-v-c741f690]:not(.index) > :nth-child(-n+8),
.emojis > .group[data-v-c741f690]:not(.index) > :nth-child(n+16):nth-child(-n+28),
.emojis > .group[data-v-c741f690]:not(.index) > :nth-child(n+30):nth-child(-n+39),
.emojis > .group[data-v-c741f690]:not(.index) > :nth-child(n+40)
{
	display: none;
}
```

---
### スマホ用デザイン調整（Android, iOS）
AndroidやiPhoneなどディスプレイサイズの小さいデバイス向けに表示を調整します。  
このページに載せているカスタムCSS例をスマホ用に調整したセットです。  

※ ブラウザによってはCSSのプロパティに!importantを付けないと反映されないことがあります。  

例：  
- 効かないかも
  `display: none;`
- 効く
  `display: none !important;`

```css
/* RN非表示 */
.xcSej.x3762:has(div.xBwhh) {
	display: none;
}

/* ウィジェットの編集リンク非表示 */
.mk-widget-edit {
	display: none !important;
}

/* デッキUI 編集サイドバー */
.left > .xECNb {
	display: none;
}

/* 絶対時間表記 */
time:after {
	content: " " attr(title);
}

/* ボタン */
.xApN7 {
	background: none;
	border-top: none;
	grid-template-columns: 1fr 1fr 1fr 1fr;
}

.xyfXN._button:not(.x7c6u) {
	background: rgba(0, 0, 0, 0.3);
}

.xyfXN._button:has(i.ti-apps) {
	display: none;
}

/* MFM */
.mfm-x2, .mfm-x3, .mfm-x4 {
	font-size: 150%;
    --mfm-zoom-size: 150%;
}
.x7pHL span {
    transform: initial !important;
}

/* 外部インスタンスのリアクション */
.xDRXD > .xeJ4G.x5kTm.x9Io4:not([src^="https://s3.arkjp.net/"]) {
	filter: grayscale(100%);
	pointer-events: none;
}

/* 絵文字のカテゴリ非表示 */
.emojis > .group[data-v-c741f690]:not(.index) > section:nth-child(-n+8),
.emojis > .group[data-v-c741f690]:not(.index) > section:nth-child(n+16):nth-child(-n+28),
.emojis > .group[data-v-c741f690]:not(.index) > section:nth-child(n+30):nth-child(-n+39),
.emojis > .group[data-v-c741f690]:not(.index) > section:nth-child(n+41)
{
	display: none;
}
```

---
### 指定したリアクションをノートや通知欄から消す
ノートに付いた指定のリアクションおよび、指定のリアクションされたという通知を消し去ります。  
どうしても見たくない絵文字がある！という場合に「特定の絵文字を含んでいるノートを非表示にする」カスタムCSSや、Misskey公式のワードミュートと組み合わせてお使いください。  
```css
/* ノートに付いたリアクション一覧から消し去ります */
._button.xDRXD.xhTzr:has([title=":chikuwa:"]) {
    display: none;
}

/* 見たくない絵文字の通知を通知欄から消し去ります */
.notification:has(.xAV2R [title=":chikuwa:"]) {
    display: none;
}
```

---
###チャンネル投稿を非表示
既知の不具合：  
チャンネル投稿に対する返信が対象の場合、返信元だけ表示されてしまう。早めに直します…
```css
/* リストは除外したい場合 */
div:has(.xj7PE:first-child) + div .x5yeR:has(.xww2J[href^="/channels/"]) {
    display: none;
}

/* リストも対象にしていい場合 */
.x5yeR:has(.xww2J[href^="/channels/"]) {
    display: none;
}
```

---
### HTL以外で画像サイズを変更
```css
/* 画像の幅を調整 */
/* デッキスタイルで特定のTLのみ */
/* この場合はデッキ左から数えて3番目のカラムにのみ適用 */
.left section:nth-child(3) .xbIzI
{
    width: 50%;
    /* これを入れると中央揃え */
    margin-left: auto;
    margin-right: auto;
}

/* 画像の高さを調整 */
.xutAY.xsfFg {
	height: 100px !important;
    margin-left: auto !important;
    margin-right: auto !important;
}
```

---
### スマホで通知受信時のポップアップ非表示
```css
/* 通知ポップアップを非表示 */
.xpjbG {
    display: none !important;
}
```

---
### 特定の人がしたRenoteを非表示
```css
/* `@_kanade_`のところをRenoteを表示したくないユーザー名にする */
.xcSej:has(.xBwhh [href^="/@_kanade_"]) {
	display: none;
}
```

---
### 通知とフォロー一覧のフォロー解除を押せなくする
```css
/* 通知とフォロー一覧のフォロー解除を押せなくする */
.kpoogebi.active.koudoku-button,
.xkPP6 .kpoogebi.active.full
{
    pointer-events: none;
    filter: grayscale(100%);
}
```

---
### TLでパトロンバッジを非表示にする
```css
/**
 * TLでパトロンバッジを非表示
 */
.x5vC9 {
    display: none !important;
}
```

---
### ホバー時の絵文字を拡大

```css
/**
 * ホバー時の絵文字を拡大
 */
/* ノートテキストに含まれる絵文字 */
.x48yH .xeJ4G:hover {
    transform: scale(2); /* 拡大率（1.5とかの指定もできる） */
    position: relative;
    z-index: 100;
}

/* 通知のリアクションを拡大 */
.xeJ4G.x5kTm.xhB9k.xdOTe {
    width: 120px; /* 拡大したい絵文字の幅 */
}

/* ノートに付いているリアクションを拡大 */
.xeJ4G.x5kTm.xhB9k.xunY9 {
    width: 120px; /* 拡大したい絵文字の幅 */   
}
```

---
### ウィジェット編集

```css
/**
 * iPhone 14などノッチありデバイスでウィジェット編集が押せない問題に対処
 */
.xsN7f {
    top: 2vh !important;
    height: 92dvh !important;
    border-radius: var(--radius);
}

/* ウィジェット編集をアイコンのみ＆位置調整 */
.mk-widget-edit {
    font-size: 0 !important;
    position: absolute;
    right: 0;
    text-decoration: none !important;
    line-height: 2rem;
}
.mk-widget-edit .ti:before {
    font-size: 1.3rem;
}
```

---
### Misskey.io アイコン差し替え

```css
/**
 * Misskey.io アイコン差し替え
 */

:root {
    --misskey-icon: url("https://s3.arkjp.net/emoji/blobcatnomblobdoggo.png") no-repeat;
}

/* サイドバー */
.item._button.instance > img {
    display: none !important;
}
.item._button.instance:before {
    display: inline-block;
    content: "";
    background: var(--misskey-icon);
    height: 48px;
    width: 48px;
    background-size: contain;
}
.banner {
    display: none !important;
}

/* ローディング */
#splash > img {
    display: none !important;
}
#splash:before {
    display: inline-block;
    content: "";
    background: var(--misskey-icon);
    height: 48px;
    width: 48px;
    background-size: contain;
    position: absolute;
    top: 0;
    right: 0;
    bottom: 0;
    left: 0;
    margin: auto;
}

/* サーバー情報 */
.fwhjspax {
    background-image: none !important;
}
.fwhjspax .content > img {
    display: none !important;
}
.fwhjspax .content:before {
    display: inline-block;
    content: "";
    background: var(--misskey-icon);
    height: 64px;
    width: 64px;
    margin: 16px auto 0;
    border-radius: 8px;
    background-size: contain;
}
```


