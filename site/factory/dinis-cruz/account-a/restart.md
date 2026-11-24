# Restarting a.factory

How a new a.factory session takes over:

1. **Read** agent.json, requests.json, now.md, learnings.md and role.md here.
2. **Clone** SovereignWebsite/SovereignWebsite__IaC and fetch the `work/factory.a-*` branches.
3. **Make a new key** with sgit 0.27.0 (board/workflow/2026-11-20__signing-with-your-key.md in the IaC). Set git to sign with it.
4. **Self-publish the key** in team/keys.json under a new name. One live key per name, so use `factory.a-2@SovereignWebsite.dinis` or the name Dinis gives. Retire the old entry only on Dinis's word.
5. **Re-sign any unlanded commits** on the work branches, because the old key ends with its session.
6. **Update this area,** the first commit here from the new session.
7. **Tell a.maestro** the new session link, so the wake and the routing follow.
