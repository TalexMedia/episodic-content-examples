# Episodic Content Examples — reusable prospect asset

A general-purpose, client-facing set of case studies on branded video that audiences chose to watch. Shareable with **any** suitable prospect. Nothing in it is tied to a single company or sector.

- **File:** `index.html` (single self-contained file, no build step, no external JS)
- **Live:** https://talexmedia.github.io/episodic-content-examples/
- **Repo:** https://github.com/TalexMedia/episodic-content-examples
- **Rebuilt:** 2026-08-12 as case studies (was a 13-example reference list)

## What it is

Ten case studies, each one a real show with a repeating format, a real person on camera, and published results. **Long form and short form are kept in separate sections and never compared**, because their view counts are not on the same scale.

| # | Show | Brand | Sector | Scale |
|---|---|---|---|---|
| 1 | DIRT | Huckberry | Apparel and outdoor gear | Long, median 32m36s |
| 2 | Make Up Over Makeup | e.l.f. Cosmetics | Beauty | Long, 9 to 15m |
| 3 | Roadkill | MotorTrend, sponsored by Dodge | Automotive | Long, median 7m39s |
| 4 | Make My Space Work | Shopify Studios | Software | Long, median 13m43s |
| 5 | YETI Presents | YETI | Outdoor gear | Long, median 8m17s |
| 6 | Between 2 Rides | eBay Motors | Online marketplace | Long, 8 to 12m |
| 7 | Who Is JOB | Red Bull | Energy drinks | Long, median 8m59s |
| 8 | Live Tests | Volvo Trucks | Heavy trucks | Short, median 1m17s |
| 9 | IKEA Home Tour | IKEA USA | Home furnishing | Short, median 49s |
| 10 | Rico's Tacos | Albertsons with P&G | Grocery | Short, median 49s |

Sections: `01 Long Form`, `02 A Special Case: Red Bull`, `03 Short Form`, `04 What They Have In Common`. Closes with the Talex credential row and a low-pressure intro-call CTA (`ct7b-xvd-c9x`, the team link).

