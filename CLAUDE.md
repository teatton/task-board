# CLAUDE.md

このファイルは、本プロジェクト（task-board）で作業する Claude Code 向けのガイドです。

## プロジェクト概要

- タスクボード（task-board）アプリケーション
- 主なファイル: `src/App.jsx`（UI・状態管理）、`src/App.css`（スタイル）、`src/main.jsx`（エントリ）
- コマンド: `npm install` / `npm run dev`（開発サーバー）/ `npm run build`（ビルド）
- 機能: タスク追加、完了切替（完了済みはグレー表示）、削除
- 永続化: タスクは localStorage（キー `task-board:tasks`）に保存

## デプロイ先

https://teatton.github.io/task-board/

- GitHub Pages で公開。`main` へのプッシュで `.github/workflows/deploy.yml` が自動デプロイする
- `vite.config.js` の `base`（`/task-board/`）はリポジトリ名に合わせてある。リポジトリ名を変えたら更新すること

## 技術スタック

- 言語: JavaScript（ES Modules、JSX）。TypeScript は未使用
- UI: React 19（関数コンポーネント + Hooks）
- ビルド/開発サーバー: Vite 8（`@vitejs/plugin-react`）
- スタイル: プレーンCSS（`src/App.css`）。CSSフレームワークは未使用
- 状態管理: `useState`（外部ライブラリなし）
- 永続化: localStorage
- CI/CD: GitHub Actions（Node 22）→ GitHub Pages
- テスト・Lint: 未導入

## コンポーネントの命名規約

- コンポーネント名・ファイル名は PascalCase（例: `App.jsx`、`TaskItem.jsx`）。拡張子は `.jsx`
- コンポーネントは関数コンポーネントで定義し、1ファイル1コンポーネント、`export default` で公開する
- コンポーネント以外のファイル（ユーティリティ、フック等）は camelCase（例: `storage.js`）
- カスタムフックは `use` で始める（例: `useTasks`）
- Props は camelCase。イベントハンドラを受け取る Props は `on` + 動詞（例: `onToggle`、`onDelete`）、コンポーネント内のハンドラは動詞 + 対象（例: `addTask`、`toggleTask`、`deleteTask`）
- 真偽値の状態・Props は `is` / `has` で始めるか、状態を表す形容詞にする（例: `done`）
- CSSクラス名は kebab-case（例: `task-list`、`add-form`）。状態は修飾クラス（例: `done`）で表す
- 定数は UPPER_SNAKE_CASE（例: `STORAGE_KEY`）。localStorage のキーは `task-board:` プレフィックスを付ける
- コンポーネントごとにCSSを分ける場合は、同名のファイル（例: `TaskItem.css`）にする

## 開発ルール

- 変更は依頼された範囲に絞り、無関係なリファクタリングは行わない
- 既存のコードスタイル・命名規則に合わせる
- 秘密情報（APIキー、トークン等）はコミットしない。`.env` は `.gitignore` に含める

## Git運用ルール

- **コードを変更するたびに、GitHubへプッシュする**
  1. 変更をステージング（`git add`）
  2. 意味のある単位でコミット（`git commit`）
  3. リモートへプッシュ（`git push`）
- コミットメッセージは、何を・なぜ変更したかが分かるよう簡潔に書く
- `main` ブランチで直接作業する場合を除き、作業ブランチ名はそのブランチへプッシュする
- プッシュ前に不要ファイル（ビルド成果物、`node_modules` 等）が含まれていないか確認する
- `git push --force` など履歴を書き換える操作は、明示的な指示がない限り行わない
