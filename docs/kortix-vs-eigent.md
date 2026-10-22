# Kortix vs Eigent: the open-source platform and the open-source desktop app

Kortix is open source, and Eigent describes itself the same way. Where the two differ is where the agents run and who owns the configuration. Kortix is the open-source AI Operating System: your agents, their skills, your company memory, and every connector live in one git repo you own, and each session runs on its own cloud computer. Eigent is an open-source Cowork desktop application that runs a multi-agent workforce locally on your machine ([Eigent on GitHub](https://github.com/eigent-ai/eigent)).

## What Kortix is

Kortix is the open-source AI Operating System, built for a team rather than one machine. Your agents, their skills, your company memory, and every connector live in one git repo you own, and `kortix.yaml` declares the machine image, the connectors, and the triggers. A session boots an isolated sandbox on its own branch, does the work, and opens a change request that a person reads as a diff before it reaches `main`. The same workforce is reachable from the web, Slack, Microsoft Teams, the CLI, and the API, and a trigger can start a session on a cron schedule or a signed webhook with nobody present. Run it on Kortix Cloud, in your VPC, or on your own on-prem network, and self-host is free ([Kortix docs](https://kortix.com/docs)).

## What Eigent is

Eigent is a desktop application, and it places the agent on the machine in front of you. It is built on the CAMEL multi-agent framework, and its recommended setup is a local, standalone deployment with a local backend, local model integration, and no cloud account required ([Eigent on GitHub](https://github.com/eigent-ai/eigent)). Its product site packages agents, skills, and connectors into reusable Space profiles, keeps secrets bound locally, and returns results for you to review or send back for revisions ([eigent.ai](https://www.eigent.ai)). A managed cloud plan is offered for teams that prefer hosted infrastructure, and team features such as a shared library and centralized billing are listed as coming soon ([eigent.ai/pricing](https://www.eigent.ai/pricing)).

## Kortix vs Eigent, side by side

| | Kortix | Eigent |
| --- | --- | --- |
| Open source | Yes | Yes |
| Licence | Open source | Apache License 2.0 |
| Self-hosting | One Docker Compose stack on a box you control; self-host free | Desktop app, local-first; a self-hosted deployment is documented |
| Models | Any provider with your own keys; ChatGPT; OpenCode Console | Cloud providers, enterprise gateways, or local models; BYOK |
| Team governance | Per-resource permissions, roles, audit trail, SAML 2.0 SSO | Roles, policies, and approvals; SSO among enterprise features |

The Eigent cells come from Eigent's own repository and its product and pricing pages, checked October 2026.

## Licence

Kortix is open source: read it, fork it, audit it ([Kortix on GitHub](https://github.com/kortix-ai/suna)). Eigent is open source too, and its repository states the project is licensed under the Apache License 2.0 ([Eigent on GitHub](https://github.com/eigent-ai/eigent)). Both products let you read and modify the code. They differ in what the open code contains. In Kortix the platform, the agents, the skills, and the connectors are all files in one repo you own, so a fork keeps the whole company and its configuration. In Eigent the open code is the desktop application, and the team control features such as a shared library and centralized billing are listed as coming soon ([eigent.ai/pricing](https://www.eigent.ai/pricing)).

## Self-hosting

Kortix self-hosts as one Docker Compose stack on a Linux box you control, and self-host is free. Point an A/AAAA record at the box and open ports 80 and 443, or use a Cloudflare tunnel to evaluate without a domain. Agent sessions run on a separate sandbox provider, with Platinum as the default and Daytona as a legacy fallback. The self-hosted instance must be reachable so a sandbox can call back, and the stack pulls its images from docker.io ([Kortix docs](https://kortix.com/docs)).

Eigent's recommended setup is a local, standalone deployment. Its repository describes a local backend with a full API, local model integration through vLLM, Ollama, or LM Studio, and no cloud account required, and it also offers a self-hosted deployment for teams that want their own environment ([Eigent on GitHub](https://github.com/eigent-ai/eigent)). The difference is the shape of the machine. Eigent runs the agents on your desktop; Kortix runs each session on its own cloud computer from a repo the team shares, so a job continues after a laptop closes and a second person can read the branch.

## Models

Kortix is model-agnostic. Any model provider works with your own keys, you can connect the ChatGPT plan you already pay for, or you can sign in with your OpenCode Console account for OpenCode Zen and Go. You pick the model per agent, per session, or per message, and on a self-hosted instance the sessions use your own key ([Kortix docs](https://kortix.com/docs)).

Eigent connects cloud providers, enterprise gateways, or local models, and its free tier supports BYOK and local models ([eigent.ai/pricing](https://www.eigent.ai/pricing)). Model choice is close between the two products. The larger difference is that Kortix pins model choice to the repo and to each session, so the same agent definition can run on a different model without a rebuild.

## Team governance

Kortix puts governance in the repo and around the session. Per-resource permissions cover people and agents, with roles, groups, and an audit trail; SAML 2.0 single sign-on and SCIM 2.0 cover the account. Each session is one isolated sandbox, session work reaches `main` through a change request, and merge is default-deny for agents. Connector rules go down to the arguments of each call, and approval gates you set decide which calls wait for a person ([Kortix docs](https://kortix.com/docs)).

Eigent manages roles and access inside the app and applies governance through policies and approvals, and it reports its enterprise security and privacy controls as in progress. SSO and access control appear among its enterprise features, with local deployment offered at the enterprise tier ([eigent.ai](https://www.eigent.ai), [Eigent on GitHub](https://github.com/eigent-ai/eigent)). The two products both ask a person to approve agent output. Kortix makes that approval a git change request that a reviewer reads as a diff, and scopes automation through the same repo the whole team can inspect.

## Which team each one fits

Choose Kortix when a team, not one person, has to run the work: one repo that holds the agents, skills, memory, and connectors, sessions on their own cloud computers, and every change landing as a reviewable change request. Teams that need their own VPC or on-prem network, per-resource permissions, and SAML 2.0 SSO are the ones Kortix is built for.

Choose Eigent when you want a single Cowork app on your own machine, with local models and keys that stay on that machine.

## Where to read more

- The setup walkthrough is in [self-hosting-eigent-alternative.md](self-hosting-eigent-alternative.md).
- The live side-by-side is at [eigentalternative.com/kortix-vs-eigent](https://eigentalternative.com/kortix-vs-eigent).
- Pricing for both is at [eigentalternative.com/eigent-pricing](https://eigentalternative.com/eigent-pricing).
- [Try Kortix](https://kortix.com) on Kortix Cloud, or self-host the open-source stack for free.
