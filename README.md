# Seventeen Hours South

A single-journey campaign proposal for **Qantas**, by **@legefilms**.
DFW → SYD on the Airbus A380 — one hero Reel, three ambient Reels.

One self-contained `index.html`. No build step, no dependencies, no framework.
Open the file, or drag the folder onto any static host.

Sibling to `airlines/united/beyond-the-horizon` — same structure, same card
system, same scroll reveals, same equirectangular route map. Three differences:

1. **It's a light deck.** Cream paper and Qantas red, not charcoal and
   electric blue.
2. **It's editorial, not technical.** The United deck sets every label in
   JetBrains Mono over Space Grotesk, which reads like an instrument panel.
   This one is **Fraunces** (a warm high-contrast serif, with an optical-size
   axis) over **Work Sans**, with no monospace anywhere. Headline second
   clauses are set in red italic rather than a paler grey — an editorial
   emphasis instead of a UI one.
3. **It's one file.** The United deck is React + Vite + Tailwind; this one
   inlines its CSS and JS so it survives being emailed as an attachment.

---

## Before you send this to anyone at Qantas

- [ ] **Wire the real scheduling link.** `GRAB 30 MINUTES?` currently opens a
      pre-filled email. There is one constant, `SCHEDULING_URL`, near the top
      of the `<script>` — drop a Calendly / Cal.com / SavvyCal URL in and the
      button re-points itself. This is the single most important fix on the
      page; a proposal built to be said yes to should not make them type.
- [ ] **Drop the media in.** See `assets/README.txt`. Missing files render a
      placeholder naming them, so the layout never breaks while you gather them.
- [ ] **Use a neutral subdomain.** Do *not* put "qantas" in the hostname —
      it reads as impersonation and it will get forwarded. Something like
      `seventeen-hours-south.pages.dev` or `17south.pages.dev`.
- [ ] **Make `og:image` absolute** once a domain is attached. Most link-preview
      scrapers will not resolve the relative `./assets/...` path, so iMessage
      and Slack will show no thumbnail until you do.
- [ ] **Check the analytics are current.** 110K+ followers, 250M+ views, 17.4%
      median like-to-view (last 30 posts, as of 1 Sep 2026), US primary market.
      Be ready to produce the platform exports — a marketing team will ask.
- [ ] **Confirm the route facts still hold** at the time you send. The
      commercial argument rests on DFW being one of two Qantas A380 US
      gateways and on Qantas being the only four-cabin A380 operator between
      the US and Australia. Both are stated as fact on the page.

Already handled: `noindex, nofollow` (in the `<meta>` and in `_headers`), no
confidentiality chrome, no revision numbers, no Instagram embeds.

---

## Swapping the route to San Francisco

One edit. Near the top of the `<script>`:

```js
const ORIGIN_CODE = "DFW";   // ← change to "SFO"
```

Both origins are fully authored in the `ORIGINS` object: coordinates, airport,
aircraft, duration, the hero title, all four "why this route" lines, the act
beats, the fare note and the ticker. Changing that one string re-points the
map, the readouts, the headline and the copy together.

Two things to know before you ship an SFO version:

- **The title changes with it.** `SEVENTEEN HOURS SOUTH` becomes
  `FIFTEEN HOURS SOUTH`, because it is derived from the origin, not hardcoded.
- **The commercial argument is genuinely different.** SFO–SYD is a 787-9
  route, not an A380 one, so the "only four-cabin A380 service" line does not
  apply and has been rewritten for that preset. Read those four lines before
  sending — they are the part a Qantas network person will scrutinise.

Add `assets/origin-sfo.jpg` when you switch.

---

## How the page is put together

Everything is data at the top of the `<script>`; the DOM below is scaffolding.

| Constant | Drives |
| --- | --- |
| `ORIGIN_CODE` / `ORIGINS` | The whole route — see above |
| `DESTINATION` | Sydney node: coordinates, airport, hook |
| `WORK` | The three Selected Work cards |
| `DELIVERABLES` | The package grid |
| `METRICS` / `BARS` | Creator analytics |
| `SCHEDULING_URL` / `CONTACT_EMAIL` | The CTA |

### The `[data-r]` pattern

Route-specific text is written into the HTML as its DFW value *and* tagged
`data-r="origin.code"`. On load, a short walk overwrites each tag from the
config. That means the page still reads correctly with JavaScript disabled —
which matters, because corporate mail gateways strip scripts — while the SFO
swap remains a one-line edit.

### The map

Equirectangular projection onto a 1000×520 space centred on 100°W, cropped by
the `viewBox` to the Pacific sector (`43 40 620 420`, roughly 95°E to 41°W).
Europe and Africa fall outside that crop deliberately.

The projection is linear with no modulo wrap, so Asia-Pacific longitudes are
authored as `lon − 360` through the `A()` helper. Sydney's +151.18 resolves to
−208.82, which puts it **west** of Dallas on the canvas — so the arc sweeps
across the Pacific in its true direction instead of doubling back over Europe.
That is the one thing an airline audience would catch instantly, so don't
"fix" the negative longitudes.

To move a node:

```js
x = ((lon - (-100) + 180) / 360) * 1000
y = ((90 - lat) / 180) * 520
```

### The palette and the type

Every colour and both typefaces are tokens in `:root`. For a pure-white deck
instead of cream:

```css
--paper: #ffffff;
--paper-band: #f5f5f5;
```

For a more classical display face, swap one token — the rest of the page
follows, because nothing names a font directly:

```css
--font-display: "Playfair Display", Georgia, serif;
```

Remember to update the Google Fonts `<link>` in the `<head>` to match.

The hero wordmark is set in title case (`Seventeen` / *Hours South*) rather
than all caps, which is most of what separates this from the technical
version. The strings live in `ORIGINS[...].title`, so change them there if you
want caps back — not in the HTML, which only holds the no-JS fallback.

`--brand` is Qantas red `#E40000`, used for fills, rules and markers.
`--brand-dp` is a deepened `#BE0000` used for small text — plain `#E40000` is
about 4.4:1 on cream, which is under the 4.5:1 floor for body-size type.

---

## Deploying

It is one HTML file plus a media folder. Any static host works.

**Cloudflare Pages:** push to GitHub, then Workers & Pages → Create → Pages →
Connect to Git. No framework preset, no build command, build output directory
`/`. `_headers` ships the security and cache headers.

**Or just send the folder.** It opens from disk with no server.
