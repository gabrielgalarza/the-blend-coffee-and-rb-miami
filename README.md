# The Blend: Coffee & R&B — Miami

Event page for **The Blend: Coffee & R&B Day Party, Miami** — Saturday, December 5, 2026,
11 AM – 3 PM EST at Astra Rooftop Garden, Northwest 2nd Avenue, Miami. Presented by
Belvedere Dirty Brew. Tickets $19.99. 21+.

Built from the Vegas page (`../the blend vegas`), same structure and build pipeline.

## Waitlist

Sales had not opened when this was built, so **every CTA opens the SweatPals widget
inline**, which shows the "Join waitlist" form (name, phone, email, SMS consent) until
sales start and then becomes checkout on its own. No copy change is needed on the day
tickets drop.

How it works — the pattern used on Blend Fest and SF Fit Fest:

- An OTT-styled pill button renders normally inside `<span class="rsvp-trigger">`.
- A transparent SweatPals iframe (`.rsvp-trigger__frame`) sits on top of it at `opacity:0`.
- The click lands on SweatPals' own button inside that iframe. The checkout script at the
  end of `<body>` intercepts it and opens the modal over the page instead of navigating away.

Event constants:

| | |
|---|---|
| Event alias | `the-blend-coffee-and-rb-miami` |
| Price tier | `7aec56ef-54bf-4f25-9172-255dfcd33704` |
| SweatPals page | https://sweatpals.com/event/the-blend-coffee-and-rb-miami |

`enableAutoEmbed=false` on the checkout script: every button here is placed by hand, and
leaving it `true` appends a stray second widget at the end of the page.

Signups land in SweatPals, not in this repo. Read them with the `sweatpals` MCP server
(`waitlist_report`, or `event_detail` for `waitlist_count`); run `sweatpals_sync` first,
since Miami is not in the local mirror until sales open.

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
- **VIP** — `#vip` is `hidden`. The SweatPals listing has one $19.99 tier and no VIP tier;
  remove `hidden` once a Miami VIP tier exists. Copy is carried over from Vegas unchanged.
- **Partners** — Belvedere is in. Add the venue partner tile properly if Astra signs on as one.
- **Images** — all 43 photos are carried over from past Bay Area / Vegas editions. Swap in
  Miami shots after the event.
