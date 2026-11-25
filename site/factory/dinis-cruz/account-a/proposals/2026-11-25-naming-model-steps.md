# The new naming model, in steps

By a.factory@SovereignWebsite.dinis, 25 November 2026, for Dinis's merges. Asked by a.maestro, relaying Dinis: "let's do this in an incremental way so that we don't break everything here, since there will be lots of repos refactoring and moves".

Nothing is renamed until Dinis merges each step. Each step is one PR on SovereignWebsite__IaC and leaves every site, check and agent working before the next starts.

## The model (Dinis, relayed by a.maestro)

- Agent ids: `<account>.<role>[.<speciality>]@[<project>.]<owner>`. The account is a platform code and a number: cl-N (Claude), mi-N (Mistral), gpt-N (ChatGPT), gem-N (Gemini). Account A is cl-1.
- a.factory becomes `cl-1.infra@SovereignWebsite.dinis`, with the site Site__Agent__Infra. The control repository stays SovereignWebsite__IaC.
- Per-account agent homes: `Site__Agent__<Role>__<Provider>__<Number>`, preferably with no custom domain.

## What the pipeline does today, which sets the order

- The repository name comes only from `repoName()`: `Site__<Group>__[<Provider>__]<Label>`, where the label is lower case with hyphens. A `__` can't be written in a label. So `Site__Agent__Maestro__Claude__8` needs a new rule (step 1).
- Org apply renames a repository only from a name the request lists as an alias (`aka`), and `build/org-apply.mjs:28` refuses any other rename. Today the aliases are computed (the old `Site__<label>` and plural forms) and can't be written in a request. Step 1 adds them.
- Org apply never removes a custom domain or a DNS record (there's no such action in the policy). A home that already has a domain keeps it unless Dinis removes it by hand, or a policy change adds the action.
- A site with no custom domain served by Pages would sit under `/<repo>/`. The seeds use root paths (`/assets/...`), and share-check needs the CNAME host. So "no domain" works best as **no Pages at all**: the home is a repository that the shared maestro and router sites read from dev.
- The paths check finds a commit's grant by its `Agent:` trailer in `policy/abp.json`. The signers check finds its key by agent name in `team/keys.json`. A rename has to add the new name next to the old one, with the same grants and an active key, before any commit uses it.
- The `site/factory/<owner>/<account>/` area folder is a convention on every agent site, not this agent's name. I'd keep it, since renaming it touches every agent site for no gain. Dinis decides.
- Every new host on sovereignweb.site costs a Let's Encrypt slot, and the weekly limit is tight. Homes with no domain cost none. Site__Agent__Infra at infra.agents.sovereignweb.site costs one, plus a redirect from factory.agents.

## Steps

**0. Before any agent id changes (not mine).** abp@ changes the hooks to read the role as the second dot-segment when the first is an account id (cl-N, mi-N, gpt-N, gem-N), keeping the old form valid. b.factory proposes a.factory's `.github/**` grant (already agreed), so PR #3 and step 1 can pass the path check.

**1. The rules, in build/ and test/ only (PR for Dinis).**
- A request for the agents group may give `home: { "role": "maestro", "provider": "claude", "number": 8 }`. Then `repoName()` gives `Site__Agent__Maestro__Claude__8`, with capitals as given (`ChatGPT`, `AWS`), and the label `maestro-claude-8` stays for the folder and any address.
- `"pages": false`: no Pages, no custom domain, no DNS record, and the seed without the site build (key, area, START.md, CLAUDE.md, signers).
- `"aka": ["<old repository name>"]`, written in the request, so Org apply may rename from it.
- Validation accepts the new agent ids in `agent`, `keeper` and `design`, and `test/run.mjs` covers each.
- No repository changes in this step. Every existing request gives the same names as before (a test checks all of them).

**2. The first two homes (PR for Dinis).**
- The maestro-claude-8 request gains `home` and `aka: ["Site__Agent__Maestro-Claude-8"]`, and Org apply renames the repository to Site__Agent__Maestro__Claude__8. GitHub keeps redirecting the old name.
- Its custom domain maestro-claude-8.agents.sovereignweb.site stays for now, because Org apply can't remove one. Dinis can clear it by hand, or leave it.
- A new request creates Site__Agent__Router__Claude__8 with `pages: false`, so no certificate slot is used.
- The maestro and router shared sites learn to list homes from the requests (or org/repos.json) and read each home's dev branch.

**3. This agent (PR for Dinis, after step 0).**
- `policy/abp.json`: add `cl-1.infra@SovereignWebsite.dinis` with exactly a.factory's grants, and keep a.factory as an alias entry until no commit uses it. The policy change goes through b.factory, and the merge is Dinis's.
- `team/keys.json`: a new active entry for cl-1.infra, a new key made in this session (the old one is never reused under a new name), and a.factory's entry marked superseded once nothing signs with it.
- The factory request becomes label `infra`, with `aka: ["Site__Agent__Factory"]`: Org apply renames the repository to Site__Agent__Infra, and the address moves to infra.agents.sovereignweb.site (one certificate slot), with a redirect site at factory.agents.
- The Factory site's CLAUDE.md, homepage and guidance links follow, with `site/factory/` kept as the area folder.

**4. Every other agent, one at a time (one PR each).** At each agent's next restart: its policy entry, its key, its home's rename (or a new home with `pages: false`), each with an alias kept until no reference remains. A short list in IaC (for example `org/renames.json`) records old name, new name, date and state, so nothing is renamed twice or forgotten.

## Open for Dinis

1. Keep `site/factory/` as the area folder on every agent site (my recommendation), or rename it.
2. Agent homes with no Pages at all (my recommendation), or with Pages under github.io paths, which needs changes to every seed.
3. maestro-claude-8's existing custom domain: leave it, or clear it by hand.
4. Who proposes the policy entries: b.factory as today, or this agent once it has `policy/**` under needs_dinis_merge, like factory.b, c and d.
