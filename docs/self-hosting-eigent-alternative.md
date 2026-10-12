# Self-host Kortix: the open-source alternative to Eigent

Kortix is open source, and this guide takes a team from a blank Linux box to a working platform, one step at a time, as an alternative to Eigent. Eigent is an open-source Cowork desktop application that runs its agents on your machine. Kortix is the open-source AI Operating System: your agents, their skills, your company memory, and every connector live in one git repo you own, and each session runs on its own cloud computer. The steps here run the Kortix platform yourself and keep the repo, the models, and the connectors under your control.

If you have not chosen yet, the [live self-hosting page](https://eigentalternative.com/self-hosting-eigent-alternative) frames the same stack, and [Kortix vs Eigent](kortix-vs-eigent.md) compares the two products directly.

## What you need before you start

Plan for these pieces. Kortix self-hosts as one Docker Compose stack, but a few things sit outside the box.

- A Linux box you control. This is the machine that runs the Kortix platform.
- Docker, for the Compose stack. The stack is one process set, and it has no Redis and no separate worker.
- Outbound internet. `kortix self-host start` pulls its images from docker.io, so the box needs to reach the internet.
- A reachable instance, so a session's sandbox can call back to it. Set this up before you expect agents to run.
- A domain for production, or a tunnel for evaluation. Point an A/AAAA record at the box and open ports 80 and 443, or use the Cloudflare tunnel option.
- A sandbox provider for sessions. Agent sessions run on a separate provider, not on the stack you host. The default is Daytona; Platinum and E2B are also supported.
- A git host for your project repo. GitHub connects in the dashboard under Settings, then Git.
- A model key. Bring your own, or connect the ChatGPT plan you already pay for, or sign in with your OpenCode Console account.

## Install the CLI and self-host the stack

Install the Kortix CLI. It is the entry point for every command in this guide.

```bash
curl -fsSL https://kortix.com/install | bash
```

Scaffold a project. This creates `kortix.yaml` together with your agents, skills, and runtime config. The project is a git repo, and that repo is the company: agents and skills are markdown, memory is files, and `kortix.yaml` declares the machine image, the connectors, and the triggers.

```bash
kortix init
```

Now choose where the platform runs. `kortix ship` pushes the repo and brings the whole thing live on Kortix Cloud. To run it yourself instead, bring up the self-hosted stack on your box:

```bash
kortix self-host start
```

For production, give the instance its domain first. Point an A/AAAA record at the box, open ports 80 and 443, then run:

```bash
kortix self-host init --domain kortix.example.com
kortix self-host start
```

For evaluation without a domain, use a Cloudflare tunnel. The tunnel URL changes on every restart, so treat it as temporary.

```bash
kortix self-host init --tunnel cloudflare
kortix self-host start
```

The first run of the stack asks six questions and no model key. GitHub connects later, in the dashboard under Settings, then Git.

## Connect models and your keys

Kortix is model-agnostic, and you keep your keys. Any model provider works with your own key, you can connect the ChatGPT subscription you already pay for, or you can sign in with your OpenCode Console account for OpenCode Zen and Go. On a self-hosted instance, sessions use your own model key.

Models are BYOK in the app, which is why the first run does not ask for one. You choose the model per agent, per session, or per message, so you can switch the day a better model lands without rebuilding anything. This is the same freedom Eigent offers with cloud APIs, enterprise gateways, and local models, and it is the reason model choice rarely decides between the two products ([eigent.ai](https://www.eigent.ai)).

## Wire up connectors and approval gates

Connectors are how agents reach the tools you already run. Connect them from the dashboard: 3,000+ apps in a click, plus MCP, OpenAPI, Postman, GraphQL, and raw HTTP. Connector credentials are brokered server-side and never enter the machine.

Two controls make connectors safe to hand to an agent.

- Per call rules: set each connector action to Allow, Ask, or Block, down to the arguments of each call. An Ask holds the call until a person approves it, then the agent resumes.
- Approval gates: gates you set. They are off until you set them, so decide which calls should wait for a person before agents run unattended work.

`kortix.yaml` declares the connectors and their grants. Secret values never appear in the repo.

## Start your first agent

An agent is two pieces: `agents/<name>.md` describes what it does in plain markdown, and an `agents.<name>` block in `kortix.yaml` sets its governance.

Start a session and give the agent a job:

```bash
kortix sessions new --prompt "Summarize this week's commits and open a change request"
```

Each session boots its own isolated sandbox on its own branch. The agent can install, run, and break anything, and only what it commits survives. When the work is ready, the agent opens a change request. Merge is default-deny for agents, so a person reads the diff and decides.

```bash
kortix cr ls      # review what the agent proposes
kortix cr merge   # merge once you are satisfied
kortix chat       # talk to a session's agent from your terminal
```

Give the agent a schedule so work starts with nobody present. A trigger is a cron schedule or a signed webhook, and it lives in `kortix.yaml`:

```yaml
# kortix.yaml
triggers:
  - slug: daily-digest
    type: cron
    cron: '0 0 9 * * 1-5'
    prompt: Summarize yesterday's support tickets and open a change request with the digest.
```

## Where to go next

- [Kortix vs Eigent](kortix-vs-eigent.md) for the licence, self-hosting, model, and governance comparison.
- [FAQ](faq.md) for the questions buyers ask before moving off a desktop Cowork app.
- The live [self-hosting page](https://eigentalternative.com/self-hosting-eigent-alternative) and [pricing page](https://eigentalternative.com/eigent-pricing) for the side-by-side.
- [Try Kortix](https://kortix.com) on Kortix Cloud, or keep running the open-source stack yourself.
