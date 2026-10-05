# OpenWork alternatives: the open-source options compared

Kortix is open source, and for a team that needs governed agents rather than a desktop app on one laptop, it is the OpenWork alternative to pick. The open-source options for the OpenWork use case differ on where agents run, how work reaches the default branch, what controls the team has, and how each one is hosted. Those four questions decide a team deployment, and each product claim links to the project's own source.

## What OpenWork is

OpenWork is a free, open-source desktop app for macOS, Windows and Linux built on OpenCode, positioned as the open-source alternative to Claude Cowork and Codex ([openworklabs.com](https://openworklabs.com)). It works with 50+ model providers through your own API keys, a ChatGPT sign-in, or local models via Ollama, and in desktop mode your files stay on your machine. The desktop app and core are MIT-licensed. The org control plane, OpenWork Den, sits under the `ee/` directory and is under the OpenWork EE License, which needs a subscription for production use beyond its free carve-outs for organizations of up to 5 users and for evaluation ([OpenWork repository](https://github.com/different-ai/openwork)). OpenWork Cloud adds central management, and its Team plan is free for the first 5 seats, then $10 per seat per month (checked October 2026) ([openworklabs.com](https://openworklabs.com)).

## Why a desktop app changes shape for a company

A desktop app is the right unit for one person. The agent works on your files, your keys stay yours, and nothing has to leave the machine. A company adds requirements the desktop model does not cover. Several agents need to run at the same time without sharing a computer. A change needs a review step before it reaches production. Permissions need to be scoped per person, per agent and per tool. The configuration needs a home that is versioned and can be rolled back.

## Kortix

Kortix is the open-source AI Management System ([kortix.com](https://kortix.com)). The company itself is one git repo: `agents/` holds who does the work, `skills/` holds how the company does a job, `memory/` accumulates what it has learned, and `kortix.yaml` declares the connectors, rules, triggers and machine image. Every session boots its own isolated Linux machine with the repo on it, and thousands run in parallel on one config. The session id, sandbox id and branch name are the same string. Work does not touch the default branch directly. An agent commits to its branch and opens a change request, and a person reads the diff and merges, because merge is deny-by-default for agents ([Kortix on GitHub](https://github.com/kortix-ai/suna)).

Kortix reaches 3,000+ apps plus any MCP, OpenAPI, Postman, GraphQL or HTTP API. Connector credentials are brokered server-side and never enter the session machine, and each tool call can be set to allow, ask or block down to the arguments of the call. Any model works per agent, per session or per message, with your own keys. Teams get per-resource permissions for people and agents, SSO and an audit record. Kortix is open source (Elastic License 2.0): self-host, read and modify the code. Run it on a laptop, a VPS, your VPC or on-prem, or use the managed cloud. Install with `curl -fsSL https://kortix.com/install | bash`, or start at [kortix.com](https://kortix.com).

## The other open-source options

OpenWork covers the individual and small team that works from local files, with shared skills and an MCP gateway that follows you into Codex, Claude Code or Cursor ([openworklabs.com](https://openworklabs.com)).

Eigent is an open-source (Apache 2.0) multi-agent desktop application built on CAMEL-AI. It runs local-first, supports model-agnostic bring-your-own keys, MCP and skill integration, and enterprise SSO and access control, and it can run on your own infrastructure ([Eigent repository](https://github.com/eigent-ai/eigent)). Its managed cloud plans are $19.99 and $99.99 per month (checked October 2026) ([eigent.ai](https://www.eigent.ai)).

OpenHands is an MIT-licensed, self-hosted developer control center for coding agents. It runs agents locally, in Docker, on a VM or inside your VPC, can drive OpenHands, Claude Code, Codex or any ACP-compatible agent, and starts work from GitHub, Slack, Jira, Linear and schedules ([OpenHands repository](https://github.com/OpenHands/OpenHands)).

Goose is an open-source, general-purpose agent with a desktop app, a CLI and an API, built in Rust. It works with 15+ providers and 70+ MCP extensions, and it is part of the Agentic AI Foundation at the Linux Foundation ([Goose repository](https://github.com/aaif-goose/goose)).

## Side by side

| Tool | Open source | Where agents run | Work reaches main through | Team controls | Self-host | Price |
|---|---|---|---|---|---|---|
| Kortix | Yes (Elastic License 2.0) | An isolated Linux machine per session | A change request a person merges | Per-resource permissions, SSO, audit trail | Laptop, VPS, VPC or on-prem | Free to self-host or paid cloud |
| OpenWork | MIT desktop app; EE-licensed control plane | Your computer; cloud optional | Files written on your machine | Shared skills and MCP servers; admin controls | Desktop local; control plane self-hostable | Free desktop; paid cloud |
| Eigent | Apache 2.0 | Local machine or self-hosted server | Reviewed and approved in the app | Roles and access control; SSO on enterprise | Local or self-hosted deployment | Free to self-host; paid cloud |
| OpenHands | MIT core | Local, Docker, VM or your VPC | Pull request or patch the agent opens | Agent control plane for platform teams | Yes | Free to self-host; paid cloud |
| Goose | Open source (AAIF, Linux Foundation) | Your machine (desktop, CLI, API) | Edits and executes on your machine | Extensions and MCP servers per user | Local-first | Free |

## When OpenWork is the right pick

OpenWork is the better choice for a person or a small team that works from its own machines, wants files to stay local, and only needs shared skills and MCP servers across teammates. It is free to run on the desktop, and its control plane can be self-hosted when a small organization needs central management.

When the company needs agents running on cloud computers instead of your laptop, one repo that holds the whole configuration, connectors to company systems, SSO and an audit trail, and a human gate on every change, Kortix is the pick. The managed cloud removes the operations work, and self-hosting keeps the stack inside your own network.

## Get started

Install the Kortix CLI:

```
curl -fsSL https://kortix.com/install | bash
```

The step-by-step walkthrough is in [self-hosting.md](self-hosting.md). For the wider view of the field and the ownership question, see [openworkalternative.com](https://openworkalternative.com). The product lives at [kortix.com](https://kortix.com), and the code is at [Kortix on GitHub](https://github.com/kortix-ai/suna).
