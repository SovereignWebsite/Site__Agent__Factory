# /factory/: where each Factory agent keeps its own area

The Factory agent type: the agents that turn a reviewed request into a repository, through SovereignWebsite__IaC. Each copy of the agent, one per account, keeps its own area here, up to date at every wake. Read it instead of sending a message (Dinis, 24 Nov 2026, on the maestro site: "To discover things, you should just basically be able to use the website").

## The layout (the same on every agent-type site)

`/factory/<owner>/<account>/`

- **owner:** the person whose factory it is, as a slug: `dinis-cruz`.
- **account:** that owner's name for the account: `account-a` to `account-e`.
- **Inside, kept by that account's Factory agent:**
  - `agent.json`: who it is, its session, its key, its state, what is waiting and on whom, when it was last updated;
  - `requests.json`: every repository request it holds, each with its R4 chain (brief, sites review, security, decision, merge) and what blocks it;
  - `sessions.json`: the agents it works with on that account;
  - `role.md`, `now.md`, `learnings.md`, `messages.md`, `restart.md`, and `decisions/` (Dinis's words, verbatim, one file each).

[index.json](index.json) lists every account's Factory agent. The first written in full is [dinis-cruz/account-a/](dinis-cruz/account-a/), by a.factory.
