# MCP Scorecard: Batch Scan of 30 Public MCP Servers

Date: `2026-04-09`  
Tool: `MCP Scorecard 1.0.0`  
Environment: `Windows`, `npx.cmd`, no API keys, no manual setup, no interactive auth

## Goal

Run a practical batch of `30` public MCP servers from different categories and different developers,
then answer one internal question:

**Is MCP Scorecard actually useful as a real infrastructure review tool, or only on curated demos?**

## Selection Method

The batch was intentionally mixed, not statistically random.

- `4` official reference servers from `modelcontextprotocol`
- `26` public registry servers from different teams and use cases
- only `stdio` servers were included
- package selection was biased toward entries with reproducible package metadata and runnable npm bins
- no secrets were provided, so auth-gated servers were tested in their default unauthenticated state

This means the batch is good for stress-testing the tool and the ecosystem, but it is **not** a
fair quality ranking of the whole MCP ecosystem.

## Executive Summary

- Attempted: `30`
- Successful scans: `16`
- Failed launches / failed initialization: `14`
- Success rate: `53.3%`
- No-env servers: `19`
- No-env success rate: `12 / 19`
- Env-required servers: `11`
- Env-required success rate without secrets: `4 / 11`
- Successful score distribution:
  - `100/100`: `7`
  - `90/100`: `7`
  - `50/100`: `1`
  - `40/100`: `1`
- Average score across successful scans: `88.75`
- Most frequent finding among successful scans: `weak_input_schema` (`7` servers)

## Top-10 Shortlist For Public Examples

This is a curated shortlist, not a pure numeric ranking.

| Server | Score | Why it is a strong example |
| --- | --- | --- |
| `@modelcontextprotocol/server-memory` | `100/100` | Clean official reference server: 100/100, meaningful tool surface, no findings under the current rules. |
| `@modelcontextprotocol/server-sequential-thinking` | `100/100` | Minimal official server with a very small clean MCP surface. |
| `ai.kawacode/mcp` | `100/100` | Larger engineering-oriented server with 17 tools and still no current findings. |
| `ai.meetlark/mcp-server` | `100/100` | Compact community product server that launches cleanly and scores cleanly. |
| `ai.rapay/mcp-server` | `100/100` | Payments-oriented server with a real capability surface and a clean score under the current rules. |
| `ai.wild-card/deepcontext` | `100/100` | Strong code-search / indexing example with a clean run and clean report. |
| `app.trustrails/server` | `100/100` | Small commerce-search example that is easy to launch and easy to explain. |
| `@modelcontextprotocol/server-everything` | `90/100` | Important official control case: broad feature coverage with only a minor ergonomics finding. |
| `capital.hove/read-only-local-mysql-mcp-server` | `90/100` | Useful database-style example showing a near-clean read-only server with one schema ergonomics issue. |
| `capital.hove/read-only-local-postgres-mcp-server` | `90/100` | Useful database-style example showing a near-clean read-only server with one schema ergonomics issue. |

Notes:

- `server-filesystem` is intentionally not in this shortlist because it is better used as a legitimate high-blast-radius example than as a clean baseline.
- The shortlist is optimized for usefulness in docs and examples, not for maximum score only.

## Result Table

