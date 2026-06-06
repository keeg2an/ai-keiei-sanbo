# ai-keiei-sanbo（AI経営参謀）

Claude API を活用した経営参謀 AI アプリ。経営課題の相談・分析・意思決定支援を行う。

## プロジェクト概要

- 経営課題・戦略に関する AI との対話（チャット）
- 財務・KPI データの入力と分析サポート
- 意思決定のための選択肢提示とリスク評価

## 技術スタック

| 層 | 技術 |
|---|---|
| フロントエンド | React 18 + Vite |
| バックエンド | Node.js + Express |
| AI | Claude API (`claude-sonnet-4-6`) |
| 永続化 | localStorage |

## ディレクトリ構成

```
ai-keiei-sanbo/
├── server/         # Express バックエンド（Claude API 呼び出し）
│   └── index.js
└── client/         # React フロントエンド
    └── src/
        ├── App.jsx
        └── components/
```

## 開発コマンド

```bash
# 初回セットアップ
npm run install:all

# .env を作成し API キーを設定
cp .env.example .env

# フロントエンド + バックエンドを同時起動
npm run dev
```

- フロントエンド: http://localhost:5173
- バックエンド: http://localhost:3001

## Git 運用ルール

### コード変更のたびに GitHub へプッシュする

ファイルを変更・追加したら、必ず以下の手順で即座に GitHub へ反映する。

```
git add <変更ファイル>
git commit -m "<種別>: <変更内容の要約>"
git push origin master
```

- `git add .` や `git add -A` は避け、変更ファイルを明示的に指定する（機密ファイルや不要なバイナリの混入防止）
- `.env` など機密情報を含むファイルは絶対にコミットしない（`.gitignore` で除外を確認してから add する）
- コミットメッセージは日本語で構わない

### コミットメッセージの種別プレフィックス

| 種別 | 用途 |
|------|------|
| `feat` | 新機能の追加 |
| `fix` | バグ修正 |
| `refactor` | リファクタリング（機能変更なし） |
| `style` | スタイル・フォーマット変更 |
| `chore` | ビルド設定・依存関係など |
| `docs` | ドキュメント更新 |

### ブランチ戦略

- 基本は `master` ブランチへ直接コミット
- 大きな機能追加は `feature/<機能名>` ブランチを切って PR でマージする

## コーディング方針

- コメントは「なぜそうするか（Why）」が自明でない箇所にのみ記載する
- エラーハンドリングはユーザー入力・外部 API など境界値にのみ行う
- 抽象化は実際に 3 箇所以上で共通化が必要になってから検討する
- Claude API のシステムプロンプトは `server/index.js` に集約し、フロントエンドには持ち込まない
