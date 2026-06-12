# Tracking transactions on the shared sandbox

Every team uses the same sandbox account, so the dashboard and API responses will contain transactions from **all** teams. You need a way to identify yours.

There are four patterns you can mix and match. None is "the right one" — pick what fits your build.

## Option A — Tag every transaction with a participant ID (metadata)

pawaPay lets you attach arbitrary key-value metadata to a deposit. Add a unique identifier for your team on every request:

```json
{
  "depositId": "f4401bd2-1b8c-4017-...",
  "amount": "100",
  "currency": "GHS",
  "payer": { "type": "MMO", "accountDetails": { "..." } },
  "metadata": [
    { "fieldName": "team", "fieldValue": "team-orange" },
    { "fieldName": "participant", "fieldValue": "jane@example.com" }
  ]
}
```

**Why pick this:** you can filter and search in the sandbox dashboard, and it survives across deposit IDs you may not have written down.

**Caveats:** you have to remember to set it on every request. Bake it into a config so you don't forget.

If you're using the WooCommerce plugin, it doesn't set metadata for you out of the box — you'd need to add it in code (a small WP filter hook). If you're building your own integration, the skill will write the right metadata block for you when you ask. See the pawaPay [Deposits API reference](https://docs.pawapay.io/v2/api-reference/Deposits/initiate-deposit) for the schema.

## Option B — Track your own transaction UUIDs

Every deposit/payout you create has a UUID (`depositId`, `payoutId`, etc.). Log them on your side as you create them, and you'll always know which transactions are yours.

**Why pick this:** zero setup. The WooCommerce plugin already stores the pawaPay transaction ID against each order; if you're rolling your own, persist the ID in your DB the moment you generate it (the skill drills this in — it's the API's idempotency mechanism).

**Caveats:** if you lose your local log (database wipe, lost laptop), you've lost the link. Pair this with Option A for safety.

## Option C — Have pawaPay forward callbacks to your URL (optional)

If you'd rather receive status updates as push callbacks (instead of polling), pawaPay can forward them to a URL of your choice on the shared account. **Ping Joel** ([joel.amoako@pawapay.co.uk](mailto:joel.amoako@pawapay.co.uk)) with:

- Your team name
- The public URL(s) you want callbacks delivered to (deposit / payout / refund — whichever you need)

You'll get the destination URL(s) back to plug into your callback configuration.

**Why pick this:** you get real-time status updates pushed to your service without each team's URL having to be set directly on the pawaPay account.

**Caveats:** callbacks need a **publicly reachable URL** on your side (ngrok, cloudflared, or a deployed endpoint). For a hackathon demo, polling is usually less hassle.

## Option D — Poll for status (recommended default)

Just hit the pawaPay status endpoint when you need to know what happened.

```
GET https://api.sandbox.pawapay.io/v2/deposits/<depositId>
```

If you're using the WooCommerce plugin, it already polls for you on the checkout page until the deposit reaches a terminal state — no extra config. If you're building your own integration, ask the skill to wire up polling; it knows the right backoff and reconciliation pattern.

**Why pick this:** no callback URL needed, no public hostname, works behind a firewall. Easy to implement in any stack.

**Caveats:** slightly higher latency than callbacks. For a hackathon demo, that doesn't matter.

## Useful links

- [pawaPay v2 docs — welcome](https://docs.pawapay.io/v2/docs/welcome)
- [Deposits API reference](https://docs.pawapay.io/v2/api-reference/Deposits/initiate-deposit)
- [Sandbox test data](https://docs.pawapay.io/v2/docs/sandbox)