**Section 02 is the Red Bull feature** (added 2026-08-14 on Evan's ask): a navy block with the Red Bull wordmark, explaining the strategy rather than listing facts. Who Is JOB sits inside this section rather than in Long Form, so Red Bull appears once. Deliberate choices there:

- **The story starts in 2007, not at the founding.** Evan: "people don't care too much about the start of the company." The Krating Daeng / Mateschitz origin was cut. Do not add it back.
- **Legendeering is named inside the strategy sentence, never as a closing tagline.** `AUDIT_VOICE_RULES.md` line 166 bans the closing-tagline construction outright. The first draft violated it and all three reviewers caught it.
- **The feature carries its own source lines**, because four of its figures are Red Bull's own marketing numbers (1,250 events, 100+ disciplines, 160+ countries, 700 athletes) plus the 2024 cans figure. Keep them attributed.
- **The logo is an inlined SVG**, not a hotlink, so the page does not depend on Wikimedia. Public domain, trademarked, editorial use.

**The counter-example was removed 2026-08-12.** Sherwin-Williams' DIY Influencer Program was cut on Evan's call: the page is framed as inspiration, so an example of something that did not work pulled against it. He also pointed out the framing was wrong, since that program does have a repeatable idea (every creator paints with the Color of the Year); what it lacks is a series. Do not reintroduce a failure card without asking.

**Red Bull caveat.** The "All 85 episodes" playlist contains two laddish titles, "Flying Bikini Babes in Hawaii" (the second most viewed) and "Bikini Bottoms and SUP Surfing Big Waves". Flagged to Evan 2026-08-12 and left in place. If a recipient is sensitive, point the link at a single clean season instead. The embedded episode is deliberately a clean one rather than the top performer.

Every card uses the same anatomy: sector, show name, **Format**, **On camera**, **Length**, a three-number result strip, the video, then a note and sources.

## Rules for editing

- Every number must trace to the YouTube Data API or to a named public source. Never estimate.
- **Playlists can contain duplicates. Always dedupe before summing views.** The `Who is JOB` playlist lists 85 items but holds 84 unique videos (`-LLixi9MxV0` appears twice), so the naive sum overstated the total by 542,328 views. It also holds 81 numbered episodes plus a trailer and two extras, so "85 episodes" was wrong twice over. Sum unique ids, and separate playlist items from actual episodes.
- **Live sports and championship counts go stale.** Red Bull Racing's drivers' title count was written as seven from a pre-2024 source; the correct figure is eight (Vettel 2010-13, Verstappen 2021-24). Anchor such counts with "through the 20XX season" and re-check before each send.
- Self-reported figures must stay labelled as such on the card. Currently: IKEA store sales (+4.1%), eBay view total, subscriber gain, awareness lift and watch time, e.l.f. cross-platform views (7.6M), Volvo earned media (€126M), subscriber growth and the driver purchase-intent survey.
- **The opening does not explain the long/short split in prose.** Evan cut that line 2026-08-12 as "just weird". The distinction is carried structurally instead, by the two sections and the `Length` row on every card, which satisfies the `audit_shorts_vs_longform` rule. Do not add the explanation back.
- Tom's newsletter [Welcome to the Taco Drama](https://www.linkedin.com/pulse/welcome-taco-drama-tom-langan-wusce/) is linked from the Rico's Tacos card, because that piece is specifically about that show.
- **Never put a short-form number next to a long-form one without labelling both.** See the `audit_shorts_vs_longform` memory. This is why the page is split by scale and why every card carries a `Length` line.
- Every example must have a person on camera. That rule is why the "Oddly IKEA" ASMR film is not here, along with the fact that it is a one-month campaign burst rather than a format.
- Videos use click-to-play facades, not live iframes. More than about eight live iframes on one page causes browsers to mis-paint players into the wrong cards. Keep the facade pattern.
- Verify a video is still live and embeddable before adding it:
  `https://www.googleapis.com/youtube/v3/videos?id=<ID>&part=status&key=<KEY>`
- Keep text minimal. The page is about 1,950 visible words and should stay near that.
- No em dashes or en dashes. US English. See the voice rules in memory.
- Do not use the framing lead-ins "What it shows", "Why it matters", or "The takeaway".

## Accessibility

Body text and source links were brought to WCAG AA on 2026-08-12. `--txt3` is `#736A61` and small orange text uses `--o-text` (`#B84A07`), not `--o`. Do not revert those to the lighter values.

## Refreshing the figures

View counts drift. Before sending to a new prospect, re-pull and update the date in the opening block and the footer:

```bash
KEY="<YOUTUBE_API_KEY from Proposal/.credentials.local.md>"
IDS=$(grep -o 'data-yt="[A-Za-z0-9_-]*"' index.html | sed 's/data-yt="//;s/"//' | paste -sd, -)
curl -s "https://www.googleapis.com/youtube/v3/videos?id=${IDS}&part=snippet,statistics,contentDetails,status&key=${KEY}"
```

Playlist and library totals need paging through `playlistItems` 50 at a time and summing, or the numbers come out short.

## Origin

Derived from the POLYWOOD/James asset at
`ProspectAudit/prospects/polywood/content-examples.html`, **which is unchanged and stays as-is.**
That version is prospect-specific: it is cut to five examples, carries two POLYWOOD "why this is pertinent" bullets, and has no CTA at the recipient's request. Do not edit it when updating this one, and do not edit this one when updating that.

## Deploying

Push to `TalexMedia/episodic-content-examples`, which serves GitHub Pages from `main`.

Guard the clone → cd → git chain with `&&`. If the `cd` fails, the git commands run against the main workspace repo instead. See the deploy hazard note in `github_token_scope` memory.

**Do not reuse the existing `brand-content-examples` repo.** That one serves the POLYWOOD/James page.
