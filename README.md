[English](#english) | [日本語](#japanese)

---

<a id="english"></a>

# HEX — design-art-gallery-digital

> **"The code is the work."**

A design study exploring a fictional generative-art / Web3-native gallery — Feral File / Bright Moments / Art Blocks tier — targeting **engineer-background Web3 collectors aged 25–40** who hold ETH/SOL, live on Discord and Twitter/X, and demand license transparency.

HEX is a fictional platform created for this design study. It is not a real gallery, dealer, artist, or work.

## Overview

| | |
|---|---|
| **Brand** | HEX |
| **Persona** | digital |
| **Live Site (planned)** | `design.art-gallery-digital.riumu.net` |

## Design Concept

- **Color**: True black `#000000` × off-white `#E6E6E6` × electric green `#00FF88` (accent) + error red + link blue
- **Typography**: JetBrains Mono (all) × Space Grotesk (hero only) × Inter (long-form body)
- **Aesthetic**: Terminal × dark-mode native × generative canvas background
- **UX**: Fixed top/bottom HUD (block height + status). Drop hero with countdown + canvas preview. Hover regenerates the canvas. Every artist has a GitHub link.
- **Background**: WebGL or Canvas2D particle field at 30fps cap.

## Tech Stack

- Pure HTML + CSS Custom Properties + Vanilla JS + vanilla WebGL/Canvas
- Google Fonts CDN (JetBrains Mono + Space Grotesk + Inter)
- No framework, no build step — GitHub Pages ready

## Spec

See [spec.md](./spec.md) for the full design specification.

## Part of

This repository is one of four design studies under the **art-gallery persona series**:

| Persona | Brand | Aesthetic |
|---------|-------|-----------|
| bluechip | NORE | Museum-grade white cube |
| emerging | HALF | DIY zine, anti-luxury |
| **digital** | HEX | Terminal, Web3 native |
| institutional | MASS | Scholarly, multilingual |

Navigator: [art-gallery](../README.md)

---

<a id="japanese"></a>

# HEX — design-art-gallery-digital（日本語）

> **「コードが本体である」**

ジェネラティブアート / Web3 ネイティブのギャラリー（Feral File / Bright Moments / Art Blocks 級）のデザイン研究。**25–40代、ETH/SOL を保有しエンジニア出身の Web3 コレクター層** — Discord 常駐、Twitter/X heavy user、ライセンス透明性を要求する層 — に特化した架空プラットフォームのサイトです。

HEX は本デザイン研究のために作成した架空プラットフォームです。実在のプラットフォーム・ディーラー・作家・作品ではありません。

## 概要

| | |
|---|---|
| **ブランド** | HEX |
| **ペルソナ** | digital |
| **公開URL（予定）** | `design.art-gallery-digital.riumu.net` |

## デザインコンセプト

- **カラー**: true black × off-white × electric green（アクセント）+ error red + link blue
- **フォント**: JetBrains Mono（全般）× Space Grotesk（ヒーローのみ）× Inter（長文）
- **世界観**: ターミナル × dark-mode native × ジェネラティブ canvas 背景
- **UX**: 固定 HUD（ブロック高度 + ステータス）。drop ヒーローに countdown + canvas プレビュー。ホバーで再生成。アーティストには必ず GitHub リンク。
- **背景**: WebGL or Canvas2D で粒子フィールド、30fps cap。

## 技術

- 純粋な HTML + CSS Custom Properties + Vanilla JS + バニラ WebGL/Canvas
- Google Fonts CDN（JetBrains Mono + Space Grotesk + Inter）
- ビルド不要で GitHub Pages 対応

## 仕様書

詳細は [spec.md](./spec.md) を参照。

## シリーズ

このリポジトリはアートギャラリー・ペルソナシリーズ4作のうちの1つ。
ナビゲーターページ: [art-gallery](../README.md)
