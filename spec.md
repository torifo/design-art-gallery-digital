# HEX — design-art-gallery-digital Spec

**Status:** Approved
**Author:** torifo
**Created:** 2026-05-22
**Updated:** 2026-05-22

---

## 1. Overview

### Problem Statement
デジタル/Web3ネイティブのアートプラットフォーム（Feral File / Bright Moments / Art Blocks / Verse 級）は、伝統的ギャラリーUIをコピーすると「Web3を理解していないギャラリー」に見え、Web3的UIに振り切ると「投機プラットフォーム」に見える。コレクター層は「アート世界の信用」と「ブロックチェーンネイティブの正確性」の両方を求める。

### Goal
"HEX"（16進数の符牒）という架空のジェネラティブアート専門デジタルギャラリーのランディングページを実装し、**ターミナル美学 × リアルタイム風データ × ジェネラティブ背景** × **museum的キュレーション言語** が両立可能であることを検証する。

### Non-Goals
- 実際のウォレット接続・トランザクション
- リアルなブロックチェーンデータフィード
- マーケットプレース機能（floor price / volume の表示）
- ライト/ダーク切替（dark固定）

### Background
- HEX は本デザイン研究のために作成した架空ブランドであり、実在のプラットフォームではない
- `design-art-gallery-digital` リポジトリ予定
- art-gallery シリーズ第3作（デジタルネイティブ軸）

---

## 2. Persona

| 属性 | 詳細 |
|------|------|
| 年齢 | 25–40代 |
| 職業 | エンジニア・スタートアップ創業者・クリプトトレーダー・デジタルアーティスト |
| 資産 | ETH/SOL 保有、年間デジタルアート購入 0.5–50 ETH |
| 行動 | Discord 常駐、Twitter/X heavy user、Art Blocks / Feral File / Verse mint 参加 |
| 共鳴する価値 | コード = アート、generative、on-chain、エンジニア出身アーティスト、ライセンス透明性 |
| 嫌うもの | フィジカル中心のUI、ニュースレター強制、価格非公開、Web2的フォーム |
| 情報源 | Twitter/X, Discord, Farcaster, Are.na, Right Click Save |

---

## 3. User Stories

| ID | Persona | Want to | So that |
|----|---------|---------|---------|
| US-01 | Web3コレクター | 開いた瞬間に「ここはエンジニア出身者の場」と分かる | 信用判定が即座に成立する |
| US-02 | 同上 | 現在 mint 中の作品をリアルタイム風に見たい（残り数・経過時間） | 参加判断ができる |
| US-03 | 同上 | アーティストの GitHub / Twitter リンクを確認したい | コードの本物性を検証できる |
| US-04 | ジェネラティブアーティスト | プラットフォームの技術スタック・ライセンスを確認したい | 自作品の出品判断ができる |
| US-05 | 鑑賞者 | ジェネラティブの実行プレビュー（パラメータ違いで再生成）を見たい | 作品の世界観を体感できる |

---

## 4. Functional Requirements

| ID | Requirement | Priority |
|----|-------------|----------|
| FR-01 | ローディング：ターミナル風 boot シーケンス（`> initializing... > connecting node... > ok`） | P0 |
| FR-02 | Canvas/WebGL ジェネラティブ背景（粒子 or noise field、低 FPS で抑える） | P0 |
| FR-03 | 固定 HUD：左上ブロック高度（偽データ）、右上 timestamp、下部 status line | P0 |
| FR-04 | ヒーロー：現在 drop タイトル + 残り mint 数 + 残り時間カウントダウン | P0 |
| FR-05 | 作品グリッド：thumbnail grid、各カードに hex ID `#A4F3` 表示 | P0 |
| FR-06 | ジェネラティブプレビュー：ホバー or クリックで Canvas が再生成される | P0 |
| FR-07 | Drop 詳細：edition size, license (CC0/MIT/All Rights), artist GitHub | P0 |
| FR-08 | About セクション：technical stack (ETH/SOL/L2), open source links | P1 |
| FR-09 | Status / Stats ストリップ：total works, total artists, total drops（mono numerals） | P1 |
| FR-10 | カスタムカーソル：crosshair（左右上下4本線） | P1 |
| FR-11 | スクロール時のターミナル風カーソル点滅（_） | P2 |
| FR-12 | モバイル対応（375px基準、WebGL は低解像度に） | P0 |
| FR-13 | グリッチ遷移（セクション切替時にスキャンライン1フレーム） | P2 |

