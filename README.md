# ontimo-website

One-page public site for Ontimo at **https://ontimoapp.com**, used for Google Play Console website verification.

- `index.html` — the landing page
- `assets/` — mascot, icons, app screenshots (cropped from the App Store set)
- `_headers` — cache rules for `assets/` (Cloudflare Pages)

## Local preview

    open index.html

## Deploy (Cloudflare Pages)

Static site, no build step. Every push to `main` redeploys automatically.

1. Cloudflare dashboard → Workers & Pages → Create → Pages → Connect to Git → authorise GitHub → pick `JOANNESUN/ontimo`.
2. Build settings: framework preset **None**, build command **empty**, build output directory **`/`**. Production branch `main`.
3. Save and Deploy. The site goes live at `<project>.pages.dev` first — check it there before touching DNS.

## Domain (registered at VentraIP)

The domain must be on Cloudflare's nameservers before Pages can serve it.

1. Cloudflare dashboard → Add a site → `ontimoapp.com` → Free plan. Cloudflare scans existing DNS and shows you two nameservers, e.g. `xxx.ns.cloudflare.com`.
2. VentraIP → VIPcontrol → Domain Names → `ontimoapp.com` → Manage → Nameservers → replace the VentraIP nameservers with Cloudflare's two. Save.
3. Wait for Cloudflare to report the zone as Active (usually minutes, can be up to 24 hours).
4. Back in the Pages project → Custom domains → Set up a domain → `ontimoapp.com`, then repeat for `www.ontimoapp.com`. Cloudflare creates the DNS records and the certificate itself.
5. Confirm `https://ontimoapp.com` loads with a padlock before starting verification.

If you keep any email on the domain, copy the existing MX and TXT records into Cloudflare DNS at step 1 before switching nameservers, or mail will stop.

## Google Play website verification

1. Play Console → Account details → Organization website. Follow the link to Search Console.
2. Search Console → Add property → **Domain** (not URL prefix) → `https://ontimoapp.com`. A Domain property covers `www` and both protocols.
3. Search Console shows a `google-site-verification=...` TXT record. Add it in Cloudflare → DNS → Records: type `TXT`, name `@`, that value. Wait a few minutes, click Verify.
4. Back in Play Console, enter `https://ontimoapp.com` and save.

The Search Console property must be owned by the same Google account as the Play developer account.

## Links used

- App Store: https://apps.apple.com/us/app/ontimo-medicine-reminder/id6808908688
- Privacy policy (footer): https://medication-scan-proxy.joannecysun.workers.dev/ — the same policy the app links to, served by the Worker. Keep one copy; do not fork it into this repo.
- Google Play: shown as "coming soon" until the Android build clears review.
