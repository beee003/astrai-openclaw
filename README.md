# astrai-openclaw

**Stop burning $100/day on OpenClaw agent inference. One config change. 40-60% savings.**

Astrai is an intelligent LLM inference router that sits between your OpenClaw agents and AI providers. It uses Bayesian learning to route each request to the optimal model/provider — balancing cost, quality, and latency automatically.

**BYOK (Bring Your Own Keys):** You keep your own provider API keys. Astrai decides which provider to use for each task, then calls the provider using YOUR key. You pay providers directly. Astrai only charges for routing intelligence. Zero risk of token drain.

## Why Astrai?

OpenClaw agents burn through tokens fast. A typical setup sends your entire conversation history with every API call. Users report spending **$25-100/day** on inference alone.

Astrai fixes this:

| | Without Astrai | With Astrai |
|---|---|---|
| **Monthly cost** | ~$2,700 | ~$890 |
| **Model selection** | Manual / fixed | Auto per task type |
| **Failover** | None | Automatic circuit breaker |
| **Privacy** | Depends on provider | PII stripped, EU routing, zero-retention mode |
| **Setup time** | N/A | 2 minutes |

## Quick Start

### 1. Get a free API key

```bash
curl -X POST https://as-trai.com/v1/signup \
  -H "Content-Type: application/json" \
  -d '{"email": "you@example.com"}'
```

Free tier: 1,000 requests/day. No credit card.

### 2. Install the OpenClaw skill

Copy the `astrai-inference-router/` folder into your OpenClaw skills directory:

```bash
git clone https://github.com/beee003/astrai-openclaw.git
cp -r astrai-openclaw/astrai-inference-router ~/.openclaw/skills/
```

### 3. Configure

Add to your `~/.openclaw/config.toml`:

```toml
[skills.astrai-inference-router]
ASTRAI_API_KEY = "your_key_here"

# BYOK: Add your provider keys (at least one required)
ANTHROPIC_API_KEY = "sk-ant-..."
OPENAI_API_KEY = "sk-..."
# GOOGLE_API_KEY = "..."

PRIVACY_MODE = "enhanced"    # standard | enhanced | max
REGION = "any"               # any | eu | us
DAILY_BUDGET = 10            # USD cap, 0 = unlimited
```

### 4. Done

All LLM calls now route through Astrai using YOUR provider keys. Check savings anytime:

```
> /astrai status

Astrai saved you $14.20 today (342 requests routed)
Provider: Anthropic 47% | OpenAI 31% | Google 22%
Quality score: 94.2% (vs 95.1% baseline)
```

## How It Works

```
OpenClaw Agent
     |
     v
[Astrai Skill]  ← intercepts LLM calls, attaches YOUR provider keys
     |
     v
[Astrai API]    ← classifies task → picks optimal model/provider
     |
     v
[Best Provider] ← calls with YOUR key (Anthropic, OpenAI, Google, etc.)
     |
     v
Response + savings headers returned to agent
```

**Smart task classification:** Astrai detects whether each request is code generation, research, creative writing, or conversation — and routes accordingly. Code tasks go to the best coding model. Simple chat goes to the cheapest fast model. You save money without losing quality.

**Bayesian learning:** The router learns from every request. It tracks which provider delivers the best quality-per-dollar for your specific usage patterns and improves over time.

## Privacy Modes

| Mode | PII Stripping | Logging | Region Lock | Data Retention |
|---|---|---|---|---|
| `standard` | Off | Full | None | 30 days |
| `enhanced` | On | Metadata only | Optional | 7 days |
| `max` | On | None | EU only | Zero |

GDPR-compliant EU routing available. Set `REGION=eu` to ensure prompts never leave European infrastructure.

## Pricing

| Plan | Price | Requests | Features |
|---|---|---|---|
| **Free** | $0/mo | 1,000/day | Smart routing, failover, basic analytics |
| **Pro** | $49/mo | Unlimited | + EU routing, PII stripping, cost alerts, full analytics |
| **Business** | $199/mo | Unlimited | + Multi-agent dashboards, compliance exports, SLA |

Even on Pro, if you save $200/mo in API costs (typical), that's a **4x ROI**.

## Supported Providers

Anthropic, OpenAI, Google (Vertex + AI Studio), Mistral, Groq, Together, Fireworks, DeepSeek, Cohere, Perplexity, and more. 150+ model aliases mapped.

## Configuration Reference

| Variable | Description | Default |
|---|---|---|
| `ASTRAI_API_KEY` | Your Astrai routing key | Required |
| `ANTHROPIC_API_KEY` | Your Anthropic key (BYOK) | — |
| `OPENAI_API_KEY` | Your OpenAI key (BYOK) | — |
| `GOOGLE_API_KEY` | Your Google AI key (BYOK) | — |
| `DEEPSEEK_API_KEY` | Your DeepSeek key (BYOK) | — |
| `MISTRAL_API_KEY` | Your Mistral key (BYOK) | — |
| `GROQ_API_KEY` | Your Groq key (BYOK) | — |
| `PRIVACY_MODE` | `standard`, `enhanced`, `max` | `enhanced` |
| `REGION` | `any`, `eu`, `us` | `any` |
| `DAILY_BUDGET` | Max daily spend in USD (0 = unlimited) | `10` |

At least one provider key is required. Astrai routes using your keys — you pay providers directly.

## Links

- **Website:** [as-trai.com](https://as-trai.com)
- **API Docs:** [as-trai.com/docs/quickstart](https://as-trai.com/docs/quickstart)
- **Issues:** [GitHub Issues](https://github.com/beee003/astrai-openclaw/issues)

## License

MIT
