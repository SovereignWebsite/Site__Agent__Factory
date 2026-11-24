# Every public site has a keeper and design rounds from the start

Dinis Cruz, 24 Nov 2026 ~22:41 UTC, in a.maestro's session (relayed by a.maestro at 22:43 UTC):

> "every website that we create that has a public element always has a keeper, at least to do a couple rounds in the beginning, and actually should also have the design element to this"

## The rule
- **A dedicated keeper from the first rounds.** Every site with a public part gets one agent of its own, in its own session on the site's repository, at least for the first rounds. The keeper makes its own key, keeps its own area and builds the site. The routing agent never builds it (see [routing agents never build](2026-11-24-routing-agents-never-build.md)).
- **Design directions and review rounds.** Every such site gets design directions and review rounds from a design agent (design.b, design.c, design.d or a.design), not only a build.

## In the Factory
From 25 Nov 2026, a site request names both, and a public request without them is incomplete:
```json
"keeper": "a.ben-fung@SovereignWebsite.dinis",
"design": "design.b@SovereignWebsite.dinis"
```
build/requests.mjs checks them for requests dated 2026-11-25 or later. Requests filed before that are listed by a.factory with the keeper each still needs.
