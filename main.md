# 便利ツールLT

<img src="http://kiito.me/assets/img/icons/tokiwa.png" style="margin:0; background: none; border:0" width=100vw />
### [ときわ](https://twitter.com/tkw_fms) (B4)

---

## Markdown関連

|||

### Markdownのアツサについて

- 誰かが語ってくれるはず
- Markdown から HTMLへ変換できるため、なんでもMarkdownで書こうとするMD教が存在する (入信済)

---

### [reveal.js](https://revealjs.com/#/)

- **Markdown** で **スライド** が作れるフレームワーク
	- node.jsベース
- GitHub Pages との組み合わせによりGitで管理できてWeb公開もできる
- Webページとしてスライドが公開できるので、共有も便利、どこでも見られる

|||

#### メリット

- Gitによるバージョン管理
- HTMLの恩恵が得られる
	- 共有のしやすさ
	- ハイパーリンク
	- iframeなどの埋め込み
- CSSによる自由度の高いデザイン
	- レスポンシブ
	- デフォルトテーマがかっこいい
- プレゼンターモードあり (`s`)

|||

#### デメリット

- 最初が初心者には難しい
- テーマが少なめ、探しづらい
	- ほとんどが日本語に適応してないのでフォントがネック
	- 一度作ってしまえばコピーするだけなので簡単
- 細かくレイアウトしようとするとHTMLを使うことになる

|||

#### 支援

- `black` テーマの[改造版](https://github.com/TokiwaTools/lecture_tools/blob/master/css/theme/black-rev.css)
- [サンプルテーマ一覧](https://github.com/hakimel/reveal.js/wiki/Example-Presentations)
	- 日本語なし
- 自作スライド
	- [阿原研2017年度末発表会](https://github.com/TokiwaTools/present_2017final)
	- [リーダブルコーザ](https://github.com/TokiwaTools/lecture_readable)
	- [GAS講座(未完成)](https://github.com/TokiwaTools/lecture_gas)
		- タイトル画面に拘りすぎた

---

### [Jekyll](https://jekyllrb-ja.github.io/)

- **Markdown** で 静的**Webページ** が作れるフレームワーク
	- Rubyベース
- GitHub Pagesと連携し、プッシュするだけでWebページができあがる
- ブログ、ポートフォリオなど多数のテンプレートがある

|||

#### メリット

- Gitによるバージョン管理
- 多数のテンプレート
	- しかもかっこいい
- 静的ページなので速い

|||

#### デメリット

- やっぱり細かくやろうとするとHTMLで書く必要がある
- 環境構築がややこしい (Windows)
- 使うテンプレートによってビルドシステムが異なり、ローカルサーバーの実行方法が異なる
	- Gradle, gulp など
	- 最初は有名なテンプレートを使うべき (資料が充実している)

|||

#### 支援

- 自作Jekyll製ページ
	- [総コンHP](https://github.com/ccc-sokon/ccc-sokon.github.io)
	- [ポートフォリオ](https://github.com/TokiwaTools/tokiwatools.github.io)
- [テーマ配布所](http://jekyllthemes.org/)

---

### [Sway](https://sway.com)

- Microsoft製のWebスライド
- PowerPointより簡単に作れる (LT向き)
- 簡単なレスポンシブページとしても

|||

#### 2016年にSway講座を開きました
<iframe width="760px" height="500px" src="https://sway.com/s/RSICxTuIcx03Gk9l/embed" frameborder="0" marginheight="0" marginwidth="0" max-width="100%" sandbox="allow-forms allow-modals allow-orientation-lock allow-popups allow-same-origin allow-scripts" scrolling="no" style="border: none; max-width: 100%; max-height: 100vh" allowfullscreen mozallowfullscreen msallowfullscreen webkitallowfullscreen></iframe>

---

### [Dropbox Paper](https://paper.dropbox.com/)

- Dropboxが最近リリースしたノートサービス
- ブラウザ, iOS, Androidがある
- Markdownで書ける
- 連携
	- Dropboxのファイル
	- Google Calendar

---

### スマホアプリ

- [Spark](https://sparkmailapp.com/) `iOS` `Mac`
	- メーラー、最強、Google, Outlook, Office365対応
- [nicoli](https://itunes.apple.com/jp/app/nicoli-for-%E3%83%8B%E3%82%B3%E3%83%8B%E3%82%B3%E5%8B%95%E7%94%BB/id918184283?mt=8) `iOS` (有料)
	- ニコニコ動画支援ツール
- [VOX](https://itunes.apple.com/jp/app/vox-player/id916215494?ls=1&mt=8) `iOS` `Mac`
	- メディアプレイヤー
- [Instaflash Pro](https://itunes.apple.com/jp/app/instaflash-pro/id888701288?mt=8) `iOS`
	- 画像加工
- [feather](https://itunes.apple.com/jp/app/feather-for-twitter/id793157344?mt=8) `iOS` (一部有料)
	- 廃人向けTwitterクライアント (Tweetdeck風)

---

### Chrome拡張機能

- [Live Streaming Checker](https://chrome.google.com/webstore/detail/live-streaming-checker/akdjdcpngmpdcojlidemkbihnjdmgllg?hl=ja)
	- Youtube Live, Twitch, ニコ生などの配信通知
- [BetterTweetDeck](https://chrome.google.com/webstore/detail/bettertweetdeck/micblkellenpbfapmcpcfhcoeohhnpob?hl=ja)
	- Twitter廃人向けクライアント「Tweetdeck」の廃人向けカスタマイズツール
- [crxMouse Chrome Gestures](https://chrome.google.com/webstore/detail/crxmouse-chrome-gestures/jlgkpaicikihijadgifklkbpdajbkhjo?hl=ja)
	- マウスジェスチャー
- [にこさぽ](https://chrome.google.com/webstore/detail/%E3%81%AB%E3%81%93%E3%81%95%E3%81%BD-%EF%BC%88%E3%83%8B%E3%82%B3%E7%94%9F%E3%82%B5%E3%83%9D%E3%83%BC%E3%83%88%EF%BC%89/kfnogdokhemdbbclknmmjpcnmjmpjknc?hl=ja)
	- ニコ生配信通知

---

### Windowsアプリ

- Mailspring (基本無料)
	- メーラー
- miraCal
	- カレンダー (ストアアプリ)
- John's Background Switcher
	- 私の[ブログ](http://tkw.hateblo.jp/entry/unify_wallpapers)を見よ
- Visual Studio Code
	- エディタ
- ATOK (有料)
	- IME
- QTTabBar
	- エクスプローラ拡張
- MacType
	- フォントレンダラー
- MusicBee
	- メディアプレイヤー
- Massigra
	- 画像ブラウザ

---

### その他

- [Qiita 人気の投稿](https://twitter.com/qiitapoi)
	- プログラミング関連の記事が流れてくる (難)
- Scrapbox `ブラウザ`
	- Markdownライクなノートサービス
- Todoist `ブラウザ` `iOS` `Android` `Chrome`
	- ToDoリストサービス
- Pushbullet
	- スマホ⇔PC間でURLの共有が簡単にできる