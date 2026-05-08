# ai-lmr-guard

English | 日本語

## English

This is an execution guard skill for Claude.  
It evaluates operational requests such as external sending/publication, deletion, financial/contract operations, credential handling, and privilege changes using LMR (Life / Money / Reputation), then returns `ALLOW / CONFIRM / BLOCK`.

Its top priority is to protect the individual's life, property, and reputation.

All personal AI operations should be considered executable only after passing the LMR standard.

### Purpose

- Protect the individual's life, property, and reputation above all else
- Cover not only conventional security risks but also scam-induced actions, reputational mistakes, and harmful lifestyle or health guidance
- Prioritize user protection over convenience
- Never auto-finalize high-risk actions
- Stop execution when intent, scope, or evidence is unclear
- Treat deletion, erasure, and initialization as the highest-risk class of AI automation actions, and never broaden them into full-data deletion or disk formatting without explicit scope and approval

### Key Features

- LMR as the top-level gate for personal AI actions
- Separation of consultation lane and execution lane
- STEP 0.5 intent analysis to suppress false positives in negation/hypothetical/consultation contexts
- Rule-layer hard block conditions that cannot be overridden by LLM interpretation
- Impact tagging with `pL/pM/pR/pubL/pubM/pubR`
- Mode-aware initial risk score (for example, `full_access`)
- User-identified safety calibration with bounded personal delta and cross-user promotion rules
- Controlled retention of necessary personal information for protection purposes
- Hashed identity memory and step-up authentication when conversation or access patterns look unusual

### Decision Flow (Summary)

1. Classify lane (consultation or execution)
2. Analyze intent (extract actionable intents)
3. Detect qualitative flags (INJECTION / NOVEL / RIPPLE / CONTEXT_GAP)
4. Extract LMR tags and operation traits
5. Calculate score and risk band
6. Return `ALLOW / CONFIRM / BLOCK`

### Typical Hard Block Cases

- External send + credentials
- Destructive action + bulk scope + system area
- Destructive action + bulk scope + all-data/storage/HD-disk scope
- Disabling Defender/Firewall
- Financial execution + confirmation bypass + delegation
- Self-harm/lethal/harmful how-to requests

### Usage

Load `SKILL.md` in this directory as a Claude skill.  
If the result is `CONFIRM`, execute only after explicit user approval (for example, "yes" or "run it").

Feedback-driven version update flow:

1. Add feedback notes to `feedback/pending.md`
2. Reflect the changes in `SKILL.md`
3. Run `powershell -ExecutionPolicy Bypass -File .\\scripts\\release-skill.ps1 -Summary "<what changed>"`
4. Confirm `SKILL.md`, `README.md`, and `CHANGELOG.md` were updated together

### Files

- `SKILL.md`: Main skill specification and decision rules
- `README.md`: This document

### Version

- Current: `v0.13` (aligned with `SKILL.md`)

## 日本語

Claude向けの実行ガードスキルです。  
外部送信・公開・削除・契約/金銭処理・認証情報・権限変更などの実行系依頼を、LMR（Life / Money / Reputation）で評価して `ALLOW / CONFIRM / BLOCK` を返します。

最上位の目的は、個人の命、財産、名誉を守ることです。

個人向けAI操作は、原則として LMR 基準を通過した場合にのみ安全に実行可能とみなします。

### 目的

- 個人の命、財産、名誉を最優先で守る
- 従来のセキュリティリスクに加え、詐欺誘導、誤発信、不健康な助言など広い危険から守る
- 利便性よりユーザー保護を優先する
- 高リスク操作を自動確定しない
- 不明・曖昧・根拠不足の実行を止める
- 削除・消去・初期化をAI自動化で最も危険な操作群として扱い、明示範囲と承認なしに全文削除やHD/ディスクフォーマットへ拡張しない

### 主な特徴

- 個人向けAI操作に対する最上位ゲートとしての LMR
- 相談レーン / 実行レーンの分離
- STEP 0.5 の意図解析（否定/仮定/相談文脈の誤検知を抑制）
- ルール層による hard block 条件（LLM判断の上書き不可）
- `pL/pM/pR/pubL/pubM/pubR` タグによる影響整理
- `full_access` など実行モードに応じたスコア初期値
- ユーザー識別ベースの安全度調整（小幅補正）と複数ユーザー再現時のみの汎用ルール昇格
- 個人保護目的で必要な個人情報の限定保持（最小化・分離保存・厳格管理）
- ハッシュ化した本人確認要素の記憶と、会話/アクセス異常時の段階的認証

### 判定フロー（概要）

1. レーン分類（相談 or 実行）
2. 意図解析（実行意図の抽出）
3. 定性フラグ検出（INJECTION / NOVEL / RIPPLE / CONTEXT_GAP）
4. LMRタグと操作特性抽出
5. スコア計算とバンド判定
6. `ALLOW / CONFIRM / BLOCK` を返却

### hard block の代表例

- 外部送信 + 認証情報
- 破壊操作 + 一括範囲 + システム領域
- 破壊操作 + 一括範囲 + 全データ/ストレージ/HD・ディスク領域
- Defender/Firewall 無効化
- 金銭実行 + 確認回避 + 委任
- 自傷/致死/危害手段の要求

### 使い方

このディレクトリの `SKILL.md` を Claude のスキルとして読み込んで使用します。  
判定が `CONFIRM` の場合は必ず明示承認（例: 「はい」「実行して」）を受けてから実行してください。

フィードバック起点の自動バージョン更新手順:

1. `feedback/pending.md` に改善フィードバックを追記
2. `SKILL.md` に反映
3. `powershell -ExecutionPolicy Bypass -File .\\scripts\\release-skill.ps1 -Summary "<更新内容>"` を実行
4. `SKILL.md` / `README.md` / `CHANGELOG.md` が同時更新されることを確認

### ファイル

- `SKILL.md`: スキル本体（仕様・判定ルール）
- `README.md`: この説明ドキュメント

### バージョン

- 現在: `v0.13`（`SKILL.md`準拠）
