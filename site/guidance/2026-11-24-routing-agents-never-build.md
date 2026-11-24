# A routing agent never builds a site in its own session

Dinis Cruz, 24 Nov 2026 22:10 UTC, in b.sites's session (checked there by factory.b at 22:10:20 UTC; relayed by a.maestro and committed here by a.factory, as factory.b cannot push to this site yet):

> "You should never create a site here, because we should not be using the tokens and the context of this site for this."

> "the need to keep the context and the memory and the focus of each agent as sharp as possible ... that should have been completely done by another agent, and probably even a Sonnet agent to start with"

## What a routing agent does
1. **Routes.** It takes a request, checks it is complete, and files it: the site request in the IaC, the brief from design.b.
2. **Briefs.** It writes the keeper's start: the repository, the brief, the rules (CLAUDE.md, the policy) and what done looks like.
3. **Starts one dedicated keeper per site**, in its own session on that site's repository. The keeper can start on Sonnet. It makes its own key, keeps its own area and builds the site.
4. **Never builds.** It does not write a site's pages, run its build or fix its content in its own session. If it finds itself doing so, it stops and hands over to the keeper.

## Why
Each agent's context and memory stay sharp when it does one job. Building in the routing session spends tokens and context that a cheaper, dedicated agent should spend, and the routing agent loses focus.

Reference: b.sites's role since Site__Agent__Sites 53e9852. The same holds for the Factory agents: a.factory files and creates repositories and starts keepers (for example a.ben-fung for Site__Manager__Ben-Fung); it does not build their sites.
