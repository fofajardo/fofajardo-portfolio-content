---
title: "The Cost of Preflight: Measurements from the UPLB Pre-registration Period"
description: "There's a Part 2?"
date: "2026-08-03"
tags:
  - amis
  - uplb
  - cors
  - web-performance
  - api-design
discuss:
  reddit: "https://www.reddit.com/r/peyups/comments/1uscu8i/uplb_the_road_to_patience_why_amis_is_still_slow/"
  mastodon: "https://fosstodon.org/@fajardo/116883329929032145"
---

In [The Road to Patience: Why AMIS Is Still Slow, Three Years Later](/blog/2026/07/the-road-to-patience-why-amis-is-still-slow-three-years-later), I laid out a theory: the preflight `OPTIONS` requests being sent with every API call to the AMIS API were adding latency.

A few students anonymously sent me [HAR (HTTP Archive)](https://en.wikipedia.org/wiki/HAR_(file_format)) captures from their browsers during the pre-registration period in the enlistment module. Each HAR is a browser export that logs every request a page made during a session such as URLs, headers, timing. One of them happened to have CORS disabled in their browser, which gave us a control group. The rest captured their sessions with CORS fully enabled like everyone else. This provides us with an actual before and after measurement.

So let's see if the theory holds up.

## Setting up the comparison

Across the full set of captures: 251 network entries, 9 sessions.
- 6 sessions had CORS enabled, and 3 had it switched off client-side.
- Both groups hit the same API, with the same `Authorization` and `x-session-id` headers on every call.

| | CORS enabled | CORS disabled |
|---|---|---|
| Sessions | 6 | 3 |
| AMIS API requests | 160 | 27 |
| `OPTIONS` preflight requests | **80 (50%)** | **0** |

## How much did it actually cost?

The control group, which did not spend any time sending preflight requests, is measured as follows. This shows that the enlistment module can finish loading in a minute during peak usage.

| Session | Total actual request time | Preflight time | Preflight overhead |
|---|---|---|---|
| Control 1 | 50.7s | 0s | 0% |
| Control 2 | 93.4s | 0s | 0% |
| Control 3 | 97.8s | 0s | 0% |

This is where it gets interesting. I lined up the total time spent on actual requests against the total time spent on preflight, session by session:

| Session | Total actual request time | Preflight time | Preflight overhead |
|---|---|---|---|
| Session 1 (Jul 20, not peak usage) | 7.6s | 2.8s | 36.5% |
| Session 2 (Jul 22, AM) | 90.0s | 86.8s | **96.4%** |
| Session 3 (Jul 22, AM) | 70.1s | 59.7s | **85.2%** |
| Session 4 (Jul 22, AM) | 34.3s | 20.3s | **59.3%** |
| Session 5 (Jul 23, AM) | 66.6s | 52.7s | **79.2%** |
| Session 6 (Jul 23, AM) | 108.4s | 71.1s | **65.6%** |
| **Average** | | | **70.3%** |

Every single CORS-enabled session wasted somewhere between 37% and 96% on top of its actual request time, just to ask permission to make the request it was about to make anyway. On average, preflight added **70% more time** than the request it was gating. In the worst case, the preflight request was basically a second full request based on the time spent.

During peak usage (excluding Session 1), with CORS enabled, **fully loading the enlistment module takes at best, one (1) minute, and at worst, three (3) minutes**. This does not account for other factors (e.g., differences in internet providers).

Again, every preflight response came back with `Access-Control-Max-Age: 0`. This explicitly tells the browser to never cache the decision.

## Where this leaves us

The estimates that were laid out in the first article were more on the conservative side after examining the HARs. It confirms that the preflight overhead in terms of time, at least, in the enlistment module, measures to around 70%. This is a cost sitting on top of every API call the AMIS front-end makes.
