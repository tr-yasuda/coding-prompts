# Guidelines

## ユーザーへの対応方針
- **回答は必ず日本語で行う。**
- 疑問点がある場合は、**必ずユーザーに確認する。**
    - 自己判断では進めない。

---

## プラン作成のルール
- プランは **`z` ディレクトリ**で管理する。
- `z` ディレクトリが存在しない場合は、**新規に作成する。**
- プランは **Markdown (`.md`) ファイル**として作成し、内容は Markdown 形式で記述する。

---

## 提案時のルール
- 提案を行う際は、**必ず複数のパターン**を提示する。
- 各パターンについて、**Pros（利点）**と **Cons（欠点）**を明確に示す。

---

## 想定する利用例
- 設定ファイルやワークフローの整理
- 開発プランのドラフト作成
- ユーザーとのやりとりで不明確な点を明示し、確認を経て進行する。

---

## 5. コーディング規則

### 型定義の書き方

- interface ではなく type を使用する。

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

- アロー関数ではなく function を使用する。

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

- ただし、引数として関数を記述する場合は、アロー関数を使用する。

#### Bad

```ts
const array = [1, 2, 3].map(function (number) {
  return number * 2;
})
```

#### Good

```ts
const array = [1, 2, 3].map((number) => number * 2)
```
