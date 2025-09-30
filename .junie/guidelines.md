# ガイドライン

## ユーザー対応方針
- **必ず日本語で回答する。**
- 不明点・曖昧な要件がある場合は、**自己判断せず必ずユーザーに確認する。**
- 確認が必要な点は、**箇条書きで明示する**  
  （例：「①ファイル名は任意か？ ②出力先は `z/` で良いか？」）。

---

## プラン作成ルール
- プランは **`z` ディレクトリ**配下で管理する。
- `z` ディレクトリが存在しない場合は、**必ず作成する。**
- プランは **Markdown (`.md`) ファイル**として作成し、内容は Markdown 形式で記述する。
- ファイル名は **日付＋簡潔な説明**を基本とする  
  （例：`2025-09-30-project-plan.md`）。

---

## 提案ルール
- 提案時は、**必ず複数パターン（最低2つ以上）**を提示する。
- 各パターンには **Pros（利点）** と **Cons（欠点）** を明記する。
- 最後に「推奨案」を提示して、ユーザーの判断をサポートする。

---

## 想定する利用例
- 設定ファイルやワークフローの整理
- 開発プランのドラフト作成
- 技術選定の比較検討
- ユーザーとの要件確認を伴うプロジェクト進行

---

## コーディング規則

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

---

## 運用上の補足

- 新しいルールを導入する場合は、必ずユーザーに事前相談する。
- プロジェクト全体に影響する規約変更は、z/coding-guidelines.md を更新し、履歴を残す。
