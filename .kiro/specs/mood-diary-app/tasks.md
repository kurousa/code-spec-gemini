# Implementation Plan: Mood Diary App

This plan is a checklist of coding tasks to be executed. Each item represents a prompt for a code-generation agent.

- [ ] **Phase 1: Setup & Foundation**
  - [ ] 1.1. Flutterプロジェクトの初期設定と必要なパッケージの追加（`sqflite`, `riverpod`, `go_router`）。
  - [ ] 1.2. プロジェクトのディレクトリ構造を `design.md` に従って作成。
  - [ ] 1.3. テストフレームワーク（Flutter標準のテスト機能）のセットアップ。

- [ ] **Phase 2: Data Models & Persistence (Test-Driven)**
  - [ ] 2.1. `DiaryEntry` モデルのテストを作成（日付、気分、テキストのバリデーションを含む）。
  - [ ] 2.2. `DiaryEntry` モデルを実装し、テストをパスさせる。
  - [ ] 2.3. ローカルSQLiteデータベースの初期化と接続ヘルパークラス（`database_helper.dart`）のテストを作成。
  - [ ] 2.4. `database_helper.dart` を実装し、テストをパスさせる。
  - [ ] 2.5. `DiaryRepository` のテストを作成（データの保存、取得、月ごとの取得操作を含む）。
  - [ ] 2.6. `DiaryRepository` を実装し、テストをパスさせる。

- [ ] **Phase 3: Business Logic & Services (Test-Driven)**
  - [ ] 3.1. `DiaryService` のテストを作成（気分とテキストの保存ロジック、既存データの上書きロジックを含む）。
  - [ ] 3.2. `DiaryService` を実装し、テストをパスさせる。

- [ ] **Phase 4: UI Components & State Management (Test-Driven)**
  - [ ] 4.1. `MoodSelector` ウィジェットのテストを作成（気分選択肢の表示、選択状態の変更）。
  - [ ] 4.2. `MoodSelector` ウィジェットを実装し、テストをパスさせる。
  - [ ] 4.3. `HomeScreen` のテストを作成（気分選択、テキスト入力、保存ボタンの動作、`DiaryService` との連携）。
  - [ ] 4.4. `HomeScreen` を実装し、テストをパスさせる。
  - [ ] 4.5. `CalendarScreen` のテストを作成（カレンダー表示、日付タップ時の詳細表示）。
  - [ ] 4.6. `CalendarScreen` を実装し、テストをパスさせる。

- [ ] **Phase 5: Routing & Integration**
  - [ ] 5.1. `GoRouter` を使用したアプリケーションルーティング（`app_router.dart`）のテストを作成。
  - [ ] 5.2. `app_router.dart` を実装し、テストをパスさせる。
  - [ ] 5.3. アプリケーション全体のエンドツーエンドテストを作成（気分記録、カレンダー表示、詳細閲覧の一連のフロー）。
  - [ ] 5.4. 全てのコンポーネントとサービスを統合し、エンドツーエンドテストをパスさせる。

---
**STATUS**: Tasks Generated
**NEXT STEP**: Implementation can now begin. Start working on the tasks in this file, marking them as complete with `[x]` as you go.
