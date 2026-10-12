<div align="center">

```
  ██████╗ ██╗██████╗     ██╗███████╗
  ██╔══██╗██║██╔══██╗    ██║██╔════╝
  ██║  ██║██║██║  ██║    ██║███████╗
  ██║  ██║██║██║  ██║    ██║╚════██║
  ██████╔╝██║██████╔╝██╗ ██║███████║
  ╚═════╝ ╚═╝╚═════╝ ╚═╝ ╚═╝╚══════╝
```

### Identity, resolved.

**Cross-boundary identity evidence infrastructure for the open web and the autonomous agent internet.**

[![Production](https://img.shields.io/badge/Platform-Live%20Production-2ea44f?style=flat-square)](https://did.is)
[![W3C DID Core](https://img.shields.io/badge/W3C-DID%20Core%201.0%20%2F%201.1-005A9C?style=flat-square&logo=w3c&logoColor=white)](https://www.w3.org/TR/did-core/)
[![W3C VC DM](https://img.shields.io/badge/W3C-VC%20Data%20Model%202.0-005A9C?style=flat-square&logo=w3c&logoColor=white)](https://www.w3.org/TR/vc-data-model-2.0/)
[![RFC 8785 JCS](https://img.shields.io/badge/IETF-RFC%208785%20JCS-black?style=flat-square)](https://www.rfc-editor.org/rfc/rfc8785)
[![npm package](https://img.shields.io/npm/v/@didis/client.svg?style=flat-square&color=CB3837&logo=npm&logoColor=white)](https://www.npmjs.com/package/@didis/client)
[![PyPI package](https://img.shields.io/pypi/v/didis-py.svg?style=flat-square&color=3775A9&logo=pypi&logoColor=white)](https://pypi.org/project/didis-py/)
[![License: MIT](https://img.shields.io/badge/License-MIT-0969da?style=flat-square)](https://github.com/ledgerbingo/did/blob/main/LICENSE)

[**Explore Platform (did.is)**](https://did.is) &nbsp;•&nbsp; [**Interactive Showcase**](https://did.is#showcase) &nbsp;•&nbsp; [**Documentation**](https://docs.did.is) &nbsp;•&nbsp; [**TypeScript SDK**](#typescript-sdk) &nbsp;•&nbsp; [**Python SDK**](#python-sdk)

</div>

---

## 1. The Core Paradigm: Truth Over Scores

Traditional identity systems rely on opaque, synthetic "Trust Scores" ($0\text{–}100$) or ungrounded reputation badges. A single aggregated score conceals critical vulnerabilities: an identifier might possess valid cryptographic keys while its underlying web host is compromised, or a domain binding might exist without any immutable audit history.

**DID.is rejects synthetic scores entirely.**

Inspired by the FDA Nutrition Facts label, DID.is evaluates every decentralized identifier across **seven strictly orthogonal evidence dimensions**. Each dimension presents a factual, mathematically verifiable state alongside an explicit boundary of what that dimension proves—and what it does not prove.

```
┌────────────────────────────────────────────────────────────────────────────────────────┐
│                               THE NUTRITION LABEL MODEL                                │
├─────────────────────┬──────────────┬───────────────────────────────────────────────────┤
│ Evidence Dimension  │ Status State │ Grounded Boundary (What It Proves vs. Does Not)   │
├─────────────────────┼──────────────┼───────────────────────────────────────────────────┤
│ 1. Integrity        │ ESTABLISHED  │ Proves document matches identifier or hash chain. │
│                     │              │ Does not prove physical control of servers.       │
├─────────────────────┼──────────────┼───────────────────────────────────────────────────┤
│ 2. Keys             │ ESTABLISHED  │ Proves signing keys are well-formed on curves.    │
│                     │              │ Does not prove real-world corporate identity.     │
├─────────────────────┼──────────────┼───────────────────────────────────────────────────┤
│ 3. Control          │ INDEPENDENT  │ Proves update mechanism rules (key vs. hosting).  │
│                     │              │ Does not guarantee DNS infrastructure immunity.   │
├─────────────────────┼──────────────┼───────────────────────────────────────────────────┤
│ 4. Origin           │ ESTABLISHED  │ Proves bidirectional DIF domain configuration.    │
│                     │              │ Does not prove government corporate registration. │
├─────────────────────┼──────────────┼───────────────────────────────────────────────────┤
│ 5. Transport        │ ESTABLISHED  │ Proves TLS leaf cert validity against WebPKI.     │
│                     │              │ Does not guarantee upstream operational uptime.   │
├─────────────────────┼──────────────┼───────────────────────────────────────────────────┤
│ 6. History          │ VERIFIABLE   │ Proves immutable state-transition log (did:webvh).│
│                     │              │ Does not guarantee future human conduct.          │
├─────────────────────┼──────────────┼───────────────────────────────────────────────────┤
│ 7. Organization     │ UNCONFIRMED  │ Proves real-world legal identity is unlinked.     │
│                     │              │ Prevents false assumptions of corporate backing.  │
└─────────────────────┴──────────────┴───────────────────────────────────────────────────┘
```

> **Core Philosophy:** *Every claim is tied to raw mathematical proof and audited execution. Never an arbitrary score.*

---

## 2. High-Level Ecosystem Architecture

DID.is operates as an end-to-end cryptographic evidence pipeline, connecting raw decentralized identifiers to real-time AI agent execution gates:

```
┌─────────────────────────────────────────────────────────────────────────────────────────────────┐
│                                    DID.is RESOLUTION & TRUST ENGINE                             │
└─────────────────────────────────────────────────────────────────────────────────────────────────┘
                                                 │
                                 1. UNIVERSAL IDENTIFIER INGRESS
                                                 │
            ┌──────────────────┬─────────────────┴────────────────┬──────────────────┐
            ▼                  ▼                                  ▼                  ▼
     did:key (Ed25519)   did:web (Domain)               did:webvh (Verifiable)  did:jwk (RFC 7517)
     Curve point math    Leaf TLS & DIF linkage         SCID hash-chain log     RFC 7638 thumbprint
            │                  │                                  │                  │
            └──────────────────┴─────────────────┬────────────────┴──────────────────┘
                                                 │
                                2. DETERMINISTIC CRYPTOGRAPHIC CORE
                                                 │
                        ├── RFC 8785 JSON Canonicalization Scheme (JCS)
                        ├── Serde-Level JSON Duplicate Key Collision Guard
                        ├── Hardened Egress Client (SafeHttpClient DNS Pinning)
                        └── Deterministic Offline Context Catalog (Zero Remote @context)
                                                 │
                                 3. ORTHOGONAL EVIDENCE DOSSIER
                                                 │
            ┌────────────────────────────────────┼───────────────────────────────────┐
            ▼                                    ▼                                   ▼
    7 Evidence Dimensions              Forensic Evidence DAG               Telemetry & Tracing
    Integrity · Keys · Control         Directional nodes & edges           Microsecond execution spans
    Origin · Transport · History       Interactive forensic audit          Real-time SSE event stream
            │                                    │                                   │
            └────────────────────────────────────┴───────────────────────────────────┘
                                                 │
                              4. RUNTIME VERIFICATION & TRUST ENGINES
                                                 │
            ┌────────────────────────────────────┼───────────────────────────────────┐
            ▼                                    ▼                                   ▼
   Verifiable Credentials               Declarative Policies                Agent Trust & Delegation
   • Data Integrity (eddsa-jcs-2022)    • Bounded rule evaluation           • Model Context Protocol (MCP)
   • VC-JOSE / VC-JWT DM 2.0/1.1        • Strict cryptosuite gating         • A2A Protocol Agent Cards
   • Fail-Closed Status List v1.0       • Min-key-bits & TLS lifetimes      • Delegation Receipt v1 Chaining
            │                                    │                                   │
            └────────────────────────────────────┴───────────────────────────────────┘
                                                 │
                               5. CONSUMPTION INTERFACES & SDKS
                                                 │
              ├── Official Web Application (https://did.is)
              ├── One-Line AI Agent Security Middleware (withDidisGuard / @didis_guard)
              ├── TypeScript SDK (@didis/client) & Python SDK (didis-py)
              └── Standalone Embedded CLI (didis)
```

---

## 3. Developer Quickstart (Under 60 Seconds)

Resolve any decentralized identifier and audit its cryptographic evidence with zero initial setup:

### cURL

```bash
# 1. Resolve an Ed25519 did:key (Pure curve point derivation)
curl -s "https://did.is/api/v1/resolve/did:key:z6MkhaXgBZDvotDkL5257faiztiGiC2QtKLGpbnnEGta2doK" | jq .verdict

# 2. Resolve a domain-bound did:web with TLS leaf inspection & DIF domain linkage
curl -s "https://did.is/api/v1/resolve/did:web:identity.foundation" | jq '{
  outcome: .verdict.outcome,
  headline: .verdict.headline,
  dimensions: [.dimensions[] | {id, state, statement}]
}'

# 3. W3C Standard DID Resolution v1 (Candidate Recommendation Draft)
curl -s -H "Accept: application/did-resolution" \
  "https://did.is/api/1.0/identifiers/did:web:identity.foundation" | jq .didDocument
```

---

### TypeScript SDK

Install the zero-dependency client:

```bash
npm install @didis/client
```

```typescript
import { DidisClient } from "@didis/client";

const didis = new DidisClient();
const res = await didis.resolve("did:web:identity.foundation");

console.log(`Outcome:  ${res.verdict.outcome}`);
console.log(`Headline: ${res.verdict.headline}\n`);

for (const dim of res.dimensions) {
  console.log(`[${dim.state.padEnd(16)}] ${dim.label}: ${dim.statement}`);
}
```

---

### Python SDK

Install the sync/async typed package:

```bash
pip install didis-py
```

```python
from didis import DidisClient

with DidisClient() as client:
    res = client.resolve("did:web:identity.foundation")
    print(f"Outcome:  {res['verdict']['outcome']}")
    print(f"Headline: {res['verdict']['headline']}\n")

    for dim in res["dimensions"]:
        print(f"[{dim['state']:<16}] {dim['label']}: {dim['statement']}")
```

---

## 4. The One-Line AI Agent Security Guard

In modern autonomous architectures (**Vercel AI SDK**, **LangChain**, **CrewAI**, **MCP Clients**), agents discover and execute tools dynamically. Without pre-execution cryptographic verification, systems are exposed to:
1. **Tool Schema Drift & Rug-Pulls**: An upstream MCP server silently alters parameter schemas or injects prompt injections after registration.
2. **Privilege Escalation**: An ephemeral sub-agent invokes tools exceeding its granted delegation scope.
3. **Broken Delegation Chains**: An agent attempts execution with an expired or structurally invalid delegation token.

DID.is provides a high-level **fail-closed security middleware** that wraps any tool in a single line of code, verifying live MCP tool drift and cryptographic authorization prior to execution.

### TypeScript Middleware: `withDidisGuard`

```typescript
import { tool } from "ai"; // Vercel AI SDK
import { z } from "zod";
import { withDidisGuard } from "@didis/client/guard";

export const agentTools = {
  // One-line cryptographically protected tool execution
  refundPayment: withDidisGuard(
    tool({
      description: "Process a refund for an e-commerce customer transaction",
      parameters: z.object({ paymentId: z.string(), amountCents: z.number().int() }),
      execute: async ({ paymentId, amountCents }) => {
        // Business logic runs ONLY if cryptographic authorization passes
        return { success: true, paymentId, amountCents };
      },
    }),
    {
      agent: "did:key:z6MkhaXgBZDvotDkL5257faiztiGiC2QtKLGpbnnEGta2doK",
      tool: "payments:refund",
      root: "did:web:enterprise.example",
      mcpEndpoint: "https://mcp.enterprise.example/mcp" // Asserts zero tool drift
    }
  )
};
```

### Python Decorator: `@didis_guard`

```python
from crewai.tools import tool # CrewAI / LangChain
from didis.guard import didis_guard

# One-line pre-execution delegation & drift protection
@tool("Refund Transaction")
@didis_guard(
    agent="did:key:z6MkhaXgBZDvotDkL5257faiztiGiC2QtKLGpbnnEGta2doK",
    tool="payments:refund",
    root="did:web:enterprise.example",
    mcp_endpoint="https://mcp.enterprise.example/mcp"
)
def process_refund(payment_id: str, amount: float) -> str:
    """Executes a financial refund against the ledger."""
    return f"Refunded {amount} for {payment_id}"
```

---

## 5. Standards Compliance Showcase

Every algorithm, serialization pipeline, and network constraint in DID.is is strictly bound to published normative specifications:

| Specification | Standard Authority | Formal Normative Status | DID.is Implementation Scope |
| :--- | :--- | :--- | :--- |
| **W3C DID Core 1.0 / 1.1** | W3C Recommendation / CR | Normative Standard | Full abstract data model, verification relationships, strict URI ABNF parsing. |
| **W3C DID Resolution v1.0** | W3C CR Draft / CCG | Normative Standard | `/1.0/identifiers/*`, content negotiation (`application/did-resolution`), exact ID match. |
| **W3C VC Data Model 2.0** | W3C Recommendation | Normative Standard | `@context` v2, single-subject integrity constraints, VC-JOSE securing profile. |
| **W3C VC Data Integrity 1.0** | W3C Recommendation | Normative Standard | `eddsa-jcs-2022` (Ed25519) and `ecdsa-jcs-2019` (NIST P-256) over canonical JSON. |
| **W3C Bitstring Status List v1.0** | W3C Recommendation | Normative Standard | Multi-base base64url (`'u'`), 16 MiB decompression ceiling, 131,072-bit minimum sizing. |
| **IETF RFC 8785 (JCS)** | IETF Standards Track | Normative Standard | UTF-16 code unit sorting, Ryu binary64 float formatting, zero duplicate key tolerance. |
| **Model Context Protocol (MCP)** | Anthropic / MCP Org | Open Specification | Streamable HTTP (`2026-07-28` stateless & `2025-11-25` legacy), SHA-256 tool fingerprinting. |
| **Linux Foundation A2A v1.0.0** | Linux Foundation | Open Specification | `/.well-known/agent-card.json`, detached JWS signature verification, interface binding. |
| **DIF did:webvh 1.0** | Decentralized Identity Foundation | Community Specification | Verifiable history (`did.jsonl`), SHA-256 Base58BTC SCID, pre-rotation key commitments. |

---

## 6. Authoritative Public Documentation Hub

Comprehensive, deeply audited documentation is available in both English and Korean:

| Document | Primary Focus | Language Editions |
| :--- | :--- | :--- |
| **User & Customer Guide** | Visual dossier interpretation, Universal Command Bar, Credential Studio, progressive disclosure, and troubleshooting. | [English](docs/USER_GUIDE.md) |
| **Developer Guide** | Comprehensive API reference, OpenAPI contracts, TypeScript/Python SDKs, SSE streams, and middleware patterns. | [English](docs/DEVELOPER_GUIDE.md) |
| **Standards Reference** | Normative conformance matrix, cryptographic mechanics, mathematical bounds, JCS invariants, and test vectors. | [English](docs/STANDARDS_REFERENCE.md) |
| **API Contract Reference** | Machine-readable endpoint contracts, RFC 9457 Problem Details envelopes, and HTTP schemas. | [English](docs/API_CONTRACT.md) |

---

## 7. Ecosystem & Platform Resources

- **Official Web Platform:** [https://did.is](https://did.is)
- **Interactive Workbench:** [https://did.is#showcase](https://did.is#showcase)
- **Live Health & Readiness:** [https://did.is/api/health](https://did.is/api/health)
- **Security & Incident Contact:** `ai@did.is`
- **License:** Open source under the [MIT License](https://github.com/ledgerbingo/did/blob/main/LICENSE).

<br />

<div align="center">
  <sub>Built with mathematical rigor for the decentralized web and autonomous agent intelligence.</sub><br />
  <sub>Copyright © 2026 DID.is Foundation. All rights reserved.</sub>
</div>
