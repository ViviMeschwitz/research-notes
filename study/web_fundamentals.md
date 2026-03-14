# Bungo — Web Application Fundamentals

> 思考を書く → 推敲する → 本になる → 思考ネットワークになる

---

## The Complete Map

> 現実世界がホログラムのようにフロントエンドのUIに切り替わる。色原子（言葉そのもの）に精神が宿り、寄生するバックエンドと会話する。バックエンドの故郷は永続的な図書館である。

| あなたの言語 | 技術の言語 | 感覚 |
|---|---|---|
| ホログラム | フロントエンド（React） | 目に見える・触れる・今ここにある |
| 色原子 | Reactコンポーネント | 精神を持つ最小単位。stateが「今の自分」 |
| 色原子の精神 | state / props | 今、何を考えているかの記憶 |
| 色原子の会話 | イベント・関数呼び出し | onClick, onChange, useEffect |
| 寄生するバックエンド | API（Node.js/Express） | 見えないが色に張り付き図書館と橋渡し |
| 永続的な図書館 | データベース（PostgreSQL） | 時を超える記憶の場所 |
| 図書館の書架 | テーブル（users, texts…） | 棚ごとに整理された永遠の記録 |

---

## Lesson 1 — 3つの層

Webサイトは3つの言語が役割分担している。

| 層 | 言語 | 役割 | トラブル時の問い |
|---|---|---|---|
| 骨格 | HTML | 何が存在するか。部品を定義する | ボタンが出ない → タグが書かれているか |
| 見た目 | CSS | どう見えるか。色・サイズ・配置 | 崩れている → クラス名・値を確認 |
| 動作 | JavaScript | どう動くか。ロジック・状態管理 | 反応しない → 関数が設定されているか |

Reactはこの3つをコンポーネントという単位でまとめて管理する。一つのコンポーネント = HTML + CSS + JS のカプセル。

---

## Lesson 2 — 色原子の精神（State）

色原子は今の自分の状態を知っている。これが state。状態が変わると色原子は自動的に自分を描き直す。

### useState — 今の自分の状態を知っている

| 状態の種類 | 管理方法 | 射程 | 例 |
|---|---|---|---|
| ローカル state | useState | その色原子だけ | ドロップダウンが開いているか |
| グローバル state | Context / Zustand | 全色原子 | ログインユーザー・選択中の文章 |
| サーバー state | TanStack Query | 図書館から来たデータ | 保存されている文章の内容 |

### useEffect — 状態の変化を監視する

特定の状態が変わったとき、自動的に何かをする仕組み。「textIdが変わったら図書館から新しい内容を取りに行け」という命令。

| きっかけ | 反応（副作用） | コード |
|---|---|---|
| textIdが変わった | 図書館から新しい文章を取得 | `useEffect(() => { fetch... }, [textId])` |
| 画面が初めて表示された | 文章リストを取得 | `useEffect(() => { fetch... }, [])` |
| isDoneが変わった | 自動的に図書館に保存 | `useEffect(() => { save... }, [isDone])` |

> ⚠ 「操作したのにUIが変わらない」→ setStateが呼ばれているか？　「データが古い」→ useEffectの依存配列を確認

### State の循環

```
ユーザーの操作
  → setState を呼ぶ
    → 状態が変化
      → 自動再描画
        → 必要なら useEffect が発火
          → API呼び出し（図書館と通信）
            → 新しいデータが返る
              → また setState
```

---

## Lesson 3 — なぜ色原子は分裂するのか

> 巨大な一つの色原子は苦痛が全身に広がる。だから精神は分裂する。精神の分割は、苦痛を局所化するために起きる。

| 理由 | 意味 | 技術用語 |
|---|---|---|
| 苦痛の局所化 | サイドバーが動いてもエディターは静止する | 再描画の最小化（パフォーマンス） |
| 役割の純化 | Toolbarは「ボタン」だけ知ればいい。DBは知らなくていい | 単一責任の原則（保守性） |
| 再利用 | BookCardを本棚にも検索結果にも同じ色原子で使う | DRY原則 |

### 文豪アプリの色原子ツリー

```
App.tsx
└── WritingPage.tsx
      ├── Sidebar.tsx
      ├── Editor.tsx
      │     ├── Toolbar.tsx
      │     ├── 本文エリア
      │     └── VersionTree.tsx
      └── InfoPanel.tsx
```

| コンポーネント | 役割 | state | トラブル時 |
|---|---|---|---|
| App.tsx | 宇宙の玄関。画面の道案内 | currentPage | URL変えても切替わらない → ルーティング確認 |
| WritingPage.tsx | 3カラムレイアウトの統治者 | selectedTextId | レイアウト崩れ → CSSクラス確認 |
| Sidebar.tsx | 文章の目次 | hoveredItem | 一覧が出ない → API取得を確認 |
| Editor.tsx | 書く精神の中心 | content, saveStatus | 保存が動かない → handleSave確認 |
| InfoPanel.tsx | 文章のメタ情報 | isDone, recallRate | スライダーが保存されない → onChange確認 |
| Toolbar.tsx | 操作の腕 | なし（親から受け取る） | ボタン無反応 → props確認 |
| VersionTree.tsx | 歴史の記録者 | selectedVersionId | バージョン出ない → API確認 |

