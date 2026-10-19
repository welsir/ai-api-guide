# AI API Guide · Models, Costs & Tool Integration

**Choose an LLM API, understand its protocol and pricing, and connect it to your coding tools or workflows.**

[Models & routes](https://orbiorbi.com/pricing?utm_source=github&utm_medium=readme&utm_campaign=ai-api-guide&utm_content=en-header-models) · [Connection docs](https://orbiorbi.com/tutorials?utm_source=github&utm_medium=readme&utm_campaign=ai-api-guide&utm_content=en-header-docs) · [Orbis](https://orbiorbi.com/?utm_source=github&utm_medium=readme&utm_campaign=ai-api-guide&utm_content=en-header-home) · [简体中文](README.md)

A practical guide to Claude, GPT, Gemini, DeepSeek, Kimi, Qwen and GLM APIs; AI coding clients; OpenAI-compatible endpoints; usage costs; and common integration errors. Maintained by **Orbis**, a commercial multi-model API platform. This is a provider-maintained guide, not an independent provider ranking.

<a id="why-orbis"></a>
## Orbis: Affordable Multi-Model API

**DeepSeek V4.1 Flash on the Orbis Exclusive route: ¥0.05 per million ordinary input tokens and ¥0.20 per million output tokens.** Choose a model and route around your budget for chat, batch processing and AI coding.

### Featured API Pricing

All prices are in **¥ / 1M tokens**, from the public catalog on **2026-10-19**. Each row refers to a specific route.

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
- **¥ pricing and usage tracking**: budget using listed prices and inspect usage and costs in the console.

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

### Explore the guide

- [AI 项目导航 / AI Resource Directory](#resource-directory)
- [托管与自部署 / Hosted vs Self-hosted](#deployment-options)
- [调用示例 / Python, JavaScript & cURL](#request-examples)
- [低成本预算 / Budget Playbook](#budget-playbook)
- [应用工作流 / Workflow Recipes](#workflow-recipes)
- [Agent 与 MCP / Agents & MCP](#agent-mcp)
- [更多问题 / More FAQ](#extended-faq)
- [术语表 / Glossary](#glossary)

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

<a id="resource-directory"></a>
## AI Resource Directory

Find a tool by the job you need it to do. Links point to the projects' own GitHub repositories; descriptions and archive status were checked on **2026-10-19**. Inclusion is not an Orbis compatibility certification. Review the current license and version requirements before deployment or commercial use.

### AI gateways and API management

| Project | Purpose | When to explore it |
|---|---|---|
| [LiteLLM](https://github.com/BerriAI/litellm) | Unified model access and call management | You already have several upstream keys |
| [New API](https://github.com/QuantumNous/new-api) | Model aggregation and distribution | You need model, channel and user management |
| [One API](https://github.com/songquanpeng/one-api) | API adaptation and key distribution | You maintain an existing One API installation |
| [Bifrost](https://github.com/maximhq/bifrost) | Model and agent gateway | You need to evaluate routing, budgets and failover |
| [Higress](https://github.com/higress-group/higress) | AI-native API gateway | You want to add AI traffic to gateway infrastructure |
| [Portkey Gateway](https://github.com/Portkey-AI/gateway) | Multi-model request routing | You need centralized upstream request policies |
| [agentgateway](https://github.com/agentgateway/agentgateway) | Agent and MCP proxy | You need to manage agent-to-MCP access |

### Coding and chat clients

| Project | Purpose | When to explore it |
|---|---|---|
| [Cline](https://github.com/cline/cline) | Coding agent | Use models and tools in a development workflow |
| [Kilo Code](https://github.com/Kilo-Org/kilocode) | Agentic development platform | Evaluate model-powered engineering workflows |
| [Aider](https://github.com/Aider-AI/aider) | Terminal pair programming | Work with a model on code from your terminal |
| [Cherry Studio](https://github.com/CherryHQ/cherry-studio) | Multi-model desktop workspace | Use multiple models and assistants in one workspace |
| [Open WebUI](https://github.com/open-webui/open-webui) | Model chat interface | Add a web chat interface to model services |
| [LobeHub](https://github.com/lobehub/lobehub) | Agent workspace | Organize multiple assistants and tasks |

### Workflows and application development

| Project | Purpose | When to explore it |
|---|---|---|
| [Dify](https://github.com/langgenius/dify) | Agent workflows and RAG applications | Build business applications with knowledge retrieval |
| [n8n](https://github.com/n8n-io/n8n) | Visual workflow automation | Connect AI steps to business systems |
| [LangChain](https://github.com/langchain-ai/langchain) | Agent application development | Compose models, tools and tasks in code |
| [LlamaIndex](https://github.com/run-llama/llama_index) | Document processing and retrieval | Connect your documents to an AI application |
| [AI SDK](https://github.com/vercel/ai) | TypeScript AI application toolkit | Integrate model interactions into a web app |

### Evaluation, observability and local inference

| Project | Purpose | When to explore it |
|---|---|---|
| [Langfuse](https://github.com/langfuse/langfuse) | Tracing and evaluation | Locate costs and failures across agent steps |
| [Promptfoo](https://github.com/promptfoo/promptfoo) | Prompt and application evaluation | Compare models on the same sample set |
| [Ollama](https://github.com/ollama/ollama) | Model runtime | Try running models on your own machine |
| [vLLM](https://github.com/vllm-project/vllm) | Model inference and serving engine | You have compute and operations capacity for serving models |

### Projects in older tutorials

The listed [Roo Code](https://github.com/RooCodeInc/Roo-Code) and [Flowise](https://github.com/FlowiseAI/Flowise) repositories were marked **Archived** when checked. Older tutorials can remain useful; check for a maintained successor and supported versions before starting a new deployment.

Clients handle interaction, workflows arrange steps, gateways manage requests, and model services perform inference. Installing a gateway does not provide upstream model credits. To connect an existing client, start with an [Orbis model and route](https://orbiorbi.com/pricing?utm_source=github&utm_medium=readme&utm_campaign=ai-api-guide&utm_content=en-resource-directory) and match its protocol to your client.

<a id="deployment-options"></a>
## Hosted APIs, Self-hosted Gateways & Local Models

| Approach | What you need | Main costs | When it fits |
|---|---|---|---|
| Direct model API | Provider account, key and client | Calls and integration maintenance | You mainly need one provider |
| Multi-model service such as Orbis | Account and a key for your selected route | Actual model and route usage | Compare models without operating a gateway |
| Self-hosted gateway such as LiteLLM | Server, configuration and upstream keys | Upstream calls, hosting and operations | Unify several upstream services |
| New API / One API deployment | Runtime, database and channels | Upstream calls, storage and maintenance | Operate your own model distribution system |
| Local model runtime | Suitable hardware, model files and runtime | Hardware, power and setup | Run inference on your own machine |
| Self-hosted inference service | Compute, model, serving engine and monitoring | Compute utilization and operations | You have sustained demand and serving expertise |

### Looking for an OpenRouter alternative?

Define what you want to replace: a shared balance, model selection, a protocol, a lower-cost route or management of your existing keys. List the endpoints and features your application uses before changing providers. The same model name does not guarantee an identical request contract.

For inexpensive model access, start with [Orbis pricing](#why-orbis) and compare cost per completed task. For managing upstream keys you already own, explore the [gateway directory](#resource-directory). You can also combine a gateway with a hosted model service.

### Is a self-hosted gateway cheaper?

Calculate `upstream inference + server + logs and storage + maintenance time`. A gateway helps manage access; it does not automatically reduce upstream rates. Compare actual hosted-service bills for occasional use, and assess operational benefits when a team needs shared access policies or routing.

<a id="request-examples"></a>
## Minimal Requests: Python, JavaScript & cURL

These are **generic Chat Completions templates**, not live-tested configurations for every Orbis route. Copy the Base URL, key and model ID from a route supporting this protocol. `AI_BASE_URL` must include its required API prefix; the examples append only `/chat/completions`.

Set `AI_BASE_URL`, `AI_API_KEY` and `AI_MODEL` in your local environment. Keep keys out of browser code, repositories and screenshots. The examples surface errors and do not automatically retry.

### Python standard library

No SDK is required. Save as `request.py`, configure the environment variables and run `python3 request.py`.

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

Check the returned `choices` and `usage`. On a 404, inspect the final path and model ID instead of blindly appending another `/v1`.

### Server-side JavaScript

Use a Node.js runtime with built-in `fetch`. Save as `request.mjs` and run `node request.mjs` on your server or local machine.

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

### cURL: inspect the raw HTTP response

Requires `curl` and `jq`. Building JSON with `jq` preserves the model ID as a JSON string.

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

### Beyond text chat

| Feature | What changes | What to verify |
|---|---|---|
| Streaming | Stream requests and incremental event parsing | Content, termination and mid-stream errors |
| Tool calling | Tool definitions, permitted execution and returned results | A full call-and-result round trip |
| Structured output | Protocol constraints and local validation | Required fields and types |
| Vision | Route-supported image message format | Correct answers about the supplied image |
| Responses / Messages | Endpoint, payload and parser | A complete request through the new protocol |

<a id="budget-playbook"></a>
## Low-cost API Budget Playbook

These examples use the listed **DeepSeek V4.1 Flash Orbis Exclusive** quote: ¥0.05 / 1M ordinary input tokens and ¥0.20 / 1M output tokens. Workloads are hypothetical; calculations exclude caching and additional billing items. They are not throughput or task-quality guarantees.

| Workload | Ordinary input / request | Output / request | Estimated request cost | 1,000 requests |
|---|---:|---:|---:|---:|
| Classification and tagging | 1,000 | 100 | ¥0.00007 | ¥0.07 |
| Short translation | 2,000 | 1,000 | ¥0.00030 | ¥0.30 |
| Document summary | 20,000 | 2,000 | ¥0.00140 | ¥1.40 |
| Longer code question | 40,000 | 5,000 | ¥0.00300 | ¥3.00 |

### Reduce agent, RAG and coding costs

| Cost driver | First adjustment | Watch for |
|---|---|---|
| Repeated conversation history | Retain relevant history and shorten old tool outputs | Lost constraints or facts |
| Too many retrieved documents | Deduplicate and select relevant passages | Missing evidence needed for the answer |
| Expensive models for every task | Separate simple classification from difficult reasoning | Completion rate, not just token price |
| Unbounded agent loops | Limit steps, time and spend | Explicit incomplete status when limits are reached |
| Overlong output | Specify useful format and length | Truncation of necessary content |
| Repeated failed requests | Classify errors and bound retries | Retrying permission or malformed-request errors |
| Misunderstood cache pricing | Track ordinary input, cache reads and writes separately | Actual hit rate and bill changes |

### Price versus cost per completed task

In a hypothetical comparison, model A costs ¥0.01 per attempt and completes 10 tasks in 20 attempts: ¥0.20 total, or ¥0.02 per completed task. Model B costs ¥0.015 per attempt and completes the same tasks in 10 attempts: ¥0.15 total, or ¥0.015 per completed task. Lower request prices can be offset by failures and retries.

Record total spend, completed tasks, completion time and manual corrections. Choose the least expensive route that meets your task's acceptance criteria.

<a id="workflow-recipes"></a>
## Practical Workflow Recipes

### Dify document Q&A

Documents → chunks → embeddings → retrieval → optional reranking → generated answers. A chat-model key does not automatically include embeddings or reranking. Start with one short document, inspect retrieved passages, then check answer citations before importing more data.

Separate ingestion costs from per-question retrieval and generation costs. Changing embedding models may require checking dimensions and rebuilding the index.

### n8n batch summarization

Read records → prepare each input → call the model → validate output → save results. Assign stable record IDs and persist success/failure status. Skip completed items when resuming. Start with low concurrency and adjust to observed rate limits instead of sending the entire dataset simultaneously.

### Coding agents

Define the task → read relevant files → propose edits → execute permitted operations → run project checks. Use one small fix to validate editing and tool calls before expanding scope. Budget for every turn, file and tool output, not just the initial instruction.

### Translation and extraction

Preserve an ID for each input and specify terminology and output fields. Track parsing failures, missing items and incorrect content separately. Test varied input lengths before a batch so one oversized item does not derail the whole run.

### Multimodal tasks

Distinguish image understanding from image generation, and speech recognition from speech synthesis. Protocols and billing units can differ. Persist asynchronous task IDs and verify final status and accessible outputs; an accepted request is not a completed generation.

<a id="agent-mcp"></a>
## LLM APIs, Agents & MCP

```text
User task
  → Client or agent: arrange context and choose the next step
    → LLM API: generate content or tool requests
    → Tool connection: read files, retrieve data, perform permitted actions
      → MCP server: expose tools or resources through a shared interface
  → Return the result and record calls and costs
```

MCP connects tools and resources; it is not model credit or a guarantee of agent compatibility. A model's tool request still needs application-side validation, execution and a returned result.

| Question | Distinction |
|---|---|
| Does buying API access give me an agent? | An agent also needs a task loop, tools and state |
| Is an MCP server a model relay? | MCP exposes tools/resources; a model gateway manages model requests |
| Has a tool executed when a model requests it? | No; the application must carry out the permitted operation |
| Can any chat model power a coding agent? | Check tool arguments, context, streaming and client protocols |
| Does workflow software include inference? | Check software licensing and model usage charges separately |

<a id="extended-faq"></a>
## More API Questions

### Can an inexpensive API work with Claude Code, Codex or Cursor?

The route must match the client's protocol, authentication and required features. Try one small task. A working chat feature does not establish that agents, completion and other features use the same custom API.

### What are an API Key, Base URL and model ID?

The key authenticates access; the Base URL identifies the service entry point; the model ID selects the requested model. Use values from the same connection instructions. A display name may differ from the invocation ID.

### Why does a listed model fail when called?

Discovery does not establish call permissions. Check the key's group, balance, route status and requested endpoint. Retain the error type and request ID instead of repeatedly refreshing the model list.

### How many words or Chinese characters are in 1M tokens?

There is no fixed conversion. Tokenizers, languages, code and symbols differ. Estimate from representative samples and actual usage rather than equating tokens with words or characters.

### Is a free API suitable for production?

Check reset periods, limits, permitted use and expiry. Trial credits can validate a flow, but budget for post-trial rates and explicitly handle exhausted credits.

### Is streaming cheaper?

Streaming changes delivery, not necessarily generation volume. Costs depend on usage and billing rules. Check whether cancelling stops upstream generation and how partial responses are billed.

### Can an OpenAI-compatible endpoint call Claude or Gemini?

Only when the service exposes those models through that protocol. Conversion can affect tools, images, reasoning fields or other features. Test what your application actually uses.

### Does a model automatically search the web?

Ordinary text requests do not imply web access. The service must expose an appropriate tool, or your application must retrieve material before generation. A recent date in an answer is not evidence of a search.

### Why do long conversations cost more?

Clients often resend conversation history, including tool outputs. Inspect input usage per turn and retain relevant history without dropping important constraints.

### Should everyone share one key?

Check platform rules and permissions. Separate credentials make attribution and revocation easier. Never expose a primary key in browser-side code.

### Does local inference remove all costs?

It may remove external per-token charges, but hardware, compute, power and maintenance remain. Compare identical workload and quality requirements, including idle capacity.

### What makes a useful support report?

Include time, client version, model ID, route, endpoint, error code and a redacted minimal request. Add a request ID if available. Exclude keys and private documents; use the [Issue templates](https://github.com/welsir/ai-api-guide/issues/new/choose).

<a id="glossary"></a>
## Glossary

| Term | Meaning | Why it matters |
|---|---|---|
| API Key | Authentication credential | Permissions and cost attribution |
| Base URL | Service entry address | Incorrect path construction can cause 404s |
| Model ID | Invocation identifier | Display names may not be callable IDs |
| Token | Model processing unit | Word count does not equal billed usage |
| Context window | Context capacity | Limits supplied material and history |
| Output limit | Maximum output size | Different from context capacity |
| Streaming / SSE | Incremental event delivery | Requires completion and error handling |
| TTFT | Time to first token | Wait before output begins |
| Tokens per second | Output rate | Different from total task speed |
| RPM / TPM | Requests / tokens per minute | Distinct limits can apply |
| Concurrency | Simultaneous requests | Different from requests per minute |
| Prompt cache | Reuse of processed input | Reads, writes and misses may differ in price |
| Tool calling | Structured action request | Application execution is still needed |
| Structured output | Constrained response shape | Business correctness still needs validation |
| Embedding | Content represented as vectors | Model changes can affect indexes |
| Rerank | Reordering candidate results | Changes evidence supplied to the model |
| RAG | Retrieve material before generation | Retrieval and answer quality both matter |
| Agent | Model, tools and state for a task | One task may involve many calls |
| MCP | Tool and resource connection protocol | Not a model API or inference credit |
| BYOK | Bring your own key | Upstream charges generally still apply |
| Fallback | Alternative handling after failure | Model, route and billing changes should be explicit |
| Observability | Inspecting calls, errors and costs | Helps explain slow or expensive tasks |

## Verification and maintenance

Content reviewed: **2026-10-19**. This first edition provides selection and configuration guidance. It does not publish completed route-by-route compatibility tests or a measured performance leaderboard. See the [verification method](docs/verification.md), [contribution guide](CONTRIBUTING.md) and [changelog](CHANGELOG.md).

Report reproducible problems using [Issues](https://github.com/welsir/ai-api-guide/issues/new/choose). Remove keys, personal data and sensitive prompts first.

Orbis maintains this guide and provides a commercial API service. No affiliation or endorsement by the named model vendors or client projects is implied. Outbound Orbis links use UTM parameters to distinguish referral sources; they contain no API keys. Original content is available under the [MIT License](LICENSE).
