# 验证方法 / Verification method

[返回指南](../README.md) · [English guide](../README.en.md)

## 当前状态

2026-10-19：首版仅核对公开产品页面和文档表达，未完成逐工具、逐线路的真实 API 调用验证。没有性能排名、模型身份认证或可用率承诺。

## 三种证据不能混用

| 类型 | 能证明什么 | 不能证明什么 |
|---|---|---|
| 目录展示 | 页面列出了某个模型、价格或能力 | 当前请求能成功、所有参数生效 |
| 配置声明 | 接入页声明某种协议或参数 | 实际执行语义、端到端兼容 |
| 实际测试 | 某日期、版本、线路下的具体测试结果 | 所有版本、全部线路和未来一直可用 |

## 一条可复核记录需要什么

- 日期与时区、工具或 SDK 版本。
- 模型 ID、所选分组线路、协议、请求路径。
- 脱敏最小请求，必要参数和测试目的。
- HTTP 状态、错误类型、响应结构或预期结果。
- 明确结果：通过、失败、未测试。不把未测试写成不支持。
- 若报告延迟或成功率，给出采样时间范围、样本数、输入输出规模和统计方法。
- 若报告费用，给出币种、计费单位、usage 与账单对应关系。

## 分层验证

1. 普通短消息：认证、模型名、消息格式。
2. 流式：事件类型、结束状态和中断处理。
3. 工具调用：工具参数、调用 ID、结果回传、下一轮响应。
4. 结构化输出：schema 验证，而非只看 JSON 能否解析。
5. 实际工具：在特定客户端版本完成受控任务。
6. 成本：按真实用量核对账单，区分重试和缓存。

模型自报名称、一个聪明回答和一次 HTTP 200 都不是模型身份或长期稳定性的证明。功能结果只能证明所测试的行为。

## 发布前脱敏

不要提交 API Key、Authorization 头、Cookie、私有服务凭据、个人信息、真实业务文档或未经允许公开的请求内容。提供可公开的最小样本；必要时联系服务方处理私有问题。

## English summary

The first edition contains no completed end-to-end certification. Separate catalog observations, declared configuration and live test results. Record date, client version, model, route, protocol, sanitized reproduction and a bounded result. Measure streaming, tools, schemas and billing separately. Never submit credentials or sensitive inputs. A successful response does not establish model identity or durable reliability.
