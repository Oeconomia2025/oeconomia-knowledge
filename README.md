# Oeconomia Knowledge

Single source of truth for public information about the Oeconomia ecosystem.
Used by the community chat bot, and intended to feed GitBook (Git Sync) and the
websites so every channel says the same thing.

## Layout
| Path | What it holds |
|---|---|
| `overview.md` | What Oeconomia is, the protocols, and how they connect |
| `tokenomics.md` | Public OEC token details (one place only) |
| `contracts.md` | Every live Sepolia contract address |
| `faq.md` | Short answers to common questions |
| `protocols/<name>/` | Per-protocol docs (features, how-tos, contract notes) |
| `bot/guidelines.md` | Rules the chat bot must follow when answering |
| `internal/` | Unannounced material (full tokenomics, sale page notes). Never loaded by the bot |

## Rules
- **Public content only.** No keys, `.env` values, private plans, or unreleased numbers.
  Anything here can be quoted to users by the bot.
- **One fact, one place.** Tokenomics live only in `tokenomics.md`; addresses only in
  `contracts.md`. Other files link to them instead of repeating numbers.
- When a protocol changes, update its folder here in the same week.

See `CLAUDE.md` for maintenance and bot-loading instructions.