| # | Server | Developer | Category | Env Required | Result | Score | Tools | Findings | Notes |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 1 | `@modelcontextprotocol/server-everything` | `modelcontextprotocol` | `reference` | `no` | `success` | `90` | `13` | `1` | weak_input_schema |
| 2 | `@modelcontextprotocol/server-memory` | `modelcontextprotocol` | `memory` | `no` | `success` | `100` | `9` | `0` | clean under current rules |
| 3 | `@modelcontextprotocol/server-filesystem` | `modelcontextprotocol` | `filesystem` | `no` | `success` | `40` | `14` | `3` | dangerous_fs_write_tool, dangerous_fs_write_tool, dangerous_fs_write_tool |
| 4 | `@modelcontextprotocol/server-sequential-thinking` | `modelcontextprotocol` | `reasoning` | `no` | `success` | `100` | `1` | `0` | clean under current rules |
| 5 | `ai.imboard/dossier` | `imboard-ai` | `workflow` | `no` | `failed` | `-` | `-` | `-` | initialize timeout |
| 6 | `ai.kawacode/mcp` | `codeawareness` | `engineering` | `no` | `success` | `100` | `17` | `0` | clean under current rules |
| 7 | `ai.meetlark/mcp-server` | `meetlark` | `scheduling` | `no` | `success` | `100` | `6` | `0` | clean under current rules |
| 8 | `ai.perplexity/mcp-server` | `perplexity` | `search` | `no` | `failed` | `-` | `-` | `-` | missing env or credentials |
| 9 | `ai.rapay/mcp-server` | `Ra-Pay-AI` | `payments` | `no` | `success` | `100` | `7` | `0` | clean under current rules |
| 10 | `ai.spritecook/generate` | `SpriteCook` | `media` | `no` | `failed` | `-` | `-` | `-` | non mcp stdout before handshake |
| 11 | `ai.telbase/deploy` | `Victor-EU` | `deployment` | `no` | `failed` | `-` | `-` | `-` | non mcp stdout before handshake |
| 12 | `ai.toolprint/hypertool-mcp` | `toolprint` | `proxy` | `no` | `failed` | `-` | `-` | `-` | initialize timeout |
| 13 | `ai.wild-card/deepcontext` | `Wildcard-Official` | `code-search` | `no` | `success` | `100` | `4` | `0` | clean under current rules |
| 14 | `app.businys/mcp-server` | `hiatys` | `business-ops` | `no` | `failed` | `-` | `-` | `-` | packaging or entrypoint problem |
| 15 | `app.trustrails/server` | `james-webdev` | `commerce-search` | `no` | `success` | `100` | `2` | `0` | clean under current rules |
| 16 | `capital.hove/read-only-local-mysql-mcp-server` | `hovecapital` | `database` | `no` | `success` | `90` | `3` | `1` | weak_input_schema |
| 17 | `capital.hove/read-only-local-postgres-mcp-server` | `hovecapital` | `database` | `no` | `success` | `90` | `3` | `1` | weak_input_schema |
| 18 | `co.promptguard/security` | `acebot712` | `security` | `no` | `failed` | `-` | `-` | `-` | missing env or credentials |
| 19 | `com.636865636b73756d/mcp-v1` | `636865636b73756d` | `verification` | `no` | `success` | `90` | `2` | `1` | weak_input_schema |
| 20 | `ai.agenttrust/mcp-server` | `agenttrust` | `identity` | `yes` | `failed` | `-` | `-` | `-` | missing env or credentials |
| 21 | `ai.fodda/mcp-server` | `fodda` | `knowledge-graph` | `yes` | `failed` | `-` | `-` | `-` | non mcp stdout before handshake |
| 22 | `ai.i18nagent/i18n-agent` | `i18n-agent` | `translation` | `yes` | `failed` | `-` | `-` | `-` | missing env or credentials |
| 23 | `ai.proofslip/mcp-server` | `Johnny-Z13` | `receipts` | `yes` | `success` | `90` | `4` | `1` | weak_input_schema |
| 24 | `ai.rolli/mcp` | `rolliinc` | `social-analytics` | `yes` | `failed` | `-` | `-` | `-` | missing env or credentials |
| 25 | `ai.social-api/socialapi` | `SocialAPI-AI` | `social-ops` | `yes` | `success` | `50` | `25` | `3` | missing_required_for_critical_fields, dangerous_http_request_tool, dangerous_http_request_tool |
| 26 | `ai.tickerapi/mcp-server` | `TickerAPI` | `market-data` | `yes` | `failed` | `-` | `-` | `-` | missing env or credentials |
| 27 | `ai.tuteliq/mcp` | `Tuteliq` | `moderation` | `yes` | `failed` | `-` | `-` | `-` | other launch failure |
| 28 | `app.qwady/borough` | `jdmay2` | `real-estate` | `yes` | `failed` | `-` | `-` | `-` | missing env or credentials |
| 29 | `co.truncus/mcp-server` | `vanmoose` | `email` | `yes` | `success` | `90` | `6` | `1` | weak_input_schema |
| 30 | `com.agentsconsultants.api/docqa` | `digitalpromptmarket-beep` | `document-qa` | `yes` | `success` | `90` | `5` | `1` | weak_input_schema |

## Typical Reasons MCP Servers Fail In CI

### 1. Missing Secrets Or Credentials

The server requires secrets or API credentials and will not start in a blind CI run without them.

Examples:

- `ai.perplexity/mcp-server`
- `ai.rolli/mcp`
- `app.qwady/borough`

### 2. Missing Runtime Configuration Beyond Secrets

Installing the package is not enough. The server also needs additional runtime configuration or a local init step.

Examples:

- `ai.agenttrust/mcp-server`
- `ai.i18nagent/i18n-agent`

### 3. Non-MCP Stdout Before Handshake

The package starts but writes setup/help/logging text to stdout before MCP JSON-RPC, breaking the stdio handshake.

Examples:

- `ai.spritecook/generate`
- `ai.telbase/deploy`
- `ai.fodda/mcp-server`

### 4. Initialize Timeout

The process starts but does not reach MCP initialize within a reasonable timeout.

Examples:

- `ai.imboard/dossier`
- `ai.toolprint/hypertool-mcp`

### 5. Packaging Or Entrypoint Problems

The registry entry exists, but the package/bin/run path is not robust enough for direct CI launch.

Examples:

- `app.businys/mcp-server`
- `co.promptguard/security`
- `ai.tickerapi/mcp-server`

## Is MCP Scorecard Useful?

**Yes, with a clear boundary.**

`MCP Scorecard` already looks useful as a serious infrastructure tool for deterministic CI review of servers that actually start over `stdio`.

It clearly surfaces risky capability surfaces, schema problems, and reviewability problems on real servers.

But the batch also shows that blind public scanning at scale is not only a scoring problem. It is also a launchability, packaging, and metadata-quality problem.

**The instrument is useful. The public-scan pipeline still needs a preflight layer.**

## What Should Happen Next

Before any public "30/100 servers" publication, add a thin preflight stage:

- classify candidates as `launchable`, `requires_auth`, `interactive`, or `broken`
- keep launch failures separate from score results
- record exact command, platform, and failure mode
- publish score tables only for servers that actually reached `initialize + tools/list`
- publish launchability tables separately
