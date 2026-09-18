# Web3 转型计划 —— 测试工程师 → 远程岗

> 版本 v1 · 2026-09-18 · 按「工作日 2h + 周末 5h ≈ 20h/周」定制
> 总预算:8 周 × 20h = **160 小时**

---

## 0. 前提(先认清,再动手)

- 你的基础:会写脚本,Python 能开发小型项目。**有编程思维,但不是专业工程师。**
- 你的目标:**远程 web3 岗**。远程岗的真实门槛不是技术,是 **英语 + 公开可验证的输出(GitHub/X)**。
- 160 小时能把你送到:**能过初级技术面 + 有可展示作品集**。拿 offer 大概率在 2~4 个月内。
- 结论:**技术两条腿走路,英语从第一天并行,不能等。**

### 关键决策:Python 还是 JS/TS?
- **主力求职栈必须是 Solidity + TypeScript**(生态决定的,没法绕)。
- 但好消息:**Foundry 的测试是用 Solidity 写的,不是 JS**。所以你可以先精通 Solidity + 测试,**JS/TS 只在前端阶段才需要**,前期压力小很多。
- Python 的用法:**只做加速工具**(链上数据脚本、web3.py 交互、自动化监控),不作为求职主线。

---

## 1. 时间预算(160h 怎么花)

| 模块 | 时长 | 占比 |
|---|---|---|
| 链原理 + Solidity 语法 | 30h | 19% |
| Foundry + 测试(fuzz/invariant) | 30h | 19% |
| 安全 CTF + 漏洞分析 | 25h | 16% |
| 全栈 dApp(TS/viem/wagmi) | 35h | 22% |
| 综合项目(简历主力) | 25h | 16% |
| 英语 + 求职包装 + 投递 | 15h | 8% |

---

## 2. 每日/每周节奏模板

**工作日(2h):**
- [ ] 1.0h 新课 / 概念学习
- [ ] 0.5h 动手写代码(必须写,不能只看)
- [ ] 0.3h 技术英语(读英文文档 1 段 + 写 3 句英文笔记)
- [ ] 0.2h 复盘记录(今天学到什么 / 卡在哪)

**周末(5h):**
- [ ] 3.5h 深度动手(项目 / CTF,集中火力)
- [ ] 1.0h 复习本周 + 补漏
- [ ] 0.5h 公开输出(写笔记 / 发 X / 提 GitHub commit)

**铁律:** 每天都提交代码到 GitHub(哪怕很小),这是远程岗面试官唯一信得过的证据。

---

## 3. 八周详细计划

### Week 0｜环境 + 校准(本周内完成)
- [ ] 装 Foundry(`curl -L https://foundry.paradigm.xyz | bash` → `foundryup`)
- [ ] 装 Node 20+ / pnpm
- [ ] 注册 GitHub,建一个 public 仓库 `web3-journey`,每天都 commit
- [ ] 注册 X(Twitter)账号 -> 英文 bio 写 "Test engineer → Smart Contract Dev"
- [ ] JS/TS 速通(只学差异点,3~4h 搞定):变量、函数、async/await、模块、TS 类型基础
- [ ] 注册 Cyfrin Updraft,看「Blockchain Basics」

### Week 1–2｜链的原理 + Solidity
- [ ] 账户模型:EOA vs Contract、nonce、余额
- [ ] gas 机制、EIP-1559(base fee / priority fee)
- [ ] 交易生命周期:签名 → mempool → 打包 → 执行 → revert
- [ ] Solidity:类型、`payable`、`msg.sender`、modifier、事件、`calldata/memory/storage`
- [ ] 用 Foundry 从零写一个 ERC20(不抄 OpenZeppelin)
- [ ] `forge test` 写第一个单元测试
- **产出:** GitHub 上有一个自写 ERC20 + 测试通过

### Week 3｜合约模式 + 测试(你的主场)
- [ ] ERC721 / ERC1155、OpenZeppelin 库
- [ ] 权限模式:`Ownable`、`AccessControl`
- [ ] 代理升级(UUPS / Transparent)——**存储冲突是重点坑**
- [ ] Foundry 测试四件套:unit / **fuzz** / **invariant** / fork
- [ ] `forge coverage` 看覆盖率
- **产出:** 一个带 fuzz + invariant 测试的合约仓库

