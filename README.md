# Gemini CLI Spec-Driven Development

> [!Note]
> このプロジェクトは、[Gemini CLI](https://github.com/google/gemini-cli) を使用して、Kiro IDEの仕様書駆動開発（Spec-Driven Development）をシミュレートします。

## 概要

このプロジェクトは、Gemini CLIの能力を活用して、仕様駆動開発を効率的に行うためのツールセットとワークフローを提供します。
各開発フェーズで定義されたスラッシュコマンドを実行することで、体系的かつ品質の高い開発プロセスを実現できます。

## セットアップ

### 自分のプロジェクトに導入する

このSpec-Driven Developmentの仕組みを自分のプロジェクトに導入するには、以下の2つのファイル/ディレクトリをコピーします。

1. **`.gemini/commands/` ディレクトリ**: `/kiro` コマンド群の定義が含まれています。
2. **`GEMINI.md` ファイル**: Gemini CLIへの指示やプロジェクトのコンテキストが記述されています。

### 初回セットアップ手順

1. 上記2つのファイル/ディレクトリを自分のプロジェクトのルートにコピーします。
2. `GEMINI.md` を開き、自分のプロジェクトに合わせて内容を調整します。
3. ターミナルでGemini CLIを起動し、最初のコマンドを実行します。

    ```bash
    # (推奨) プロジェクトのステアリング文書を作成または更新します
    /kiro:steering

    # 最初の機能仕様を作成します
    /kiro:spec-init "あなたの機能やプロジェクトに関する詳細な説明"
    ```

## 使い方 (Spec-Driven Development Workflow)

開発は、**要件定義 → 設計 → タスク分割** の3フェーズ承認ワークフローに従って進みます。
Gemini CLIで以下のスラッシュコマンドを実行します。

### Phase 0: ステアリング生成 (推奨)

プロジェクトの全体像をAIに理解させるためのドキュメントを生成します。

```bash
# ステアリング文書をインテリジェントに作成・更新
/kiro:steering
```

### Phase 1: 仕様作成

1. **仕様の初期化**

    ```bash
    # 機能説明から仕様の骨格を作成
    /kiro:spec-init "[機能の詳細な説明]"
    ```

2. **要件定義**

    ```bash
    # AIが要件を生成
    /kiro:spec-requirements [feature-name]
    ```

    生成された `.kiro/specs/[feature-name]/requirements.md` を確認し、必要であれば編集します。

3. **技術設計**

    ```bash
    # AIが技術設計書を生成
    /kiro:spec-design [feature-name]
    ```

    実行前に `requirements.md` のレビューが完了しているか確認されます。生成された `design.md` をレビュー・編集します。

4. **タスク分割**

    ```bash
    # AIが実装タスクを生成
    /kiro:spec-tasks [feature-name]
    ```

    実行前に `design.md` のレビューが完了しているか確認されます。生成された `tasks.md` をレビュー・編集します。

5. **実装**

    ```bash
    # AIがタスクを実行
    /kiro:spec-run-tasks [feature-name]
    ```

    AIが仕様承認済みのfeatureの実装タスク（tasks.md）を自動実行し、進捗を管理します。

### Phase 2: 進捗確認

```bash
# 特定機能の現在の進捗と承認フェーズを確認
/kiro:spec-status [feature-name]
```

`tasks.md` 内のチェックボックス (`- [ ]` -> `- [x]`) の状態を元に進捗率が計算されます。

## 3フェーズ承認ワークフロー

このワークフローの核心は、各フェーズで人間によるレビューと承認を必須とすることです。これにより、後工程での手戻りを防ぎ、開発の品質を担保します。

1. **要件定義**: `/kiro:spec-requirements` で生成 → 人間がレビュー＆承認
2. **技術設計**: `/kiro:spec-design` で生成 → 人間がレビュー＆承認
3. **タスク分割**: `/kiro:spec-tasks` で生成 → 人間がレビュー＆承認

実装は、これら3つのフェーズがすべて承認された後に開始されます。

## プロジェクト構造

```
.
├── .gemini/
│   └── commands/
│       └── kiro/
│           ├── spec-design.toml
│           ├── spec-init.toml
│           ├── spec-requirements.toml
│           ├── spec-run-tasks.toml
│           ├── spec-status.toml
│           ├── spec-tasks.toml
│           ├── steering-custom.toml
│           └── steering.toml
├── .kiro/
│   ├── specs/
│   │   └── [feature-name]/
│   │       ├── design.md
│   │       ├── requirements.md
│   │       ├── spec.json      # フェーズ承認状態
│   │       └── tasks.md
│   └── steering/
│       ├── product.md
│       ├── structure.md
│       └── tech.md
├── GEMINI.md
├── README.md
└── (あなたのプロジェクトファイル)
```
