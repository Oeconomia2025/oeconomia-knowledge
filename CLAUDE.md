# Oeconomia Knowledge: maintenance spec for Claude Code

## Purpose
Public knowledge base for the Oeconomia ecosystem. Consumed by:
1. The community chat bot (Claude API), which loads these files into its prompt.
2. GitBook via Git Sync (planned), and the websites (oeconomia.io, oeconomia.tech).

## Sources
`protocols/*` was copied (Nov 2026) from the `docs/` folders of the eloqura, alluria,
oec-initial-staking and oeconomia-dao-hub repos, minus deployment, env-var, API and
admin pages. Those repo docs are developer-facing; when rewriting, make them user-facing
(how to do X, what Y means) and drop source-file references.

## Rules
- Public information only. No secrets, env values, or unreleased plans.
- One fact, one place: tokenomics only in `tokenomics.md`, addresses only in `contracts.md`.
  Elsewhere, link to them. If you find a conflicting number anywhere, flag it to Jason.
- `tokenomics.md` has a DRAFT banner until Jason confirms the figures. Don't remove it
  without his explicit confirmation.
- Keep total size small (target under ~60k tokens) so the bot can load everything with
  prompt caching instead of needing RAG.

## Chat bot loading (for the bot repo)
- On startup: read every `.md` file except `CLAUDE.md` and `README.md`, in a stable order
  (`bot/guidelines.md` first, then `overview.md`, `tokenomics.md`, `contracts.md`,
  `faq.md`, then `protocols/**`), join with file-path headers, and send as a cached
  system prompt block.
- Reload when this repo changes (GitHub webhook or a GitHub Action calling the bot's
  reload endpoint). Poll the latest commit SHA hourly as a fallback.

## Open items
- Confirm tokenomics (see `tokenomics.md` open items), then remove the DRAFT banner.
- Retire or update oeconomia.tech/tokeninfo (old 100M / 5% fee figures).
- Add DAO governor and presale contract to `contracts.md` once deployed.
- Add points program details once Season 1 is live.
