# pawaPay Builders — Cameroon Hackathon

Welcome! This is your starting kit for the **pawaPay × Mountain Hub** hackathon at PROMOTE.

Build something on top of pawaPay between Monday and Wednesday — demo it Thursday. What you build is up to you: a mobile money checkout, a payouts dashboard, a bill-splitter, a remittance flow, a crypto-on-ramp, anything you can dream up. Any language, any framework.

This repo gives you three things to make that fast:

1. **A Claude skill** ([`skill/`](skill/)) that knows the pawaPay Merchant API v2 inside out. Drop it into Claude and you've got an AI pair-programmer that can write integrations in any language — Node, Python, Go, PHP, Java, React, Flutter, whatever you prefer.
2. **A WooCommerce plugin** ([`plugin/`](plugin/)) — a pre-built WordPress payment gateway, in case you specifically want a commerce-shaped starting point rather than building from scratch. Skip this if WooCommerce isn't your thing.
3. **Onboarding docs** ([`docs/`](docs/)) for the shared sandbox account, including how to identify your transactions on it.

> 🎥 **See the skill in action**: [Loom walkthrough](https://www.loom.com/share/af99d1a8a13048a89220d21f1e001226) — the WooCommerce plugin was built end-to-end in about six prompts using the skill.

## Quick start

1. **Get sandbox access** — ping **@Joel** ([joel.amoako@pawapay.co.uk](mailto:joel.amoako@pawapay.co.uk)) to be added as a user on the shared sandbox account.
2. **Generate an API token** — once you're in, follow the [API tokens guide](https://docs.pawapay.io/dashboard/other/system_conf/api_tokens) on [dashboard.sandbox.pawapay.io](https://dashboard.sandbox.pawapay.io).
3. **Pick your build path:**
   - **Build something custom** — see [`skill/README.md`](skill/README.md) to load the Claude skill and start coding in your stack of choice.
   - **Use the WooCommerce plugin** — see [`plugin/README.md`](plugin/README.md) to install it into WordPress.
4. **Track your transactions** — the sandbox account is shared across all teams, so see [`docs/tracking-transactions.md`](docs/tracking-transactions.md) for how to identify yours.

## What's in this repo

| Path | What it is |
| --- | --- |
| `skill/` | Claude skill bundle — load it into Claude Code or Claude.ai to get pawaPay expertise in any project |
| `skill/README.md` | How to load the skill into Claude |
| `plugin/` | The pawaPay WooCommerce plugin `.zip` — optional, only if you want a WordPress-based start |
| `plugin/README.md` | How to install and configure the WooCommerce plugin |
| `docs/getting-started.md` | Sandbox onboarding: account access + token generation |
| `docs/tracking-transactions.md` | Four patterns for tracking your transactions on the shared account |
| `docs/resources.md` | Every link you'll need in one place |

## Key links

- **pawaPay docs** — https://docs.pawapay.io/v2/docs/welcome
- **Sandbox dashboard** — https://dashboard.sandbox.pawapay.io
- **API token guide** — https://docs.pawapay.io/dashboard/other/system_conf/api_tokens

> Want callbacks delivered to your service? Polling works out of the box — if you specifically need push callbacks, ping Joel and we'll wire them up for you. See [docs/tracking-transactions.md](docs/tracking-transactions.md).

## Getting help during the event

- **Sandbox access / API tokens**: email Joel — joel.amoako@pawapay.co.uk
- **At the venue**: Calixte and Julie (pawaPay), Ayuk (Mountain Hub)
- **Anything else**: check [`docs/resources.md`](docs/resources.md)

Good luck — we want to see what you build.
