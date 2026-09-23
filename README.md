# ontimo-website

One-page public site for Ontimo at **https://ontimoapp.com**, used for Google Play Console website verification.

- `index.html`: the landing page (English)
- `assets/`: mascot, icons, shared stylesheet, app screenshots (cropped from the App Store set)
- `zh/`, `id/`: Traditional Chinese and Indonesian versions
- `CNAME`: the custom domain, read by GitHub Pages
- `.nojekyll`: serves files as they are, no Jekyll processing

## Local preview

    open index.html

## Deploy (GitHub Pages)

Static site, no build step. Every push to `main` redeploys automatically.

1. The repo must be **public**. Pages from a private repo needs GitHub Pro.
2. Repo → **Settings** → **Pages** → Source: **Deploy from a branch** → branch `main`, folder `/ (root)` → Save.
3. Under **Custom domain**, enter `ontimoapp.com` and Save. (The `CNAME` file in this repo sets the same thing.)
4. Once DNS is in place and the check passes, tick **Enforce HTTPS**.

First build takes a minute or two; the site is live at `https://joannesun.github.io/ontimo/` until the domain resolves.

## DNS (domain registered at VentraIP)

In VIPcontrol → Domain Names → `ontimoapp.com` → Manage → DNS:

| Type | Name | Value |
| --- | --- | --- |
| A | `@` | `185.199.108.153` |
| A | `@` | `185.199.109.153` |
| A | `@` | `185.199.110.153` |
| A | `@` | `185.199.111.153` |
| CNAME | `www` | `joannesun.github.io.` |

All four A records are needed. They are GitHub's Pages servers. Allow up to a day for propagation, then GitHub issues the Let's Encrypt certificate automatically.

## Google Play website verification

1. Play Console → Account details → Organization website. Follow the link to Search Console.
2. Search Console → Add property → **Domain** (not URL prefix) → `https://ontimoapp.com`. A Domain property covers `www` and both protocols.
3. Search Console shows a `google-site-verification=...` TXT record. Add it in VentraIP DNS: type `TXT`, name `@`, that value. Wait a few minutes, click Verify.
4. Back in Play Console, enter `https://ontimoapp.com` and save.

The Search Console property must be owned by the same Google account as the Play developer account.

## Links used

- App Store: https://apps.apple.com/us/app/ontimo-medicine-reminder/id6808908688
- Privacy policy (footer): https://medication-scan-proxy.joannecysun.workers.dev/ is the same policy the app links to, served by the Worker. Keep one copy; do not fork it into this repo.
- Google Play: shown as "coming soon" until the Android build clears review.
