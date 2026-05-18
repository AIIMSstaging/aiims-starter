# AIIMS Project Starter — `.claude/` folder

Drop these files into the root of any AIIMS client repo to give Claude Code the AIIMS web-build standard out of the box.

## What's in here

```
your-project/
├── CLAUDE.md                ← project facts & rules — FILL THE PLACEHOLDERS
├── .gitignore               ← blocks secrets, env files, local-only configs
└── .claude/
    ├── settings.json        ← team-shared permissions (committed to git)
    └── skills/
        └── aiims-web-build/  ← the AIIMS web-build workflow skill
```

## How to use it

1. Copy `CLAUDE.md`, `.gitignore`, and the `.claude/` folder into the client repo root.
2. **Open `CLAUDE.md` and fill every `[BRACKETED]` placeholder.** This is the step that matters — the skill handles *workflow*, CLAUDE.md handles *this client's facts* (stack, hosting, brand colors, tracking IDs).
3. Commit all three. The whole team now builds the same way on this repo.
4. Restart Claude Code so it loads the skill, then verify with `/skills`.

## CLAUDE.md vs settings.json — the split

- **CLAUDE.md** = what Claude should *know and do* — project context, brand, conventions, rules. Plain English.
- **settings.json** = what Claude is *allowed to do* — tool permissions. JSON config.
- **The `aiims-web-build` skill** = *how* AIIMS builds websites — the repeatable workflow. Same on every project.

Rule of thumb: a *rule* goes in CLAUDE.md; a *permission/config* goes in settings.json.

## settings.json — what it does

- **allow:** read/write/edit, npm/npx/node, php, and safe git commands run without prompting.
- **ask:** `git push`, `vercel` deploys, and `npm publish` pause for your approval — these touch the outside world.
- **deny:** reading `.env`/secrets and destructive commands (`rm -rf`, force-push, `curl`/`wget`) are blocked outright.

Adjust per project if needed. Personal tweaks go in `.claude/settings.local.json` (gitignored, never committed) — not in this file.

## Local / personal files (never committed — already in .gitignore)

- `.claude/settings.local.json` — your personal permission overrides.
- `CLAUDE.local.md` — your personal notes for this project.

## Updating the skill

When the `aiims-web-build` skill improves, replace the `.claude/skills/aiims-web-build/` folder and commit. Every project that pulls gets the update. Later, if you bundle AIIMS's skills into a plugin, this per-repo copy can be retired in favour of a single plugin install.