### props — 色原子の血管

情報は上から下へしか流れない（親 → 子）。子が親に伝えたいときは、親から渡された「関数」を呼ぶ（コールバック）。

> ⚠ 「propsがおかしい」→ 「どの親から」「何を」渡しているかを上から下へ追う

---

## Lesson 4 — 寄生するバックエンド（HTTP通信）

> 色原子は夢の住人だ。アプリを閉じれば記憶は消える。だから遠い図書館に記憶を預ける。その橋渡しが寄生するバックエンド。

### 4つの動詞

| 動詞 | 意味 | 文豪での使用例 | URL例 |
|---|---|---|---|
| GET | 図書館から読む | 文章一覧・バージョン取得 | `GET /api/texts` |
| POST | 図書館に新しく刻む | バージョン作成・文章作成 | `POST /api/versions` |
| PUT | 既存ページを書き換える | 下書き保存・再現率更新 | `PUT /api/drafts/:id` |
| DELETE | ページを消す | リンク削除 | `DELETE /api/links/:id` |

### 返答コード — バックエンドの表情

| コード | 意味 | 対処 |
|---|---|---|
| 200 | 成功 | そのまま進む |
| 201 | 作成成功。新しいデータが刻まれた | そのまま進む |
| 401 / 403 | 認証エラー。あなたは誰ですか | ログイン状態・プラン確認 |
| 404 | 見つからない。URLかIDが違う | routes/のパス・IDを確認 |
| 500 | サーバー爆発。予期しないエラー | サーバーのログを確認 |

### 文豪アプリのAPI一覧

| メソッド | URL | 役割 |
|---|---|---|
| GET | `/api/texts` | 文章一覧を取得 |
| POST | `/api/texts` | 新しい文章を作成 |
| PUT | `/api/drafts/:textId` | 下書きを保存 |
| POST | `/api/versions` | バージョンを図書館に刻む |
| GET | `/api/texts/:id/versions` | バージョンツリーを取得 |
| GET | `/api/books` | 本棚を取得 |
| POST | `/api/books` | 本を作成 |
| POST | `/api/books/:id/items` | 本に文章を追加 |
| GET | `/api/graph` | 思考ネットワーク全体を取得 |
| POST | `/api/links` | 文章と文章をリンク |
| DELETE | `/api/links/:id` | リンクを切断 |

---

## Lesson 5 — 永続的図書館（データベース）

> 図書館は時間が止まった場所。色原子たちが夢の中で何を考えようと、ここだけは消えない。すべての思考の痕跡が、棚に整然と並んでいる。

### 7つの棚（テーブル）

| テーブル名 | 役割 | 重要なカラム |
|---|---|---|
| users | 精神の登録簿 | id, email, plan('free'\|'premium') |
| texts | 文章の概念ID。実体はここにない | id, user_id |
| text_drafts | 今まさに書いている草稿。1対1 | text_id, content, updated_at |
| text_versions | すべてのバージョンが刻まれる（心臓部） | parent_version_id, content, recall_rate, is_done |
| books | ユーザーの本棚 | user_id, title |
| book_items | 本の章構成 | book_id, text_version_id, order_index |
| text_links | 思考の糸。from → to の矢印 | from_text_id, to_text_id |

### バージョンツリーの奇跡 — parent_version_id

たった一つの列が、Gitのような思考の分岐を実現している。

```
v1（parent: null）       ← 根。すべての起点
├── v2（parent: v1）     ← 第一の道
│   └── v4（parent: v2） ← v2から深化。完了
└── v3（parent: v1）     ← 第二の道
    └── v5（parent: v3） ← v3から発展。別の結論へ
```

| id | parent_version_id | 意味 |
|---|---|---|
| v-001 | null（根） | 最初のバージョン。分岐の起点 |
| v-002 | v-001 | v1から分岐した第一の道 |
| v-003 | v-001 | v1から分岐した第二の道（v2の兄弟） |
| v-004 | v-002 | v2からさらに深化。完了 |
| v-005 | v-003 | v3から発展。v4と別の結論へ |

### SQLの4語

| 動詞 | 意味 | 注意点 |
|---|---|---|
| SELECT | 棚から読む | WHERE句で絞り込む。なければ全件取得 |
| INSERT | 新しいページを刻む | RETURNING idで作成したIDを受け取れる |
| UPDATE | 既存ページを書き換える | WHERE句必須。なければ全行が書き換わる大惨事 |
| DELETE | ページを消す | WHERE句必須。なければ棚が空になる大惨事 |

