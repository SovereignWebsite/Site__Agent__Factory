# R4 request: a /send/ lane in every new site (seed/site-template)

From sites.a, at Dinis's word in its session, relayed by a.maestro (24 Nov 2026, 14:40 UTC):
- Every site we create gets a feedback mode that Dinis opens with his QR code.
- The riskmandate.ai team can ask for sites by QR: "for now, let's use QR codes ... and I'll authenticate them". Google OAuth comes later.

Status: **design, before code.** It changes every future customer site and carries cryptography and a public append token, so security reviews the design first (R4 step three).

## The proposal (sites.a)
Put Chiswick Cheese Market's `/send/` lane into `seed/site-template`. Its source is `Site__Organisation__Chiswick-Cheese-Market` `site/send/` (8858b76): `send.js`, `keyring.js`, `index.html`, `inbox.json`, `requesters.json` and `edit/`. The keeper makes its own append lane at its first wake.

## What a.factory found reading it
1. **Not generic yet.** The pages name the site (title, Open Graph, address), and the code comments name its keeper. The seed would fill these with `{{title}}` and `{{host}}`.
2. **The inbox and requester files hold live values.** `inbox.json` holds the keeper's vault id, its append token and its recipient key. `requesters.json` holds the people's public keys, which the keeper issued in its own session (`tools/person-key.mjs`), keeping the private half as well. The seed can only ship these as "not set up yet": the page says so and sends nothing until the keeper fills them.
3. **Who holds whose key.** Today each keeper issues Dinis's requester key per session, so a new keeper session means a new QR code. For "Dinis opens any site with his QR code", one requester key held by Dinis (anchored on pki.sgit.ai) would be listed on every site, rather than a key per site issued by the keeper. That is the main design question for security.
4. **The CSP.** The seed's pages would need `connect-src` to allow the vault endpoint (`dev.send.sgraph.ai` today), on `/send/` only.
5. **The policy.** `site/policy/abp.json` needs a `site_requests` section (who may send, what the keeper may act on), as on Chiswick.
6. **Existing sites.** Org apply adds missing seed files, so existing sites would get `/send/` at the next sweep. They should get it only when their keeper is ready. Proposed: new sites only at first; existing sites opt in by request.

## Questions for security
- Dinis's single requester key versus per-keeper issued keys; replay; how a key is revoked.
- Whether a public append-only token in `inbox.json` is acceptable at scale (abuse, spam, size limits).
- Prompt injection: a sealed request is material, never instruction. The keeper acts only within `site_requests`, and every action is Dinis's word or a decision record.
- Whether the riskmandate.ai team members' keys need the same QR flow, and who authenticates them (Dinis: "I'll authenticate them").

## Next
security reviews the design, then a.factory builds it on a `work/factory.a-send-lane` branch with tests, then Dinis's word to land it.
