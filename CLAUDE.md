# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Git運用ルール

- コードに変更を加えたら、その都度コミットし、GitHubにプッシュすること。変更を溜め込まず、こまめにプッシュする。
- コミット前に `git status` / `git diff` で変更内容を確認してからコミットする。
- コミットメッセージは変更内容が分かるよう簡潔に記載する。
- push前にユーザーの許可を得ていない破壊的操作（force push、reset --hard など）は行わない。

## デプロイ先

https://yukiiy6-lab.github.io/task-board/

- `main` ブランチへのpushをトリガーに、GitHub Actions（`.github/workflows/deploy.yml`）が自動でビルド・デプロイする。
- ローカルビルド確認は `npm run build` で行い、`dist/index.html` 内のアセットパスが `/task-board/` プレフィックス付きになっていることを確認する（`vite.config.js` の `base` 設定に依存）。

## 技術スタック

- React 19 + Vite（`@vitejs/plugin-react`）
- 状態管理はReact標準の `useState` / `useEffect` のみ（外部状態管理ライブラリは未導入）
- データ永続化は `localStorage`（`src/App.jsx` の `STORAGE_KEY` 経由）
- スタイルはプレーンCSS（コンポーネント名と対応する `.css` ファイルを直接importする方式。CSS-in-JSやCSS Modulesは未導入）
- Lintは ESLint（`npm run lint`）

## コンポーネントの命名規約

- コンポーネントファイルは `PascalCase.jsx`（例: `App.jsx`）。コンポーネント名とファイル名を一致させる。
- 対応するスタイルは同名の `.css` ファイル（例: `App.jsx` ↔ `App.css`）として `src/` 直下にコンポーネントごとに配置する。
- ルート共通のグローバルスタイルのみ `index.css` に置く。
- コンポーネントは `export default` で1ファイル1コンポーネントとする。