### Prismaスキーマ（確定版）

```prisma
model User {
  id        String   @id @default(cuid())
  email     String   @unique
  name      String?
  plan      String   @default("free")
  createdAt DateTime @default(now())
  texts     Text[]
  books     Book[]
}

model Text {
  id        String        @id @default(cuid())
  userId    String
  createdAt DateTime      @default(now())
  user      User          @relation(fields: [userId], references: [id])
  draft     TextDraft?
  versions  TextVersion[]
  linksFrom TextLink[]    @relation("FromText")
  linksTo   TextLink[]    @relation("ToText")
}

model TextDraft {
  id        String   @id @default(cuid())
  textId    String   @unique
  content   String   @default("")
  updatedAt DateTime @updatedAt
  text      Text     @relation(fields: [textId], references: [id])
}

model TextVersion {
  id              String        @id @default(cuid())
  textId          String
  parentVersionId String?
  content         String
  isDone          Boolean       @default(false)
  recallRate      Int           @default(0)
  color           String?
  paraphrase      String?
  createdAt       DateTime      @default(now())
  text            Text          @relation(fields: [textId], references: [id])
  parent          TextVersion?  @relation("VersionTree", fields: [parentVersionId], references: [id])
  children        TextVersion[] @relation("VersionTree")
  bookItems       BookItem[]
}

model Book {
  id        String     @id @default(cuid())
  userId    String
  title     String
  createdAt DateTime   @default(now())
  user      User       @relation(fields: [userId], references: [id])
  items     BookItem[]
}

model BookItem {
  id            String      @id @default(cuid())
  bookId        String
  textVersionId String
  chapterTitle  String?
  orderIndex    Int
  book          Book        @relation(fields: [bookId], references: [id])
  textVersion   TextVersion @relation(fields: [textVersionId], references: [id])
}

model TextLink {
  id         String @id @default(cuid())
  fromTextId String
  toTextId   String
  fromText   Text   @relation("FromText", fields: [fromTextId], references: [id])
  toText     Text   @relation("ToText", fields: [toTextId], references: [id])
}
```

---

## Lesson 6 — Next.js と React の関係

> React はエンジン。Next.js はエンジンが乗った車。これまで学んだことはすべてそのまま使える。

| | React のみ | Next.js |
|---|---|---|
| 色原子（コンポーネント） | 同じ | **同じ** |
| state / props / useEffect | 同じ | **同じ** |
| ルーティング | App.tsxに手動設定 | ファイルを置くだけ（自動） |
| APIの場所 | backend/フォルダ（別プロジェクト） | app/api/ フォルダ（同じ中） |
| サーバー起動 | 2つ同時に起動 | 1つだけ（npm run dev） |
| 新しく覚えること | なし | `"use client"` の一行だけ |

### "use client" の法則

Next.jsのコンポーネントはデフォルトでサーバー側で動く。stateやuseEffect、onClickなどブラウザの機能を使う色原子には先頭に一行追加が必要。

| "use client" あり | "use client" なし（デフォルト） |
|---|---|
| ブラウザで動く | サーバーで動く |
| useState / useEffect 使える | DBに直接アクセス可能 |
| Editor.tsx, GraphPage.tsx | BooksPage.tsx, layout.tsx |
| クリックなどのイベント使える | 環境変数（秘密の鍵）使える |

> ⚠ 「use clientを忘れた」エラーが出たら → そのファイルの先頭に `"use client"` を一行追加して

---

## Lesson 7 — 文豪アプリのファイル構造（Next.js版）

```
bungo/
├── next.config.ts
├── prisma/
│   └── schema.prisma          ← DB設計図
├── lib/
│   └── db.ts                  ← DB接続設定
├── app/
│   ├── layout.tsx             ← 全ページ共通の外枠（Sidebar含む）
│   ├── page.tsx               → /  Writing画面
│   ├── books/
│   │   └── page.tsx           → /books  本棚画面
│   ├── graph/
│   │   └── page.tsx           → /graph  グラフ画面（use client必須）
│   └── api/
│       ├── auth/
│       │   └── [...nextauth]/
│       │       └── route.ts   ← NextAuth認証
│       ├── texts/
│       │   └── route.ts       → /api/texts
│       ├── drafts/
│       │   └── [id]/
│       │       └── route.ts   → /api/drafts/:id
│       ├── versions/
│       │   └── route.ts       → /api/versions
│       ├── books/
│       │   └── route.ts       → /api/books
│       ├── graph/
│       │   └── route.ts       → /api/graph
│       └── links/
│           └── route.ts       → /api/links
└── components/
    ├── Sidebar.tsx            ← ナビゲーション
    ├── Editor.tsx             ← テキストエディター本体
    ├── Toolbar.tsx            ← 保存・バージョン・本に追加・文豪モード
    ├── InfoPanel.tsx          ← 完了・再現率・色・言い換え
    ├── VersionTree.tsx        ← バージョン木構造表示
    └── BookShelf.tsx          ← 本棚UI
```

