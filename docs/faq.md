# Kortix FAQ: self-hosting the open-source Eigent alternative

Kortix is open source, and these are the questions a team asks before it moves off Eigent to run Kortix itself. The short answers point to the detail in the rest of this repository.

## Is Eigent open source?

Yes. Eigent describes itself as an open-source Cowork desktop application, and its repository states the code can be downloaded, inspected, and modified under the Apache License 2.0 ([Eigent on GitHub](https://github.com/eigent-ai/eigent)). Kortix is open source as well. The two differ on where the agents run and who owns the configuration, and that difference decides the setup.

## Can I self-host Kortix, and is self-hosting free?

Yes. Kortix self-hosts as one Docker Compose stack on a Linux box you control, and self-host is free. The stack pulls its images from docker.io, so the box needs outbound internet, and the instance must be reachable so an agent's sandbox can call back. Agent sessions run on a separate sandbox provider, with Platinum as the default.

## What does a team gain from Kortix over a desktop Cowork app?

A team gets one repo that holds every agent, skill, memory file, and connector, so the setup is shared and reviewable instead of living on one machine. Each session runs on its own cloud computer, so the work continues when a laptop closes, and thousands of agents run in parallel on one config. Every change lands as a change request a person reads.

## Where do agent sessions run when I self-host Kortix?

Agent sessions run on a separate sandbox provider, not on the stack you host. Platinum is the default; Daytona remains available as a legacy fallback. Each session gets its own isolated sandbox and its own branch, and the self-hosted instance must be reachable so the sandbox can call back to it.

## Do I need a domain to self-host Kortix?

Not for evaluation. Run `kortix self-host init --tunnel cloudflare` to stand up a Cloudflare tunnel and reach the instance without a domain, though the tunnel URL changes on every restart. For production, point an A/AAAA record at the box, open ports 80 and 443, and run `kortix self-host init --domain kortix.example.com` before `kortix self-host start`.

## Can I keep using my own model keys?

Yes. Kortix is model-agnostic. Bring any model provider with your own keys, connect the ChatGPT plan you already pay for, or sign in with your OpenCode Console account for OpenCode Zen and Go. You pick the model per agent, per session, or per message, and a self-hosted instance uses your own model key.

## How is an agent's work reviewed before it lands?

Session work reaches `main` through a change request. Merge is default-deny for agents, so a person reads the diff and decides. You can list and merge change requests from the CLI with `kortix cr ls` and `kortix cr merge`. Approval gates you set decide which connector calls pause for a person before the agent continues.

## What do Kortix and Eigent cost?

Kortix self-host is free. The team plan is $40 per seat per month with 2,500 pooled credits per seat, and Free is $0 with 200 credits per month and 1 project ([kortix.com/pricing](https://kortix.com/pricing), checked October 2026). Eigent is free with your own keys or local models, then $19.99 per month for 2,000 task credits and $99.99 per month for 10,000 task credits after a 7-day trial ([eigent.ai/pricing](https://www.eigent.ai/pricing), checked October 2026).

## Where can I compare the two products?

The [Kortix vs Eigent page](https://eigentalternative.com/kortix-vs-eigent) puts licence, self-hosting, models, and team governance side by side, and the [self-hosting page](https://eigentalternative.com/self-hosting-eigent-alternative) has the setup walkthrough. This repository's own comparison is in [kortix-vs-eigent.md](kortix-vs-eigent.md).
