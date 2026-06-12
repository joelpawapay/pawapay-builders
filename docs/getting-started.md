# Getting started on the shared sandbox

Every team in this hackathon uses the **same shared sandbox account** that pawaPay has set up. You get added as a user, log in to the sandbox dashboard, and generate your own API token from there.

## 1. Get added to the account

Ping **Joel** ([joel.amoako@pawapay.co.uk](mailto:joel.amoako@pawapay.co.uk)) — over Slack or email — with the email address you'd like to use, and he'll invite you as a user on the shared sandbox account. You'll get an invite email from pawaPay; accept it and set your password.

> The account lives on **[dashboard.sandbox.pawapay.io](https://dashboard.sandbox.pawapay.io)**, not the production dashboard. Don't try to sign up directly — you need the invite.

## 2. Generate an API token

Once you're logged in, follow the official guide here:

**👉 [pawaPay docs — API tokens](https://docs.pawapay.io/dashboard/other/system_conf/api_tokens)**

In short:

1. Open **System configuration → API tokens** in the sandbox dashboard.
2. Click **Create token**, give it a name (e.g. `team-<your-team-name>`), and set its permissions.
3. **Copy the token immediately** — pawaPay only shows it to you once.

Each team should generate its **own** token — that way transactions can be attributed correctly, and a single team's token can be revoked without disrupting anyone else.

## 3. Plug the token into the plugin

- Install the plugin (see [../plugin/README.md](../plugin/README.md))
- WooCommerce → Settings → Payments → **Mobile Money (pawaPay)** → Manage
- Paste your token, set environment to **Sandbox**, save

## 4. You're ready

Make a test order. Use the sandbox phone numbers from the [pawaPay sandbox docs](https://docs.pawapay.io/v2/docs/sandbox) so transactions resolve predictably.

Then read [tracking-transactions.md](tracking-transactions.md) to figure out how you want to identify your transactions on a shared account.

## Common gotchas

- **You can see everyone's transactions in the dashboard.** That's expected — it's a shared account. Use the patterns in [tracking-transactions.md](tracking-transactions.md) to filter to your own.
- **Sandbox token ≠ production token.** Don't try a production token here, and don't ship sandbox tokens to a live store.
- **Lost your token?** Generate a new one and revoke the old one in the dashboard. No way to recover an existing token.
