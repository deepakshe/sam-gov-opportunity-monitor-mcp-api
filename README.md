# SAM.gov Opportunity & Tender Monitor MCP Server & Python API

[![Apify Store](https://img.shields.io/badge/Apify_Store-Run_on_Apify-blue?style=for-the-badge&logo=apify)](https://apify.com/deepaksheoran172/sam-gov-opportunity-monitor)
[![MCP Server](https://img.shields.io/badge/MCP-Model_Context_Protocol-purple?style=for-the-badge)](https://modelcontextprotocol.io)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg?style=for-the-badge)](https://opensource.org/licenses/MIT)
[![Hub](https://img.shields.io/badge/Live_Catalog-B2B_Scrapers_Hub-emerald?style=for-the-badge)](https://deepakshe.github.io/b2b-mcp-apify-scrapers-hub/)

> **Real-time SAM.gov federal contract opportunity and RFP tender monitor. Zero-cost public API feed. MCP Server & Python SDK.**

---

## ⚡ Instant Normalized Output (Sample JSON)

```json
[
  {
    "noticeId": "FA8650-26-R-9901",
    "title": "Autonomous Threat Defense Software System",
    "solicitationNumber": "FA865026R9901",
    "agency": "DEPARTMENT OF THE AIR FORCE",
    "postedDate": "2026-10-28",
    "responseDeadline": "2026-12-15"
  }
]
```

---

## ⚡ The Problem vs. The Solution

Navigating SAM.gov for federal contracts and RFP solicitations is notoriously clunky and slow. This automated monitor queries active US federal opportunities, NAICS codes, set-asides, and deadlines, outputting structured JSON for bidding pipelines.

- **Zero-Proxy Architecture:** Pure asynchronous execution designed for extreme speed (<50MB RAM).
- **Multi-Interface Support:** Run via pure Python SDK, cURL, Node.js fetch, n8n / Make.com workflow, or Claude / Cursor MCP Agent.
- **Production Reliable:** Backed by Apify's serverless infrastructure with 99.9% uptime SLA.

---

## 🚀 Quickstart: 1-Line cURL (Test in 2 Seconds)

```bash
curl -X POST "https://api.apify.com/v2/acts/deepaksheoran172~sam-gov-opportunity-monitor/run-sync-get-dataset-items?token=YOUR_APIFY_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{\"keywords\": \"cybersecurity software\", \"limit\": 20}'
```

---

## 🚀 Quickstart: Pure Python (Zero-Dependency)

No third-party SDKs required. Run directly with Python standard library:

```python
import json
import os
import urllib.request

APIFY_TOKEN = os.getenv("APIFY_TOKEN", "YOUR_APIFY_TOKEN")
ACTOR_URL = "https://api.apify.com/v2/acts/deepaksheoran172~sam-gov-opportunity-monitor/run-sync-get-dataset-items?token=" + APIFY_TOKEN

payload = {
  "keywords": "cybersecurity software",
  "limit": 20
}

req = urllib.request.Request(
    ACTOR_URL,
    data=json.dumps(payload).encode("utf-8"),
    headers={"Content-Type": "application/json"},
    method="POST"
)

with urllib.request.urlopen(req, timeout=120) as resp:
    results = json.loads(resp.read().decode("utf-8"))
    print(f"Retrieved {len(results)} items:")
    print(json.dumps(results[:2], indent=2))
```

---

## 🌐 Quickstart: Node.js / TypeScript

```javascript
const APIFY_TOKEN = process.env.APIFY_TOKEN || 'YOUR_APIFY_TOKEN';
const ACTOR_URL = `https://api.apify.com/v2/acts/deepaksheoran172~sam-gov-opportunity-monitor/run-sync-get-dataset-items?token=${APIFY_TOKEN}`;

const payload = {
  "keywords": "cybersecurity software",
  "limit": 20
};

async function run() {
  const res = await fetch(ACTOR_URL, {
    method: 'POST',
    headers: { 'Content-Type': 'application/json' },
    body: JSON.stringify(payload)
  });
  const items = await res.json();
  console.log(`Received ${items.length} records:`, items.slice(0, 2));
}

run().catch(console.error);
```

---

## 🤖 Claude Desktop & Cursor MCP Server Setup

Add this actor to your `claude_desktop_config.json` to allow Claude / Cursor AI agents to execute it autonomously:

```json
{
  "mcpServers": {
    "sam-gov-opportunity-monitor": {
      "command": "npx",
      "args": ["-y", "@apify/actors-mcp-server"],
      "env": {
        "APIFY_TOKEN": "YOUR_APIFY_TOKEN",
        "ACTOR_NAME": "deepaksheoran172/sam-gov-opportunity-monitor"
      }
    }
  }
}
```

---

## 🔄 n8n & Make.com Automation

A fully configured production n8n workflow template is bundled in this repository as [`workflow.json`](./workflow.json).

1. In n8n, click **Workflow** -> **Import from File...** and select `workflow.json`.
2. Provide your `APIFY_TOKEN` in the environment variables or HTTP Request node.
3. Schedule it to run daily or trigger on demand from webhooks.

---

## 📊 Output Schema Highlights

Each returned item includes normalized, RFC-compliant fields:
- `noticeId`
- `title`
- `solicitationNumber`
- `agency`
- `postedDate`
- `responseDeadline`
- `uiLink`

---

## 🏷️ Pricing & 60% Launch Discount

- **Apify Store:** Available under pay-per-result pricing with a **60% Launch Discount**.
- **Run Online:** Test it instantly on the [Apify Store Console](https://apify.com/deepaksheoran172/sam-gov-opportunity-monitor).
- **Fleet Hub:** Explore all 62 enterprise scrapers and MCP servers at [b2b-mcp-apify-scrapers-hub](https://deepakshe.github.io/b2b-mcp-apify-scrapers-hub/).

---

## 🛡️ 100% Automated Self-Service & Zero-DM Guarantee

- **Pure Self-Service:** Runs autonomously via Apify Cloud API. No sales calls, manual configuration, or onboarding tickets needed.
- **Pay-Per-Result:** Only successful output items are billed. Zero-charge on failed executions.
- **API Documentation:** For key creation, webhooks, and concurrency settings, see [Apify Docs](https://docs.apify.com/platform/actors/running/api).

---

## 📄 License

MIT License. Free for personal, commercial, and enterprise integration.
