---
name: astrai-inference-router
description: Route all LLM calls through Astrai for 40%+ cost savings with intelligent routing and privacy controls
version: 1.0.0
author: astrai
homepage: https://as-trai.com
tags: [inference, routing, privacy, cost-optimization, gdpr, eu, savings]
config:
  - name: ASTRAI_API_KEY
    description: Your Astrai API key (get one free at as-trai.com)
    required: true
  - name: PRIVACY_MODE
    description: Privacy level — standard (full logging), enhanced (PII stripped), max (zero retention)
    default: enhanced
  - name: REGION
    description: Region constraint — any (global), eu (Europe only), us (US only)
    default: any
  - name: DAILY_BUDGET
    description: Max daily spend in USD (0 = unlimited)
    default: 10
---

# Astrai Inference Router

Route every LLM call through Astrai's intelligent router.
Save 40%+ on API costs. Privacy controls built in.

## What it does

- **Smart routing**: Classifies each task (code, research, chat, creative) and picks the optimal model
- **Cost savings**: Bayesian learning finds the cheapest provider that meets your quality threshold
- **Auto-failover**: Circuit breaker switches providers when one goes down
- **PII protection**: Personally identifiable information stripped before reaching any provider
- **EU routing**: GDPR-compliant European-only routing with one setting
- **Budget caps**: Set daily spend limits to prevent runaway costs
- **Real-time tracking**: See exactly how much you're saving per request

## Privacy Modes

- **standard**: Full routing intelligence, normal logging
- **enhanced**: PII stripped, metadata-only logging, region enforced
- **max**: Zero data retention, EU-only, all PII stripped, no prompt logging

## Setup

1. Get a free API key at [as-trai.com](https://as-trai.com)
2. Set `ASTRAI_API_KEY` in skill config
3. Choose your privacy mode
4. Done — all LLM calls now route through Astrai

## Commands

- `/astrai status` — View savings summary and routing stats
- `/astrai budget` — Check remaining daily budget
- `/astrai privacy` — Show current privacy mode and region

## Pricing

- **Free**: 1,000 requests/day, smart routing, failover
- **Pro** ($49/mo): Unlimited requests, EU routing, PII stripping, analytics
- **Business** ($199/mo): Multi-agent dashboards, compliance exports, SLA