---

## 5. Design System

### Color Palette
```css
--bg:        #000000;   /* true black, terminal */
--bg-sub:    #0A0A0A;   /* ほぼ黒、セクション分離 */
--bg-card:   #111111;   /* カードバック */
--fg:        #E6E6E6;   /* off-white, 完全白を避ける */
--fg-muted:  #6E6E6E;   /* secondary text */
--fg-dim:    #3A3A3A;   /* tertiary, 罫線 */
--border:    #1F1F1F;   /* 細罫線、scanline 風 */
--accent:    #00FF88;   /* electric green, terminal classic */
--accent-2:  #FF3C68;   /* error red, mint失敗時など */
--accent-3:  #1FA8FF;   /* link blue, hex string */
```

### Typography
```css
--font-mono:    'JetBrains Mono', 'IBM Plex Mono', 'SF Mono', monospace; /* All */
--font-display: 'Space Grotesk', 'Inter', sans-serif;  /* ヒーロー大型のみ */
--font-sans:    'Inter', sans-serif;                   /* body 長文時のみ */
```
- Google Fonts CDN: JetBrains Mono (wght 400, 500, 700), Space Grotesk (wght 500, 700), Inter (wght 400)
- 基本は全 mono（コード美学の徹底）
- ヒーロー巨大数字のみ Space Grotesk
- Display サイズ: clamp(3.5rem, 10vw, 11rem)、tabular-nums
- Body サイズ: 14px / line-height 1.6 / mono
- HUD サイズ: 11px / mono / accent green

### Numerals & Code
- 数値は必ず tabular-nums + mono
- hex ID は `#0xA4F3` 形式、accent-3 (青) で表示
- block height: `#19,824,310` カンマ区切り、緑
- timestamp: ISO 8601 形式 `2026-05-22T14:23:08Z`

### Spacing
```css
--space-xl: clamp(4rem, 8vw, 7rem);
--space-md: 1.2rem;
--space-sm: 0.5rem;
--grid-gap: 1px;            /* セル間1px、grid 罫線として機能 */
```

### Motion
```css
--ease:    cubic-bezier(0.7, 0, 0.3, 1);
/* loader: typewriter 各行 0.3s stagger */
/* WebGL bg: requestAnimationFrame, 30fps cap */
/* generative preview: canvas regenerate on hover, 0.4s ease */
/* scroll reveal: opacity step (not gradient), 1 frame snap */
/* glitch: clip-path scanline jump 0.08s */
/* terminal cursor: blink 1s infinite step-end */
```

### Background Canvas
- WebGL or Canvas2D で粒子フィールド
- 200–400 粒子、cursor 周辺で密度上昇
- 色は accent green を低彩度で
- prefers-reduced-motion で静止画に切替

---

## 6. Architecture

```
index.html
├── #bg-canvas           # WebGL ジェネラティブ背景
├── .hud-top             # 左上 block高度 / 右上 timestamp
├── .hud-bottom          # ステータスライン "> status: live | latency: 12ms | ..."
├── nav                  # 左 "HEX" mono / 右 drops / artists / about / connect
├── .hero
│   ├── .drop-meta       # > NOW MINTING / Edition 142 of 256
│   ├── .drop-title      # 大型 Space Grotesk タイトル
│   ├── .countdown       # 残り時間 mono tabular
│   └── .preview-canvas  # ジェネラティブ プレビュー (interactive)
├── .stats-strip         # WORKS / ARTISTS / DROPS / VOLUME 数字
├── .section#drops       # 作品サムネ grid、hex ID + edition
├── .section#artists     # アーティストリスト + GitHub
├── .section#about       # 技術スタック・ライセンス
├── footer               # license, status URL, RSS, source
```

---

## 7. Key Design Decisions