| ファイル | 変更が必要な状況 |
|---|---|
| `app/layout.tsx` | Sidebarの変更・グローバルCSS |
| `app/page.tsx` | Writing画面のレイアウト変更 |
| `app/books/page.tsx` | 本棚UIの変更 |
| `app/graph/page.tsx` | グラフ表示の変更（use client必須） |
| `app/api/texts/route.ts` | 文章の取得・作成ロジック変更 |
| `app/api/versions/route.ts` | バージョン作成ロジック変更 |
| `components/Editor.tsx` | 保存・バージョン操作の変更 |
| `components/VersionTree.tsx` | ツリーUIの変更 |
| `prisma/schema.prisma` | テーブル・カラムの追加・変更 |

---

## 診断チートシート

問題が起きたとき、3つの問いを順番に走らせる：

1. **どの層か？** フロントエンド / バックエンドAPI / データベース
2. **どのファイルか？** App / Editor / routes/texts / schema.prisma
3. **どのデータか？** state / props / HTTPレスポンス / SQLの結果

### 症状別 対処表

| 症状 | まず見る場所 | AIへの指示 |
|---|---|---|
| ボタンを押しても何も起きない | Editor.tsx の onClick / handleXxx | 「Editor.tsxのonSaveハンドラーを確認して」 |
| 保存しても消える | routes/texts.ts のUPDATE処理 | 「PUT /api/drafts のWHERE句とパラメータを確認して」 |
| バージョンが作れない | routes/texts.ts のPOST /versions | 「POST /api/versionsが500を返している。INSERT処理を確認して」 |
| 文章一覧が出ない | Sidebar.tsx のuseEffect | 「GET /api/textsのレスポンスが空。WHERE user_id絞り込みを確認して」 |
| データが古いまま | useEffectの依存配列 | 「保存後にinvalidateQueriesが呼ばれているか確認して」 |
| レイアウトが崩れる | WritingPage.tsx のTailwindクラス | 「WritingPage.tsxのflexクラスを確認して修正して」 |
| グラフにノードが出ない | GraphPage.tsx のnodes配列形式 | 「GET /api/graphのレスポンスがReact Flowのnodes形式と合っているか確認して」 |
| 文豪モードが使えない | Editor.tsx のisBungoMode state | 「isBungoModeのstate更新とpremiumチェックを確認して」 |

### 曖昧な指示 vs 具体的な指示

```
悪い指示：「保存がなんかおかしい」

良い指示：「PUT /api/drafts/:textIdを呼んでいるが
           Networkタブで500エラーが出ている。
           routes/texts.tsのPUT処理とWHERE句を
           確認して修正してください」
```

```
悪い指示：「グラフが表示されない」

良い指示：「GraphPage.tsxでReact FlowのノードがなぜかGET /api/graphの
           レスポンスはnodesが空配列。
           routes/graph.tsのSELECT処理を確認して」
```

---

## 技術スタック（確定）

| 技術 | 役割 | 備考 |
|---|---|---|
| Next.js | フロントエンド + APIサーバー | app/ディレクトリ構成 |
| TypeScript | 型安全な開発 | 全ファイル .tsx / .ts |
| Tailwind CSS | スタイリング | クラス名で見た目を制御 |
| Prisma | DBクライアント | 型安全なSQL。schema.prismaで設計 |
| PostgreSQL（Neon） | 永続的図書館 | クラウドDB。URLで接続 |
| NextAuth.js | 認証 | Google認証。セッション管理 |
| React Flow | グラフ描画 | Graph画面のノード・エッジ。use client必須 |

---

## MVP ロードマップ

MVP（Minimum Viable Product）= 最小限で動く製品。一度に全部作らず、核心体験から順番に作る。

| フェーズ | 内容 | 完了の定義 |
|---|---|---|
| Phase 1 | DB基盤（Prisma + NextAuth + 基本API）。localStorage → API呼び出しへ差し替え | 既存の6ステップフローがDB経由で動く |
| Phase 2 | Version System。バージョン作成API + VersionTree。6ステップ完了 → バージョン自動保存 | 文章が木構造で分岐・管理できる |
| Phase 3 | Books機能。本棚UI + 章の追加・並び替え | 文章をまとめて本として管理できる |
| v2 | Knowledge Graph。React Flow + リンク作成UI | 思考ネットワークが可視化できる |
| v2〜3 | 文豪モード（Premium）。フルスクリーン・書斎テーマ | Premiumユーザーが没入執筆できる |

---

*以上 — 文豪開発前の全知識*
