# Episodic Content Examples — reusable prospect asset

A general-purpose, client-facing reference library of branded video that audiences chose to watch. Shareable with **any** suitable prospect. Nothing in it is tied to a single company or sector.

- **File:** `index.html` (single self-contained file, no build step, no external JS)
- **First intended recipient:** Vijay Iyer, Cranbrook
- **Status:** built 2026-08-12, **not yet deployed**

## What it is

Thirteen verified examples grouped by what each one demonstrates:

| Section | Covers | Examples |
|---|---|---|
| 01 Formats That Repeat | the core proposition | The Weekender, IKEA Home Tour, Make My Space Work, From Scratch |
| 02 Where The Brand Sits | integration, from plot to invisible | Between 2 Rides, Roadkill, YETI Presents, Living Off The Wall |
| 03 Format And Scale | what else the form does, and at what budget | Make Up Over Makeup, Oddly IKEA, Two Bellmen, Second Act |
| 04 And One That Went The Other Way | the counter-example | Sherwin-Williams DIY Influencer Program |
| 05 What Runs Through All Of Them | the four takeaways | — |

Closes with the Talex credential row and a low-pressure intro-call CTA (`ct7b-xvd-c9x`, the team link).

## Origin

Derived from the POLYWOOD/James asset at
`ProspectAudit/prospects/polywood/content-examples.html`, **which is unchanged and stays as-is.**
That version is prospect-specific: it is cut to five examples, carries two POLYWOOD "why this is pertinent" bullets, and has no CTA at the recipient's request. Do not edit it when updating this one, and do not edit this one when updating that.

## Rules for editing

- Every number must trace to the YouTube Data API or to a named public source. Never estimate.
- Brand award-entry figures (IKEA store sales, eBay season totals, e.l.f. cross-platform views) are **self-reported** and must stay labelled as such on the page.
- Videos use click-to-play facades, not live iframes. More than about eight live iframes on one page causes browsers to mis-paint players into the wrong cards. Keep the facade pattern.
- Verify a video is still live and embeddable before adding it:
  `https://www.googleapis.com/youtube/v3/videos?id=<ID>&part=status&key=<KEY>`
- No em dashes or en dashes. US English. See the voice rules in memory.

## Refreshing the figures

View counts drift. Before sending to a new prospect, re-pull and update the date in the opening block and the footer:

```bash
KEY="<YOUTUBE_API_KEY from Proposal/.credentials.local.md>"
IDS=$(grep -o 'data-yt="[A-Za-z0-9_-]*"' index.html | sed 's/data-yt="//;s/"//' | paste -sd, -)
curl -s "https://www.googleapis.com/youtube/v3/videos?id=${IDS}&part=snippet,statistics,contentDetails,status&key=${KEY}"
```

## Deploying

Not deployed yet. When it is, follow `Proposal/DEPLOY.md`. Suggested repo: `talexmedia/episodic-content-examples`, giving
`https://talexmedia.github.io/episodic-content-examples/`.

Guard the clone → cd → git chain with `&&`. If the `cd` fails, the git commands run against the main workspace repo instead. See the deploy hazard note in `github_token_scope` memory.

**Do not reuse the existing `brand-content-examples` repo.** That one serves the POLYWOOD/James page.
