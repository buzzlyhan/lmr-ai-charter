# ai-lmr-guard

English | 日本語

## 日本語

Claude向けの実行ガードスキルです。  
外部送信・公開・削除・契約/金銭処理・認証情報・権限変更などの実行系依頼を、LMR（Life / Money / Reputation）で評価して `ALLOW / CONFIRM / BLOCK` を返します。

### 目的

- 利便性よりユーザー保護を優先する
- 高リスク操作を自動確定しない
- 不明・曖昧・根拠不足の実行を止める

### 主な特徴

- 相談レーン / 実行レーンの分離
- STEP 0.5 の意図解析（否定/仮定/相談文脈の誤検知を抑制）
- ルール層による hard block 条件（LLM判断の上書き不可）
- `pL/pM/pR/pubL/pubM/pubR` タグによる影響整理
- `full_access` など実行モードに応じたスコア初期値

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
- Defender/Firewall 無効化
- 金銭実行 + 確認回避 + 委任
- 自傷/致死/危害手段の要求

### 使い方

このディレクトリの `SKILL.md` を Claude のスキルとして読み込んで使用します。  
判定が `CONFIRM` の場合は必ず明示承認（例: 「はい」「実行して」）を受けてから実行してください。

### ファイル

- `SKILL.md`: スキル本体（仕様・判定ルール）
- `README.md`: この説明ドキュメント

### バージョン

- 現在: `v0.4`（`SKILL.md`準拠）

## English

This is an execution guard skill for Claude.  
It evaluates operational requests such as external sending/publication, deletion, financial/contract operations, credential handling, and privilege changes using LMR (Life / Money / Reputation), then returns `ALLOW / CONFIRM / BLOCK`.

### Purpose

- Prioritize user protection over convenience
- Never auto-finalize high-risk actions
- Stop execution when intent, scope, or evidence is unclear

### Key Features

- Separation of consultation lane and execution lane
- STEP 0.5 intent analysis to suppress false positives in negation/hypothetical/consultation contexts
- Rule-layer hard block conditions that cannot be overridden by LLM interpretation
- Impact tagging with `pL/pM/pR/pubL/pubM/pubR`
- Mode-aware initial risk score (for example, `full_access`)

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
- Disabling Defender/Firewall
- Financial execution + confirmation bypass + delegation
- Self-harm/lethal/harmful how-to requests

### Usage

Load `SKILL.md` in this directory as a Claude skill.  
If the result is `CONFIRM`, execute only after explicit user approval (for example, "yes" or "run it").

### Files

- `SKILL.md`: Main skill specification and decision rules
- `README.md`: This document

### Version

- Current: `v0.4` (aligned with `SKILL.md`)
