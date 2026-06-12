# Getting started on the shared sandbox

pawaPay runs one shared sandbox account for all teams in this hackathon. Joel adds you as a user, you log in to the dashboard, and you generate your own API token.

## 1. Get added to the account

Email Joel at [joel.amoako@pawapay.co.uk](mailto:joel.amoako@pawapay.co.uk) with the address you'd like to use. He'll invite you as a user on the shared sandbox account, and you'll get an invite email from pawaPay. Accept it and set your password.

> The account lives on **[dashboard.sandbox.pawapay.io](https://dashboard.sandbox.pawapay.io)**, not the production dashboard. You can't sign up directly. The invite is the only way in.

## 2. Generate an API token

Follow the official guide:

**👉 [pawaPay docs: API tokens](https://docs.pawapay.io/dashboard/other/system_conf/api_tokens)**

The short version:

1. Open **System configuration → API tokens** in the sandbox dashboard.
2. Click **Create token**, name it (e.g. `team-<your-team-name>`), set its permissions.
3. **Copy the token now.** pawaPay shows it once.

Each team generates its own token. That way you can attribute transactions correctly, and pawaPay can revoke a single team's token without disrupting anyone else.

## 3. Use the token

Pick your build path:

- **Building something custom**: load the [Claude skill](skill/README.md) into your editor and ask it to scaffold your integration. Pass your token in the `Authorization: Bearer <token>` header on every API call.
- **Using the WooCommerce plugin**: see [plugin/README.md](plugin/README.md). Paste the token into the gateway settings and set environment to **Sandbox**.

## 4. You're ready

Make a test transaction. Use the sandbox phone numbers from the [pawaPay sandbox docs](https://docs.pawapay.io/v2/docs/sandbox) so the outcomes are deterministic.

Then read [tracking-transactions.md](tracking-transactions.md) for how to identify your own transactions on the shared account.

## Common gotchas

- **You can see everyone's transactions in the dashboard.** It's a shared account. Use the patterns in [tracking-transactions.md](tracking-transactions.md) to filter to your own.
- **Sandbox token ≠ production token.** Don't try a production token here, and don't ship sandbox tokens to a live store.
- **Lost your token?** Generate a new one and revoke the old one in the dashboard. There's no way to recover the original.