| Decision | Chosen | Rationale |
|----------|--------|-----------|
| テーマ | Dark / true black | terminal native、コード環境の延長 |
| Display font | JetBrains Mono 中心 + Space Grotesk | 全 mono は重いので大型のみ可読性確保 |
| アクセント | electric green #00FF88 | terminal classic、Matrix系も継承 |
| 数値表記 | hex / tabular-nums / mono | エンジニア層への信号、信用形成の核 |
| HUD | 固定 top/bottom | "live system" 感、Web3 dapp の文法 |
| ヒーロー | drop title + countdown + preview | 「今 mint 中」が常に主役、現在性の演出 |
| 価格 | ETH 単位、USD 併記 | Web3 単位を主、法定通貨はサブ |
| ジェネラティブプレビュー | hover で再生成 | 「アルゴリズムが本体」を伝える最小UX |
| 背景 | WebGL canvas | 単なる装飾ではなく「動いているプラットフォーム」感 |
| カーソル | crosshair | エンジニアツール感 (Figma / Photoshop) |
| カート | 表示せず "Connect Wallet" | Web3文法、Web2 EC を拒否 |
| Texture | scanline / グリッチのみ | 紙質感は使わない (digital purity) |
| Loader | terminal boot 風 | 第一印象でブランド人格確定 |

---

## 8. Layout Reference

### Hero (Desktop, Dark)
```
┌──────────────────────────────────────────────────────────┐
│ #19,824,310                          2026-05-22T14:23:08Z│  ← HUD
├──────────────────────────────────────────────────────────┤
│ HEX                drops  artists  about  [connect]      │  ← nav mono
├──────────────────────────────────────────────────────────┤
│                                                          │
│  > NOW MINTING                                           │
│                                                          │
│  TERRA / 0xA4F3                  ┌─────────────────┐    │
│  ━━━━━━━━━━━━━━━━━━━━━━           │                 │    │
│  Edition 142 / 256                │  [GEN PREVIEW]  │    │  ← canvas, hover regen
│  Time remaining: 02:14:33         │  Click to seed  │    │
│                                   │                 │    │
│  License: CC0  • by @0xMartine    └─────────────────┘    │
│                                                          │
├──────────────────────────────────────────────────────────┤
│ > status: live | latency: 12ms | gas: 24 gwei            │  ← bottom HUD
└──────────────────────────────────────────────────────────┘
```

### Drops Grid (Desktop)
```
┌────────────────────────────────────────────────────┐
│ ┌──────────┐ ┌──────────┐ ┌──────────┐ ┌────────┐│
│ │ [PREVIEW]│ │ [PREVIEW]│ │ [PREVIEW]│ │[PREVIEW]│  ← canvas thumbs
│ │   #0xA4F3│ │   #0xB291│ │   #0xC014│ │  #0xD7E2│
│ │ 142/256  │ │ 89/100   │ │ 1/1      │ │ 12/∞    │
│ │ 0.5 ETH  │ │ 1.2 ETH  │ │ 4.0 ETH  │ │ 0.08 ETH│
│ └──────────┘ └──────────┘ └──────────┘ └────────┘│
└────────────────────────────────────────────────────┘
```

---

## 9. Accessibility

| 項目 | 実装 |
|------|------|
| コントラスト比 | fg #E6E6E6 on bg #000000 = 17.4:1 (AAA) |
| アクセント緑 | accent on bg = 13.6:1 (AAA) |
| WebGL背景 | prefers-reduced-motion で静止画/単色に |
| カーソル crosshair | カスタムカーソル無効化オプション（settings UI不要、CSS で） |
| 数値 | aria-label でフラット読み上げ ("Edition 142 of 256") |
| ターミナル風アニメ | 自動再生のみ、ユーザー操作必要なし |
| 言語 | `<html lang="en">` |

---

## 10. Tech & Deploy

- 単一 `index.html`、CSS Custom Properties、Vanilla JS
- WebGL: 軽量ライブラリ無し、Vanilla WebGL or Canvas 2D
- フォント: Google Fonts CDN（JetBrains Mono + Space Grotesk + Inter）
- 画像: 静的サムネ + Canvas 動的生成
- デプロイ: GitHub Pages, `design-art-gallery-digital` リポジトリ
- カスタムドメイン: `design.art-gallery-digital.riumu.net` 予定

---

## 11. Inspiration & References

- feralfile.com — collector-grade NFT、museum 的キュレーション + Web3
- brightmoments.io — IRL/digital ハイブリッド、ターミナル風 UI
- artblocks.io — generative art の総本山、テクニカル UI
- verse.works — UK ベース、洗練された Web3 ギャラリー
- vercel.com / linear.app — Web3 ではないが mono/dark UI の参照
- vitalik.eth.limo — エンジニア出身者向け minimal UI

HEX は上記から「**全 mono + dark + 動くキャンバス + ジェネラティブ + 透明ライセンス**」を抽出した架空のブランド。NORE と HALF の真逆 (digital purity)。
