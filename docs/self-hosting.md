# Self-hosting Kortix, the open-source AI Management System

Kortix is open source, and you can run the whole platform on your own infrastructure with one Docker Compose stack. Self-hosting keeps accounts, projects, sessions, agents, skills, connectors, secrets, change requests and the audit record inside your own network. The path from a bare host to a first merged change request is a handful of steps: install the CLI, point DNS, start the stack, scaffold a project, and run a session.

## What the self-hosted stack runs

Self-hosting runs the same product surface as the cloud: accounts, projects, sessions, agents, skills, connectors, channels, triggers, secrets, change requests and the audit record. The stack is one Docker Compose deployment with the frontend, the API, the LLM gateway and the Supabase distribution. Agent sessions run on a separate sandbox provider rather than on this stack. Daytona is the default provider, and Platinum and E2B are also supported. Kortix is open source (Elastic License 2.0): self-host, read and modify the code. The full reference is at [kortix.com/docs/host](https://kortix.com/docs/host).

## Prerequisites

You need a Linux host or VPS for the one-shot bootstrap, Docker, a domain with a DNS record for the domain and for `api.<domain>`, and ports 80 and 443 open so the bundled Caddy proxy can issue a TLS certificate. You also need a sandbox provider key, because agent sessions boot on a separate provider. The one-shot bootstrap is Linux only. On another operating system, install the CLI and use the manual path below.

## Install the CLI

```
curl -fsSL https://kortix.com/install | bash
```

The installer downloads a prebuilt binary for macOS and Linux. Windows is not supported.

## Bring the stack up

On a bare Linux box, the one-shot bootstrap installs Docker, installs the CLI, and starts the stack. The manual path is three steps. Install the CLI first. Then create the DNS records and initialize:

```
kortix self-host init --domain kortix.example.com
```

Then start the stack:

```
kortix self-host start
```

Check progress with `kortix self-host status`, `kortix self-host logs` and `kortix self-host doctor`. To evaluate with no domain, initialize with a Cloudflare tunnel instead:

```
kortix self-host init --tunnel cloudflare
kortix self-host start
```

The tunnel URL changes on every restart, so use that mode for evaluation rather than production. After the stack starts, set your sandbox provider key:

```
kortix self-host configure
```

`configure` prompts for the sandbox provider key and an optional managed-git token. Sign up in the dashboard, then connect your own LLM key in the model picker. Self-hosted instances use your own key by default.

## A first project

`kortix init` scaffolds a project directory with a starter manifest:

```
kortix init acme-co
cd acme-co
```

The project is a git repo plus `kortix.yaml`, and the layout is the company:

```
acme-co/
├─ kortix.yaml      connectors, rules, triggers, machine image
├─ agents/          who does the work, in markdown
├─ skills/          how the company does a job
└─ memory/          what it has learned so far
```

`kortix.yaml` declares `kortix_version: 2` and runs the OpenCode harness. Agents and skills are markdown files. Memory is files that accumulate. Connectors, rules, triggers and the machine image are declared in `kortix.yaml`, so any change is a diff you can review and roll back.

## Run a first session

Sessions run inside your own git repo. Start one with a prompt:

```
kortix sessions new --prompt "Summarize this week's commits and open a change request" --wait
```

Each session runs in an isolated sandbox on its own branch, and the session id, sandbox id and branch name are the same string. List running sessions with `kortix sessions ls`, attach with `kortix connect`, or chat with `kortix sessions chat`. When the agent has commits ready, it opens a change request:

```
kortix cr ls
kortix cr diff 1
kortix cr merge 1
```

Merge is deny-by-default for agents, so a person reads the diff before it lands.

## Where memory and connectors live

Memory lives as files under `memory/` in the project repo, so it accumulates with the work and is versioned with the code. Connectors, rules and triggers are declared in `kortix.yaml`. Wire up the tools once, then scope which agent may touch which one. Kortix reaches 3,000+ apps plus any MCP, OpenAPI, Postman, GraphQL or HTTP API. Connector credentials are brokered server-side and never enter the session machine. Set each tool call to allow, ask or block, down to the arguments of the call, and an ask holds the call until a person approves it.

## Updates and backups

Each instance updates itself automatically. Pin an exact version with `kortix self-host update --tag <version>`, or turn the updater off. Kortix has no separate backup system. Back up the two data directories under `~/.config/kortix/self-host/<instance>/`, `volumes/db/data` and `volumes/storage`, plus the instance `.env` file, before any destructive command.

## Self-host or managed cloud

Self-host when the stack and the data have to stay inside your network, in a VPC or on-prem, under your own accounts and audit trail. Use managed cloud when you want the same platform without operating it. Both run the same configuration from your repo, so moving between them changes the machine, not the company.

Pricing comes from [kortix.com/pricing](https://kortix.com/pricing) (checked October 2026). Free is $0 with 200 credits a month for sandbox compute and 1 project. Team is $40 per seat per month with 2,500 credits a month per seat, pooled, up to 200 projects and 100 seats. Enterprise is custom with SAML SSO, SCIM directory sync, advanced RBAC and audit logs, and cloud, VPC or on-prem deployment. Self-hosting the code is free.

Start with the install:

```
curl -fsSL https://kortix.com/install | bash
```

Then read the [Kortix docs](https://kortix.com/docs) and [Kortix on GitHub](https://github.com/kortix-ai/suna).
