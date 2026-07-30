# Publishing this page under your own URL

`index.html` is fully self-contained — no external fonts, scripts, images or CSS.
Drop it on any static host and it works.

## Option A — GitHub Pages (free, gives `apostolosvagias.github.io`)

1. Create a GitHub repo named exactly `<your-username>.github.io` (public).
2. From this folder:

```bash
cd ~/homepage
git init -b main
git add index.html
git commit -m "Personal homepage"
git remote add origin https://github.com/<your-username>/<your-username>.github.io.git
git push -u origin main
```

3. Live at `https://<your-username>.github.io` within a minute or two.
   No Pages settings needed for a `*.github.io` repo — it publishes automatically.

For any *other* repo name, go to Settings → Pages → Source → `main` / root,
and the URL becomes `https://<username>.github.io/<repo>/`.

## Option B — Cloudflare Pages or Netlify (free, drag-and-drop)

No git required. Sign in, choose "deploy without git" / "drag and drop",
drop this folder in. You get `something.pages.dev` or `something.netlify.app`.
Both let you attach a custom domain for free afterwards.

## Option C — your own domain (the one with no platform name in it)

Buy a domain (~€10/year; `.eu`, `.science`, `.net` are cheap and uncontested),
then point it at whichever host above:

- **GitHub Pages**: add a file named `CNAME` next to `index.html` containing just
  your domain, then at your registrar create a `CNAME` record for `www` →
  `<username>.github.io`, plus four `A` records for the apex pointing at
  `185.199.108.153`, `185.199.109.153`, `185.199.110.153`, `185.199.111.153`.
- **Cloudflare Pages / Netlify**: add the domain in their dashboard and follow
  the DNS instructions they generate. Simpler than the above.

HTTPS is automatic and free on all three.

## Option D — your institutional page

ILL staff pages carry more authority for an instrument scientist than any
personal domain, and cost nothing. Worth asking ILL communications whether you
can host or link this there. Best used *alongside* one of the above, not instead.

## Before you publish

Edit the `PROFILE` block near the top of the `<script>` in `index.html`:

- `photo` — for a self-hosted page a relative path works: `"photo.jpg"`
  (put the file next to `index.html`). The data-URI advice only applies inside
  a Claude artifact, where external hosts are blocked.
- `track` — replace the four `20XX` placeholders with real dates. They render
  underlined in amber until you do.
- `links` — LinkedIn and Scholar are set; ORCID is still empty.

Then check the metrics line in the Publications section — it is hard-coded
"as of July 2026" and will go stale.
