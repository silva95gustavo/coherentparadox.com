# Domain configuration

GitHub Pages: deploy from `master`, `/` (root). Custom domain: `coherentparadox.com`. `CNAME` is checked into the repository.

## Cloudflare

1. Point the apex domain to GitHub Pages using A records `185.199.108.153`, `185.199.109.153`, `185.199.110.153`, `185.199.111.153`. Use DNS only while GitHub validates the domain and issues its certificate. Remove conflicting apex A/AAAA/CNAME records, while preserving email and verification records.
2. Point `www` to `silva95gustavo.github.io` with a DNS-only CNAME.
3. Change the current redirect so it continues returning **302** to `https://gustavosilva.me/`, but excludes `/actor-terms` and all paths under `/actor-terms/`. For a Cloudflare Single Redirect expression:

   ```text
   (http.host in {"coherentparadox.com" "www.coherentparadox.com"}) and not (http.request.uri.path eq "/actor-terms" or starts_with(http.request.uri.path, "/actor-terms/") or starts_with(http.request.uri.path, "/.well-known/acme-challenge/"))
   ```

   Static destination: `https://gustavosilva.me`; status: `302`; preserve query strings (matching the original redirect).
4. Once the GitHub certificate is issued, enable Enforce HTTPS in GitHub Pages. Enable Cloudflare proxy if desired, with SSL/TLS **Full (strict)**.
5. Verify root returns the original redirect, `/actor-terms/` returns the contract, `/actor-terms` resolves to it, and `/actor-terms/contract.pdf` downloads the PDF.

If the current redirect uses Page Rules, a Bulk Redirect, or a Worker, edit or replace that rule so it no longer catches the terms paths. Keep a single active catch-all redirect excluding the terms paths.

Official setup: https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/managing-a-custom-domain-for-your-github-pages-site

The ACME certificate verification path must also bypass the redirect so GitHub can renew the HTTPS certificate. Email and domain verification DNS records must be preserved.

## Current production setup

- Apex: four GitHub Pages A records and four AAAA records, proxied by Cloudflare.
- `www`: proxied CNAME to `silva95gustavo.github.io`.
- Cloudflare SSL/TLS: Full (strict).
- GitHub Pages: custom domain `coherentparadox.com`, approved certificate, Enforce HTTPS enabled.
- First redirect rule: `www` terms paths return 302 to the same path on `https://coherentparadox.com`, preserving query strings.
- Existing catch-all rule: original 302 to `https://gustavosilva.me`, preserving query strings, except terms paths and ACME certificate verification paths.

Verified: root and `www` root retain the original 302; `/actor-terms/` and its PDF return 200; `/actor-terms` redirects to the trailing-slash URL. The live PDF matches the approved source exactly.
