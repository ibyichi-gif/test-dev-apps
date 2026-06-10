# テスト開発アプリ — Court 🏐

バレーボールコートをイメージしたアプリギャラリー。
`apps/` 配下に置いた HTML アプリを、コートの 6 ポジションから選択／検索できます。

## 構成

```
テスト開発アプリ/
├─ index.html                      ← ギャラリー（コート画面、/ で検索フォーカス）
├─ apps/
│   ├─ volley-formation-editor/
│   │   ├─ index.html              ← 陣形エディタ v4（2D配置 + コース描画 + 3Dビュー）
│   │   ├─ catalog.html            ← 陣形カタログ（11陣形のSVG図解）
│   │   └─ PLACEMENT_RULES.md      ← 陣形・座標系の設計書
│   └─ sample-court/
│       └─ index.html              ← サンプルアプリ（デプロイ動作確認用）
├─ package.json
├─ vercel.json
├─ .gitignore
└─ README.md
```

## アプリ紹介

### 🏐 Volley陣形エディタ v4（`apps/volley-formation-editor/`）

小学生バレー（16m×8m・ネット2.00m・6役割 L/C/R/S/LB/RB）向けの陣形ボード。

- **7パターン管理**: 01〜06 は自由編集、07 は自動コースシミュレーション
- **シーン切替**: 🛡 ディグ（スパイクレシーブ）/ 📥 レセプション（サーブレシーブ）
- **配置モード**: 選手・ボールをドラッグ（コート外OK）、プリセット11陣形、左右反転
- **コースモード**: 球種（強打/ワンタッチ/ループ/フェイント）・サーブ種（アンダー〜ジャンプ）別に軌道を描画、扇形の到達範囲表示
- **3Dビュー**: Three.js でコートを立体表示。カメラプリセット、身長調整＋🛡/💥ポーズ、弾道再生アニメ
- **チームプロファイル**: 実在チームの身長分布を一括適用
- **↩ 元に戻す（Ctrl+Z）**: 移動・削除・リセットなどを取り消し
- **保存**: localStorage 自動保存 + JSONファイルのエクスポート/インポート
- **❓ 使い方**: アプリ内ヘルプ参照

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

## Vercel に公開する手順（GitHub 連携・推奨）

1. <https://vercel.com> にログイン（GitHub アカウントで OK）
2. **Add New… → Project** を押す
3. リポジトリ `test-dev-apps` を選択 → **Import**
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
