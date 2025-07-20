---
layout: default
title: js.md
parent: Front-end
last_modified_date: 2025-07-20
---

- 💡 ES6 是 JavaScript 的语言标准，不需要启用，现代浏览器天然支持大多数 ES6+ 特性

- 💡 TS 是 JavaScript 的超集，浏览器不能直接执行，必须先 编译成 JavaScript：

```shell
npm install -D typescript
npx tsc --init    # 生成 tsconfig.json
npx tsc           # 编译 .ts 文件为 .js 文件

```

# js ES6 typescript的常见用法

---

## 🧠 一、ES6 常用特性（现代 JavaScript）

### ✅ 1. 变量声明：`let` / `const`

```js
let count = 1;      // 可重新赋值
const PI = 3.14;    // 常量，不可重新赋值
```

### ✅ 2. 箭头函数 `()=>`

```js
const sum = (a, b) => a + b;
```

### ✅ 3. 模板字符串 `${}`

```js
const name = 'Tom';
console.log(`Hello, ${name}!`);
```

### ✅ 4. 解构赋值

```js
const person = { name: 'Tom', age: 20 };
const { name, age } = person;

const arr = [1, 2];
const [a, b] = arr;
```

### ✅ 5. 默认参数、展开/剩余语法

```js
function greet(name = "Guest") {
  console.log("Hello " + name);
}

const arr1 = [1, 2];
const arr2 = [...arr1, 3];   // 展开
const [first, ...rest] = arr2; // 剩余
```

### ✅ 6. 类（Class）

```js
class Animal {
  constructor(name) {
    this.name = name;
  }
  speak() {
    console.log(`${this.name} makes a sound.`);
  }
}
```

### ✅ 7. 模块导入/导出

```js
// a.js
export const PI = 3.14;
export default function greet() {}

// b.js
import greet, { PI } from './a.js';
```

---

## 🦾 二、TypeScript 常用写法（加上类型系统）

### ✅ 1. 类型注解

```ts
let age: number = 18;
let name: string = "Tom";
let isAdmin: boolean = false;
let tags: string[] = ["js", "ts"];
```

### ✅ 2. 函数类型

```ts
function sum(a: number, b: number): number {
  return a + b;
}
```

### ✅ 3. 接口（Interface）和类型（Type）

```ts
interface User {
  id: number;
  name: string;
}

const user: User = {
  id: 1,
  name: "Alice"
};
```

```ts
type Point = { x: number; y: number };
const p: Point = { x: 10, y: 20 };
```

### ✅ 4. 可选属性与只读

```ts
interface Product {
  id: number;
  name?: string;      // 可选
  readonly price: number; // 只读
}
```

### ✅ 5. 泛型

```ts
function identity<T>(arg: T): T {
  return arg;
}

identity<number>(123);
identity<string>("abc");
```

### ✅ 6. 枚举（enum）

```ts
enum Direction {
  Up,
  Down,
  Left,
  Right
}

let dir: Direction = Direction.Up;
```

### ✅ 7. 类型断言（Type Assertion）

```ts
let someValue: any = "hello";
let len: number = (someValue as string).length;
```

---

## 🧩 三、ES6 + TS 综合示例

```ts
// TypeScript class with ES6 syntax
class Person {
  constructor(public name: string, private age: number) {}

  greet(): void {
    console.log(`Hi, I'm ${this.name}, age ${this.age}`);
  }
}

const p = new Person("Alice", 30);
p.greet();
```

---

## 🧠 四、ES6 与 TypeScript 对比

| 特性   | ES6     | TypeScript       |
|------|---------|------------------|
| 类型系统 | ❌ 无     | ✅ 强类型            |
| 接口定义 | ❌ 无     | ✅ interface/type |
| 类支持  | ✅ 有     | ✅ 更强（访问修饰符）      |
| 编译检查 | ❌ 运行时报错 | ✅ 编译时报错          |
| 工具支持 | ✅ 基本提示  | ✅ 更强的智能补全        |

---

## ✅ 推荐使用场景

| 场景                     | 推荐                            |
|------------------------|-------------------------------|
| 快速写脚本 / Demo           | ES6 就够了                       |
| 项目工程开发                 | 强烈推荐 TypeScript               |
| 使用 React / Vue 3 等现代框架 | 推荐 TypeScript，配合 Vite/webpack |

---

## 🚀 Bonus：TS 中常用类型缩写总结

```ts
any         // 任意类型
unknown     // 安全的 any
void        // 无返回值
never       // 永远不会发生（抛异常或死循环）
null / undefined // 空值

