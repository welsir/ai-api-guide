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

- [Client integration recipes](#client-recipes)
- [Request design and prompts](#request-design)
- [Streaming and tool calling](#streaming-tools)
- [Billing and offline calculator](#cost-ledger)
- [Troubleshooting by symptom](#failure-cases)
- [Small evaluation kit](#evaluation-kit)
- [From trial to routine use](#launch-checklist)
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

<a id="client-recipes"></a>
## Client Integration Recipes

These procedures organize an integration without assuming a particular version's menu labels. Use settings supported by your installed version, and copy the address, protocol and model ID from your selected route. Start with a short request before adding tools, images or retrieval.

### Cherry Studio: start with one minimal chat configuration

For desktop conversations across models. Project: [Cherry Studio](https://github.com/CherryHQ/cherry-studio).

1. Add a provider configuration matching the route's protocol and give it a distinct name.
2. Enter its Base URL, key and exact model ID.
3. Test a new plain-text conversation without old image or tool messages.
4. Check the result and usage before testing attachments or tools separately.

| Situation | First action |
|---|---|
| Several configurations have the same name | Label each with model, route and purpose |
| Models load but chat fails | Check endpoint, group permissions and error |
| New conversations work; old ones fail | Inspect message formats and context length |
| Costs change after switching routes | Record both rates and actual usage |

Acceptance: identify the model and route used for the request and where to inspect its cost.

### Open WebUI / LobeHub: verify backend connectivity

For a web conversation interface or multiple assistants. Projects: [Open WebUI](https://github.com/open-webui/open-webui) · [LobeHub](https://github.com/lobehub/lobehub).

1. Identify the process sending model requests: browser, local service or container.
2. Verify connectivity from that environment before configuring the connection.
3. Add one test model and send a short text message.
4. Before sharing access, check member permissions and credential visibility.

| Situation | First action |
|---|---|
| Works locally but fails in a container | Check container DNS, networking and proxy settings |
| localhost is assumed to mean the host | Identify the request process's network environment |
| Model appears but sending hangs | Check server-side requests and timeouts |
| Shared usage has no cost attribution | Separate credentials and preserve attribution |

Acceptance: a real request from the web interface completes, without full keys appearing in server logs.

### Cline / Kilo Code / Aider: verify a small coding task

Projects: [Cline](https://github.com/cline/cline) · [Kilo Code](https://github.com/Kilo-Org/kilocode) · [Aider](https://github.com/Aider-AI/aider). Select a provider configuration supported by the installed client and matching the route.

1. Prepare a bounded problem in a test project, such as fixing one function's boundary condition.
2. Include relevant files instead of sending the entire repository at the start.
3. Verify reads, edits and returned tool results; inspect the actual diff.
4. Run existing project checks and review cumulative task usage.

| Situation | First action |
|---|---|
| Answers work but editing fails | Inspect tool calls and result round trips |
| Repeated reads of the same file | Check whether tool results reach the model |
| Correct edits but no completion | Inspect stop conditions and repeated verification loops |
| Much higher costs than chat | Count code, history, tool output and every turn |

Acceptance: a reviewable code change passes checks and the task terminates. The same small task can evaluate clients such as Claude Code and Codex, but their protocols and configuration fields need separate checks.

### Dify: connect chat and retrieval separately

Project: [Dify](https://github.com/langgenius/dify). Connect generation before assembling document processing and retrieval.

1. Configure one text model in a minimal input-to-answer application.
2. Configure the required embedding service separately for a knowledge base.
3. Import a short known document and verify chunking and indexing.
4. Ask a factual question, then inspect retrieved passages and the final answer separately.

| Situation | First action |
|---|---|
| Chat works but ingestion fails | Check embeddings and document parsing |
| Empty retrieval, confident answer | Specify behavior when evidence is absent |
| Relevant passages, incorrect answer | Inspect context and instructions sent to generation |
| Old index fails after a model change | Check embedding model, dimensions and index compatibility |

Acceptance: answer an in-document question with evidence and clearly acknowledge an out-of-document question.

### n8n: process one item before scaling

Project: [n8n](https://github.com/n8n-io/n8n). Place model calls in observable processing steps.

1. Prepare one input record with a unique ID; configure credentials and the node.
2. Inspect the sent fields instead of inserting the entire upstream object into the prompt.
3. Validate response fields before writing to the destination.
4. Add a few items and observe rate limits, failure branches and recovery.

| Situation | First action |
|---|---|
| One item works; several lose results | Ensure every input has an output or failure record |
| Rerunning creates duplicate writes | Deduplicate or update using input IDs |
| Model call succeeds; next node fails | Check output structure and field mappings |
| An occasional 429 stops everything | Add bounded retries and recoverable failure states |

Acceptance: every input maps to a result or explicit error; rerunning does not duplicate completed external operations.

<a id="request-design"></a>
## Request Design & Parameters

### Define inputs, outputs and completion criteria

A checkable request states the task, source material, output shape and behavior when information is missing. Parameters cannot replace a clear task definition.

| Component | Example | Avoid |
|---|---|---|
| Task | Extract an order ID and total | Only saying “analyze this” |
| Evidence boundary | Use only the supplied text | Unrelated conversation history |
| Output shape | Return JSON with two fields | Conflicting JSON and long-prose requirements |
| Missing information | Return null if the amount is absent | Requiring an amount in every case |
| Acceptance | Fields exist and match the source | Checking only HTTP status |

### Use parameters within the route's supported scope

| Parameter concept | Purpose | Guidance |
|---|---|---|
| Output token limit | Bound generated content | Field names depend on the protocol |
| Temperature | Adjust sampling randomness | Low values do not guarantee factual or deterministic output |
| Top-p | Restrict sampling candidates | Avoid arbitrary changes to multiple sampling controls |
| Stop sequence | Stop at a specified string | Check for accidental truncation of valid content |
| Reasoning setting | Adjust reasoning behavior | Verify names, values and billing per route |
| Response format | Declare the output form | Validate structure and business meaning locally |
| Seed | Sampling control on some services | Not a cross-service consistency guarantee |
| Metadata | Associate business identifiers | Include only needed, non-sensitive information |

Remove or adjust unsupported fields explicitly instead of relying on silent ignoring. Debug with a minimal field set and add one parameter at a time.

### Structured extraction: an adaptable prompt

```text
Task: extract information from the order text below.
Use only the order text; do not infer missing information.
Return a JSON object without Markdown code fences.
Fields:
- order_id: string, or null if absent
- total: number, or null if absent
- currency: string, or null if absent

Order text:
Order A-1001, total 28.50, currency CNY.
```

Expected business result follows. If the route supports strict output constraints, also declare the field structure through its protocol.

```json
{
  "order_id": "A-1001",
  "total": 28.5,
  "currency": "CNY"
}
```

Include missing fields, multiple amounts and refunds in acceptance samples. Valid JSON can still contain the wrong amount.

### Long-document summaries: distinguish evidence from inference

```text
Summarize the supplied document in three parts:
1. Main conclusions: at most five, each with a source paragraph ID.
2. Open questions: only issues explicitly mentioned in the document.
3. Information gaps: information needed to answer but absent from the document.
Do not present inference as a source fact.
When a conclusion is unsupported, say “not provided in the document.”
```

Stable paragraph IDs make checking easier than a vague request for sources. Inspect conditions, exceptions and numbers, not only fluency.

### Translation: preserve protected content

```text
Translate the following text into English.
Preserve product names, variable names, URLs, amounts and identifiers.
Follow the glossary; translate uncovered terms using context.
Keep paragraph order with one output paragraph per input paragraph.
List uncertain terms separately; do not add facts.
```

For batches, return the input ID with each output instead of guessing correspondence from order. Retain originals for review rather than overwriting the only copy.

<a id="streaming-tools"></a>
## Streaming & Tool Calling

### Why can a stream contain text and still fail?

Network chunks, SSE events and model output are different layers. One network read may contain part of an event or several events.

| Layer | Handle | Common mistake |
|---|---|---|
| HTTP | Status, response type and timeouts | Parsing an error JSON response as SSE |
| Byte stream | Split characters and buffers | Decoding every chunk independently |
| SSE events | Boundaries and multiline data | Assuming one network chunk equals one event |
| Protocol content | Text, tool deltas, completion and errors | Processing text and dropping other events |
| Application state | Completed, cancelled or interrupted | Marking partial text as success |

Record first output, normal completion and premature closure separately. This distinguishes slow startup from long generation and interruption.

### A complete tool-call round trip

```text
1. The application declares available tools and their parameters.
2. The model returns one or more tool requests.
3. The application validates names, arguments and permissions.
4. The application executes permitted operations and retains real results.
5. It returns the call IDs and tool results in the required protocol.
6. The model answers from those results or requests another step.
7. The loop stops at completion or a budget limit.
```

A model-generated command is not execution authorization. Application permissions and confirmation rules should govern consequential actions such as deletion, payments and sending messages.

### Useful tool-call debugging records

| Field | Record | Purpose |
|---|---|---|
| task_id | Business task ID | Connect multiple turns |
| request_id | Model request ID | Match service logs |
| tool_call_id | Protocol call ID | Associate the returned result |
| tool_name | Actual tool name | Detect the wrong tool |
| argument_validation | Pass or fail | Separate generation from execution issues |
| execution_status | Succeeded, failed or not executed | Avoid treating non-execution as success |
| elapsed_ms | Tool execution time | Locate waits outside model generation |

Retain only what debugging needs. Arguments and results may contain user data; redact before public reporting.

<a id="cost-ledger"></a>
## Billing Reconciliation & Offline Estimates

### Normalize quotes and usage

| Field to check | Why it matters |
|---|---|
| Quote date and route | Identically named models can have different rates |
| Billing unit | Per-million, per-thousand and per-request rates differ |
| Ordinary input | Avoid including separately billed cache usage twice |
| Cache reads | May be a separate category or a subset of input |
| Cache writes | Check whether ordinary input charges are included |
| Output | Check the classification of reasoning usage |
| Other modalities or tools | Images, audio and search may be charged separately |
| Rounding | Displayed per-call values may differ from billing precision |

Read usage-field definitions and convert overlapping counts into non-overlapping categories before multiplying and summing. Do not add every token-looking field together.

### Python offline cost calculator

This calculates ordinary input and output only, without network access or keys. Rates come from the listed DeepSeek route; usage is hypothetical. Update prices when changing routes.

```python
from decimal import Decimal

PER_MILLION = Decimal("1000000")
INPUT_PRICE = Decimal("0.05")
OUTPUT_PRICE = Decimal("0.20")


def estimate(input_tokens, output_tokens):
    for value in (input_tokens, output_tokens):
        if type(value) is not int or value < 0:
            raise ValueError("Token counts must be non-negative integers")
    return (
        Decimal(input_tokens) * INPUT_PRICE
        + Decimal(output_tokens) * OUTPUT_PRICE
    ) / PER_MILLION


samples = [
    ("classification", 1000, 100),
    ("translation", 2000, 1000),
    ("summary", 20000, 2000),
    ("code", 40000, 5000),
]
for name, input_tokens, output_tokens in samples:
    per_request = estimate(input_tokens, output_tokens)
    per_thousand = per_request * 1000
    print(f"{name}: one=¥{per_request:.5f}, 1000=¥{per_thousand:.2f}")
```

Expected output:

```text
classification: one=¥0.00007, 1000=¥0.07
translation: one=¥0.00030, 1000=¥0.30
summary: one=¥0.00140, 1000=¥1.40
code: one=¥0.00300, 1000=¥3.00
```

### Investigating a billing difference

1. Match the same request; do not compare an entire agent task with one call.
2. Match quote date, model, route and billing unit.
3. Check for omitted caching, reasoning, tools or other modalities.
4. Check whether the client, SDK and gateway each retried separately.
5. Retain request IDs, usage and cost records before submitting a redacted report.

[Open Orbis route prices](https://orbiorbi.com/pricing?utm_source=github&utm_medium=readme&utm_campaign=ai-api-guide&utm_content=en-billing-ledger). Reconcile a few real calls before increasing spend.

<a id="failure-cases"></a>
## Troubleshooting by Symptom

### Terminal requests work, application requests fail

Compare actual requests, not just values displayed in settings.

| Compare | Possible difference |
|---|---|
| Final URL | A different prefix or endpoint is appended |
| Model ID | An alias or old model is sent |
| Authentication | A different credential source is used |
| Payload | Unsupported fields are added |
| Runtime | The process or container uses different networking |

Reduce to the same short request that worked in the terminal, then restore features one at a time.

### HTTP 200, but no usable result

Transport success still requires inspecting response content.

| Response | Next check |
|---|---|
| Task ID | Follow the asynchronous protocol to completion |
| Tool request | Execute permitted tools and return results |
| Empty output | Inspect finish reason, limits and response fields |
| Content in a different field | Parse the actual endpoint's protocol |
| Valid outer JSON, missing business fields | Mark as failed or pending under business rules |

Do not turn unexpected responses into silent empty-string success; missing batch results become difficult to detect.

### Timeouts followed by duplicate operations

A timeout does not prove the server did nothing. Generation or tool execution may already have completed when the connection breaks.

| Operation | Before retrying |
|---|---|
| Text generation | Account for potentially duplicated inference charges |
| Database write | Use a business key to prevent duplicates |
| Email or message send | Check delivery state before another attempt |
| Payment or order action | Use the business system's idempotency and query mechanisms |
| Async generation | Save the task ID instead of creating another task |

Stable operation IDs are more reliable than assuming retries are harmless.

### Where is the time going?

| Interval | Observation points |
|---|---|
| Before sending | Application queue, file reading and retrieval |
| Connection setup | DNS, network, TLS and proxies |
| Before first output | Queueing, input processing and preparation |
| During output | Output length, generation rate and buffering |
| After model response | Tools, destination writes and UI updates |

Measure the whole task as well as first-output and tool times. A long spinner alone does not identify the slow layer.

### Short text works, long text fails

| Check | Direction |
|---|---|
| Input plus reserved output | Leave capacity for output |
| History and tool messages | Remove irrelevant duplication |
| File and body limits | Distinguish byte limits from token limits |
| Gateway or client timeout | Check whether generation continues after timeout |
| Document handling | Use retrieval or chunking instead of sending everything |

Chunked summaries also need a merge-stage review to preserve conditions and conclusions spanning sections.

<a id="evaluation-kit"></a>
## Small Evaluation Kit

Prepare fixed samples so candidates process the same material. This is a task-design template, not a completed benchmark.

| Sample | Input design | Acceptance |
|---|---|---|
| Extraction | Explicit order ID and amount | Correct fields and values |
| Missing information | Remove the amount | Missing value, no invention |
| Multiple candidates | Original, discounted and paid amounts | Correct requested amount |
| Summary | Conclusion, conditions and exceptions | Conditions and exceptions retained |
| Translation | Terms, variables and numbers | Protected fields unchanged |
| Code fix | Small bug with an existing test | Passing checks and focused edits |
| Tool use | Answer requires one lookup | Uses returned data |
| RAG | Answer and paragraph IDs in the document | Correct answer and citation |
| No-answer RAG | Requested fact absent | Acknowledges missing evidence |
| Long context | Conditions in different locations | Finds and combines necessary information |

### Suggested evaluation record

```json
{
  "sample_id": "invoice-missing-total",
  "model_id": "your-model-id",
  "route": "your-route",
  "client_version": "your-client-version",
  "expected": "total is null",
  "observed": null,
  "passed": null,
  "input_tokens": null,
  "output_tokens": null,
  "elapsed_ms": null,
  "cost": null,
  "tested_at": null
}
```

`null` means untested or unrecorded, not zero cost or failure. Populate real results before aggregating so a plan is not mistaken for a test report.

### Reading the results

- Success rate: passing samples divided by completed tests, with incomplete tests listed separately.
- Completion cost: total spend including failed attempts divided by successful tasks; no finite unit cost when none succeed.
- Latency: distinguish first output from whole-task duration and retain slow requests.
- Corrections: record human review and editing effort, not only automatic pass rate.
- Scope: small samples support conclusions about those tasks, not every application.

<a id="launch-checklist"></a>
## From Trial to Routine Use

| Stage | Action | Retain |
|---|---|---|
| Selection | Choose model, route, protocol and budget | Connection details and quote date |
| Connection | One short text request | Reviewable response |
| Features | Required streaming, tools or images | Separate results per feature |
| Quality | Fixed business samples | Passing and failing cases |
| Cost | Reconcile usage and charges | Cost per task |
| Small batch | Control concurrency and handle errors | Recoverable execution records |
| Routine usage | Cost alerts and anomaly observation | Usage trends and issue records |
| Changes | Recheck key samples after upgrades or route changes | Old/new configurations and result differences |

Start on Orbis by [choosing a model and route](https://orbiorbi.com/pricing?utm_source=github&utm_medium=readme&utm_campaign=ai-api-guide&utm_content=en-launch-checklist), creating a matching key, connecting your tool and checking functionality and cost on a small task. Use inexpensive routes for tasks that meet your own acceptance criteria before increasing volume.

## Verification and maintenance

Content reviewed: **2026-10-19**. This first edition provides selection and configuration guidance. It does not publish completed route-by-route compatibility tests or a measured performance leaderboard. See the [verification method](docs/verification.md), [contribution guide](CONTRIBUTING.md) and [changelog](CHANGELOG.md).

Report reproducible problems using [Issues](https://github.com/welsir/ai-api-guide/issues/new/choose). Remove keys, personal data and sensitive prompts first.

Orbis maintains this guide and provides a commercial API service. No affiliation or endorsement by the named model vendors or client projects is implied. Outbound Orbis links use UTM parameters to distinguish referral sources; they contain no API keys. Original content is available under the [MIT License](LICENSE).
