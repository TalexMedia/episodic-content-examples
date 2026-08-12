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
| 7 | Live Tests | Volvo Trucks | Heavy trucks | Short, median 1m17s |
| 8 | IKEA Home Tour | IKEA USA | Home furnishing | Short, median 49s |
| 9 | Rico's Tacos | Albertsons with P&G | Grocery | Short, median 49s |
| 10 | DIY Influencer Program | Sherwin-Williams | Paint | Counter-example |

Sections: `01 Long Form`, `02 Short Form`, `03 And One That Did Not`, `04 What They Have In Common`. Closes with the Talex credential row and a low-pressure intro-call CTA (`ct7b-xvd-c9x`, the team link).

Every card uses the same anatomy: sector, show name, **Format**, **On camera**, **Length**, a three-number result strip, the video, then a note and sources.

## Rules for editing

- Every number must trace to the YouTube Data API or to a named public source. Never estimate.
- Self-reported figures must stay labelled as such on the card. Currently: IKEA store sales (+4.1%), eBay view total, subscriber gain, awareness lift and watch time, e.l.f. cross-platform views (7.6M), Volvo earned media (€126M), subscriber growth and the driver purchase-intent survey.
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
