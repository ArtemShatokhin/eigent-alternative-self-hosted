# Kortix: self-host the open-source Eigent alternative

> Kortix is open source, and this is the setup guide for running it yourself as an alternative to Eigent's desktop Cowork app.

Kortix is open source, and this repository shows a team how to run it on its own infrastructure when it wants an open-source alternative to Eigent. Eigent is an open-source Cowork desktop application that runs a multi-agent workforce locally on your machine, built on the CAMEL framework ([Eigent on GitHub](https://github.com/eigent-ai/eigent)). Kortix is the open-source AI Operating System: your agents, their skills, your company memory, and every connector live in one git repo you own, and each session runs on its own cloud computer. Both products are open source, and the difference that matters is where the work runs and who owns the configuration.

Self-hosting Kortix means one Docker Compose stack on a Linux box you control, with agent sessions running on a separate sandbox provider. You keep the platform, the models, and the connectors on your own infrastructure, and self-host is free. If you want to read the wider field first, the [open-source alternatives page](https://eigentalternative.com/eigent-alternatives) compares Kortix with the desktop Cowork apps row by row.

## What a team gets that a desktop app does not

Kortix runs a whole team, not a single machine. An account holds projects and people, per-resource permissions cover people and agents, and each session gets its own isolated sandbox and its own branch. People start and steer the same workforce from the web, Slack, Microsoft Teams, the CLI, or the API. Thousands of agents run in parallel on one config, and work reaches `main` through a change request a person reads as a diff.

For a security review, Kortix adds roles, groups, an audit trail, approval gates you set, SAML 2.0 single sign-on, and SCIM 2.0. It runs on Kortix Cloud, in your VPC, or on your own on-prem network. Eigent keeps its setup inside the desktop app, in Space profiles bound to the machine.

## Quickstart

Install the Kortix CLI, scaffold a project, and bring the platform up on your own box:

```bash
# 1. Install the Kortix CLI
curl -fsSL https://kortix.com/install | bash

# 2. Scaffold a project. This creates kortix.yaml plus your agents and skills
kortix init

# 3. Bring the platform up on your own box
kortix self-host start
```

For production, point an A/AAAA record at the box and open ports 80 and 443, then give the instance its domain:

```bash
kortix self-host init --domain kortix.example.com
kortix self-host start
```

To evaluate without a domain, `kortix self-host init --tunnel cloudflare` stands up a Cloudflare tunnel. The tunnel URL changes on every restart.

Start work and review what the agent proposes:

```bash
kortix sessions new --prompt "Summarize this week's commits and open a change request"
kortix cr ls
```

The full walkthrough, from host requirements to your first agent, is in [docs/self-hosting-eigent-alternative.md](docs/self-hosting-eigent-alternative.md).

## Kortix and Eigent at a glance

| Option | Open source | Where it runs | How work lands |
| --- | --- | --- | --- |
| Kortix | Yes | A cloud sandbox per session; self-host on your own box | A change request a person reviews |
| Eigent | Yes | Your desktop, local-first; a managed cloud is optional | Results on your desktop, for review |

Kortix's row comes from its own documentation. Eigent's row comes from Eigent's repository and product site, checked October 2026. The deeper comparison, on licence, self-hosting, models, and team governance, is in [docs/kortix-vs-eigent.md](docs/kortix-vs-eigent.md).

## What is in this repository

- [Self-host an open-source Eigent alternative](docs/self-hosting-eigent-alternative.md): host requirements, install, models and keys, connectors, and a first agent.
- [Kortix vs Eigent](docs/kortix-vs-eigent.md): a source-cited comparison on licence, self-hosting, models, and team governance.
- [FAQ](docs/faq.md): the questions a buyer asks before moving off a desktop Cowork app.

## Where to go next

- Read the live self-hosting guide at [eigentalternative.com/self-hosting-eigent-alternative](https://eigentalternative.com/self-hosting-eigent-alternative).
- See the side-by-side at [eigentalternative.com/kortix-vs-eigent](https://eigentalternative.com/kortix-vs-eigent).
- [Try Kortix](https://kortix.com) on Kortix Cloud, or self-host the open-source stack for free.
- Kortix is open source: read it, fork it, audit it. The repository is [Kortix on GitHub](https://github.com/kortix-ai/suna).
