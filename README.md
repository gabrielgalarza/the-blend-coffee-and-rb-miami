# The Blend: Coffee & R&B — Miami

Event page for **The Blend: Coffee & R&B Day Party, Miami** — Saturday, December 5, 2026,
11 AM – 3 PM EST at Astra Rooftop Garden, Northwest 2nd Avenue, Miami. Presented by
Belvedere Dirty Brew. Tickets $19.99. 21+.

Built from the Vegas page (`../the blend vegas`), same structure and build pipeline.

## Registration

Every CTA is a plain link to the SweatPals event page, opened in a new tab:

```
https://sweatpals.com/event/the-blend-coffee-and-rb-miami
```

That is the house rule in the OTT page template, and this page had to be moved onto it.
It previously used a transparent-iframe overlay that opened checkout in a modal here.
Two things killed that:

- The template's notes record the overlay returning "event not found" for Gabriel on Vegas.
- It had to name a single price tier id. That went stale the moment the early-bird tier
  sold out, and the page kept advertising $19.99 after GA had moved to $29.99.

The event page always sells whichever tier is current, and before sales open it shows its
own "get notified" button, so one link covers the waitlist phase too.

The `[data-register]` attribute stays on all three links: `script.js` uses it to fire the
Meta Pixel `Lead` event.

| | |
|---|---|
| Event alias | `the-blend-coffee-and-rb-miami` |
| SweatPals page | https://sweatpals.com/event/the-blend-coffee-and-rb-miami |

Signups and sales land in SweatPals, not in this repo. Read them with the `sweatpals` MCP
server (`event_detail`, `waitlist_report`); run `sweatpals_sync` first.

### Known dead CSS

`styles.css` still carries `.rsvp-frame*` and `.rsvp-modal*` (~190 lines), unreferenced by
`index.html` or `script.js`. They are left over from earlier popup attempts on LA/Vegas and
predate the overlay removal. Safe to delete; left in place to avoid an unrelated edit during
an active sale.

## Build

Two targets from one source: this repo as its own GitHub Pages page, and a Webflow Code
Embed on overthetopxp.com.

```
python3 build-embed.py
```

Run it after **any** change to `index.html`, `styles.css` or `script.js`. It writes
`embed.css` / `embed.js` (commit and push these — Pages serves them) and `webflow-embed.html`
to paste into the Webflow Code Embed. It namespaces every class to `b-*` and scopes every
rule under `#blend-miami`, because Webflow's theme owns `.line`, `.btn`, `.container`,
`.card`, `.hero`, `.gallery`, `.h2` and `.text-center` too.

Bump `?v=` in `index.html` when you want browsers to drop the cached bundle; the builder
copies that number into the embed.

Local preview:

```
python3 -m http.server 8742
```

## Still to do

- **Lineup photos** — confirmed: Bobby B. (11–12), Keith B (12–1), Sea Rae (1–2),
  Blinkdalink (2–3). The four portraits were cropped out of the event flyer, so they are only
  184×245. They are sharp enough for the tiles but will look soft if the tiles ever get bigger —
  replace `images/dj-*.jpg` with the originals when they turn up.
- **VIP** — `#vip` is still `hidden`, but Miami IS selling VIP now (13 sold as of 2026-11-11,
  $99.99 list, going out nearer $69.99). The blocker is the copy: it is Vegas's, carried over
  unchanged and never checked against what Miami VIP includes. Check it, then un-hide.
- **Ticket price goes stale** — the page hard-codes a price in four places (meta, good-to-know,
  the stat row, the closing CTA). Tiers escalate, so it drifts: it shipped at $19.99 (flash early
  bird), and by 2026-11-11 GA was ADVANCE TIER 3 at $29.99, $34.92 with fees. Re-check against
  `event_detail` before any push, or drop the number.
- **Partners** — Belvedere is in. Add the venue partner tile properly if Astra signs on as one.
- **Images** — all 43 photos are carried over from past Bay Area / Vegas editions. Swap in
  Miami shots after the event.
