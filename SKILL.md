---
name: design-art-gallery-digital
description: "art gallery landing-page design study — 'digital' theme/persona (pure HTML/CSS/JS, no build). Use when designing a 'digital'-style art gallery site aesthetic. The code is the work. art galleryの「digital」テーマLPのデザイン参照スキル。"
---

# design-art-gallery-digital

A landing-page **design study** for a fictional **digital**-theme art gallery (pure HTML + CSS + vanilla JS, no build, GitHub-Pages ready). Use this as a **style / design-system reference** when building a similar aesthetic.

架空の「digital」テーマのart gallery LP デザイン研究。同種の世界観を作るときの**スタイル／デザインシステム参照**として使う。

## When to use / 使いどころ
- **EN:** designing a 'digital'-style art gallery site — match its palette, typography and layout discipline.
- **JP:** 「digital」系のart galleryサイトを設計するとき。配色・タイポ・レイアウト規律を流用。

## Bundled assets / 同梱アセット
This skill folder is the reference implementation — start from these files:
- `index.html` — full page markup
- `style.css` — design tokens (CSS custom properties) + layout
- `script.js` — vanilla JS (if present)
- `README.md` — full bilingual doc, brand context and series links

## Design reference / デザイン参照
_Lifted from the repo README — see README.md for the complete, bilingual version._

### Overview
| | |
|---|---|
| **Brand** | HEX |
| **Persona** | digital |
| **Live Site (planned)** | `design.art-gallery-digital.riumu.net` |

### Design Concept
- **Color**: True black `#000000` × off-white `#E6E6E6` × electric green `#00FF88` (accent) + error red + link blue
- **Typography**: JetBrains Mono (all) × Space Grotesk (hero only) × Inter (long-form body)
- **Aesthetic**: Terminal × dark-mode native × generative canvas background
- **UX**: Fixed top/bottom HUD (block height + status). Drop hero with countdown + canvas preview. Hover regenerates the canvas. Every artist has a GitHub link.
- **Background**: WebGL or Canvas2D particle field at 30fps cap.

### 概要
| | |
|---|---|
| **ブランド** | HEX |
| **ペルソナ** | digital |
| **公開URL（予定）** | `design.art-gallery-digital.riumu.net` |

### デザインコンセプト
- **カラー**: true black × off-white × electric green（アクセント）+ error red + link blue
- **フォント**: JetBrains Mono（全般）× Space Grotesk（ヒーローのみ）× Inter（長文）
- **世界観**: ターミナル × dark-mode native × ジェネラティブ canvas 背景
- **UX**: 固定 HUD（ブロック高度 + ステータス）。drop ヒーローに countdown + canvas プレビュー。ホバーで再生成。アーティストには必ず GitHub リンク。
- **背景**: WebGL or Canvas2D で粒子フィールド、30fps cap。

## Tech / 技術
- Pure HTML + CSS Custom Properties + Vanilla JS + vanilla WebGL/Canvas
- Google Fonts CDN (JetBrains Mono + Space Grotesk + Inter)
- No framework, no build step — GitHub Pages ready

## How to apply / 適用方法
1. Reuse `style.css` custom properties (color / type / spacing tokens) as the design-system base.
2. Copy `index.html` layout as the starting structure, then swap brand name and content.
3. Keep the palette, font pairing and layout discipline described above.

---
> The brand is fictional (design study) — replace all brand/content. Full context: see **`README.md`**.
