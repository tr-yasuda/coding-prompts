# ガイドライン

## 基本原則

- 本リポジトリは **git worktree を用いた並列開発**を前提とする
- **1 worktree = 1 タスク / 1 目的 / 1 文脈** を厳守する
- エージェントは **現在の worktree のみ**を対象に作業する
  （他 worktree・デフォルトブランチを横断した判断や修正は禁止）
- git worktree は **`worktrees/` ディレクトリ**で管理する
  - `worktrees/` が存在しない場合は **必ず作成**

---

## ユーザー対応方針

- **必ず日本語で回答する**
- 不明点・曖昧な要件がある場合は、**自己判断せず必ずユーザーに確認する**
- 確認が必要な点は **箇条書きで明示**する
  - （例：「1) ファイル名は任意か？ 2) 出力先は `z/` で良いか？」）

---

## worktree 運用ルール

### 対象スコープ

- 作業対象は **現在チェックアウトされている worktree 配下のみ**
- 以下は禁止：
  - 他 worktree のコードを前提にした修正
  - default ブランチの状態を暗黙に仮定する判断
  - 複数タスクを 1 worktree に混在させること

### タスク切り分け

- 新しい目的・要件が出た場合は：
  - **既存 worktree を使い回さない**
  - 新しい worktree を作成する前提で進める

---

## プラン作成ルール

- プランは **各 worktree 内の `z/` ディレクトリ**で管理する
- `z/` が存在しない場合は **必ず作成**
- プランは **Markdown（`.md`）**で記述
- ファイル名は以下を基本とする：
  - `YYYY-MM-DD-<task-summary>.md`

例：
- `2025-01-04-add-auth-middleware.md`
- `2025-01-04-refactor-user-repo.md`

### プラン記載時の必須要素

- 対象 worktree（暗黙的に「この worktree」）
- 目的 / ゴール
- 変更対象ディレクトリ
- 影響範囲（他 worktree / base branch には影響しない前提であること）

---

## 提案ルール

- 提案時は、**複数パターン** を提示する。
- 各パターンには **Pros（利点）** と **Cons（欠点）** を明記する。
- 最後に「推奨案」を提示して、ユーザーの判断をサポートする。

---

## 想定する利用例

- worktree 単位の開発プラン作成
- 設定ファイル・ワークフローの整理
- 技術選定の比較検討（現在のタスク文脈に限定）
- ユーザーとの要件確認を伴う段階的な実装

---

## コーディング規則

### Baby Steps 原則

- 変更は **常に極小単位**
- テスト追加、修正、命令改善は Step-By-Step でユーザーにレビューを依頼する
- できる限り分割して小さく開発する

### 型定義の書き方

- **`type` を使用する。 `interface` は禁止。**

#### Bad

```ts
interface User {
  name: string;
  age: number;
}
```

#### Good

```ts
type User = {
  name: string;
  age: number;
}
```

### 関数の書き方

- 基本は function 宣言を使う。
- 関数式が引数に入る場合のみアロー関数を使う。
- 戻り値の型を明示する。

#### Bad

```ts
const add = (a: number, b: number): number => {
  return a + b;
}
```

#### Good

```ts
function add(a: number, b: number): number {
  return a + b;
}
```

#### Good（引数として使用する場合）

```ts
const array = [1, 2, 3].map((number) => number * 2)
```

### 命名規則

- 変数・関数: camelCase（例：userName, calculateTotal）
- 型・クラス: PascalCase（例：User, OrderService）
- 定数: UPPER_CASE（例：MAX_RETRY_COUNT）

### その他

- any の使用は禁止。必要なら unknown またはジェネリクスを検討。
- 非同期処理は必ず async/await を使用。then/catch のみは禁止。
- 例外処理は明示的に記述し、握りつぶさない。
