# AI API Guide · 模型选型、价格与工具接入指南

**从 Claude、GPT、Gemini、DeepSeek、Kimi、Qwen，到 Claude Code、Codex、Cline 和 AI 工作流：先弄清怎么选，再开始调用。**

[模型与线路](https://orbiorbi.com/pricing?utm_source=github&utm_medium=readme&utm_campaign=ai-api-guide&utm_content=header-models) · [接入文档](https://orbiorbi.com/tutorials?utm_source=github&utm_medium=readme&utm_campaign=ai-api-guide&utm_content=header-docs) · [Orbis](https://orbiorbi.com/?utm_source=github&utm_medium=readme&utm_campaign=ai-api-guide&utm_content=header-home) · [English](README.en.md)

这里整理 AI API、LLM API 与 API 中转服务的选型方法、模型家族、客户端配置要点、调用成本和常见错误。由 **Orbis** 维护；Orbis 是提供多模型、多线路接入的商业 API 平台。文中的选型方法也适用于其他服务，不是第三方独立排名。

---

## 快速选择：你现在要解决什么？

| 你的问题 | 从这里开始 | 要拿到的结果 |
|---|---|---|
| 想给 Claude Code、Codex 或 Cline 接模型 | [工具接入](#tool-setup) | 工具需要的协议、地址格式和验证步骤 |
| 想比较 Claude、GPT、DeepSeek、Kimi 等 API | [模型选型](#model-guide) | 按实际任务挑候选模型，再比较线路 |
| 想找便宜的 AI API，又怕成本算错 | [价格与成本](#cost-guide) | 输入、输出、缓存和失败重试的完整成本 |
| 已有 OpenAI SDK 项目，想换服务 | [协议与迁移](#protocol-guide) | 不把“兼容”误解为所有端点都支持 |
| 遇到 401、404、429 或流式中断 | [排错表](#troubleshooting) | 一个可定位的最小问题 |
| 在做 RAG、Agent、n8n 或 Dify 工作流 | [应用场景](#use-cases) | 先核对真正需要的模型能力 |
| 想直接使用 Orbis | [Orbis 接入](#orbis-setup) | 选模型、选线路、创建对应 Key |

### 目录

- [API 服务怎么选](#choose-provider)
- [Claude、GPT、Gemini、DeepSeek、Kimi、Qwen 模型选型](#model-guide)
- [Claude Code、Codex、Cline 等工具接入](#tool-setup)
- [OpenAI-compatible、Anthropic 与 API 迁移](#protocol-guide)
- [价格、缓存与场景成本](#cost-guide)
- [RAG、Agent、多模态与工作流](#use-cases)
- [常见错误与 FAQ](#troubleshooting)
- [通过 Orbis 接入](#orbis-setup)
- [验证记录、更新与贡献](#maintenance)

<a id="choose-provider"></a>
## API 服务怎么选：看任务、协议和完整成本

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
## 模型选型：模型家族 × 真实任务

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

**三步缩小选择范围：**先按功能筛选 → 用同一组真实样本比较 → 结合成本与失败情况决定。短题答对、模型自报名称或一次接口成功都不能证明模型身份。

[查看 Orbis 当前模型与线路](https://orbiorbi.com/pricing?utm_source=github&utm_medium=readme&utm_campaign=ai-api-guide&utm_content=model-guide)。具体版本、可用状态和报价以选择的线路页面为准。

<a id="tool-setup"></a>
## AI 工具接入：Claude Code、Codex、Cline 与聊天客户端

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
## OpenAI-compatible、Anthropic 与 API 迁移

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
## AI API 价格怎么算：输入、输出、缓存与任务成本

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
## RAG、Agent、翻译与多模态：按任务核对能力

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
## API 常见错误与 FAQ

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
## 通过 Orbis 接入：模型 + 线路 + Key

[Orbis](https://orbiorbi.com/?utm_source=github&utm_medium=readme&utm_campaign=ai-api-guide&utm_content=orbis-setup) 把模型及可选择的分组线路集中展示。根据已查看的产品页面，同一模型可有不同线路，价格与协议按线路区分，API Key 绑定所选分组。

1. **选模型**：在[模型广场](https://orbiorbi.com/pricing?utm_source=github&utm_medium=readme&utm_campaign=ai-api-guide&utm_content=select-route)找到目标模型。
2. **选线路**：比较价格、协议和参数说明，打开该线路的接入页。
3. **创建 Key**：选择与线路一致的分组；Key 只放在你自己的凭据设置中。
4. **复制配置**：使用接入页给出的 Base URL 和模型 ID。
5. **小量验证**：先完成短请求，再验证流式、工具调用等所需能力，核对账单。

网站展示、线路声明和实际测试是三类不同证据。标记为“配置声明 · 执行未知”的参数，不能当作已验证功能。

**下一步：**[查看模型与线路](https://orbiorbi.com/pricing?utm_source=github&utm_medium=readme&utm_campaign=ai-api-guide&utm_content=footer-models) · [阅读接入文档](https://orbiorbi.com/tutorials?utm_source=github&utm_medium=readme&utm_campaign=ai-api-guide&utm_content=footer-docs) · [进入 API Key 页面](https://orbiorbi.com/keys?utm_source=github&utm_medium=readme&utm_campaign=ai-api-guide&utm_content=footer-keys)

<a id="maintenance"></a>
## 验证记录、更新与贡献

**内容核对日期：2026-10-19。** 首版完成选型、配置检查与成本说明；尚未发布逐线路端到端兼容测试结果，也没有实测性能排行。验证如何记录，见[验证方法](docs/verification.md)。

- 价格与模型可用性：查看 Orbis 当前线路页；本文的数字成本例子为假设算例。
- 纠错或接入需求：[提交 Issue](https://github.com/welsir/ai-api-guide/issues/new/choose)，附工具版本、模型与脱敏错误。
- 内容贡献：[贡献指南](CONTRIBUTING.md)；提交真实经验或可复现的修正。
- 更新历史：[CHANGELOG](CHANGELOG.md)。

### 参考与维护关系

目录与选型组织方式参考了社区项目 [Awesome AI Gateway](https://github.com/cuihuan/awesome-ai-gateway)。本文为独立编写，不复制其排名或评测结论。

本项目由 Orbis 维护，包含指向 Orbis 商业服务的链接；不代表所提及模型厂商、客户端或框架的官方项目或背书。链接中的 UTM 用于区分访问来源，不包含 API Key。

原创内容按 [MIT License](LICENSE) 提供；第三方名称和商标属于其各自所有者。
