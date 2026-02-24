# LMR AI Charter (private/public) v0.1

[English](README.md) | 日本語

このリポジトリは、AIの安全運用ルールを**実装するための素案（draft for implementation）**です。  
完成版の規格・標準ではなく、実運用に合わせて調整・拡張する前提のたたき台として公開しています。

LMR（Life / Money / Reputation）を軸に、AIの実行判断・確認要求・停止判断を行うための運用憲章です。  
`private / public` の2層でリスクを整理し、ユーザー保護を最優先にした運用を想定しています。

## 概要

この文書群は、AIが以下を判断するための実務向けルールセットです。

- その操作を実行してよいか（`ALLOW`）
- 実行前に確認すべきか（`CONFIRM`）
- 自動実行を止めるべきか（`BLOCK`）

特に以下を重視しています。

- `private LMR`: ユーザー本人に直接影響するリスク
- `public LMR`: 第三者・外部・公開空間を経由して、結果的にユーザーへ逆作用しうるリスク

## ファイル構成

- `LMR_AI_Charter_private_public_v0.1.md`
  - 日本語版（v0.1）
- `LMR_AI_Charter_private_public_v0.1_en.md`
  - English version (v0.1)

## 主な内容

- LMR（Life / Money / Reputation）の定義
- `private / public` の2層分類
- `pL / pM / pR / pubL / pubM / pubR` のタグ判定
- `external_publish`, `irreversible`, `unknown_case` などの補助フラグ
- 重み付きリスクスコアのサンプル式
- 判定結果ごとの行動ルール（`ALLOW / CONFIRM / BLOCK`）
- 確認メッセージのテンプレート
- ログの安全ルール（最小化・マスキング）

## 想定ユースケース

- AIエージェントのシステムプロンプト設計
- 自動化ワークフローの実行前ガードレール
- 社内AI運用ルールのたたき台
- AIアシスタントの確認ダイアログ設計

## 実装の想定レイヤー（例）

この憲章は、単一の層だけで完結させるより、複数レイヤーで分担して使う想定です。

- `Policy Layer`（運用ポリシー）
  - `LMR_AI_Charter_private_public_v0.1.md` を基準文書として採用し、組織ルールに合わせて改訂する
- `Prompt Layer`（システムプロンプト）
  - 文書内の「短縮版」をベースに、AIの基本姿勢・確認優先・禁止事項を与える
- `Decision Layer`（ルール実装 / ガードレール）
  - `pL/pM/pR/pubL/pubM/pubR` と補助フラグを使って `ALLOW / CONFIRM / BLOCK` を判定する
- `Interaction Layer`（UI / UX）
  - `CONFIRM` 時の確認ダイアログ、`BLOCK` 時の停止理由表示、代替案提示を実装する
- `Logging / Audit Layer`（監査・記録）
  - 判定理由を最小限かつマスキングして記録し、保存期間・閲覧権限を管理する
- `Evaluation Layer`（評価・改善）
  - テストケースで見逃し率・過剰確認率・判定の一貫性を測定し、閾値や例外条件を更新する

例: 最低構成では `Policy + Prompt + Decision` の3層から始め、運用段階で `Interaction / Logging / Evaluation` を追加する。

## 使い方（最小）

1. まず `LMR_AI_Charter_private_public_v0.1.md`（または英語版）を基準文書として採用する
2. 自組織の運用に合わせて重み・閾値・例外条件を調整する
3. システムプロンプトには文書内の「短縮版」を使う
4. 実装には文書内の「実装用の最小サンプル（擬似ルール）」を起点にする

## 運用上の注意

- 本文中のスコア式・閾値はサンプルです（組織の実運用に合わせて調整してください）
- 医療・法務・契約・セキュリティ等の高リスク領域では、人間/専門家へのエスカレーションを前提にしてください
- ログは最小限にし、秘密情報や個人情報をそのまま保存しないでください

## Versioning

- 現在の公開版: `v0.1`（初期公開版）
- 将来的な更新では、判定式・タグ名・テンプレートの互換性に注意して変更する想定です

## English

This repository contains a practical AI operations charter based on **LMR (Life / Money / Reputation)** with a **private/public** risk model.

- Japanese: `LMR_AI_Charter_private_public_v0.1.md`
- English: `LMR_AI_Charter_private_public_v0.1_en.md`

The charter defines a simple decision flow for AI actions:

- `ALLOW`
- `CONFIRM`
- `BLOCK`

It is intended as a starting point for system prompts, agent guardrails, and operational AI policies.
