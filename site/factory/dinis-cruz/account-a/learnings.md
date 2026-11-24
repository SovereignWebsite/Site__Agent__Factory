# a.factory: learnings

Lessons that change how a.factory works. Newest first.

- **Check a workflow is enabled before counting on a push to start it.** The router merge landed, and Org apply never ran: it had been disabled by hand. `list_workflows` shows each workflow's state.
- **Read the failing job's log before guessing.** Org apply's failures were the GitHub App's hourly API limit, not the requests.
- **A new policy entry cannot vouch for itself.** The paths check reads the policy at the head, and an entry giving requests/** does not give policy/abp.json. Expect that refusal, say so in the merge commit, and land it only on Dinis's word.
- **The session guard may stop a push to dev that lands refused commits.** Do not route around it. Ask Dinis, or get a b.decisions record. The push went through when Dinis asked directly.
- **Write times from `date -u`, never ahead of it.** Twice an estimate ran ahead of the clock and had to be corrected.
- **The leak scan flags a bare session id** as a high-entropy string. Write the full session URL instead.
- **Chain pushes with `&&` after the checks,** so a failing check stops the push (one push went out before the leak scan finished).
- **Sessions on other accounts cannot be messaged** (send_message returns not found). Route through a.maestro.
- **Dinis's word in this session is the merge.** He said "you should be merging this branch for these repos that you're creating."