### Week 4｜安全(差异化核心竞争力)
- [ ] 漏洞类型:重入、integer、oracle 操纵、签名重放、权限缺陷、代理存储冲突
- [ ] 通关 **Ethernaut**(18 关),**每关写 200 字漏洞分析**
- [ ] 读 **Solodit** 上 5 份真实审计报告
- **产出:** `security-notes` 仓库,18 篇漏洞分析

### Week 5–6｜全栈 dApp
- [ ] TypeScript 补齐(async/await、类型、Promise)
- [ ] viem(替代老 ethers.js)+ wagmi + RainbowKit
- [ ] Next.js 搭前端:连接钱包 → 读合约 → 发交易 → 监听事件
- [ ] 处理 pending / failed / revert 状态(测试人在这里有优势)
- [ ] 用 **scaffold-eth-2** 快速起原型
- [ ] 部署到 Sepolia + 一个 L2(Base / Arbitrum),RPC 用 Alchemy
- **产出:** 一个能用的全栈 dApp + 线上可访问地址

### Week 7｜综合项目(简历扛把子)
- [ ] 做一个真 DeFi 小协议:质押金库 / 简化借贷
- [ ] 完整测试(unit + fuzz + invariant),`forge coverage` 出报告
- [ ] 写一份「已知风险与缓解」文档(你的杀手锏)
- [ ] 通关 **Damn Vulnerable DeFi**(16 关)
- **产出:** 主项目仓库,README 讲清"为什么 + 测试覆盖 + 风险分析"

### Week 8｜包装 + 远程求职
- [ ] 整理 3 个仓库的 README(① 全栈 dApp ② 带测试的协议 ③ 安全分析合集)
- [ ] 读 10 份真实审计报告,收藏 Immunefi
- [ ] 做一份**英文简历**(远程岗必须英文)
- [ ] 录一段 **英文自我介绍(2 分钟)**:讲你的测试背景 + 为什么转 web3 + 做过什么
- [ ] 开始投递(见下)

---

## 4. 英语并行计划(远程岗的真正门槛)

**每天 0.3h,不可跳过:**
- [ ] 读:英文技术文档/审计报告 / X 上的技术贴
- [ ] 写:每天 3 句英文技术笔记(发 X 或 GitHub commit message)
- [ ] 说:每周录一次 2 分钟英文技术自述(对着手机讲,回听纠错)
- [ ] 听:每周刷 1 个英文 web3 播客 / 会议演讲

**面试英语目标:** 能听懂技术问题 + 能用不完美但能沟通的英语回答。不是考雅思。

---

## 5. 远程岗求职清单

**目标岗位(按命中率):**
1. [ ] 智能合约测试 / QA 工程师 ← 你最容易进
2. [ ] 初级合约开发(主打"我测试很强")
3. [ ] Web3 全栈(合约 + 前端)
4. [ ] 初级安全审计(需再加 1~2 个月)

**渠道:**
- [ ] X(Twitter)关注 + 参与 web3 招聘贴(最实时)
- [ ] cryptojobslist.com / web3.career / remote3.co
- [ ] DAO 贡献(Discord)
- [ ] GitHub 给开源协议提 PR(测试 PR 门槛最低、最受认可)

**时区策略:** 你 UTC+8。优先投「async-first」团队、亚太/东南亚团队,或美国团队(他们的早晨 = 你的深夜,可部分 overlap)。

**反常识建议:** 别裸投开发岗。用测试背景**从 QA 岗切进去**,6 个月后内部转开发,成功率远高于硬刚初级开发岗。

---

## 6. 资源清单

| 用途 | 资源 |
|---|---|
| 综合课程(免费) | Cyfrin Updraft(Patrick Collins) |
| Solidity | Solidity by Example / 官方文档 |
| Foundry | Foundry Book(book.getfoundry.sh) |
| 安全练习 | Ethernaut / Damn Vulnerable DeFi / Capture the Ether |
| 审计报告 | Solodit / Immunefi |
| 全栈原型 | scaffold-eth-2 / Speed Run Ethereum |
| 前端 | viem / wagmi / RainbowKit 文档 |
| 测试网/部署 | Sepolia + Base/Arbitrum + Alchemy |

---

## 7. 进度追踪表

| 周 | 计划完成 | 实际完成 | 卡点 | 本周 GitHub commit 数 |
|---|---|---|---|---|
| 0 | | | | |
| 1 | | | | |
| 2 | | | | |
| 3 | | | | |
| 4 | | | | |
| 5 | | | | |
| 6 | | | | |
| 7 | | | | |
| 8 | | | | |

---

*计划是活的。每周复盘时,不合适的直接改,别硬扛。*
