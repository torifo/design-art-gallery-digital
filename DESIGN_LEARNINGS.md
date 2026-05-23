# HEX Design Learnings

## 目的

digitalペルソナは、エンジニア出身でETH/SOLを保有する25–40代のWeb3コレクター。彼らはDiscord常駐、GitHubで作品のコードを読む層であり、ホワイトキューブ的体験には何の権威も感じない。HEXでは、ターミナルとブロックチェーンエクスプローラそのものをWebの審美原則に据え、コードと作品が等価であるという思想を体現した。

このプラットフォームは架空ブランドであり、実在のプラットフォーム・作家・作品ではない。

## 設計したこと

- ヘッダーとフッターを HUD（Heads-Up Display）化し、ブロック高度と接続ステータスを常時表示。「いまブロックチェーン上にいる」という体感を作った。
- ヒーローは drop（販売開始）のカウントダウン+ canvas プレビュー。ホバーで再生成し、生成系作品の本質を直接見せる。
- アーティストプロフィールには必ず GitHub リンクを置き、「コードを読める」ことを前提とした。
- 背景に WebGL 粒子フィールドを 30fps cap で動かし、生命感のあるダークモードを成立させた。

## CSS

主要なCSS判断:

```css
:root {
  --bg: #000000;
  --fg: #e6e6e6;
  --accent: #00ff88;       /* electric green, terminal phosphor */
  --link: #5aa9ff;
  --error: #ff3a3a;
  --font-mono: 'JetBrains Mono', ui-monospace, monospace;
  --font-hero: 'Space Grotesk', sans-serif;
  --font-body: 'Inter', sans-serif;
}

/* HUD that survives scroll */
.hud {
  position: fixed;
  inset: 0 0 auto 0;
  font-family: var(--font-mono);
  font-size: .72rem;
  letter-spacing: .15em;
  border-bottom: 1px solid color-mix(in srgb, var(--accent) 30%, transparent);
}

/* generative canvas behind everything */
canvas#field {
  position: fixed; inset: 0;
  z-index: -1;
  opacity: .55;
  mix-blend-mode: screen;
}
```

色は黒・白系の少数+蛍光グリーン+ステータス色（link / error）に厳格に絞った。情報パネルの密度は CSS Grid と `font-feature-settings: 'tnum'` で揃え、エンジニアが読みやすい数値ブロックを作った。

## アニメーション

- canvasの粒子は30fps cap、`prefers-reduced-motion: reduce` で停止。
- 作品サムネは hover で再生成（loadではなく interaction で動く）— 「インタラクションが作品の一部」であるため。
- ローダーは出さない代わりに、ブロック高度の数字が常にカウントアップする小さな動きで「生きている」感を維持。

## フォント

- 全般: `JetBrains Mono`
- Hero only: `Space Grotesk`
- 長文本文: `Inter`

JetBrains Monoはコード以外でも軸として機能する。Space Grotesk はヒーロー1箇所のみに使い、見出しが「コード以外の声」を持つことを示唆した。

## ボタン

ボタンはターミナルプロンプトの再解釈。

```
$ mint --drop=0042 ▌
$ connect_wallet ▌
```

`▌` のカーソル点滅を CSS animation で再現し、クリック対象であることを示す。背景塗りはせず、線と文字のみ。

## UI/UX

- 価格は ETH 表記が主、USD 換算は subtle に。
- すべてのアセットページに License: CC BY 4.0 / CC0 などのバッジを必須化。
- 作家ページから直接 GitHub repo と Etherscan address に飛べる導線。
- Discord 招待リンクをグローバルナビに据え置く（コミュニティが製品である、というWeb3の前提）。

## レイアウト

3カラムの密なグリッド。コードエディタの行番号ガターを参考に、左端にブロック高度・タイムスタンプを通している。

スクロール時にもHUDが上下に貼り付き、画面の中央ペインだけがコンテンツとして移動する — ターミナルマルチプレクサ（tmux）の精神を踏襲。
