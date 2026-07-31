# Publishing this page under your own URL

**Currently live at <https://apostolosvag.github.io>**, deployed from `main` by
`.github/workflows/pages.yml` on every push. The options below are kept for
moving it somewhere else later; nothing in them needs doing today.

`index.html` is fully self-contained — no external fonts, scripts, images or CSS.
Drop it on any static host and it works.

## Option A — GitHub Pages (free, gives `<username>.github.io`) — in use

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

## Keeping it up to date

Most of the page is hand-edited in the `PROFILE` block near the top of the
`<script>` in `index.html` — photo, positions, links, collaborations, and the
hand-written `news` items (talks, beamtime, students, moves).

Two blocks refresh themselves and should **not** be edited by hand. Both sit
between `AUTO-…-BEGIN` / `AUTO-…-END` markers, and both are rewritten by
`tools/update_news.py`, which `.github/workflows/news.yml` runs at 06:15 UTC on
the 1st of each month (or on demand from the Actions tab):

- **`newsAuto`** — recent publications, from the public ORCID API.
- **`metrics`** — citations, h-index and i10-index, from the public OpenAlex API.

Run it locally any time with `python3 tools/update_news.py`. It only writes when
something actually changed, and it fails safe: if either API is unreachable, or
if OpenAlex returns implausible zeroes, it leaves that block untouched rather
than publishing bad numbers.

Two things worth knowing about the metrics:

- They are **OpenAlex** numbers, and are labelled as such on the page. Google
  Scholar indexes more sources and reports higher; its numbers can't be
  refreshed automatically, so the page links out to Scholar instead of quoting it.
- OpenAlex holds a duplicate author record carrying the same ORCID, and the
  ORCID-based lookup resolves to the near-empty one. The script therefore pins
  the canonical ID (`A5000055007`, set via `--author`). If the numbers ever look
  wrong, check that record hasn't been split again upstream.

### Still open

The 2013–2016 gap in `track` is now filled (FORTH / Jülich postdoc, then
military service). Two smaller date questions remain, both needing confirmation
rather than research:

- **MPI-P overlaps the postdoc.** MPI-P is listed as ending 2014, but the
  postdoc starts Nov 2013. One of the two is off — most likely MPI-P should end
  2013, since the postdoc date is month-precise and the MPI-P one is not.
- **Jun 2016 → 2017 is unaccounted.** Military service ends Jun 2016 and
  Groningen is listed as starting 2017. If Groningen actually began in 2016,
  that closes it.
