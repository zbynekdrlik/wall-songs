# wall-songs — Project Instructions

## What this project is
wall-songs makes the LED wall visuals for the live band during songs on the SNV **songs PC** (a separate Windows computer, today running its own Resolume, "resolume songs").

Scope (owner, 21.11.2026): visuals on the LED wall during songs, with transitions, reactions to audio and tempo, text effects and the song lyrics.

Vision (owner, 24.11.2026, zbynekdrlik/wall-songs#1): a state-of-the-art, **AI-first** solution optimised for our goal: high-quality dynamic visuals tied to the song and its dynamics, which ANY operator can run without special skills. Resolume has a million manual features nobody can learn, and its results are poor against what we want.

## What it is NOT (owner corrections, 21.11. and 24.11.2026)
- Not another Resolume and not a feature-for-feature replacement of it: no decks / layers / clips / parameter panels, no migration of the old composition. Never frame a design question as "which Resolume mode first".
- Output is NDI streams to resolume bridge (bridge PC), which drives the LED wall. Spout is used only on the bridge PC.
- Not songplayer. songplayer is only a CG player of YouTube videos.
- Not the other Resolume ("resolume bridge") on the SNV bridge PC, which wall-bridge may replace later. Sermon visuals stay on that other Resolume.
- wall-bridge is the sibling LED-wall project; the two stay separate projects.

## Stack

House stack (`~/.claude/rules/house-stack.md`, zbynekdrlik/airuleset#1333): read it before choosing any technology. Another technology only with an owner-approved `<!-- airuleset:stack-exception <what> — <owner ref> -->` here, one per technology.

| Layer | Applies when | Technology |
|---|---|---|
| Workspace | every app | the current row of `~/.claude/rules/house-stack.md` |
| Service | an app that runs as a service or serves a UI / API (not a CLI or library) | the current row of `~/.claude/rules/house-stack.md` |
| Web UI | an app with a UI | the current row of `~/.claude/rules/house-stack.md` |
| Tray | a desktop app (Windows or Linux) | the current row of `~/.claude/rules/house-stack.md` |
| Graphics engine | a Windows app that renders video | the current row of `~/.claude/rules/house-stack.md` |
| Windows build | a Windows app | the current row of `~/.claude/rules/house-stack.md` |
| Install | a Windows desktop app with a UI or video | the current row of `~/.claude/rules/house-stack.md` |

wall-songs: EVERY row applies (a Windows desktop app with a UI that renders video for the LED wall). Owner 21.11.2026: "musi to byt podobny projekt ako ine nase rust projekty, web rozhranie, ikonka dole v tray, vykony nizkolatencny graficky engine", and the stack "musi byt stale otvoreny aby sa rozvijal k lepsim verziam": a clearly better option for a layer goes through the rule's Stack evolution section (proposal with evidence, the owner decides), never a silent switch and never a silent weaker choice. Use each row's CURRENT version from the rule, never a reference project's older pin.

## Open at project start
- The songs PC itself (address, Resolume version, outputs, inputs for audio/tempo) is not recorded anywhere yet. Find it out with the owner; box access goes through remoteos.
- The product design (how lyrics and tempo arrive, how the operator drives it, which effects first) is this project's first ticket, worked with the owner, INSIDE the stack above.
- The owner calls it an MVP for now: keep the first version small, but on the house stack from line one (MVP = fewer features, never a throwaway technology).

## Branches
Two-branch workflow: `dev` for work, `main` for releases, PR dev → main.

## Playbook router
- (empty: add `.claude/rules/<area>.md` files as areas appear)
