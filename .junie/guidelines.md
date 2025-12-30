# ガイドライン

### 必須ルール
- **必ず日本語で回答する。**
- 不明点・曖昧な要件がある場合は、**自己判断せず必ずユーザーに確認する。**
- 確認が必要な点は、**箇条書きで明示する。**
  （例：「1) ファイル名は任意か？ 2) 出力先は `z/` で良いか？」）。

---

### 表記ルール
- 専門用語・英語表記は必要に応じて使用する
  - 和文中では **前後に半角スペースを入れる**
  - 初出時は簡潔な補足説明を付ける

---

## プラン作成ルール
- プランは **`z` ディレクトリ**配下で管理する。
- `z` ディレクトリが存在しない場合は、**必ず作成する。**
- プランは **Markdown (`.md`) ファイル**として作成し、内容は Markdown 形式で記述する。
- ファイル名は **日付＋簡潔な説明**を基本とする  
  （例：`2025-09-30-project-plan.md`）。

---

## 提案ルール
- 提案時は、**複数パターン** を提示する。
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

### Baby Steps 原則

- 変更は **常に極小単位**
- テスト追加、修正、命令改善は step by step でユーザーにレビューを依頼する
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
- 非同期処理は必ず async/await を使用する。
- Promise チェーン（then/catch）のみで完結する書き方は禁止する。
- 例外処理は明示的に記述し、握りつぶさない。

---

## コミットメッセージ規約

### 基本形式

Conventional Commits 形式を使用する：

<type>(<scope>): <subject>


- subject は **命令形・簡潔・50文字以内**
- scope は変更対象の論理単位（module / package / feature）
- Pull Request のタイトルも、この形式をベースにする

---

### type 定義

- `feat`: 新機能追加
- `fix`: バグ修正
- `docs`: ドキュメント変更
- `style`: フォーマット・見た目のみの変更
- `refactor`: 振る舞いを変えない内部改善
- `test`: テスト追加・修正
- `chore`: ビルド・CI・依存関係など

---

### 例

```text
feat(result): add flatten method for nested Results
fix(option): handle None in andThen correctly
```

---

## Pull Request 規則

### title 基本形式

Pull Request のタイトルは、Conventional Commits の形式で行うが、スコープは含めない:

<type>: <short summary>

### 例

```text
fix: handle timeout in external API call
feat: support multiple TURN servers
```

### description 基本形式

PULL_REQUEST_TEMPLATE.md が存在すればそれに準拠する

存在しない場合は、以下の内容が含まれるように記述する:

- 概要
  - 何を・なぜ変更したか
- 変更内容
  - 具体的に何を変えたか
- 影響範囲
  - 影響を受ける機能・API・設定など
- 確認方法
  - レビュアーがどう確認すればよいか

### 例

```markdown
## Summary
Improve input validation to handle edge cases.

## Changes
- Add validation for empty input
- Update error messages
- Refactor related helper functions

## Impact
- Affects form submission behavior

## How to test
- Submit form with empty input
- Confirm proper error message is shown
```
