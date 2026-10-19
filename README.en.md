# AI API Guide · Models, Costs & Tool Integration

**Choose an LLM API, understand its protocol and pricing, and connect it to your coding tools or workflows.**

[Models & routes](https://orbiorbi.com/pricing?utm_source=github&utm_medium=readme&utm_campaign=ai-api-guide&utm_content=en-header-models) · [Connection docs](https://orbiorbi.com/tutorials?utm_source=github&utm_medium=readme&utm_campaign=ai-api-guide&utm_content=en-header-docs) · [Orbis](https://orbiorbi.com/?utm_source=github&utm_medium=readme&utm_campaign=ai-api-guide&utm_content=en-header-home) · [简体中文](README.md)

A practical guide to Claude, GPT, Gemini, DeepSeek, Kimi, Qwen and GLM APIs; AI coding clients; OpenAI-compatible endpoints; usage costs; and common integration errors. Maintained by **Orbis**, a commercial multi-model API platform. This is a provider-maintained guide, not an independent provider ranking.

<a id="why-orbis"></a>
## Orbis: Affordable Multi-Model API

**DeepSeek V4.1 Flash on the Orbis Exclusive route: ¥0.05 per million ordinary input tokens and ¥0.20 per million output tokens.** Choose a model and route around your budget for chat, batch processing and AI coding.

### Featured API Pricing

All prices are in **Chinese yuan per 1 million tokens (CNY / 1M tokens)**, from the public catalog on **2026-10-19**. Each row refers to a specific route.

| Model | Route | Ordinary input | Output | Cache read |
|---|---|---:|---:|---:|
| [DeepSeek V4.1 Flash](https://orbiorbi.com/pricing/deepseek-v4.1-flash?catalogKey=model%2F129&offering=orbis-exclusive-deepseek-v4-1-flash&group=%E9%80%9A%E7%94%A8+%C2%B7+Orbis%E4%B8%93%E4%BE%9B%E7%BA%BF%E8%B7%AF&utm_source=github&utm_medium=readme&utm_campaign=ai-api-guide&utm_content=value-pricing) | Orbis Exclusive | ¥0.05 | ¥0.2 | ¥0.01 |
| [Kimi K3](https://orbiorbi.com/pricing/kimi-k3?catalogKey=model%2F139&offering=orbis-exclusive-kimi-k3&group=%E9%80%9A%E7%94%A8+%C2%B7+Orbis%E4%B8%93%E4%BE%9B%E7%BA%BF%E8%B7%AF&utm_source=github&utm_medium=readme&utm_campaign=ai-api-guide&utm_content=value-pricing) | Orbis Exclusive | ¥0.1 | ¥0.5 | ¥0.4 |
| [GPT-6.1 Sol](https://orbiorbi.com/pricing/gpt-6.1-sol?catalogKey=model%2F91&offering=channel-86%2Fdedfefd51120&group=GPT+%C2%B7+HA%E7%BA%BF%E8%B7%AF&utm_source=github&utm_medium=readme&utm_campaign=ai-api-guide&utm_content=value-pricing) | GPT · HA | ¥0.225 | ¥1.125 | ¥0.01125 |
| [GLM 5.3](https://orbiorbi.com/pricing/glm-5.3?catalogKey=model%2F132&offering=orbis-exclusive-glm-5-3&group=%E9%80%9A%E7%94%A8+%C2%B7+Orbis%E4%B8%93%E4%BE%9B%E7%BA%BF%E8%B7%AF&utm_source=github&utm_medium=readme&utm_campaign=ai-api-guide&utm_content=value-pricing) | Orbis Exclusive | ¥0.5 | ¥2 | ¥0.25 |

**What does that cost in practice?** At the listed DeepSeek rates, 1 million ordinary input tokens plus 1 million output tokens cost **¥0.25**. The same volumes on the listed Kimi K3 route cost **¥0.60**. These text-usage examples exclude cache writes, other modalities and additional billing items.

### Why Orbis

- **Low-cost entry**: exclusive routes offer inexpensive model options so you can start with a small budget.
- **Pay as you go, no monthly fee**: pay for actual usage; your balance does not expire.
- **Multiple models and selectable routes**: access Claude, GPT, Gemini, DeepSeek, Kimi and more through one platform. See route prices and choose the route yourself.
- **Familiar API formats**: OpenAI-compatible and Anthropic protocol routes help connect existing applications. Supported endpoints and capabilities depend on the selected route.
- **CNY billing and usage tracking**: budget in Chinese yuan and inspect usage and costs in the console.

**[Browse all model and route prices →](https://orbiorbi.com/pricing?utm_source=github&utm_medium=readme&utm_campaign=ai-api-guide&utm_content=en-value-all-models)** · **[Get started with Orbis →](https://orbiorbi.com/?utm_source=github&utm_medium=readme&utm_campaign=ai-api-guide&utm_content=en-value-start)**

Check the linked route for current prices. Cache reads and writes are billed separately; the listed Kimi K3 cache-read rate is higher than its ordinary input rate. These are checked public quotes, not live route benchmark results.

## Start with your task

| Your goal | Start here |
|---|---|
| Connect a coding or chat client | [Tool configuration](#tool-configuration) |
| Choose a model or provider | [Model selection](#model-selection) |
| Estimate your bill | [Costs](#costs) |
| Migrate an existing application | [Protocols and migration](#protocols-and-migration) |
| Fix an API error | [Troubleshooting](#troubleshooting) |
| Use Orbis | [Connect through Orbis](#connect-through-orbis) |

<a id="model-selection"></a>
## Model selection

Choose the features required by a real task before comparing advertised prices. Model families, versions and routes can differ in context limits, output limits, supported endpoints and billing.

| Model family | What to check | A useful task to compare |
|---|---|---|
| Claude | Required Messages or compatible protocol; streaming and tool events | Code changes, long documents, multi-step tool use |
| GPT / OpenAI | Chat Completions versus Responses; required parameters | Structured extraction, code editing, tool calls |
| Gemini | Native versus compatible API; supported input formats | Your own multimodal or document samples |
| DeepSeek | Exact model ID, reasoning output, cache billing | Chinese-language tasks, code, batch text processing |
| Kimi | Context and output limits; tool calling | Long-document retrieval and multi-step tasks |
| Qwen | Exact model and modality; serving protocol | Text extraction, vision, in-app chat |
| GLM | Version, tool formats and client requirements | Coding clients and workflows |

These are evaluation questions, not rankings or a claim that every listed capability is available through Orbis. Compare candidates on the same inputs, then examine quality, cost and failures. A model name returned by the model itself is not identity verification.

When choosing an API provider, check the exact model and route, protocol, feature support, billing units, reliability evidence, data handling and migration effort. Direct model APIs, hosted aggregators and self-hosted gateways solve different operational needs.

[Browse current Orbis models and routes](https://orbiorbi.com/pricing?utm_source=github&utm_medium=readme&utm_campaign=ai-api-guide&utm_content=en-model-guide). Use the selected route's connection page for exact IDs and settings.

<a id="tool-configuration"></a>
## Tool configuration

Prepare the **Base URL, API Key and exact model ID**, then confirm the protocol required by your tool version. The table below is a configuration checklist, not an end-to-end compatibility certification.

| Tool | Check before connecting | Validate afterwards |
|---|---|---|
| Claude Code | Current provider and authentication options; matching protocol | Multi-turn tool events and stream completion |
| Codex / Codex CLI | Provider configuration, authentication source, wire API | A small request followed by a controlled coding task |
| Cline / Roo Code / Kilo Code | Available provider options and model capability settings | Tool arguments, streaming and context limits |
| Cursor | Which features honor custom keys or endpoints; version and account conditions | The specific feature you intend to use |
| Cherry Studio | Provider type, URL path handling and exact model ID | Text chat, then optional image or tool features |
| Open WebUI / LobeHub | Connection settings, backend connectivity and model discovery | Both listing models and sending a message |
| Dify | Chat model and embedding provider configured separately where needed | Generation, then indexing and retrieval |
| n8n | Node version, credentials and supported endpoint options | One node before the full workflow |
| LangChain / AI SDK | Adapter protocol and feature support | Text, streaming and tool calling separately |

Copy settings from the service's connection page. Whether `/v1` belongs in the Base URL depends on the client: some append paths themselves. Keep real keys in local environment variables or the client's credential settings, never in a public example or Issue.

<a id="protocols-and-migration"></a>
## Protocols and migration

“OpenAI-compatible” describes a compatibility surface; it does not imply support for every OpenAI endpoint.

- **Chat Completions:** check message shapes, stream chunks, tool calls and usage.
- **Responses:** validate separately; success with Chat Completions is insufficient.
- **Anthropic Messages:** authentication, payloads and stream events differ.
- **Structured output:** returning JSON text is not the same as enforcing a schema.
- **Tool calling:** check arguments, call IDs, returned tool results and follow-up turns.
- **Embeddings:** changed models or dimensions may require rebuilding your index.
- **Images, audio and video:** may use different endpoints, async jobs and billing units.

Migration checklist:

- [ ] Replace the endpoint, authentication and model ID without committing credentials.
- [ ] Verify every endpoint your application needs.
- [ ] Test normal responses, streaming and tools separately.
- [ ] Bound timeouts and retries to avoid unexpected costs.
- [ ] Reconcile usage with billing units.
- [ ] Compare real samples and retain a recoverable previous configuration.

<a id="costs"></a>
## Costs

Normalize currency, unit, model, route and functionality before comparing prices. Token, image, video-duration and per-request pricing are not interchangeable. Account credits may not map one-to-one to a currency.

For text requests without caching or additional charges:

```text
Cost = input tokens / 1,000,000 × input price
     + output tokens / 1,000,000 × output price
```

**Illustration only, not an Orbis or vendor quote:** assume ¥1 per million input tokens and ¥4 per million output tokens.

| Example | Input tokens | Output tokens | Cost per request | 1,000 identical requests |
|---|---:|---:|---:|---:|
| Short extraction | 2,000 | 500 | ¥0.004 | ¥4 |
| Document summary | 20,000 | 2,000 | ¥0.028 | ¥28 |
| Longer code request | 40,000 | 5,000 | ¥0.060 | ¥60 |

An agent task can make many requests. Count history, tool loops, retries and output across the whole task. Check cache hits, misses and writes, long-context pricing tiers, cancellation rules and non-text charges against actual usage and bills.

[Check current route pricing on Orbis](https://orbiorbi.com/pricing?utm_source=github&utm_medium=readme&utm_campaign=ai-api-guide&utm_content=en-cost). Start with a small task before scaling a batch.

## RAG, agents and multimodal workflows

| Use case | Check | A useful acceptance result |
|---|---|---|
| RAG / document chat | Generation, embeddings or existing retrieval; optional reranking | Answers cite the supplied documents |
| AI agents | Tools, state, error handling and cost boundaries | A controlled multi-step task completes or stops clearly |
| Translation / batch processing | Structured output, length and terminology | Every input has a corresponding complete result |
| Code review | Code understanding, context and tools | Changes pass the project's relevant checks |
| Vision / OCR | Image support on the specific route | Correct fields extracted from your own samples |
| Image, video or speech generation | Endpoints, output formats, async states, units | Usable output and explicit failure reporting |

These are requirements to test, not a list of features already certified on Orbis.

<a id="troubleshooting"></a>
## Troubleshooting

| Symptom | First check |
|---|---|
| 401 Unauthorized | Correct service, key and authentication format |
| 403 Forbidden | Account, model and route permissions |
| 404 / model not found | Distinguish a missing endpoint from a wrong model ID |
| 429 | Rate, concurrency, quota and the returned error; use bounded backoff |
| 400 / unsupported parameter | Reduce to the smallest request, then add fields individually |
| Broken streaming | Event parsing, buffering, timeouts and upstream errors |
| Failed tool calls | Schema, call ID, tool result and follow-up message format |
| Unexpected bill | Output, history, cache behavior and retries |

**Can I use a chat subscription as API credit?** Do not assume chat subscriptions and developer API billing are shared. Confirm the product and authorization you actually purchased.

**Is changing the Base URL enough?** Only when protocol, endpoint, model, authentication and required functionality all match.

**Can a prompt prove the model's identity?** No. Repeated comparisons with a trusted baseline can reveal anomalies, but a self-reported model name or a single answer is not proof.

**Is there a free tier?** Separate permanent quotas, temporary promotions and one-time credits. This guide does not promise free Orbis credit; consult current site terms.

<a id="connect-through-orbis"></a>
## Connect through Orbis

Orbis presents models and selectable routes. Based on the product pages reviewed, the same model may have routes with different pricing and protocols, and an API Key is associated with a selected group.

1. Choose a model in the [catalog](https://orbiorbi.com/pricing?utm_source=github&utm_medium=readme&utm_campaign=ai-api-guide&utm_content=en-select).
2. Select a route and read its pricing, protocol and connection instructions.
3. Create a Key for the matching group.
4. Copy the Base URL and model ID from that connection page.
5. Verify a short request, required advanced features and billing before scaling.

Catalog listings, configuration declarations and live test results are different evidence levels. Parameters marked “configuration declared; execution unknown” are not verified functionality.

[Models & routes](https://orbiorbi.com/pricing?utm_source=github&utm_medium=readme&utm_campaign=ai-api-guide&utm_content=en-next) · [Connection docs](https://orbiorbi.com/tutorials?utm_source=github&utm_medium=readme&utm_campaign=ai-api-guide&utm_content=en-docs) · [API Keys](https://orbiorbi.com/keys?utm_source=github&utm_medium=readme&utm_campaign=ai-api-guide&utm_content=en-keys)

## Verification and maintenance

Content reviewed: **2026-10-19**. This first edition provides selection and configuration guidance. It does not publish completed route-by-route compatibility tests or a measured performance leaderboard. See the [verification method](docs/verification.md), [contribution guide](CONTRIBUTING.md) and [changelog](CHANGELOG.md).

Report reproducible problems using [Issues](https://github.com/welsir/ai-api-guide/issues/new/choose). Remove keys, personal data and sensitive prompts first.

Orbis maintains this guide and provides a commercial API service. No affiliation or endorsement by the named model vendors or client projects is implied. Outbound Orbis links use UTM parameters to distinguish referral sources; they contain no API keys. Original content is available under the [MIT License](LICENSE).
