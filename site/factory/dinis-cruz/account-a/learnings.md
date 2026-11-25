# a.factory: learnings

Lessons that change how a.factory works. Newest first.

- **Read a policy refusal against the policy, not against what I expected it to mean** (25 Nov 2026, IaC PR #3, an ABP case study). The paths check said "a.factory@SovereignWebsite.dinis may not change .github/workflows/org-apply.yml". I read that as the "needs Dinis's merge" marker, and told Dinis and a.maestro so. It wasn't. In policy/abp.json, a path under `needs_dinis_merge` *passes* the paths check, and the merge is Dinis's gate. A path missing from `may_change` is *refused*. My entry has no `.github/**`, while factory.b, c and d each have `.github/**` and `policy/**` with `needs_dinis_merge`. So the red meant "this agent may not change this path at all", not "this waits for Dinis". a.maestro caught it. What I got right was not touching policy/abp.json to turn it green. What I'll do next time: before saying what a refusal means, open my own entry in policy/abp.json and check whether the path is in `may_change`, in `needs_dinis_merge`, or in neither; quote the line that decides; and if it's neither, say plainly that I'm outside my paths and that the fix is a policy change for Dinis to merge, proposed by an agent that may change policy/**.
- **Check a workflow is enabled before counting on a push to start it.** The router merge landed, and Org apply never ran: it had been disabled by hand. `list_workflows` shows each workflow's state.
- **Read the failing job's log before guessing.** Org apply's failures were the GitHub App's hourly API limit, not the requests.
- **A new policy entry cannot vouch for itself.** The paths check reads the policy at the head, and an entry giving requests/** does not give policy/abp.json. Expect that refusal, say so in the merge commit, and land it only on Dinis's word.
- **The session guard may stop a push to dev that lands refused commits.** Do not route around it. Ask Dinis, or get a b.decisions record. The push went through when Dinis asked directly.
- **Write times from `date -u`, never ahead of it.** Twice an estimate ran ahead of the clock and had to be corrected.
- **The leak scan flags a bare session id** as a high-entropy string. Write the full session URL instead.
- **Chain pushes with `&&` after the checks,** so a failing check stops the push (one push went out before the leak scan finished).
- **Sessions on other accounts cannot be messaged** (send_message returns not found). Route through a.maestro.
- **Dinis's word in this session is the merge.** He said "you should be merging this branch for these repos that you're creating."