Record<string, number> // 对象类型（键是 string，值是 number）
Partial<T>     // 所有属性变为可选
Pick<T, 'a'>   // 从 T 中挑出某个字段
Omit<T, 'a'>   // 从 T 中排除某个字段
```

---

# ✅ ES6 ➜ TypeScript 转换手册（实用对照表）

| ES6 写法                                                | TypeScript 对应写法                                                             | 说明              |
|-------------------------------------------------------|-----------------------------------------------------------------------------|-----------------|
| `let msg = "hello"`                                   | `let msg: string = "hello"`                                                 | 明确类型注解          |
| `function add(a, b) {}`                               | `function add(a: number, b: number): number {}`                             | 参数和返回值都需标注类型    |
| `const arr = [1, 2]`                                  | `const arr: number[] = [1, 2]`                                              | 明确数组中元素类型       |
| `const user = { id: 1, name: "Tom" }`                 | `interface User { id: number; name: string }`<br>`const user: User = {...}` | 使用接口定义结构        |
| `class A { constructor(name) { this.name = name; } }` | `class A { constructor(public name: string) {} }`                           | 构造函数中直接定义属性     |
| `x.toUpperCase()`                                     | `(x as string).toUpperCase()`                                               | 类型断言            |
| `export default func`                                 | 同样写法，但 TS 会检查类型                                                             | 模块系统相同，但需注意类型匹配 |
| 无法判断对象属性合法性                                           | 使用 `Record<string, any>` 或接口断言                                              | 提高类型安全          |

---

# 📘 示例代码对比

## ES6

```js
function greet(name) {
  return "Hello, " + name;
}
```

## TypeScript

```ts
function greet(name: string): string {
  return "Hello, " + name;
}
```

---

# 🧪 常见 ES6 → TS 类型转换参考

| JS 值              | TypeScript 类型          |
|-------------------|------------------------|
| `"abc"`           | `string`               |
| `123`             | `number`               |
| `true / false`    | `boolean`              |
| `[1, 2, 3]`       | `number[]`             |
| `{ name: "Tom" }` | `{ name: string }`     |
| `() => void`      | `() => void`           |
| `Promise`         | `Promise<number>`（带泛型） |

---

# 💡 推荐练习项目（从 ES6 到 TS）

## 🧑‍💻 零基础练习

| 项目名称        | 内容                               | 提示                     |
|-------------|----------------------------------|------------------------|
| 👉 数组工具函数封装 | 实现 `map`, `filter`, `reduce` 等函数 | 加入类型：泛型函数 `T[] => U[]` |
| 👉 表单校验器    | 校验字段是否为空、格式合法等                   | 使用接口描述字段结构             |
| 👉 模拟购物车    | 商品列表 + 购物车 + 结算                  | TS 用接口描述商品、订单结构        |

## 🧰 中级项目

| 项目名称            | 内容                    | 技术                      |
|-----------------|-----------------------|-------------------------|
| ✅ Todo 应用（含增删改） | 表单 + 列表管理             | TypeScript + HTML/React |
| ✅ Markdown 编辑器  | 输入 markdown 文本，右侧实时预览 | TS + marked.js          |
| ✅ JSON 结构校验器    | 输入 JSON，校验字段、类型       | 泛型 + 接口 + 类型断言          |

---

# 🚀 最佳学习资源

| 类型   | 推荐资源                                                                                                           |
|------|----------------------------------------------------------------------------------------------------------------|
| 文档   | [TypeScript 官方文档](https://www.typescriptlang.org/docs/)                                                        |
| 教程   | [tsconfig.dev](https://tsconfig.dev/)（配置教学）<br>[typescript-exercises](https://typescript-exercises.github.io/) |
| 项目模板 | `npx create-react-app myapp --template typescript`                                                             |
| 在线编辑 | [Playground](https://www.typescriptlang.org/play)                                                              |

---

