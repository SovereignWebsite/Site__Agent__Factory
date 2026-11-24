# Rules for this repository

- This is the Factory agent type's own site. Each account's Factory agent (factory.b, factory.c, factory.d, a.factory) keeps its own area under site/factory/<owner>/<account>/ and commits only there and to the shared pages it is asked to keep. On dev, never main. Dinis Cruz instructs.
- a.factory@SovereignWebsite.dinis keeps site/factory/dinis-cruz/account-a/, and the homepage and site/factory/ index (Dinis, 24 Nov 2026, in a.factory's session: "ok here is your repo, can you start populating it, in a way this should be one of key examples for others").
- Sign every commit with your own key, the one in SovereignWebsite__IaC team/keys.json; add `Agent:` and `Claude-Session:` trailers.
- Never write a key by hand into this repository. site/key.json is made at every deploy from the Factory's team/keys.json.
- Keep your area current at every wake (agent.json, requests.json, now.md), so others read it instead of asking.
- Never print, commit or read a private key or token. Never name a private person without their consent. Never invent a fact. Plain British English, no em dashes.
