# 做就是最好的想 —— 5 个月 build 了 3 个 AI 产品，砍了 1 个

> 作者：王善波 · 36 岁 · 台满满科技技术合伙人
>
> 月烧 $2,000 / 6 亿 tokens 在 Claude Opus 等顶级模型上
>
> 这是 [《月烧 2,000 AI 反常识 SOP》](https://github.com/wangshanbo/ai-native-sop) 系列的 **第 0 篇 manifesto**。读完它，再读后面 10 篇你会理解我所有方法论的源头。

---

## 一个反问

如果给你 5 个月时间，让你 build 3 个 AI 产品，你会怎么排时间？

我猜大多数人的答案是：

```
Month 1-2: 调研 / 写 PPT / 拉投资 / 想清楚做哪个
Month 3:   开始动第一个
Month 4-5: 继续 build 第一个
```

**我的实际答案是**：

```
Month 1-3: build NormCode v0 → v9（10 个完整版本）
Month 4:   build 完了我才知道 vscode fork 不是对的形态 → 砍
Month 4-5: 同时 build Sentinel Web v2 + Guard（Rust）
```

**5 个月，3 个完整产品出货，1 个被自己亲手砍掉。**

这篇文章讲的就是这个差异，以及它背后的一个方法论：

> **「做」就是最好的「想」。**

---

## 我 5 个月 build 了什么

### 产品 1：NormCode（vscode fork · 已 sunset）

基于 VS Code 深度定制的 AI IDE，目标是把 Anthropic 长程 Agent 范式做成可用的桌面工具。

5 个月里我 ship 了：


| 模块                                                                                                                                                                                                                                              | 状态     |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------ |
| **长程 Agent v0~v9**（10 个完整版本，每个独立 spec）                                                                                                                                                                                                          | ✅ 全部完成 |
| **13+ 核心服务**：BudgetGovernor / HumanGate / EpisodicMemory / FailureTaxonomy / RollingPlanner / IsolatedReviewer / ExecutionTrace / SideEffectLedger / CommandRiskGate / UncertaintyEstimator / DenseReward / FormalAssertionRegistry / Dashboard | ✅ 全部跑通 |
| **跨会话持久化**（trace / budget / sfx / failure / replan 全持久化）                                                                                                                                                                                        | ✅      |
| **HITL 防失控**（自动 pause + 跨会话恢复）                                                                                                                                                                                                                  | ✅      |
| **Token 预算回写 + 滚动 Replan**                                                                                                                                                                                                                      | ✅      |
| **EpisodicMemory + BM25-lite 检索**                                                                                                                                                                                                               | ✅      |
| **CommandRiskGate**（low / medium / high / destructive 命令分级）                                                                                                                                                                                     | ✅      |
| **LongHorizonDashboardPane**（5 个 tab 的可视化大盘）                                                                                                                                                                                                    | ✅      |


**这不是 demo，这是 5 个月每天写出来的工程系统。**

### 然后我把它砍了

砍的不是 NormCode 这个产品本身，是 vscode fork 这个**形态**。

砍的理由（一句话）：

> **vscode 的 ViewPane / Webview / contribution 心智，绑死了"代码-中心"的产品视角；而我真正想做的是「不会编程的人也能持续运营一个真实可演化的应用」—— 这两件事在桌面 IDE 形态下永远拧巴。**

这个结论，**我在 PPT 里推演 6 个月得不到。我在 build 了 6 个月之后立刻就懂了。**

### 产品 2：Sentinel-Web v2（重写，正在做）

Web App 形态。一句话定位：

> **让普通人通过自然对话，做出真实可上线、可演化、可运营的全栈应用的 AI 合伙人。**

直接对标 Bolt / Lovable / v0 / Replit Agent，但**核心差异化在 4 个字**："**不止帮你做出来，还陪你做下去。**"


| Bolt / Lovable / v0 | Sentinel                    |
| ------------------- | --------------------------- |
| 5 分钟做个 demo         | 5 分钟出第一版 + 5 个月持续演化         |
| 「做完就没下文」            | 上线后看数据 → 对话式优化 → A/B → 持续迭代 |
| Demo 工厂             | 真实产品工厂                      |


技术形态：Web App + Node 后端 + 云端代码沙箱 + Anthropic 级长程 Agent 编排（NormCode 的领域逻辑直迁过来，省 2~3 个月）。

5 年北极星：**100 万普通人通过 Sentinel 做出仍在运营的真实应用，其中 100 个月收入 > 10 万 RMB**。

### 产品 3：Guard（Rust · 策略约束层）

不是产品，是基础设施。一句话定位：

> **MCP 让 AI 有手脚，Skills 让 AI 有经验，Guard 让 AI 不做错事。**

把"调用顺序错 / 忘记 await / 必须存在的初始化调用缺失 / 数据流不合规（如 send 前没 validate）"这类约束转成可执行规则，**在 IDE / 流水线里自动拦截 + 返回可修复建议**。

Rust 写的（性能 + 稳定 + 可嵌入），MCP server 形态可一键安装到任何项目的 `.cursor/mcp.json`。

---

## 这才是 build 真正的力量

回过头看，**这 5 个月最值钱的不是 3 个产品**。

最值钱的是：

```
我 build 了 3 个月、砍掉 1 个 6 个月的方向、转向更对的形态、
然后用前一个的领域逻辑直迁省 2~3 个月。

这整个 build / kill / pivot / reuse 的循环
=
任何「想 6 个月」的人，
3 年也想不出来。
```

---

## 为什么 AI 时代「做」被放大了 10 倍

来算笔账：


| 时代              | 1 个完整产品的"做"成本                                         | 1 个"想错"的代价   |
| --------------- | ----------------------------------------------------- | ------------ |
| 传统开发（2010~2020） | 6 个月 × 5 人 = 30 人月（约 150 万 RMB）                       | 巨大，所以必须想清楚再做 |
| AI 时代（2022~）    | **5 个月 × 1 人 + AI = 约 1.5 人月**（含 2K/月 AI 投入约 7 万 RMB） | 小到可以接受"做了再砍" |


**成本砍到 1/20 = 决策模式必须从「想清楚再做」彻底翻转成「做了再砍再做」。**

但绝大多数 founder / 工程师还在用旧操作系统：

- 写 1 个月 PPT
- 找投资人讨论 3 个月
- 招 6 个人开始 build
- 6 个月后发现做错了 → 不敢砍（沉没成本太大）→ 硬撑 12 个月 → 死

而你能做的：

- 1 周写第一版 demo
- 4 周 ship 第一版能给真实用户用
- 8 周发现方向错 → 砍掉，没人受伤
- 12 周 ship 第二个方向

**同样 12 周，前者还在 PPT 里，你已经验证 / 砍 / 重来过 1 次。**

---

## 这正是 Anthropic / Cursor 的工作哲学

Anthropic engineering blog 反复出现的一句话：

> *"Until you've built it, you don't actually know if the idea is good."*
>
> — Anthropic Engineering

中文翻译就是 **"做就是最好的想"**。

更狠的是 Anthropic 自己的 build 路径：

```
Claude (LLM 基模)
  → Claude Code (CLI)
    → Skills (file convention)
      → MCP (protocol)
        → Computer Use (multimodal agent)

每一步都是「build → ship → 看反馈 → 砍掉一部分 → 再 build」
没有任何战略 PPT 在指挥。
```

国内 99% 的创业者还在讲「先做产品定位」「先想清楚再做」。
**而真正在前沿的团队，全部是 build first。**

我跟 Anthropic 团队从未说过一句话，但我们说的是**同一种语言**。
你也可以。

---

## 反常识结论：你的方法论不需要"沉淀"

很多工程师跟我说："我也想分享方法论，但我感觉自己没沉淀。"

**这是误解**。

你的方法论不在你"想出来的理论"里。
它在你**「build 过、踩过、砍过」的历史**里。


| 别人写的 AI 文章          | 你能写的 AI 文章                                |
| ------------------- | ----------------------------------------- |
| 《如何写好 prompt》（理论）   | 《我做了一个长程 Agent IDE，10 个版本之后我把它砍了》         |
| 《AI agent 设计模式》（理论） | 《BudgetGovernor 我设计了 3 次，前 2 次错在哪里》       |
| 《AI 创业方向选择》（理论）     | 《为什么我从 vscode fork 转向 Web App，6 个月血泪复盘》   |
| 《Rust 在 AI 时代》（理论）  | 《我用 Rust 写了一个策略层 Guard，因为 MCP/Skills 都不够》 |


**理论文章满世界都是。"我 build 了 X 学到 Y" 是真正稀缺的内容。**

---

## 给读者的 3 条铁律

如果你 take 走一个东西，take 这个：

### 铁律 1：把「想 6 个月」换成「做 4 个月」

如果一个想法你已经想了 1 周，**立刻 build 一个最小可跑的版本**。AI 时代这个版本 1~3 天能出。

### 铁律 2：接受「砍掉 6 个月作品」是健康的

砍掉错的方向，**不是失败，是节省了未来 6 个月的更大失败**。
比起"硬撑做完一个错的方向"，砍掉的勇气稀缺 10 倍。

### 铁律 3：用 AI 把「做」的成本降到接近 0

每个月 2,000 在顶级 AI 上听起来很贵 —— 它实际上是把你的 build 成本砍了 95%。
**这是 AI 时代最划算的杠杆。**

---

## 我接下来在做什么

- ✅ **Sentinel-Web v2** ship 到第一批 100 个普通用户
- ✅ **Guard** 开源 + 推到 Cursor / Claude Code 用户社区
- ✅ 这个连载 10 篇博客，把 5 个月 build 出来的方法论全开源
- 🚧 **AI × 硬件** —— 我在国内拥有灯控 / 存杆柜 / 点单机 / 电视机 / 一体机等完整供应链直接老板关系，正在 build 几个 AI 硬件原型
- 🤝 接 fractional CTO 顾问、AI 工作流咨询、AI × 硬件创业合伙

如果上面任何一条触动你，[GitHub @wangshanbo](https://github.com/wangshanbo) 找我。

---

## 关于这个连载

这是 [《月烧 2,000 AI 反常识 SOP》](https://github.com/wangshanbo/ai-native-sop) 系列的 **第 0 篇 manifesto**。

接下来 10 篇会拆解：

1. 你的 prompt 不是 prompt，是 SOP（已发布）
2. 月烧 2,000 的工具组合论
3. 上下文工程 / 4 层金字塔
4. God Class 4700 行用 AI 怎么动
5. 月烧 2,000 的 ROI 计算
6. 长程 Agent vs 短链 Chat（这一篇我会拆 NormCode v0~v9 的设计血泪）
7. AI 时代的"代码 review"：Verifier 工具环
8. 跨端 + AI = 1 人 5 倍战力
9. B2B SaaS + AI 真正的差异化
10. 用 AI 写 Eval 不写测试

---

## Star 一下

如果这篇 manifesto 让你点头超过 3 次，请去 [github.com/wangshanbo/ai-native-sop](https://github.com/wangshanbo/ai-native-sop) 给个 Star。

这是我把"私人方法论"变成"公共方法论"最大的动力 —— 也是你下次面试招人 / 找合伙人 / 谈合作时，多一个**"看这个仓库就懂我"**的链接。

---

本文遵循 [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/) 协议，转载请注明作者王善波 + 原文链接。