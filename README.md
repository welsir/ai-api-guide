# AI API Guide · 模型选型与接入 / Model Selection & Integration

**从 Claude、GPT、Gemini、DeepSeek、Kimi、Qwen，到 Claude Code、Codex、Cline 和 AI 工作流：先弄清怎么选，再开始调用。**

A practical guide to **AI API providers, LLM model selection, API pricing and cost comparison, OpenAI-compatible endpoints, coding tool integration, and troubleshooting**. Connect models to Claude Code, Codex, Cline, chat clients and AI workflows. Maintained by Orbis; [read the full English guide](README.en.md).

[模型与线路](https://orbiorbi.com/pricing?utm_source=github&utm_medium=readme&utm_campaign=ai-api-guide&utm_content=header-models) · [接入文档](https://orbiorbi.com/tutorials?utm_source=github&utm_medium=readme&utm_campaign=ai-api-guide&utm_content=header-docs) · [Orbis](https://orbiorbi.com/?utm_source=github&utm_medium=readme&utm_campaign=ai-api-guide&utm_content=header-home) · [English](README.en.md)

这里整理 AI API、LLM API 与 API 中转服务的选型方法、模型家族、客户端配置要点、调用成本和常见错误。由 **Orbis** 维护；Orbis 是提供多模型、多线路接入的商业 API 平台。文中的选型方法也适用于其他服务，不是第三方独立排名。

---

<a id="why-orbis"></a>
## Orbis：低价多模型 API / Affordable Multi-Model API

**DeepSeek V4.1 Flash 专供线路：普通输入 ¥0.05 / 百万 tokens，输出 ¥0.20 / 百万 tokens。** 从低成本对话、批量处理到 AI 编程，在 Orbis 按预算选择模型和线路。

### 热门模型价格 / Featured API Pricing

单位：**¥ / 100 万 tokens（¥ / 1M tokens）**。以下为 2026-10-19 公开报价，每行对应指定线路。

| 模型 / Model | 线路 / Route | 普通输入 / Input | 输出 / Output | 缓存读取 / Cache read |
|---|---|---:|---:|---:|
| [DeepSeek V4.1 Flash](https://orbiorbi.com/pricing/deepseek-v4.1-flash?catalogKey=model%2F129&offering=orbis-exclusive-deepseek-v4-1-flash&group=%E9%80%9A%E7%94%A8+%C2%B7+Orbis%E4%B8%93%E4%BE%9B%E7%BA%BF%E8%B7%AF&utm_source=github&utm_medium=readme&utm_campaign=ai-api-guide&utm_content=value-pricing) | 通用 · Orbis专供线路 | ¥0.05 | ¥0.2 | ¥0.01 |
| [Kimi K3](https://orbiorbi.com/pricing/kimi-k3?catalogKey=model%2F139&offering=orbis-exclusive-kimi-k3&group=%E9%80%9A%E7%94%A8+%C2%B7+Orbis%E4%B8%93%E4%BE%9B%E7%BA%BF%E8%B7%AF&utm_source=github&utm_medium=readme&utm_campaign=ai-api-guide&utm_content=value-pricing) | 通用 · Orbis专供线路 | ¥0.1 | ¥0.5 | ¥0.4 |
| [GPT-6.1 Sol](https://orbiorbi.com/pricing/gpt-6.1-sol?catalogKey=model%2F91&offering=channel-86%2Fdedfefd51120&group=GPT+%C2%B7+HA%E7%BA%BF%E8%B7%AF&utm_source=github&utm_medium=readme&utm_campaign=ai-api-guide&utm_content=value-pricing) | GPT · HA线路 | ¥0.225 | ¥1.125 | ¥0.01125 |
| [GLM 5.3](https://orbiorbi.com/pricing/glm-5.3?catalogKey=model%2F132&offering=orbis-exclusive-glm-5-3&group=%E9%80%9A%E7%94%A8+%C2%B7+Orbis%E4%B8%93%E4%BE%9B%E7%BA%BF%E8%B7%AF&utm_source=github&utm_medium=readme&utm_campaign=ai-api-guide&utm_content=value-pricing) | 通用 · Orbis专供线路 | ¥0.5 | ¥2 | ¥0.25 |

**费用有多低？** 以上述 DeepSeek 线路为例，100 万普通输入 tokens + 100 万输出 tokens，按表中单价计算共 **¥0.25**；相同用量的 Kimi K3 为 **¥0.60**。这是文本用量算例，不含缓存写入、其他模态或额外计费项。

### 为什么选 Orbis / Why Orbis

- **低成本起步 / Low-cost entry**：专供线路提供低价模型选择，先用小预算跑通自己的任务。
- **按量付费，无月费 / Pay as you go**：按实际用量计费，余额不过期，无需为固定月套餐买单。
- **多模型、多线路 / Models and routes in one place**：同一平台选择 Claude、GPT、Gemini、DeepSeek、Kimi 等模型；线路价格公开，自己决定使用哪一条。
- **兼容常用 API / Familiar API formats**：提供 OpenAI 兼容及 Anthropic 协议线路，便于接入已有应用；具体端点与能力以所选线路为准。
- **¥ 计价，查看用量 / ¥ pricing and usage tracking**：按标价估算预算，在控制台查看调用用量与费用。

**[查看全部模型与线路价格 →](https://orbiorbi.com/pricing?utm_source=github&utm_medium=readme&utm_campaign=ai-api-guide&utm_content=value-all-models)** · **[进入 Orbis，开始接入 →](https://orbiorbi.com/?utm_source=github&utm_medium=readme&utm_campaign=ai-api-guide&utm_content=value-start)**

价格以对应线路页面的最新报价为准；缓存读取、缓存写入分别计费，Kimi K3 此线路的缓存读取单价高于普通输入单价。上表为公开报价核对，不代表逐线路实测结论。

## 快速选择 / Quick Start

| 你的问题 | 从这里开始 | 要拿到的结果 |
|---|---|---|
| 想给 Claude Code、Codex 或 Cline 接模型 | [工具接入](#tool-setup) | 工具需要的协议、地址格式和验证步骤 |
| 想比较 Claude、GPT、DeepSeek、Kimi 等 API | [模型选型](#model-guide) | 按实际任务挑候选模型，再比较线路 |
| 想找便宜的 AI API，又怕成本算错 | [价格与成本](#cost-guide) | 输入、输出、缓存和失败重试的完整成本 |
| 已有 OpenAI SDK 项目，想换服务 | [协议与迁移](#protocol-guide) | 不把“兼容”误解为所有端点都支持 |
| 遇到 401、404、429 或流式中断 | [排错表](#troubleshooting) | 一个可定位的最小问题 |
| 在做 RAG、Agent、n8n 或 Dify 工作流 | [应用场景](#use-cases) | 先核对真正需要的模型能力 |
| 想直接使用 Orbis | [Orbis 接入](#orbis-setup) | 选模型、选线路、创建对应 Key |

### 目录 / Contents

- [Orbis 价格与特点 / Orbis Pricing](#why-orbis)
- [AI 项目导航 / AI Resource Directory](#resource-directory)
- [托管与自部署 / Hosted vs Self-hosted](#deployment-options)
- [调用示例 / Python, JavaScript & cURL](#request-examples)
- [低成本预算 / Budget Playbook](#budget-playbook)
- [应用工作流 / Workflow Recipes](#workflow-recipes)
- [Agent 与 MCP / Agents & MCP](#agent-mcp)
- [更多问题 / More FAQ](#extended-faq)
- [术语表 / Glossary](#glossary)
- [API 服务选型 / Choosing an API Provider](#choose-provider)
- [模型选型 / Claude, GPT, Gemini, DeepSeek, Kimi & Qwen](#model-guide)
- [工具接入 / Claude Code, Codex & Cline Integration](#tool-setup)
- [协议与迁移 / OpenAI-compatible APIs & Migration](#protocol-guide)
- [价格与成本 / API Pricing, Caching & Token Costs](#cost-guide)
- [应用场景 / RAG, Agents & Multimodal Workflows](#use-cases)
- [常见错误 / Troubleshooting & FAQ](#troubleshooting)
- [通过 Orbis 接入 / Connect through Orbis](#orbis-setup)
- [验证与更新 / Verification & Updates](#maintenance)

<a id="choose-provider"></a>
## API 服务选型 / Choosing an AI API Provider

别只比较模型数量或最低单价。先挑一个真实任务，例如修改一段项目代码、总结一份文档或调用一次外部工具，再按同样的输入比较候选方案。

| 维度 | 应该核对什么 | 可以留下的证据 |
|---|---|---|
| 模型与线路 | 模型 ID、服务提供方式、可选择的线路 | 当前接入卡与模型列表 |
| 协议 | Chat Completions、Responses、Messages 中需要哪一种 | 实际请求路径与脱敏结果 |
| 功能 | 流式、工具调用、结构化输出、图片输入 | 对应功能的请求与响应，不能只测试普通聊天 |
| 成本 | 输入、输出、缓存、计费单位、币种、重试 | usage 与对应账单；标明测试时间 |
| 可靠性 | 失败率、首字延迟、完成时间、并发限制 | 多次、有时间范围的测试，而非一次成功 |
| 数据处理 | 日志保留、上游处理规则、删除方式 | 服务说明；不清楚时不提交敏感数据 |
| 支持与迁移 | 故障反馈、状态页、替换服务的成本 | 迁移清单、问题回复与变更说明 |

**官方 API、聚合 API、API 中转、自部署网关不是同一种产品。** 官方 API 通常直接对接一家提供方；聚合或中转服务集中接入和计费；自部署网关则需要自行承担部署、运维及上游接入。选择取决于你的任务与维护能力。

<a id="model-guide"></a>
## 模型选型 / LLM Model Selection

同一家族的不同版本、不同线路也可能有不同的上下文、输出上限和功能。下表是选择时的问题清单，不是能力排名，也不代表 Orbis 当前提供表中每一种功能。

| 模型家族 | 接入时优先确认 | 建议用自己的什么任务比较 |
|---|---|---|
| **Claude API** | 客户端需要 Anthropic Messages 还是兼容接口；工具调用和流式事件是否完整 | 项目代码修改、长文档理解、多轮工具任务 |
| **GPT / OpenAI API** | 需要 Chat Completions 还是 Responses；哪些参数和工具可用 | 结构化提取、代码编辑、工具调用 |
| **Gemini API** | 原生接口与兼容接口的功能差异；图片、音频等输入格式 | 自己的多模态样本、长资料问答 |
| **DeepSeek API** | 模型 ID、推理输出处理、缓存计费、工具兼容性 | 中文任务、代码任务、批量文本处理 |
| **Kimi API** | 长上下文约束、输出上限、Agent 所需的工具调用 | 长材料提取、跨文档问答、多步任务 |
| **Qwen API** | 具体模型是文本、视觉还是其他模态；部署与服务协议 | 中文提取、视觉输入、应用内对话 |
| **GLM API** | 模型版本、流式与工具格式、客户端接入要求 | 编程工具、工作流和中文任务 |

**三步缩小选择范围：** 先按功能筛选 → 用同一组真实样本比较 → 结合成本与失败情况决定。短题答对、模型自报名称或一次接口成功都不能证明模型身份。

[查看 Orbis 当前模型与线路](https://orbiorbi.com/pricing?utm_source=github&utm_medium=readme&utm_campaign=ai-api-guide&utm_content=model-guide)。具体版本、可用状态和报价以选择的线路页面为准。

<a id="tool-setup"></a>
## 工具接入 / Claude Code, Codex, Cline & Chat Client Integration

先准备三个值：**服务地址（Base URL）、该线路的 API Key、精确的模型 ID**。再核对工具所需协议。下面列的是配置检查重点，不是逐工具实测兼容承诺。

| 工具 / 客户端 | 配置前检查 | 首次连接后要验证 |
|---|---|---|
| **Claude Code** | 当前版本支持的认证和 provider 方式；服务端协议是否匹配 | 多轮对话、工具事件、流式结束和错误返回 |
| **Codex / Codex CLI** | provider 配置、认证来源、wire API 与服务端接口 | 简单请求，再到文件读取或代码修改任务 |
| **Cline / Roo Code / Kilo Code** | 当前版本的 provider 选项；模型能力配置与实际能力是否一致 | 工具调用参数、流式、上下文与输出上限 |
| **Cursor** | 自定义 API Key / Base URL 对哪些功能生效、账户条件和当前版本限制 | 目标功能本身；聊天能用不等于所有 Agent 功能能用 |
| **Cherry Studio** | provider 类型、Base URL 是否自动拼接路径、模型 ID | 普通对话，再分别检查图片或工具功能 |
| **Open WebUI / LobeHub** | 连接配置、后端网络可达性、模型发现与手动模型配置 | 模型列表和实际消息请求分别验证 |
| **Dify** | 模型 provider、聊天模型与 embedding 模型是否分别配置 | 文本生成；若做知识库，再测试索引和检索 |
| **n8n** | 节点与凭据类型、节点版本、可配置的服务地址 | 单节点调用成功后，再验证完整工作流 |
| **LangChain / AI SDK** | 所选适配器使用哪种协议、是否支持当前功能 | 普通文本、streaming、tool calling 分开测试 |

### 通用配置顺序

1. 从服务的接入页复制地址和模型 ID，不从第三方截图猜写。
2. 按工具版本选择正确的 provider / 协议选项。
3. 填入环境变量或工具提供的凭据设置；不要把真实 Key 写进公开配置。
4. 用一条短消息确认基本请求，再检查应用真正需要的功能。
5. 记录工具版本、模型、线路、日期和结果，便于升级后复查。

`/v1` 是否应写进 Base URL，取决于客户端会不会自动拼接；不要机械地添加或删除。若最终请求出现重复路径，先修正地址拼接。

<a id="protocol-guide"></a>
## 协议与迁移 / OpenAI-compatible APIs, Anthropic & API Migration

**OpenAI-compatible 描述兼容范围，并不自动保证支持所有 OpenAI 接口。** 迁移时把以下接口和能力分别检查：

| 接口 / 能力 | 为什么需要单独检查 |
|---|---|
| Chat Completions | 消息格式、流式 chunk、工具调用和 usage 字段各有要求 |
| Responses | 不能仅凭 Chat Completions 成功推断可用；客户端可能依赖特定事件 |
| Anthropic Messages | 认证头、请求结构与事件格式不同于 Chat Completions |
| Structured output | 普通 JSON 文本不等于严格符合指定 schema |
| Tool / function calling | 应检查参数、调用 ID、结果回传及后续轮次 |
| Embeddings | 向量维度与模型变化可能要求重建已有索引 |
| Images / audio / video | 可能采用独立端点、异步任务或不同计费单位 |

### 更换 API 服务的最小检查清单

- [ ] 地址、认证和模型 ID 已替换，生产 Key 没有进入版本库。
- [ ] 应用所需端点在新线路上存在。
- [ ] 普通响应、流式、工具调用分别验证。
- [ ] 错误码、超时和重试逻辑不会产生无限重试或意外费用。
- [ ] usage 字段与账单单位对得上。
- [ ] 用真实小样本比较质量，保留可恢复的原配置。

<a id="cost-guide"></a>
## API 价格与成本 / API Pricing & Token Cost Comparison

比较便宜的 LLM API，先统一 **币种、单位、模型、线路和功能**。每百万 tokens、每张图片、每秒视频、每次请求不能直接横向比较。充值到账的额度单位也不一定等于实际货币。

### 文本调用成本

不考虑缓存、阶梯价格和其他费用时：

```text
单次成本 = 输入 tokens ÷ 1,000,000 × 输入单价
         + 输出 tokens ÷ 1,000,000 × 输出单价
批量成本 = 各次实际调用成本之和
```

以下全部是假设价格，只演示算法，**不是 Orbis 或任何厂商报价**：输入 ¥1 / 百万 tokens，输出 ¥4 / 百万 tokens。

| 假设场景 | 输入 | 输出 | 单次估算 | 1,000 次相同调用 |
|---|---:|---:|---:|---:|
| 短文本提取 | 2,000 tokens | 500 tokens | ¥0.004 | ¥4 |
| 文档总结 | 20,000 tokens | 2,000 tokens | ¥0.028 | ¥28 |
| 一次较长代码请求 | 40,000 tokens | 5,000 tokens | ¥0.060 | ¥60 |

Agent 一项任务通常可能包含多次请求。应统计整项任务的输入、输出、工具循环和重试；不能用一次请求价格代表任务总价。

### 缓存与重试容易漏算什么？

- 缓存命中、未命中、写入是否采用不同单价？usage 中是否能区分？
- 历史上下文是否在后续轮次再次计入输入？
- 请求失败、中途取消或重试如何计费？需要以服务规则和账单核对。
- 长上下文是否触发不同价格档位？
- 图片、音频、视频是否还有额外计费项？

[比较 Orbis 各条线路的当前价格](https://orbiorbi.com/pricing?utm_source=github&utm_medium=readme&utm_campaign=ai-api-guide&utm_content=cost-guide)。先做小量任务，核对用量和账单，再扩大批量规模。

<a id="use-cases"></a>
## 应用场景 / RAG, AI Agents, Translation & Multimodal Workflows

| 场景 | 优先确认的能力 | 验证一个什么样的结果 |
|---|---|---|
| **RAG / 文档问答** | 文本生成、embedding 或已有检索服务；可选 rerank | 回答能引用样本文档，检索失败时不会编造来源 |
| **AI Agent / 自动化** | 工具调用、状态管理、错误处理、成本边界 | 能完成一个受控的多步骤任务，并停止于预算或失败边界 |
| **AI 翻译 / 批处理** | 结构化输出、长度控制、术语一致性 | 多条样本无漏译，输入输出逐项对应 |
| **代码审查 / AI 编程** | 代码理解、上下文、工具调用 | 修改经过项目检查，而不是只生成看起来正确的代码 |
| **图像理解 / OCR** | 具体线路支持图像输入，格式和尺寸要求清楚 | 从自己的图片提取正确字段 |
| **图像、视频、语音生成** | 独立端点、产物格式、异步状态、计费单位 | 产物能获取和使用，任务失败能明确识别 |

这里是需求检查表。模型广场中的能力标签，不替代具体线路的实际功能测试。

<a id="troubleshooting"></a>
## 常见错误 / API Troubleshooting & FAQ

| 现象 | 先检查 | 下一步 |
|---|---|---|
| **401 / Unauthorized** | Key 是否完整、属于当前服务，认证方式是否正确 | 重新核对凭据来源，不在 Issue 粘贴真实 Key |
| **403 / Forbidden** | 模型、线路或账户是否有访问权限 | 查看返回错误信息；更换 Key 不能替代权限核实 |
| **404 / Model not found** | 请求路径、精确模型 ID、所选线路提供的模型 | 区分“端点不存在”和“模型不存在” |
| **429 / Rate limit** | 请求频率、并发、额度和响应说明 | 按服务提示退避，设置最大重试次数 |
| **400 / 参数不支持** | 当前端点接受的字段、参数值和消息格式 | 简化为最小请求，再逐项加入参数 |
| **流式中断 / SSE 不完整** | 客户端事件解析、网络超时、网关缓冲及上游错误 | 保存脱敏错误与请求 ID；普通响应成功不能排除流式问题 |
| **工具调用失败** | tools schema、调用 ID、工具结果格式、后续消息 | 单独测试一次工具调用与结果回传 |
| **费用高于估计** | 输出量、多轮上下文、缓存和重试 | 对照每次 usage 与账单，而不只看提示词字数 |

### ChatGPT 或 Claude 的订阅能直接当 API 额度吗？

不要假定聊天产品订阅与开发者 API 共享额度。确认实际购买的产品、授权方式与账单来源；在 Orbis 中使用的是对应线路的 API Key。

### 能只改 Base URL 就完成迁移吗？

只有在协议、端点、模型名称、认证和应用所需能力都匹配时，改动才可能很少。先验证最小请求，再验证完整任务。

### 如何判断模型是否被替换或能力受限？

用固定样本、相同参数与可信基线做多次对比，可以发现异常，但不能单凭模型自报、一道题或风格证明身份。记录可观察差异，并向服务方核实。

### API 中转站与 OpenRouter 类多模型服务怎么比较？

先比较你实际要用的模型、协议、计费、数据处理和可靠性证据，再看接入便利度。本站由 Orbis 维护，不提供没有证据的“第一名”或竞品质量结论。

### 有没有免费 API 或试用额度？

区分长期免费额度、限时活动和一次性赠额，并核对限制。本文不承诺 Orbis 存在免费额度；当前政策以网站展示为准。

<a id="orbis-setup"></a>
## 通过 Orbis 接入 / Connect Models, Routes & API Keys

[Orbis](https://orbiorbi.com/?utm_source=github&utm_medium=readme&utm_campaign=ai-api-guide&utm_content=orbis-setup) 把模型及可选择的分组线路集中展示。根据已查看的产品页面，同一模型可有不同线路，价格与协议按线路区分，API Key 绑定所选分组。

1. **选模型**：在[模型广场](https://orbiorbi.com/pricing?utm_source=github&utm_medium=readme&utm_campaign=ai-api-guide&utm_content=select-route)找到目标模型。
2. **选线路**：比较价格、协议和参数说明，打开该线路的接入页。
3. **创建 Key**：选择与线路一致的分组；Key 只放在你自己的凭据设置中。
4. **复制配置**：使用接入页给出的 Base URL 和模型 ID。
5. **小量验证**：先完成短请求，再验证流式、工具调用等所需能力，核对账单。

网站展示、线路声明和实际测试是三类不同证据。标记为“配置声明 · 执行未知”的参数，不能当作已验证功能。

**下一步：**[查看模型与线路](https://orbiorbi.com/pricing?utm_source=github&utm_medium=readme&utm_campaign=ai-api-guide&utm_content=footer-models) · [阅读接入文档](https://orbiorbi.com/tutorials?utm_source=github&utm_medium=readme&utm_campaign=ai-api-guide&utm_content=footer-docs) · [进入 API Key 页面](https://orbiorbi.com/keys?utm_source=github&utm_medium=readme&utm_campaign=ai-api-guide&utm_content=footer-keys)

<a id="resource-directory"></a>
## AI 开源项目与工具导航 / AI Resource Directory

按你正在做的事情找工具。以下链接指向项目自身的 GitHub 仓库，简介与归档状态核对日期为 **2026-10-19**。收录不代表已完成 Orbis 兼容测试；部署或商用前查看该项目当前许可证和版本要求。

### AI 网关与 API 管理 / AI Gateways

| 项目 | 用途 | 什么时候看它 |
|---|---|---|
| [LiteLLM](https://github.com/BerriAI/litellm) | 统一模型接入与调用管理 | 已有多个上游 Key，希望统一接入 |
| [New API](https://github.com/QuantumNous/new-api) | 模型聚合与分发管理 | 需要模型、渠道与用户接入管理 |
| [One API](https://github.com/songquanpeng/one-api) | API 适配与 Key 分发 | 维护现有 One API 接入体系 |
| [Bifrost](https://github.com/maximhq/bifrost) | 模型及 Agent 网关 | 评估路由、预算与故障切换 |
| [Higress](https://github.com/higress-group/higress) | AI 原生 API 网关 | 已有网关基础设施，准备接入 AI 流量 |
| [Portkey Gateway](https://github.com/Portkey-AI/gateway) | 多模型请求路由 | 需要集中处理上游请求策略 |
| [agentgateway](https://github.com/agentgateway/agentgateway) | Agent 与 MCP 代理 | 需要管理 Agent 与 MCP 服务之间的访问 |

### AI 编程与对话客户端 / Coding & Chat

| 项目 | 用途 | 什么时候看它 |
|---|---|---|
| [Cline](https://github.com/cline/cline) | 编程 Agent | 在开发流程中调用模型与工具 |
| [Kilo Code](https://github.com/Kilo-Org/kilocode) | Agent 编程平台 | 评估模型驱动的工程工作流 |
| [Aider](https://github.com/Aider-AI/aider) | 终端结对编程 | 从终端与模型协作修改代码 |
| [Cherry Studio](https://github.com/CherryHQ/cherry-studio) | 多模型桌面工作台 | 集中使用不同模型与助手 |
| [Open WebUI](https://github.com/open-webui/open-webui) | 模型对话界面 | 为模型服务提供网页对话入口 |
| [LobeHub](https://github.com/lobehub/lobehub) | Agent 工作空间 | 组织多个助手和任务 |

### 工作流与应用开发 / Workflows & SDKs

| 项目 | 用途 | 什么时候看它 |
|---|---|---|
| [Dify](https://github.com/langgenius/dify) | Agent 工作流与 RAG 应用 | 搭建带知识库的业务应用 |
| [n8n](https://github.com/n8n-io/n8n) | 可视化自动化工作流 | 将 AI 步骤连接到业务系统 |
| [LangChain](https://github.com/langchain-ai/langchain) | Agent 应用开发 | 用代码组织模型、工具和任务 |
| [LlamaIndex](https://github.com/run-llama/llama_index) | 文档处理与检索应用 | 将自己的资料接入 AI 应用 |
| [AI SDK](https://github.com/vercel/ai) | TypeScript AI 应用工具包 | 在 Web 应用中集成模型交互 |

### 评估、观测与本地推理 / Evaluation & Inference

| 项目 | 用途 | 什么时候看它 |
|---|---|---|
| [Langfuse](https://github.com/langfuse/langfuse) | 调用链观测与评估 | 定位 Agent 多步骤调用的成本和失败 |
| [Promptfoo](https://github.com/promptfoo/promptfoo) | 提示词与应用评估 | 比较多个模型在相同样本上的结果 |
| [Ollama](https://github.com/ollama/ollama) | 模型运行工具 | 尝试在自己的设备上运行模型 |
| [vLLM](https://github.com/vllm-project/vllm) | 模型推理与服务引擎 | 有算力和运维能力，需要部署模型服务 |

### 旧教程中的项目 / Projects in Older Tutorials

[Roo Code](https://github.com/RooCodeInc/Roo-Code) 与 [Flowise](https://github.com/FlowiseAI/Flowise) 的上述仓库在核对时标记为 **Archived**。阅读旧教程仍有参考价值；新项目选型时先确认是否有后续维护仓库，以及当前版本的支持范围。

**网关、客户端和模型服务怎么配合？** 客户端负责交互，工作流负责安排步骤，网关负责转发和管理请求，模型服务负责推理。搭建一个网关并不会附送上游模型额度。若只是希望给现有客户端接入模型，可以先从 [Orbis 的模型与线路](https://orbiorbi.com/pricing?utm_source=github&utm_medium=readme&utm_campaign=ai-api-guide&utm_content=resource-directory) 选择服务，再按客户端需要的协议配置。

<a id="deployment-options"></a>
## 聚合 API、自部署网关与本地模型 / Hosted vs Self-hosted

| 方案 | 你需要准备 | 主要成本 | 适合什么情况 |
|---|---|---|---|
| 直接接模型厂商 API | 对应厂商账户、Key、客户端 | 各家的调用费用与集成维护 | 明确只需要一家模型服务 |
| 使用多模型服务，如 Orbis | 平台账户、所选线路 Key | 所选模型和线路的实际用量 | 希望比较模型并快速接入，不自行维护网关 |
| 自部署 LiteLLM 等网关 | 服务器、网关配置、上游 Key | 上游调用费、服务器与维护 | 已有多个上游，需要统一入口 |
| 自部署 New API / One API | 部署环境、数据库、渠道配置 | 上游调用费、存储、维护 | 需要自己管理模型分发体系 |
| 本地运行模型 | 合适的硬件、模型文件、运行工具 | 硬件、电力、部署时间 | 希望在自己的设备上完成推理 |
| 自建推理服务 | 算力、模型、服务引擎、监控 | 算力利用率与运维投入 | 有持续用量和模型服务维护能力 |

### OpenRouter alternative / 多模型 API 替代方案怎么选？

“替代”要落到具体功能上：你需要的是统一余额、更多模型、特定协议、某个便宜的线路，还是自己的 Key 管理？先写下现在应用实际使用的端点和功能，再选服务。品牌相似、模型同名，并不保证迁移时请求完全相同。

如果重点是低成本接入，可以先看 [Orbis 价格表](#why-orbis)，对同一任务比较“完成成本”。如果重点是管理你已经购买的多家 Key，则先看 [网关项目](#resource-directory)。二者解决的问题不同，也可以组合使用。

### 自部署网关是否更便宜？

把成本拆开：`上游推理费用 + 服务器 + 存储与日志 + 维护时间`。网关可以帮助统一管理，但不会自动降低上游单价。个人低频使用可以先比较托管服务的实际账单；已有团队用量、需要统一权限或路由策略时，再评估自部署带来的管理收益。

<a id="request-examples"></a>
## 最小调用示例 / Python, JavaScript & cURL

这些是 **Chat Completions 通用请求模板**，不是每条 Orbis 线路的实测接入配置。先从所选线路复制支持该协议的 Base URL、Key 和模型 ID。`AI_BASE_URL` 应包含该线路要求的 API 前缀；下面只追加 `/chat/completions`。

在本地环境中设置 `AI_BASE_URL`、`AI_API_KEY`、`AI_MODEL`。不要把 Key 放进网页前端、GitHub 仓库或截图。以下代码不自动重试，错误会明确报出。

### Python：标准库调用 / Python Standard Library

不需要安装 SDK。保存为 `request.py`，配置环境变量后运行 `python3 request.py`。

```python
import json
import os
import urllib.request

endpoint = os.environ["AI_BASE_URL"].rstrip("/") + "/chat/completions"
payload = {
    "model": os.environ["AI_MODEL"],
    "messages": [{"role": "user", "content": "Reply with one short greeting."}],
    "stream": False,
}
request = urllib.request.Request(
    endpoint,
    data=json.dumps(payload).encode("utf-8"),
    headers={
        "Authorization": "Bearer " + os.environ["AI_API_KEY"],
        "Content-Type": "application/json",
    },
    method="POST",
)
with urllib.request.urlopen(request, timeout=60) as response:
    result = json.load(response)
print(json.dumps(result, ensure_ascii=False, indent=2))
```

成功后先查看 `choices` 中的返回内容及 `usage`。如果返回 404，检查拼接后的路径和模型 ID；不要直接在地址末尾继续加一层 `/v1`。

### JavaScript：服务端 fetch / Server-side JavaScript

使用提供内置 `fetch` 的 Node.js 运行环境，保存为 `request.mjs`，运行 `node request.mjs`。这段代码应运行在服务端或本机终端。

```javascript
const { AI_BASE_URL, AI_API_KEY, AI_MODEL } = process.env;
if (!AI_BASE_URL || !AI_API_KEY || !AI_MODEL) {
  throw new Error("Set AI_BASE_URL, AI_API_KEY and AI_MODEL first");
}
const response = await fetch(
  `${AI_BASE_URL.replace(/\/+$/, "")}/chat/completions`,
  {
    method: "POST",
    headers: {
      Authorization: `Bearer ${AI_API_KEY}`,
      "Content-Type": "application/json",
    },
    body: JSON.stringify({
      model: AI_MODEL,
      messages: [{ role: "user", content: "Reply with one short greeting." }],
      stream: false,
    }),
    signal: AbortSignal.timeout(60_000),
  },
);
if (!response.ok) throw new Error(`HTTP ${response.status}`);
console.log(JSON.stringify(await response.json(), null, 2));
```

### cURL：检查原始 HTTP 响应 / Raw HTTP

需要 `curl` 和 `jq`。用 `jq` 构造 JSON，避免模型 ID 中的字符破坏请求体。

```bash
: "${AI_BASE_URL:?Set AI_BASE_URL first}"
: "${AI_API_KEY:?Set AI_API_KEY first}"
: "${AI_MODEL:?Set AI_MODEL first}"
jq -n --arg model "$AI_MODEL" \
  '{model: $model, messages: [{role: "user", content: "Hello"}], stream: false}' \
  > request.json
curl --fail-with-body --silent --show-error --max-time 60 \
  "${AI_BASE_URL%/}/chat/completions" \
  -H "Authorization: Bearer ${AI_API_KEY}" \
  -H 'Content-Type: application/json' \
  --data-binary @request.json
```

### 下一步：从普通聊天到应用功能 / Beyond Text Chat

| 要增加的功能 | 需要改变什么 | 判断成功的标准 |
|---|---|---|
| Streaming / 流式输出 | 使用流式请求，并逐条解析事件 | 收到内容和结束事件，处理中途失败 |
| Tool calling / 工具调用 | 提供工具定义，执行经允许的工具，再回传结果 | 模型能基于真实工具结果继续回答 |
| JSON output / 结构化输出 | 根据协议启用输出约束，并进行本地解析校验 | 字段、类型、必填项符合预期 |
| Vision / 图片输入 | 使用该线路接受的图像消息格式 | 能正确回答与图片内容相关的问题 |
| Responses / Messages | 更换端点、请求结构和解析器 | 用新协议单独跑通整个请求流程 |

<a id="budget-playbook"></a>
## 低成本 AI 应用预算 / Low-cost API Budget Playbook

以下使用开头 **DeepSeek V4.1 Flash 专供线路** 的公开报价：普通输入 ¥0.05 / 1M，输出 ¥0.20 / 1M。用量是假设场景，费用是按报价计算；不含缓存及其他计费项，不是生产吞吐量或任务质量承诺。

| 场景 | 每次普通输入 | 每次输出 | 每次估算 | 1,000 次估算 |
|---|---:|---:|---:|---:|
| 分类、打标签 | 1,000 tokens | 100 tokens | ¥0.00007 | ¥0.07 |
| 短文本翻译 | 2,000 tokens | 1,000 tokens | ¥0.00030 | ¥0.30 |
| 文档摘要 | 20,000 tokens | 2,000 tokens | ¥0.00140 | ¥1.40 |
| 较长代码问答 | 40,000 tokens | 5,000 tokens | ¥0.00300 | ¥3.00 |

### 如何降低 Agent、RAG 与 AI 编程费用？

| 成本来自哪里 | 可以先做的调整 | 需要同时观察 |
|---|---|---|
| 每轮重复发送大量历史 | 保留必要历史，压缩旧工具输出 | 是否丢失任务约束和重要事实 |
| 检索返回过多文档 | 去重，按相关性选择片段 | 正确答案所需片段是否还在 |
| 所有任务都用昂贵模型 | 简单分类和复杂推理分别选模型 | 完成率，不能只比较输入单价 |
| Agent 一直调用工具 | 设轮数、时间、费用上限 | 触顶时明确返回未完成状态 |
| 输出过长 | 在任务里指定结果格式和长度 | 是否截断必要内容 |
| 错误自动反复重试 | 区分限流、权限、参数错误；限制次数 | 不要重试无法自行恢复的错误 |
| 缓存价格理解错误 | 把普通输入、缓存读、缓存写分开统计 | 命中率与实际账单变化 |

### 便宜和划算的区别 / Price vs Cost per Completed Task

假设模型 A 每次尝试 ¥0.01，20 次完成 10 项任务，总花费 ¥0.20，平均每项完成任务 ¥0.02。模型 B 每次 ¥0.015，10 次完成同样 10 项任务，总花费 ¥0.15，平均每项 ¥0.015。这个假设例子说明：更低的单次价格可能被失败和重试抵消。

评估时同时记录 **总花费、完成任务数、平均完成时间、人工修正量**。选择最便宜且能满足你任务标准的线路，而不是只看模型名或输入报价。

<a id="workflow-recipes"></a>
## AI 应用组合与工作流 / Practical Workflow Recipes

### Dify 知识库 / Document Q&A

基本流程：文档 → 切分 → embedding → 检索 → 可选 rerank → 文本模型回答。聊天模型的 API Key 不代表一定能调用 embedding 或 rerank。先用一份短文档检查检索片段，再查看回答引用，最后扩展资料量。

预算分成两部分：导入文档时的处理费用，以及每次问答时的检索和生成费用。更换 embedding 模型后，应检查向量维度及已有索引是否仍适用。

### n8n 批量摘要 / Batch Summarization

基本流程：读取记录 → 按条组织输入 → 调用模型 → 校验输出 → 保存结果。给每条记录一个稳定 ID，保存成功和失败状态；恢复执行时跳过已完成项。并发从小量开始，遇到限流再调整，而不是直接把全部数据同时发送。

### AI 编程 / Coding Agents

基本流程：明确任务 → 读取相关文件 → 模型提出修改 → 执行允许的操作 → 运行项目检查。先用一个小修复验证工具调用及代码编辑，确认后再扩大任务。预算应覆盖所有轮次、文件内容和工具输出，而不是只计算第一句需求。

### 翻译与结构化提取 / Translation & Extraction

为每条输入保留 ID，明确术语表及输出字段。将输出解析失败、漏项和内容失败分开记录。批量任务先用一小组长短不同的样本检查，避免一条过长文本导致整批无法处理。

### 图片、语音与视频 / Multimodal Tasks

先确认自己需要的是图片理解还是图片生成、语音识别还是语音合成。这些任务可能有独立协议和计费单位。异步任务应保存 task ID，检查最终状态和产物是否可下载；请求被接受不等于生成完成。

<a id="agent-mcp"></a>
## LLM API、Agent 与 MCP 的区别 / LLM APIs, Agents & MCP

```text
用户任务
  → 客户端或 Agent：组织上下文、决定下一步
    → LLM API：调用模型生成内容或工具请求
    → 工具连接：读取文件、查询资料、执行获准操作
      → MCP Server：以约定接口提供工具或资源
  → 返回结果，并记录调用与费用
```

MCP 是连接工具和资源的一种方式，不是模型额度，也不会让不支持工具调用的线路自动获得完整 Agent 能力。即使模型返回了工具调用参数，仍需要应用验证参数、执行操作并回传结果。

| 常见疑问 | 区分方式 |
|---|---|
| 买了 API，是不是就有 Agent？ | API 提供模型调用；Agent 还需要任务循环、工具和状态管理 |
| MCP Server 是否等于 API 中转？ | MCP Server 提供工具或资源；模型网关主要管理模型请求 |
| 工具调用是否代表命令已执行？ | 模型可能只是提出调用请求，实际执行由应用完成 |
| 一个模型能聊天，是否就能用于编程 Agent？ | 还要检查工具参数、长上下文、流式事件与客户端协议 |
| 工作流工具是否免费提供模型？ | 工具的软件许可和模型调用费用应分别核对 |

<a id="extended-faq"></a>
## 更多常见问题 / More API Questions

### 便宜 API 能直接用在 Claude Code、Codex 或 Cursor 吗？

要同时满足客户端的协议、认证和所用功能。先确认具体线路，再做一个小任务。某个编辑器中的聊天功能可用，不代表其 Agent、补全和其他功能都会走相同的自定义 API。

### API Key、Base URL、模型 ID 分别是什么？

Key 用于认证和权限；Base URL 指向模型服务入口；模型 ID 指定调用对象。三者来自同一套接入说明才有意义。模型的展示名称可能与请求中需要的 ID 不同。

### 为什么模型列表里看得到，却调用失败？

列表只是可发现信息。实际调用还受 Key 所属分组、账户额度、线路状态和具体端点影响。保存错误类型和请求 ID，逐项检查，而不是反复刷新模型列表。

### 1M tokens 等于多少汉字？

没有固定换算。模型使用的 tokenizer、语言、代码和符号都会改变 token 数。预算先用代表性样本的实际 usage 外推；不要把“百万 tokens”写成“百万字”。

### 免费 AI API 适合生产使用吗？

先看额度周期、限速、允许的用途和到期规则。试用额度可以用于验证流程；生产预算应按试用结束后的费用计算，并准备额度用尽时的明确错误处理。

### 流式输出会不会自动更便宜？

流式只是传输方式，不等于少生成 tokens。它可以更早展示内容，但费用仍取决于具体计费规则和实际用量。取消请求后，上游是否立即停止以及如何计费，需要单独核对。

### OpenAI-compatible 能不能调用 Claude 或 Gemini？

只有服务为相应模型提供该兼容协议时才可以。协议转换还可能影响工具、图片、推理字段或其他特性；用应用真正需要的功能验证。

### 模型会自动联网搜索吗？

普通文本请求并不自动包含联网搜索。需要模型服务提供相应工具，或由应用先检索再把资料交给模型。仅有最新日期或自信的回答不能证明实际搜索过。

### 为什么长对话越来越贵？

许多客户端会把历史消息再次加入后续请求，工具输出也可能进入上下文。观察每轮输入量，保留必要信息，适时整理历史；同时注意不要删掉影响结果的约束。

### 多人共用一个 Key 可以吗？

先核对平台规则和权限需求。实际管理中，为不同应用或使用者分开配置凭据更容易定位费用和撤销访问。不要在前端代码里公开主 Key。

### 自部署模型就没有 API 费用了吗？

可能不再向外部平台按 token 付费，但仍有硬件、算力、电力和运维成本。比较时用同样的任务量和质量要求，并考虑闲置资源。

### 怎样反馈问题更快得到处理？

提供时间、客户端版本、模型 ID、线路、端点、错误码和脱敏后的最小请求。如果有 request ID 一并提供；不要提供完整 Key 或私人文档。可使用本仓库的 [问题模板](https://github.com/welsir/ai-api-guide/issues/new/choose)。

<a id="glossary"></a>
## AI API 术语表 / Glossary

| 术语 | 含义 | 为什么会影响你 |
|---|---|---|
| API Key | 调用凭据 | 决定权限及费用归属 |
| Base URL | 服务基础地址 | 拼接错误可能导致 404 |
| Model ID | 请求中的模型标识 | 展示名称不一定能直接调用 |
| Token | 模型处理文本等内容的计量单元 | 字数不能直接替代账单用量 |
| Context window | 单次上下文容量 | 影响能放入多少资料与历史 |
| Output limit | 输出上限 | 与上下文窗口不是同一个数 |
| Streaming / SSE | 持续发送事件或内容 | 客户端需要处理结束和错误事件 |
| TTFT | 首个 token 的等待时间 | 反映开始看到输出前的等待 |
| Tokens per second | token 输出速度 | 不等于整个任务的完成速度 |
| RPM / TPM | 每分钟请求数 / token 数 | 两种限制可能分别触发 |
| Concurrency | 同时进行的请求数 | 与每分钟总请求数不同 |
| Prompt cache | 复用已处理的输入部分 | 需要区分缓存读、写和未命中 |
| Tool calling | 模型提出结构化工具请求 | 应用仍需执行和回传结果 |
| Structured output | 约束输出结构 | 仍要校验业务内容是否正确 |
| Embedding | 将内容转换为向量 | 用于检索等任务，模型变化影响索引 |
| Rerank | 对候选结果重新排序 | 可以改变最终传给模型的材料 |
| RAG | 检索资料后再生成回答 | 检索质量和回答质量都要检查 |
| Agent | 结合模型、工具和状态执行任务 | 费用可能包含很多轮调用 |
| MCP | 工具与资源连接协议 | 不等同于模型 API 或模型额度 |
| BYOK | 使用自己的 Key | 通常仍需承担 Key 对应上游费用 |
| Fallback | 失败后的替代处理 | 应明确是否切模型、切线路及如何计费 |
| Observability | 观测调用、错误与费用 | 帮助定位复杂任务为什么慢或贵 |

<a id="maintenance"></a>
## 验证与更新 / Verification, Updates & Contributions

**内容核对日期：2026-10-19。** 首版完成选型、配置检查与成本说明；尚未发布逐线路端到端兼容测试结果，也没有实测性能排行。验证如何记录，见[验证方法](docs/verification.md)。

- 价格与模型可用性：查看 Orbis 当前线路页；本文的数字成本例子为假设算例。
- 纠错或接入需求：[提交 Issue](https://github.com/welsir/ai-api-guide/issues/new/choose)，附工具版本、模型与脱敏错误。
- 内容贡献：[贡献指南](CONTRIBUTING.md)；提交真实经验或可复现的修正。
- 更新历史：[CHANGELOG](CHANGELOG.md)。

### 维护关系

本项目由 Orbis 维护，包含指向 Orbis 商业服务的链接；不代表所提及模型厂商、客户端或框架的官方项目或背书。链接中的 UTM 用于区分访问来源，不包含 API Key。

原创内容按 [MIT License](LICENSE) 提供；第三方名称和商标属于其各自所有者。
