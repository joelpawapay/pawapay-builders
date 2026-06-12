# pawaPay WooCommerce Plugin

A WooCommerce payment gateway for pawaPay, supporting mobile money deposits across all pawaPay-supported countries and providers.

> **This is optional** — only useful if you want a WordPress/WooCommerce starting point. If you're building something custom (Next.js, Flutter, mobile app, anything), ignore this folder and use the [Claude skill](../skill/README.md) instead.

## What it does

- Adds **"Mobile Money"** as a payment method at WooCommerce checkout
- Supports both **Blocks** (the new WooCommerce checkout) and the **classic shortcode** checkout
- Performs **provider prediction** from the customer's phone number — no carrier picker required for supported numbers
- Handles **on-site deposits** via the pawaPay v2 Deposits API, with polling for status
- Supports the **Wave redirect flow** where applicable
- Wires up **refunds** from the WooCommerce admin
- Supports **RFC 9421 request signing** (optional — signing key configured in admin)
- Provides an **admin settings page** for token, environment (sandbox/production), and signing key

## Prerequisites

- WordPress 6.4+ (tested on 6.9)
- WooCommerce 8.0+
- A pawaPay sandbox account and API token — see [../docs/getting-started.md](../docs/getting-started.md)

## Install

1. Download `woocommerce-pawapay.zip` from this directory, or grab the [latest GitHub Release](../../../releases/latest).
2. In WordPress admin → **Plugins → Add New → Upload Plugin** — pick the `.zip`, install, and activate.
3. Go to **WooCommerce → Settings → Payments** — you should see **"Mobile Money (pawaPay)"** in the list.
4. Click **Manage**, then:
   - Paste your sandbox API token (see [docs/getting-started.md](../docs/getting-started.md) for how to generate one)
   - Set environment to **Sandbox**
   - (Optional) Paste a signing key if you want signed requests
   - **Callback URL**: leave blank — the plugin polls for status. If you specifically need push callbacks, see [../docs/tracking-transactions.md](../docs/tracking-transactions.md) (you'll ping Joel and he'll wire one up for you).
5. Save. Add a product, go to checkout, and try a sandbox deposit.

## Configuration reference

| Setting | What to put |
| --- | --- |
| API token | Your sandbox token from the dashboard |
| Environment | `Sandbox` while building; `Production` is for live merchants only |
| Signing key | Optional. Set this if you want HTTP signatures on requests. |
| Callback URL | Leave blank for the hackathon — the plugin polls. If you need push callbacks, ping Joel; see tracking doc. |

## Testing in sandbox

In sandbox, pawaPay simulates the provider flow — you don't need a real mobile-money account. Use sandbox phone numbers from the [pawaPay testing docs](https://docs.pawapay.io/v2/docs/sandbox). The plugin will show status transitions (pending → completed/failed) in the WooCommerce order view.

## Troubleshooting

- **"Mobile Money" doesn't appear at checkout** — check the gateway is enabled in WC settings and that your store country matches a pawaPay-supported country.
- **Token rejected** — confirm you're using a sandbox token while the gateway is set to Sandbox. Production tokens won't work in sandbox and vice versa.
- **Stuck on "pending"** — pawaPay deposits resolve asynchronously; the plugin polls. If you've configured a callback URL that isn't reachable, switch to polling-only and try again. See [../docs/tracking-transactions.md](../docs/tracking-transactions.md).
- **Anything else** — ping Joel/Calixte/Julie at the event, or check the [pawaPay docs](https://docs.pawapay.io/v2/docs/welcome).

## Plugin bundle contents

The `.zip` contains:

- `woocommerce-pawapay.php` — main plugin file
- `includes/` — the gateway, REST client, Blocks support, signing, logger
- `readme.txt` — WordPress.org-style plugin readme
- `docker/` — an optional `docker-compose` setup if you want to spin up a local WP + WooCommerce environment with the plugin pre-mounted (see `docker/README.md` inside)
