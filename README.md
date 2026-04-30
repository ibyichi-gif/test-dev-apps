# テスト開発アプリ — Court 🏐

バレーボールコートをイメージしたアプリギャラリー。
`apps/` 配下に置いた HTML アプリを、コートの 6 ポジションから選択／検索できます。

## 構成

```
テスト開発アプリ/
├─ index.html              ← ギャラリー（コート画面）
├─ apps/
│   └─ sample-court/
│       └─ index.html       ← サンプルアプリ（アプリ確認）
├─ package.json
├─ vercel.json
├─ .gitignore
└─ README.md
```

## ローカル確認

```bash
# 方法 A：index.html をダブルクリックでブラウザ表示
# 方法 B：簡易サーバーで起動
npm run dev    # http://localhost:3000
```

## 新しいアプリの追加手順

1. `apps/<アプリ名>/index.html` を作成
2. ルートの `index.html` 内 `apps` 配列にエントリを追加
   ```js
   { pos: 4, title: "新アプリ", desc: "概要", tag: "WIP", url: "apps/<アプリ名>/index.html" }
   ```
3. `pos` は 1〜6（バレーのポジション番号）。前衛：4/3/2、後衛：5/6/1。

## GitHub に push する手順

```bash
cd "C:/Users/市村勇司/Desktop/テスト開発アプリ"
git init
git add .
git commit -m "init: volleyball court app gallery"

# GitHub 側で空のリポジトリを作成（Web）してから：
git branch -M main
git remote add origin https://github.com/<your-account>/test-dev-apps.git
git push -u origin main
```

## Vercel に公開する手順（GitHub 連携・推奨）

1. <https://vercel.com> にログイン（GitHub アカウントで OK）
2. **Add New… → Project** を押す
3. 上で push したリポジトリ `test-dev-apps` を選択 → **Import**
4. Framework Preset は **Other**（静的 HTML なので変更不要）
5. **Deploy** を押す → 数十秒で `https://<project>.vercel.app` が払い出される
6. 以降、`main` に push するたびに自動デプロイされます

## Vercel CLI で公開する場合（任意）

```bash
npm i -g vercel
vercel login        # ブラウザで認証
vercel              # 初回：プロジェクトを作成して Preview デプロイ
vercel --prod       # 本番デプロイ
```

## 補足

- 静的 HTML 構成のため、ビルドステップは不要。
- `vercel.json` でセキュリティヘッダと URL 末尾の `.html` 省略を設定済み。
- ギャラリー側は `index.html` 内の `apps` 配列を編集するだけで増減可能。
