# 📧 Custom Domain Email Guide

> The complete, beginner-friendly guide to receiving and sending email from your own domain (like `hi@yourdomain.com`) for free, using Cloudflare Email Routing and Gmail — no paid mailbox required!

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](http://makeapullrequest.com)
[![GitHub stars](https://img.shields.io/github/stars/jishnuteegala/custom-domain-email-guide?style=social)](https://github.com/jishnuteegala/custom-domain-email-guide)

## ✨ Features

- ✅ Receive email at `anything@yourdomain.com`, forwarded to your existing inbox
- ✅ Send email *as* `hi@yourdomain.com` directly from Gmail
- ✅ Completely free — no Google Workspace or paid mailbox needed
- ✅ Step-by-step instructions with exact field values
- ✅ Comprehensive troubleshooting for common issues
- ✅ Catch-all addresses, plus-addressing, and multiple aliases
- ✅ Security notes on SPF, DKIM, and app passwords

## 🚀 Quick Start

1. Move your domain's DNS to [Cloudflare](https://dash.cloudflare.com/) (free plan is fine)
2. Enable **Email Routing** and create a forwarding rule → [Part 1](#part-1-receiving-email-cloudflare-email-routing)
3. Add the address as a Gmail **"Send mail as"** alias → [Part 2](#part-2-sending-email-from-gmail)
4. Enjoy professional email on your own domain! 🎉

## 🎯 Who Is This For?

- Developers with a personal site who want a matching email address
- Anyone who owns a domain and doesn't want to pay for a mailbox
- Freelancers and indie hackers wanting a professional contact address
- People consolidating multiple addresses into one Gmail inbox

## 📖 What You'll Learn

- How email forwarding works (and its limits)
- Setting up Cloudflare Email Routing to receive mail on your domain
- Configuring Gmail to send as your custom address via SMTP
- Creating catch-all addresses and multiple aliases
- Troubleshooting delivery, verification, and "via gmail.com" issues

---

## Custom Domain Email Setup Guide

> **A comprehensive, beginner-friendly guide to receiving and sending email from your own domain using Cloudflare Email Routing and Gmail.**

## 📋 Table of Contents

- [How It Works](#how-it-works)
- [Prerequisites](#prerequisites)
- [Part 1: Receiving Email (Cloudflare Email Routing)](#part-1-receiving-email-cloudflare-email-routing)
  - [Step 1: Enable Email Routing](#step-1-enable-email-routing)
  - [Step 2: Add and Verify a Destination Address](#step-2-add-and-verify-a-destination-address)
  - [Step 3: Create a Routing Rule](#step-3-create-a-routing-rule)
  - [Step 4: Test Receiving](#step-4-test-receiving)
- [Part 2: Sending Email (from Gmail)](#part-2-sending-email-from-gmail)
  - [Step 5: Create a Google App Password](#step-5-create-a-google-app-password)
  - [Step 6: Add the Address in Gmail](#step-6-add-the-address-in-gmail)
  - [Step 7: Verify the Alias](#step-7-verify-the-alias)
  - [Step 8: Test Sending](#step-8-test-sending)
- [Optional Extras](#optional-extras)
- [Troubleshooting](#troubleshooting)
- [Limitations](#limitations)
- [Reference Values](#reference-values)
- [Security Notes](#security-notes)
- [FAQ](#faq)

---

## How It Works

There are two independent halves to email, and this guide wires each one up separately:

**Receiving** — Cloudflare Email Routing acts as a free forwarding service. It adds MX records to your domain so mail sent to `hi@yourdomain.com` is delivered to Cloudflare, which then forwards it to your existing inbox (Gmail, Outlook, anything). No mailbox is created; Cloudflare is just a relay.

**Sending** — Gmail's "Send mail as" feature lets you compose email that shows `hi@yourdomain.com` in the From field. Under the hood, Gmail sends it through its own SMTP servers (`smtp.gmail.com`), authenticated with your Google account. Your domain never needs its own mail server.

```
Incoming:  sender → MX records → Cloudflare Email Routing → your Gmail inbox
Outgoing:  your Gmail → smtp.gmail.com → recipient  (From: hi@yourdomain.com)
```

The key insight: **your domain has no mail server, and it doesn't need one.** Cloudflare handles inbound, Gmail handles outbound.

## Prerequisites

Before starting, ensure you have:

- **A domain** you own (any registrar)
- **Cloudflare managing your domain's DNS** — Email Routing requires it. If your DNS is elsewhere, [add your site to Cloudflare](https://developers.cloudflare.com/fundamentals/setup/manage-domains/add-site/) (free plan) and update your nameservers at your registrar first.
- **A Gmail account** (a regular free one is fine) for Part 2
- **2-Step Verification enabled** on your Google account (required for app passwords)

> **Note:** Part 1 (receiving) works with any destination inbox — Gmail, Outlook, Proton, etc. Part 2 (sending) is Gmail-specific; see the [FAQ](#faq) for other providers.

---

## Part 1: Receiving Email (Cloudflare Email Routing)

### Step 1: Enable Email Routing

1. Go to the [Cloudflare dashboard](https://dash.cloudflare.com/) and sign in
2. In the sidebar, go to **Compute** → **Email Service** → **Email Routing**
   - On older dashboard layouts: select your domain → **Email** → **Email Routing**
3. Select **Onboard Domain** (or **Get started**) and choose your domain
4. Cloudflare shows the DNS records it will add:
   - **MX records** — route incoming mail to Cloudflare
   - **TXT (SPF)** — authorises Cloudflare to handle mail for your domain
   - **TXT (DKIM)** — authenticates forwarded mail
5. Select **Done** — Cloudflare adds all records automatically. **You type nothing.**

> **⚠️ Warning:** If your domain already has MX records (an existing mail provider), enabling Email Routing replaces them. Only proceed if you're not already receiving mail elsewhere on this domain.

DNS changes usually take effect within 5–15 minutes for domains on Cloudflare DNS.

### Step 2: Add and Verify a Destination Address

The destination is the real inbox that will receive forwarded mail.

1. In Email Routing, open the **Destination addresses** tab
2. Enter your personal email address (e.g. `yourname@gmail.com`) and submit
3. Cloudflare sends a **verification email** to that address
4. Open it and click **Verify email address**

The address now shows as **Verified** in the dashboard.

### Step 3: Create a Routing Rule

1. In Email Routing, select your domain and open the **Routing rules** tab
2. Select **Create routing rule** (or use the **Custom addresses** form)
3. Fill in:

   | Field | Value |
   |---|---|
   | Email pattern / Custom address | `hi` (the part before the @) |
   | Action | **Send to an email** |
   | Destination | your verified personal address |

4. Select **Save**

You can create as many aliases as you like (`contact@`, `jobs@`, `newsletter@`...) — all pointing at the same destination or different ones.

### Step 4: Test Receiving

1. Send an email to `hi@yourdomain.com` **from a different account than the destination** — some providers silently discard messages that appear to come from the same account they are delivered to
2. Check the destination inbox (and the spam folder)
3. The email should arrive within seconds

✅ **Receiving is done.** Anything sent to `hi@yourdomain.com` now lands in your inbox.

---

## Part 2: Sending Email (from Gmail)

Cloudflare Email Routing is **receive-only** — it cannot send. To send *as* your custom address, add it to Gmail as a "Send mail as" alias using Gmail's own SMTP server.

### Step 5: Create a Google App Password

Gmail's SMTP requires an app password (your normal password won't work here).

1. Go to your [Google Account](https://myaccount.google.com/) → **Security**
2. Ensure **2-Step Verification** is turned on (app passwords require it)
3. Search for **"App passwords"** in the account search bar (or go to [App passwords](https://myaccount.google.com/apppasswords))
4. Enter a name like `gmail-alias` and select **Create**
5. **Copy the 16-character password** shown — you won't see it again

### Step 6: Add the Address in Gmail

1. Open Gmail → ⚙️ **Settings** → **See all settings** → **Accounts and Import** tab
2. In the **"Send mail as"** section, click **Add another email address**
3. In the popup:
   - **Name:** your name (what recipients see)
   - **Email address:** `hi@yourdomain.com`
   - Keep **"Treat as an alias"** ticked
4. Click **Next Step**
5. On the SMTP screen, enter:

   | Field | Value |
   |---|---|
   | SMTP Server | `smtp.gmail.com` |
   | Port | `587` |
   | Username | your **full Gmail address** (not the alias!) |
   | Password | the 16-character **app password** from Step 5 |
   | Secured connection | **TLS** (recommended) |

   > **⚠️ Common mistake:** Gmail pre-fills the SMTP server as `smtp.yourdomain.com` — **change it to `smtp.gmail.com`**. Your domain has no mail server; Cloudflare only forwards. The pre-filled value will fail.

6. Click **Add Account**

### Step 7: Verify the Alias

1. Gmail sends a **confirmation code** to `hi@yourdomain.com`
2. Cloudflare forwards it straight to your inbox (that's Part 1 working!)
3. Click the confirmation link in that email, or paste the code into the popup

### Step 8: Test Sending

1. Compose a new email in Gmail
2. Click the **From** field — select `hi@yourdomain.com` from the dropdown
3. Send it to another account you own and confirm it arrives showing the custom address

✅ **Done!** You can now receive and send as `hi@yourdomain.com`.

> **Tip:** In Settings → Accounts and Import → "Send mail as", you can set the alias as the **default** From address, and enable *"Reply from the same address the message was sent to"* so replies to `hi@` automatically go out as `hi@`.

---

## Optional Extras

### Catch-all address

Forward *everything* sent to your domain (any local part) to your inbox:

1. Email Routing → **Routing rules** tab
2. Enable the **Catch-all address** rule → Action: **Send to an email** → your destination

Now `anything-at-all@yourdomain.com` reaches you. Great for signing up to services with per-site addresses like `netflix@yourdomain.com`.

### Multiple aliases

Create separate rules for `contact@`, `jobs@`, `billing@` etc. Each can forward to a different destination address (each destination must be verified once).

To also *send* from an additional alias, repeat [Step 6](#step-6-add-the-address-in-gmail) for it — and **reuse the same app password**. The app password authenticates your Google account against `smtp.gmail.com`, not any particular alias, so one password covers every "Send mail as" address on that account. Only generate a new one if you've lost the original (Google never shows it again) or want per-use revocability.

### Subdomain addresses

Email Routing also works on subdomains (e.g. `hi@mail.yourdomain.com`) — add the subdomain in the Email Routing settings.

### Route to a Worker

Beyond forwarding, Cloudflare can pipe incoming email into a [Worker](https://developers.cloudflare.com/email-routing/email-workers/) for custom processing — auto-replies, filtering, webhooks. Out of scope for this guide, but good to know it exists.

---

## Troubleshooting

### Forwarded emails never arrive

- Check the **spam folder** of the destination inbox
- Confirm the destination address shows **Verified** in Cloudflare
- Confirm the routing rule status is **Active**
- Verify the MX records exist: run `nslookup -type=MX yourdomain.com` — you should see `route1/2/3.mx.cloudflare.net`
- Did you test by emailing from the destination account itself? Some providers silently drop self-forwards — **test from a different account**

### Gmail verification email (Step 7) never arrives

- This email is delivered *through* your Part 1 forwarding — so if receiving is broken, fix that first ([test receiving](#step-4-test-receiving))
- Check spam
- Click **Re-send email** in the Gmail popup

### "Authentication failed" when adding the SMTP details

- Username must be your **full Gmail address**, not the custom alias
- Password must be the **16-character app password**, not your Google password (spaces are ignored — paste it with or without them)
- App passwords require **2-Step Verification** to be enabled first
- Server must be `smtp.gmail.com`, port `587`, TLS

### Gmail pre-filled `smtp.yourdomain.com` and it fails

Expected — that server doesn't exist. Your domain has no mail server; Cloudflare only forwards inbound mail. Change the server to `smtp.gmail.com` as in [Step 6](#step-6-add-the-address-in-gmail).

### Recipients see "via gmail.com" next to my address

Some clients show this because the mail is physically sent by Gmail's servers rather than your domain's. It's cosmetic and fine for personal use. To remove it you'd need a sending provider with your own domain's DKIM (e.g. a transactional email service or a paid mailbox) — see [Limitations](#limitations).

### My emails go to recipients' spam

- Make sure you kept the SPF and DKIM TXT records Cloudflare added — don't delete them
- Avoid sending bulk mail through a Gmail alias; it's designed for normal personal volumes
- New domains have little sending reputation; this improves with normal use

### Error 522 / "address is unroutable" when others email me

- MX records may still be propagating — wait 15 minutes and retry
- Confirm Email Routing status is **Enabled** in the dashboard and no MX records were manually edited

---

## Limitations

Be aware of what this free setup does and doesn't give you:

| Capability | Status |
|---|---|
| Receive at custom domain | ✅ Forwarded to any inbox |
| Send as custom domain from Gmail | ✅ Via Gmail SMTP |
| Free | ✅ Cloudflare Email Routing and Gmail cost nothing |
| Actual mailbox on your domain | ❌ Mail lives in your Gmail account |
| IMAP/POP access at your domain | ❌ Use your Gmail credentials instead |
| "via gmail.com" hidden | ❌ Shown by some clients |
| Bulk / marketing sending | ❌ Use a proper email service |

If you outgrow this (e.g. you need a real mailbox, shared team inboxes, or your own DKIM sending), the usual next steps are Google Workspace, Zoho Mail (has a free tier), Fastmail, or Proton — your Cloudflare MX records just point at them instead.

---

## Reference Values

Quick lookup for the exact values used in this guide:

**Cloudflare routing rule**

```
Email pattern:  hi            (or any local part; enable catch-all for everything)
Action:         Send to an email
Destination:    your verified personal inbox
```

**Gmail "Send mail as" SMTP settings**

```
SMTP Server:  smtp.gmail.com
Port:         587
Username:     your-full-address@gmail.com
Password:     16-character Google app password
Security:     TLS
```

**Verify MX records are live**

```bash
nslookup -type=MX yourdomain.com
# Expect: route1.mx.cloudflare.net, route2..., route3...

nslookup -type=TXT yourdomain.com
# Expect a TXT containing: v=spf1 include:_spf.mx.cloudflare.net ~all
```

---

## Security Notes

- **App passwords bypass 2-Step Verification** — treat the 16-character password like a real password. Store it in a password manager or nowhere at all (you can always generate a new one).
- **Revoke unused app passwords** at [myaccount.google.com/apppasswords](https://myaccount.google.com/apppasswords) if you stop using the alias or suspect compromise.
- **Keep the SPF/DKIM records** Cloudflare added — removing them will hurt deliverability of forwarded mail.
- **Don't publish your destination address** — the whole point of the alias is that your real inbox stays private. Cloudflare hides it.
- Email forwarded through Cloudflare is processed by Cloudflare — read their [privacy policy](https://www.cloudflare.com/privacypolicy/) if handling sensitive mail.

---

## FAQ

### Q: Does this cost anything?
**A:** No. Cloudflare Email Routing is free (including catch-all and multiple rules), and Gmail SMTP is free. Your only cost is the domain itself.

### Q: Can I use Outlook/Proton/other providers as the destination?
**A:** Yes — Part 1 forwards to any inbox. Part 2 is Gmail-specific, but Outlook.com has a similar "connected accounts / send as" feature, and Proton supports custom domains natively on paid plans.

### Q: Can I have multiple custom addresses?
**A:** Yes. Create a routing rule per address in Cloudflare, and add each one as a separate "Send mail as" alias in Gmail if you also want to send from it. Or enable catch-all to receive everything with one rule.

### Q: Do I need a new app password for each alias?
**A:** No — reuse the same one. The app password belongs to your Google account, not to an alias: it authenticates the SMTP connection as you, whatever From address rides on it. One app password works for every "Send mail as" alias you add. Generate a fresh one only if you no longer have the original (it's shown once) or want to be able to revoke aliases' access independently.

### Q: Do I need Google Workspace?
**A:** No — that's the point of this guide. Workspace gives you a real mailbox on your domain (~£5/month); this setup gives you the same practical experience for free with minor cosmetic trade-offs.

### Q: What happens to replies?
**A:** Replies go to `hi@yourdomain.com`, which Cloudflare forwards to your inbox. With Gmail's *"Reply from the same address"* setting enabled, your reply goes back out as `hi@` too — the loop is seamless.

### Q: Will recipients see my real Gmail address?
**A:** The From header shows your custom address. Technically-minded recipients can inspect raw headers and infer Gmail was the sending server, and some clients show "via gmail.com" — but your actual Gmail address is not displayed in normal clients when "Treat as an alias" is configured correctly.

### Q: Is my domain's DNS on another provider — can I still do this?
**A:** Not directly. Email Routing requires Cloudflare to be your authoritative DNS. Moving DNS to Cloudflare is free and doesn't require transferring your domain registration.

### Q: Can I send from my phone's Gmail app?
**A:** Yes — aliases configured in Gmail on the web sync to the mobile apps. Tap the From field when composing.

### Q: What about SPF/DKIM/DMARC for my outgoing mail?
**A:** Gmail signs the mail with Google's DKIM and it passes SPF as Google's infrastructure. Mail authenticates as Gmail-sent, which is why "via gmail.com" can appear. Adding your own DMARC record is optional; if you do, start with `p=none`.

---

## Changelog

Current version: v1.0 (2026-07-20)

See [CHANGELOG.md](CHANGELOG.md) for dated major/minor releases and notes on structural updates.

---

## 🤝 Contributing

Found an issue or have a suggestion? Contributions are welcome!

1. Fork this repository
2. Create a feature branch: `git checkout -b feature/improvement`
3. Make your changes and commit
4. Push to your fork: `git push origin feature/improvement`
5. Open a Pull Request

For detailed contribution guidelines, including commit message conventions, see [CONTRIBUTING.md](CONTRIBUTING.md).

**Helpful contributions:**
- Instructions for other destination providers (Outlook, Proton, Fastmail)
- Additional troubleshooting scenarios
- Screenshots or visual guides
- Translations to other languages
- Guidance for other DNS providers with forwarding services (ImprovMX, Forward Email)

---

## 📝 License

This guide is released under the **MIT License** - see the [LICENSE](LICENSE) file for details.

---

## Additional Resources

- [Cloudflare Email Routing documentation](https://developers.cloudflare.com/email-routing/)
- [Gmail: Send emails from a different address or alias](https://support.google.com/mail/answer/22370)
- [Google: Sign in with app passwords](https://support.google.com/accounts/answer/185833)
- [Cloudflare: Email Routing limits](https://developers.cloudflare.com/email-routing/limits/)

---

## 📬 Support

- **Issues**: [GitHub Issues](https://github.com/jishnuteegala/custom-domain-email-guide/issues)
- **Discussions**: [GitHub Discussions](https://github.com/jishnuteegala/custom-domain-email-guide/discussions)

---

Done! You now have professional email on your own domain — for free. 🎉

---

**⭐ If this guide helped you, consider giving it a star and sharing it with others!**

---

**Made with ❤️ for the open-source community**
