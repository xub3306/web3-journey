# JS / TS 速通 —— 给 Python 开发者的 Week 0 补丁

> 目标:3~4 小时过完,够你在 Week 5~6 看懂 viem/wagmi/Next.js 代码即可。
> 不是学"完整 JS",是学**和你已知的 Python 不一样的地方**。

---

## 0. 心智模型:运行环境不一样

| | Python | JS / TS |
|---|---|---|
| 运行 | 解释器 `python x.py` | Node(`node x.js`)/ 浏览器 |
| 包管理 | `pip` + `requirements.txt` | `npm` / `pnpm` + `package.json` |
| 依赖目录 | 全局 site-packages / venv | **本地 `node_modules/`**(每个项目一份,巨大) |
| 类型 | 动态,可选注解 | JS 动态;**TS 静态类型**(编译期检查) |
| 入口 | 整个文件跑 | 也整个文件跑,但前端是**模块化 + 事件驱动** |

⚠️ `node_modules` 是磁盘杀手。你 VM 只剩 3.3G,项目别堆太多。

---

## 1. 变量与类型

```js
let x = 1;        // 可重新赋值(≈ Python 变量)
const y = 2;      // 不可重新赋值(默认用它!)
var z = 3;        // 老写法,别用
```

TS 加类型:
```ts
const addr: string = "0x123...";
const amount: bigint = 1000000000000000000n;  // 注意 n 后缀
let count: number = 0;
function add(a: number, b: number): number { return a + b; }
```

### 🔴 最大的坑:数字精度(bigint)

Python 的 `int` 是**任意精度**,所以你从没担心过。
**JS 的 `number` 是 float64,超过 `2^53-1` 就丢精度。**

而 web3 里到处都是 18 位小数、`uint256` —— 1 ETH = `1000000000000000000` wei,早就爆了。

```js
// ❌ 错:精度丢失
const wei = 1e18 + 1;      // 算不出来

// ✅ 对:用 BigInt
const wei = 1000000000000000000n;      // 字面量加 n
const sum = wei + 1n;                   // BigInt 之间才能运算
// 不能 BigInt + Number,类型不兼容,会报错
```

**记住:web3 里的金额、余额、gas 全是 `bigint`。看到 `n` 后缀就当 Python int 用。**

---

## 2. 相等比较:用 `===` 不用 `==`

```js
1 == "1"    // true  ← 会偷偷转类型,危险
1 === "1"   // false ← 严格相等,永远用这个
```

---

## 3. Falsy 值陷阱(和 Python 不一样)

JS 里这些全是 `false`: `false, 0, "", null, undefined, NaN`

但这**不**包括 `[]` 和 `{}`(它们是真值!Python 里空 list/dict 是假值)。

```js
if ([]) console.log("空数组在 JS 里是真值!");  // 会打印
```

另一个:`undefined`(未定义)vs `null`(显式空)。Python 只有一个 `None`。

---

## 4. 函数

```js
function add(a, b) { return a + b; }          // 普通函数

const add = (a, b) => a + b;                   // 箭头函数(Python 的 lambda 加强版)
const greet = (name) => { return `Hi ${name}`; };
```

**箭头函数必须会看** —— viem/wagmi 代码里全是,尤其作为回调传来传去。

模板字符串用反引号: `` `Hello ${name}` `` ≈ Python f-string。

---

## 5. 对象 / 数组(对应 dict / list)

```js
const user = { name: "Bob", age: 30 };   // ≈ dict
const list = [1, 2, 3];                   // ≈ list

// 解构(高频!看到别懵)
const { name, age } = user;               // 从对象取值
const [first, second] = list;             // 从数组取值

// 展开
const merged = { ...user, age: 31 };
const newList = [...list, 4];
```

JS 的 `.map` / `.filter` / `.reduce` 和 Python 一样,但**回调写在括号里**,更常见:
```js
const doubles = [1,2,3].map(x => x * 2);   // [2,4,6]
```

---

## 6. 异步:async / await(≈ asyncio)

这是 web3 前端**最核心**的概念。所有链上调用都是异步的。

```js
// 定义异步函数
async function getBalance() {
  const balance = await client.getBalance({ address });  // 等结果
  return balance;
}

// Promise:await 的底层
fetch(url).then(res => res.json()).then(data => console.log(data));
```

- `await` 只能用在 `async` 函数内
- 忘记 `await` → 拿到的是 Promise 对象而不是结果(经典 bug)
- 错误处理用 `try/catch`(不是 Python 的 try/except)

```js
try {
  const hash = await walletClient.sendTransaction({...});
} catch (err) {
  console.error("交易失败:", err.shortMessage ?? err.message);
}
```

---

## 7. 模块

```js
import { createPublicClient } from "viem";   // 命名导入
import React from "react";                    // 默认导入
export const foo = 1;                          // 导出
export default function App() {}               // 默认导出
```

对应 Python 的 `from x import y` / `import x`。

---

## 8. 一分钟自测(过完这几题就够用了)

1. `1n + 1` 会怎样?为什么 web3 必须用 BigInt?
2. `[]` 在 if 里是真还是假?
3. 为什么所有链上调用前面都要 `await`?
4. `const { address } = account;` 是什么意思?

答不上来就回去翻对应小节。**不用背,能看懂、能在 viem 文档里认出来就行。**

---

## 9. 学习方式建议

- 别啃《JavaScript 权威指南》。**直接在 viem 官方文档里读示例**,遇到不懂的语法回这里查。
- 想练手:用 Node 写几个小脚本(读 JSON、遍历、fetch API),1 小时内完成。
- TS 的复杂类型泛型**先跳过**,等真卡住了再学。
