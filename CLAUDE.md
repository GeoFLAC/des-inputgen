# CLAUDE.md

Operating notes for Claude Code in this repo. For what the project is and how
to use it, see `README.md` — this file only covers things specific to how an
AI agent should work here, and shouldn't duplicate README content.

## What this repo is

A static web form (`index.html` + `parameters.js`, no build step, no
dependencies) that generates DES3D config files. `parameters.js` mirrors
`declare_parameters()` in DynEarthSol's `input.cxx` and must be kept in sync
with it by hand.

## Before touching `parameters.js`

Read "Syncing `parameters.js` with DynEarthSol" in `README.md` first — it has
the full verification procedure. The short version, since it's easy to get
wrong:

- `.github/workflows/check-input-cxx.yml` opens an issue with a cited commit
  hash whenever `input.cxx` changes upstream. **That hash is not reliable on
  its own** — it has pointed at an unrelated commit before. Always diff the
  live `input.cxx` against `parameters.js` directly rather than trusting the
  cited commit.
- When grepping `input.cxx` for option names, a few matches are false
  positives, not real gaps: default-value strings that look like
  `section.name` (e.g. filenames), and `po::value(...)` lines that are
  commented out.
- After any parameters.js change, update the sync banner near the top of
  `index.html` (the DynEarthSol PR + merge date) — it's a separate manual
  step, not automatic.

## Conventions established in this repo

- Push directly to `main`; no PR workflow has been requested for this repo.
- Use a `Closes #N` trailer in the commit message — GitHub auto-closes the
  issue on push, and a follow-up `gh issue comment` explaining what was
  found/changed is still worth posting since the auto-close has no body.
- `gh` is available for issue/PR operations; check `gh auth status` if
  commands fail with an auth error.
