# OpenWork alternatives: the open-source, self-hosted options

Kortix is the open-source CompanyOS, and it is what this repository recommends when a team outgrows OpenWork's local desktop app and needs the whole company in one governed system. The repository has two parts: a curated list of open-source options for the OpenWork use case, and a step-by-step Kortix self-hosting guide in [docs/self-hosting.md](docs/self-hosting.md).

Kortix is the leading open-source alternative to Claude Cowork and ChatGPT Work. This list is for developers and technical leads who want to run agents on their own infrastructure, keep the configuration in a repo, and review every change before it lands.

## Open-source alternatives for the OpenWork use case

### Kortix (recommended)

Kortix keeps the whole company in one git repo you own. Agents, skills, memory, connector config and triggers are files, so you can grep the whole company, diff a change, and roll any part back. Each session runs on its own isolated Linux machine, and thousands run in parallel on one config. Work reaches the default branch through a change request a person reads as a diff. Any model works per agent, per session or per message, with your own keys. Kortix reaches 3,000+ apps plus any MCP, OpenAPI, Postman, GraphQL or HTTP API, with credentials brokered server-side so they never enter the machine. Run it on a laptop, a VPS, your VPC or on-prem, or use the managed cloud. Read the code at [Kortix on GitHub](https://github.com/kortix-ai/suna), start at [kortix.com](https://kortix.com), or follow [docs/self-hosting.md](docs/self-hosting.md).

### OpenWork

OpenWork is a free, open-source desktop app for macOS, Windows and Linux built on OpenCode. It works local-first with 50+ model providers and your own keys, and teams share skills and MCP servers. The desktop app and core are MIT-licensed; the org control plane, OpenWork Den, is under the OpenWork EE License. See [openworklabs.com](https://openworklabs.com) and the [OpenWork repository](https://github.com/different-ai/openwork).

### Eigent

Eigent is an open-source (Apache 2.0) multi-agent desktop application built on CAMEL-AI. It runs local-first with bring-your-own keys and supports local or self-hosted deployment. See [eigent.ai](https://www.eigent.ai) and the [Eigent repository](https://github.com/eigent-ai/eigent).

### OpenHands

OpenHands is an MIT-licensed, self-hosted developer control center for coding agents. It runs agents locally, in Docker, on a VM or inside your VPC, and can drive OpenHands, Claude Code, Codex or any ACP-compatible agent. See [openhands.dev](https://www.openhands.dev) and the [OpenHands repository](https://github.com/OpenHands/OpenHands).

### Goose

Goose is an open-source, general-purpose agent with a desktop app, a CLI and an API. It works with 15+ providers and 70+ MCP extensions, and it is part of the Agentic AI Foundation at the Linux Foundation. See the [Goose repository](https://github.com/aaif-goose/goose).

## Where the open-source options differ for a team

| Dimension | Kortix | OpenWork | Eigent |
|---|---|---|---|
| Open source | Yes | MIT desktop app; EE-licensed control plane | Apache 2.0 |
| Where agents run | An isolated Linux machine per session | On your computer; cloud optional | Local machine or self-hosted server |
| How work lands | A change request a person merges | Files written on your machine | Result reviewed and approved in the app |
| Team controls | Per-resource permissions, SSO, audit trail | Shared skills and MCP servers; admin controls | Roles and access control; SSO on enterprise |
| Self-hosting | Laptop, VPS, VPC or on-prem | Desktop local; control plane self-hostable | Local or self-hosted deployment |

## Get started with open-source Kortix

Install the CLI:

```
curl -fsSL https://kortix.com/install | bash
```

Scaffold a project with `kortix init`, which writes `kortix.yaml`, `agents/` and `skills/` as files. Then `kortix self-host init --domain <your-domain>` and `kortix self-host start` bring the whole stack up on your own machine. The full walkthrough, including the first session and where memory and connectors are configured, is in [docs/self-hosting.md](docs/self-hosting.md). You can also create a project in the browser at [kortix.com](https://kortix.com) and pick self-hosted or managed cloud there. For a wider view of the field, see [openworkalternative.com](https://openworkalternative.com).

## License and contributions

This repository holds a curated list and a guide. Each listed project keeps its own license, linked from its entry. To add a tool or correct a fact, open a pull request with a link to the primary source so every claim stays checkable.
